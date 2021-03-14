# 注册中心

支持的配置中心，可以配置多注册中心

* consul
* zookeeper
* eureka
* redis
* etcd
* nacos
* ....

## 服务端

### 配置文件 application.properties

~~~properties
#注册中心1
dubbo.registries.tiger_zk.address=zookeeper://49.234.55.50:2181
dubbo.registries.tiger_zk.timeout=10000
## 服务启动的时候，如果注册中心有问题，配置是否启动失败
dubbo.registries.tiger_zk.check=false

#注册中心2
dubbo.registries.tiger_nacos.address=nacos://49.234.55.50:8848

# 不指定情况下，默认的注册中心【tiger_nacos】
dubbo.registries.tiger_nacos.default=true
~~~

### 代码示例，HelloWorldMultiRegistryServiceImpl.java

~~~java
/**
 * 1、支持多个注册中心【tiger_nacos,tiger_zk】,在配置文件中自定义
 */
@DubboService(registry = {"tiger_nacos", "tiger_zk"})
public class HelloWorldMultiRegistryServiceImpl implements HelloWorldService {

    @Override
    public String hello(String msg) {
        String ret = "hello:" + msg;
        System.out.println(ret);
        return ret;
    }
}
~~~

## 消费端

### 配置文件  application.properties

~~~properties
#注册中心1
dubbo.registries.tiger_zk.address=zookeeper://49.234.55.50:2181
dubbo.registries.tiger_zk.timeout=10000
dubbo.registries.tiger_zk.zone=shanghai
dubbo.registries.tiger_zk.weight=100

#注册中心2
dubbo.registries.tiger_nacos.address=nacos://49.234.55.50:8848
dubbo.registries.tiger_nacos.weight=10
dubbo.registries.tiger_nacos.preferred=true
~~~

### 代码示例  HelloWorldController.java

~~~java
// ...
@RestController
public class HelloWorldController {

    @DubboReference( registry = {"tiger_nacos","tiger_zk"})
    HelloWorldService helloWorldService;

    // ...
}
~~~

# 负载均衡

在消费端的controller层控制相关参数

1. random，默认加权随机，根据权重生成区间

   ~~~java
   // ...
   @RestController
   public class HelloWorldController {
   
       @DubboReference(loadbalance = "random")
       HelloWorldService helloWorldService;
   
       // ...
   }
   ~~~

2. 轮询

   ~~~java
   // ...
   @RestController
   public class HelloWorldController {
   
       @DubboReference(loadbalance = "roundrobin")
       HelloWorldService helloWorldService;
   
       // ...
   }
   ~~~

3. 一致性hash

   ~~~java
   // ...
   @RestController
   public class HelloWorldController {
   
       @DubboReference(loadbalance = "consistenthash")
       HelloWorldService helloWorldService;
   
       // ...
   }
   ~~~

4. 最小活跃度，根据目标集群服务列表，处理性能最高的权重越大，反之亦然。

   ~~~java
   // ...
   @RestController
   public class HelloWorldController {
   
       @DubboReference(loadbalance = "leastactive")
       HelloWorldService helloWorldService;
   
       // ...
   }
   ~~~

5. …

# 集群容错

容忍错误的能力，客户端发起一次请求，因为网络等各种原因出错了，怎么办？

1. 失败自动切换重试【failover】,默认重试【retries】2次，重试其他服务器，对于事务请求，服务端需要做幂等操作（对于客户端发起n次请求，结果都是一样）

   ~~~java
   // ...
   @DubboService(cluster = "failover", retries = 2)
   public class HelloWorldMultiRegistryServiceImpl implements HelloWorldService {
       
       // ...
   }
   ~~~

2. 快速失败

   ~~~java
   // ...
   @DubboService(cluster = "failfast")
   public class HelloWorldMultiRegistryServiceImpl implements HelloWorldService {
       
       // ...
   }
   ~~~

3. 失败安全，出现异常，不做任何处理，直接吞掉，例如日志操作

   ~~~java
   // ...
   @DubboService(cluster = "failsafe")
   public class HelloWorldMultiRegistryServiceImpl implements HelloWorldService {
       
       // ...
   }
   ~~~

   

4. 失败自动恢复，记录失败请求，定时重发

   ~~~java
   // ...
   @DubboService(cluster = "failback")
   public class HelloWorldMultiRegistryServiceImpl implements HelloWorldService {
       
       // ...
   }
   ~~~

5. 并行调用，并行调用多个节点，只要一个成功返回，就直接返回结果

   ~~~java
   // ...
   @DubboService(cluster = "forking")
   public class HelloWorldMultiRegistryServiceImpl implements HelloWorldService {
       
       // ...
   }
   ~~~

6. 广播调用，请求会调用所有服务提供者，只要一台报错，请求就失败

   ~~~java
   // ...
   @DubboService(cluster = "broadcast")
   public class HelloWorldMultiRegistryServiceImpl implements HelloWorldService {
       
       // ...
   }
   ~~~

7. …

# 泛化

没有接口的契约，跨平台语言调用

## 消费端

~~~java
// ...
@RestController
public class GeneralizationController {

    @DubboReference(interfaceName = "com.tiger.springboot.dubbo.demo.provider.services.GeneralizationService",
            generic = true
    )
    GenericService genericService;

    @GetMapping("/generalization")
    public String generalization() {
        return genericService.$invoke("getName",new String[0],null).toString();
    }
}
~~~

# 服务降级

## 消费端

~~~java

@RestController
public class HelloWorldController {

    @DubboReference(
            mock = "com.tiger.springboot.dubbo.demo.consumer.services.impl.MockHelloWorldServiceImpl",
            timeout = 500
    )
    HelloWorldService helloWorldService;

    @GetMapping("/say")
    public String say() {
        System.out.println("=== say ===");
        return helloWorldService.hello("老虎");
    }
}
~~~

mock 接口实现

~~~java
// ...
public class MockHelloWorldServiceImpl implements HelloWorldService {

    @Override
    public String hello(String msg) {
        // ...
        return "hello -> 触发服务降级";
    }
}
~~~

# 启动时检查

服务之间的相互调用。避免陷入死循环

~~~properties
# 单注册中心
dubbo.registry.address=nacos://49.234.55.50:8848
dubbo.registry.check=false
~~~

~~~java
// ...
@RestController
public class HelloWorldController {

    @DubboReference( check = false )
    HelloWorldService helloWorldService;

    @GetMapping("/say")
    public String say() {
       
        return helloWorldService.hello("老虎");
    }
}
~~~

# 配置优先级

## @DubboReference 与@DubboService 优先级

1. 客户端  > 服务端 > 
2. 方法层面  > 接口层面 > 全局

## 配置信息优先级

系统启动参数(System.Properties) > 外部环境参数(配置中心…) > Spring/API > 本地配置文件

# 多序列化

