>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1，Spring背景](#spring_day01)

[1.1 Spring地位](#1-1-)

[1.2 Spring优势和学习内容](#1-2-)

[2，Spring相关概念](#2-spring-)

[2.1 初识Spring](#2-1-spring)

[2.1.1 Spring家族](#2-1-1-spring-)

[2.1.2 Spring发展史](#2-1-2-spring-)

[2.2 Spring系统架构](#2-2-spring-)

[2.2.1 系统架构图](#2-2-1-)

[2.2.2 学习内容](#2-2-2-)

[2.3 Spring核心概念](#2-3-spring-)

[2.3.1 不使用Spring项目中的问题](#2-3-1-)

[2.3.2 IOC、IOC容器、Bean、DI](#2-3-2-ioc-ioc-bean-di)

[2.3.3 核心概念小结](#2-3-3-)

[3，入门案例（配置开发版）](#3-)

[3.1 IOC入门案例](#3-1-ioc-)

[3.1.1 入门案例思路分析](#3-1-1-)

[3.1.2 入门案例代码实现](#3-1-2-)

[3.2 DI入门案例，通过配置除掉service里的new](#3-2-di-)

[3.2.1 入门案例思路分析](#3.2.1%20%E5%85%A5%E9%97%A8%E6%A1%88%E4%BE%8B%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90)

[3.2.2 入门案例代码实现](#3-2-2-)

[4，IOC相关内容](#4-ioc-)

[4.1 bean基础配置](#4-1-bean-)

[4.1.0 概述](#4-14-bean-)

[4.1.1 bean基础配置(id与class)](#4-1-1-bean-id-class-)

[4.1.2 bean的name属性](#4.1.2%20bean%E7%9A%84name%E5%B1%9E%E6%80%A7)

[4.1.3 bean作用范围scope配置，单例和非单例](#4-1-3-bean-scope-)

[4.2 bean的三种创建方式](#4-2-bean-)

[4.2.1 环境准备](#4-2-1-)

[4.2.2 bean的创建方法:1：无参构造方法实例化（常用）](#4-2-2-)

[4.2.3 Spring的报错信息从下往上看](#4-2-3-spring-)

[4.2.4 bean的创建方式2：静态工厂实例化（了解）](#4-2-4-)

[4.2.5 bean的创建方式3：实例工厂（了解）与FactoryBean（常用）](#4-2-5-factorybean)

[4.2.6 bean实例化小结](#4-2-6-bean-)

[4.3 bean的生命周期](#4-3-bean-)

[4.3.1 环境准备](#4-3-1-)

[4.3.2 生命周期控制](#4-3-2-)

[4.3.3 关闭IOC容器方法：close关闭容器、注册钩子关闭容器](#4-3-3-close-)

[4.3.4 InitializingBean， DisposableBean控制生命周期](#4.3.4%C2%A0InitializingBean%EF%BC%8C%C2%A0DisposableBean%E6%8E%A7%E5%88%B6%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

[4.3.5 bean生命周期小结](#4-3-5-bean-)

[5，DI相关内容](#5-di-)

[5.1 setter注入](#5-1-setter-)

[5.1.1 环境准备](#5-1-1-)

[5.1.2 注入多个引用数据类型（property标签的name和ref）](#5-1-2-)

[5.1.3 注入简单数据类型（property标签的name和value）](#5-1-3-)

[5.2 构造器注入](#5-2-)

[5.2.1 环境准备](#5-2-1-)

[5.2.2 构造器注入引用数据类型（constructor-arg标签的name和ref）](#5-2-2-)

[5.2.3 构造器注入多个引用数据类型](#5-2-3-)

[5.2.4 构造器注入多个简单数据类型（constructor-arg标签的name和value）](#5-2-4-)

[5.2.5 依赖注入方式选择](#5.2.5%20%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5%E6%96%B9%E5%BC%8F%E9%80%89%E6%8B%A9)

[5.3 自动配置依赖注入](#5-3-)

[5.3.1 什么是依赖自动装配?](#5-3-1-)

[5.3.2 自动装配方式有哪些?](#5-3-2-)

[5.3.3 准备下案例环境](#5-3-3-)

[5.3.4 完成自动装配的配置](#5-3-4-)

[5.4 数组、集合注入](#5-4-)

[5.4.1 环境准备](#5-4-1-)

[5.4.2 注入数组类型数据](#5-4-2-)

[5.4.3 注入List类型数据](#5-4-3-list-)

[5.4.4 注入Set类型数据](#5-4-4-set-)

[5.4.5 注入Map类型数据](#5-4-5-map-)

[5.4.6 注入Properties类型数据](#5-4-6-properties-)

--

## 1，Spring背景

### 1.1 Spring地位

-   从使用和占有率看
    
    -   Spring在市场的占有率与使用率高，未使用Spring的项目一般都是些比较老的项目，大多都处于维护阶段。
        
    -   Spring在企业的技术选型命中率高，Spring是微服务架构基础，是传统开发主流技术。所以说,Spring技术是JavaEE开发必备技能
        

![](https://i-blog.csdnimg.cn/blog_migrate/2602256180a9b397de3d7fd42ca57003.png)

### 1.2 Spring优势和学习内容

Spring框架主要的优势是在**`简化开发`**和**`框架整合`**上：

-   **简化开发:** Spring两大核心技术**IOC、****AOP。**
    
-   **事务处理**属于Spring中AOP的具体应用，可以简化项目中的事务管理，也是Spring技术中的一大亮点。

-   **框架整合:** Spring可以整合市面上几乎所有主流框架，比如:
    
    -   **MyBatis**
    -   MyBatis-plus
    -   Struts
    -   Struts2
    -   Hibernate
    -   ……

**学习内容:**

-   **Spring核心容器的IOC/DI**
-   **Spring的AOP**
-   **AOP的具体应用,事务管理**
-   **IOC/DI的具体应用,整合Mybatis**

## 2，Spring相关概念

### 2.1 初识Spring

#### 2.1.1 Spring家族

-   官网：https://spring.io
    
    -   **Spring能做什么:**用以开发web、微服务以及分布式系统等。光这三块就已经占了JavaEE开发的**九成多**。
    -   Spring并不是单一的一个技术，而是一个**大家族**，可以从官网的`Projects`中查看其包含的所有技术。
-   Spring发展到今天已经形成了一种开发的生态圈,Spring提供了若干个项目,每个项目用于完成特定的功能。
    
    -   **Spring已形成了完整的生态圈**。我们可以使用Spring技术完成整个项目的构建、设计与开发。
        
    -   Spring**有若干个项目**。可以根据需要自行选择，把这些个项目组合起来，起了一个名称叫**全家桶**，如下图所示![](https://i-blog.csdnimg.cn/blog_migrate/0e710e8ca5c7a62e740fd0f50c033a47.png)
        
        **说明:**
        
        图中的图标都代表什么含义，可以进入`https://spring.io/projects`网站进行对比查看。
        
        这些技术并不是所有的都需要学习，额外需要重点关注`Spring Framework`、`SpringBoot`和`SpringCloud`:
        
        除了上面的这三个技术外，还有很多其他的技术，也比较流行，如SpringData,SpringSecurity等，这些都可以被应用在我们的项目中。
        
        -   **Spring Framework:**Spring框架，是Spring中最早最核心的技术，也是所有其他技术的基础。
        -   **SpringBoot:**Spring是来简化开发，而SpringBoot是来帮助Spring在简化的基础上能**更快速进行开发**。
        -   **SpringCloud:**这个是用来做**分布式之微服务架构的相关开发**。

我们今天所学习的Spring其实指的是**Spring Framework**。

#### 2.1.2 Spring发展史

接下来我们介绍下Spring Framework这个技术是如何来的呢?

![](https://i-blog.csdnimg.cn/blog_migrate/99345836ce0709b390521354a8fccac4.png)

Spring发展史

-   IBM(IT公司-国际商业机器公司)在1997年提出了EJB思想,早期的JAVAEE开发大都基于该思想。
-   Rod Johnson(Java和J2EE开发领域的专家)在2002年出版的`Expert One-on-One J2EE Design and Development`,书中有阐述在开发中使用EJB该如何做。
-   Rod Johnson在2004年出版的`Expert One-on-One J2EE Development without EJB`,书中提出了比EJB思想更高效的实现方案，并且在同年将方案进行了具体的落地实现，这个实现就是Spring1.0。
-   随着时间推移，版本不断更新维护，目前最新的是Spring5
    -   **Spring1.0**是纯配置文件开发
    -   **Spring2.0**为了简化开发引入了注解开发，此时是配置文件加注解的开发方式
    -   **Spring3.0**已经可以进行**纯注解开发**，使开发效率大幅提升，我们的课程会以注解开发为主
    -   **Spring4.0**根据JDK的版本升级对个别API进行了调整
    -   **Spring5.0**已经全面支持JDK8，现在Spring最新的是5系列所以建议大家**把JDK安装成1.8版**

本节介绍了Spring家族与Spring的发展史，需要大家重点掌握的是:

-   今天所学的Spring其实是Spring家族中的Spring Framework
-   Spring Framework是Spring家族中其他框架的底层基础，**学好Spring可以为其他Spring框架的学习打好基础**

### 2.2 Spring系统架构

spring框架主要指的是Spring Framework。

#### 2.2.1 系统架构图

-   Spring Framework是Spring生态圈中最基础的项目，是其他项目的根基。Spring Framework的发展也经历了很多版本的变更，每个版本都有相应的调整。![](https://i-blog.csdnimg.cn/blog_migrate/1b8c6db9801318511b77ffc5a6a376bb.png)
    
-   Spring Framework的5版本目前没有最新的架构图，而最新的是4版本，所以接下来主要研究的是**Spring4的架构图**![](https://i-blog.csdnimg.cn/blog_migrate/74a475741c0ecb899c1a7f16507110ff.png)
    
     系统架构讲究上层依赖下层，所以越下层越核心，最下层的是核心容器。
    
    **(1)核心层**
    
    -   Core Container:核心容器，这个模块是Spring最核心的模块，其他的都需要依赖该模块
    
    **(2)AOP层**
    
    -   **AOP**（Aspect Oriented Programming，aspect译为切面，方面；oriented译为面向，以...为方向；）:面向切面编程。它依赖核心层容器，目的是**在不改变原有代码的前提下对其进行功能增强**
    -   **Aspects**：AOP是思想,Aspects是对AOP思想的具体实现
    
    **(3)数据层**
    
    -   Data Access:数据访问，Spring全家桶中有对数据访问的具体实现技术
    -   Data Integration:数据集成，Spring支持整合其他的数据层解决方案，比如Mybatis。integration译为集成，结合，融合。
    -   Transactions:事务，Spring中事务管理是Spring AOP的一个具体实现，也是后期学习的重点内容。Transactions译为事务，业务，交易。
    
    **(4)Web层**
    
    -   这一层的内容将在SpringMVC框架具体学习
    
    **(5)Test层**
    
    -   Spring主要整合了Junit来完成单元测试和集成测试

#### 2.2.2 学习内容

主要包含四部分内容:

-   **Spring核心容器的IOC/DI**
-   **Spring的AOP**
-   **AOP的具体应用,事务管理**
-   **IOC/DI的具体应用,整合Mybatis**

![](https://i-blog.csdnimg.cn/blog_migrate/43c9595ca53fc07e0f9f7a85fd7d85e5.png)

### 2.3 Spring核心概念

在Spring核心概念这部分内容中主要包含`IOC/DI`、`IOC容器`和`Bean`,那么问题就来了，这些都是什么呢?

#### 2.3.1 不使用Spring项目中的问题

> **回顾：** 
> 
> 在上一节整合Javaweb开发商品管理系统写业务层的时候，方案是写BrandService接口，然后BrandServiceImp1实现BrandService接口，在Servlet创建service对象时候是
> 
> ```java
> BrandService service=new BrandServiceImp1;
> ```
> 
> [JavaWeb基础10——VUE&Element&整合Javaweb的商品管理系统\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126186764?spm=1001.2014.3001.5501 "JavaWeb基础10——VUE&Element&整合Javaweb的商品管理系统_vincewm的博客-CSDN博客")
> 
> 当时优化时说使用接口实现类方法比直接业务类更好，能降低耦合度。在更新业务层实现方法时候，Servlet里就只需要修改new后的实现类名，甚至在使用Spring后可以不改Servlet代码。

**问题: 耦合度偏高**

![](https://i-blog.csdnimg.cn/blog_migrate/c3031c7397c16259b0bd27b5187b4343.png)

(1)业务层需要调用数据层的方法，就需要在业务层new数据层的对象

(2)如果数据层的实现类发生变化，那么业务层的代码也需要跟着改变，发生变更后，都需要进行编译打包和重部署

(3)所以，现在代码在编写的过程中存在的问题是：**耦合度偏高**

**解决方案：不要主动使用new产生对象，转换为由外部提供对象。即Ioc控制反转思想。**

![](https://i-blog.csdnimg.cn/blog_migrate/0b7c9189078c8e19e00f24b097f8dbca.png)

把框中的内容给去掉，就可以降低依赖了，同时为了使程序可以运行，Spring就提出了一个解决方案:

-   使用对象时，在程序中不要主动使用new产生对象，转换为由**外部**提供对象

#### 2.3.2 IOC、IOC容器、Bean、DI

**1.IOC（Inversion of Control）控制反转**

inversion译为反转，相反。 

**（1）控制反转：**

-   **对象创建控制权由程序转移到外部（IOC容器）**，此思想称为控制反转。使用对象时，由主动new产生对象转换为**由外部提供对象。**
    -   业务层要用数据层的类对象，以前是自己`new`的
    -   现在自己不new了，交给`别人[外部]`来创建对象
    -   `别人[外部]`就**反转控制**了数据层对象的**创建权**
    -   这种思想就是控制反转，别人【外部】是IOC容器

**(2)Spring和IOC之间的关系是什么呢?**

-   Spring**实现**了IOC思想
-   Spring提供了一个容器，称为**IOC容器**，用来充当IOC思想中的`别人[外部]`

**(3)IOC容器的作用以及内部存放的是什么?**

作用： 

-   IOC容器负责**对象的创建、初始化**等一系列工作，其中包含了**数据层和业务层**的**类对象**
-   **被创建或被管理的对象在IOC容器中统称为Bean**

内部存放：

-   IOC容器中放的就是一个个的**Bean对象**

**(4)当IOC容器中创建好service和dao对象后，还需要DI依赖注入**

> Dao(Data Access Object)：数据访问对象

-   service运行需要依赖dao对象
-   IOC容器中虽然有service和dao对象，但是service对象和dao对象没有任何关系
-   所以**要绑定service和dao对象之间的关系**

像这种**在容器中建立对象与对象之间的绑定关系就要用到DI依赖注入。**

**2.DI（Dependency Injection）依赖注入**

![](https://i-blog.csdnimg.cn/blog_migrate/36c6accc6b8033cbb0fbe561a5722f4d.png)

**(1)依赖注入**

-   在容器中**绑定bean与bean之间的依赖关系**的整个过程，称为依赖注入
    -   业务层要用数据层的类对象，以前是自己`new`的，现在**靠`IOC容器`注入进来**
    -   这种**思想**就是依赖注入

**(2)IOC容器中哪些bean之间要建立依赖关系?**

-   这个需要程序员根据业务需求提前建立好关系，如业务层需要依赖数据层，**service就要和dao建立依赖关系**

Spring的IOC和DI这两个概念的最终目标就是:**充分解耦**，具体实现方式:

-   使用**IOC容器**管理bean（IOC)
-   在IOC容器内将有依赖关系的bean进行**依赖关系绑定**（DI）
-   最终结果为:**使用对象时不仅可以直接从IOC容器中获取，并且获取到的bean已经绑定了所有的依赖关系.**

#### 2.3.3 核心概念小结

这节比较重要，重点要理解`什么是IOC/DI思想`、`什么是IOC容器`和`什么是Bean`：

**(1)什么IOC/DI思想?**

-   **IOC:控制反转，控制反转的是对象的创建权，反转给IOC容器**
-   **DI:依赖注入，绑定对象与对象之间的依赖关系**

**(2)什么是IOC容器?**

Spring创建了一个容器用来存放所创建的对象，这个容器就叫IOC容器

**(3)什么是Bean?**

容器中所存放的一个个对象就叫Bean或Bean对象

## 3，入门案例（配置开发版）

> 了解即可，以后更多用的是注解开发。 

介绍完Spring的核心概念后，接下来我们得思考一个问题就是，**Spring到底是如何来实现IOC和DI的**，那接下来就通过一些简单的入门案例，来演示下具体实现过程:

### 3.1 IOC入门案例

#### 3.1.1 入门案例思路分析

**IOC创建bean有四种方式：无参构造方法实例化（常用）**、静态工厂实例化（了解）、实例工厂（了解）、FactoryBean（常用）。

这里入门案例使用的是无参构造方法实例化（常用）。

**(1)Spring是使用容器来管理bean对象的，bean对象有哪些?**

-   答：主要管理项目中所使用到的类对象，比如**Service和Dao**

**(2)如何将被管理的对象告知IOC容器?**

-   答：使用配置文件applicationContext.xml的bean标签。
    
    ```XML
        <bean id="bookDao" class="package1.dao.impl.BookDaoImpl"/>
    ```
    

**(3)****如何获取到IOC容器?**

-   答：Spring框架提供相应的接口ApplicationContext，实现类ClassPathXmlApplicationContext
    
    ```java
    //        ClassPathXmlApplicationContext了解即可，有new后面会被优化
            ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
    ```
    

**(4)如何从容器中获取bean?**

-   答：调用ApplicationContext的getBean()方法，根据id或name获取Bean：

```java
// 根据名称获取bean。默认的bean名称为首字母小写的类名。缺点：书写时没有提示，可能会写错。
       BookDao bookDao = (BookDao) applicationContext.getBean("bookDao");
       bookDao.save();

// 根据类型获取bean。优点：书写时有提示。缺点：IOC容器存在多个同类型不同名的Bean时，无法确定获取哪个Bean，报错。
       BookDao bookDao = (BookDao) applicationContext.getBean(BookDao.class);
// 根据名称+类型获取bean。推荐，精准指定，有提示避免报错，可读性高
       BookDao bookDao = (BookDao) applicationContext.getBean(BookDao.class);
       BookDao bookDao = (BookDao) applicationContext.getBean("bookDao",BookDao.class);
```

**(5)使用Spring需要导入哪些坐标?**

-   答：用别人的东西，就需要在pom.xml添加**spring-context依赖**
    
    ```XML
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-context</artifactId>
                <version>5.3.22</version>
            </dependency>
    ```
    

#### 3.1.2 入门案例代码实现

> **需求分析:**
> 
> 将BookServiceImpl和BookDaoImpl交给Spring管理，并从容器中获取对应的bean对象进行方法调用。
> 
> **步骤：**
> 
> 1.创建Maven的java项目
> 
> 2.pom.xml添加Spring的依赖jar包
> 
> 3.创建BookService,BookServiceImpl，BookDao和BookDaoImpl四个类
> 
> 4.resources下添加spring配置文件，并完成bean的配置
> 
> 5.使用Spring提供的接口完成IOC容器的创建
> 
> 6.从容器中获取对象进行方法调用

**步骤1:创建Maven项目**

![](https://i-blog.csdnimg.cn/blog_migrate/169efd41eb69ac06b4f19ba1b2480734.png)

**步骤2:添加Spring的依赖jar包**

pom.xml导入Spring和junit依赖

```XML
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.10.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

**步骤3:创建dao和service**

创建BookService,BookServiceImpl，BookDao和BookDaoImpl四个类

![](https://i-blog.csdnimg.cn/blog_migrate/4d34cf7567073c0a199030d3f7f73d23.png)

```java
public interface BookDao {
    public void save();
}
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface BookService {
    public void save();
}
public class BookServiceImpl implements BookService {
    private BookDao bookDao = new BookDaoImpl();
    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

**步骤4:添加spring配置文件**

resources下添加spring配置文件**applicationContext.xml。**

> applicationContext译为配置文件、应用上下文，是约定俗成的Spring配置文件命名规范。

![](https://i-blog.csdnimg.cn/blog_migrate/5b53ffeb9bdf90f6a84d6e7129da5dc0.png)

 创建完上面有提示让配置应用程序上下文，点击确定即可：

![](https://i-blog.csdnimg.cn/blog_migrate/93ef0b9f18bb1b533b3ce07dd671814c.png)

![](https://i-blog.csdnimg.cn/blog_migrate/a8472a98c311d71531b4af38e6641e8e.png)

**步骤5:在配置文件中完成bean的配置**

**bean标签：**配置bean  
**id属性：**给bean起名字，唯一标识  
**class属性：**给bean定义类型 

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--bean标签表示配置bean
        id属性表示给bean起名字，唯一标识
        class属性表示给bean定义类型
    -->
    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl"/>

</beans>
```

> ****注意事项：bean定义时id是bean的未知标识，属性在同一个上下文中(配置文件)不能重复****

**步骤6:获取IOC容器**

使用Spring提供的**ApplicationContext** **接口**和ClassPathXmlApplicationContext实现类完成IOC容器的创建，创建App类，编写main方法

> ClassPathXmlApplicationContext实现类**了解即可**，用到new耦合度高，以后会被优化。

```java
public class App {
    public static void main(String[] args) {
        //获取IOC容器
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml"); 
    }
}
```

**步骤7:从容器中获取bean并调用bean的方法**

```java
public class App {
    public static void main(String[] args) {
        //获取IOC容器
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml"); 
//        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
//        bookDao.save();
        BookService bookService = (BookService) ctx.getBean("bookService");    //bookService是前面定义的bean的id，这里是根据id获取ioc容器里的bean
        bookService.save();
    }
}
```

**步骤8:运行程序**

测试结果为：

![](https://i-blog.csdnimg.cn/blog_migrate/0a481b68297ba532913378cb60c7d477.png)

Spring的IOC入门案例已经完成。但是在`BookServiceImpl`的类中**依然存在**`BookDaoImpl`对象的**new操作**，它们之间的耦合度还是比较高，这就需要用到下面的`DI:依赖注入`。

### 3.2 DI入门案例，通过配置除掉service里的new

#### 3.2.1 入门案例思路分析

**Spring提供了两种注入方式**，分别是:

-   **setter注入**
    -   简单类型
    -   **引用类型**
-   构造器注入
    -   简单类型
    -   引用类型

这里入门案例使用的是引用类型setter注入。

**(1)要想实现依赖注入，必须要基于IOC管理Bean**

-   **在IOC容器中绑定bean与bean之间的依赖关系**的整个过程，称为依赖注入

**(2)Service中使用new形式创建的Dao对象是否保留?**

-   答：需要删除掉，同时为dao引用设置setter方法。最终要使用IOC容器中的bean对象
    
    ```java
    
    public class BookServiceImpl implements BookService {
        //删除业务层中使用new的方式创建的dao对象
        private BookDao bookDao;
     
        public void save() {
            System.out.println("book service save ...");
            bookDao.save();
        }
        //提供对应的set方法
        public void setBookDao(BookDao bookDao) {
            this.bookDao = bookDao;
        }
    }
    ```
    

**(3)Service中需要的Dao对象如何进入到Service中?**

-   答：**在Service中提供方法**，让Spring的IOC容器可以通过该方法传入bean对象

**(4)Service与Dao间的关系如何描述?**

-   答：使用配置文件，service的bean标签内通过**property标签配置name和ref**。
    
    ```XML
        <bean id="bookDao" class="package1.dao.impl.BookDaoImpl"/>
        <bean id="bookService" class="package1.service.impl.BookServiceImpl">
            <property name="bookDao" ref="bookDao"/>
        </bean>
    ```
    

#### 3.2.2 入门案例代码实现

> **需求:**
> 
> 基于IOC入门案例，在BookServiceImpl类中删除new对象的方式，使用Spring的DI完成Dao层的注入。
> 
> **步骤：**
> 
> 1.删除业务层中使用new的方式创建的dao对象
> 
> 2.在业务层提供BookDao的setter方法
> 
> 3.在配置文件中添加依赖注入的配置
> 
> 4.运行程序调用方法

**步骤1: 去除业务实现类中的new**，仅留下定义数据访问对象dao引用

在业务层BookServiceImpl类中，删除业务层中使用new的方式创建的dao对象

```java
public class BookServiceImpl implements BookService {
    //删除业务层中使用new的方式创建的dao对象
    private BookDao bookDao;

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

**步骤2:为业务实现类属性提供setter方法**

在BookServiceImpl类中,为BookDao提供setter方法

```java
public class BookServiceImpl implements BookService {
    //删除业务层中使用new的方式创建的dao对象
    private BookDao bookDao;

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
    //提供对应的set方法
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
}
```

**步骤3:修改配置完成property属性注入**

是service里调用dao，所以要在配置文件service的bean中配置service和dao的关系

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--bean标签标示配置bean
        id属性标示给bean起名字
        class属性表示给bean定义类型
    -->
    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>

    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <!--配置server与dao的关系-->
        <!--property标签表示配置当前bean的属性
                name属性表示配置哪一个具体的属性，值是在service中创建的私有dao引用。
                ref属性表示参照哪一个id的bean
        -->
        <property name="bookDao" ref="bookDao"/>
    </bean>

</beans>
```

> **注意:property标签中的两个bookDao的含义是不一样的**
> 
> **name="bookDao"中`bookDao`：表示配置哪一个具体的属性。**
> 
> **作用：**让Spring的IOC容器在获取到名称后，将首字母大写，前面加set找对应的`setBookDao()`方法进行对象注入
> 
> **ref="bookDao"中`bookDao`：表示参照哪一个id的bean。**
> 
> **作用：**让Spring能在IOC容器中找到id为`bookDao`的Bean对象给`bookService`进行注入
> 
> 综上所述，对应关系如下:
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3f6394d8f258ff2ebc69116809418542.png)

**步骤4:运行程序**

运行，测试结果为：

![](https://i-blog.csdnimg.cn/blog_migrate/8bf093405db30c7e861a2a35a14640a4.png)

## 4，IOC相关内容

IOC容器主要是创建和管理类对象bean的，这一章节主要讲bean的配置、实例化、生命周期。

### 4.1 bean基础配置

#### 4.1.0 概述

关于bean的基础配置中，需要大家掌握以下属性:

![](https://i-blog.csdnimg.cn/blog_migrate/15c79f920949715edd9626c40b212fae.png)

#### 4.1.1 bean基础配置(id与class)

对于bean的基础配置，在前面的案例中已经使用过:

```XML
<bean id="" class=""/>
```

其中，bean标签的功能、使用方式以及id和class属性的作用，我们通过一张图来描述下

![](https://i-blog.csdnimg.cn/blog_migrate/d27797f31cfa10b029d5d057e953e367.png)

需要重点掌握的是:**bean标签的id和class属性的使用**。

> **思考：**
> 
> -   class属性能不能写接口如`BookDao`的类全名呢?
> 
> 答案肯定是不行，因为**接口是没办法创建对象的**。
> 
> -   前面提过为bean设置id时，id必须唯一，但是如果由于命名习惯而产生了分歧后，该如何解决?
> 
> 通过bean的name属性起别名。

#### 4.1.2 bean的name属性

首先来看下别名的配置说明:

![](https://i-blog.csdnimg.cn/blog_migrate/a3d6be4c472d660cf03d2533b83ac030.png)

 **步骤0：重新搭建和前面一样的的案例：**

![](https://i-blog.csdnimg.cn/blog_migrate/cebdb7a0fe4af78a6c737a18de991dd9.png)

**步骤1：配置别名**

打开spring的配置文件applicationContext.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--name:为bean指定别名，别名可以有多个，使用逗号，分号，空格进行分隔-->
    <bean id="bookService" name="service service4 bookEbi" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>

    <!--scope：为bean设置作用范围，可选值为单例singloton，非单例prototype-->
    <bean id="bookDao" name="dao" class="com.itheima.dao.impl.BookDaoImpl"/>
</beans>
```

> **说明:**service起名bookEbi。**Ebi全称Enterprise Business Interface，翻译为企业业务接口**

**步骤2:根据name在容器中获取bean对象**

```java
public class AppForName {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        //此处根据bean标签的id属性和name属性的任意一个值来获取bean对象
        BookService bookService = (BookService) ctx.getBean("service4");
        bookService.save();
    }
}
```

**步骤3:运行程序**

测试结果为：

![](https://i-blog.csdnimg.cn/blog_migrate/c98b6274ed7cb759f904c3f2ba7f7f10.png)

> **注意事项:**
> 
> -   bean依赖注入的ref属性可以是指定bean的id或name，建议使用id注入
>     
>     ![](https://i-blog.csdnimg.cn/blog_migrate/15186bd76a75cca157e3ad2b214b8de6.png)
>     
> -   如果不存在,则会报错**NoSuchBeanDefinitionException**，如下:
>     
>     ![](https://i-blog.csdnimg.cn/blog_migrate/8eaa6883aacf1a0be9512eb5120a01b8.png)
>     
>     ![](https://i-blog.csdnimg.cn/blog_migrate/ad5e835c7b2c4d01e7e68d5fe44d2cdd.png)
>     
>     获取bean无论是通过id还是name获取，如果无法获取到，将抛出异常**NoSuchBeanDefinitionException**
>     

#### 4.1.3 bean作用范围scope配置，单例和非单例

![](https://i-blog.csdnimg.cn/blog_migrate/29c761b41316ef7b48fdae3ca98b03b7.png)

singleton译为单例，单独的人、物。

prototype译为非单例，原型、雏形

**默认情况下，Spring创建的bean对象都是单例的**。

**单例避免了对象的频繁创建与销毁**，**达到了bean对象的复用**。

> **验证IOC容器中对象是否为单例**
> 
> **单例singleton：** 下面两个引用指向同一个实例化的bean对象
> 
> ```java
>         BookDao bookDao1 = (BookDao) ctx.getBean("bookDao");
>         BookDao bookDao2 = (BookDao) ctx.getBean("bookDao");
> ```
> 
> **验证思路**
> 
> ​ 同一个bean获取两次，将对象打印到控制台，看打印出的地址值是否一致。
> 
> **具体实现**
> 
> -   创建一个AppForScope的类，在其main方法中来验证
>     
>     ```
>     public class AppForScope {
>         public static void main(String[] args) {
>             ApplicationContext ctx = new 
>                 ClassPathXmlApplicationContext("applicationContext.xml");
>     
>             BookDao bookDao1 = (BookDao) ctx.getBean("bookDao");
>             BookDao bookDao2 = (BookDao) ctx.getBean("bookDao");
>             System.out.println(bookDao1);
>             System.out.println(bookDao2);
>         }
>     }
>     ```
>     
> -   打印，观察控制台的打印结果![](https://i-blog.csdnimg.cn/blog_migrate/b2cd86102675c61a19517b7cd4847616.png)
>     
> -   结论:**默认情况下，Spring创建的bean对象都是单例的**
>     

获取到结论后，问题就来了，那如果我想创建出来非单例的bean对象，该如何实现呢?

**配置bean为非单例**

-   **将scope设置为`prototype`**
    
    ```XML
    <bean id="bookDao" name="dao" class="com.itheima.dao.impl.BookDaoImpl" scope="prototype"/>
    ```
    
    运行AppForScope，打印看结果
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/898f8b66b7f38745e1b0d26bb8da0d51.png)
    
-   结论，使用bean的`scope`属性可以控制bean的创建是否为单例：
    
    -   `singleton`默认为单例
    -   `prototype`为非单例

> **思考**
> 
> -   **为什么bean默认为单例?**
>     -   bean为单例的意思是在Spring的IOC容器中只会有该类的一个对象
>     -   bean对象只有一个就**避免了对象的频繁创建与销毁**，**达到了bean对象的复用**，性能高
> -   **bean在容器中是单例的，会不会产生线程安全问题?**
>     -   如果对象是**有状态对象**（该对象有成员变量可以用来存储数据的）
>     -   因为所有请求线程共用一个bean对象，所以会**存在线程安全问题**。
>     -   如果对象是**无状态对象**（该对象没有成员变量没有进行数据存储的，不建议存在IOC容器中）
>     -   因方法中的局部变量在方法调用完成后会被销毁，所以**不会存在线程安全问题**。
> -   **哪些bean对象适合交给容器进行管理?**
>     -   表现层对象
>     -   业务层对象
>     -   数据层对象
>     -   工具对象
> -   **哪些bean对象不适合交给容器进行管理?**
>     -   **封装实例的域对象**，因为会引发线程安全问题，所以不适合。
> -   **JSP四大域对象**
> 
> 1.page域对象（只在当前页面中有效）
> 
> 2.request域对象（只在一次请求中有效，服务端跳转有效，客户端跳转无效）
> 
> 3.session域对象（在一次会话中有效，服务端客户端跳转都有效）
> 
> 4.application域对象（在整个应用程序中都有效）
> 
> **域对象：**可以在不同的[Servlet](https://so.csdn.net/so/search?q=Servlet&spm=1001.2101.3001.7020 "Servlet")中进行数据传递的对象就称为域对象。
> 
> **域对象必须有的方法：**
> 
> ```java
>     setAttribute(name,value);存储数据的方法
>     getAttribute(name);根据name获取对应数据值
>     removeAttribute(name)；删除数据
> ```

### 4.2 bean的三种创建方式

> 思考：
> 
> **容器是如何来创建对象的呢?**
> 
> bean本质上就是对象，对象在new的时候会使用构造方法完成，那创建bean也是使用构造方法完成的。

在这块内容中主要解决两部分内容，分别是

-   bean是如何创建的
-   实例化bean的三种方式，`构造方法`,`静态工厂`和`实例工厂`

#### 4.2.1 环境准备

重新准备个开发环境，

-   创建一个Maven项目
-   pom.xml添加Spring依赖
-   resources下添加spring的配置文件applicationContext.xml

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/2173c78e3bc717e026c66b841bbb17e3.png)

#### 4.2.2 bean的创建方法:1：无参构造方法实例化（常用）

**Spring底层是通过反射的无参构造方法创建类的对象bean。** 

**步骤1:准备需要被创建的类**

准备一个BookDao和BookDaoImpl类

```java

public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

**步骤2:将类配置到Spring容器**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>

</beans>
```

**步骤3:编写运行程序**

```java
public class AppForInstanceBook {
    public static void main(String[] args) {
        ApplicationContext ctx = new 
            ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.save();

    }
}
```

**步骤4:DAO类中提供无参构造函数测试，证明IOC容器创建对象通过无参构造方法**

在BookDaoImpl类中添加一个无参构造函数，并打印一句话，方便观察结果。

```java
public class BookDaoImpl implements BookDao {
    public BookDaoImpl() {
        System.out.println("book dao constructor is running ....");
    }
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

运行程序，如果控制台有打印构造函数中的输出，说明Spring容器在创建对象的时候也走的是构造函数

![](https://i-blog.csdnimg.cn/blog_migrate/6c00968d3f75cdaceb0dd5c43aa9aa2a.png)

**步骤5:将构造函数改成私有，证明IOC容器通过反射调用无参构造方法**

```java
public class BookDaoImpl implements BookDao {
    private BookDaoImpl() {
        System.out.println("book dao constructor is running ....");
    }
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

运行程序，能执行成功,说明内部走的依然是构造函数,能访问到类中的私有构造方法,显而易见**Spring底层用的是反射**

![](https://i-blog.csdnimg.cn/blog_migrate/05574085dced1d3d40d973343a2b5e56.png)

**步骤6:构造函数中添加一个参数，证明IOC通过无参数的构造方法创建bean**

```java
public class BookDaoImpl implements BookDao {
    private BookDaoImpl(int i) {
        System.out.println("book dao constructor is running ....");
    }
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

运行程序，

**程序会报错**，说明**Spring底层使用的是类的无参构造方法**。

![](https://i-blog.csdnimg.cn/blog_migrate/9d3460378e8ff114b109119e140cec8b.png)

#### 4.2.3 Spring的报错信息从下往上看

![](https://i-blog.csdnimg.cn/blog_migrate/9d3460378e8ff114b109119e140cec8b.png)

-   **错误信息从下往上依次查看**，因为上面的错误大都是对下面错误的一个包装，**最核心错误是在最下面**
-   Caused by: java.lang.NoSuchMethodException: com.itheima.dao.impl.BookDaoImpl.`<init>`()
    -   Caused by 翻译为`引起`，即出现错误的原因
    -   java.lang.NoSuchMethodException:抛出的异常为`没有这样的方法异常`
    -   com.itheima.dao.impl.BookDaoImpl.`<init>`():哪个类的哪个方法没有被找到导致的异常，**`<init>`()指定是类的无参构造方法**

如果最后一行错误获取不到错误信息，接下来查看第二层:

Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate \[com.itheima.dao.impl.BookDaoImpl\]: No default constructor found; nested exception is java.lang.NoSuchMethodException: com.itheima.dao.impl.BookDaoImpl.`<init>`()

-   nested:嵌套的意思，后面的异常内容和最底层的异常是一致的
-   Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate \[com.itheima.dao.impl.BookDaoImpl\]: No default constructor found;
    -   Caused by: `引发`
    -   BeanInstantiationException:翻译为`bean实例化异常`
    -   No default constructor found:没有一个默认的构造函数被发现

看到这其实错误已经比较明显，给大家个练习，把倒数第三层的错误分析下吧:

Exception in thread "main" org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'bookDao' defined in class path resource \[applicationContext.xml\]: Instantiation of bean failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate \[com.itheima.dao.impl.BookDaoImpl\]: No default constructor found; nested exception is java.lang.NoSuchMethodException: com.itheima.dao.impl.BookDaoImpl.`<init>`()。

至此，关于Spring的构造方法实例化就已经学习完了，因为每一个类默认都会提供一个无参构造函数，所以其实真正在使用这种方式的时候，我们什么也不需要做。这也是我们以后比较常用的一种方式。

#### 4.2.4 bean的创建方式2：静态工厂实例化（了解）

静态工厂一般在service层里使用，用于获取dao对象。 

> **了解为主，**这种方式一般是用来兼容早期的一些老系统，所以**了解为主**。

> **回顾，工厂方式创建对象**
> 
> 以前最常接触到的工厂类是封装SqlSessionFactory工具类，提高代码复用性、通过静态代码块避免工厂类资源浪费。
> 
> ```java
> public class SqlSessionFactoryUtils {
> 
>     private static SqlSessionFactory sqlSessionFactory;
> 
>     static {
>         //静态代码块会随着类的加载而自动执行，且只执行一次
>         try {
>             String resource = "mybatis-config.xml";
>             InputStream inputStream = Resources.getResourceAsStream(resource);
>             sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
>         } catch (IOException e) {
>             e.printStackTrace();
>         }
>     }
> 
> 
>     public static SqlSessionFactory getSqlSessionFactory(){
>         return sqlSessionFactory;
>     }
> }
> ```
> 
> ```java
> SqlSessionFactory sqlSessionFactory=SqlSessionFactoryUtils.getSqlSessionFactory();
> ```

**工厂方式创建bean** 

(1)准备一个OrderDao和OrderDaoImpl类

```java
public interface OrderDao {
    public void save();
}

public class OrderDaoImpl implements OrderDao {
    public void save() {
        System.out.println("order dao save ...");
    }
}
```

(2)创建一个工厂类**OrderDaoFactory**并提供一个**静态方法创建对象**

```java
//静态工厂创建对象
public class OrderDaoFactory {
    public static OrderDao getOrderDao(){
        return new OrderDaoImpl();
    }
}
```

(3)编写AppForInstanceOrder运行类，在类中**通过工厂获取对象**

```java
public class AppForInstanceOrder {
    public static void main(String[] args) {
        //通过静态工厂创建对象
        OrderDao orderDao = OrderDaoFactory.getOrderDao();
        orderDao.save();
    }
}
```

(4)运行后，可以查看到结果

![](https://i-blog.csdnimg.cn/blog_migrate/bc686d0f703b1a18b7fd65b368432ea7.png)

**Spring静态工厂实例化**

具体实现步骤为:

**(1)在spring的配置文件application.properties中配置工厂类的bean**

```XML
<bean id="orderDao" class="com.itheima.factory.OrderDaoFactory" factory-method="getOrderDao"/>
```

class:工厂类的类全名

**factory-mehod:具体工厂类中创建对象的方法名**

对应关系如下图:

![](https://i-blog.csdnimg.cn/blog_migrate/143f18d97f133ebc2465fdee1fc9fb09.png)

**(2)在AppForInstanceOrder运行类，使用从IOC容器中获取bean的方法进行运行测试**

```java
public class AppForInstanceOrder {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        //直接获取dao对象。获取方式是调用配置的factory里的静态方法getOrderDao
        OrderDao orderDao = (OrderDao) ctx.getBean("orderDao");

        orderDao.save();

    }
}
```

(3)运行后，可以查看到结果

![](https://i-blog.csdnimg.cn/blog_migrate/fe7450c8f9d54cda479b9c904b4ec2d0.png)

**出现问题：工厂类中也是直接new对象的，和自己直接new的区别**

**主要的原因是:**

-   在工厂的静态方法中，我们除了new对象还可以做其他的一些业务操作，这些操作必不可少,如SqlSessionFactoryUtil类里有静态代码块创建SqlSessionFactory对象。又例如:

```java
public class OrderDaoFactory {
    public static OrderDao getOrderDao(){
        System.out.println("factory setup....");//模拟必要的业务操作
        return new OrderDaoImpl();
    }
}
```

![](https://i-blog.csdnimg.cn/blog_migrate/fe1565712d7f0b2500a51cc25622d36d.png)

这种方式一般是用来兼容早期的一些老系统，所以**了解为主**。

#### 4.2.5 bean的创建方式3：实例工厂（了解）与FactoryBean（常用）

**环境准备**

(1)准备一个UserDao和UserDaoImpl类

```java
public interface UserDao {
    public void save();
}

public class UserDaoImpl implements UserDao {

    public void save() {
        System.out.println("user dao save ...");
    }
}
```

(2)创建一个工厂类OrderDaoFactory并提供一个普通方法，注意此处和静态工厂的工厂类不一样的地方是**方法不是静态方法**

```java
public class UserDaoFactory {
    public UserDao getUserDao(){
        return new UserDaoImpl();
    }
}
```

(3)编写AppForInstanceUser运行类，在类中通过工厂获取对象

```java
public class AppForInstanceUser {
    public static void main(String[] args) {
        //创建实例工厂对象
        UserDaoFactory userDaoFactory = new UserDaoFactory();
        //通过实例工厂对象创建对象
        UserDao userDao = userDaoFactory.getUserDao();
        userDao.save();
}
```

(4)运行后，可以查看到结果

![](https://i-blog.csdnimg.cn/blog_migrate/bd46e38b0c766a881b22ec9ed2a9b8b8.png)

对于上面这种实例工厂的方式如何交给Spring管理呢?

**实例工厂实例化方法A**

> **了解即可**，更多用下面方法B，**FactoryBean**

**(1)在spring的配置文件中添加以下内容:**

```XML
<!--   第一步，创建实例化工厂对象，实际无意义，主要为了第二步用它-->
<bean id="userFactory" class="com.itheima.factory.UserDaoFactory"/>
<!--   第二步，调用实例化工厂对象中的方法来创建bean，不用class属性是因为getUserDao返回值是UserDao，ioc容器是可以找到UserDao的-->
<bean id="userDao" factory-method="getUserDao" factory-bean="userFactory"/>
```

**实例化工厂运行的顺序是:**

-   **创建实例化工厂对象**,对应的是第一行配置
    
-   **调用对象中的方法来创建bean**，对应的是第二行配置
    
    -   **factory-bean:**工厂的实例对象
        
    -   **factory-method:**工厂bean的id,对应关系如下:
        
        ![](https://i-blog.csdnimg.cn/blog_migrate/b4df15db9d87a400da1a7af1140fa5ac.png)
        

factory-mehod:具体工厂类中创建对象的方法名

(2)在AppForInstanceUser运行类，使用从IOC容器中获取bean的方法进行运行测试

```java
public class AppForInstanceUser {
    public static void main(String[] args) {
        ApplicationContext ctx = new 
            ClassPathXmlApplicationContext("applicationContext.xml");
        UserDao userDao = (UserDao) ctx.getBean("userDao");
        userDao.save();
    }
}
```

(3)运行后，可以查看到结果

![](https://i-blog.csdnimg.cn/blog_migrate/34167cdf0706a5662ab5e5a2312ea860.png)

实例工厂实例化的方式就已经介绍完了，配置的过程还是比较复杂，所以Spring为了简化这种配置方式就提供了一种叫`FactoryBean`的方式来简化开发。

**实例工厂实例化方法B：FactoryBean的使用**

(1)创建一个UserDaoFactoryBean的类，**实现FactoryBean接口**，重写接口的方法。**这两个方法会在创建ApplicationContext对象时候就先后调用。**

```java
public class UserDaoFactoryBean implements FactoryBean<UserDao> {
    //代替原始实例工厂中创建对象的方法
    public UserDao getObject() throws Exception {
        //返回dao实现类的实例
        return new UserDaoImpl();
    }
    //返回所创建类的Class对象
    public Class<?> getObjectType() {
        //返回dao接口的字节码
        return UserDao.class;
    }
}
```

(2)在Spring的配置文件中进行配置，注意class里UserDaoFactoryBean

```XML
<bean id="userDao" class="com.itheima.factory.UserDaoFactoryBean"/>
```

(3)AppForInstanceUser运行类不用做任何修改，直接运行

![](https://i-blog.csdnimg.cn/blog_migrate/847d733c747acee7e34cc0114726c80e.png)

>  **注意：**
> 
> 在IOC容器创建时会直接创建其内所有bean对象，像下面代码，即使没有调用任何方法，运行后会输出getObject和getObjectType
> 
> ```java
> public class BookDaoFactoryBean implements FactoryBean<BookDao> {
>     @Override
>     public BookDao getObject() throws Exception {
>         System.out.println("getObject");
>         return new BookDaoImpl();
>     }
> 
>     @Override
>     public Class<?> getObjectType() {
>         System.out.println("getObjectType");
>         return BookDao.class;
>     }
> }
> ```
> 
> ```java
> ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/0942aac75c97ed4d5bdcc7b193c6919c.png)

这种方式在Spring去整合其他框架的时候会被用到，所以这种方式需要大家理解掌握。

**FactoryBean接口的三个方法**

查看源码会发现，FactoryBean接口其实会有三个方法，分别是:

```java
T getObject() throws Exception;

Class<?> getObjectType();

default boolean isSingleton() {
        return true;
}
```

方法一:getObject()，被重写后，在方法中进行对象的创建并返回

方法二:getObjectType(),被重写后，主要返回的是被创建类的Class对象

方法三:没有被重写，因为它已经给了默认值，从方法名中可以看出其作用是设置对象是否为单例，默认true，从意思上来看，我们猜想默认应该是单例，如何来验证呢?

思路很简单，就是从容器中获取该对象的多个值，打印到控制台，查看是否为同一个对象。

```java
public class AppForInstanceUser {
    public static void main(String[] args) {
        ApplicationContext ctx = new 
            ClassPathXmlApplicationContext("applicationContext.xml");
        UserDao userDao1 = (UserDao) ctx.getBean("userDao");
        UserDao userDao2 = (UserDao) ctx.getBean("userDao");
        System.out.println(userDao1);
        System.out.println(userDao2);
    }
}
```

打印结果，如下:

![](https://i-blog.csdnimg.cn/blog_migrate/896194b771716dafcce8e59ed9c77c52.png)

通过验证，会发现默认是单例。

**FactoryBean设置单例、非单例：**

只需要将isSingleton()方法进行重写，修改返回为false，即可

```java
//FactoryBean创建对象
public class UserDaoFactoryBean implements FactoryBean<UserDao> {
    //代替原始实例工厂中创建对象的方法
    public UserDao getObject() throws Exception {
        return new UserDaoImpl();
    }

    public Class<?> getObjectType() {
        return UserDao.class;
    }

    public boolean isSingleton() {
        return false;
    }
}
```

重新运行AppForInstanceUser，查看结果

![](https://i-blog.csdnimg.cn/blog_migrate/b395e8803edee8e951b475e7bc9b7960.png)

从结果中可以看出现在已经是非单例了，但是一般情况下我们都会采用单例，也就是采用默认即可。所以isSingleton()方法一般不需要进行重写。

#### 4.2.6 bean实例化小结

通过这一节的学习，需要掌握:

(1)bean是如何创建的呢?

```
构造方法
```

(2)Spring的IOC实例化对象的三种方式分别是:

-   **构造方法(常用)**
-   **静态工厂(了解)**
-   **实例工厂(了解)**
    -   **FactoryBean(实用)**

这些方式中，重点掌握`构造方法`和`FactoryBean`即可。

需要注意的一点是，构造方法在类中默认会提供，但是如果重写了构造方法，默认的就会消失，在使用的过程中需要注意，如果需要重写构造方法，最好把默认的构造方法也重写下。

### 4.3 bean的生命周期

**思考：**

-   什么是生命周期?
    -   从创建到消亡的完整过程,例如人从出生到死亡的整个过程就是一个生命周期。
-   **bean生命周期是什么?**
    -   bean对象从创建到销毁的整体过程。
-   **bean生命周期控制是什么**?
    -   在bean创建后到销毁前做一些事情。

#### 4.3.1 环境准备

为了方便大家后期代码的阅读，我们重新搭建下环境:

-   创建一个Maven项目
-   pom.xml添加依赖
-   resources下添加spring的配置文件applicationContext.xml

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/2d49d188331bbdf3343ab471356b088a.png)

(1)项目中添加BookDao、BookDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
}

public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
</beans>
```

(3)编写AppForLifeCycle运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForLifeCycle {
    public static void main( String[] args ) {
        ApplicationContext ctx = new 
            ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.save();
    }
}
```

#### 4.3.2 生命周期控制

接下来，在上面这个环境中来为BookDao添加生命周期的控制方法，具体的控制有两个阶段:

-   bean**创建init**之后，想要添加内容，比如用来初始化需要用到资源
-   bean**销毁destory**之前，想要添加内容，比如用来释放用到的资源

**步骤1:添加初始化和销毁方法**

针对这两个阶段，我们在BooDaoImpl类中分别添加两个方法，**方法名任意**

```java
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
    //表示bean初始化对应的操作
    public void init(){
        System.out.println("init...");
    }
    //表示bean销毁前对应的操作
    public void destory(){
        System.out.println("destory...");
    }
}
```

**步骤2:配置生命周期**

在配置文件添加配置，如下:

```XML
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl" init-method="init" destroy-method="destory"/>
```

**步骤3:运行程序**

运行AppForLifeCycle打印结果为:

![](https://i-blog.csdnimg.cn/blog_migrate/9f0f4b4777d36579d290a64cf9006edb.png)

从结果中可以看出，**init方法执行了，但是destroy方法却未执行**，这是为什么呢?

-   Spring的**IOC容器是运行在JVM中**
-   运行main方法后,JVM启动,Spring加载配置文件生成IOC容器,从容器获取bean对象，然后调方法执行
-   main方法执行完后，**JVM退出**，这个时候IOC容器中的**bean还没有来得及销毁就已经结束了**
-   所以没有调用对应的destroy方法

**解决办法1：**使用ClassPathXmlApplicationContext的**close方法**。

**解决方法2：注册钩子**关闭容器

另外还可以用Spring的两个接口**`InitializingBean`， `DisposableBean`**实现初始化和销毁，但想要销毁方法执行出来还得用上面两种解决办法。

#### 4.3.3 关闭IOC容器方法：close关闭容器、**注册钩子关闭容器**

> **了解即可**，主要用4.3.4中的**`InitializingBean`， `DisposableBean`控制生命周期** 

**close关闭容器**

-   ApplicationContext中没有close方法
    
-   需要将ApplicationContext更换成ClassPathXmlApplicationContext
    
    ```java
    ClassPathXmlApplicationContext ctx = new 
        ClassPathXmlApplicationContext("applicationContext.xml");
    ```
    
-   调用ctx的close()方法
    
    ```java
    ctx.close();
    ```
    
-   运行程序，就能执行destroy方法的内容
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/680024421f17772835f60ff74e3a14b9.png)
    

**销毁方法二：注册钩子关闭容器**

-   在容器未关闭之前，提前设置好回调函数，让JVM在退出之前回调此函数来关闭容器
    
-   调用ClassPathXmlApplicationContext的registerShutdownHook()方法
    
    ```java
    ctx.registerShutdownHook();
    ```
    
    **注意:**registerShutdownHook在ApplicationContext中也没有
    
-   运行后，查询打印结果
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/96f905498c160abd0d1143fbf26ba62e.png)
    

两种方式介绍完后，close和registerShutdownHook选哪个?

**相同点:**这两种都能用来关闭容器

**不同点:**

close()是在**调用的时候**强制关闭，如果后面还有IOC的相关代码会报错。

registerShutdownHook()是在**JVM退出前调用**关闭。

#### 4.3.4 **`InitializingBean`， `DisposableBean`控制生命周期**

**`Disposable译为用完即丢弃的，一次性的`**

Spring提供了两个接口来完成生命周期的控制，好处是可以不用再进行配置`init-method`和`destroy-method，坏处是`想要销毁方法执行出来还得用上面两种解决办法。

**代码示例：**

修改service实现类BookServiceImpl，添加两个接口`InitializingBean`， `DisposableBean`并实现接口中的两个方法`afterPropertiesSet`和`destroy`

```java
public class BookServiceImpl implements BookService, InitializingBean, DisposableBean {
    private BookDao bookDao;
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
    public void save() {
        System.out.println("book service save ...");
        bookDao.save(); 
    }
    public void destroy() throws Exception {
        System.out.println("service destroy");
    }
    public void afterPropertiesSet() throws Exception {
        System.out.println("service init");
    }
}
```

```java
public class BookDaoImpl implements BookDao {
    @Override
    public void save() {
        System.out.println("BookDao save...");
    }

    private void init() {
        System.out.println("book dao init");
    }

    private void destroy() {
        System.out.println("book dao destroy");
    }
}
```

​​​​​​​ 

```XML
    <bean id="bookDao" class="package1.dao.impl.BookDaoImpl" init-method="init" destroy-method="destroy"/>
    <bean id="bookService" class="package1.service.impl.BookServiceImpl" >
        <property name="bookDao" ref="bookDao"/>
    </bean>
```

```java
public class Demo {
    public static void main(String[] args) {
//        ClassPathXmlApplicationContext了解即可，有new后面会被优化
        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        System.out.println("创建IOC容器后...");
        BookDao bookDao=(BookDao)applicationContext.getBean("bookDao");
        bookDao.save();

        applicationContext.close();
    }
}
```

重新运行AppForLifeCycle类，

![](https://i-blog.csdnimg.cn/blog_migrate/d4567525fc0cabae6dfb2d03e5320379.png)

> 思考：
> 
> **dao先初始化、最后销毁的原因：**
> 
> 配置的初始化和销毁方法，要更严格，实现接口的方法都是创建和销毁中间完成的。
> 
> **控制台出现service的原因：**
> 
> **创建IOC容器时会创建所有的bean对象，并加载这些对象的init和destroy方法。**
> 
> 就像前面4.2.5 FactoryBean那里，创建IOC容器时候会调用getObject和getObjectType方法。

**小细节**

-   对于InitializingBean接口中的afterPropertiesSet方法，翻译过来为`属性设置之后`。
    
-   对于BookServiceImpl来说，bookDao是它的一个属性，setBookDao方法是Spring的IOC容器为其注入属性的方法
    
-   ​​​​​​​**思考:afterPropertiesSet和setBookDao谁先执行?**
    
    -   从方法名分析，猜想应该是setBookDao方法先执行
        
    -   验证思路，在setBookDao方法中添加一句话
        
        ```java
        public void setBookDao(BookDao bookDao) {
                System.out.println("set .....");
                this.bookDao = bookDao;
            }
        ```
        
    -   重新运行AppForLifeCycle，打印结果如下:
        
        ![](https://i-blog.csdnimg.cn/blog_migrate/da27c2e6df20cfd1e1ccf120603cb4ad.png)
        
        验证的结果和我们猜想的结果是一致的，所以初始化方法会在类中属性设置之后执行。
        

#### 4.3.5 bean生命周期小结

(1)关于Spring中对bean生命周期控制提供了两种方式:

-   在配置文件中的bean标签中添加`init-method`和`destroy-method`属性
-   类实现`InitializingBean`与`DisposableBean`接口，这种方式了解下即可。

(2)对于bean的生命周期控制在bean的整个生命周期中所处的位置如下:

-   初始化容器
    -   1.创建对象(内存分配)
    -   2.执行构造方法
    -   3.执行属性注入(set操作)
    -   **4.执行bean初始化方法**
-   使用bean
    -   1.执行业务操作
-   关闭/销毁容器
    -   **1.执行bean销毁方法**

(3)关闭容器的两种方式:

-   ConfigurableApplicationContext是ApplicationContext的子类
    -   close()方法
    -   registerShutdownHook()方法

## 5，DI相关内容

> 前面我们已经完成了bean相关操作的讲解，接下来就进入第二个大的模块`DI依赖注入`，首先来介绍下Spring中有哪些注入方式?
> 
> 我们先来**思考**
> 
> -   向一个类中传递数据的方式有几种?
>     -   普通方法(set方法)
>     -   构造方法
> -   依赖注入描述了在容器中建立bean与bean之间的依赖关系的过程，如果bean运行需要的是数字或字符串呢?
>     -   引用类型（前面3.2快速入门方案，service里注入dao的引用）
>     -   简单类型(基本数据类型与String)

**Spring提供了两种注入方式：**

-   **setter注入**
    -   简单类型
    -   引用类型（前面3.2快速入门方案）
-   **构造器注入**
    -   简单类型
    -   引用类型

### 5.1 setter注入

1.  对于setter方式注入引用类型的方式之前已经学习过，快速回顾下:
    
2.  在bean中定义引用类型属性，并提供可访问的**set**方法
    

```java
public class BookServiceImpl implements BookService {
    private BookDao bookDao;
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
}
```

-   配置中使用**property**标签**ref**属性注入引用类型对象

```XML
<bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
    <property name="bookDao" ref="bookDao"/>
</bean>

<bean id="bookDao" class="com.itheima.dao.imipl.BookDaoImpl"/>
```

#### 5.1.1 环境准备

为了更好的学习下面内容，我们依旧准备一个新环境:

-   创建一个Maven项目
-   pom.xml添加依赖
-   resources下添加spring的配置文件

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/8a24e90259ba05839772c048e5dc94b5.png)

(1)项目中添加BookDao、BookDaoImpl、UserDao、UserDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface UserDao {
    public void save();
}
public class UserDaoImpl implements UserDao {
    public void save() {
        System.out.println("user dao save ...");
    }
}

public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

(3)编写AppForDISet运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForDISet {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookService bookService = (BookService) ctx.getBean("bookService");
        bookService.save();
    }
}
```

接下来，在上面这个环境中来完成setter注入的学习:

#### 5.1.2 注入多个引用数据类型（property标签的name和ref）

因为有ref，所以叫引用数据类型，引用值是被注入类里定义的私有注入类的对象。

> 需求:在bookServiceImpl对象中注入userDao
> 
> 1.在BookServiceImpl中声明userDao属性
> 
> 2.为userDao属性提供setter方法
> 
> 3.在配置文件中使用property标签注入

**步骤1:声明属性并提供setter方法**

在BookServiceImpl中声明userDao属性，并提供setter方法

```java
public class BookServiceImpl implements BookService{
    private BookDao bookDao;
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
        userDao.save();
    }
}
```

**步骤2:配置文件中进行注入配置**

在applicationContext.xml配置文件中使用property标签注入

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
        <property name="userDao" ref="userDao"/>
    </bean>
</beans>
```

![](https://i-blog.csdnimg.cn/blog_migrate/3f6394d8f258ff2ebc69116809418542.png)

**步骤3:运行程序**

运行AppForDISet类，查看结果，说明userDao已经成功注入。

![](https://i-blog.csdnimg.cn/blog_migrate/c6f3e63eb8d9f1b9da017862dc35f77e.png)

#### 5.1.3 注入简单数据类型（property标签的name和value）

> **需求：**
> 
> 给BookDaoImpl注入一些简单数据类型的数据
> 
> 参考引用数据类型的注入，我们可以推出具体的步骤为:
> 
> 1.在BookDaoImpl类中声明对应的简单数据类型的属性
> 
> 2.为这些属性提供对应的setter方法
> 
> 3.在applicationContext.xml中配置

> **思考:**
> 
> **问题：**引用类型使用的是`<property name="" ref=""/>`,简单数据类型还是使用ref么?
> 
> **答案：**不是ref，二手property标签的name和value。
> 
> 问题：ref是指向Spring的IOC容器中的另一个bean对象的，对于简单数据类型，没有对应的bean对象，该如何配置?
> 
> 答案：

**步骤1:声明属性并提供setter方法**

在BookDaoImpl类中声明对应的简单数据类型的属性,并提供对应的setter方法

```java
public class BookDaoImpl implements BookDao {

    private String databaseName;
    private int connectionNum;

    public void setConnectionNum(int connectionNum) {
        this.connectionNum = connectionNum;
    }

    public void setDatabaseName(String databaseName) {
        this.databaseName = databaseName;
    }

    public void save() {
        System.out.println("book dao save ..."+databaseName+","+connectionNum);
    }
}
```

**步骤2:配置文件中进行注入配置**

在applicationContext.xml配置文件中使用property标签注入

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
        <property name="databaseName" value="mysql"/>
         <property name="connectionNum" value="10"/>
    </bean>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
        <property name="userDao" ref="userDao"/>
    </bean>
</beans>
```

property标签里，name填的是bean类里定义的私有变量名，value填的是注入的值。

> **注意:**
> 
> value后面跟的是简单数据类型，注意数据类型格式。
> 
> 对于参数类型，Spring在注入的时候会自动转换，但是不能写成
> 
> ```XML
> <property name="connectionNum" value="abc"/>
> ```
> 
> 这样的话，spring在将`abc`转换成int类型的时候就会报错。

**步骤3:运行程序**

运行AppForDISet类，查看结果，说明userDao已经成功注入。

![](https://i-blog.csdnimg.cn/blog_migrate/f314710c84c8df3471768d8f5e456a0a.png)

**注意:**两个property注入标签的顺序可以任意。

对于setter注入方式的基本使用就已经介绍完了，

-   对于引用数据类型使用的是`<property name="" ref=""/>`
-   对于简单数据类型使用的是`<property name="" value=""/>`

### 5.2 构造器注入

#### 5.2.1 环境准备

构造器注入也就是构造方法注入，学习之前，还是先准备下环境，和前面的都一致:

-   创建一个Maven项目
-   pom.xml添加依赖
-   resources下添加spring的配置文件

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/1896c51cb0ef38463619a908ada52957.png)

(1)项目中添加BookDao、BookDaoImpl、UserDao、UserDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {

    private String databaseName;
    private int connectionNum;

    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface UserDao {
    public void save();
}
public class UserDaoImpl implements UserDao {
    public void save() {
        System.out.println("user dao save ...");
    }
}

public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

(3)编写AppForDIConstructor运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForDIConstructor {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookService bookService = (BookService) ctx.getBean("bookService");
        bookService.save();
    }
}
```

#### 5.2.2 构造器注入引用数据类型（constructor-arg标签的name和ref）

接下来，在上面这个环境中来完成构造器注入的学习:

> 需求：将BookServiceImpl类中的bookDao修改成使用构造器的方式注入。
> 
> 1.将bookDao的setter方法删除掉
> 
> 2.添加带有bookDao参数的构造方法
> 
> 3.在applicationContext.xml中配置

**步骤1:删除setter方法并提供构造方法**

在BookServiceImpl类中将bookDao的setter方法删除掉,并添加带有bookDao参数的构造方法

```java
public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public BookServiceImpl(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

**步骤2:配置文件中进行配置构造方式注入**

在applicationContext.xml中配置，bean便签中的constructor-arg便签

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <constructor-arg name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

> **说明:**
> 
> arg是argument的缩写，译为参数、争论、理由。constructor-arg译为构造参数。
> 
> **标签constructor-arg**的属性
> 
> -   **name属性：**对应的值为**构造函数中方法形参的参数名**，不是私有成员变量名，必须要保持一致。
>     
> -   **ref属性：**指向的是spring的IOC容器中其他bean对象的id。
>     

**步骤3：运行程序**

运行AppForDIConstructor类，查看结果，说明bookDao已经成功注入。

![](https://i-blog.csdnimg.cn/blog_migrate/55eb323b5887d8b3949eadaa8b733cf8.png)

#### 5.2.3 构造器注入多个引用数据类型

> 需求:在BookServiceImpl使用构造函数注入多个引用数据类型，比如userDao
> 
> 1.声明userDao属性
> 
> 2.生成一个带有bookDao和userDao参数的构造函数
> 
> 3.在applicationContext.xml中配置注入

**步骤1:提供多个属性的构造函数**

在BookServiceImpl声明userDao并提供多个参数的构造函数

```java
public class BookServiceImpl implements BookService{
    private BookDao bookDao;
    private UserDao userDao;

    public BookServiceImpl(BookDao bookDao,UserDao userDao) {
        this.bookDao = bookDao;
        this.userDao = userDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
        userDao.save();
    }
}
```

**步骤2:配置文件中配置多参数注入**

在applicationContext.xml中配置注入

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <constructor-arg name="bookDao" ref="bookDao"/>
        <constructor-arg name="userDao" ref="userDao"/>
    </bean>
</beans>
```

> **说明:**这两个`<contructor-arg>`的配置顺序可以任意

**步骤3:运行程序**

运行AppForDIConstructor类，查看结果，说明userDao已经成功注入。

![](https://i-blog.csdnimg.cn/blog_migrate/b37d626e58fc17b32651d1e59bc41fc9.png)

#### 5.2.4 构造器注入多个简单数据类型（constructor-arg标签的name和value）

> 需求:在BookDaoImpl中，使用构造函数注入databaseName和connectionNum两个参数。
> 
> 参考引用数据类型的注入，我们可以推出具体的步骤为:
> 
> 1.提供一个包含这两个参数的构造方法
> 
> 2.在applicationContext.xml中进行注入配置

**步骤1:添加多个简单属性并提供构造方法**

修改BookDaoImpl类，添加构造方法

```java
public class BookDaoImpl implements BookDao {
    private String databaseName;
    private int connectionNum;

    public BookDaoImpl(String databaseName, int connectionNum) {
        this.databaseName = databaseName;
        this.connectionNum = connectionNum;
    }

    public void save() {
        System.out.println("book dao save ..."+databaseName+","+connectionNum);
    }
}
```

**步骤2:配置完成多个属性构造器注入**

在applicationContext.xml中进行注入配置，bean标签内constructor-arg标签的属性name和value

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
        <constructor-arg name="databaseName" value="mysql"/>
        <constructor-arg name="connectionNum" value="666"/>
    </bean>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <constructor-arg name="bookDao" ref="bookDao"/>
        <constructor-arg name="userDao" ref="userDao"/>
    </bean>
</beans>
```

**说明:**这两个`<contructor-arg>`的配置顺序可以任意

**步骤3:运行程序**

运行AppForDIConstructor类，查看结果

![](https://i-blog.csdnimg.cn/blog_migrate/e9acea74765a8368c46a6b5832b737b8.png)

**存在问题:name属性的紧耦合**

![](https://i-blog.csdnimg.cn/blog_migrate/667e2ce06d4e932b038b894b4167bd6a.png)

-   当构造函数中方法的参数名发生变化后，配置文件中的name属性也需要跟着变
-   这两块存在**紧耦合**，具体该如何解决?

**解决方案（有缺点，了解即可）：**

> **了解即可。**参数名发生变化的情况并不多，并且解决方案有缺点类型限制或顺序限制。

**方式一:**删除name属性，添加type属性，**按照类型注入**

```XML
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
    <constructor-arg type="int" value="10"/>
    <constructor-arg type="java.lang.String" value="mysql"/>
</bean>
```

-   这种方式可以解决构造函数形参名发生变化带来的耦合问题
-   但是如果构造方法参数中**有类型相同的参数**，这种方式就**不太好实现**了

**方式二:**删除type属性，添加index属性，**按照索引下标注入**，下标从0开始

```XML
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
    <constructor-arg index="1" value="100"/>
    <constructor-arg index="0" value="mysql"/>
</bean>
```

-   这种方式可以解决参数类型重复问题
-   但是如果构造方法参**数顺序发生变化后**，这种方式又带来了**耦合问题**

### **5.2.5 依赖注入方式选择**

1.  **强制依赖**使用**构造器**进行，使用**setter注入有概率不进行注入导致null对象**出现。**强制依赖**指对象在创建的过程中必须要注入指定的参数。
2.  **可选依赖**使用**setter**注入进行，灵活性强。**可选依赖**指对象在创建过程中注入的参数可有可无
3.  **Spring框架倡导使用构造器**，第三方框架内部大多数采用构造器注入的形式进行数据初始化，相对严谨
4.  如果有必要**可以两者同时使用**，使用构造器注入完成强制依赖的注入，使用setter注入完成可选依赖的注入
5.  实际开发过程中还要根据实际情况分析，如果受控对象没有提供setter方法就必须使用构造器注入
6.  ****自己开发的模块推荐优先使用setter注入****

**总结：**建议用setter注入。 

这节中主要讲解的是Spring的依赖注入的实现方式:

-   setter注入
    
    -   简单数据类型
        
        ```XML
        <bean ...>
            <property name="" value=""/>
        </bean>
        ```
        
    -   引用数据类型
        
        ```XML
        <bean ...>
            <property name="" ref=""/>
        </bean>
        ```
        
-   构造器注入
    
    -   简单数据类型
        
        ```XML
        <bean ...>
            <constructor-arg name="" index="" type="" value=""/>
        </bean>
        ```
        
    -   引用数据类型
        
        ```XML
        <bean ...>
            <constructor-arg name="" index="" type="" ref=""/>
        </bean>
        ```
        
-   依赖注入的方式选择上
    
    -   建议使用setter注入
    -   第三方技术根据情况选择

### 5.3 自动配置依赖注入

前面花了大量的时间把Spring的注入去学习了下，很**麻烦**，可以使用**自动配置**优化。

#### 5.3.1 什么是依赖自动装配?

-   **IoC容器**根据bean所依赖的资源在容器中**自动查找并注入**到bean中的过程称为自动装配

#### 5.3.2 自动装配方式有哪些?

-   **按类型（常用）**
-   按名称
-   按构造方法
-   不启用自动装配

#### 5.3.3 准备下案例环境

-   创建一个Maven项目
-   pom.xml添加依赖
-   resources下添加spring的配置文件

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/30cf4bc22e0c80dd14f0563004fab66c.png)

(1)项目中添加BookDao、BookDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {

    private String databaseName;
    private int connectionNum;

    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

(3)编写AppForAutoware运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForAutoware {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookService bookService = (BookService) ctx.getBean("bookService");
        bookService.save();
    }
}
```

#### 5.3.4 完成自动装配的配置

**自动装配只需要修改applicationContext.xml配置文件即可:**

(1)将dao的id删除，service的bean里`<property>`标签删除

(2)在service的`<bean>`标签中添加autowire属性，autowire就译为自动装配

（3）要确保自动装配的类里的有setter方法。

**按照类型注入的配置**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="com.itheima.dao.impl.BookDaoImpl"/>
    <!--autowire属性：开启自动装配，通常使用按类型装配-->
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl" autowire="byType"/>

</beans>
```

> **注意事项:**
> 
> -   需要注入属性的类中对应属性的**setter方法不能省略**
> -   被注入的对象必须要被Spring的IOC容器管理
> -   按类型注入必须保障**容器中相同类型的bean唯一，否则会报`NoUniqueBeanDefinitionException`**

**容器中相同类型的bean不唯一的情况：**

![](https://i-blog.csdnimg.cn/blog_migrate/ea44212de110832eea64230722e0b8fd.png)

**按照名称注入：** 

一个类型在IOC中有多个对象，还想要注入成功，这个时候就需要**按照名称注入**，配置方式为:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="com.itheima.dao.impl.BookDaoImpl"/>
    <!--autowire属性：开启自动装配，通常使用按类型装配-->
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl" autowire="byName"/>

</beans>
```

> **注意事项:**
> 
> -   **按照名称注入中的名称指的是什么?**
>     
>     ![](https://i-blog.csdnimg.cn/blog_migrate/17ea4d056feb69744b791e95f4db3060.png)
>     
>     -   bookDao是private修饰的，外部类无法直接方法
>     -   外部类只能通过属性的**set方法**进行访问
>     -   对外部类来说，setBookDao方法名，去掉set后首字母小写是其属性名
>         -   为什么是去掉set首字母小写?
>         -   这个规则是set方法生成的默认规则，set方法的生成是把属性名首字母大写前面加set形成的方法名
>     -   所以按**照名称注入，其实是和对应的set方法有关**，但是如果按照标准起名称，属性名和set对应的名是一致的
> -   如果按照名称去找对应的bean对象，找不到则注入Null
>     
> -   **当某一个类型在IOC容器中有多个对象，按照名称注入只找其指定名称对应的bean对象，不会报错**
>     

两种方式介绍完后，以后用的更多的是**按照类型**注入。

> 自动配置依赖注入的**特点:**
> 
> 1.  **自动装配**用于引用类型依赖注入，**不能对简单类型进行操作**
> 2.  使用**按类型装配**时（byType）必须保障**容器中相同类型的bean唯一**，推荐使用
> 3.  使用按名称装配时（byName）必须保障容器中具有指定名称的bean，因变量名与配置耦合，不推荐使用
> 4.  自动装配优先级低于setter注入与构造器注入，同时出现时自动装配配置失效

### 5.4 数组、集合注入

集合中既可以装简单数据类型也可以装引用数据类型。先来回顾下，常见的集合类型有哪些?

-   List
-   Set
-   Map
-   Properties

针对不同的集合类型，该如何实现注入呢?

#### 5.4.1 环境准备

-   创建一个Maven项目
-   pom.xml添加依赖
-   resources下添加spring的配置文件applicationContext.xml

这些步骤和**前面的都一致**，大家可以快速的拷贝即可，最终项目的结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/34a7fc64da966e6a05c419aa6e03f578.png)

(1)项目中添加添加BookDao、BookDaoImpl类

```java
public interface BookDao {
    public void save();
}


public class BookDaoImpl implements BookDao {

    private int[] array;

    private List<String> list;

    private Set<String> set;

    private Map<String,String> map;

    private Properties properties;

     public void save() {
        System.out.println("book dao save ...");

        System.out.println("遍历数组:" + Arrays.toString(array));

        System.out.println("遍历List" + list);

        System.out.println("遍历Set" + set);

        System.out.println("遍历Map" + map);

        System.out.println("遍历Properties" + properties);
    }
    //setter....方法省略，自己使用工具生成
}
```

(2)resources下提供spring的配置文件，applicationContext.xml

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
</beans>
```

(3)编写AppForDICollection运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForDICollection {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.save();
    }
}
```

接下来，在上面这个环境中来完成`集合注入`的学习:

下面的所以配置方式，都是在bookDao的bean标签中使用进行注入

```XML
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">

    </bean>
</beans>
```

#### 5.4.2 注入数组类型数据

```XML
<property name="array">
    <array>
        <value>100</value>
        <value>200</value>
        <value>300</value>
    </array>
</property>
```

#### 5.4.3 注入List类型数据

```XML
<property name="list">
    <list>
        <value>itcast</value>
        <value>itheima</value>
        <value>boxuegu</value>
        <value>chuanzhihui</value>
    </list>
</property>
```

#### 5.4.4 注入Set类型数据

```XML
<property name="set">
    <set>
        <value>itcast</value>
        <value>itheima</value>
        <value>boxuegu</value>
        <value>boxuegu</value>
    </set>
</property>
```

#### 5.4.5 注入Map类型数据

注意map最内标签不是value，是entry键值对。 

```XML
<property name="map">
    <map>
        <entry key="country" value="china"/>
        <entry key="province" value="henan"/>
        <entry key="city" value="kaifeng"/>
    </map>
</property>
```

#### 5.4.6 注入Properties类型数据

```XML
<property name="properties">
    <props>
        <prop key="country">china</prop>
        <prop key="province">henan</prop>
        <prop key="city">kaifeng</prop>
    </props>
</property>
```

配置完成后，运行下看结果:

![](https://i-blog.csdnimg.cn/blog_migrate/4a3003111eb1c9a51b596adab7ed4846.png)

> **说明：**
> 
> -   **property标签表示setter方式注入**，**构造方式注入**constructor-arg标签内部**也可以写**`<array>`、`<list>`、`<set>`、`<map>`、`<props>`标签
> -   List的底层也是通过数组实现的，所以`<list>`和`<array>`标签是可以混用
> -   集合中要添加引用类型，只需要把`<value>`标签改成`<ref>`标签，这种方式用的比较少