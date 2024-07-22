>  **导航：**
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})

[TOC]



# 1.微服务介绍

## 1.0.微服务技术栈 

随着互联网行业的发展，对服务的要求也越来越高，服务架构也从**单体架构**逐渐演变为现在流行的**微服务架构**。

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/4c5396deb23945f882d45452f165e333.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/385707975fee43e697c4b83723fd2b5c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**服务集群：**一个业务需要多个服务共同完成，这些服务组成服务集群。**远程调用：RestTemplate、Feign（推荐）**

**注册中心：** 记录每个服务的ip、端口、用途等服务信息。当一个服务需要调用另一个服务时，只需要从注册中心拉取或注册服务信息即可。**ureka、nacos（推荐）**

**配置中心：**统一管理服务集群的配置信息，更改配置可以实现对应服务的热更新。**nacos**

**服务网关：**访问权限管理、将请求路由到具体的服务并负载均衡、请求限流。**zuul、gateway（推荐）**

**分布式缓存：**降低数据库高并发压力，请求先过缓存再查询数据库

**分布式搜索：**简单、安全性高的搜索可以用数据库，复杂搜索和统计需要用分布式搜索。

**消息队列：**异步通讯，服务之间通过异步消息实现互相调用。

**分布式日志服务：**统一服务集群中的日志。

**系统监控链路追踪：**实时监控每个服务运行状态。

**持续集成：**对微服务项目进行自动化编译、打包、镜像、自动化部署。 



## 1.1.单体架构

**单体架构**：将业务的所有功能集中在一个项目中开发，打成一个包部署。

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/efbd01ba5cf0356673bb8560c0f6f5b1.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

单体架构的优缺点如下：

**优点：**

- 架构简单
- **部署成本低（打jar包、部署、负载均衡就完成了）**

**缺点：**

- 耦合度高（维护困难、升级困难，不利于大项目开发）



## 1.2.分布式架构

**分布式架构**：根据业务功能对系统做拆分，**每个业务功能模块作为独立项目开发**，称为一个**服务**。

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/63837f7ee1bbb5f1175bf74559c89e66.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



分布式架构的优缺点：

**优点：**

- 降低服务耦合
- 有利于服务升级和拓展

**缺点：**

- 服务调用关系错综复杂，**难度大**



> **思考：**
>
> 分布式架构虽然降低了服务耦合，但是服务拆分时也有很多问题需要思考：
>
> - 服务**拆分的粒度**如何界定？每个服务对应唯一的业务能力。
> - **服务之间如何调用**？注册中心、消息队列
> - 服务的调用关系如何管理？消息队列
>
> 人们需要制定一套行之有效的标准来约束分布式架构。



## 1.3.微服务

**微服务**是一种经过良好架构设计的**分布式架构方案** 。 

> 分布式架构：根据业务功能对系统做拆分，每个业务功能模块作为独立项目开发，称为一个服务。 

**微服务的架构特征：**

- **单一职责：**微服务拆分粒度更小，**每一个服务都对应唯一的业务能力**，做到单一职责
- **自治：**团队独立、技术独立、数据独立，独立部署和交付
- **面向服务：**服务提供**统一标准的接口**，与语言和技术无关
- **隔离性强：**服务调用做好**隔离**、容错、降级，避免出现级联问题

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/27ebf6be529ace4513a671e3413b29a5.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

微服务的上述特性其实是在给分布式架构制定一个标准，进一步降低服务之间的耦合度，提供服务的独立性和灵活性。做到高内聚，低耦合。

因此，可以认为**微服务**是一种经过良好架构设计的**分布式架构方案** 。

> 全球的互联网公司都在积极尝试自己的微服务落地方案。其中在Java领域国内最知名的是**SpringCloud和Dubbo**。

## 1.4.SpringCloud、SpringCloudAlibaba、springboot版本兼容

SpringCloud是目前国内**使用最广泛的微服务框架**。官网地址：[Spring Cloud](https://spring.io/projects/spring-cloud)。

SpringCloud集成了各种微服务功能组件，并基于SpringBoot实现了这些组件的自动装配，从而提供了良好的开箱即用体验。

其中常见的组件包括：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/d0bf0af4fff8894debc1ab5af9b1c8eb.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



另外，SpringCloud底层是依赖于SpringBoot的，并且有版本的兼容关系，如下：

这里使用的版本是 **Hoxton.SR10**，因此对应的**SpringBoot版本是2.3.x版本**。

**SpringCloud和SpringBoot：**

| Release Train                                                | Boot Version                          |
| ------------------------------------------------------------ | ------------------------------------- |
| [2021.0.x](https://github.com/spring-cloud/spring-cloud-release/wiki/Spring-Cloud-2021.0-Release-Notes) aka Jubilee | 2.6.x, 2.7.x (Starting with 2021.0.3) |
| [2020.0.x](https://github.com/spring-cloud/spring-cloud-release/wiki/Spring-Cloud-2020.0-Release-Notes) aka Ilford | 2.4.x, 2.5.x (Starting with 2020.0.3) |
| [Hoxton](https://github.com/spring-cloud/spring-cloud-release/wiki/Spring-Cloud-Hoxton-Release-Notes) | 2.2.x, 2.3.x (Starting with SR5)      |
| [Greenwich](https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Greenwich-Release-Notes) | 2.1.x                                 |
| [Finchley](https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Finchley-Release-Notes) | 2.0.x                                 |
| [Edgware](https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Edgware-Release-Notes) | 1.5.x                                 |
| [Dalston](https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Dalston-Release-Notes) | 1.5.x                                 |

| Spring Cloud Alibaba Version | Spring Cloud Version  | Spring Boot Version |
| ---------------------------- | --------------------- | ------------------- |
| 2021.0.4.0*                  | Spring Cloud 2021.0.4 | 2.6.11              |
| 2021.0.1.0                   | Spring Cloud 2021.0.1 | 2.6.3               |
| 2021.1                       | Spring Cloud 2020.0.1 | 2.4.2               |

不兼容报错：Error creating bean with name 'configurationPropertiesBeans' d

```

2021-03-11 12:38:15.512 ERROR 16912 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'configurationPropertiesBeans' defined in class path resource [org/springframework/cloud/autoconfigure/ConfigurationPropertiesRebinderAutoConfiguration.class]: Post-processing of merged bean definition failed; nested exception is java.lang.IllegalStateException: Failed to introspect Class [org.springframework.cloud.context.properties.ConfigurationPropertiesBeans] from ClassLoader [sun.misc.Launcher$AppClassLoader@18b4aac2]


```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **springcloud对比dubbo：**
>
> 
>
> ![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/e1f6524c050d493299c7e99102136e80.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> **企业需求：**
>
> ![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/41297e7330aa4cffaba32bc2b88368bc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 1.5.微服务、分布式、集群的区别

**微服务：**一种架构设计风格。**根据业务拆分成一个一个的服务**,彻底去掉耦合,每一个微服务提供单个业务功能,**一个服务只做一件事**。微服务是设计层面的东西，一般考虑如何将系统从逻辑上进行拆分，也就是垂直拆分。微服务可以是分布式的，即可以将不同服务部署在不同计算机上，当然如果量小**也可以部署在单机上**。

**集群：**一种部署方式。按照微服务架构风格拆分出来的**同一个业务系统部署到多个服务器上**，多个服务干一件事情，某一个服务宕机，用户基本无感知。主要为了保证**高可用**。我们通常讲的tomcat集群，nginx集群，redis集群都是为了确保系统的稳定性。

**分布式：**一种部署方式。将一个大系统中拆分出来的**子系统分别部署到不同的服务器上**，某一个服务宕机，其他未关联服务不受影响；重启某一个服务，其他服务也不受影响；某一个服务是瓶颈，则只针对这个服务提升性能做成集群，资源利用率高。分布式是部署层面的东西。

## 1.6.总结

- 单体架构：简单方便，高度耦合，扩展性差，适合小型项目。例如：学生管理系统

- 分布式架构：松耦合，扩展性好，但架构复杂，难度大。适合大型互联网项目，例如：京东、淘宝

- 微服务：一种良好的分布式架构方案

  ①优点：拆分粒度更小、服务更独立、耦合度更低

  ②缺点：架构非常复杂，运维、监控、部署难度提高

- SpringCloud是微服务架构的一站式解决方案，集成了各种优秀微服务功能组件





# 2.服务拆分和远程调用

任何分布式架构都离不开服务的拆分。

## 2.1.服务拆分原则

微服务拆分时的原则：

- 不同微服务，**不要重复开发相同业务**。如果两个服务间有相同业务，那一定是设计有问题。
- 微服务**数据独立**，不要访问其它微服务的数据库
- 微服务可以将自己的**业务暴露为接口**，供其它微服务调用

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/1e915c2c59bc420b51b326c9201a6fe4.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 2.2.服务拆分示例

以课前资料中的微服务cloud-demo为例，其结构如下：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/3bf3a86cc40ecec383d7f6421f99ad02.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

cloud-demo：父工程，管理依赖

- order-service：订单微服务，负责订单相关业务
- user-service：用户微服务，负责用户相关业务

**要求：**

- 订单微服务和用户微服务都必须有**各自的数据库**，相互独立
- 订单服务和用户服务都**对外暴露Restful风格的接口**
- 订单服务如果需要查询用户信息，只能调用用户服务的Restful接口，不能查询用户数据库

> **回顾RESTful：**
>
> **REST**（Representational State Transfer），**表现性状态转换**,它是一种**软件架构风格。**
>
> 
>
> - **根据REST风格对资源进行访问**称为**RESTful**。
>
> 按照REST风格访问资源时使用请求方式区分对资源进行了何种操作。
>  http://localhost/users 查询全部用户信息 GET（查询）
>  http://localhost/users/1 查询指定用户信息 GET（查询）
>  http://localhost/users 添加用户信息 POST（新增/保存）
>  http://localhost/users 修改用户信息 PUT（修改/更新）
>  http://localhost/users/1 删除用户信息 DELETE（删除）

### **2.2.1.导入Sql语句**

首先，将课前资料提供的`cloud-order.sql`和`cloud-user.sql`导入到cloud_order、cloud_user数据库中：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/d4c60553048448c19775abbf06cdd817.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/b70ace4ed3fe7e92c64a6eaf338c8607.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



cloud-user表中初始数据如下：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/fd4793e41cec4ccdb873879a6475b653.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



cloud-order表中初始数据如下：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/7d0f63bb0d15917ecbede9a645bce37d.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



cloud-order表中持有cloud-user表中的id字段。



### **2.2.2.导入demo工程**

用IDEA导入课前资料提供的Demo：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/ea0a797b60e4266c4f8d802c19dbb3d7.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



项目结构如下：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/3a20d7fdf73c6a871730b0c9c66e3b90.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





导入后，修改yml中数据库密码，会在IDEA右下角出现弹窗：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/05fd9fa0bc18ccbf146e00512037ec05.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

点击弹窗，然后按下图选择：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/ca423297737fef0f1233cccb8da1cb92.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

会出现这样的菜单：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/db3f4c27356ef7bad4ec1678502d8a6f.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



配置下项目使用的JDK：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/6d533d64981a30943bb0b3cbe5bbe9c3.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/dc00867668674ee78d59eb95dd1b4a3e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/104aa3bcd8354a55a5b150212002c4e6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **推荐个json格式化插件：**
>
> https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa/related?hl=zh-CN

## 2.3.远程调用案例，RestTemplate

>  **了解即可，推荐Feign远程调用。**
>
> **RestTemplate存在问题：**
>
> •代码可读性差，编程体验不统一
>
> **•参数复杂URL难以维护**
>
> 
>
> **Feign是一个声明式的http客户端**，官方地址：[GitHub - OpenFeign/feign: Feign makes writing java http clients easier](https://github.com/OpenFeign/feign)
>
> 其作用就是帮助我们**优雅的实现http请求的发送**，解决上面提到的问题。
>
> [SpringCloud基础2——nacos配置、Feign、Gateway_nacos feign配置_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126772669?spm=1001.2014.3001.5501)

### 2.3.1.案例需求

在order-service服务中，有一个根据id查询订单的接口：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/6d6927ae79c58f1663d795eacb82574c.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

根据id查询订单，返回值是Order对象，如图：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/0860e0558f1c13a6ab98c4853089ef8a.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

其中的user为null

在user-service中有一个根据id查询用户的接口：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/920f54299b193448d6fcfcd12c97286b.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

查询的结果如图：



![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/3082ee002bc64311849dce59ada70b88.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



修改order-service中的根据id查询订单业务，要求在查询订单的同时，根据订单中包含的userId查询出用户信息，一起返回。

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/6eee6022edcdb0b82c8e790369ff8c0e.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



因此，我们需要在order-service中 向user-service发起一个http的请求，调用http://localhost:8081/user/{userId}这个接口。

大概的步骤是这样的：

- 注册一个RestTemplate的实例到Spring容器
- 修改order-service服务中的OrderService类中的queryOrderById方法，根据Order对象中的userId查询User
- 将查询的User填充到Order对象，一起返回



### 2.3.2.注册RestTemplate

首先，我们在order-service服务中的OrderApplication启动类中，注册RestTemplate实例：

```java
package cn.itcast.order;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.web.client.RestTemplate;

@MapperScan("cn.itcast.order.mapper")
@SpringBootApplication
public class OrderApplication {

    public static void main(String[] args) {
        SpringApplication.run(OrderApplication.class, args);
    }

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.3.3.实现远程调用，RestTemplete的getForObject()方法

修改order-service服务中的cn.itcast.order.service包下的OrderService类中的queryOrderById方法：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/691f72112543afc58a639da5606ef41f.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)







## 2.4.提供者与消费者

在服务调用关系中，会有两个不同的角色：

**服务提供者**：一次业务中，被其它微服务调用的服务。（提供接口给其它微服务）

**服务消费者**：一次业务中，调用其它微服务的服务。（调用其它微服务提供的接口）

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/bc3e97c0821a5f733b02b8a7301b1562.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **思考：**
>
> 但是，服务提供者与服务消费者的角色并不是绝对的，而是相对于业务而言。
>
> 如果服务**A调用了服务B，而服务B又调用了服务C**，服务B的角色是什么？
>
> - 对于A调用B的业务而言：A是服务消费者，B是服务提供者
> - 对于B调用C的业务而言：B是服务消费者，C是服务提供者
>
> 因此，**一个服务既可以是服务提供者，也可以是服务消费者。**



# 3.Eureka注册中心



假如我们的服务提供者user-service部署了多个实例，如图：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/69739291b65a29c20d5d2407bd07d80b.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **思考：**
>
> - order-service在发起远程调用的时候，该如何得知user-service实例的ip地址和端口？
> - 有多个user-service实例地址，order-service调用时该如何选择？
> - order-service如何得知某个user-service实例是否依然健康，是不是已经宕机？



## 3.1.Eureka原理

> **注册中心：** 记录每个服务的ip、端口、用途等服务信息。当一个服务需要调用另一个服务时，只需要从注册中心拉取或注册服务信息即可。**ureka、nacos（推荐）** 

这些问题都需要利用SpringCloud中的注册中心来解决，其中最广为人知的注册中心就是Eureka，其结构如下：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/6397a85b6835f27fa99cb68979c1ed07.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**注册过程：**

1. **服务注册：**服务实例启动后，将自己的信息注册到注册中心。
2. **保存服务映射关系：**注册中心保存（服务名称---->服务实例地址列表）的映射关系
3. **服务拉取：**服务拉取时，根据服务名称和映射关系，拉取实例地址列表。
4. **负载均衡：**服务拉取后，利用负载均衡算法从实例地址列表里选中一个实例地址；

**心跳检测故障：**实例每隔一段时间（默认30秒）向注册中心发起请求，报告自己状态；当超过一定时间没有发送心跳时，eureka-server会认为微服务实例故障，将该实例从服务列表中剔除。

> **问题1：order-service如何得知user-service实例地址？**
>
> 获取地址信息的流程如下：
>
> - user-service服务实例启动后，将自己的**信息注册到eureka-server（Eureka服务端）**。这个叫**服务注册**
> - **eureka-server保存服务名称到服务实例地址列表的映射关系**
> - order-service根据服务名称，**拉取实例地址列表**。这个叫服务发现或**服务拉取**
>
> 
>
> **问题2：order-service如何从多个user-service实例中选择具体的实例？**
>
> - order-service从实例列表中利用**负载均衡算法**选中一个实例地址
> - 向该实例地址发起远程调用
>
> 
>
> **问题3：order-service如何得知某个user-service实例是否依然健康，是不是已经宕机？**
>
> - user-service会每隔一段时间**（默认30秒）**向eureka-server发起请求，报告自己状态，称为**心跳**
> - 当超过一定时间**没有发送心跳**时，eureka-server会认为微服务实例故障，将该实例从服务列表中**剔除**
> - order-service拉取服务时，就能将**故障实例排除了**



> **注意：**一个微服务，既可以是服务提供者，又可以是服务消费者，因此eureka将服务注册、服务发现等功能统一封装到了eureka-client端



因此，接下来我们动手实践的步骤包括：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/77ae3f0239687379b82b6b249183f853.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 3.2.搭建eureka-server，**@EnableEurekaServer**

首先大家注册中心服务端：eureka-server，这必须是一个独立的微服务

**3.2.1.创建eureka-server服务**

在cloud-demo父工程下，创建一个子Maven模块：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/327505f3028bfbab7907efb0f23c1365.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

填写模块信息：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/8427e6045c985331d9715c2c06f20fb6.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



然后填写服务信息：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/c170e475f95802fa46da227f998f4424.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**3.2.2.引入eureka依赖**

引入SpringCloud为eureka提供的starter依赖：

```XML
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**3.2.3.编写启动类，@EnableEurekaServer**

给eureka-server服务编写一个启动类，一定要添加一个@EnableEurekaServer注解，开启eureka的注册中心功能：

```java
package cn.itcast.eureka;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**3.2.4.编写配置文件**

编写一个application.yml文件，内容如下：

```bash
server:
  port: 10086
spring:
  application:
    name: eureka-server
#eureka也是微服务，自己也要注册到自己上
eureka:
  client:
    service-url: 
      defaultZone: http://127.0.0.1:10086/eureka
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**3.2.5.启动服务**

启动微服务，然后在浏览器访问：http://127.0.0.1:10086

看到下面结果应该是成功了：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/ce2b64b67ebe28fd76fc6cbef3b9f2a6.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/b9c0f848041943cda25e5a1494b1f943.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 3.3.服务注册

下面，我们**将user-service模块注册到eureka-server中**去。

### 3.3.1.代码实现 

**1）引入依赖**

在user-service的pom文件中，引入下面的eureka-client依赖：

```XML
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2）配置文件**

在user-service中，修改application.yml文件，添加服务名称、eureka地址：

```bash
spring:
  application:
    name: userservice
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:10086/eureka
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

http://127.0.0.1:10086/ ：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/a276b35252574d52821755f1ad587efc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **3.3.2.启动多个user-service实例**

**复制并修改启动配置** 

为了演示一个服务有多个实例的场景，我们添加一个SpringBoot的**启动配置，再启动一个user-service。**



首先，复制原来的user-service启动配置：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/9deeb22fc5bc16227e864379cfd3093b.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**在弹出的窗口中，填写信息：**

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/57dde943ee3750e19e1fe45da372bcd7.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



现在，SpringBoot窗口会出现两个user-service启动配置：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/b29ca851397c3fb9a5b0e4b22af3d4ab.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

不过，第一个是8081端口，第二个是8082端口。

启动两个user-service实例：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/197d8f42f64a36513acecd26c2460bca.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

查看eureka-server管理页面，可以看见user-server两个实例：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/55ab67be592817cd6d8c7a0b6e93fffd.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





## 3.4.服务发现/拉取和负载均衡，**@LoadBalanced**

**0）概述**

**服务拉取是基于服务名称拉取服务列**表，然后对服务列表做负载均衡。 

这就需要前面yml配置了服务名称：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/c61ddb8bd7a64497bc8c50928ced22d2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**实际上就是两个步骤：**

> 先确保导入eureka的client依赖、服务在yml中spring.application.name起了名

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/7ce3574cfcdc42f4947499bfdb94bc6c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



下面，我们将order-service的逻辑修改：向eureka-server拉取user-service的信息，实现服务发现。

**1）引入依赖**

之前说过，服务发现、服务注册统一都封装在eureka-client依赖，因此这一步与服务注册时一致。

在order-service的pom文件中，引入下面的eureka-client依赖：

```XML
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2）配置文件**

服务发现也需要知道eureka地址，因此第二步与服务注册一致，都是配置eureka信息：

在order-service中，修改application.yml文件，**添加服务名称**、eureka地址：

```bash
spring:
  application:
    name: orderservice
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:10086/eureka
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**3）服务拉取和负载均衡，注解@LoadBalanced**

最后，我们要去eureka-server中拉取user-service服务的实例列表，并且实现负载均衡。

不过这些动作不用我们去做，只需要添加一些注解即可。



在order-service的OrderApplication中，给RestTemplate这个Bean添加一个**@LoadBalanced注解：**

```java
@MapperScan("cn.itcast.order.mapper")
@SpringBootApplication
public class OrderApplication {

    public static void main(String[] args) {
        SpringApplication.run(OrderApplication.class, args);
    }
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate(){
        return new RestTemplate();
    }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

修改order-service服务中的cn.itcast.order.service包下的OrderService类中的queryOrderById方法。**修改访问的url路径，用服务名代替ip、端口：**

```java
@RestController
@RequestMapping("order")
public class OrderController {

   @Autowired
   private OrderService orderService;
   @Autowired
   private RestTemplate restTemplate;

    @GetMapping("{orderId}")
    public Order queryOrderByUserId(@PathVariable("orderId") Long orderId) {
        // 根据id查询订单并返回
        Order order = orderService.queryOrderById(orderId);
        User user = restTemplate.getForObject("http://user-server/user/" + order.getUserId(), User.class);
        order.setUser(user);
        return order;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

spring会自动帮助我们从eureka-server端，根据userservice这个服务名称，获取实例列表，而后完成**负载均衡**。

**测试负载均衡：**

不断刷新order-service请求，发现两个user-service实例轮询调用数据库：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/c03dbf473e944a6a90966ab7ec03b44a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/45e5ae8673bb4f41813f26e8d849054f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 4.Ribbon负载均衡

## 4.1.负载均衡原理

**SpringCloud底层**其实是利用了一个名为**Ribbon**的组件，来**实现负载均衡功能**的。

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/19951286d0145501ceff4cb6571685f0.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **思考：**
>
> 我们发出的请求明明是http://userservice/user/1，怎么变成了http://localhost:8081的呢？
>
> **答案：**
>
> 负载均衡拦截器LoadBalancerInterceptor
>
> ![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/a9f06a2afa7045e2aa68cdcdadaf147f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 4.2.源码跟踪

为什么我们只输入了service名称就可以访问了呢？之前还要获取ip和端口。

显然有人帮我们根据service名称，获取到了服务实例的ip和端口。它就是`LoadBalancerInterceptor`，这个类会在对RestTemplate的请求进行拦截，然后从Eureka根据服务id获取服务列表，随后利用负载均衡算法得到真实的服务地址信息，替换服务id。

我们进行源码跟踪：

**1）LoadBalancerIntercepor**

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/9b56aaa8b3816ade4a6aec52e9fd3489.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

可以看到这里的intercept方法，拦截了用户的HttpRequest请求，然后做了几件事：

- `request.getURI()`：获取请求uri，本例中就是 http://user-service/user/8
- `originalUri.getHost()`：获取uri路径的主机名，其实就是服务id，`user-service`
- `this.loadBalancer.execute()`：处理服务id，和用户请求。

这里的`this.loadBalancer`是`LoadBalancerClient`类型，我们继续跟入。



**2）LoadBalancerClient**

继续跟入execute方法：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/891ae989abd4fff386b6ff189f40b465.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

代码是这样的：

- getLoadBalancer(serviceId)：根据服务id获取ILoadBalancer，而ILoadBalancer会拿着服务id去eureka中获取服务列表并保存起来。
- getServer(loadBalancer)：利用内置的负载均衡算法，从服务列表中选择一个。本例中，可以看到获取了8082端口的服务



放行后，再次访问并跟踪，发现获取的是8081：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/a5690b11b73197a725767ad9bc6e64d7.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

果然实现了负载均衡。



**3）负载均衡策略IRule**

在刚才的代码中，可以看到获取服务使通过一个`getServer`方法来做负载均衡:

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/a5690b11b73197a725767ad9bc6e64d7.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

我们继续跟入：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/b534541df5a8787d76de2eec98d2b3dd.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

继续跟踪源码chooseServer方法，发现这么一段代码：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/af57fdb460975e63f1cfb022c5623d31.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

我们看看这个rule是谁：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/5dcc9fe154e9b381e8de324931005c11.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这里的rule默认值是一个`RoundRobinRule`，看类的介绍：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/41e0b011a155aff6400e6814fdba1752.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这不就是轮询的意思嘛。

到这里，整个负载均衡的流程我们就清楚了。



**4）总结**

SpringCloudRibbon的底层采用了一个拦截器，拦截了RestTemplate发出的请求，对地址做了修改。用一幅图来总结一下：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/f4f2601898be669f0856d90996eb76f6.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**基本流程如下：**

- 拦截我们的RestTemplate请求http://userservice/user/1
- RibbonLoadBalancerClient会从请求url中获取服务名称，也就是user-service
- DynamicServerListLoadBalancer根据user-service到eureka拉取服务列表
- eureka返回列表，localhost:8081、localhost:8082
- IRule利用内置负载均衡规则，从列表中选择一个，例如localhost:8081
- RibbonLoadBalancerClient修改请求地址，用localhost:8081替代userservice，得到http://localhost:8081/user/1，发起真实请求



## 4.3.负载均衡策略



### 4.3.1.负载均衡策略

负载均衡的规则都定义在IRule接口中，而IRule有很多不同的实现类：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/e469e0be45df652068d22c689e710378.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

不同规则的含义如下：

| **内置负载均衡规则类**     | **规则描述**                                                 |
| -------------------------- | ------------------------------------------------------------ |
| **RoundRobinRule（默认）** | 简单**轮询服务列表**来选择服务器。它是**Ribbon默认的负载均衡规则**。 |
| AvailabilityFilteringRule  | 对以下两种服务器进行忽略： （1）在默认情况下，这台服务器如果3次连接失败，这台服务器就会被设置为“短路”状态。短路状态将持续30秒，如果再次连接失败，短路的持续时间就会几何级地增加。 （2）并发数过高的服务器。如果一个服务器的并发连接数过高，配置了AvailabilityFilteringRule规则的客户端也会将其忽略。并发连接数的上限，可以由客户端的..ActiveConnectionsLimit属性进行配置。 |
| WeightedResponseTimeRule   | 为每一个服务器赋予一个权重值。服务器响应时间越长，这个服务器的权重就越小。这个规则会随机选择服务器，这个权重值会影响服务器的选择。 |
| **ZoneAvoidanceRule**      | 以区域可用的服务器为基础进行服务器的选择。使用Zone对服务器进行分类，这个Zone可以理解为一个机房、一个机架等。而后再对Zone内的多个服务做轮询。 |
| BestAvailableRule          | 忽略那些短路的服务器，并选择并发数较低的服务器。             |
| RandomRule                 | 随机选择一个可用的服务器。                                   |
| RetryRule                  | 重试机制的选择逻辑                                           |



默认的实现就是ZoneAvoidanceRule，是一种轮询方案



### 4.3.2.自定义负载均衡策略为RandomRule

> **注意，一般用默认的负载均衡规则，不做修改。** 

通过定义IRule实现可以修改负载均衡规则，有两种方式：

1. **代码方式（全局，此模块调用所有模块的策略）：**在order-service中的OrderApplication类中，定义一个新的IRule：

```java
@Bean
public IRule randomRule(){
    return new RandomRule();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



1. **配置文件方式（局部，此模块调用某些模块的策略）：**在order-service的application.yml文件中，添加新的配置也可以修改规则：

```bash
userservice: # 给某个微服务配置负载均衡规则，这里是userservice服务
  ribbon:
    NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RandomRule # 负载均衡规则 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

测试：

访问localhost:8080/order/1,localhost:8080/order/2,localhost:8080/order/3,localhost:8080/order/4

发现4次都随机到8081端口的user-server 

> **注意，一般用默认的负载均衡规则，不做修改。**



## 4.4.饥饿加载

**Ribbon默认是采用懒加载**，即**第一次访问时才会去创建负载均衡客户端LoadBalanceClient，缓存服务列表**，请求时间会很长。

而**饥饿加载则会在项目启动时创建**，降低第一次访问的耗时，通过下面配置开启饥饿加载：

```bash
ribbon:
  eager-load:
#开启饥饿加载
    enabled: true
#指定饥饿加载的服务名称
    clients: 
       - userservice
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 5.Nacos注册中心

国内公司一般都推崇阿里巴巴的技术，比如注册中心，SpringCloudAlibaba也推出了一个名为Nacos的注册中心。

## 5.1.认识Nacos

### 5.1.1.Nacos原理

[Nacos](https://nacos.io/)是阿里巴巴的产品，现在是[SpringCloud](https://spring.io/projects/spring-cloud)中的一个组件。相比[Eureka](https://github.com/Netflix/eureka)功能更加丰富，在国内受欢迎程度较高。

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/d135cd9660a97b95a651bd062c38b106.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**注册过程：**

1. **服务注册：**服务实例启动后，将自己的信息注册到注册中心。
2. **保存服务映射关系：**注册中心保存（服务名称---->服务实例地址列表）的映射关系
3. **服务拉取：**服务拉取时，根据服务名称和映射关系，拉取实例地址列表。
4. **负载均衡：**服务拉取后，利用负载均衡算法从实例地址列表里选中一个实例地址；

**心跳检测故障：**临时实例每隔一段时间（默认30秒）向注册中心发起请求，报告自己状态；当超过一定时间没有发送心跳时，eureka-server会认为微服务实例故障，将该实例从服务列表中剔除。

**主动检测故障：**nacos会主动发请求检测非临时实例是否故障，若故障则会等待其恢复健康而不是剔除。

**配置分临时实例：**

```bash
spring:
  cloud:
    nacos:
      discovery:
        ephemeral: false # 设置为非临时实例
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 5.1.2.下载安装配置启动 

这里下载1.4.1.版本的Nacos  

**下载页：**[Releases · alibaba/nacos · GitHub](https://github.com/alibaba/nacos/releases)

**下载地址：**https://github.com/alibaba/nacos/releases/download/1.4.1/nacos-server-1.4.1.zip 

**目录说明：**

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/3d409947b42a4dda9cf07b2b902bad00.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- bin：启动脚本
- conf：配置文件

**默认端口：8848**

***\*![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/842d9fc2949a4e339bf29dbc5638626b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)\****

**启动：**

在bin目录下：

```
startup.cmd -m standalone
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/d7570fb629af4c2c9b94faf07681f53a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



账号密码都是nacos。 

## 5.2.服务注册到nacos

Nacos是SpringCloudAlibaba的组件，而SpringCloudAlibaba也遵循SpringCloud中定义的服务注册、服务发现规范。因此**使用Nacos和使用Eureka对于微服务来说，并没有太大区别。**

主要差异在于：

- 依赖不同
- 服务地址不同

**0）注册前先确保启动了nacos：**

```
startup.cmd -m standalone
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**1）引入依赖**

在cloud-demo父工程的pom文件中的`<dependencyManagement>`中引入**SpringCloudAlibaba的依赖：**

```XML
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.2.6.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  **注意：SpringCloud、SpringCloudAlibaba和springboot地版本是需要互相对应的**，具体看文章上面1.4版本兼容。

**注释掉eureka的客户端依赖**，然后在user-service和order-service中的pom文件中**引入nacos-discovery依赖：**

```XML
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **注意**：**不要忘了注释掉eureka的客户端依赖。**



**2）配置nacos地址**

先**注释掉eureka的地址**，在user-service和order-service的application.yml中**添加nacos地址：**

```bash
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **注意**：**不要忘了注释掉eureka的地址**

**2.5）拉取和ureka一样：**

```java
@RestController
@RequestMapping("order")
public class OrderController {
 
   @Autowired
   private OrderService orderService;
   @Autowired
   private RestTemplate restTemplate;
 
    @GetMapping("{orderId}")
    public Order queryOrderByUserId(@PathVariable("orderId") Long orderId) {
        // 根据id查询订单并返回
        Order order = orderService.queryOrderById(orderId);
        User user = restTemplate.getForObject("http://user-server/user/" + order.getUserId(), User.class);
        order.setUser(user);
        return order;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3）重启**

重启微服务后，登录nacos管理页面，可以看到微服务信息：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/ec625ebf3d26bd5aba2dfe910836c758.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 5.3.服务分级存储模型

### 5.3.0.概述

**一个服务可以有多个实例**，例如我们的user-service，可以有:

- 127.0.0.1:8081
- 127.0.0.1:8082
- 127.0.0.1:8083

假如这些实例分布于全国各地的不同机房，例如：

- 127.0.0.1:8081，在上海机房
- 127.0.0.1:8082，在上海机房
- 127.0.0.1:8083，在杭州机房

Nacos就将**同一机房内的实例**划分为一个**集群**。

也就是说，user-service是服务，**一个服务可以包含多个集群**，如杭州、上海，每个集群下可以有多个实例，形成分级模型，如图：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/5a2a85adff02f81863470f22c0679961.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



微服务互相访问时，应该**尽可能访问同集群实例**，因为本地访问**速度更快**。当本集群内不可用时，才访问其它集群。例如：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/d346ca9e7a3a30f9a89b44e18007c5e5.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

杭州机房内的order-service应该优先访问同机房的user-service。





### 5.3.1.给user-service配置集群



修改user-service的application.yml文件，添加集群配置：

```bash
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        cluster-name: HZ # 集群名称
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

重启两个user-service实例后，我们可以在nacos控制台看到下面结果：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/6f7418180c0c0822143e932f3ee83e72.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



我们再次复制一个user-service启动配置，添加属性：

```
-Dserver.port=8083 -Dspring.cloud.nacos.discovery.cluster-name=SH
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

配置如图所示：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/d0bcc8ba83d088c14863f3f815e4fcdd.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



启动UserApplication3后再次查看nacos控制台：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/a7017d65df1be25adade064ac27c56da.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 5.3.2.同集群优先的负载均衡

默认的`ZoneAvoidanceRule`并不能实现根据同集群优先来实现负载均衡。

因此Nacos中提供了一个`NacosRule`的实现，可以优先从同集群中挑选实例。

**1）给order-service配置集群信息**

修改order-service的application.yml文件，添加集群配置：

```bash
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        cluster-name: HZ # 集群名称
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2）修改负载均衡规则**

修改**order-service**的application.yml文件，修改负载均衡规则：

```bash
userservice:
  ribbon:
    NFLoadBalancerRuleClassName: com.alibaba.cloud.nacos.ribbon.NacosRule # 负载均衡规则 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - **NacosRule**是优先选择本地集群，在**本地集群内部是随机访问的**，如果本地集群找不到提供者，会**去其他集群寻找并报警告**。
> - 对比eureka的**ZoneAvoidanceRule**是同区域内**轮询**

## 5.4.权重配置

实际部署中会出现这样的场景：

服务器设备性能有差异，部分实例所在机器性能较好，另一些较差，我们希望性能好的机器承担更多的用户请求。

但默认情况下NacosRule是同集群内随机挑选，不会考虑机器的性能问题。



因此，**Nacos提供了权重配置来控制访问频率，性能越好的机器权重越大则访问频率越高。**



在nacos控制台，找到user-service的实例列表，点击编辑，即可修改权重，**默认权重是1**：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/dd27c20c9e85d99bc7be4eb754877823.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在弹出的编辑窗口，修改权重：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/24789bdad80d1f9c66886ee0f9d9ac08.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





> **注意**：如果权重修改为0，则该实例永远不会被访问



## 5.5.环境隔离，namespace

Nacos提供了**namespace来实现环境隔离功能**。

- nacos中可以有多个namespace
- namespace下可以有**组group、服务存储service/数据存储data**等。业务相关度高的服务放在一个组group，例如订单和支付。
- **不同namespace之间相互隔离**，例如不同namespace的服务互相不可见



![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/87cb1d93240a4f622bfd4b32c59198c1.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**5.5.1.创建namespace**

**默认**情况下，所有**service、data、group都在同一个namespace**，名为**public**：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/e716791c76b65851f00ec0120af4b74f.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/23023e55e290480bbca587f11dce91da.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





我们可以点击页面新增按钮，**添加一个namespace**：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/a2a0819ecfd1205c55221ab307758b66.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



然后，填写表单：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/6e325a46487df25829979ee171b1968a.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

就能在页面看到一个新的namespace：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/df0911130b81cd044b38d332fca6f837.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**5.5.2.给微服务配置namespace**

给微服务配置namespace只能通过修改配置来实现。

例如，修改order-service的application.yml文件：

```bash
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        cluster-name: HZ
        namespace: 492a7d5d-237b-46a1-a99a-fa8e98e4b0f9 # 命名空间，填ID
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



重启order-service后，访问控制台，可以看到下面的结果：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/a02d6488a341448e5ecb6c049292bdfb.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/92d248f9dc05a1c8df8fa8650f950a80.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

此时访问order-service，因为namespace不同，会导致找不到userservice，控制台会报错：

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/efd49422f2d3b61925e89d814ebba3b7.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 5.6.Nacos与Eureka的区别

**Nacos**的服务实例分为两种l类型：

- **临时实例（默认）：**如果实例宕机超过一定时间，会从服务列表剔除，默认的类型。
- **非临时实例：**如果实例宕机，不会从服务列表剔除，也可以叫永久实例。



配置一个服务实例为永久实例：

```bash
spring:
  cloud:
    nacos:
      discovery:
        ephemeral: false # 设置为非临时实例
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> ephemeral译为短暂的，短命的。

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/feb29ed554a040b2838b30dbb5245d47.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



Nacos和Eureka整体结构类似，服务注册、服务拉取、心跳等待，但是也存在一些差异：包括**给消费者主动推送变更消息，对非临时实例主动检测状态。**

![img](SpringCloud基础1——远程调用、Eureka,Nacos注册中心、Ribbon负载均衡.assets/3588a110139ea49b0851216632a61a71.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **Nacos与eureka的共同点**
  - **注册拉取：**都支持服务注册和服务拉取
  - **心跳：**都支持服务提供者心跳方式做健康检测
- **Nacos与Eureka的区别**
  - **检测故障：**Nacos临时实例采用心跳模式，非临时实例采用主动检测模式；eureka是只能采用心跳模式。
  - **故障实例剔除：**nacos临时实例心跳不正常会被剔除，非临时实例则不会被剔除；eureka只支持心跳。
  - **及时更新：**Nacos支持服务列表变更的消息推送模式，服务列表更新更及时
  - **分布式指标：**Nacos集群默认采用AP方式（最终一致），当集群中存在非临时实例时，采用CP模式（强一致）；Eureka采用AP方式

> **CAP：**分布式三个指标，不可能同时满足，只能满足CP（一致性、分区容错性）或者AP（可用性、分区容错性）。
>
> - **一致性C：**Consistency，访问同一个集群里的多个实例，得到的数据必须一致。
> - **可用性A：**Availability ，访问集群中的任意健康节点，必须能得到响应，而不是超时或拒绝。
> - **分区容错P：**Partition Tolerance，节点故障导致集群分区后，系统依然对外提供服务。
>
> **AP（可用+分区容错，最终一致）：**各子事务分别执行和提交，允许出现结果不一致，然后采用弥补措施恢复数据即可，实现最终一致。
>
> **CP（一致+分区容错，强一致）：**各个子事务执行后互相等待，同时提交，同时回滚，达成强一致。但事务等待过程中，处于弱可用状态。
>
> **集群：**一种部署方式。按照微服务架构风格拆分出来的**同一个业务系统部署到多个服务器上**，多个服务干一件事情，某一个服务宕机，用户基本无感知。主要为了保证**高可用**。我们通常讲的tomcat集群，nginx集群，redis集群都是为了确保系统的稳定性。