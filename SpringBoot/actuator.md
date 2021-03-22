# 应用场景

  微服务应用开发完成以后，最终目的是为了发布到生产环境上给用户试用，开发结束并不意味着研发的生命周期结束，更多的时候他只是一个开始，因为服务在本地测试完成以后，并不一定能够非常完善的考虑到各种场景。所以需要通过运维来保障服务的稳定。

## 引入 actuator starter包

~~~xml
        <!-- actuator 监控依赖包-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
~~~

## 开启所有监控信息

~~~properties

# 默认只开放[health,info]，如果需要开放所有，则配置*
management.endpoints.web.exposure.include=*
 
management.endpoints.jmx.exposure.include=*
spring.jmx.enabled=true

management.endpoint.health.show-details=always

info.app.name=@project.name@

~~~



## 启动项目

[Endpoint]: https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-endpoints

访问：http://localhost:8080/actuator

# SpringBoot的信息 可以发布到 Prometheus+Grafana

## docker安装Prometheus

创建挂载配置文件，并授权

~~~shell
mkdir -p /usr/local/docker/prometheus/prometheus.yml
chmod 777 -R /usr/local/docker/prometheus
~~~

配置文件

~~~yaml
global:
  scrape_interval:     60s
  evaluation_interval: 60s
 
scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ['localhost:9090']
        labels:
          instance: prometheus
~~~

启动

~~~shell
docker run  -d \
  -p 9090:9090 \
  -v /usr/local/docker/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml \
  -v /usr/local/docker/prometheus/data:/prometheus \
  prom/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.retention.time=100d
~~~







