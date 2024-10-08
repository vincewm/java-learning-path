> **导航：** 
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?spm=1001.2014.3001.5501 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1\. 媒资管理模块简介](#%E5%AA%92%E8%B5%84%E7%AE%A1%E7%90%86%E6%A8%A1%E5%9D%97)

[1.1 模块介绍](#%E6%A8%A1%E5%9D%97%E4%BB%8B%E7%BB%8D)

[1.2 业务流程](#1.2%20%E4%B8%9A%E5%8A%A1%E6%B5%81%E7%A8%8B)

[1.2.1 上传课程图片](#1.2.1%20%E4%B8%8A%E4%BC%A0%E8%AF%BE%E7%A8%8B%E5%9B%BE%E7%89%87)

[1.2.2 上传视频](#1.2.2%20%E4%B8%8A%E4%BC%A0%E8%A7%86%E9%A2%91)

[1.2.3 处理视频](#1.2.3%20%E5%A4%84%E7%90%86%E8%A7%86%E9%A2%91)

[1.2.4 审核媒资](#1.2.4%20%E5%AE%A1%E6%A0%B8%E5%AA%92%E8%B5%84)

[1.2.5 绑定媒资](#1.2.5%20%E7%BB%91%E5%AE%9A%E5%AA%92%E8%B5%84)

[1.3 数据模型](#1.3%20%E6%95%B0%E6%8D%AE%E6%A8%A1%E5%9E%8B)

[2\. 模块环境gateway+nacos+feign介绍](#%E6%A8%A1%E5%9D%97%E7%8E%AF%E5%A2%83gateway%2Bnacos%2Bfeign%E5%88%86%E6%9E%90)

[3 搭建Nacos、gateway](#%E6%90%AD%E5%BB%BANacos%E3%80%81gateway)

[3.1 Nacos服务发现中心](#Nacos%E6%9C%8D%E5%8A%A1%E5%8F%91%E7%8E%B0%E4%B8%AD%E5%BF%83)

[3.1.1 启动nacos，配置命名环境和分组](#%E5%90%AF%E5%8A%A8nacos%EF%BC%8C%E9%85%8D%E7%BD%AE%E5%91%BD%E5%90%8D%E7%8E%AF%E5%A2%83%E5%92%8C%E5%88%86%E7%BB%84)

[3.1.2 将系统和内容服务注册到Naocs](#%E5%B0%86%E7%B3%BB%E7%BB%9F%E5%92%8C%E5%86%85%E5%AE%B9%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E5%88%B0Naocs)

[3.2 nacos配置中心](#nacos%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83)

[3.2.1 配置中心-配置三要素，namespace、group、dataid](#%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83-%E9%85%8D%E7%BD%AE%E4%B8%89%E8%A6%81%E7%B4%A0%EF%BC%8Cnamespace%E3%80%81group%E3%80%81dataid)

[3.2.2 配置中心-配置content-service服务](#%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83-%E9%85%8D%E7%BD%AEcontent-service%E6%9C%8D%E5%8A%A1)

[3.2.3 配置中心-配置content-api服务](#%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83-%E9%85%8D%E7%BD%AEcontent-api%E6%9C%8D%E5%8A%A1)

[3.2.3 公用配置，抽取swagger配置](#2.2.3%20%E5%85%AC%E7%94%A8%E9%85%8D%E7%BD%AE%EF%BC%8C%E6%8A%BD%E5%8F%96swagger%E9%85%8D%E7%BD%AE)

[3.2.4 配置优先级](#%E9%85%8D%E7%BD%AE%E4%BC%98%E5%85%88%E7%BA%A7)

[3.2.5 导入配置文件](#%E5%AF%BC%E5%85%A5%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)

[3.3 搭建Gateway](#%E6%90%AD%E5%BB%BAGateway)

[4 搭建媒资工程](#%E6%90%AD%E5%BB%BA%E5%AA%92%E8%B5%84%E5%B7%A5%E7%A8%8B)

[5 MinIO构建分布式文件系统](#MinIO%E6%9E%84%E5%BB%BA%E5%88%86%E5%B8%83%E5%BC%8F%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F)

[5.1 分布式文件系统介绍](#%E5%88%86%E5%B8%83%E5%BC%8F%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E4%BB%8B%E7%BB%8D%C2%A0) 

[5.2 MinIO介绍](#3.2%20MinIO%E4%BB%8B%E7%BB%8D)

[5.3 MinIO数据恢复演示](#MinIO%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D%E6%BC%94%E7%A4%BA%C2%A0) 

[5.3.1 下载启动登录](#%E4%B8%8B%E8%BD%BD%E5%90%AF%E5%8A%A8%E7%99%BB%E5%BD%95%C2%A0) 

[5.3.2 创建bucket、上传文件](#%E5%88%9B%E5%BB%BAbucket%E3%80%81%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6)

[5.3.3 测试minio的数据恢复过程](#%E6%B5%8B%E8%AF%95minio%E7%9A%84%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D%E8%BF%87%E7%A8%8B)

[5.4 Docker安装MinIO、创建桶](#Docker%E5%AE%89%E8%A3%85MinIO%E3%80%81%E5%88%9B%E5%BB%BA%E6%A1%B6)

[5.5 MinIO快速入门](#MinIO%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)

[5.5.1 依赖、JDK版本要求、官方示例代码](#%E4%BE%9D%E8%B5%96%E3%80%81JDK%E7%89%88%E6%9C%AC%E8%A6%81%E6%B1%82%E3%80%81%E5%AE%98%E6%96%B9%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81)

[5.5.2 MinIO实现文件上传](#MinIO%E5%AE%9E%E7%8E%B0%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0)

[5.5.3 MinIO实现删除文件](#MinIO%E5%AE%9E%E7%8E%B0%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6)

[5.5.4 MinIO实现查询文件](#MinIO%E5%AE%9E%E7%8E%B0%E6%9F%A5%E8%AF%A2%E6%96%87%E4%BB%B6)

[6【媒资模块】上传图片](#%E3%80%90%E5%AA%92%E8%B5%84%E6%A8%A1%E5%9D%97%E3%80%91%E4%B8%8A%E4%BC%A0%E5%9B%BE%E7%89%87)

[6.1 需求分析](#%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90)

[6.1.1 业务流程](#%E4%B8%9A%E5%8A%A1%E6%B5%81%E7%A8%8B%C2%A0) 

[6.1.2 数据模型](#%E6%95%B0%E6%8D%AE%E6%A8%A1%E5%9E%8B%C2%A0) 

[6.2 创建桶+nacos配置+minio客户端配置类](#%E5%88%9B%E5%BB%BA%E6%A1%B6%2Bnacos%E9%85%8D%E7%BD%AE%2Bminio%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%85%8D%E7%BD%AE%E7%B1%BB)

[6.3 dto](#dto)

[6.4 api](#api)

[6.5 service](#service)

[6.6 Service事务优化，有网络访问的业务不要用Spring的事务控制](#Service%E4%BA%8B%E5%8A%A1%E4%BC%98%E5%8C%96)

--

## **1\. 媒资管理模块简介**

### **1.1 模块介绍**

媒资管理的主要管理对象是视频、图片、文档等，包括：媒资文件的查询、文件上传、视频处理等。

媒资查询：教学机构查询自己所拥有的媒资信息。

文件上传：包括上传图片、上传文档、上传视频。

视频处理：视频上传成功，系统自动对视频进行编码处理。

文件删除：教学机构删除自己上传的媒资文件。

媒资管理在整体流程的位置：

![](https://i-blog.csdnimg.cn/blog_migrate/ee1353f16d6ffec800d3c29408dca00e.png)

### **1.2** **业务流程**

#### **1.2.1** **上传课程图片**

教学机构人员在课程信息编辑页面**上传课程图片**，课程图片统一记录在媒资管理系统。

下图是上传图片的界面：

![](https://i-blog.csdnimg.cn/blog_migrate/9079d0b8a9f3aa9d2379d607af6c5506.png)

#### **1.2.2** **上传视频**

1、教学机构人员进入媒资管理列表查询自己上传的媒资文件。

点击“媒资管理”

![](https://i-blog.csdnimg.cn/blog_migrate/0d072f206f0b345e119d7e2628a63fbc.png)

进入媒资管理列表页面查询本机构上传的媒资文件。

![](https://i-blog.csdnimg.cn/blog_migrate/ada44d680d59c80ffa36288e7ca305ae.png)

2、教育机构用户在"媒资管理"页面中点击 "上传视频" 按钮。

![](https://i-blog.csdnimg.cn/blog_migrate/6f2c705a462e03e3cfb2c526cb91e336.png)

点击“上传视频”打开上传页面

![](https://i-blog.csdnimg.cn/blog_migrate/4e09d02f378bd8bd9518e5eceb47b83c.png)

3、选择要上传的文件，自动执行文件上传，视频上传成功会自动处理。

![](https://i-blog.csdnimg.cn/blog_migrate/a6debb59cbe5f9ef0c04232e177fc7d4.png)

#### **1.2.3** **处理视频**

对需要转码处理的视频系统会自动对其处理，处理后生成视频的URL。

处理视频没有用户界面，完全是后台自动执行。

#### **1.2.4** **审核媒资**

审核媒资包括**程序自动审核和人工审核**，程序可以通过**阿里云鉴黄接口**(https://www.aliyun.com/product/lvwang?spm=5176.19720258.J\_3207526240.51.e93976f4rSq796)审核视频，对有异议的视频由人工进行审核。

1.运营用户登入运营平台并进入媒资管理页面，查找待审核媒资

![bcdab469c19a15da367837d5e54f44cb.png](https://i-blog.csdnimg.cn/blog_migrate/13ad35e4dbd25b6b050e7fefa5a753c2.png)

2.点击列表中媒资名称链接，可预览该媒资，若是视频，则播放视频。

![](https://i-blog.csdnimg.cn/blog_migrate/b445a36aa86930b22cbc2e808a962274.png)

3.点击列表中某媒资后的"审核" 按钮，既完成媒资的审批过程。

![](https://i-blog.csdnimg.cn/blog_migrate/2b22653f1705ce013914a8b3b0cea678.png)

 点击“审核”，选择审核结果，输入审核意见。

![](https://i-blog.csdnimg.cn/blog_migrate/c97bb4fb226fea3024371396328b28b3.png)

#### **1.2.5** **绑定媒资**

课程计划创建好后需要绑定媒资文件，比如：如果课程计划绑定了视频文件，进入课程在线学习界面后点课程计划名称则在线播放视频。如下图：

![](https://i-blog.csdnimg.cn/blog_migrate/d6793ec9ed31e85ac4f94a634229343a.png)

如何将课程计划绑定媒资呢？

1.教育机构用户进入课程管理页面并编辑某一个课程，在"课程大纲"标签页的某一小节后可点击”添加视频“。

![](https://i-blog.csdnimg.cn/blog_migrate/d6453fa943ded5f8cb3a92940a096182.png)

2.弹出添加视频对话框，可通过视频关键字搜索已审核通过的视频媒资。

![](https://i-blog.csdnimg.cn/blog_migrate/aa6adb79a83bff197402544e282aa2d7.png)

3.选择视频媒资，点击提交按钮，完成课程计划绑定媒资流程。

![](https://i-blog.csdnimg.cn/blog_migrate/8aaaaf4e54f9fd90e5a72ec339eebc0f.png)

课程计划关联视频后如下图：

![](https://i-blog.csdnimg.cn/blog_migrate/eb94b849f82e4541c8eae1731a33ea3b.png)

### **1.3** **数据模型**

本模块媒资文件相关的数据表如下：

![f3e947e16918672169fc883e68adaacc.png](https://i-blog.csdnimg.cn/blog_migrate/cc7538356ea7fa874d01be5d5b583cd4.png)

**媒资文件表：**存储文件信息，包括图片、视频、文档等。

**media\_process:** 待处理视频表。

**media\_process\_history:** 视频处理历史表，记录已经处理成功的视频信息。

媒资文件与课程计划绑定关系表如下：

![](https://i-blog.csdnimg.cn/blog_migrate/e4817ab30402920eb2c0eb2f61e1dc7e.png)

## **2\. 模块环境gateway+nacos+feign介绍**

![](https://i-blog.csdnimg.cn/blog_migrate/28275c376c2e22f537327b3176157903.png)

网关可以实现请求路由、权限控制、限流等功能。

项目采用Spring Cloud Gateway作为网关，网关在请求路由时需要知道每个微服务实例的地址，项目使用Nacos作用服务发现中心和配置中心，整体的架构图如下：

![](https://i-blog.csdnimg.cn/blog_migrate/c51d03a3eae6259cc78febfc51a1a4b3.png)

**流程如下：**

1、微服务启动，将自己注册到Nacos，Nacos记录了各微服务实例的地址。

2、网关从Nacos读取服务列表，包括服务名称、服务地址等。

3、请求到达网关，网关将请求路由到具体的微服务。

**Nacos有两个作用：**

1、服务发现中心。

微服务将自身注册至Nacos，网关从Nacos获取微服务列表。

2、配置中心。

微服务众多，它们的配置信息也非常复杂，为了提供系统的可维护性，微服务的配置信息统一在Nacos配置。

## **3 搭建****Nacos、gateway**

### **3.1 Nacos服务发现中心**

#### **3.1.1 启动nacos，配置命名环境和分组**

> Spring Cloud ：一套规范
> 
> **Spring Cloud alibaba:** nacos服务注册中心，配置中心
> 
> 要使用网关要首先搭建Nacos注册、配置中心。

> Nacos服务发现中心两个概念：namespace和group
> 
> **namespace：用于区分环境，即环境隔离**、比如：开发环境、测试环境、生产环境。
> 
> **group：用于区分项目**，比如：xuecheng-plus项目、xuecheng2.0项目

**linux启动Naocs：**

```bash
sh /data/soft/restart.sh
```

> windows启动nacos：
> 
> ```bash
> startup.cmd -m standalone
> ```

访问：http://192.168.101.65:8848/nacos/

账号密码：nacos/nacos

登录成功，点击左侧菜单“命名空间”进入命名空间管理界面，

![](https://i-blog.csdnimg.cn/blog_migrate/8390ea8931030828a389c2070b5fa97e.png)

**在nacos配置命名空间（用于区分环境）:** 

点击“新建命名空间”，填写命名空间的相关信息。如下图：

![](https://i-blog.csdnimg.cn/blog_migrate/47801c23887df1f3f74b999e88e3c78f.png)

使用相同的方法再创建“测试环境”、"生产环境"的命名空间。

![](https://i-blog.csdnimg.cn/blog_migrate/61a4481525675cf9cdde2cdfd82d4f32.png)

![](https://i-blog.csdnimg.cn/blog_migrate/211a0d86d107e15e2c54629d1b7ad1a1.png)

创建成功，如下图：

![](https://i-blog.csdnimg.cn/blog_migrate/7d6aaf6deea590f274b9c360b2475e3d.png)

在教学中可以创建具体班级的命名空间，假如创建1010班级的命名空间，如下：

![](https://i-blog.csdnimg.cn/blog_migrate/a5c77abbaf82239e40b915eef7965a9f.png)

> **注意：**如果使用dev1010命名空间，在下边的配置中对namespace配置为dev1010。

#### 3.1.2 将系统和内容服务注册到Naocs

1) 在**父模块**xuecheng-plus-parent中添加**依赖管理**

```XML

<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>${spring-cloud-alibaba.version}</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```

2）在**内容管理模块**的**接口**工程、**系统管理模块**的**接口**工程中添加如下依赖

```XML
<!-- nacos注册发现-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

> 后面nacos配置中心时还有个依赖：
> 
> ```XML
>         <!--nacos配置管理依赖-->
>         <dependency>
>             <groupId>com.alibaba.cloud</groupId>
>             <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
>         </dependency>
> <!--使用bootstrap配置文件的依赖。在SpringBoot 2.4.x的版本之后，对于bootstrap.properties/bootstrap.yaml配置文件(我们合起来成为Bootstrap配置文件)的支持，需要导入如下的依赖-->
>         <dependency>
>             <groupId>org.springframework.cloud</groupId>
>             <artifactId>spring-cloud-starter-bootstrap</artifactId>
>             <version>3.1.4</version>
>         </dependency>
> ```

**3）配置nacos的地址、命名空间、分组**

在**系统管理**的接口工程的配置文件中：

```bash

#微服务配置
spring:
  application:
    name: system-service
  cloud:
    nacos:
      server-addr: 192.168.101.65:8848
      discovery:
        namespace: dev
        group: xuecheng-plus-project
```

在**内容管理**的接口工程的配置文件中配置如下信息：

```bash
spring:
  application:
    name: content-api
  cloud:
    nacos:
      server-addr: 192.168.101.65:8848
      discovery:
        namespace: dev
        group: xuecheng-plus-project
```

**4）重启内容管理服务、系统管理服务。**

待微服务启动成功，进入Nacos服务查看服务列表

![](https://i-blog.csdnimg.cn/blog_migrate/fceecb24e641a5a5172e36bac2d0b792.png)

在 “开发环境” 命名空间下有两个服务这说明内容管理微服务和系统管理微服务在Nacos注册成功。

点击其它一个微服务的“详情”

![](https://i-blog.csdnimg.cn/blog_migrate/64851267d92bad4ea8ff7d8b074ae921.png)

通过上图可以查看微服务实例的地址。

### **3.2 nacos配置中心**

#### **3.2.1 配置中心-配置三要素，namespace、group、dataid**

**1、每个项目特有的配置**

是指该配置只在有些项目中需要配置，或者该配置在每个项目中配置的值不同。

比如：spring.application.name每个项目都需要配置但值不一样，以及有些项目需要连接数据库而有些项目不需要，有些项目需要配置消息队列而有些项目不需要。

**2、项目所公用的配置**

是指在若干项目中配置内容相同的配置。比如：redis的配置，很多项目用的同一套redis服务所以配置也一样。

nacos通过namespace、group、dataid去定位一个具体的配置文件：

1、**通过namespace、group找到具体的环境和具体的项目**。

2、**通过dataid找到具体的配置文件**，dataid有三部分组成

比如：content-service-dev.yaml配置文件  由（content-service）-（dev）. (yaml)三部分组成

content-service：第一部分，它是在application.yaml中配置的应用名，即spring.application.name的值。

dev：第二部分，它是环境名，通过spring.profiles.active指定，

Yaml: 第三部分，它是配置文件 的后缀，目前nacos支持properties、yaml等格式类型，本项目选择yaml格式类型。

所以，如果我们要配置content-service工程的配置文件:

**在开发环境中配置content-service-dev.yaml**

**在测试环境中配置content-service-test.yaml**

**在生产环境中配置content-service-prod.yaml**

我们启动项目中传入spring.profiles.active的参数决定引用哪个环境的配置文件，例如：传入spring.profiles.active=dev表示使用dev环境的配置文件即content-service-dev.yaml。

#### **3.2.2 配置中心-配置**content-service**服务**

**nacos添加配置：** 

下边以开发环境为例对content-service工程的配置文件进行配置，进入nacos，进入开发环境。

![](https://i-blog.csdnimg.cn/blog_migrate/f484b39bee3cc4a7cb72dd6619e97a32.png)

点击加号，添加一个配置

![](https://i-blog.csdnimg.cn/blog_migrate/964912fedcdb766d3aad3f9abd930a48.png)

> 这个是在命名空间dev402下配置的：![](https://i-blog.csdnimg.cn/blog_migrate/f41233ee94b0fc59e0dd107388248b88.png)

输入data id、group以及配置文件内容。

> **为什么没在nacos中配置下边的内容 ？**
> 
> ```bash
> 
> spring:
>   application:
>     name: content-service
> ```
> 
>  因为dataid第一部分就是spring.application.name，nacos 客户端要根据此值确定配置文件 名称，所以spring.application.name不在nacos中配置，而是要在工程的本地bootstrap.yaml进行配置。

**bootstrap.yaml** 

在content-service工程的test/resources 中添加**bootstrap.yaml**，内容如下：

```bash

spring:
  application:
    name: content-service
  cloud:
    nacos:
      server-addr: 192.168.101.65:8848
      discovery:
        namespace: dev
        group: xuecheng-plus-project
      config:
        namespace: dev
        group: xuecheng-plus-project
        file-extension: yaml
        refresh-enabled: true

#profiles默认为dev
  profiles:
    active: dev
```

> 这些配置都是必须要配置的，包括服务名、nacos地址、命名空间、分组名、配置的后缀、热刷新，项目的环境。

**导入配置依赖** 

在内容管理模块的接口工程和service工程配置依赖：

```XML

<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
</dependency>
```

配置完成，运行content-service工程 的单元测试文件，能否正常测试，跟踪单元测试方法可以正常读取数据库的数据，说明从nacos读取配置信息正常。

通过运行观察控制台打印出下边的信息，NacosRestTemplate.java通过Post方式与nacos服务端交互读取配置信息。

<table border="1" cellspacing="0"><tbody><tr><td style="background-color:#f5f6f7;border-color:#dee0e3;width:15cm;"><p style="margin-left:0;text-align:left;"><span style="color:#646a73;">Plain Text</span><br><span style="color:#000000;">[NacosRestTemplate.java:476] - HTTP method: POST, url: http://192.168.101.65:8848/nacos/v1/cs/configs/listener, body: {Listening-Configs=content-service.yaml?xuecheng-plus-project??dev?content-service-dev.yaml?xuecheng-plus-project?88459b1483b8381eccc2ef462bd59182?dev?content-service?xuecheng-plus-project??dev?, tenant=dev}</span></p></td></tr></tbody></table>

#### **3.2.3 配置中心-配置****content-api服务**

> 思路：api引用service的配置

**nacos配置content-api-dev.yaml**

以相同的方法配置content-api工程的配置文件，在nacos中的开发环境中配置content-api-dev.yaml，内容如下：

```bash
server:
  servlet:
    context-path: /content
  port: 63040

# 日志文件配置路径
logging:
  config: classpath:log4j2-dev.xml

# swagger 文档配置
swagger:
  title: "学成在线内容管理系统"
  description: "内容系统管理系统对课程相关信息进行业务管理数据"
  base-package: com.xuecheng.content
  enabled: true
  version: 1.0.0
```

在content-api工程 的本地配置bootstrap.yaml，内容如下：

```bash


#微服务配置
spring:
  application:
    name: content-api
  cloud:
    nacos:
      server-addr: 192.168.101.65:8848
      discovery:
        namespace: dev
        group: xuecheng-plus-project
      config:
        namespace: dev
        group: xuecheng-plus-project
        file-extension: yaml
        refresh-enabled: true
        extension-configs:    #api模块引入service模块的配置，主要是数据源信息
          - data-id: content-service-${spring.profiles.active}.yaml
            group: xuecheng-plus-project
            refresh: true
  profiles:
    active: dev

```

> **注意：**因为api接口工程依赖了service工程 的jar，所以这里使用**extension-configs扩展配置文件**的方式引用service工程所用到的配置文件。
> 
> 引入内容：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/964912fedcdb766d3aad3f9abd930a48.png)

> ```bash
> 
>         extension-configs:
>           - data-id: content-service-${spring.profiles.active}.yaml
>             group: xuecheng-plus-project
>             refresh: true
> ```
> 
> 如果添加多个扩展文件，继续在下添加即可，如下：
> 
> ```bash
> 
>         extension-configs:
>           - data-id: content-service-${spring.profiles.active}.yaml
>             group: xuecheng-plus-project
>             refresh: true
>           - data-id: 填写文件 dataid
>             group: xuecheng-plus-project
>             refresh: true          
> ```

启动content-api工程，查询控制台是否打印出了请求nacos的日志，如下:

<table border="1" cellspacing="0"><tbody><tr><td style="background-color:#f5f6f7;border-color:#dee0e3;width:15cm;"><p style="margin-left:0;text-align:left;"><span style="color:#646a73;">Bash</span><br><span style="color:#000000;">[NacosRestTemplate.java:476] - HTTP method: POST, url: http://192.168.101.65:8848/nacos/v1/cs/configs/listener</span></p></td></tr></tbody></table>

并使用Httpclient测试课程查询接口是否可以正常查询。

#### **3.2.3 公用配置，抽取swagger配置**

还有一个优化的点是如何在nacos中配置项目的公用配置呢？

nacos提供了shared-configs可以引入公用配置。

在content-api中配置了swagger，所有的接口工程 都需要配置swagger，这里就可以将swagger的配置定义为一个公用配置，哪个项目用引入即可。

单独在xuecheng-plus-common分组下创建xuecheng-plus的公用配置，进入nacos的开发环境，添加swagger-dev.yaml公用配置

![](https://i-blog.csdnimg.cn/blog_migrate/26c38165df20a41d96e4f9acb8564da2.png)

删除接口工程中对swagger的配置。

项目使用shared-configs可以引入公用配置。在**内容接口工程**的本地配置文件中引入公用配置，如下：

```bash

spring:
  application:
    name: content-api
  cloud:
    nacos:
      server-addr: 192.168.101.65:8848
      discovery:
        namespace: dev
        group: xuecheng-plus-project
      config:
        namespace: dev
        group: xuecheng-plus-project
        file-extension: yaml
        refresh-enabled: true
        extension-configs:
          - data-id: content-service-${spring.profiles.active}.yaml
            group: xuecheng-plus-project
            refresh: true
        shared-configs:
          - data-id: swagger-${spring.profiles.active}.yaml
            group: xuecheng-plus-common
            refresh: true
          - data-id: logging-${spring.profiles.active}.yaml
            group: xuecheng-plus-common
            refresh: true
  profiles:
    active: dev
```

再以相同 的方法配置日志的公用配置。

![](https://i-blog.csdnimg.cn/blog_migrate/7456b8b3b4d43e324aa6a9ec9614a93e.png)

在接口工程和业务工程，引入loggin-dev.yaml公用配置文件

![](https://i-blog.csdnimg.cn/blog_migrate/33afbbfb2cf52077e8b2f0bf5e28e0df.png)

配置完成，重启content-api接口工程，访问http://localhost:63040/content/swagger-ui.html 查看swagger接口文档是否可以正常访问，查看控制台log4j2日志输出是否正常。

#### **3.2.4 配置优先级**

**nacos的环境>nacos的共享>本地**

![](https://i-blog.csdnimg.cn/blog_migrate/3d58e578b87dc167d1bc27d602fe3134.png)

引入配置文件的形式有：

1、以项目应用名方式引入

2、以扩展配置文件方式引入

3、以共享配置文件 方式引入

4、本地配置文件

各配置文件的优先级：**项目应用名配置文件 > 扩展配置文件  > 共享配置文件 > 本地配置文件**。

#### **3.2.5 导入配置文件**

进入具体的命名空间，点击“导入配置”

![](https://i-blog.csdnimg.cn/blog_migrate/a8d6c938a3025769bad3b5cb7aab89be.png)

打开导入窗口

![](https://i-blog.csdnimg.cn/blog_migrate/4479690fba6aa8768b4eb5336a52678c.png)

相同的配置选择覆盖配置。

然后点击“上传文件”选择资料中的zip包导入。zip包名例如nacos\_config\_export.zip。

导入后的nacos配置： 

![](https://i-blog.csdnimg.cn/blog_migrate/529206b7cb0498a355a3751d65308148.png)

### **3.3 搭建****Gateway**

本项目使用Spring Cloud Gateway作为网关，下边创建网关工程。

新建一个网关工程。

![](https://i-blog.csdnimg.cn/blog_migrate/95d53f849ccf0389b8148180aeddb3a1.png)

工程结构

![](https://i-blog.csdnimg.cn/blog_migrate/91bf3157474a1e986c354e1ae5b98fb4.png)

添加依赖：

```XML

<parent>
    <groupId>com.xuecheng</groupId>
    <artifactId>xuecheng-plus-parent</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <relativePath>../xuecheng-plus-parent</relativePath>
</parent>
<artifactId>xuecheng-plus-gateway</artifactId>

<dependencies>

    <!--网关-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-gateway</artifactId>
    </dependency>

    <!--服务发现中心-->
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    </dependency>
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
    </dependency>
    <!-- 排除 Spring Boot 依赖的日志包冲突 -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <!-- Spring Boot 集成 log4j2 -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>


</dependencies>
```

配置网关的bootstrap.yaml配置文件

```bash
#微服务配置
spring:
  application:
    name: gateway
  cloud:
    nacos:
      server-addr: 192.168.101.65:8848
      discovery:
        namespace: dev
        group: xuecheng-plus-project
      config:
        namespace: dev
        group: xuecheng-plus-project
        file-extension: yaml
        refresh-enabled: true
        shared-configs:
          - data-id: logging-${spring.profiles.active}.yaml
            group: xuecheng-plus-common
            refresh: true


  profiles:
    active: dev
```

在nacos上配置网关路由策略：

![](https://i-blog.csdnimg.cn/blog_migrate/c4610e2ad7daf263b7bbfca862e61fca.png)

详细配置如下：

```bash

server:
  port: 63010 # 网关端口
spring:
  cloud:
    gateway:
#      filter:
#        strip-prefix:
#          enabled: true
      routes: # 网关路由配置
        - id: content-api # 路由id，自定义，只要唯一即可
          # uri: http://127.0.0.1:8081 # 路由的目标地址 http就是固定地址
          uri: lb://content-api # 路由的目标地址 lb就是负载均衡，后面跟服务名称
          predicates: # 路由断言，也就是判断请求是否符合路由规则的条件
            - Path=/content/** # 这个是按照路径匹配，只要以/content/开头就符合要求
#          filters:
#            - StripPrefix=1
        - id: system-api
          # uri: http://127.0.0.1:8081
          uri: lb://system-api
          predicates:
            - Path=/system/**
#          filters:
#            - StripPrefix=1
        - id: media-api
          # uri: http://127.0.0.1:8081
          uri: lb://media-api
          predicates:
            - Path=/media/**
#          filters:
#            - StripPrefix=1
```

启动网关工程。

## **4 搭建媒资工程**

![](https://i-blog.csdnimg.cn/blog_migrate/36ca2d55d019478b7e43c0f87e4cd3d6.png)

## **5 MinIO**构建分布式文件系统

### **5.1 分布式文件系统**介绍 

       文件系统是负责管理和存储文件的系统软件，**操作系统通过文件系统提供的接口去存取文件**，用户通过操作系统访问磁盘上的文件。

文件系统所处的位置：

![](https://i-blog.csdnimg.cn/blog_migrate/91af7a1839eae1eaf1f346ebebc3bbe6.png)

常见的文件系统：FAT16/FAT32、NTFS、HFS、UFS、APFS、XFS、Ext4等 。

**分布式文件系统**就是海量用户查阅海量文件的方案，**通过网络将若干计算机组织起来共同去存储海量的文件**，去接收海量用户的请求，这些组织起来的计算机通过网络进行通信，如下图：

![](https://i-blog.csdnimg.cn/blog_migrate/0fe27f519a71a12b47d49dd3c6258d29.png)

 **好处：**

1、一台计算机的文件系统处理能力扩充到多台计算机**同时处理**。

 2、一台计算机挂了还有另外**副本**计算机提供数据。

 3、每台计算机可以放在不同的地域，这样用户就可以**就近访问**，提高访问速度。

常见的分布式文件系统：NFS、GFS、HDFS、云计算厂家（如**阿里云对象存储服务oss**，适合存储不敏感的数据）

### **5.2 MinIO介绍**

本项目采用MinIO构建分布式文件系统，MinIO 是一个非常**轻量**的服务,可以很简单的和其他应用的结合使用，它兼容亚马逊 S3 云存储服务接口，非常适合于**存储大容量非结构化的数据**，例如图片、视频、日志文件、备份数据和容器/虚拟机镜像等。

它一大特点就是轻量，使用简单，功能强大，支持各种平台，单个文件最大5TB，兼容 Amazon S3接口，提供了 Java、Python、GO等多版本SDK支持。

> **官网：**https://min.io
> 
> **中文：**https://www.minio.org.cn/，http://docs.minio.org.cn/docs/

MinIO集群采用**去中心化共享架构**，**每个结点是对等关系**，通过Nginx可对MinIO进行负载均衡访问。

> **去中心化有什么好处？**
> 
> 在大数据领域，通常的设计理念都是无中心和分布式。
> 
> Minio分布式模式可以帮助你搭建一个**高可用的对象存储服务**，你可以使用这些存储设备，而**不用考虑其真实物理位置**。
> 
> 它**将分布在不同服务器上的多块硬盘组成一个对象存储服务**。由于硬盘分布在不同的节点上，分布式Minio**避免了单点故障**。如下图：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/905a15734b120de5aa7775841272728f.png)

**纠删码技术**

Minio使用纠删码技术来**保护数据**，它是一种**恢复丢失和损坏数据的数学算法**，它将数据分块冗余的分散存储在各各节点的磁盘上，所有的可用磁盘组成一个集合，上图由8块硬盘组成一个集合，当上传一个文件时会通过纠删码算法计算对文件进行分块存储，除了将文件本身分成4个数据块，还会生成4个校验块，数据块和校验块会分散的存储在这8块硬盘上。

使用纠删码的好处是**即便丢失一半数量（N/2）的硬盘，仍然可以恢复数据。** 比如上边集合中有4个以内的硬盘损害仍可保证数据恢复，不影响上传和下载，如果多于一半的硬盘坏了则无法恢复。

### 5.3 MinIO**数据恢复演示** 

下边在本机演示MinIO恢复数据的过程，在本地创建4个目录表示4个硬盘。

![](https://i-blog.csdnimg.cn/blog_migrate/88b7de91db22f916ebab08eac4dedb8b.png)

#### 5.3.1 下载启动登录 

下载minio，下载地址在https://dl.min.io/server/minio/release/

![](https://i-blog.csdnimg.cn/blog_migrate/c7d8a47476111b6db73d1d5137693e05.png)

CMD进入有minio.exe的目录，运行下边的命令，启动并指定存储路径： 

```bash

minio.exe server D:\develop\minio_data\data1  D:\develop\minio_data\data2  D:\develop\minio_data\data3  D:\develop\minio_data\data4
```

启动结果如下：

![](https://i-blog.csdnimg.cn/blog_migrate/f1ca4ca566048676ff74c07d9674a0dd.png)

> 说明：
> 
> 1）老版本使用的MINIO\_ACCESS\_KEY 和 MINIO\_SECRET\_KEY不推荐使用，推荐使用MINIO\_ROOT\_USER 和MINIO\_ROOT\_PASSWORD设置账号和密码。
> 
> 2）pool即minio节点组成的池子，当前有一个pool和4个硬盘组成的set集合
> 
> 3）因为集合是4个硬盘，大于2的硬盘损坏数据将无法恢复。
> 
> 4）账号和密码默认为minioadmin、minioadmin，可以在环境变量中设置通过'MINIO\_ROOT\_USER' and 'MINIO\_ROOT\_PASSWORD' 进行设置。

**访问：**下边输入http://localhost:9000进行登录，账号和密码为：minioadmin/minioadmin

![](https://i-blog.csdnimg.cn/blog_migrate/b7680e55bf32439ccb23ea9167b4bab5.png)

登录成功：

![](https://i-blog.csdnimg.cn/blog_migrate/763fc26da66ad39d7bf012bdc25fdd89.png)

#### **5.3.2 创建bucket、上传文件**

创建bucket，桶，它相当于存储文件的目录，可以创建若干的桶。

![](https://i-blog.csdnimg.cn/blog_migrate/15510236c5f16a38f38806f0e9d16446.png)

输入bucket的名称，点击“CreateBucket”，创建成功

![](https://i-blog.csdnimg.cn/blog_migrate/649d9e0a2d3f4ce8856bb50a37ec97e1.png)

**点击“upload”上传文件：**

![](https://i-blog.csdnimg.cn/blog_migrate/97f56c36c2df047f47be32210e2d4352.png)

下边去四个目录观察文件的存储情况

![](https://i-blog.csdnimg.cn/blog_migrate/fb99f1a1b70bd139f2a0509a47c37bb0.png)

我们发现上传的1.mp4文件存储在了四个目录，即四个硬盘上。

#### 5.3.3 测试minio的数据恢复过程

1、首先删除一个目录。

删除目录后仍然可以在web控制台上传文件和下载文件。

稍等片刻删除的目录自动恢复。

2、删除两个目录。

删除两个目录也会自动恢复。

3、删除三个目录 。

由于 集合中共有4块硬盘，有大于一半的硬盘损坏数据无法恢复。

此时报错：We encountered an internal error, please try again.  (Read failed.  Insufficient number of drives online)在线驱动器数量不足。

### **5.4 Docker安装**MinIO、创建桶

开发阶段和生产阶段统一使用Docker下的MINIO。

docker安装MinIO的镜像和容器，执行

```bash
sh /data/soft /restart.sh
```

启动Docker下的MinIO

启动完成登录MinIO查看是否正常。

访问

```bash
http://192.168.101.65:9000
```

![](https://i-blog.csdnimg.cn/blog_migrate/ed43e2e184982d46f38fefa524cadd80.png)

本项目创建两个buckets：

mediafiles： 普通文件

video：视频文件

### 5.5 MinIO快速入门

#### 5.5.1 依赖、JDK版本要求、官方示例代码

MinIO兼容 Amazon S3接口，提供了 Java、Python、GO等多版本SDK支持。

MinIO提供多个语言版本SDK的支持，下边找到java版本的文档：

```bash
https://docs.min.io/docs/java-client-quickstart-guide.html
```

![](https://i-blog.csdnimg.cn/blog_migrate/088a342f4b0dcffdbbb40d814f508311.png)

**最低需求Java 1.8或更高版本。**

maven依赖如下：在**media-service工程**添加此依赖。

```XML

<dependency>
    <groupId>io.minio</groupId>
    <artifactId>minio</artifactId>
    <version>8.4.3</version>
</dependency>
<dependency>
    <groupId>com.squareup.okhttp3</groupId>
    <artifactId>okhttp</artifactId>
    <version>4.8.1</version>
</dependency>
```

> **参数说明：**
> 
> 需要三个参数才能连接到minio服务。
> 
> <table border="1" cellspacing="0"><tbody><tr><td style="background-color:#ffffff;border-color:#dee0e3;width:134.8pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">参数</span></p></td><td style="background-color:#ffffff;border-color:#dee0e3;width:290.4pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">说明</span></p></td></tr><tr><td style="border-color:#dee0e3;vertical-align:top;width:134.8pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">Endpoint</span></p></td><td style="vertical-align:top;width:290.4pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">对象存储服务的</span><span style="color:#000000;">URL</span></p></td></tr><tr><td style="border-color:#dee0e3;vertical-align:top;width:134.8pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">Access Key</span></p></td><td style="vertical-align:top;width:290.4pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">Access key</span><span style="color:#000000;">就像用户</span><span style="color:#000000;">ID</span><span style="color:#000000;">，可以唯一标识你的账户。</span></p></td></tr><tr><td style="border-color:#dee0e3;vertical-align:top;width:134.8pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">Secret Key</span></p></td><td style="vertical-align:top;width:290.4pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">Secret key</span><span style="color:#000000;">是你账户的密码。</span></p></td></tr></tbody></table>

**上传文件-官方的示例代码如下：**

```java

import io.minio.BucketExistsArgs;
import io.minio.MakeBucketArgs;
import io.minio.MinioClient;
import io.minio.UploadObjectArgs;
import io.minio.errors.MinioException;
import java.io.IOException;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;
public class FileUploader {
  public static void main(String[] args)throws IOException, NoSuchAlgorithmException, InvalidKeyException {
    try {
      // Create a minioClient with the MinIO server playground, its access key and secret key.
      MinioClient minioClient =
          MinioClient.builder()
              .endpoint("https://play.min.io")
              .credentials("Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG")
              .build();
      // Make 'asiatrip' bucket if not exist.
      boolean found =
          minioClient.bucketExists(BucketExistsArgs.builder().bucket("asiatrip").build());
      if (!found) {
        // Make a new bucket called 'asiatrip'.
        minioClient.makeBucket(MakeBucketArgs.builder().bucket("asiatrip").build());
      } else {
        System.out.println("Bucket 'asiatrip' already exists.");
      }
      // Upload '/home/user/Photos/asiaphotos.zip' as object name 'asiaphotos-2015.zip' to bucket
      // 'asiatrip'.
      minioClient.uploadObject(
          UploadObjectArgs.builder()
              .bucket("asiatrip")
              .object("asiaphotos-2015.zip")
              .filename("/home/user/Photos/asiaphotos.zip")
              .build());
      System.out.println(
          "'/home/user/Photos/asiaphotos.zip' is successfully uploaded as "
              + "object 'asiaphotos-2015.zip' to bucket 'asiatrip'.");
    } catch (MinioException e) {
      System.out.println("Error occurred: " + e);
      System.out.println("HTTP trace: " + e.httpTrace());
    }
  }
}
```

#### 5.5.2 MinIO实现文件上传

在**media-service工程**中测试上传文件功能： 

**创建 bucket**

首先创建一个用于测试的bucket

![](https://i-blog.csdnimg.cn/blog_migrate/6acd4fcc0e6a8d537cad1b4a75e827d2.png)

**访问权限** 

点击“Manage”修改bucket的访问权限

![](https://i-blog.csdnimg.cn/blog_migrate/5f48a6fcf61a8d63b8e8bd36f5fb02bc.png)

选择public权限

![](https://i-blog.csdnimg.cn/blog_migrate/63e1923abd6b2ecb880b65b5693c73c1.png)

**代码**

在xuecheng-plus-media-service工程 的test下编写测试代码如下：

```java

package com.xuecheng.media;

/**
 * @description 测试MinIO

 */
public class MinioTest {

    static MinioClient minioClient =
            MinioClient.builder()
                    .endpoint("http://192.168.101.65:9000")
                    .credentials("minioadmin", "minioadmin")    //accessKey和secretKey
                    .build();

   //上传文件
    @Test
    public  void upload() {
        try {
            UploadObjectArgs testbucket = UploadObjectArgs.builder()
                    .bucket("testbucket")//桶名
//                    .object("test001.mp4")
                    .object("test/001/1.mp4")//对象，上传后的文件名
                    .filename("D:\\develop\\upload\\1.mp4")    //待上传的本地文件路径
                    .contentType("video/mp4")//默认根据扩展名确定文件内容类型，也可以指定
                    .build();
            minioClient.uploadObject(testbucket);
            System.out.println("上传成功");
        } catch (Exception e) {
            e.printStackTrace();
            System.out.println("上传失败");
        }

    }

}
```

**启动测试** 

**执行upload方法**，分别测试向桶的根目录上传文件以及子目录上传文件。

上传成功，通过web控制台刷新查看文件，并预览文件。

![](https://i-blog.csdnimg.cn/blog_migrate/e101f9ed0a760744b470f316c5770878.png)

> **说明：**
> 
> **设置contentType**可以通过com.j256.simplemagic.ContentType枚举类查看常用的mimeType**（媒体类型）**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/754d169e1d44b3a869a7e60317b45622.png)

 **通过扩展名（如.mp4）得到媒体类型mimeType：**

```java

    //根据扩展名取出mimeType
    ContentInfo extensionMatch = ContentInfoUtil.findExtensionMatch(".mp4");
    String mimeType = MediaType.APPLICATION_OCTET_STREAM_VALUE;//通用mimeType，字节流
```

通过扩展名得到媒体类型mimeType，完善上边的代码 如下：

```java

@Test
    public  void upload() {
        //根据扩展名取出mimeType
        ContentInfo extensionMatch = ContentInfoUtil.findExtensionMatch(".mp4");
        String mimeType = MediaType.APPLICATION_OCTET_STREAM_VALUE;//通用mimeType，字节流
        if(extensionMatch!=null){
            mimeType = extensionMatch.getMimeType();
        }
        try {
            UploadObjectArgs testbucket = UploadObjectArgs.builder()
                    .bucket("testbucket")
//                    .object("test001.mp4")
                    .object("001/test001.mp4")//添加子目录
                    .filename("D:\\develop\\upload\\1mp4.temp")
                    .contentType(mimeType)//默认根据扩展名确定文件内容类型，也可以指定
                    .build();
            minioClient.uploadObject(testbucket);
            System.out.println("上传成功");
        } catch (Exception e) {
            e.printStackTrace();
            System.out.println("上传失败");
        }

    }
```

#### 5.5.3 MinIO实现**删除文件**

下边测试删除文件

参考：https://docs.min.io/docs/java-client-api-reference#removeObject

```java

@Test
public void delete(){
    try {
        minioClient.removeObject(
               RemoveObjectArgs.builder().bucket("testbucket").object("001/test001.mp4").build());
        System.out.println("删除成功");
    } catch (Exception e) {
       e.printStackTrace();
        System.out.println("删除失败");
    }
}
```

#### 5.5.4 MinIO实现**查询文件**

通过查询文件查看文件是否存在minio中。

参考：https://docs.min.io/docs/java-client-api-reference#getObject

**不校验文件的完整性查询文件**

```java

//查询文件
@Test
public void getFile() {
    GetObjectArgs getObjectArgs = GetObjectArgs.builder().bucket("testbucket").object("test001.mp4").build();
    try(
        FilterInputStream inputStream = minioClient.getObject(getObjectArgs);
        FileOutputStream outputStream = new FileOutputStream(new File("D:\\develop\\upload\\1_2.mp4"));
     ) {
        IOUtils.copy(inputStream,outputStream);

     } catch (Exception e) {
        e.printStackTrace();
     }
}
```

**校验文件的完整性：**

对文件计算出md5值，比较原始文件的md5和目标文件的md5，一致则说明完整

```java

//校验文件的完整性对文件的内容进行md5
FileInputStream fileInputStream1 = new FileInputStream(new File("D:\\develop\\upload\\1.mp4"));
String source_md5 = DigestUtils.md5Hex(fileInputStream1);
FileInputStream fileInputStream = new FileInputStream(new File("D:\\develop\\upload\\1a.mp4"));
String local_md5 = DigestUtils.md5Hex(fileInputStream);
if(source_md5.equals(local_md5)){
    System.out.println("下载成功");
}
```

## 6**【媒资模块】上传图片**

### **6.1 需求分析**

#### 6.1.1 业务流程 

新增课程界面上传课程图片： 

![](https://i-blog.csdnimg.cn/blog_migrate/10881a6ed063df82b61991cb72102af6.png)

上传课程图片总体上包括两部分：

1、上传课程图片前端请求媒资管理服务将**文件上传至分布式文件系统**，并且在媒资管理数据库保存文件信息。

2、上传图片成功保存**图片地址到课程基本信息表**中，地址不能包含域名端口地址的前缀，降低耦合。

**详细流程如下：**

![](https://i-blog.csdnimg.cn/blog_migrate/43ab7fe26573492758f26b7356cb0419.png)

#### 6.1.2 数据模型 

![](https://i-blog.csdnimg.cn/blog_migrate/c8ff7f8c2b699b6d85b55bfa3450ba06.png)

各字段描述如下：

![](https://i-blog.csdnimg.cn/blog_migrate/39567ca8ca2ac8f4bd9791bab1176d49.png)

这里主键是**文件的md5值**，获取方式DigestUtils.md5Hex(fileInputStream)。

### 6.2 创建桶+nacos配置+minio客户端配置类

创建桶，并设置为**公开**： 

**mediafiles桶：**存储视频以外的文件 

**video桶：**存视频

在nacos配置中minio的相关信息，进入media-service-dev.yaml:

![](https://i-blog.csdnimg.cn/blog_migrate/d33ee07c127e71773102ceba6608a0c8.png)

配置信息如下：

```bash

minio:
  endpoint: http://192.168.101.65:9000
  accessKey: minioadmin
  secretKey: minioadmin
  bucket:
    files: mediafiles
    videofiles: video
```

在media-service工程编写minio的配置类：

```java

package com.xuecheng.media.config;
/**
 * @description minio配置
 */
 @Configuration
public class MinioConfig {


 @Value("${minio.endpoint}")
 private String endpoint;
 @Value("${minio.accessKey}")
 private String accessKey;
 @Value("${minio.secretKey}")
 private String secretKey;

 @Bean
 public MinioClient minioClient() {

  MinioClient minioClient =
          MinioClient.builder()
                  .endpoint(endpoint)
                  .credentials(accessKey, secretKey)
                  .build();
  return minioClient;
 }
}
```

### 6.3 dto

响应模型类： 

```java
package com.xuecheng.media.model.dto;
//使用dto，而不是实体类，是为了后期方便加数据

@Data
public class UploadFileResultDto extends MediaFiles {
  

}
```

请求参数类：

```java
package com.xuecheng.media.model.dto;


 @Data
public class UploadFileParamsDto {

 /**
  * 文件名称
  */
 private String filename;


 /**
  * 文件类型（文档，音频，视频）
  */
 private String fileType;
 /**
  * 文件大小
  */
 private Long fileSize;

 /**
  * 标签
  */
 private String tags;

 /**
  * 上传人
  */
 private String username;

 /**
  * 备注
  */
 private String remark;



}
```

### 6.4 api

> 请求地址：/media/upload/coursefile
> 
> 请求内容：**Content-Type:** multipart/form-data;
> 
> form-data：name="filedata"; filename="具体的文件名称"

媒体-api包下： 

> -   请求参数是**multipart/form-data**格式，不是**application/json**，所以要用@RequestMapping的consumes属性指定请求的提交内容类型**(Content-Type)**;
> -   **@RequestPart**这个注解用在multipart/form-data表单提交请求的方法上，主要用来搭配springboot接收MultipartFile类型的文件。

```java
@ApiOperation("上传文件")
@RequestMapping(value = "/upload/coursefile",consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
@ResponseBody
public UploadFileResultDto upload(
        @RequestPart("filedata") MultipartFile upload,
        @RequestParam(value = "folder",required=false) String folder,
        @RequestParam(value = "objectName",required=false) String objectName
    ) throws IOException {

        Long companyId = 1232141425L;
    UploadFileParamsDto uploadFileParamsDto = new UploadFileParamsDto();
    //文件大小
    uploadFileParamsDto.setFileSize(filedata.getSize());
    //图片
    uploadFileParamsDto.setFileType("001001");
    //文件名称
    uploadFileParamsDto.setFilename(filedata.getOriginalFilename());//文件名称
    //文件大小
    long fileSize = filedata.getSize();
    uploadFileParamsDto.setFileSize(fileSize);
    //创建临时文件
    File tempFile = File.createTempFile("minio", "temp");
    //上传的文件拷贝到临时文件
    filedata.transferTo(tempFile);
    //文件路径
    String absolutePath = tempFile.getAbsolutePath();
    //上传文件
    UploadFileResultDto uploadFileResultDto = mediaFileService.uploadFile(companyId, uploadFileParamsDto, absolutePath);
    
    return uploadFileResultDto;
}
```

### 6.5 service

```java
@Autowired
MinioClient minioClient;

@Autowired
MediaFilesMapper mediaFilesMapper;

//普通文件桶
@Value("${minio.bucket.files}")
private String bucket_Files;


//获取文件默认存储目录路径 年/月/日
private String getDefaultFolderPath() {
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
    String folder = sdf.format(new Date()).replace("-", "/")+"/";
    return folder;
}

//获取文件的md5
private String getFileMd5(File file) {
    try (FileInputStream fileInputStream = new FileInputStream(file)) {
        String fileMd5 = DigestUtils.md5Hex(fileInputStream);
        return fileMd5;
    } catch (Exception e) {
        e.printStackTrace();
        return null;
    }
}

//根据扩展名获取mimeType。例如视频的mimeType为video/mp4
private String getMimeType(String extension){
    if(extension==null)
        extension = "";
    //根据扩展名取出mimeType
    ContentInfo extensionMatch = ContentInfoUtil.findExtensionMatch(extension);
    //通用mimeType，字节流
    String mimeType = MediaType.APPLICATION_OCTET_STREAM_VALUE;
    if(extensionMatch!=null){
        mimeType = extensionMatch.getMimeType();
    }
    return mimeType;
}
/**
 * @description 将文件写入minIO
 * @param localFilePath  文件地址
 * @param bucket  桶
 * @param objectName 对象名称
 * @return void
 * @author Mr.M
 * @date 2022/10/12 21:22
 */
public boolean addMediaFilesToMinIO(String localFilePath,String mimeType,String bucket, String objectName) {
    try {
        UploadObjectArgs testbucket = UploadObjectArgs.builder()
                .bucket(bucket)
                .object(objectName)
                .filename(localFilePath)
                .contentType(mimeType)
                .build();
        minioClient.uploadObject(testbucket);
        log.debug("上传文件到minio成功,bucket:{},objectName:{}",bucket,objectName);
        System.out.println("上传成功");
        return true;
    } catch (Exception e) {
        e.printStackTrace();
        log.error("上传文件到minio出错,bucket:{},objectName:{},错误原因:{}",bucket,objectName,e.getMessage(),e);
        XueChengPlusException.cast("上传文件到文件系统失败");
    }
    return false;
}

/**
 * @description 将文件信息添加到文件表
 * @param companyId  机构id
 * @param fileMd5  文件md5值
 * @param uploadFileParamsDto  上传文件的信息
 * @param bucket  桶
 * @param objectName 对象名称
 * @return com.xuecheng.media.model.po.MediaFiles
 * @author Mr.M
 * @date 2022/10/12 21:22
 */
@Transactional
public MediaFiles addMediaFilesToDb(Long companyId,String fileMd5,UploadFileParamsDto uploadFileParamsDto,String bucket,String objectName){
    //从数据库查询文件
    MediaFiles mediaFiles = mediaFilesMapper.selectById(fileMd5);
    if (mediaFiles == null) {
        mediaFiles = new MediaFiles();
        //拷贝基本信息
        BeanUtils.copyProperties(uploadFileParamsDto, mediaFiles);
        mediaFiles.setId(fileMd5);
        mediaFiles.setFileId(fileMd5);
        mediaFiles.setCompanyId(companyId);
        mediaFiles.setUrl("/" + bucket + "/" + objectName);
        mediaFiles.setBucket(bucket);
        mediaFiles.setFilePath(objectName);
        mediaFiles.setCreateDate(LocalDateTime.now());
        mediaFiles.setAuditStatus("002003");
        mediaFiles.setStatus("1");
        //保存文件信息到文件表
        int insert = mediaFilesMapper.insert(mediaFiles);
        if (insert < 0) {
            log.error("保存文件信息到数据库失败,{}",mediaFiles.toString());
            XueChengPlusException.cast("保存文件信息失败");
        }
        log.debug("保存文件信息到数据库成功,{}",mediaFiles.toString());

    }
    return mediaFiles;

}
@Transactional
@Override
public UploadFileResultDto uploadFile(Long companyId, UploadFileParamsDto uploadFileParamsDto, String localFilePath) {
    File file = new File(localFilePath);
    if (!file.exists()) {
        XueChengPlusException.cast("文件不存在");
    }
    //文件名称
    String filename = uploadFileParamsDto.getFilename();
    //文件扩展名
    String extension = filename.substring(filename.lastIndexOf("."));
    //文件mimeType
    String mimeType = getMimeType(extension);
    //文件的md5值
    String fileMd5 = getFileMd5(file);
    //文件的默认目录
    String defaultFolderPath = getDefaultFolderPath();
    //存储到minio中的对象名(带目录)
    String  objectName = defaultFolderPath + fileMd5 + exension;
    //将文件上传到minio
    boolean b = addMediaFilesToMinIO(localFilePath, mimeType, bucket_files, objectName);
    //文件大小
    uploadFileParamsDto.setFileSize(file.length());
    //将文件信息存储到数据库
    MediaFiles mediaFiles = addMediaFilesToDb(companyId, fileMd5, uploadFileParamsDto, bucket_files, objectName);
    //准备返回数据
    UploadFileResultDto uploadFileResultDto = new UploadFileResultDto();
    BeanUtils.copyProperties(mediaFiles, uploadFileResultDto);
    return uploadFileResultDto;

}
```

### **6.6 Service事务优化，**有网络访问的业务不要用Spring的事务控制

目前是在uploadFile方法上添加@Transactional，当调用uploadFile方法前会开启数据库事务。

1.  优化前：整个上传图片业务@Transactional。导致上传文件到minIO时，数据库事务也在开启状态。Spring事务的本质其实就是数据库对事务的支持，它本身并不实现事务。有网络访问的业务千万不能用Spring的事务控制，防止网络延迟导致数据库事务持续时间过长，导致数据库一直被占用。
    
2.  优化后：仅添加数据库时@Transactional。
    

如果上传文件过程时间较长那么数据库的事务持续时间就会变长，这样数据库链接释放就慢，最终导致数据库链接不够用。

我们**只将addMediaFilesToDb方法添加事务控制即可**,uploadFile方法上的@Transactional注解去掉。

```java
@Transactional
public MediaFiles addMediaFilesToDb(Long companyId,String fileMd5,UploadFileParamsDto uploadFileParamsDto,String bucket,String objectName){

   //从数据库查询文件
MediaFiles mediaFiles = mediaFilesMapper.selectById(fileMd5);
if (mediaFiles == null) {
    mediaFiles = new MediaFiles();
    //拷贝基本信息
    BeanUtils.copyProperties(uploadFileParamsDto, mediaFiles);
    mediaFiles.setId(fileMd5);
    mediaFiles.setFileId(fileMd5);
    mediaFiles.setCompanyId(companyId);
    mediaFiles.setUrl("/" + bucket + "/" + objectName);
    mediaFiles.setBucket(bucket);
    mediaFiles.setFilePath(objectName);
    mediaFiles.setCreateDate(LocalDateTime.now());
    mediaFiles.setAuditStatus("002003");
    mediaFiles.setStatus("1");
    //保存文件信息到文件表
    int insert = mediaFilesMapper.insert(mediaFiles);
    if (insert < 0) {
        log.error("保存文件信息到数据库失败,{}",mediaFiles.toString());
        XueChengPlusException.cast("保存文件信息失败");
    }
    log.debug("保存文件信息到数据库成功,{}",mediaFiles.toString());

}
return mediaFiles;

}
```