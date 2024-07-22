 

>  **导航：**
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})

[TOC]



# 1.初识Sentinel

## 1.1.雪崩问题及解决方案

### 1.1.1.雪崩问题

微服务中，服务间调用关系错综复杂，一个微服务往往依赖于多个其它微服务。

![1533829099748](SpringCloud基础5——微服务保护、Sentinel.assets/946e07359958dd27c51efab67d0a7515.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如图，如果服务提供者I发生了故障，当前的应用的部分业务因为依赖于服务I，因此也会被阻塞。此时，其它不依赖于服务I的业务似乎不受影响。

![1533829198240](SpringCloud基础5——微服务保护、Sentinel.assets/8ec93cf95b1ef34aba20edc23cf5c508.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

但是，依赖服务I的业务请求被阻塞，用户不会得到响应，则tomcat的这个线程不会释放，于是越来越多的用户请求到来，越来越多的线程会阻塞：

![1533829307389](SpringCloud基础5——微服务保护、Sentinel.assets/b05b1495462bbfd5953e50d8e73ba037.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**服务器支持的线程和并发数有限，请求一直阻塞，会导致服务器资源耗尽，从而导致所有其它服务都不可用**，那么当前服务也就不可用了。

那么，依赖于当前服务的其它服务随着时间的推移，最终也**都会变的不可用**，形成级联失败，雪崩就发生了：

![image-20210715172710340](SpringCloud基础5——微服务保护、Sentinel.assets/a285717c2c730c569ce3550a5344ce63.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**解决办法：**超时处理、线程隔离、降级熔断。

**预防办法：**流量控制 

### 1.1.2.方案1：超时处理

解决雪崩问题的常见方式有四种：

**•超时处理：**设定超时时间，**请求超过一定时间没有响应就返回错误信息**，不会无休止等待

![image-20210715172820438](SpringCloud基础5——微服务保护、Sentinel.assets/fdca0e1bebf97859469da89c3981a5b5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.1.3.方案2：仓壁模式/线程隔离



仓壁模式来源于船舱的设计：

![image-20210715172946352](SpringCloud基础5——微服务保护、Sentinel.assets/e08f534cc6aad20690f32260ef0c0e04.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

船舱都会被隔板分离为多个独立空间，当船体破损时，只会导致部分空间进入，将故障控制在一定范围内，避免整个船体都被淹没。

于此类似，我们可以**限定每个业务能使用的线程数**，避免耗尽整个tomcat的资源，因此**也叫线程隔离。**

![image-20210715173215243](SpringCloud基础5——微服务保护、Sentinel.assets/1c9bdb1f7e4148986504156f8529eafc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.1.4.方案3：断路器

**断路器模式：**由**断路器**统计业务执行的**异常比例**，如果**超出阈值则会熔断该业务**，**拦截**访问**该业务**的**一切请求**。

断路器会统计访问某个服务的请求数量，异常比例：

![image-20210715173327075](SpringCloud基础5——微服务保护、Sentinel.assets/804285d25b65f1852560ae540245fad1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

当发现访问服务D的请求**异常比例**过高时，认为服务D有导致雪崩的风险，会拦截访问服务D的一切请求，形成熔断：

![image-20210715173428073](SpringCloud基础5——微服务保护、Sentinel.assets/283128b63b954bd520df170feb781376.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.1.5.方案4（预防）：限流

**流量控制**：**限制**业务访问的**QPS（**Queries-per-second**每秒查询的数量）**，**避免瞬间高并发的流量**导致服务故障。



前面方案都是出现雪崩风险后采取措施，限流方案是预防雪崩。 

这里就用到**sentinel（译为哨兵、守卫）**了， 它可以**按照目标服务能承受的频率释放请求**。

![image-20210715173555158](SpringCloud基础5——微服务保护、Sentinel.assets/355a0582878f4ffaa4405ad9bffe68ed.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.1.6.总结，雪崩问题

**什么是雪崩问题？**

- 微服务之间相互调用，因为调用链中的一个服务故障，引起整个链路都无法访问的情况。

可以认为：

**限流**是对服务的保护，避免因瞬间高并发流量而导致服务故障，进而避免雪崩。是一种**预防**措施。

**超时处理、线程隔离、降级熔断**是在部分服务故障时，将故障控制在一定范围，避免雪崩。是一种**补救**措施。

## 1.2.服务保护技术对比

在SpringCloud当中支持多种服务保护技术：

- [Netfix Hystrix](https://github.com/Netflix/Hystrix)
- [Sentinel](https://github.com/alibaba/Sentinel)
- [Resilience4J](https://github.com/resilience4j/resilience4j)

早期比较流行的是Hystrix框架，但目前国内使用**最广泛的还是阿里巴巴的Sentinel框架**，这里我们做下对比：

|                | **Sentinel**                                   | **Hystrix**                   |
| -------------- | ---------------------------------------------- | ----------------------------- |
| 隔离策略       | 信号量隔离                                     | 线程池隔离/信号量隔离         |
| 熔断降级策略   | 基于慢调用比例或异常比例                       | 基于失败比率                  |
| 实时指标实现   | 滑动窗口                                       | 滑动窗口（基于 RxJava）       |
| 规则配置       | 支持多种数据源                                 | 支持多种数据源                |
| 扩展性         | 多个扩展点                                     | 插件的形式                    |
| 基于注解的支持 | 支持                                           | 支持                          |
| 限流           | 基于 QPS，支持基于调用关系的限流               | 有限的支持                    |
| 流量整形       | 支持慢启动、匀速排队模式                       | 不支持                        |
| 系统自适应保护 | 支持                                           | 不支持                        |
| 控制台         | 开箱即用，可配置规则、查看秒级监控、机器发现等 | 不完善                        |
| 常见框架的适配 | Servlet、Spring Cloud、Dubbo、gRPC 等          | Servlet、Spring Cloud Netflix |

> **线程池隔离：**当前业务给每个被隔离的业务都创建一个独立的线程池。优点隔离性好，缺点线程数量成倍增长，cpu压力增大。
>
> **信号隔离：**限制每个业务能使用线程的数量，超过限制不再创建新线程。**比线程池隔离更好**，优点是不影响性能，缺点是隔离性稍差于线程池隔离，因为所有业务在一个池子里，而线程池每个业务有独立的线程池。

## 1.3.Sentinel介绍和安装

### 1.3.1.初识Sentinel

Sentinel是阿里巴巴开源的一款微服务流量控制组件。官网地址：https://sentinelguard.io/zh-cn/index.html

Sentinel 具有以下特征:

•**丰富的应用场景**：Sentinel 承接了阿里巴巴近 10 年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等。

•**完备的实时监控**：Sentinel 同时提供实时的监控功能。您可以在控制台中看到接入应用的单台机器秒级数据，甚至 500 台以下规模的集群的汇总运行情况。

•**广泛的开源生态**：Sentinel 提供开箱即用的与其它开源框架/库的整合模块，例如与 Spring Cloud、Dubbo、gRPC 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。

•**完善的** **SPI** **扩展点**：Sentinel 提供简单易用、完善的 SPI 扩展接口。您可以通过实现扩展接口来快速地定制逻辑。例如定制规则管理、适配动态数据源等。

### 1.3.2.安装Sentinel

**1）下载**

sentinel官方提供了UI控制台，方便我们对系统做限流设置。大家可以在[GitHub](https://github.com/alibaba/Sentinel/releases)下载。

课前资料也提供了下载好的jar包：

![image-20210715174252531](SpringCloud基础5——微服务保护、Sentinel.assets/2f6efacfe4872ddf6205d1d6ece6c109.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）运行**

将jar包放到任意**非中文目录**，在地址栏cmd回车打开命令行，执行下面命令：

```
java -jar sentinel-dashboard-1.8.1.jar
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如果要修改Sentinel的默认端口、账户、密码，可以通过下列配置：

| **配置项**                       | **默认值** | **说明**   |
| -------------------------------- | ---------- | ---------- |
| server.port                      | 8080       | 服务端口   |
| sentinel.dashboard.auth.username | sentinel   | 默认用户名 |
| sentinel.dashboard.auth.password | sentinel   | 默认密码   |

例如，如果想要**修改端口：**

```
java -Dserver.port=8090 -jar sentinel-dashboard-1.8.1.jar
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3）访问**

访问**http://localhost:8080**页面，就可以看到sentinel的控制台了：

![image-20210715190827846](SpringCloud基础5——微服务保护、Sentinel.assets/c1b3a4611644cad8c0e26ab5a86fff02.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

需要输入账号和密码，默认都是：sentinel

登录后，发现一片空白，什么都没有：

![img](SpringCloud基础5——微服务保护、Sentinel.assets/0f2413150f1f772b269d9aeb626921f3.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这是因为我们还没有与微服务整合。

## 1.4.微服务整合Sentinel

我们在cloud-demo的**order-service**中整合sentinel，并连接sentinel的控制台，步骤如下：

>  cloud-demo是学网关、feign、微服务、nacos等时候的学习项目
>
> yml：
>
> ```bash
> server:
>   port: 8080
> spring:
>   cloud:
>     nacos:
>       discovery:
>         server-addr: nacos:8848
>         cluster-name: HZ
>   application:
>     name: order-service
>   datasource:
>     url: jdbc:mysql://mysql:3306/cloud_order?useSSL=false
>     username: root
>     password: 1234
>     driver-class-name: com.mysql.jdbc.Driver
> mybatis:
>   type-aliases-package: cn.itcast.user.pojo
>   configuration:
>     map-underscore-to-camel-case: true
> logging:
>   level:
>     cn.itcast: debug
>   pattern:
>     dateformat: MM-dd HH:mm:ss:SSS
> #eureka:
> #  client:
> #    service-url:
> #      defaultZone: http://127.0.0.1:10086/eureka
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 使用前先打开nacos服务器：
>
> 双击bin目录下
>
> ```bash
> startup.cmd -m standalone
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**1）在order-service引入sentinel依赖**

```XML
<!--sentinel-->
<dependency>
    <groupId>com.alibaba.cloud</groupId> 
    <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）配置控制台**

修改application.yaml文件，添加下面内容：

```bash
server:
  port: 8088
spring:
  cloud: 
    sentinel:
      transport:
        dashboard: localhost:8080    #译为控制面板、仪表盘
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3）重启服务后访问order-service的任意端点**

打开浏览器，访问http://localhost:8088/order/101，这样才能触发sentinel的监控。

然后再访问sentinel的控制台，查看效果：

![image-20210715191241799](SpringCloud基础5——微服务保护、Sentinel.assets/c96415883ed65079fa81c6389d78a2a8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - **如果刷新后实时监控无数据，那就是你的 http://localhost:8088/order/101是假刷新，ctrl+f5清理缓存刷新就好了**

# 2.流量控制

雪崩问题虽然有四种方案，但是限流是避免服务因突发的流量而发生故障，是对微服务雪崩问题的预防。我们先学习这种模式。

## 2.1.簇点链路

当请求进入微服务时，首先会访问DispatcherServlet，然后进入Controller、Service、Mapper，这样的一个调用链就叫做**簇点链路**。簇点链路中**被监控的每一个接口**就是一个**资源**。

**默认**情况下sentinel会**监控**SpringMVC的**每一个端点**（Endpoint，也就是**controller中的方法**），因此SpringMVC的**每一个端点**（Endpoint）**就是调用链路中的一个资源**。

例如，我们刚才访问的order-service中的OrderController中的端点：/order/{orderId}

![image-20210715191757319](SpringCloud基础5——微服务保护、Sentinel.assets/44cdd4d7d50014f4b0e6e024c23dbe21.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**流控、熔断等都是针对簇点链路中的资源来设置的**，因此我们可以点击对应资源后面的按钮来设置规则：

- **流控：**流量控制
- **降级：**降级熔断
- **热点：**热点参数限流，是限流的一种
- **授权：**请求的权限控制

## 2.1.流量控制示例（直接模式）

### 2.1.1.示例

点击资源/order/{orderId}后面的流控按钮，就可以弹出表单。

![image-20210715191757319](SpringCloud基础5——微服务保护、Sentinel.assets/44cdd4d7d50014f4b0e6e024c23dbe21.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

表单中可以填写限流规则，如下：

![image-20210715192010657](SpringCloud基础5——微服务保护、Sentinel.assets/37585958b4e6b50082804862dba4f4c0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

单机阈值为QPS类型的1，含义是限制 /order/{orderId}这个资源的单机**QPS(queries per second)为1**，即**每秒只允许1次请求**，超出的请求会被拦截并报错。

### 2.1.2.**jmeter压力测试**

需求：给 /order/{orderId}这个资源设置流控规则，QPS不能超过 5，然后测试。

**1）首先在sentinel控制台添加限流规则**

![image-20210715192455429](SpringCloud基础5——微服务保护、Sentinel.assets/ada9fb8a6e72f372f97b61c968a4a110.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）利用jmeter测试**

如果没有用过jmeter，可以参考课前资料提供的文档《Jmeter快速入门.md》

课前资料提供了编写好的Jmeter测试样例：

![image-20210715200431615](SpringCloud基础5——微服务保护、Sentinel.assets/1ee1e169f84b64663f4214f644467b6a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

打开jmeter，导入课前资料提供的测试样例：

![image-20210715200537171](SpringCloud基础5——微服务保护、Sentinel.assets/a5fda0a512c46d76d778b68cfd31ca10.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

选择：

![image-20210715200635414](SpringCloud基础5——微服务保护、Sentinel.assets/25ec63f87e90bfaad579e66828100040.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**20个用户，2秒内运行完**，QPS是10，超过了5.

选中`流控入门，QPS<5`右键运行：

![image-20210715200804594](SpringCloud基础5——微服务保护、Sentinel.assets/50f582e389113a6c8bd2822c639079c8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意，**不要点击菜单中的执行按钮来运行。

**结果：****成功的请求每次只有5个，而QPS值正好是5：**

![image-20210715200853671](SpringCloud基础5——微服务保护、Sentinel.assets/5911059dea5107f2c515b33ee1d6868a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 2.2.流控模式

在添加**限流规则**时，点击**高级选项**，可以选择**三种流控模式**：

- **直接（默认）：**统计当前资源的请求，**触发阈值**时对当前资源**直接限流**，也是**默认**的模式
- **关联：**统计与当前资源**相关的另一个资源，触发阈值**时，对**当前资源限流**
- **链路：**统计从指定链路访问到本资源的请求，触发阈值时，对**指定链路限流。**例如a、b访问资源c，只对指定的a到c的请求链路限流，b到c没指定就不管。

![img](SpringCloud基础5——微服务保护、Sentinel.assets/c958fee4fb9949a984a9e45441982b7e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![image-20210715201827886](SpringCloud基础5——微服务保护、Sentinel.assets/7c75168f5354acda2313ba74559cd9c5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.1流量控制测试的就是直接模式。

### 2.2.1.关联模式

**关联模式**：统计与当前资源相关的另一个资源，触发阈值时，对当前资源限流

**配置规则**：

![image-20210715202540786](SpringCloud基础5——微服务保护、Sentinel.assets/78b3986ac2b389d954dae658c27b687e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**语法说明**：当/write资源访问量触发阈值时，就会对/read资源限流，避免影响/write资源。

**使用场景**：比如用户支付时需要修改订单状态，同时用户要查询订单。查询和修改操作会争抢数据库锁，产生竞争。业务需求是优先支付和更新订单的业务，因此当修改订单业务触发阈值时，需要对查询订单业务限流。

> **需求说明**：
>
> - 在OrderController新建两个端点：**/order/query和/order/update**，无需实现业务
> - 配置流控规则，当**/order/ update**资源被访问的**QPS超过5**时，**对/order/query请求限流**

**1）定义/order/query端点，模拟订单查询**

```java
@GetMapping("/query")
public String queryOrder() {
    return "查询订单成功";
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）定义/order/update端点，模拟订单更新**

```java
@GetMapping("/update")
public String updateOrder() {
    return "更新订单成功";
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**重启服务，查看sentinel控制台的簇点链路：**

![image-20210716101805951](SpringCloud基础5——微服务保护、Sentinel.assets/4ef86b4949e0276d6fb3ec0e68220950.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3）配置流控规则**

对哪个端点限流，就点击哪个端点后面的按钮。我们是对订单查询/order/query限流，因此点击它后面的按钮：

![image-20210716101934499](SpringCloud基础5——微服务保护、Sentinel.assets/97524bdf6b408ecaa6b54a988cb2061c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在表单中填写流控规则：

![image-20210716102103814](SpringCloud基础5——微服务保护、Sentinel.assets/30c65a9fe7d63e0caccfdf6b778f38d2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**4）在Jmeter测试**

选择《流控模式-关联》：

![image-20210716102416266](SpringCloud基础5——微服务保护、Sentinel.assets/574616b774b457ad17ed5c4f8f05f9ba.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

可以看到1000个用户，100秒，因此QPS为10，超过了我们设定的阈值：5

查看http请求：

![image-20210716102532554](SpringCloud基础5——微服务保护、Sentinel.assets/39e86ba7b0192cab3e1123a35d43f0ca.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**请求的目标是/order/update**，这样这个断点就会触发阈值。

**但限流的目标是/order/query****：**

![image-20210716102636030](SpringCloud基础5——微服务保护、Sentinel.assets/131548cddbccc5aae8c0fcad6ede30ab.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**5）总结**

![image-20210716103143002](SpringCloud基础5——微服务保护、Sentinel.assets/f51eaa6d966e763989331253f386e2df.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.2.链路模式，**@SentinelResource**

**链路模式**：只针对从指定链路访问到本资源的请求做统计，判断是否超过阈值。

**配置示例**：

例如有两条请求链路：

- /test1 --> /common
- /test2 --> /common

如果只希望统计从/test2进入到/common的请求，则可以这样配置：

![image-20210716103536346](SpringCloud基础5——微服务保护、Sentinel.assets/30581d0cef6a243d9dfab792204ae30c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**实战案例**

> **需求：**有查询订单和创建订单业务，两者都需要查询商品。针对从查询订单进入到查询商品的请求统计，并设置限流。

> **步骤：**
>
> 1. 在OrderService中添加一个queryGoods方法，不用实现业务
> 2. 在OrderController中，改造/order/query端点，调用OrderService中的queryGoods方法
> 3. 在OrderController中添加一个/order/save的端点，调用OrderService的queryGoods方法
> 4. 给queryGoods设置限流规则，从/order/query进入queryGoods的方法限制QPS必须小于2

**实现：**

**1）添加查询商品方法**

在order-service服务中，给OrderService类添加一个queryGoods方法：

```
public void queryGoods(){
    System.err.println("查询商品");
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）查询订单时，查询商品**

在order-service的OrderController中，修改/order/query端点的业务逻辑：

```java
@GetMapping("/query")
public String queryOrder() {
    // 查询商品
    orderService.queryGoods();
    // 查询订单
    System.out.println("查询订单");
    return "查询订单成功";
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3）新增订单，查询商品**

在order-service的OrderController中，修改/order/save端点，模拟新增订单：

```java
@GetMapping("/save")
public String saveOrder() {
    // 查询商品
    orderService.queryGoods();
    // 查询订单
    System.err.println("新增订单");
    return "新增订单成功";
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**4）给查询商品添加资源标记，并关闭对SpringMVC的资源聚合**

默认情况下，OrderService中的方法是不被Sentinel监控的，需要我们自己通过注解来标记要监控的方法。

给OrderService的queryGoods方法添加**@SentinelResource**注解：

```java
@SentinelResource("goods")
public void queryGoods(){
    System.err.println("查询商品");
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

链路模式中，是对不同来源的两个链路做监控。但是**sentinel默认会给进入SpringMVC的所有请求设置同一个root资源，会导致链路模式失效。**

我们需要**关闭这种对SpringMVC的资源聚合**，修改order-service服务的application.yml文件：

```bash
spring:
  cloud:
    sentinel:
      web-context-unify: false # 关闭context整合
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**重启服务**，访问/order/query和/order/save，可以查看到sentinel的簇点链路规则中，出现了**新的资源：**

![image-20210716105227163](SpringCloud基础5——微服务保护、Sentinel.assets/3298346474806793e22bf54e03478e81.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**5）添加流控规则**

点击goods资源后面的流控按钮，在弹出的表单中填写下面信息：

![image-20210716105408723](SpringCloud基础5——微服务保护、Sentinel.assets/768b4c2462522ca2d2cea4b008f883b8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

只统计从/order/query进入/goods的资源，QPS阈值为2，超出则被限流。

6）Jmeter测试

选择《流控模式-链路》：

![image-20210716105612312](SpringCloud基础5——微服务保护、Sentinel.assets/b2758a570e5a795f365beab2bd07c047.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

可以看到这里200个用户，50秒内发完，QPS为4，超过了我们设定的阈值2

一个http请求是访问/order/save：

![image-20210716105812789](SpringCloud基础5——微服务保护、Sentinel.assets/3319ee79aedd31fb368c3184ab7480b1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

运行的结果：

![image-20210716110027064](SpringCloud基础5——微服务保护、Sentinel.assets/b97e6cfb68b36d16ffdff7684138034f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

完全不受影响。

另一个是访问/order/query：

![image-20210716105855951](SpringCloud基础5——微服务保护、Sentinel.assets/bdd0d5d0a852d2ad4b945c0b6f266341.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

运行结果：

![image-20210716105956401](SpringCloud基础5——微服务保护、Sentinel.assets/c9ce589a75bb234fda4b12c6e59c5759.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

每次只有2个通过。

### 2.2.3.总结

流控模式有哪些？

•直接：对当前资源限流

•关联：高优先级资源触发阈值，对低优先级资源限流。

•链路：阈值统计时，只统计从指定资源进入当前资源的请求，是对请求来源的限流

## 2.3.流控效果

在流控的高级选项中，还有一个**流控效果选项：**

![image-20210716110225104](SpringCloud基础5——微服务保护、Sentinel.assets/6f032eea3464343bbd466a6745dca952.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

流控效果是指请求达到流控阈值时应该采取的措施，包括三种：

- **快速失败（默认）：**达到阈值后，新的请求会被立即拒绝并抛出FlowException异常，状态码429。是默认的处理方式。
- **warm up预热模式：**对超出阈值的请求同样是拒绝并抛出异常。但这种模式**阈值会动态变化**，从一个较小值**逐渐增加到最大阈值，阈值初始值是“最大阈值/冷启动因子”，**默认冷启动因子coldFactor是3，也就是阈值默认会从1/3最大阈值到最大阈值。
- **排队等待：**让所有的**请求**按照**先后次序排队执行**，两个请求的间隔不能小于指定时长

### 2.3.1.warm up

阈值一般是一个微服务能承担的最大QPS，但是一个**服务刚刚启动时，一切资源尚未初始化**（**冷启动**），如果**直接将QPS跑到最大值**，**可能导致服务瞬间宕机**。

warm up也叫**预热模式**，是**应对服务冷启动**的一种方案。请求**阈值初始值**是 **maxThreshold / coldFactor**，持续指定时长后，逐渐提高到maxThreshold值。而**冷启动因子coldFactor的默认值是3.**

**例如**，我设置QPS的maxThreshold为10，预热时间为5秒，那么初始阈值就是 10 / 3 ，也就是3，然后在5秒后逐渐增长到10.

![image-20210716110629796](SpringCloud基础5——微服务保护、Sentinel.assets/dd19d45d4643bfcc0f6c8a43ea8986ea.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**案例**

> **需求：**给/order/{orderId}这个资源设置限流，最大QPS为10，利用warm up效果，预热时长为5秒

**1）配置流控规则：**

![image-20210716111012387](SpringCloud基础5——微服务保护、Sentinel.assets/e65ee8f5e9278063b68b15cacf1046c0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）Jmeter测试**

选择《流控效果，warm up》：

![image-20210716111136699](SpringCloud基础5——微服务保护、Sentinel.assets/d335fc4aeacfdae45ff9aa3c0832ad15.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

QPS为10.

**刚刚启动时，大部分请求失败，成功的只有3个，说明QPS被限定在3：**

![image-20210716111303701](SpringCloud基础5——微服务保护、Sentinel.assets/1ed27173600004176a56c7cd6da0c01a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**随着时间推移，成功比例越来越高：**

![image-20210716111404717](SpringCloud基础5——微服务保护、Sentinel.assets/2b83bbacd16d949d6b09cd2a12fb84c5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

到Sentinel控制台查看实时监控：

![image-20210716111526480](SpringCloud基础5——微服务保护、Sentinel.assets/628f9e46066d1b2c7b34fd37c54a07cc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**一段时间（5秒）后：**

![image-20210716111658541](SpringCloud基础5——微服务保护、Sentinel.assets/a8f89536eb098ebade9e82a1c4e6897c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.3.2.排队等待

当请求超过QPS阈值时，快速失败和warm up 会拒绝新的请求并抛出异常。

而排队等待则是让**所有请求进入一个队列中**，然后按照**阈值允许的时间间隔**依次执行。后来的请求必须等待前面执行完成，如果请求**预期的等待时间超出最大时长**，则会**被拒绝**。

**工作原理**

**例如：**QPS = 5，每秒处理5个请求，即每200ms处理一个队列中的请求；设置超时时间timeout = 2000，意味着**预期等待时长**超过2000ms的请求会被拒绝并抛出异常。

![img](SpringCloud基础5——微服务保护、Sentinel.assets/00205a90efda4fe3a8fc24227d1e58e3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**那什么叫做预期等待时长呢？**

比如现在一下子来了12 个请求，因为每200ms执行一个请求，那么：

- 第6个请求的**预期等待时长** = 200 * （6 - 1） = 1000ms
- 第12个请求的预期等待时长 = 200 * （12-1） = 2200ms

现在，第1秒同时接收到10个请求，但第2秒只有1个请求，此时QPS的曲线这样的：

![image-20210716113147176](SpringCloud基础5——微服务保护、Sentinel.assets/332f05a519f068f862b826208a92eea0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如果**使用队列模式做流控**，所有进入的请求都要**排队**，以固定的200ms的间隔执行，**QPS会变的很平滑：**

![image-20210716113426524](SpringCloud基础5——微服务保护、Sentinel.assets/5e86aead800b076b7e0176dda65908ff.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

平滑的QPS曲线，对于**服务器来说是更友好的**。

**案例**

> **需求：**给/order/{orderId}这个资源设置限流，最大QPS为10，利用排队的流控效果，超时时长设置为5s

**1）添加流控规则**

![image-20210716114048918](SpringCloud基础5——微服务保护、Sentinel.assets/a86cfda20946f7e129c96bf65e85ad08.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）Jmeter测试**

选择《流控效果，队列》：

![image-20210716114243558](SpringCloud基础5——微服务保护、Sentinel.assets/3fc260fed058fd2d0ab8e5edd14aed3d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**QPS为15，已经超过了我们设定的10。**

如果是之前的 快速失败、warmup模式，超出的请求应该会直接报错。

但是我们看看队列模式的运行结果：

![image-20210716114429361](SpringCloud基础5——微服务保护、Sentinel.assets/6ac010a93956382e8dd0fd27b9700ef1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**全部都通过了。**

再去sentinel查看实时监控的QPS曲线：

![image-20210716114522935](SpringCloud基础5——微服务保护、Sentinel.assets/cac6c9059dc75e68a4dd55e43822da41.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**QPS非常平滑，一致保持在10**，但是**超出的请求没有被拒绝**，而是放入队列。因此**响应时间**（等待时间）**会越来越长**。

当**队列满了以后**，才会有**部分请求失败**：

![image-20210716114651137](SpringCloud基础5——微服务保护、Sentinel.assets/5ac6e5d7d659d86b6b4433b71a509935.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.3.3.总结，三种流控效果

**流控效果有哪些？**

- **快速失败：**QPS超过阈值时，拒绝新的请求
- **warm up：** QPS超过阈值时，拒绝新的请求；QPS阈值是逐渐提升的，可以**避免冷启动时高并发导致服务宕机。**
- **排队等待：**请求会进入**队列**，按照阈值允许的时间间隔依次执行请求；如果请求预期等待时长大于超时时间，直接拒绝

## 2.4.热点参数限流

之前的限流是统计访问某个资源的所有请求，判断是否超过QPS阈值。而热点参数限流是**分别统计参数值相同的请求**，**判断是否超过QPS阈值。**

例如一堆请求里，大部分请求携带的参数都是id=1，id=1就是热点参数，我们对它进行限流。

### 2.4.1.全局参数限流

例如，一个根据id查询商品的接口：

![image-20210716115014663](SpringCloud基础5——微服务保护、Sentinel.assets/397fafb0f9582da5fac3784d52271578.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问/goods/{id}的请求中，id参数值会有变化，热点参数限流会根据参数值分别统计QPS，统计结果：

![img](SpringCloud基础5——微服务保护、Sentinel.assets/84d579114069f7e6188293503be87785.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

当id=1的请求触发阈值被限流时，id值不为1的请求不受影响。

配置示例：

![image-20210716115232426](SpringCloud基础5——微服务保护、Sentinel.assets/a242e3710f979489316e2423628bbc95.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

代表的含义是：对hot这个资源的0号参数（第一个参数）做统计，每1秒**相同参数值**的请求数不能超过5

### 2.4.2.热点参数限流

刚才的配置中，对查询商品这个接口的所有商品一视同仁，QPS都限定为5.

而在实际开发中，可能部分商品是热点商品，例如秒杀商品，我们希望这部分商品的QPS限制与其它商品不一样，高一些。那就需要配置热点参数限流的高级选项了：

![img](SpringCloud基础5——微服务保护、Sentinel.assets/502791a057eb47e985de9abe1c888ae7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





![image-20210716115717523](SpringCloud基础5——微服务保护、Sentinel.assets/bffb6a48eedbb1f5b977d871bd94879b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

结合上一个配置，这里的含义是对0号的long类型参数限流，每1秒相同参数的QPS不能超过5，有两个例外：

•如果参数值是100，则每1秒允许的QPS为10

•如果参数值是101，则每1秒允许的QPS为15

### 2.4.4.案例

> **案例需求**：给/order/{orderId}这个资源添加热点参数限流，规则如下：
>
> •默认的热点参数规则是每1秒请求量不超过2
>
> •给102这个参数设置例外：每1秒请求量不超过4
>
> •给103这个参数设置例外：每1秒请求量不超过10
>
> **注意事项**：热点参数限流对默认的SpringMVC资源无效，需要利用**@SentinelResource注解**标记资源

**1）标记资源**

给order-service中的OrderController中的/order/{orderId}资源添加注解：

![image-20210716120033572](SpringCloud基础5——微服务保护、Sentinel.assets/ff3ef016f94d127cf9d451834b11192b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）热点参数限流规则**

访问该接口，可以看到我们标记的hot资源出现了：

![img](SpringCloud基础5——微服务保护、Sentinel.assets/1a4906f54ad9452ca9d09422f20c71b6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



这里不要点击hot后面的按钮，页面有BUG

**点击左侧菜单中热点规则菜单：**

![image-20210716120319009](SpringCloud基础5——微服务保护、Sentinel.assets/7a8c88f57bc6e0b144f63001e642407d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

点击新增，填写表单：

![image-20210716120536714](SpringCloud基础5——微服务保护、Sentinel.assets/76d1ceac59c83d3a2a0c61462aff16ba.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3）Jmeter测试**

选择《热点参数限流 QPS1》：

![image-20210716120754527](SpringCloud基础5——微服务保护、Sentinel.assets/dc53251f7776b03006b27a774fe7a483.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这里发起请求的QPS为5.

包含3个http请求：

**普通参数，QPS阈值为2**

![image-20210716120840501](SpringCloud基础5——微服务保护、Sentinel.assets/b1ac2a6749926a95d7c2d8bd202e9135.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

运行结果：

![image-20210716121105567](SpringCloud基础5——微服务保护、Sentinel.assets/7f1dd7587f2a924176711436c7a24e67.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**例外项102，QPS阈值为4**

![image-20210716120900365](SpringCloud基础5——微服务保护、Sentinel.assets/472c978e0f568dd2e9c93aa1bfd3699d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

运行结果：

![image-20210716121201630](SpringCloud基础5——微服务保护、Sentinel.assets/d5a34f01fbaa8821d75f67e4053026b6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**例外项103，QPS阈值为10**

![image-20210716120919131](SpringCloud基础5——微服务保护、Sentinel.assets/f9637532aa3340d49c5081981b1ea431.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

运行结果：

![image-20210716121220305](SpringCloud基础5——微服务保护、Sentinel.assets/755784efe53efebf35e1b36f215662b4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 3.隔离和降级

## 3.0.线程隔离和熔断降级回顾

**限流是一种预防措施**，虽然限流可以尽量避免因高并发而引起的服务故障，但服务还会因为其它原因而故障。

而要将这些故障控制在一定范围，避免雪崩，就要靠**线程隔离**（舱壁模式）和**熔断降级**手段了。

**线程隔离**之前讲到过：调用者在调用服务提供者时，给每个调用的请求分配独立线程池，出现故障时，最多消耗这个线程池内资源，避免把调用者的所有资源耗尽。

![image-20210715173215243](SpringCloud基础5——微服务保护、Sentinel.assets/9aeb8e5ba179ccb18c28e816ff379a84.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**熔断降级**：是在调用方这边加入断路器，统计对服务提供者的调用，如果调用的失败比例过高，则熔断该业务，不允许访问该服务的提供者了。

![image-20210715173428073](SpringCloud基础5——微服务保护、Sentinel.assets/283128b63b954bd520df170feb781376.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

可以看到，**不管是线程隔离还是熔断降级，都是对客户端（调用方）的保护**。需要在**客户端**发起远程调用时做线程隔离、或者服务熔断，防止客户端因阻塞崩溃。

而我们的微服务远程调用都是基于Feign来完成的，因此我们需要将Feign与Sentinel整合，在Feign里面实现线程隔离和服务熔断。

## 3.1.FeignClient整合Sentinel

SpringCloud中，微服务调用都是通过Feign来实现的，因此做客户端保护必须整合Feign和Sentinel。

### 3.1.1.修改配置，开启sentinel功能

修改OrderService的application.yml文件，开启Feign的Sentinel功能：

```bash
feign:
  sentinel:
    enabled: true # 开启feign对sentinel的支持
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.1.2.编写失败后的降级逻辑

**失败逻辑：业务失败后，不能直接报错，而应该返回用户一个友好提示或者默认结果，这个就是失败降级逻辑。**

给FeignClient编写失败后的降级逻辑

**①方式一：**FallbackClass，无法对远程调用的异常做处理

**②方式二（推荐）：FallbackFactory**，**可以对远程调用的异常做处理**，我们选择这种

这里我们演示方式二的失败降级处理。

**步骤一**：在**feing-api项目**中定义类，**实现FallbackFactory<>接口：**

![image-20210716122403502](SpringCloud基础5——微服务保护、Sentinel.assets/dc2d54b9ec6c2e97600a2b2ab9afea70.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```java
package cn.itcast.feign.clients.fallback;

import cn.itcast.feign.clients.UserClient;
import cn.itcast.feign.pojo.User;
import feign.hystrix.FallbackFactory;
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class UserClientFallbackFactory implements FallbackFactory<UserClient> {
    @Override
    public UserClient create(Throwable throwable) {
        return new UserClient() {
            //匿名内部类，重写UserClient里的方法
            @Override
            public User findById(Long id) {
                log.error("查询用户异常", throwable);
                return new User();
            }
        };
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> UserClient
>
> ```java
> @FeignClient("user-service")
> public interface UserClient {
>     @GetMapping("/user/{id}")
>     public User findById(@PathVariable Long id);
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**步骤二**：在**feing-api项目中**的config.DefaultFeignConfiguration配置类中**将UserClientFallbackFactory注册为一个Bean：**

```java
@Configuration
public class DefaultFeignConfiguration {
    @Bean
    public UserClientFallbackFactory userClientFallbackFactory(){
        return new UserClientFallbackFactory();
    }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**步骤三**：在feing-api项目中的**UserClient接口中使用UserClientFallbackFactory：**

```java
import cn.itcast.feign.clients.fallback.UserClientFallbackFactory;
import cn.itcast.feign.pojo.User;
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

@FeignClient(value = "userservice", fallbackFactory = UserClientFallbackFactory.class)
public interface UserClient {

    @GetMapping("/user/{id}")
    User findById(@PathVariable("id") Long id);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**重启order-service**后，访问一次订单查询业务，然后查看sentinel控制台，可以看到新的簇点链路：

![image-20210716123705780](SpringCloud基础5——微服务保护、Sentinel.assets/3c651fab78a8fdfe40148be480b20e2a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.1.3.总结整合步骤

Sentinel支持的雪崩解决方案：

- 线程隔离（仓壁模式）
- 降级熔断

Feign整合Sentinel的步骤：

- 在application.yml中配置：feign.sentienl.enable=true
- 给FeignClient编写FallbackFactory并注册为Bean
- 将FallbackFactory配置到FeignClient

## 3.2.线程隔离（舱壁模式）

### 3.2.1.线程隔离的实现方式

线程隔离有两种方式实现：

- **线程池隔离**
- **信号量隔离（Sentinel默认采用）**

如图：

![image-20210716123036937](SpringCloud基础5——微服务保护、Sentinel.assets/4ef91901461346802ccb2ab8f1479166.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**线程池隔离**：给每个服务调用业务分配一个线程池，利用线程池本身实现隔离效果

**信号量隔离**：不创建线程池，而是计数器模式，记录业务使用的**线程数量**，达到**信号量上限**时，**禁止新的请求。**

两者的优缺点：

![image-20210716123240518](SpringCloud基础5——微服务保护、Sentinel.assets/91de87f8ebbcebcd55fa74cccef15add.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 线程池隔离：
>
> **主动超时**是线程池能主动终止线程池中的某线程。
>
> **异步：**请求不同服务时调用不同线程池，所以能异步调用。
>
> **低扇出：**此服务依赖的服务数量少，就是扇出低，需要创建的线程池数量也少。

### 3.2.2.sentinel的线程隔离

**用法说明**：

在**添加限流规则时**，可以选择两种阈值类型：

![image-20210716123411217](SpringCloud基础5——微服务保护、Sentinel.assets/949f1c188cd5eadd4e98608fc4df3e33.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- QPS：就是每秒的请求数，在快速入门中已经演示过
- 线程数：是该资源能使用用的tomcat线程数的最大值。也就是通过限制线程数量，实现**线程隔离**（舱壁模式）。

> **案例需求**：给 order-service服务中的UserClient的查询用户接口设置流控规则，线程数不能超过 2。然后利用jemeter测试。

**1）配置隔离规则**

选择feign接口后面的流控按钮：![img](SpringCloud基础5——微服务保护、Sentinel.assets/aca8deac683f4e61bb61781b892cc206.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





填写表单：

![image-20210716123936844](SpringCloud基础5——微服务保护、Sentinel.assets/e99dca58c058ba15804e23e2565a2f39.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）Jmeter测试**

选择《阈值类型-线程数<2》：

![image-20210716124229894](SpringCloud基础5——微服务保护、Sentinel.assets/0bdced9074a6642e24ae863879c50d71.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

一次发生10个请求，有较大概率并发线程数超过2，而超出的请求会走之前定义的失败降级逻辑。

查看运行结果：

![image-20210716124147820](SpringCloud基础5——微服务保护、Sentinel.assets/347f3799ba8e820c95eb7fe92533c201.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

发现**虽然结果都是通过了，不过部分请求得到的响应是降级返回的null信息。**

### 3.2.3.总结

线程隔离的两种手段是？

- 信号量隔离
- 线程池隔离

信号量隔离的特点是？

- 基于计数器模式，简单，开销小

线程池隔离的特点是？

- 基于线程池模式，有额外开销，但隔离控制更强

## 3.3.熔断降级

熔断降级是解决雪崩问题的重要手段。其思路是由**断路器统计服务调用的异常比例、慢请求比例，**如果**超出阈值**则会**熔断**该服务。即拦截访问该服务的一切请求；而当**服务恢复时**，断路器会**放行**访问该服务的请求。

断路器**控制熔断和放行**是通过**状态机**来完成的：

![image-20210716130958518](SpringCloud基础5——微服务保护、Sentinel.assets/6fd52d723619f2459bf8b45db9903d13.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**状态机包括三个状态：**

- **closed：关闭状态**，断路器**放行所有请求**，并开始统计异常比例、慢请求比例。超过阈值则切换到open状态

- **open：打开状态**，服务调用被**熔断**，访问被熔断服务的请求会被拒绝，快速失败，直接走降级逻辑。Open状态5秒后会进入half-open状态

- half-open：半开状态

  ，放行一次请求，根据执行结果来判断接下来的操作。 

  - **请求成功：**则切换到closed状态
  - **请求失败：**则切换到open状态

断路器熔断策略有三种：慢调用、异常比例、异常数

### 3.3.1.慢调用

**慢调用**：业务的**响应时长**（RT，ResponseTime）**大于指定时长的请求**认定为**慢调用请求**。在指定时间内，如果请求数量超过设定的最小数量，**慢调用比例大于设定的阈值，则触发熔断**。

> **例如：**
>
> ![image-20210716145934347](SpringCloud基础5——微服务保护、Sentinel.assets/73dc45d24b97a149ff675daaf60a20bf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> **解读：**RT超过500ms的调用是慢调用，统计最近10000ms内的请求，如果请求量超过10次，并且慢调用比例不低于0.5，则触发熔断，熔断时长为5秒。然后进入half-open状态，放行一次请求做测试。

**案例**

> **需求：**给 UserClient的查询用户接口设置降级规则，慢调用的RT阈值为50ms，统计时间为1秒，最小请求数量为5，失败阈值比例为0.4，熔断时长为5

**1）设置慢调用**

修改user-service中的/user/{id}这个接口的业务。通过休眠模拟一个延迟时间：

![image-20210716150234787](SpringCloud基础5——微服务保护、Sentinel.assets/4cdcbd0ba00c33fc719d97caa4dd8aa7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

此时，orderId=101的订单，关联的是id为1的用户，调用时长为60ms：

![image-20210716150510956](SpringCloud基础5——微服务保护、Sentinel.assets/9713fb0c314558965ce3b0fbea3d9a38.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

orderId=102的订单，关联的是id为2的用户，调用时长为非常短；

![image-20210716150605208](SpringCloud基础5——微服务保护、Sentinel.assets/3935a3f86c118f59aed637acb09a309c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）设置熔断规则**

下面，给feign接口设置降级规则：

![image-20210716150654094](SpringCloud基础5——微服务保护、Sentinel.assets/3a244e71fc471047d1a21b114ca24916.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

规则：

![image-20210716150740434](SpringCloud基础5——微服务保护、Sentinel.assets/37a241ea3cfd9e101960057e7c1cdd36.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

超过50ms的请求都会被认为是慢请求

**3）测试**

在浏览器访问：http://localhost:8088/order/101，快速刷新5次，可以发现：

![image-20210716150911004](SpringCloud基础5——微服务保护、Sentinel.assets/a28b114eb9dadf1a963ae9f859a526af.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

触发了熔断，请求时长缩短至5ms，快速失败了，并且走降级逻辑，返回的null

在浏览器访问：http://localhost:8088/order/102，竟然也被熔断了：

![image-20210716151107785](SpringCloud基础5——微服务保护、Sentinel.assets/10db1732bfe67d3a17757651e5db63d8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 3.3.2.异常比例、异常数

**异常比例或异常数**：统计指定时间内的调用，如果**调用次数超过指定请求数**，并且出现**异常的比例达到设定的比例阈值**（或超过指定异常数），则**触发熔断**。

例如，一个异常比例设置：

![image-20210716131430682](SpringCloud基础5——微服务保护、Sentinel.assets/8469ff0baed9e35c3c0243954be97996.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

解读：统计最近1000ms内的请求，如果请求量超过10次，并且异常比例不低于0.4，则触发熔断。

一个异常数设置：

![image-20210716131522912](SpringCloud基础5——微服务保护、Sentinel.assets/b5649d5eb1b66ef2fa36f477da077930.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

解读：统计最近1000ms内的请求，如果请求量超过10次，并且异常比例不低于2次，则触发熔断。

**案例**

需求：给 UserClient的查询用户接口设置降级规则，统计时间为1秒，最小请求数量为5，失败阈值比例为0.4，熔断时长为5s

**1）设置异常请求**

首先，修改user-service中的/user/{id}这个接口的业务。手动抛出异常，以触发异常比例的熔断：

![image-20210716151348183](SpringCloud基础5——微服务保护、Sentinel.assets/02a00b6d9cc52797b4fd09d52e687d7a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

也就是说，id 为 2时，就会触发异常

**2）设置熔断规则**

下面，给feign接口设置降级规则：

![image-20210716150654094](SpringCloud基础5——微服务保护、Sentinel.assets/3a244e71fc471047d1a21b114ca24916.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

规则：

![image-20210716151538785](SpringCloud基础5——微服务保护、Sentinel.assets/104f3f9776ee7057822b7eecf8e91308.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在5次请求中，只要异常比例超过0.4，也就是有2次以上的异常，就会触发熔断。

**3）测试**

在浏览器快速访问：http://localhost:8088/order/102，快速刷新5次，触发熔断：

![image-20210716151722916](SpringCloud基础5——微服务保护、Sentinel.assets/c82828a446105a43bb260221afc6bcae.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

此时，我们去访问本来应该正常的103：

![image-20210716151844817](SpringCloud基础5——微服务保护、Sentinel.assets/df3a405f73f6e81e33827fe285b52be6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 4.授权规则

授权规则可以对请求方来源做判断和控制。

## 4.1.授权规则

### 4.1.1.基本规则

授权规则可以**对调用方的来源做控制**，有白名单和黑名单两种方式。

- **白名单：**来源（origin）在白名单内的调用者允许访问
- **黑名单：**来源（origin）在黑名单内的调用者不允许访问

点击左侧菜单的授权，可以看到授权规则：

![image-20210716152010750](SpringCloud基础5——微服务保护、Sentinel.assets/b16d92dc96e19c0f4959a54c3260f836.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **资源名：**就是受保护的资源，例如/order/{orderId}
- **流控应用：**是来源者的名单，
  - 如果是勾选白名单，则名单中的来源被许可访问。
  - 如果是勾选黑名单，则名单中的来源被禁止访问。

比如：

![image-20210716152349191](SpringCloud基础5——微服务保护、Sentinel.assets/816365d1f99e619536cb69ed767f7c7f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

我们允许请求从gateway到order-service，不允许浏览器访问order-service，那么白名单中就要填写**网关的来源名称（origin）**。

### 4.1.2.如何获取origin（用来识别请求来自网关）

Sentinel是通过RequestOriginParser这个接口的parseOrigin来获取请求的来源的。

```java
public interface RequestOriginParser {
    /**
     * 从请求request对象中获取origin，获取方式自定义
     */
    String parseOrigin(HttpServletRequest request);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这个方法的作用就是从request对象中，获取请求者的origin值并返回。

**默认**情况下，**sentinel**不管请求者从哪里来，返回值永远是default，也就是说**一切请求的来源都被认为是一样的值default。**

因此，我们需要**自定义这个接口的实现**，让**不同的请求，返回不同的origin**。

例如**order-service服务**中，我们定义一个**RequestOriginParser的实现类：**

```java
package cn.itcast.order.sentinel;

import com.alibaba.csp.sentinel.adapter.spring.webmvc.callback.RequestOriginParser;
import org.springframework.stereotype.Component;
import org.springframework.util.StringUtils;

import javax.servlet.http.HttpServletRequest;

@Component
public class HeaderOriginParser implements RequestOriginParser {
    @Override
    public String parseOrigin(HttpServletRequest request) {
        // 1.获取请求头。来自网关过滤器的请求请求头origin值为gateway
        String origin = request.getHeader("origin");
        // 2.非空判断。如果origin为空则设定值为“blank”
        if (StringUtils.isEmpty(origin)) {
            origin = "blank";
        }
        return origin;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

我们会尝试从request-header中获取origin值。

### 4.1.3.给网关添加请求头

既然获取请求origin的方式是从reques-header中获取origin值，我们必须让**所有从gateway路由到微服务的请求都带上origin头**。

这个需要利用之前学习的一个GatewayFilter来实现，AddRequestHeaderGatewayFilter。

修改gateway服务中的application.yml，添加一个defaultFilter：

```bash
spring:
  cloud:
    gateway:
      default-filters:
        - AddRequestHeader=origin,gateway
      routes:
       # ...略
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这样，从gateway路由的所有请求都会带上origin头，值为gateway。而从其它地方到达微服务的请求则没有这个头。

### 4.1.4.配置授权规则

接下来，我们添加一个授权规则，放行origin值为gateway的请求。

![image-20210716153250134](SpringCloud基础5——微服务保护、Sentinel.assets/a062cadec2ae7c42ce7bb2148e78581b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

配置如下：

![image-20210716153301069](SpringCloud基础5——微服务保护、Sentinel.assets/8a74cd3182a93b57a74a46ea9072be09.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

现在，我们直接跳过网关，访问order-service服务：

![img](SpringCloud基础5——微服务保护、Sentinel.assets/cf5dca46611341babe5cac1af4273f5c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





通过网关访问：

![image-20210716153434095](SpringCloud基础5——微服务保护、Sentinel.assets/b8caab2f6bc5449cc57a5168df6e84d2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 这里authorization是前面学网关时添加的自定义全局过滤器 

## 4.2.自定义异常结果

**默认情况下，发生限流、降级、授权拦截时，都会抛出异常到调用方**。**异常结果都是flow limmiting（限流）。**这样不够友好，无法得知是限流还是降级还是授权拦截。

### 4.2.1.异常类型

而如果要自定义异常时的返回结果，**需要实现BlockExceptionHandler接口：**

```java
public interface BlockExceptionHandler {
    /**
     * 处理请求被限流、降级、授权拦截时抛出的异常：BlockException
     */
    void handle(HttpServletRequest request, HttpServletResponse response, BlockException e) throws Exception;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这个方法有三个参数：

- HttpServletRequest request：request对象
- HttpServletResponse response：response对象
- **BlockException e：被sentinel拦截时抛出的异常**

这里的**BlockException包含多个不同的子类：**

| **异常**             | **说明**           |
| -------------------- | ------------------ |
| FlowException        | 限流异常           |
| ParamFlowException   | 热点参数限流的异常 |
| DegradeException     | 降级异常           |
| AuthorityException   | 授权规则异常       |
| SystemBlockException | 系统规则异常       |

### 4.2.2.自定义异常处理，BlockExceptionHandler接口

下面，我们就在order-service定义一个自定义异常处理类：

```java
package cn.itcast.order.sentinel;

import com.alibaba.csp.sentinel.adapter.spring.webmvc.callback.BlockExceptionHandler;
import com.alibaba.csp.sentinel.slots.block.BlockException;
import com.alibaba.csp.sentinel.slots.block.authority.AuthorityException;
import com.alibaba.csp.sentinel.slots.block.degrade.DegradeException;
import com.alibaba.csp.sentinel.slots.block.flow.FlowException;
import com.alibaba.csp.sentinel.slots.block.flow.param.ParamFlowException;
import org.springframework.stereotype.Component;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@Component
public class SentinelExceptionHandler implements BlockExceptionHandler {
    @Override
    public void handle(HttpServletRequest request, HttpServletResponse response, BlockException e) throws Exception {
        String msg = "未知异常";
        int status = 429;

        if (e instanceof FlowException) {
            msg = "请求被限流了";
        } else if (e instanceof ParamFlowException) {
            msg = "请求被热点参数限流";
        } else if (e instanceof DegradeException) {
            msg = "请求被降级了";
        } else if (e instanceof AuthorityException) {
            msg = "没有权限访问";
            status = 401;
        }

        response.setContentType("application/json;charset=utf-8");
        response.setStatus(status);
        response.getWriter().println("{\"msg\": " + msg + ", \"status\": " + status + "}");
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.2.3.测试自定义的限流和授权异常

**重启测试**，在不同场景下，会返回不同的异常消息.

**限流：**

![img](SpringCloud基础5——微服务保护、Sentinel.assets/fa8bebfd1ed144fbb1ed6d401b07337d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![image-20210716153938887](SpringCloud基础5——微服务保护、Sentinel.assets/9df848fb31269e60cfce738543d21465.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**授权拦截时：**

![img](SpringCloud基础5——微服务保护、Sentinel.assets/efb55387e78a4b30bf38c5cc0daf2712.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![image-20210716154012736](SpringCloud基础5——微服务保护、Sentinel.assets/a55e806d9491c82e2267121856b7abe6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 5.规则持久化，避免规则丢失

现在，**sentinel的所有规则默认都是内存存储**，**重启后所有规则都会丢失**。在生产环境下，我们必须确保这些规则的**持久化，避免丢失**。

## 5.1.规则管理模式

规则是否能持久化，取决于规则管理模式，sentinel支持三种规则管理模式：

- **原始模式：**Sentinel的默认模式，将规则保存在内存，重启服务会丢失。
- **pull模式**
- **push模式**

### 5.1.1.pull模式

**pull模式：**控制台将配置的规则推送到Sentinel客户端，而客户端会**将配置规则保存在本地文件或数据库中**。以后会**定时**去本地文件或数据库中**查询规则变化情况**（微服务环境下多个服务都会更改sentinel规则），**更新本地规则**。

**缺点**就是定时查询规则变化情况，可能会在规则变化后**不及时更新本地规则**。

![image-20210716154155238](SpringCloud基础5——微服务保护、Sentinel.assets/341ce0e7f7eea298b59e38b7fe3b2993.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 5.1.2.push模式

**push模式：**控制台将配置**规则推送到远程配置中心**，例如Nacos。Sentinel客户端监听Nacos，获取配置变更的推送消息，完成本地配置更新。

![image-20210716154215456](SpringCloud基础5——微服务保护、Sentinel.assets/fa5481e194c1bfaee491601079a31e7b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 5.2.实现push模式



## 5.2.1.修改order-service服务

修改OrderService，让其监听Nacos中的sentinel规则配置。

具体步骤如下：

### 1.引入依赖

在order-service中引入sentinel监听nacos的依赖：

```XML
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-datasource-nacos</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.配置nacos地址

在order-service中的application.yml文件配置nacos地址及监听的配置信息：

```bash
spring:
  cloud:
    sentinel:
      datasource:
        flow:
          nacos:
            server-addr: localhost:8848 # nacos地址
            dataId: orderservice-flow-rules
            groupId: SENTINEL_GROUP
            rule-type: flow # 还可以是：degrade、authority、param-flow
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 5.2.2.修改sentinel-dashboard源码

SentinelDashboard默认不支持nacos的持久化，需要修改源码。

### 1. 解压

解压课前资料中的sentinel源码包：

![image-20210618201340086](SpringCloud基础5——微服务保护、Sentinel.assets/8262e9fe89c0b3df48e7d37580f572c1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

然后并用IDEA打开这个项目，结构如下：

![image-20210618201412878](SpringCloud基础5——微服务保护、Sentinel.assets/a345ed6f79c444d1b1aa9e486af393f1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2. 修改nacos依赖

在sentinel-dashboard源码的pom文件中，nacos的依赖默认的scope是test，只能在测试时使用，这里要去除：

![image-20210618201607831](SpringCloud基础5——微服务保护、Sentinel.assets/894087efd3fc6bffa4fbbdb6a37943ce.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

将sentinel-datasource-nacos依赖的scope去掉：

```XML
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-datasource-nacos</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3. 添加nacos支持

在sentinel-dashboard的test包下，已经编写了对nacos的支持，我们需要将其拷贝到main下。

![image-20210618201726280](SpringCloud基础5——微服务保护、Sentinel.assets/19f469defc2908c33ae968781f897776.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4. 修改nacos地址

然后，还需要修改测试代码中的NacosConfig类：

![image-20210618201912078](SpringCloud基础5——微服务保护、Sentinel.assets/00b9260cb988eba4fc34c24e1be2012a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

修改其中的nacos地址，让其读取application.properties中的配置：

![image-20210618202047575](SpringCloud基础5——微服务保护、Sentinel.assets/e4f9bdf12f05f71a67f3a247bcb7cd35.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在sentinel-dashboard的application.properties中添加nacos地址配置：

```
nacos.addr=localhost:8848
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 5. 配置nacos数据源

另外，还需要修改com.alibaba.csp.sentinel.dashboard.controller.v2包下的FlowControllerV2类：

![image-20210618202322301](SpringCloud基础5——微服务保护、Sentinel.assets/ddf4b86664754d70de9ee2b22bc8dc7b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

让我们添加的Nacos数据源生效：

![image-20210618202334536](SpringCloud基础5——微服务保护、Sentinel.assets/63324650ff253ce40503768d37f2045e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 6. 修改前端页面

接下来，还要修改前端页面，添加一个支持nacos的菜单。

修改src/main/webapp/resources/app/scripts/directives/sidebar/目录下的sidebar.html文件：

![image-20210618202433356](SpringCloud基础5——微服务保护、Sentinel.assets/c48130a8c4a5de6385121118d2a3f6ec.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

将其中的这部分注释打开：

![image-20210618202449881](SpringCloud基础5——微服务保护、Sentinel.assets/840e853d6550de40cfbfa9acf6726feb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

修改其中的文本：

![image-20210618202501928](SpringCloud基础5——微服务保护、Sentinel.assets/c558a81e8ad16ed50fafb17ae9e64870.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 7. 重新编译、打包项目

运行IDEA中的maven插件，编译和打包修改好的Sentinel-Dashboard：

![image-20210618202701492](SpringCloud基础5——微服务保护、Sentinel.assets/b7fd28d469988f0f5e0ed9d07a1595f9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 8.启动

启动方式跟官方一样：

```
java -jar sentinel-dashboard.jar
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如果要修改nacos地址，需要添加参数：

```
java -jar -Dnacos.addr=localhost:8848 sentinel-dashboard.jar
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)