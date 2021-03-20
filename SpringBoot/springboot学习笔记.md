# 前世今生

了解其技术的演进过程，一步一步进行优化，使得code变得更加简单

1. spring framework APO、IOC/DI

   spring之前是在代码中直接new，springboot之后，对象由IOC容器管理。

2. spring可集成任何东西，万能胶

3. 当项目很大时，需要维护配置很多xml，造成文件配置重量级，如何对配置进行轻量化，由此引出springboot，约定优于配置。

4. 需要一个脚手架来实现项目的自动化构建（springboot）

5. …

# 特性

1. EnableAutoConfiguration 自动装配
2. Start启动，依赖于自动装配技术
3. Actuator 监控 , 提供了一些endpoint ，http、jmx形式去进行访问， health信息。 metrics 信 息
4. Spring Boot CLI（命令行操作的功能， groovy脚本） 客户端, groovy
5. …

# 注解驱动的发展过程（Spring Framework）

一代一代升级，在前面基础之上不断创新，尽可能减少重复性工作，使得开发变得更加简洁，能够有更多时间关注业务逻辑，核心：怎么样简单快速构建项目，如何简单将对象交由IOC进行管理

## Spring 1.x阶段

在SpringFramework1.x时代，其中在1.2.0是这个时代的分水岭，当时Java5刚刚发布，业界正兴起了使 用Annotation的技术风，Spring Framework自然也提供了支持，比如当时已经支持了@Transactional 等注解，但是这个时候，XML配置方式还是唯一选择

~~~xml
<bean name="" class=""/>
~~~

## Spring 2.x阶段

Spring Framework2.x时代，2.0版本在Annotation中添加了@Required、@Repository以及AOP相关 的@Aspect等注解，同时也提升了XML配置能力，也就是可扩展的XML，比如Dubbo这样的开源框架就 是基于Spring XML的扩展来完美的集成Spring，从而降低了Dubbo使用的门槛。在2.x时代，2.5版本也是这个时代的分水岭， 它引入了一些很核心的Annotation

* Autowired 依赖注入 
* @Qualifier 依赖查找 
* @Component、@Service 组件声明 
* @Controller、@RequestMappring等spring mvc的注解

尽管Spring 2.x时代提供了不少的注解，但是仍然没有脱离XML配置驱动，比如context:annotation-co nfig context:componet-scan , 前者的职责是注册Annotation处理器，后者是负责扫描classpath下指定 包路径下被Spring模式注解标注的类，将他们注册成为Spring Bean 

## Spring 3.x阶段

Spring Framework3.0是一个里程碑式的时代，他的功能特性开始出现了非常大的扩展，比如全面拥抱 Java5、以及Spring Annotation。更重要的是，它提供了配置类注解@Configuration， 他出现的首要任务就是取代XML配置方式，无配置化的方式实现Bean的装配

* @Configuration 去xml化

  > 核心目的是：把bean对象如何更加便捷的方式去加载到Spring IOC容器中

* @ComponentScan

* @Import，导入另外一个模块下的配置类

* …

## Enable模块驱动

为了便于集成第三方jar包

* 创建一个配置类 @Configuration

* @bean注解来声明一个bean，或者通过@Service等方式扫描成bean

  ~~~java
  @Bean
  DefaultKaptcha defaultKaptcha(){
  }
  ~~~

* @EnableXXX

## Spring 4.x阶段

@Conditional，条件化配置，控制类在满足什么样的条件下才需要装载到IOC容器中

# Spring 5.x阶段

@Indexed，性能优化，



