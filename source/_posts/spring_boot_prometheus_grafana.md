

Spring Boot 支持 prometheus 监控：文档地址-> [这儿](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-metrics-export-prometheus)



## 原理

spring-boot-starter-actuator 组件支持生成符合  prometheus 数据格式的 metric



## 安装

### build.gradle

```bash
# build.gradle

implementation 'org.springframework.boot:spring-boot-starter-actuator'
implementation 'io.micrometer:micrometer-registry-prometheus'
```



### 修改Spring配置文件

修改Spring 配置文件，使 Spring 项目暴露 metric 接口
https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-endpoints

```bash
# application.yml
management:
  endpoints:
    web:
      exposure:
        include:  '*'
```

## 集成prometheus



```bash
# 修改prometheus 配置文件，收集Spring metric
vim /usr/local/etc/prometheus.yml
```

```bash
# 将以下SpringBoot应用配置加入prometheus.yml 尾部

  - job_name: 'springBootPrometheus'
    scrape_interval: 5s
    metrics_path: '/actuator/prometheus'
    static_configs:
    - targets: ['127.0.0.1:6666']
```

```bash
#重启 prometheus                
brew services restart prometheus
```

此时打开 http://localhost:9090/targets 可以看到 springBootPrometheus

![image-20201216102113830](/Users/spaco/Library/Application Support/typora-user-images/image-20201216102113830.png)



## 集成Grafana

prometheus 的可视化功能不如 Grafana 强大，所以我们可以集成 Grafana 可视化功能

可以通过 https://grafana.com/grafana/dashboards 搜索你需要的可视化 dashboards

这里我们使用  [JVM (Micrometer)](https://grafana.com/grafana/dashboards/4701) 和 [Spring Boot Statistics](https://grafana.com/grafana/dashboards/6756)

### JVM (Micrometer)

JVM 相关信息可视化

#### 获取模版id

[JVM (Micrometer)](https://grafana.com/grafana/dashboards/4701) 

![image-20201216103346037](/Users/spaco/Library/Application Support/typora-user-images/image-20201216103346037.png)

模版id: 4701

#### import dashbord

![image-20201216103511332](/Users/spaco/Library/Application Support/typora-user-images/image-20201216103511332.png)

![image-20201216103542115](/Users/spaco/Library/Application Support/typora-user-images/image-20201216103542115.png)



#### 设置 dashbord 数据源 

![image-20201216103634959](/Users/spaco/Library/Application Support/typora-user-images/image-20201216103634959.png)

点击 Import 按钮, 会跳转到 JVM 数据页面

![image-20201216103825240](/Users/spaco/Library/Application Support/typora-user-images/image-20201216103825240.png)



### *Spring Boot Statistics*

展示Spring Boot 项目的相关信息

#### 获取模版id

 [Spring Boot Statistics](https://grafana.com/grafana/dashboards/6756)

模版id: 6756

![image-20201216103954627](/Users/spaco/Library/Application Support/typora-user-images/image-20201216103954627.png)

#### import dashbord

同上

####设置 dashbord 数据源  

同上

会跳转到如下页面

