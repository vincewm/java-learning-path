>  **导航：**
>
>  [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})
>
>  Maven高级：[Maven高级_java relativepath_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126445624) 

[TOC]



# 一、构建工具Maven

## 1.1 简介

**Maven**是专门用于**管理和构建Java项目**的工具。

**传统项目管理缺点：**

1.jar包版本不统一、不兼容

2.工程升级维护过程操作繁琐

**Maven介绍：**

Maven 的本质是一个**项目管理工具**，将项目开发和管理过程抽象成一个项目对象模型（POM）。

maven是用java语言写的，它管理的项目都以面对对象形式设计，最终**把一个项目看成一个对象**，即POM。

**POM:**

POM（Project Object Model）：项目对象模型

### 1.1.1 作用和功能

**作用：**

**项目构建：**提供标准的、**跨平台**的自动化项目构建方式

**依赖管理：**方便快捷的管理项目依赖的资源（jar包），避免资源间的版本冲突问题

**统一开发结构：**提供标准的、统一的项目结构

**功能：**

Maven是专门用于管理和构建Java项目的工具，它的主要功能有：

- **提供了一套标准化的项目结构**

每一个开发工具（IDE）都有自己不同的项目结构，它们互相之间不通用。

而Maven提供了一套标准化的项目结构，**所有的IDE使用Maven构建的项目完全一样**，所以IDE创建的Maven项目可以通用。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/32a99c6beb9c42a2a09f9d32a7e4051b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **提供了一套标准化的构建流程（编译，测试，打包，发布……）**

![img](JavaWeb基础3——Maven基础&MyBatis.assets/638a130ec1874256991de06c02444f04.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **提供了一套依赖管理机制**

Maven使用标准的**坐标**配置来管理各种依赖， 只需要简单的配置就可以完成依赖管理：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/825cd7e723704ae5b67bcce18ed31f3c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 1.1.2 Maven模型

- 项目对象模型pom (Project Object Model)
- 依赖管理模型(Dependency)
- 插件(Plugin)

![img](JavaWeb基础3——Maven基础&MyBatis.assets/c2c442ad43d24bc7b3588895cded3401.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**项目对象模型pom**就是将我们自己抽象成一个对象模型，有自己专属的坐标，是唯一标识。

项目对象模型pom通过xml格式保存的pom.xml文件。该文件用于管理：源代码、配置文件、开发者的信息和角色、问题追踪系统、组织信息、项目授权、项目的url、项目的依赖关系等等。

如下图所示是一个Maven项目：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/762aa50fdb9a4c5c873c710e252db847.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) **依赖管理模型**则是使用坐标来描述当前项目依赖哪些第三方jar包，如下图所示：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/93922f56c78a4857b7405c4bf44da00f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 项目管理模型和依赖管理模型结合起来，体现Maven方便的依赖管理。



**构建生命周期和插件部分**用来完成 **`标准化构建流程`** 。

如我们需要**编译**，Maven提供了一个编译插件供我们使用。我们需要**打包**，Maven就提供了一个打包插件提供我们使用等。  

### 1.1.3 仓库

Maven用坐标配置管理依赖。

依赖jar包则其实存储在本地仓库中，项目运行时从本地仓库中拿需要的依赖jar包。



- **本地仓库**：自己电脑上存储资源的仓库（是个目录），连接远程仓库获取资源
- **中央仓库**：由Maven团队维护的全球唯一的仓库，Maven团队维护，存储所有资源的仓库
  - 地址： [Central Repository:](https://repo1.maven.org/maven2/)
- **远程仓库(私服)**：一般由公司团队搭建的私有仓库。部门/公司范围内存储资源的仓库，从中央仓库获取资源

**私服的作用：**

- 保存具有版权的资源，包含购买或自主研发的jar。中央仓库中的jar都是开源的，不能存储具有版权的资源
- 一定范围内共享资源，仅对内部开放，不对外共享



当项目中使用坐标引入对应依赖jar包后，首先会查找本地仓库中是否有对应的jar包：

- 如果有，则在项目直接引用;
- 如果没有，则去中央仓库中下载对应的jar包到本地仓库。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/9caef45c0d3249339575dbb6127a3487.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如果还可以搭建远程仓库，将来jar包的查找顺序则变为：

> 本地仓库 --> 远程仓库--> 中央仓库

![img](JavaWeb基础3——Maven基础&MyBatis.assets/d5b72bc176ca4ba4848972962a12ff53.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.1.4 Maven 坐标详解

**什么是坐标？**

- Maven 中的坐标是**资源的唯一标识**
- 使用坐标来定义项目或引入项目中需要的依赖

**所有坐标官网（需要梯子）：**

https://mvnrepository.com/

![img](JavaWeb基础3——Maven基础&MyBatis.assets/9a7028c21b834009aa75abce90b96a64.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](JavaWeb基础3——Maven基础&MyBatis.assets/52683fcf4a604819b0ed68f274f1fd6a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**Maven 坐标主要组成**

- groupId：定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.itheima）

- artifactId：定义当前Maven项目名称（通常是模块名称，例如 order-service、goods-service）

- version：定义当前项目版本号

- scope：范围，像Servlet、jsp依赖都需要设置范围为provided

  ```XML
  <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <!--
        此处为什么需要添加该标签?
        provided指的是在编译和测试过程中有效,在运行时无效，最后生成的war包时不会加入
         因为Tomcat的lib目录中已经有servlet-api这个jar包，如果在生成war包的时候生效就会和Tomcat中的jar包冲突，导致报错
      -->
      <scope>provided</scope>
  </dependency>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  



> **注意：**
>
> - 上面所说的资源可以是插件、依赖、当前项目。
> - 我们的项目如果被其他的项目依赖时，也是需要坐标来引入的。



## 1.2 Maven安装配置

**1.下载**

官方下载链接：https://maven.[apache](https://so.csdn.net/so/search?q=apache&spm=1001.2101.3001.7020).org/download.cgi

Binary是可执行版本，已经编译好可以直接使用。
 Source是源代码版本，需要自己编译成可执行软件才可使用。

我们选择已经编译好的windows可执行版本进行安装：选择zip版本(linux选择tar.gz)

**2.配置环境变量：**

![img](JavaWeb基础3——Maven基础&MyBatis.assets/d87f852d32414bf9a2ff9cddd900f8e2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础3——Maven基础&MyBatis.assets/5d7b4e87aee442bd91ce886b066122e1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **3.配置本地仓库**

 修改 D:\apache-maven-3.8.6\conf/settings.xml 中的 <localRepository> 为一个指定目录（例如D:\apache-maven-3.8.6\mvn_resp）作为本地仓库，用来存储jar包。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/1d2e6f9adefb4d4da72578a49684f81f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```XML
<localRepository>D:\apache-maven-3.8.6\mvn_resp</localRepository>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **4.配置jdk**

默认使用jdk1.4，太老，可能会出问题要手动配置：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/a210e147d76943abab5034b6a1202c1d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



将下面代码加到<profiles >

```XML
	  <profile>  
		 <id>jdk-1.8</id>  
		 <activation>  
			 <activeByDefault>true</activeByDefault>  
			 <jdk>1.8</jdk>  
		 </activation>
		 <properties>
			 <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
			 <maven.compiler.source>1.8</maven.compiler.source>  
			 <maven.compiler.target>1.8</maven.compiler.target>   
		 </properties>   
		</profile>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**4.配置阿里云私服:**

中央仓库在国外，所以下载jar包速度可能比较慢，而阿里公司提供了一个远程仓库，里面基本也都有开源项目的jar包。

修改 conf/settings.xml 中的 <mirrors>标签，为其添加如下子标签：

```XML
<mirror>  
    <id>alimaven</id>  
    <name>aliyun maven</name>  
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>          
</mirror>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 1.3 Maven基本使用

### 1.3.1 Maven常用命令

- compile ：编译，生成target目录
- clean：清理，删除target目录
- test：测试，执行test文件下测试代码
- package：打包，将当前项目打包成的jar包
- install：安装，将当前项目打成jar包，并安装到本地仓库

![img](JavaWeb基础3——Maven基础&MyBatis.assets/5575c75c956248ea94d643c644cdd431.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**编译命令演示：**

命令行运行**mvn compile。**

首次编译会先从阿里云（之前conf/settings.xml配置了阿里云私服）下载编译需要插件的jar包，在本地仓库（之前conf/settings.xml配置了本地仓库位置）也能看到下载好的插件。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/68964d433bca46c69d95e4343a0765cd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在项目下会生成一个 `target` 目录，里面保存编译后的字节码文件。

 ![img](JavaWeb基础3——Maven基础&MyBatis.assets/13b8974d28914a4baa2cbd25b3abbadf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**清理命令演示：**

```
mvn clean
```

执行上述命令可以看到

- 从阿里云下载清理需要的插件jar包
- 删除项目下的 `target` 目录



### 1.3.2 Maven 生命周期

![img](JavaWeb基础3——Maven基础&MyBatis.assets/2da5e14e32a6436da50099a4ba44ddc6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **简洁版：**
>
> - **clean：**清理上次构建结果
> - **valide：**校验工程信息是否正确
> - **comple：**编译工程
> - **test：**执行工程测试流程(标注的test的程序)
> - **package：**打包工程
> - **verify：**验证包的有效性
> - **install：**安装包到本地仓库
> - **deploy：**推送包到远程仓库

Maven 构建项目生命周期描述的是一次构建过程经历经历了多少个事件

Maven 对项目构建的生命周期划分为3套：

- **clean ：**项目清理的处理，移除所有上一次构建生成的文件。
- **default(或 build)** ：核心工作，例如编译，测试，打包，安装等。
- **site** ： 产生报告，发布站点等。这套生命周期一般不会使用。



**Clean 生命周期**

当我们执行 mvn post-clean 命令时，Maven 调用 clean 生命周期，它包含以下阶段：

- pre-clean：执行一些需要在clean之前完成的工作
- clean：移除所有上一次构建生成的文件
- post-clean：执行一些需要在clean之后立刻完成的工作

**default生命周期** 

| 阶段          | 处理     | 描述                                                     |
| ------------- | -------- | -------------------------------------------------------- |
| 验证 validate | 验证项目 | 验证项目是否正确且所有必须信息是可用的                   |
| 编译 compile  | 执行编译 | 源代码编译在此阶段完成                                   |
| 测试 Test     | 测试     | 使用适当的单元测试框架（例如JUnit）运行测试。            |
| 包装 package  | 打包     | 创建JAR/WAR包如在 pom.xml 中定义提及的包                 |
| 检查 verify   | 检查     | 对集成测试的结果进行检查，以保证质量达标                 |
| 安装 install  | 安装     | 安装打包的项目到本地仓库，以供其他项目使用               |
| 部署 deploy   | 部署     | 拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程 |

> **注意：**
>
> - **打包前先clean是好习惯，能够保证上一次构建的输出不会影响到本次构建。**
> - **同一套生命周期内，执行后边的命令，前面的所有命令会自动执行。例如执行安装会先执行打包。**

![img](JavaWeb基础3——Maven基础&MyBatis.assets/5e95d72e561744c1990882dafc81e62c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础3——Maven基础&MyBatis.assets/fc80eaeb72b741cbb5a60a547e8ee8e6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **site构建生命周期：**



- pre-site：执行一些需要在生成站点文档之前完成的工作
- site：生成项目的站点文档
- post-site： 执行一些需要在生成站点文档之后完成的工作，并且为部署做准备
- site-deploy：将生成的站点文档部署到特定的服务器上



## 1.4 IDEA使用Maven

### 1.4.1 IDEA配置Maven环境

> **注意：**一定要先file-close project**关闭项目**， 然后再设置，就是全局设置，否则仅本项目内生效。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/81fe06bed3c14a5a89203ce21263b8da.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

设置 IDEA 使用本地安装的 Maven，并修改配置文件路径，记得apply： 

![img](JavaWeb基础3——Maven基础&MyBatis.assets/b78d058d3719475aaf99a96e32d4bb2d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

apply再ok。 

### 1.4.2 IDEA 创建 Maven项目

file-new module-选择构建Maven、jdk版本最好大于1.5：

> 也可以先创建空项目，在项目内创建Maven模块。
>
> 下面生成器Maven archetype（原型）是创建Maven web的，在下下一篇讲Tomcat时会用到

![img](JavaWeb基础3——Maven基础&MyBatis.assets/f13417cf3d5b4c3c9054b32161d95142.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





填写模块名称，坐标信息，点击finish，创建完成  

![img](JavaWeb基础3——Maven基础&MyBatis.assets/4563a70fc2fa4786a65622ac3b24aae3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 创建好的项目目录结构如下：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/e8d6773aff0f44b4aae7e081c5d63c94.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

然后在java文件夹下建包，创建类 

**导入Maven项目**：open-双击项目的pom.xml文件即可

### 1.4.3 pom.xml解释

此阶段packaging不用设置，默认是打包成jar包，以后创建Maven web时候要配置成war。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/518d6ade61bf4c43b394cc94b85618e2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





### 1.4.4 IDEA创建Maven web项目

现阶段还用不到，将在Tomcat的文章里详细书写：

[JavaWeb基础5——HTTP&Tomcat&Servlet_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/125970595?spm=1001.2014.3001.5501)



### **1.4.5 配置 Maven-Helper 插件**

Maven-Helper可以右键Maven项目，直接run Maven和调试。

File --> Settings--Plugins--搜索 Maven，选择第一个 Maven Helper，点击Install安装，弹出面板中点击Accept--重启

![img](JavaWeb基础3——Maven基础&MyBatis.assets/03b3665e5e4f4946b50389511d01339a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 1.4.6 编码设置，报错解决

打包时出现编码错误：

**彻底解决：**全部编码设置成utf-8 

![img](JavaWeb基础3——Maven基础&MyBatis.assets/c8a31840cda743139ee90bd6b100e14d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 **单文件解决：** 

 在pom.xml配置如下代码，适用于项目要在不同项目移动：

```XML
<properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.encoding>UTF-8</maven.compiler.encoding>
        <java.version>11</java.version>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
 </properties>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





## 1.5 依赖管理

### **1.5.1 依赖概述**

**依赖**

依赖指当前项目运行所需的jar，一个项目可以设置多个依赖。

groupId：依赖所属群组id。

artifactId：依赖所属项目id。

version：依赖版本号。

scope：依赖生效范围。

optional：为true时是可选依赖，指对外隐藏当前所依赖的资源——不透明。设置后其他依赖引用本项目时候将无法看到这个依赖。控制别人能不能看到你用到你。

exclusions-exclusion：排除依赖指主动断开依赖的资源，被排除的资源无需指定版本。控制你引用的项目中需要排除的依赖。

**依赖范围scope**

依赖的jar默认在任何地方使用，通过scope便签设定其范围。

通过设置坐标的依赖范围(scope)，可以设置对应jar包的作用范围：编译环境、测试环境、运行环境。

如下图所示给 `junit` 依赖通过 `scope` 标签指定依赖的作用范围。 那么这个依赖就只能作用在测试环境，其他环境下不能使用。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/e3b8a97d5bf645b281219863eec86946.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**依赖范围scope可取值：**

| **依赖范围** | 编译classpath | 测试classpath | 运行classpath | 例子              |
| ------------ | ------------- | ------------- | ------------- | ----------------- |
| **compile**  | Y             | Y             | Y             | logback           |
| **test**     | -             | Y             | -             | Junit             |
| **provided** | Y             | Y             | -             | servlet-api       |
| **runtime**  | -             | Y             | Y             | jdbc驱动          |
| **system**   | Y             | Y             | -             | 存储在本地的jar包 |

配置后可以在依赖中看到：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/39e170c8e40d408e900a9bda951307be.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**依赖具有传递性**

**直接依赖**：在当前项目中通过依赖配置建立的依赖关系

**间接依赖**：被资源的资源如果依赖其他资源，当前项目间接依赖其他资源
 ![img](JavaWeb基础3——Maven基础&MyBatis.assets/4a770eb3bf6a4c78b1690a6f11ff7483.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​编辑

**project2直接引用project3依赖** 

![img](JavaWeb基础3——Maven基础&MyBatis.assets/d4097031263c408589934bb0956db19a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**依赖传递冲突问题**

**路径优先：**当依赖中出现相同的资源时，层级越深，优先级越低，层级越浅，优先级越高

**声明优先：**当资源在相同层级被依赖时，配置顺序靠前的覆盖配置顺序靠后的

**特殊优先：**当同级配置了相同资源的不同版本，**后配置的覆盖先配置的**

![img](JavaWeb基础3——Maven基础&MyBatis.assets/4b0a9fd916c34766b0facdf8b9c9b1eb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**可选依赖**optional

可选依赖指对外隐藏当前所依赖的资源——不透明

![img](JavaWeb基础3——Maven基础&MyBatis.assets/aef94648fbd44c44b75a5aad56a02a15.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**排除依赖**exclusions-exclusion

排除依赖指主动断开依赖的资源，被排除的资源无需指定版本

 ![img](JavaWeb基础3——Maven基础&MyBatis.assets/026749534e29480c856020f43a6a4961.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 1.5.2 导入依赖

1.点击底栏依赖：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/8e70c28b8d5e4d2fbd1dc2f8cc7aed65.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



或者在pom.xml使用alt+insert快捷键，点击添加依赖项：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/ae6157fd146740008fa2ef96b681c91b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.搜索需要导入的依赖项，点击添加导入：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/a65e892c58be4cf38ac2af7c906d340d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **1.5.3 依赖jar包引用，设置自动刷新**

**使用坐标引入依赖的jar包**

1.在项目的 pom.xml 中编写 <dependencies> 标签

2.在 <dependencies> 标签中 使用 <dependency> 引入坐标

3.定义坐标的 groupId，artifactId，version

> **groupId：**定义当前[Maven](https://so.csdn.net/so/search?q=Maven&spm=1001.2101.3001.7020)项目隶属的实际项目。
>
> 例如org.sonatype.nexus，此id前半部分org.sonatype代表此项目隶属的组织或公司，后部分代表项目的名称。
>
> 如果此项目多模块话开发的话就子模块可以分为org.sonatype.nexus.plugins和org.sonatype.nexus.utils等。特别注意的是groupId不应该对应项目隶属的组织或公司，也就是说groupId不能只有org.sonatype而没有nexus。
>
> 
>
> **artifactId：**构件ID。该元素定义实际项目中的一个Maven项目或者是子模块，如上面官方约定中所说，**构建名称必须小写字母，没有其他的特殊字符**，推荐使用“**实际项目名称－模块名称**”的方式定义，例如：spirng-mvn、spring-core等。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/f079d8baf18a4ebd824871fba28b2a9b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](JavaWeb基础3——Maven基础&MyBatis.assets/a0069af968d84b03af7babc451f09915.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





点击刷新按钮，使坐标生效

 ![img](JavaWeb基础3——Maven基础&MyBatis.assets/573c71460fff444c8bf113d53cd46b9d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> 注意：
>
> - 具体的坐标我们可以到如下网站进行搜索
> - https://mvnrepository.com/

**设置自动刷新：**

File --> Settings---Build Tools---any changes

![img](JavaWeb基础3——Maven基础&MyBatis.assets/e7ab5d6163e84adc80f57e1923777d1f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**快捷方式引入jar包**

1.在 pom.xml 中 按 alt + insert，选择 Dependency

![img](JavaWeb基础3——Maven基础&MyBatis.assets/98f44f85e66c45ad9ec6fa587d773fe2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





2.在弹出的面板中搜索对应坐标，然后双击选中对应坐标

![img](JavaWeb基础3——Maven基础&MyBatis.assets/b03c04f9c8034c8a963bb1c94e285eaf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



3.点击刷新按钮，使坐标生效



## 1.6 插件

**插件**

- 插件与生命周期内的阶段绑定，在执行到对应生命周期时执行对应的插件功能。
- 默认maven在各个生命周期上绑定有预设的功能。
- 通过插件可以自定义其他功能。

**示例：Tomcat部署的插件**

```XML
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
      </plugin>
    </plugins>
  </build>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 二、Mybatis

## 2.1 Mybatis概述

### 2.1.1 Mybatis、持久层、框架简介

[MyBatis中文网](https://mybatis.net.cn/)

- MyBatis 是一款优秀的**持久层框架**，用于**简化 JDBC 开发**
- MyBatis 本是 Apache 的一个开源项目iBatis, 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。2013年11月迁移到Github
- 官网：[mybatis – MyBatis 3 | 简介](https://mybatis.org/mybatis-3/zh/index.html)

**持久层：**

- 负责将数据保存到数据库的那一层代码。

  以后开发我们会**将操作数据库的Java代码作为持久层**。而**Mybatis就是对jdbc代码进行了封装**。

- JavaEE三层架构：表现层做页面展示、业务层做逻辑处理、持久层对数据持久化

- 下图是持久层框架的使用占比。

  ![img](JavaWeb基础3——Maven基础&MyBatis.assets/954dd4c3496a42249c71083562fd3e1e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**框架：**

- 框架就是一个半成品软件，是一套**可重用的、通用的、软件基础代码模型**
- 在框架的基础之上构建软件编写更加高效、规范、通用、可扩展

### 2.1.2 Mybatis对比JDBC

**JDBC 缺点**

下面是 JDBC 代码，我们通过该代码分析都存在什么缺点：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/26eb553deed5416d819409d6d2fa270e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





- 硬编码

  - 注册驱动、获取连接

    上图标1的代码有很多字符串，而这些是连接数据库的四个基本信息，以后如果要将Mysql数据库换成其他的关系型数据库的话，这四个地方都需要修改，如果放在此处就意味着要修改我们的源代码。

  - SQL语句

    上图标2的代码。如果表结构发生变化，SQL语句就要进行更改。这也不方便后期的维护。

- 操作繁琐

  - 手动设置参数

  - 手动封装结果集

    上图标4的代码是对查询到的数据进行封装，而这部分代码是没有什么技术含量，而且特别耗费时间的。

**Mybatis 优化**

- **硬编码**可以配置到**配置文件**
- 操作繁琐的地方mybatis都**自动完成**

如图所示

![img](JavaWeb基础3——Maven基础&MyBatis.assets/28e9e422a1774914a9eba665072e9df6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 2.2 核心配置文件mybatis-config.xml

核心配置文件标签必须有向后顺序（相比之下，SQL映射配置文件的同级标签没有先后顺序），如下：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/2f1da003493f48d4961672caedf6fbcf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.2.1 configuration【根标签】

所有子标签均需书写在当前根标签内部

示例：

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--根标签configuration-->
<configuration>
<!--    typeAliases类型别名-->
<!--    指定一个包名，MyBatis 会在包名下面搜索需要的 Java Bean-->
    <typeAliases>
        <package name="package1.pojo"/>
    </typeAliases>

    <!--
    environments：配置数据库连接环境信息。可以配置多个environment，通过default属性切换不同的environment
    尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。
    -->
<!--    default是每个environment默认使用的环境 ID-->
    <environments default="development">
<!--        指定每个 environment 元素定义的环境 ID-->
<!--        注意：环境可以随意命名，但务必保证默认的环境 ID 要匹配其中一个环境 ID。-->
        <environment id="development">
<!--            事务管理器transactionManager的配置，不用太在意，事务管理之后是用Spring接管-->
<!--            在 MyBatis 中有两种类型的事务管理器（也就是 type="[JDBC|MANAGED]"）：-->

<!--            JDBC – 这个配置直接使用了 JDBC 的提交和回滚设施，它依赖从数据源获得的连接来管理事务作用域。-->
<!--            MANAGED – 这个配置几乎没做什么。它从不提交或回滚一个连接，而是让容器来管理事务的整个生命周期（比如 JEE 应用服务器的上下文）。 默认情况下它会关闭连接。然而一些容器并不希望连接被关闭，因此需要将 closeConnection 属性设置为 false 来阻止默认的关闭行为。-->
            <transactionManager type="JDBC"/>
<!--            数据源dataSource 元素使用标准的 JDBC 数据源接口来配置 JDBC 连接对象的资源。-->

<!--            大多数 MyBatis 应用程序会按示例中的例子来配置数据源。虽然数据源配置是可选的，但如果要启用延迟加载特性，就必须配置数据源。-->
<!--            有三种内建的数据源类型（也就是 type="[UNPOOLED|POOLED|JNDI]"）：-->
<!--            POOLED– 这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间。-->
<!--            UNPOOLED– 这个数据源的实现会每次请求时打开和关闭连接。-->
<!--            JNDI – 这个数据源实现是为了能在如 EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的数据源引用。-->
            <dataSource type="POOLED">
                <!--数据库连接信息-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <!--加载sql映射文件，告诉MyBatis 去哪寻找映射SQL 的语句。-->
<!--        Maven项目编译后，java和resources下的目录和文件都在同一个跟目录下，所以路径是这样的，注意路径是/，不是.-->
<!--        <mapper resource="UserMapper.xml"/>-->
<!--        <mapper resource="package1/mapper/UserMapper.xml"/>-->
<!--        扫描包指定name的包下所有mapper配置文件-->
        <package name="package1.mapper"/>
    </mappers>
</configuration>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.2 properties【属性标签】

作用：**将数据库配置属性从dataSource标签内部提取到外部**
 属性：
 resource：设置外部属性文件类路径
 url：设置外部属性文件真实路径

示例：

```XML
<!--    属性标签-->
    <properties resource="druid.properties"></properties>
    
    <!--    设置数据库环境-->
    <environments default="development">
        <environment id="development">
            <!--设置事务管理器-->
            <transactionManager type="JDBC"/>
            <!--设置数据源-->
            <dataSource type="POOLED">
                <property name="driver" value="${driverClassName}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
<!--                <property name="initialSize" value="${initialSize}"/>-->
            </dataSource>
        </environment>
    </environments>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.3 settings【设置标签】

作用： 是mybatis中极为重要的调整设置，他们会**改变mybatis的运行时行为**

mapUnderscoreToCamelCase：开启驼峰命名自动映射，即从经典数据库列名 A_COLUMN 映射到经典 Java 属性名 aColumn。
 默认值为false,当设置为true时开启驼峰命名
 注意：只能将a_bc与aBc自动映射，不能将a_b与aBc自动映射

示例代码

```XML
<settings>
        <!--开启驼峰式命名自动映射-->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
</settings>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.4 **typeAliases【类型别名】**

**alias译为别名**
 作用 ：类型别名可为 Java 类型设置一个缩写名字。 它仅用于 XML 配置，意在降低冗余的全限定类名书写。
 自定义别名

```XML
<typeAliases>
  <typeAlias alias="Author" type="domain.blog.Author"/>
  <typeAlias alias="Blog" type="domain.blog.Blog"/>
  <typeAlias alias="Comment" type="domain.blog.Comment"/>
  <typeAlias alias="Post" type="domain.blog.Post"/>
  <typeAlias alias="Section" type="domain.blog.Section"/>
  <typeAlias alias="Tag" type="domain.blog.Tag"/>
</typeAliases>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

也可以指定一个包名进行扫描，MyBatis 会在包名下面搜索需要的 Java Bean，比如：

```XML
<!--    typeAliases类型别名-->
<!--    给指定name包下的所有类起一个别名，-->
    <typeAliases>
        <package name="package1.pojo"/>
    </typeAliases>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这样sql映射文件resultType属性就可以省略路径package1.pojo:

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--        映射配置文件 UserMapper.xml-->
<!--namespace名称空间，该命名空间和对应mapper接口的全限定名一致-->
<mapper namespace="package1.mapper.UserMapper">
<!--    resultType="User"或"user"也可以，因为核心配置文件中有给package1.pojo起别名，且有别名后不区分大小写-->
    <select id="selectAll" resultType="package1.pojo.User">
        select * from tb_user;
    </select>
</mapper>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.2.5 typeHandlers【类型处理器】

### 2.2.6 objectFactory【对象工厂】

### 2.2.7 plugins（插件）

### 2.2.8 **environments【数据库环境设置】**

作用：**配置数据库连接环境信息。**

> - 可以配置多个environment。
> - 环境可以随意命名，但务必保证默认的环境 ID 要匹配其中一个环境 ID。这样通过default属性切换不同的environment环境**。**
> - 尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。

**environments**属性default是每个environment默认使用的环境 ID

**environment**属性id是指定该 environment 元素定义的环境 ID。

**事务管理器transactionManager**属性type有两种：

```
JDBC – 这个配置直接使用了 JDBC 的提交和回滚设施，它依赖从数据源获得的连接来管理事务作用域。
MANAGED – 这个配置几乎没做什么。它从不提交或回滚一个连接，而是让容器来管理事务的整个生命周期（比如 JEE 应用服务器的上下文）。 默认情况下它会关闭连接。然而一些容器并不希望连接被关闭，因此需要将 closeConnection 属性设置为 false 来阻止默认的关闭行为。
数据源dataSource 元素使用标准的 JDBC 数据源接口来配置 JDBC 连接对象的资源,type有三种：
POOLED– 这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间。
UNPOOLED– 这个数据源的实现会每次请求时打开和关闭连接。
JNDI – 这个数据源实现是为了能在如 EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的数据源引用。
```

示例：

```XML
    <!--
    environments：配置数据库连接环境信息。可以配置多个environment，通过default属性切换不同的environment
    尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。
    -->
<!--    default是每个environment默认使用的环境 ID-->
    <environments default="development">
<!--        指定每个 environment 元素定义的环境 ID-->
<!--        注意：环境可以随意命名，但务必保证默认的环境 ID 要匹配其中一个环境 ID。-->
        <environment id="development">
<!--            事务管理器transactionManager的配置，不用太在意，事务管理之后是用Spring接管-->
<!--            在 MyBatis 中有两种类型的事务管理器（也就是 type="[JDBC|MANAGED]"）：-->

<!--            JDBC – 这个配置直接使用了 JDBC 的提交和回滚设施，它依赖从数据源获得的连接来管理事务作用域。-->
<!--            MANAGED – 这个配置几乎没做什么。它从不提交或回滚一个连接，而是让容器来管理事务的整个生命周期（比如 JEE 应用服务器的上下文）。 默认情况下它会关闭连接。然而一些容器并不希望连接被关闭，因此需要将 closeConnection 属性设置为 false 来阻止默认的关闭行为。-->
            <transactionManager type="JDBC"/>
<!--            数据源dataSource 元素使用标准的 JDBC 数据源接口来配置 JDBC 连接对象的资源。-->

<!--            大多数 MyBatis 应用程序会按示例中的例子来配置数据源。虽然数据源配置是可选的，但如果要启用延迟加载特性，就必须配置数据源。-->
<!--            有三种内建的数据源类型（也就是 type="[UNPOOLED|POOLED|JNDI]"）：-->
<!--            POOLED– 这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间。-->
<!--            UNPOOLED– 这个数据源的实现会每次请求时打开和关闭连接。-->
<!--            JNDI – 这个数据源实现是为了能在如 EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的数据源引用。-->
            <dataSource type="POOLED">
                <!--数据库连接信息-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.9 databaseIdProvider（数据库厂商标识）

### 2.2.10 mappers 【映射器】


 作用：加载映射文件


```XML
    <mappers>
        <!--加载sql映射文件，告诉MyBatis 去哪寻找映射SQL 的语句。-->
        <mapper resource="UserMapper.xml"/>
    </mappers>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

也可以扫描包寻找sql映射文件文件，推荐这种方法

```XML
    <mappers>
        <!--扫描mapper-->
        <package name="package1.mapper"/>
    </mappers>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.3 Mybatis入门案例（不用mapper）

### 2.3.1 代码实现

**需求：查询user表中所有的数据**

![img](JavaWeb基础3——Maven基础&MyBatis.assets/e824eee9518f471fad4d26cd9df79d04.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**1.创建user表，添加数据**

```sql
create database mybatis;
use mybatis;

drop table if exists tb_user;

create table tb_user(
    id int primary key auto_increment,
    username varchar(20),
    password varchar(20),
    gender char(1),
    addr varchar(30)
);

INSERT INTO tb_user VALUES (1, 'zhangsan', '123', '男', '北京');
INSERT INTO tb_user VALUES (2, '李四', '234', '女', '天津');
INSERT INTO tb_user VALUES (3, '王五', '11', '男', '西安');
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2.创建模块，导入坐标**

在创建好的模块中的 pom.xml 配置文件中添加依赖的坐标:

其实依赖**只需要导入mybatis,mysql即可，其他是日志、测试之类的**。

```XML
<dependencies>
    <!--mybatis 依赖-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.5</version>
    </dependency>

    <!--mysql 驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.46</version>
    </dependency>

    <!--junit 单元测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13</version>
        <scope>test</scope>
    </dependency>

    <!-- 添加slf4j日志api -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.20</version>
    </dependency>
    <!-- 添加logback-classic依赖 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <!-- 添加logback-core依赖 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-core</artifactId>
        <version>1.2.3</version>
    </dependency>
</dependencies>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**需要在项目的 resources 目录下创建logback的配置文件

```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!--
        CONSOLE ：表示当前的日志信息是可以输出到控制台的。
    -->
    <appender name="Console" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>[%level]  %cyan([%thread]) %boldGreen(%logger{15}) - %msg %n</pattern>
        </encoder>
    </appender>
<!--    这里要改，包名-->
    <logger name="package1" level="DEBUG" additivity="false">
        <appender-ref ref="Console"/>
    </logger>


    <!--

      level:用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL 和 OFF
     ， 默认debug
      <root>可以包含零个或多个<appender-ref>元素，标识这个输出位置将会被本日志级别控制。
      -->
    <root level="DEBUG">
        <appender-ref ref="Console"/>
    </root>
</configuration>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



slf4j，simple logging facade for java的缩写，翻译为java的简单日志外观。slf4j是一个开源项目，它提供我们一个一致的API来使用不同的日志框架，比如： java.util.logging，logback，log4j等。slf4j使用户可以在运行时嵌入他们想使用的日志框架。从名字中可以看出，它其实使用的是facade设计模式来实现的。 

Logback是SpringBoot内置的日志处理框架,你会发现spring-boot-starter其中包含了spring-boot-starter-logging，该依赖内容就是 Spring Boot 默认的日志框架 logback。官方文档：http://logback.qos.ch/manual/

**3.编写 MyBatis 核心配置文件** -- > 替换连接信息 解决硬编码问题

在模块下的 resources 目录下创建mybatis的配置文件 `mybatis-config.xml`，内容如下：

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--根标签configuration-->
<configuration>
<!--    typeAliases类型别名-->
<!--    指定一个包名，MyBatis 会在包名下面搜索需要的 Java Bean-->
    <typeAliases>
        <package name="package1.pojo"/>
    </typeAliases>

    <!--
    environments：配置数据库连接环境信息。可以配置多个environment，通过default属性切换不同的environment
    尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。
    -->
<!--    default是每个environment默认使用的环境 ID-->
    <environments default="development">
<!--        指定每个 environment 元素定义的环境 ID-->
<!--        注意：环境可以随意命名，但务必保证默认的环境 ID 要匹配其中一个环境 ID。-->
        <environment id="development">
<!--            事务管理器transactionManager的配置-->
<!--            在 MyBatis 中有两种类型的事务管理器（也就是 type="[JDBC|MANAGED]"）：-->

<!--            JDBC – 这个配置直接使用了 JDBC 的提交和回滚设施，它依赖从数据源获得的连接来管理事务作用域。-->
<!--            MANAGED – 这个配置几乎没做什么。它从不提交或回滚一个连接，而是让容器来管理事务的整个生命周期（比如 JEE 应用服务器的上下文）。 默认情况下它会关闭连接。然而一些容器并不希望连接被关闭，因此需要将 closeConnection 属性设置为 false 来阻止默认的关闭行为。-->
            <transactionManager type="JDBC"/>
<!--            数据源dataSource 元素使用标准的 JDBC 数据源接口来配置 JDBC 连接对象的资源。-->

<!--            大多数 MyBatis 应用程序会按示例中的例子来配置数据源。虽然数据源配置是可选的，但如果要启用延迟加载特性，就必须配置数据源。-->
<!--            有三种内建的数据源类型（也就是 type="[UNPOOLED|POOLED|JNDI]"）：-->
<!--            POOLED– 这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间。-->
<!--            UNPOOLED– 这个数据源的实现会每次请求时打开和关闭连接。-->
<!--            JNDI – 这个数据源实现是为了能在如 EJB 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的数据源引用。-->
            <dataSource type="POOLED">
                <!--数据库连接信息-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <!--加载sql映射文件，告诉MyBatis 去哪寻找映射SQL 的语句。-->
<!--        Maven项目编译后，java和resources下的目录和文件都在同一个跟目录下，所以路径是这样的-->
        <mapper resource="UserMapper.xml"/>
    </mappers>
</configuration>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**4.编写 SQL 映射文件** --> 统一管理sql语句，解决硬编码问题

在模块的 `resources` 目录下创建映射配置文件 `UserMapper.xml`，内容如下：

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--        映射配置文件 UserMapper.xml-->
<!--namespace名称空间，该命名空间和对应mapper接口的全限定名一致-->
<mapper namespace="test">
    <select id="selectAll" resultType="package1.pojo.User">
        select * from tb_user;
    </select>
</mapper>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **另外，可通过resultMap实现对数据库列名起别名**，以解决数据库列名和User类属性命名法不对应问题（数据库标识符不区分大小写，采用下划线命名法，java标识符常用驼峰命名法）：
>
> ```XML
> <!--    统一起别名，resultMap标签的id为自定义的唯一标识，type为package1.pojo.User，若核心配置有typeAliases扫描pojo包，user-->
> <resultMap id="userResultMap" type="user">
> <!--        对数据库的指定列起别名-->
>   <result column="username" property="userName"/>
>   <result column="password" property="passWord"/>
> </resultMap>
> <!--    起别名了，resultType改成resultMap，值为上面resultMap的id-->
> <select id="selectAll" resultMap="userResultMap">
>   select * from tb_user;
> </select>
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**根标签**【mapper】
 作用：所用子标签均需书写在mapper内部
 namespace与接口全路径类名【类的全限定名】一致

 **八大子标签：**

insert：定义增加SQL语句
 delete：定义删除SQL语句
 update：定义修改语句
 select:定义查询SQL语句
 sql：定义SQL语句块
 resultMap：定义结果集映射【resultType解决不了时，使用resultMap】
 cache：定义缓冲类
 cache-ref：定义引用缓存

**5.在package1.pojo包下创建 User类**

[POJO](https://so.csdn.net/so/search?q=POJO&spm=1001.2101.3001.7020)(Plain Old Java Objects)译为，简单的Java对象，其实就是**没有从任何类继承、也没有实现任何接口，更没有被其它框架侵入的，没有遵从特定的Java对象模型、约定或框架（如EJB）的不受任何限制的java对象**。



```java
package package1.pojo;
//pojo译为，简单的Java对象.其实就是没有从任何类继承、也没有实现任何接口，更没有被其它框架侵入的，没有遵从特定的Java对象模型、约定或框架（如EJB）的不受任何限制的java对象。

public class User {
    private int id;
    private String username;
//下面两个passWord改成password
    private String passWord;
    private String gender;
    private String addr;

    //省略了 setter 和 getter

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", passWord='" + password + '\'' +
                ", gender='" + gender + '\'' +
                ", addr='" + addr + '\'' +
                '}';
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**6.在package1包下编写 MybatisDemo 测试类**

**步骤：**

```
1. 加载mybatis的核心配置文件，获取 SqlSessionFactory
```

session译为“会话”，factory译为“工厂”。

```
2. 获取SqlSession对象，用它来执行sql
3. 执行sql
4. 释放资源
```

**示例：**

**不用太花时间记，第三步执行SQL前的代码在所有案例中都是一样的，直接复制粘贴即可。而且整合Spring后就只剩mapper优化后的执行方法**

```java
public class Demo {

    public static void main(String[] args) throws IOException {
        //1. 加载mybatis的核心配置文件，获取 SqlSessionFactory
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

        //2. 获取SqlSession对象，用它来执行sql
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //3. 执行sql，这步不用记，一般这步都是使用mapper代理开发       sqlSession.getMapper(UserMapper.class);
        //参数是一个字符串，该字符串必须是映射配置文件的namespace.id
        List<User> users = sqlSession.selectList("test.selectAll");
        System.out.println(users);
        //4. 释放资源
        sqlSession.close();
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **回顾对比一下jdbc：**
>
> ```java
> /**
>  * 简单版
>  */
> public class Demo {
> 
>     public static void main(String[] args) throws Exception {
>         //1. 注册驱动
> 
>         //Class.forName("com.mysql.jdbc.Driver");//通过反射获取Driver实现类对象，从而加载驱动，注册驱动语句DriverManager.registerDriver(driver)在Driver的静态代码块里做过了。
>         //此句仅在mysql可省略，其他数据库不能省略
>         //2. 获取连接
>         String url = "jdbc:mysql://127.0.0.1:3306/db1?useSSL=false";
>         String username = "root";
>         String passWord = "1234";
>         Connection conn = DriverManager.getConnection(url, username, passWord);
>         //3. 定义sql
>         String sql = "update student set age = 80 where name='xiaohua'";
>         //4. 获取执行sql的对象 Statement
>         Statement stmt = conn.createStatement();
>         //5. 执行sql
>         int count = stmt.executeUpdate(sql);//受影响的行数
>         //6. 处理结果
>         System.out.println(count);
>         //7. 释放资源
>         stmt.close();
>         conn.close();
>     }
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.3.2 SqlSessionFactory工具类抽取

```java
String resource = "mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new 
	SqlSessionFactoryBuilder().build(inputStream);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

第三步执行SQL前的代码在所有案例中都是一样的，这些重复代码就会造成一些**问题:**

- 重复代码不利于后期的维护
- **SqlSessionFactory工厂类进行重复创建**
  - 就相当于每次买手机都需要重新创建一个手机生产工厂来给你制造一个手机一样，**资源消耗非常大但性能却非常低**。所以这么做是不允许的。





**解决方案**

- 代码重复可以**抽取工具类**
- 对指定代码只需要执行一次可以使用**静态代码块** 

> **注意：**
>
> ```java
> SqlSession sqlSession = sqlSessionFactory.openSession();
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 虽然上面语句也重复，但**不能抽取到工具类**里。因为SqlSession是一个连接、**会话**，每次连接数据库时候创建一次会话是合适，如果所有连接都共用一个会话会互相影响。
>
> SqlSession是一个**会话**，相当于JDBC中的一个Connection对象，Mybatis中所有的数据库交互都由SqlSession来完成。

**代码示例：**

**抽取工具类**

```java
public class SqlSessionFactoryUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        //静态代码块会随着类的加载而自动执行，且只执行一次
        //静态代码块不能抛异常，要用try-catch
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


    public static SqlSessionFactory getSqlSessionFactory(){
        return sqlSessionFactory;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**使用工具类**

```java
SqlSessionFactory sqlSessionFactory =SqlSessionFactoryUtils.getSqlSessionFactory();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.3.3 IDEA连接数据库 

**解决SQL映射文件的警告提示：**

在入门案例映射配置文件中存在报红的情况。问题如下：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/eb97cc15bfcb4f55b72c676f62138c5e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





- 产生的原因：Idea和数据库没有建立连接，不识别表信息。但是大家一定要记住，它并不影响程序的执行。
- 解决方式：在Idea中配置MySQL数据库连接。

**IDEA中配置MySQL数据库连接**

- 点击IDEA右边框的 `Database` ，在展开的界面点击 `+` 选择 `Data Source` ，再选择 `MySQL`

![img](JavaWeb基础3——Maven基础&MyBatis.assets/eeb8cd9e4ce5451a9dcadb717ab15361.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- 在弹出的界面进行基本信息的填写

![img](JavaWeb基础3——Maven基础&MyBatis.assets/538e8e11a78449edb8e04603346613c6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- 点击完成后就能看到数据库编译器界面
- 而此界面就和 `navicat` 工具一样可以进行数据库的操作。也可以编写SQL语句

另外，如果发现写表明时候没有提示：

**打开File的settings，把SQL Dialects选项的右边那个None改为你的默认数据库，我这边之前默认的是Generic SQL，然后我把它改回了我使用的mysql，之后就会有提示了。**

![img](JavaWeb基础3——Maven基础&MyBatis.assets/82bca1833abe44ae9e911fd436765634.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 2.4 Mapper代理开发

### 2.4.1 目的

**Mapper 代理方式的目的：**

- 解决原生方式中的硬编码
- 简化后期执行SQL

![img](JavaWeb基础3——Maven基础&MyBatis.assets/c6bfee517a7240ebb18cebc44cb3da92.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **2.4.2 使用mapper实现查询**

1.定义与SQL映射文件同名的Mapper接口，并且将Mapper接口和SQL映射文件放置在同一目录下。如下图放就可以，因为编译Maven后java和resources下的目录和文件都在同一个根目录下。

> 注意：在resources下建多层文件夹要用斜杠，例如aa/bb，不能aa.bb。如果直接建aa.bb，则只建了一个名为aa.bb的文件夹，而不是两个。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/846dcb2bb7b341e382acb3f9f2d42576.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](JavaWeb基础3——Maven基础&MyBatis.assets/ffbb65aa78b6429ea3818b05b6c9edd8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



2.设置SQL映射文件的namespace属性为Mapper接口全限定名：

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--        映射配置文件 UserMapper.xml-->
<!--namespace名称空间，该命名空间和对应mapper接口的全限定名一致-->
<mapper namespace="package1.mapper.UserMapper">
    <select id="selectAll" resultType="package1.pojo.User">
        select * from tb_user;
    </select>
</mapper>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



3.在 Mapper 接口中定义方法，方法名就是SQL映射文件中sql语句的id，并保持参数类型和返回值类型一致

![img](JavaWeb基础3——Maven基础&MyBatis.assets/ea01953b74b0430b927dda47334af89a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 4.Mapper代理开发

```java
public class Demo {

    public static void main(String[] args) throws IOException {
        //1. 加载mybatis的核心配置文件，获取 SqlSessionFactory
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

        //2. 获取SqlSession对象，用它来执行sql
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //3. 执行sql
        //参数是一个字符串，该字符串必须是映射配置文件的namespace.id
//        List<User> users = sqlSession.selectList("test.selectAll");
        //3.1获取UserMapper接口的代理对象
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        //3.2调用sql方法
        List<User> users = userMapper.selectAll();
        System.out.println(users);
        //4. 释放资源
        sqlSession.close();
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**如果Mapper接口名称和SQL映射文件名称相同，并在同一目录下，则可以使用在核心配置文件mybatis-config.xml中用**包扫描**的方式简化SQL映射文件的加载。示例：

```XML
    <mappers>
        <!--加载sql映射文件，告诉MyBatis 去哪寻找映射SQL 的语句。-->
<!--        Maven项目编译后，java和resources下的目录和文件都在同一个跟目录下，所以路径是这样的，注意路径是/，不是.-->
<!--        <mapper resource="UserMapper.xml"/>-->
        <mapper resource="package1/mapper/UserMapper.xml"/>
    </mappers>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **简化成：**

```XML
    <mappers>
        <!--加载sql映射文件，告诉MyBatis 去哪寻找映射SQL 的语句。-->
<!--        Maven项目编译后，java和resources下的目录和文件都在同一个跟目录下，所以路径是这样的，注意路径是/，不是.-->
<!--        <mapper resource="UserMapper.xml"/>-->
<!--        <mapper resource="package1/mapper/UserMapper.xml"/>-->
<!--        扫描包指定name的包下所有mapper配置文件-->
        <package name="package1.mapper"/>
    </mappers>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.5 配置文件实现增删改查

### 2.5.0 MybatisX插件、占位符、XML特殊字符转义

**安装MybatisX插件：**

Setting--Plugins--MybatisX

作用是通过小鸟图标，方便mapper接口和mapper配置文件之间代码的统一。

**参数占位符：**

参数占位符里的内容为传入的参数名，或者参数的成员变量名，或map的键名。

mybatis提供了两种参数占位符：

- \#{} ：执行SQL时，会将 #{} 占位符替换为？，将来自动设置参数值。底层使用的是 `PreparedStatement`
- ${} ：拼接SQL。底层使用的是 `Statement`，会存在SQL注入问题。  

 示例：

```XML
    <select id="selectById" resultMap="userResultMap">
        select * from tb_user where id=#{id};
    </select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **特殊字符处理：**

1.转义字符

XML中，需要转义的字符有： 
 　(1)&　　　`&` 
 　(2)<　　　`<` 
 　(3)>　　　`>` 
 　(4)＂　　　`"` 
 　(5)＇　　　`'` 

2.CDATA区

```XML
    <select id="selectById" resultMap="userResultMap">
        select * from tb_user where id <![CDATA[
            >        
        ]]> #{id};
    </select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.1 环境准备 

- 数据库表（tb_brand）及数据准备

  ```sql
  -- 删除tb_brand表
  drop table if exists tb_brand;
  -- 创建tb_brand表
  create table tb_brand
  (
      -- id 主键
      id           int primary key auto_increment,
      -- 品牌名称
      brand_name   varchar(20),
      -- 企业名称
      company_name varchar(20),
      -- 排序字段
      ordered      int,
      -- 描述信息
      description  varchar(100),
      -- 状态：0：禁用  1：启用
      status       int
  );
  -- 添加数据
  insert into tb_brand (brand_name, company_name, ordered, description, status)
  values ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
         ('华为', '华为技术有限公司', 100, '华为致力于把数字世界带入每个人、每个家庭、每个组织，构建万物互联的智能世界', 1),
         ('小米', '小米科技有限公司', 50, 'are you ok', 1);
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 实体类 Brand

  在 `com.itheima.pojo` 包下创建 Brand 实体类。

  ```java
  public class Brand {
      // id 主键
      private Integer id;
      // 品牌名称
      private String brandName;
      // 企业名称
      private String companyName;
      // 排序字段
      private Integer ordered;
      // 描述信息
      private String description;
      // 状态：0：禁用  1：启用
      private Integer status;
      
      //省略 setter and getter。自己写时要补全这部分代码
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 编写测试用例

  测试代码需要在 `test/java` 目录下创建包及测试用例。项目结构如下：

  ![img](JavaWeb基础3——Maven基础&MyBatis.assets/dd175fc1a913469881bc5f32d69b3499.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **2.5.2 resultType查询所有**

> 适用于数据库字段名和实体类属性名一致的情况。 

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--        映射配置文件 UserMapper.xml-->
<!--namespace名称空间，该命名空间和对应mapper接口的全限定名一致-->
<mapper namespace="package1.mapper.UserMapper">
    <select id="selectAll" resultType="package1.pojo.User">
        select * from tb_user;
    </select>
</mapper>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **2.5.3 resultMap给列起别名并查询所有**

>  适用于数据库字段名和实体类属性名不同的情况。 

SQL语句下划线命名法的**列名**和java实体类驼峰命名法的**成员变量不同**，会导致数据库给成员变量无法赋值的问题。**通过resultMap标签给数据库列名起别名，可以解决这个问题。**

> **注意：**只有select方法能用到resultMap，删改查都用不到。 

接口**UserMapper.java**定义抽象方法：

```java
List<Brand> selectAll();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> SQL语句简单的话，也可以使用注解，xml就不需要再生成statement了：
>
> ```java
> /**
>   * 查询所有
>   * @return
>   */
> @Select("select * from tb_brand")
> @ResultMap("brandResultMap")    //xml里要有resultMap标签起别名
> List<Brand> selectAll();
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**UserMapper.xml**

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.itheima.mapper.BrandMapper">
    <!--给列名起别名，让列名和成员变量一致，实现赋值-->
<resultMap id="brandResultMap" type="brand">
    <!--
            id：完成主键字段的映射
                column：表的列名
                property：实体类的属性名
            result：完成一般字段的映射
                column：表的列名
                property：实体类的属性名
        -->
    <result column="brand_name" property="brandName"/>
    <result column="company_name" property="companyName"/>
</resultMap>
    <select id="selectAll" resultMap="brandResultMap">
        select *
        from tb_brand;
    </select>
</mapper>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

sql映射配置文件查询成功后通过测试类List<Brand> brands = brandMapper.selectAll();获得所有对象组成的List列表。



### **2.5.4 单条件查询**

UserMapper.java 

```java
User selectById(int id);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

UserMapper.xml

```XML
<!--    parameterType="int"可省略-->
<!--    传入单个参数，#{}里的值可以随便命名，系统都会自动识别的，例如写成id=#{aaabb}都是能成功查询的-->
    <select id="selectById" resultMap="userResultMap" >
            select * from tb_user where id=#{id};
    </select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - 单个参数不用@Param注解起别名，会自动识别要传的参数。
> - 如果是传入多个参数，就需要使用下面三种传多参数方法。

### 2.5.5 多条件查询（三种传多参方法）

**`BrandMapper`.java**

三种传参方法：

> **事先注意：**
>
> mapper传参数，如果参数包括对象和散装参数，那么对象必须也注解，写SQL语句时候不能忘记对象.属性，例如brand.status.
>
> **示例：**
>
> ```java
> List<Brand> selectByPageAndCondition(@Param("begin") int begin,@Param("size") int size,@Param("brand") Brand brand);
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**①散装参数**：使用 `@Param("参数名称")` 标记每一个参数，在映射配置文件中就需要使用 `#{参数名称}` 进行占位

```java
//BrandMapper.java
List<Brand> selectByCondition(@Param("status") int status, @Param("companyName") String companyName,@Param("brandName") String brandName);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```XML
<!--    BrandMapper.xml-->
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    where status = #{status}
    and company_name like #{companyName}
    and brand_name like #{brandName}
</select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```java
//Demo.java
List<Brand> brands = brandMapper.selectByCondition(status, companyName, brandName);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**②实体类封装参数**：将多个参数封装成一个 实体对象 ，将该实体对象作为接口的方法参数。该方式要求在映射配置文件的SQL中使用 `#{内容}` 时，里面的**内容必须和实体类属性名保持一致**。

```java
//BrandMapper.java
List<Brand> selectByCondition(Brand brand);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```XML
<!--    BrandMapper.xml-->
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    where status = #{status}
    and company_name like #{companyName}
    and brand_name like #{brandName}
</select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```java
//Demo.java
        Brand brand = new Brand();
        brand.setStatus(status);
        brand.setCompanyName(companyName);
        brand.setBrandName(brandName);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**③map集合**：将多个参数封装到map集合中，将map集合作为接口的方法参数。该方式要求在映射配置文件的SQL中使用 `#{内容}` 时，里面的**内容必须和map集合中键的名称一致**。

```java
//BrandMapper.java
List<Brand> selectByCondition(Map map);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```XML
<!--    BrandMapper.xml-->
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    where status = #{status}
    and company_name like #{companyName}
    and brand_name like #{brandName}
</select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```java
//Demo.java
    Map map = new HashMap();
    map.put("status" , status);
    map.put("companyName", companyName);
    map.put("brandName" , brandName);
    List<Brand> brands = brandMapper.selectByCondition(map);
    System.out.println(brands);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**BrandMapper.xml都是一样的**  

```XML
<!--    BrandMapper.xml-->
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    where status = #{status}
    and company_name like #{companyName}
    and brand_name like #{brandName}
</select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**测试类：**

```java
@Test
public void Demo() throws IOException {
    //接收参数
    int status = 1;
    String companyName = "华为";
    String brandName = "华为";

    // 处理参数
    companyName = "%" + companyName + "%";
    brandName = "%" + brandName + "%";

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);

    //4. 执行方法
	//方式一 ：接口方法参数使用 @Param 方式调用的方法
    //List<Brand> brands = brandMapper.selectByCondition(status, companyName, brandName);
    //方式二 ：接口方法参数是 实体类对象 方式调用的方法
     //封装对象
    /* Brand brand = new Brand();
        brand.setStatus(status);
        brand.setCompanyName(companyName);
        brand.setBrandName(brandName);*/
    
    //List<Brand> brands = brandMapper.selectByCondition(brand);
    
    //方式三 ：接口方法参数是 map集合对象 方式调用的方法
    Map map = new HashMap();
    map.put("status" , status);
    map.put("companyName", companyName);
    map.put("brandName" , brandName);
    List<Brand> brands = brandMapper.selectByCondition(map);
    System.out.println(brands);

    //5. 释放资源
    sqlSession.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上述功能实现存在很大的问题。用户在输入条件时，肯定不会所有的条件都填写，这个时候我们的SQL语句就不能那样写，要使用动态SQL。 

### 2.5.6 多条件动态查询（动态SQL）

![img](JavaWeb基础3——Maven基础&MyBatis.assets/3a930f3e4c114cbd8245f779f46484a2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**动态SQL：**SQL语句随着用户的输入或外部条件的变化而变化，称为动态SQL。

Mybatis关于动态SQL的**标签**：

> - if
> - choose (when, otherwise)
> - trim (where, set)
> - foreach

**if标签**的test 属性：逻辑表达式

为了防止出现SQL语句where 后直接跟and的情况，给所有条件加了and，并且where后跟了1=1.

```XML
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
<!--        这里1=1是防止where后直接跟and的情况发生，更好的办法是用where标签，根据语法动态去and或where关键字-->
    where 1=1
        <if test="status != null">
            and status = #{status}
        </if>
        <if test="companyName != null and companyName != '' ">
            and company_name like #{companyName}
        </if>
        <if test="brandName != null and brandName != '' ">
            and brand_name like #{brandName}
        </if>
</select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**where 标签**作用：

- 替换where关键字
- 会动态的去掉第一个条件前的 and
- 如果所有的参数没有值则不加where关键字

示例：

```XML
    <select id="selectByCondition" resultMap="brandResultMap">
        select *
        from tb_brand
        <where>
<!--            where标签下注意所有if都要加and-->
            <if test="status != null">
                and status = #{status}
            </if>
            <if test="companyName != null and companyName != '' ">
                and company_name like #{companyName}
            </if>
            <if test="brandName != null and brandName != '' ">
                and brand_name like #{brandName}
            </if>
        </where>
    </select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.7 单条件动态查询（动态SQL）

先选择，再输入查询。

![img](JavaWeb基础3——Maven基础&MyBatis.assets/efea4121d2394ff0b61fe9372d38c1f2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**`choose（when，otherwise）`**标签**类似于Java 中的switch**语句，自带break。  

> **注意：**
>
> choose-when是多选一，一项<when>满足条件后其他就不判断了。
>
> <if>可以多层判断。

**代码：**

```XML
<!--    BrandMapper.xml-->
<select id="selectByConditionSingle" resultMap="brandResultMap">
    select *
    from tb_brand
    <where>
        <choose><!--相当于switch-->
            <when test="status != null"><!--相当于case-->
                status = #{status}
            </when>
            <when test="companyName != null and companyName != '' "><!--相当于case-->
                company_name like #{companyName}
            </when>
            <when test="brandName != null and brandName != ''"><!--相当于case-->
                brand_name like #{brandName}
            </when>
        </choose>
    </where>
</select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```java
//BrandMapper.java
List<Brand> selectByConditionSingle(Brand brand);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```java
//Demo.java
@Test
public void testSelectByConditionSingle() throws IOException {
    //接收参数
    int status = 1;
    String companyName = "华为";
    String brandName = "华为";

    // 处理参数
    companyName = "%" + companyName + "%";
    brandName = "%" + brandName + "%";

    //封装对象
    Brand brand = new Brand();
    //brand.setStatus(status);
    brand.setCompanyName(companyName);
    //brand.setBrandName(brandName);

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    List<Brand> brands = brandMapper.selectByConditionSingle(brand);
    System.out.println(brands);

    //5. 释放资源
    sqlSession.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.8 添加数据

```java
//BrandMapper.java
 /**
   * 添加，如果返回值为int，则返回改变的行数，也可void，通过异常了解添加成功或失败
   */
int add(Brand brand);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```XML
<!--    BrandMapper.xml-->
<insert id="add">
    insert into tb_brand (brand_name, company_name, ordered, description, status)
    values (#{brandName}, #{companyName}, #{ordered}, #{description}, #{status});
</insert>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```java
//测试类
@Test
public void testAdd() throws IOException {
    //接收参数
    int status = 1;
    String companyName = "波导手机";
    String brandName = "波导";
    String description = "手机中的战斗机";
    int ordered = 100;

    //封装对象
    Brand brand = new Brand();
    brand.setStatus(status);
    brand.setCompanyName(companyName);
    brand.setBrandName(brandName);
    brand.setDescription(description);
    brand.setOrdered(ordered);

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true); //设置自动提交事务，这种情况不需要手动提交事务了
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    
    System.out.println(brandMapper.add(brand));
    //要手动提交，不然会回滚事务。如果前面sqlSessionFactory.openSession(true)，就不用再提交事务了
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**Mybatis事务：**
 ![img](JavaWeb基础3——Maven基础&MyBatis.assets/2d24bc46bbd14a329308622970db52bb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​编辑

 **返回主键**

在 insert 标签上添加如下属性：

- useGeneratedKeys：是够获取自动增长的主键值。true表示获取
- keyProperty ：指定将获取到的主键值封装到哪儿个属性里  

```XML
<insert id="add" useGeneratedKeys="true" keyProperty="id">
    insert into tb_brand (brand_name, company_name, ordered, description, status)
    values (#{brandName}, #{companyName}, #{ordered}, #{description}, #{status});
</insert>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```java
brandMapper.add(brand);
System.out.println(brand.getId());
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.9 修改全部字段

获取到修改后的数据和id，修改此id对应的一行数据。

`BrandMapper` 接口

```java
 /**
   * 修改
   */
void update(Brand brand);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

BrandMapper.xml

```XML
<update id="update">
    update tb_brand
    <set>
        <if test="brandName != null and brandName != ''">
            brand_name = #{brandName},
        </if>
        <if test="companyName != null and companyName != ''">
            company_name = #{companyName},
        </if>
        <if test="ordered != null">
            ordered = #{ordered},
        </if>
        <if test="description != null and description != ''">
            description = #{description},
        </if>
        <if test="status != null">
            status = #{status}
        </if>
    </set>
    where id = #{id};
</update>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

MybatisTest类

```java
@Test
public void testUpdate() throws IOException {
    //接收参数
    int status = 0;
    String companyName = "波导手机";
    String brandName = "波导";
    String description = "波导手机,手机中的战斗机";
    int ordered = 200;
    int id = 6;

    //封装对象
    Brand brand = new Brand();
    brand.setStatus(status);
    //        brand.setCompanyName(companyName);
    //        brand.setBrandName(brandName);
    //        brand.setDescription(description);
    //        brand.setOrdered(ordered);
    brand.setId(id);

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true);
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    int count = brandMapper.update(brand);
    System.out.println(count);
    //提交事务
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.10 修改动态字段

在修改界面用户可能只修改部分属性， 所以加条件<if>判断每个属性修改框用户有没有填写，用<set>防止更新语句最后一行有逗号。 

![img](JavaWeb基础3——Maven基础&MyBatis.assets/4bbf72d7ddbd47d2bbb7ebc85dd0feb7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.11 删除一行数据

`BrandMapper` 接口

```java
/**
  * 根据id删除
  */
void deleteById(int id);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

BrandMapper.xml

```XML
<delete id="deleteById">
    delete from tb_brand where id = #{id};
</delete>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

MybatisTest类

```java
 @Test
public void testDeleteById() throws IOException {
    //接收参数
    int id = 6;

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true);
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    brandMapper.deleteById(id);
    //提交事务
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.12 批量删除

编写SQL时需要遍历数组来拼接SQL语句。Mybatis 提供了 `foreach` 标签供我们使用

**foreach 标签**

用来迭代任何可迭代的对象（如数组，集合）。

- collection 属性：指定遍历的数组
  - mybatis会将数组参数，封装为一个Map集合。
    - 默认：array = 数组，key是array而不是数组名，如collection="array"和void deleteByIds(int[] ids);
    - 可以使用@Param注解改变map集合的默认key的名称为数组名，如collection="ids"和void deleteByIds(@Param("ids") int[] ids);
- item 属性：本次迭代获取到的元素，如item="id"。
- separator 属性：集合项迭代之间的分隔符。`foreach` 标签不会错误地添加多余的分隔符。也就是最后一次迭代不会加分隔符。如separator=","
- open 属性：该属性值是在拼接SQL语句之前拼接的语句，只会拼接一次。如open="("
- close 属性：该属性值是在拼接SQL语句拼接后拼接的语句，只会拼接一次。如close=")"

`BrandMapper` 接口

```java
/**
  * 批量删除
  */
void deleteByIds(int[] ids);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

BrandMapper.xml

```XML
<delete id="deleteByIds">
    delete from tb_brand where id
    in
    <foreach collection="array" item="id" separator="," open="(" close=")">
        #{id}
    </foreach>
    ;
</delete>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

MybatisTest类

```java
@Test
public void testDeleteByIds() throws IOException {
    //接收参数
    int[] ids = {5,7,8};

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true);
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    brandMapper.deleteByIds(ids);
    //提交事务
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.6 Mybatis参数传递

Mybatis 接口方法中可以接收各种各样的参数，如下：

- 多个参数
- 单个参数：单个参数又可以是如下类型
  - **POJO 类型，传入对象**
  - Map 集合类型，传入map
  - Collection 集合类型
  - List 集合类型
  - Array 类型
  - 其他类型

> **事先注意：**
>
> mapper传参数，如果**参数包括对象和散装参数**，那么**对象必须也注解**，写SQL语句时候不能忘记对象.属性，例如brand.status.
>
> 示例：
>
> ```java
> List<Brand> selectByPageAndCondition(@Param("begin") int begin,@Param("size") int size,@Param("brand") Brand brand);
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**多个参数注解传递**

如下面的代码，就是接收两个参数，而接收多个参数需要使用 `@Param` 注解，那么为什么要加该注解呢？这个问题要弄明白就必须来研究Mybatis 底层对于这些参数是如何处理的。

```XML
User select(@Param("username") String username,@Param("password") String password);
<select id="select" resultType="user">
    select *
    from tb_user
    where 
        username=#{username}
        and password=#{password}
</select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**注解底层，了解即可** 

我们在接口方法中定义多个参数，Mybatis 会将这些参数封装成 Map 集合对象，值就是参数值，而键在没有使用 `@Param` 注解时有以下命名规则：

- 以 arg 开头 ：第一个参数就叫 arg0，第二个参数就叫 arg1，以此类推。如：

  > map.put("arg0"，参数值1);
  >
  > map.put("arg1"，参数值2);

- 以 param 开头 ： 第一个参数就叫 param1，第二个参数就叫 param2，依次类推。如：

  > map.put("param1"，参数值1);
  >
  > map.put("param2"，参数值2);

代码验证：

- 在 `UserMapper` 接口中定义如下方法

  ```
  User select(String username,String password);
  ```

- 在 `UserMapper.xml` 映射配置文件中定义SQL

  ```XML
  <select id="select" resultType="user">
      select *
      from tb_user
      where 
          username=#{arg0}
          and password=#{arg1}
  </select>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  或者

  ```XML
  <select id="select" resultType="user">
      select *
      from tb_user
      where 
          username=#{param1}
          and password=#{param2}
  </select>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

运行代码结果如下

![img](JavaWeb基础3——Maven基础&MyBatis.assets/3d4e42ec0d1e4c15b5fdbca53ad616de.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- 在映射配合文件的SQL语句中使用用 `arg` 开头的和 `param` 书写，代码的可读性会变的特别差，此时可以使用 `@Param` 注解。



在接口方法参数上使用 `@Param` 注解，Mybatis 会将 `arg` 开头的键名替换为对应注解的属性值。

代码验证：

- 在 `UserMapper` 接口中定义如下方法，在 `username` 参数前加上 `@Param` 注解

  ```
  User select(@Param("username") String username, String password);
  ```

  Mybatis 在封装 Map 集合时，键名就会变成如下：

  > map.put("username"，参数值1);
  >
  > map.put("arg1"，参数值2);
  >
  > map.put("param1"，参数值1);
  >
  > map.put("param2"，参数值2);

- 在 `UserMapper.xml` 映射配置文件中定义SQL

  ```
  <select id="select" resultType="user">
      select *
      from tb_user
      where 
          username=#{username}
          and password=#{param2}
  </select>
  ```

- 运行程序结果没有报错。而如果将 `#{}` 中的 `username` 还是写成 `arg0`

  ```
  <select id="select" resultType="user">
      select *
      from tb_user
      where 
          username=#{arg0}
          and password=#{param2}
  </select>
  ```

- 运行程序则可以看到错误

![img](JavaWeb基础3——Maven基础&MyBatis.assets/f7f003dfdf5e4eedb3a988ee0e28e901.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**结论：以后接口参数是多个时，在每个参数上都使用 `@Param` 注解。这样代码的可读性更高。**

## 2.7 注解实现增删改查

如果**SQL语句简单**，使用注解开发会比配置文件开发更加**方便**。

如下就是使用注解进行开发

```java
@Select(value = "select * from tb_user where id = #{id}")
public User select(int id);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - 注解后是没有分号的。
> - 注解是用来替换映射配置文件方式配置的，所以使用了注解，就不需要再映射配置文件中书写对应的 `statement`

Mybatis 针对 CURD 操作都提供了对应的注解，已经做到见名知意。如下：

- 查询 ：@Select
- 添加 ：@Insert
- 修改 ：@Update
- 删除 ：@Delete

**注意：**在官方文档中 `入门` 中有这样的一段话：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/e417dfe1489947c3ad579d47d51cfa83.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





所以，**注解完成简单功能，配置文件完成复杂功能。**

而我们之前写的动态 SQL 就是复杂的功能，如果用注解使用的话，就需要使用到 Mybatis 提供的SQL构建器来完成，而对应的代码如下：

![img](JavaWeb基础3——Maven基础&MyBatis.assets/4553fc6b112a4cb58f9bb932346417e3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





上述代码将java代码和SQL语句融到了一块，使得代码的可读性大幅度降低。