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
scrape_configs:
# The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'
# metrics_path defaults to '/metrics'
# scheme defaults to 'http'.
    static_configs:
    - targets: ['localhost:9090']
  - job_name: 'spring-actuator'
    metrics_path: '/actuator/prometheus'
    scrape_interval: 5s
    static_configs:
    - targets: ['159.75.79.151:8080'] #需要监控的应用节点
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

## 安装Grafana

~~~shell
docker run -d --name grafana  -p 3000:3000 -v /usr/local/docker/grafana/grafana.ini:/etc/grafana/grafana.ini grafana/grafana grafana
~~~

查看密码

~~~shell
docker exec -it grafana /bin/bash cat /etc/grafana/grafana.ini > grafana.ini
~~~

## Grafana面板配置

菜单选择 Configuration -> Data Source -> Add Data Source 配置Prometheus作为数据源下载别人配置好的面板直接导入 Grafana的面板配置过程还是比较繁琐的，如果我们不想自己去配置，那我们可以去Grafana官网上去 下载一个dashboard。 

推荐： https://grafana.com/grafana/dashboards/6756 下载完成后，在"+"这个菜单中，点击"import"，导入下载好的json文件即可。 

根据ID进行load 模板地址：https://grafana.com/dashboards 在搜索框中搜索 Spring Boot 会检索出相关的模板，选择一个自己喜欢。 这里可以采用: https://grafana.com/grafana/dashboards/10280 这个，看起来比较清晰 复制下图所示的dashboard的ID号



