> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[一、Bean的生命周期](#Bean%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

[1.1 概念准备](#%E6%A6%82%E5%BF%B5%E5%87%86%E5%A4%87)

[1.2 简介](#%E7%AE%80%E4%BB%8B)

[1.3 环境准备](#%E4%BB%A3%E7%A0%81%E5%87%86%E5%A4%87)

[1.3.1 代码准备](#1.3.1%20%E4%BB%A3%E7%A0%81%E5%87%86%E5%A4%87)

[1.3.2 如何给Spring源码添加注释？](#1.3.2%20Spring%E6%BA%90%E7%A0%81%E6%B3%A8%E9%87%8A%E6%95%99%E5%AD%A6)

[方法一：IDEA插件Private Notes](#%E6%96%B9%E6%B3%95%E4%B8%80%EF%BC%9AIDEA%E6%8F%92%E4%BB%B6Private%20Notes)

[方法二（推荐）：覆盖类（基于双亲委派模型）](#%E6%96%B9%E6%B3%95%E4%BA%8C%EF%BC%88%E6%8E%A8%E8%8D%90%EF%BC%89%EF%BC%9A%E8%A6%86%E7%9B%96%E7%B1%BB%EF%BC%88%E5%9F%BA%E4%BA%8E%E5%8F%8C%E4%BA%B2%E5%A7%94%E6%B4%BE%E6%A8%A1%E5%9E%8B%EF%BC%89)

[1.4 应用上下文获取Bean的流程](#%E5%BA%94%E7%94%A8%E4%B8%8A%E4%B8%8B%E6%96%87%E8%8E%B7%E5%8F%96Bean%E7%9A%84%E6%B5%81%E7%A8%8B)

[1.4.1 AnnotationConfigApplicationContext类：启动IOC容器](#AnnotationConfigApplicationContext%E7%B1%BB%EF%BC%9A%E5%90%AF%E5%8A%A8IOC%E5%AE%B9%E5%99%A8)

[1.4.2 构造方法：注册配置类、启动IOC容器](#%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95%EF%BC%9A%E6%B3%A8%E5%86%8C%E9%85%8D%E7%BD%AE%E7%B1%BB%E3%80%81%E5%90%AF%E5%8A%A8IOC%E5%AE%B9%E5%99%A8)

[1.4.3 this.refresh()：创建并初始化BeanAbstractApplicationContext类： Bean的初始化和销毁](#this.refresh%28%29%EF%BC%9A%E5%88%9B%E5%BB%BA%E5%B9%B6%E5%88%9D%E5%A7%8B%E5%8C%96BeanAbstractApplicationContext%E7%B1%BB%EF%BC%9A%C2%A0Bean%E7%9A%84%E5%88%9D%E5%A7%8B%E5%8C%96%E5%92%8C%E9%94%80%E6%AF%81)

[1.4.3.1 概述](#%E6%A6%82%E8%BF%B0%C2%A0) 

[1.4.3.2 Bean的声明类：BeanDefinition](#Bean%E7%9A%84%E5%A3%B0%E6%98%8E%E7%B1%BB%EF%BC%9ABeanDefinition)

[1.4.3.3 AbstractBeanDefinition：定义BeanDefinition属性](#1.4%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B.%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B3.3%C2%A0AbstractBeanDefinition%EF%BC%9A%E5%AE%9A%E4%B9%89BeanDefinition%E5%B1%9E%E6%80%A7)

[1.4.3.4 后置处理器：PostProcessor](#%E5%90%8E%E7%BD%AE%E5%A4%84%E7%90%86%E5%99%A8%EF%BC%9APostProcessor)

[1.4.​​​​​​​5 finishBeanFactoryInitialization()：初始化所有单例bean](#finishBeanFactoryInitialization%28%29%EF%BC%9A%E5%88%9D%E5%A7%8B%E5%8C%96%E6%89%80%E6%9C%89%E5%8D%95%E4%BE%8Bbean)

[1.4​​​​​​​.​​​​​​​6 beanFactory.preInstantiateSingletons()：实例化所有非懒加载的单例 Bean](#beanFactory.preInstantiateSingletons%28%29%EF%BC%9A%E5%AE%9E%E4%BE%8B%E5%8C%96%E6%89%80%E6%9C%89%E9%9D%9E%E6%87%92%E5%8A%A0%E8%BD%BD%E7%9A%84%E5%8D%95%E4%BE%8B%20Bean)

[二、Bean的创建流程](#Bean%E7%9A%84%E5%88%9B%E5%BB%BA%E6%B5%81%E7%A8%8B%C2%A0) 

[2.1 核心流程和继承关系](#%E6%A0%B8%E5%BF%83%E6%B5%81%E7%A8%8B%E5%92%8C%E7%BB%A7%E6%89%BF%E5%85%B3%E7%B3%BB)

[2.2 getBean()：根据Bean名称获取Bean](#getBean%28%29%EF%BC%9A%E6%A0%B9%E6%8D%AEBean%E5%90%8D%E7%A7%B0%E8%8E%B7%E5%8F%96Bean)

[2.2.1 基本介绍](#2.2.1%20%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D)

[2.2.2  扩展](#2.2.2%C2%A0%20%E6%89%A9%E5%B1%95)

[2.2.2.1 AbstractBeanFactory类：抽象BeanFactory基类](#2.2.2.1%20AbstractBeanFactory%E7%B1%BB%EF%BC%9A%E6%8A%BD%E8%B1%A1BeanFactory%E5%9F%BA%E7%B1%BB)

[2.2.2.2 BeanFactory接口 ：IOC容器根接口，获取Bean的基础信息](#2.2.2.2%20BeanFactory%E6%8E%A5%E5%8F%A3%C2%A0%EF%BC%9AIOC%E5%AE%B9%E5%99%A8%E6%9C%80%E9%A1%B6%E7%BA%A7%E6%8E%A5%E5%8F%A3%EF%BC%8C%E8%8E%B7%E5%8F%96Bean%E7%9A%84%E5%9F%BA%E7%A1%80%E4%BF%A1%E6%81%AF)

[2.3 doGetBean()方法：getBean()的核心逻辑处理方法](#doGetBean%28%29%E6%96%B9%E6%B3%95%EF%BC%9AgetBean%28%29%E7%9A%84%E6%A0%B8%E5%BF%83%E9%80%BB%E8%BE%91%E5%A4%84%E7%90%86%E6%96%B9%E6%B3%95)

[2.4 getSingleton(beanName,objectFactory​​​​​​​)方法：三级缓存获取单例Bean](#getSingleton%28%29%E6%96%B9%E6%B3%95%EF%BC%9A%E4%B8%89%E7%BA%A7%E7%BC%93%E5%AD%98%E8%8E%B7%E5%8F%96%E5%8D%95%E4%BE%8BBean)

[2.4.1 基本介绍](#2.4.1%20%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D%C2%A0) 

[2.4.2 DefaultSingletonBeanRegistry类：注册和获取单例Bean](#2.4.2%C2%A0DefaultSingletonBeanRegistry%E7%B1%BB%EF%BC%9A%E6%B3%A8%E5%86%8C%E5%92%8C%E8%8E%B7%E5%8F%96%E5%8D%95%E4%BE%8BBean)

[2.5 createBean()方法：创建Bean](#createBean%28%29%E6%96%B9%E6%B3%95%EF%BC%9A%E5%88%9B%E5%BB%BABean)

[2.5.1 基本介绍](#2.5.1%20%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D)

[2.5.2 AbstractAutowireCapableBeanFactory类：初始化Bean和自动装配](#2.5.2%C2%A0AbstractAutowireCapableBeanFactory%E7%B1%BB%EF%BC%9A%E5%88%9D%E5%A7%8B%E5%8C%96Bean%E5%92%8C%E8%87%AA%E5%8A%A8%E8%A3%85%E9%85%8D)

[2.6 doCreateBean()方法：创建Bean的核心逻辑处理方法](#doCreateBean%28%29%E6%96%B9%E6%B3%95%EF%BC%9A%E5%88%9B%E5%BB%BABean%E7%9A%84%E6%A0%B8%E5%BF%83%E9%80%BB%E8%BE%91%E5%A4%84%E7%90%86%E6%96%B9%E6%B3%95)

[2.6.1 核心流程](#%E6%A0%B8%E5%BF%83%E6%B5%81%E7%A8%8B)

[2.6​​​​​​​.2 BeanWrapper及其与BeanDefinition的区别](#BeanWrapper%E5%92%8CBeanDefinition%E7%9A%84%E5%8C%BA%E5%88%AB)

[2.6​​​​​​​.3 详细流程](#%E8%AF%A6%E7%BB%86%E6%B5%81%E7%A8%8B)

[2.​​​7 createBeanInstance()：推断并实例化Bean](#createBeanInstance%28%29%EF%BC%9ABeanWrapper%E4%B8%BA%E7%A9%BA%E6%97%B6%E5%88%9B%E5%BB%BABean%E5%AE%9E%E4%BE%8B)

[2.​​​8 instantiateBean()：实例化和包装Bean](#instantiateBean%28%29%EF%BC%9A%E5%AE%9E%E4%BE%8B%E5%8C%96%E5%92%8C%E5%8C%85%E8%A3%85Bean)

[2.​​​9 instantiate()：根据构造方法实例化Bean](#instantiate%28%29%EF%BC%9A%E6%A0%B9%E6%8D%AE%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95%E5%AE%9E%E4%BE%8B%E5%8C%96Bean)

[2.​​​10 BeanUtils.instantiateClass()：基于反射实例化Bean](#BeanUtils.instantiateClass%28%29%EF%BC%9A%E5%9F%BA%E4%BA%8E%E5%8F%8D%E5%B0%84%E5%AE%9E%E4%BE%8B%E5%8C%96Bean)

[2.​​​11 initializeBean()： 初始化和调用前后置处理器](#initializeBean%28%29%EF%BC%9A%C2%A0%E5%88%9D%E5%A7%8B%E5%8C%96%E5%92%8C%E8%B0%83%E7%94%A8%E5%89%8D%E5%90%8E%E7%BD%AE%E5%A4%84%E7%90%86%E5%99%A8)

--

## 一、Bean的生命周期

### 1.1 概念准备

-   **IOC控制反转思想：**创建对象的控制权由内部（即new实例化）反转到外部（即IOC容器）。
-   **Bean：**IOC容器中存放的一个个对象
-   **DI依赖注入：**绑定IOC容器中bean与bean之间的依赖关系。例如将dao层对象注入到service层对象。

> IoC是控制反转的意思，是一种面向对象编程的设计思想。在不采用这种思想的情况下，我们需要自己维护对象与对象之间的依赖关系，很容易造成对象之间的耦合度过高，在一个大型的项目中这十分的不利于代码的维护。IoC则可以解决这种问题，它可以帮我们**维护对象与对象之间的依赖关系，并且降低对象之间的耦合度**。

### 1.2 简介

**Bean的生命周期：**指从Bean的创建到销毁的整个过程，主要包括Bean的创建、初始化、使用和销毁等阶段。

**生命周期核心流程：**

**1.扫描Bean：**Spring启动后，基于反射通过@ComponentScan、@Component等注解找到所有Bean，并给每个Bean创建**BeanDefinition对象**（存放Class对象、作用域等信息），放进**beanDefinitionMap**（映射关系是"Bean名"--->“对应的BeanDefinition”。）；

**2.遍历beanDefinitionMap：**遍历所有Bean进行Bean的创建，每个Bean的创建过程如下：

-   **推断构造方法、****实例化：**基于反射获取推断出的构造器对象，通过这个Constructor对象的newInstance(xx) 方法实例化类，得到原始对象；
-   **存入三级缓存：**基于原始对象生成Lambda表达式，并放入三**级缓存singletonFactories**。以后如果执行这个Lambda表达式，生成的将是代理对象。
-   **属性填充：**因为我们是从前到后遍历Bean的，所以存在当前Bean注入的属性Bean在加载时还没经历过声明周期得情况，那么这个属性Bean就要经历一次Bean的生命周期。具体的步骤如下：
    -   **单例池找：**先去一级缓存（单例池）找该Bean，若找到，则代表它已经历完整生命周期，没有发生循环依赖。一级缓存中存的是完整生命周期的Bean。
    -   **判断循环依赖：**若没找到，就代表它还未经过完整生命周期，要判断循环依赖。判断方法是在creattingSet<>中寻找该Bean，若找到则说明AService正在创建中，发生了循环依赖。
    -   **二级缓存找：**从二级缓存中找该Bean。二级缓存是earlySingletonObjects，存的就是未经历完整生命周期、提前aop的Bean。
    -   **三级缓存找到，生成提前代理对象、存二级缓存：**若没找到，就执行三级缓存该Bean的Lambda表达式，生成该Bean的提前代理对象，将其存入二级缓存并返回；
-   **处理Aware回调：**如果Bean实例实现了BeanNameAware接口（通过instanceof判断），调用Bean重写的setBeanName()方法，给Bean实例的beanName变量赋值。
-   **执行所有BeanPostProcessor的初始化前方法：**遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessBeforeInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
-   **初始化：**如果Bean实例实现了InitializingBean接口（通过instanceof判断），调用Bean重写的afterPropertiesSet()方法，处理初始化逻辑。afterPropertiesSet译为“在属性填充之后”
-   **执行所有BeanPostProcessor的初始化后方法：**遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessAfterInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
-   **存入单例池：**如果是单例，就将最终的代理对象存入单例池（**一级缓存**，singletonObjects）。
-   **生存期：**Bean已就绪，可以被使用，所有Bean将一直驻留在应用上下文中，直到应用上下文被销毁。
-   **销毁：**如果bean实现了DisposableBean接口，Spring将调用它的destory()接口方法，同样，如果有方法注解了@PreDestroy，该方法也会被调用。

### 1.3 环境准备

#### 1.3.1 代码准备

配置类： 

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/18
 * @Description: 配置类
 * @Version: 1.0
 */
@ComponentScan("com.vince.springboottest")
@Configuration
public class AppConfig {

}
```

测试Bean： 

```java
/**
 * @Author: vince
 * @CreateTime: 2024/04/01
 * @Description: 测试service
 * @Version: 1.0
 */
@Component
public class TestService {
    /**
     * TestService构造方法
     */
    public TestService() {
        System.out.println("TestService构造方法...");
    }

    /**
     * 测试方法
     */
    public void test() {
        System.out.println("TestService.test()...");
    }
}
```

#### 1.3.2 如何给Spring源码添加注释？

当我们进行debug时候，想要给Spring源码加注释，而源码都在项目引的依赖的jar包里，无法直接加注释，这就需要采取以下两种方法。

##### 方法一：IDEA插件Private Notes

> **Private Notes 官方介绍：**
> 
> 你还在为项目中不敢添加 "敏感注释"! 源码是只读文件不能添加注释而烦恼吗？ 
> 
> -   在任何你想加注释的地方 按下Alt + Enter鼠标移出点击即可保存
> -   已有私人注释 按下Alt + Enter即可快速编辑
> -   Alt + p 可快速添加或者编辑私人注释
> -   Alt + o 展示私人注释的其它操作
> -   右键菜单私人注释查看操作
> 
> **同步操作：**
> 
> -   数据都缓存当前用户目录下的 .privateNotes文件夹中,如需同步，可以借助强大的Git
> -   右键私人注释 可使用常用Git命令

**安装步骤：**

使用IDEA，搜索插件Private Notes并安装，然后重启即可生效：

![](https://i-blog.csdnimg.cn/blog_migrate/0d49dd3e52586140cc7a9f4d6f4588d0.png)  
 

**使用效果：**

打开任意源码，例如org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory，在任意行 “Alt + 回车”或者“Alt + P”，即可添加注释：

![](https://i-blog.csdnimg.cn/blog_migrate/cf36896de09e52936ea755bcda44e55a.png)

![](https://i-blog.csdnimg.cn/blog_migrate/3fba6c01638d95e26a63fccd273115a7.png)

关闭注释窗口，可以看到效果：

![](https://i-blog.csdnimg.cn/blog_migrate/eb7e9df459b6568ae4b301d89c3e7791.png)

##### 方法二（推荐）：覆盖类（基于双亲委派模型）

> **类加载机制和双亲委派模型：**
> 
> [Java的类是怎样在虚拟机中加载的？详细阐述JVM的加载、验证和解析过程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/135250030 "Java的类是怎样在虚拟机中加载的？详细阐述JVM的加载、验证和解析过程-CSDN博客")

双亲委派模型这里不再过多赘述，详情看上面文章。

基于双亲委派模型，我们可以在本地创建一个与原始类路径、全限定名完全一致的类，就可以实现对原类的覆盖，代码debug时，也会进入我们覆盖的类，而不是原类：

例如我们覆盖AbstractAutowireCapableBeanFactory类，代码内容也完全拷贝过来，仅修改doCreateBean()方法，加上断点，debug可以发现断点进了我们覆盖的类：

![](https://i-blog.csdnimg.cn/blog_migrate/f5a072ed8d1f0df33732916cdec55658.png)

![](https://i-blog.csdnimg.cn/blog_migrate/e62291e2c39a368483932eec2b1270c8.png)

### 1.4 应用上下文获取Bean的流程

#### 1.4.1 **AnnotationConfigApplicationContext类：启动IOC容器**

在Spring框架中，我们一般通过AnnotationConfigApplicationContext类、ClassPathXmlApplicationContext等类加载IOC容器，前者是通过注解的形式加载Spring容器，后者是通过配置文件的形式加载Spring容器。

本文章中使用注解方式加载Spring容器。

**启动IOC容器并获取Bean：**

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/20
 * @Description: 测试类：循环依赖
 * @Version: 1.0
 */
public class Test {
    public static void main(String[] args) {
        // 1.注解方式启动IOC容器，加载配置类
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        // 2.调用TestService的test()方法
        TestService testService = context.getBean(TestService.class, "testService");
        testService.test();
    }
}
```

#### 1.4.2 构造方法：注册配置类、启动IOC容器

 进入上面AnnotationConfigApplicationContext类，我们可以看到构造方法会执行this.refresh()，这个方法是实际启动Spring容器的方法。

**核心流程：**

1.  **调用无参构造函数；**
2.  **注册配置类：**将传入的配置类注册到应用程序上下文中。这些配置类通常使用了 @Configuration 注解，通过@ComponentScan或者@Bean定义了一些 Bean。
3.  **启动容器：**完成 Bean 的加载、注册和初始化等操作。

**详细流程：**

org.springframework.context.annotation.AnnotationConfigApplicationContext 

```java
    /**
     * 通过构造器实例化Bean
     * @param componentClasses 配置类
     */
    public AnnotationConfigApplicationContext(Class<?>... componentClasses) {
        // 1.调用 AnnotationConfigApplicationContext 的无参构造函数
        this();
        // 2.将传入的配置类注册到应用程序上下文中。
        // 这些配置类通常使用了 @Configuration 注解，通过@ComponentScan或者@Bean定义了一些 Bean。
        this.register(componentClasses);
        // 3.刷新应用程序上下文，启动容器，完成 Bean 的加载、注册和初始化等操作。
        this.refresh();
    }
```

> this.refresh()是IOC容器的核心方法，整个容器就是通过该方法，完成所有的 bean 的创建以及初始化。

#### 1.4.3 **this.refresh()：创建并初始化BeanAbstractApplicationContext类：** Bean的初始化和销毁

##### 1.4.3.1 概述 

ctrl+B追进去**this.refresh()**，我们可以看到AnnotationConfigApplicationContext的父类——**AbstractApplicationContext**的refresh()方法。

> **AbstractApplicationContext类：**
> 
> AbstractApplicationContext类是抽象应用程序上下文，是所有Spring应用上下文的基类。
> 
> 它定义了一些模板方法，用于子类实现具体的ApplicationContext（代表了Spring容器）的创建和销毁逻辑。

**核心流程：**

1.  beanFactory 的创建和初始化：创建并给 beanFactory 设置类加载器、PostProcessor等
2.  beanFactory 的后置处理
3.  初始化消息源、事件派发器、子容器中的 bean
4.  注册监听器
5.  **初始化所有单例bean**

**详细流程：**

org.springframework.context.support.AbstractApplicationContext 

```java
    public void refresh() throws BeansException, IllegalStateException {
        synchronized(this.startupShutdownMonitor) {
            StartupStep contextRefresh = this.applicationStartup.start("spring.context.refresh");
            // 1.beanFactory 的创建及预准备工作
            // 1.1 激活开启容器：设置容器为激活、未关闭状态、初始化属性、校验属性、声明事件集合earlyApplicationEvents
            this.prepareRefresh();
            // 1.2 获取 bean 工厂
            ConfigurableListableBeanFactory beanFactory = this.obtainFreshBeanFactory();
            // 1.3 对获取到的 beanFactory 做预处理设置：给 beanFactory 设置类加载器、添加属性编辑器、添加 beanPostProcessor、添加事件监听器、添加 beanFactoryPostProcessor
            this.prepareBeanFactory(beanFactory);

            try {
                // 2. beanFactory 的后置处理
                // 2.1 为 beanFactory 做一些后置的处理：默认是空方法，子类可以重写
                this.postProcessBeanFactory(beanFactory);
                StartupStep beanPostProcess = this.applicationStartup.start("spring.context.beans.post-process");
                // 2.2 执行 beanFactory 后置处理器的方法：获取所有BeanFactoryPostProcessor，排序并放进 beanFactory 中
                this.invokeBeanFactoryPostProcessors(beanFactory);
                // 2.3 注册 bean 的后置处理器：获取所有 BeanPostProcessor，排序并放进 beanFactory 中
                this.registerBeanPostProcessors(beanFactory);
                beanPostProcess.end();
                // 3. 初始化消息源、事件派发器、子容器中的 bean
                // 3.1 初始化 MessageSource 组件：MessageSource 组件用于国际化，可以根据消息代码和区域设置获取对应区域的消息文本，加载国际化资源文件
                this.initMessageSource();
                // 3.2 初始化事件派发器,多播器
                this.initApplicationEventMulticaster();
                // 3.3 初始化子容器中的bean：默认是空方法，子类可以重写
                this.onRefresh();
                // 4. 注册监听器
                // 注册监听器
                this.registerListeners();
                // 5. 初始化所有单例bean
                // 5.1 实例化所有非懒加载的单例bean：获取所有的bean，如果是单例且非懒加载的，就实例化
                // 此步骤真正开始了对象的实例化操作
                this.finishBeanFactoryInitialization(beanFactory);
                // 5.2 完成刷新过程：通知生命周期处理器lifecycleProcessor刷新过程
                this.finishRefresh();
            } catch (BeansException var10) {
                if (this.logger.isWarnEnabled()) {
                    this.logger.warn("Exception encountered during context initialization - cancelling refresh attempt: " + var10);
                }

                this.destroyBeans();
                this.cancelRefresh(var10);
                throw var10;
            } finally {
                this.resetCommonCaches();
                contextRefresh.end();
            }

        }
    }
```

##### 1.4.3.2 **Bean的声明类：BeanDefinition**

BeanDefinition 接口定义了 Bean 的配置元信息，提供了一些通用的Bean信息的setter和getter方法，用于实现类声明Bean属性，并重写这些setter和getter方法，从而设置和获取Bean的作用域、是否单例、初始化方法等信息：

-   **作用域相关方法**：
    -   setScope(String scope)：设置 Bean 的作用域。
    -   getScope()：获取 Bean 的作用域。
-   **懒加载相关方法**：
    -   setLazyInit(boolean lazyInit)：设置 Bean 是否懒加载。
    -   isLazyInit()：判断 Bean 是否懒加载。
-   **依赖关系相关方法**：
    -   setDependsOn(String... dependsOn)：设置 Bean 的依赖关系。
    -   getDependsOn()：获取 Bean 的依赖关系。
-   **自动装配相关方法**：
    -   setAutowireCandidate(boolean autowireCandidate)：设置 Bean 是否是自动装配的候选者。
    -   isAutowireCandidate()：判断 Bean 是否是自动装配的候选者。
-   **Factory 相关方法**：
    -   setFactoryBeanName(String factoryBeanName)：设置 Bean 的工厂 Bean 名称。
    -   getFactoryBeanName()：获取 Bean 的工厂 Bean 名称。
    -   setFactoryMethodName(String factoryMethodName)：设置 Bean 的工厂方法名称。
    -   getFactoryMethodName()：获取 Bean 的工厂方法名称。
-   **构造函数和属性值相关方法**：
    -   getConstructorArgumentValues()：获取 Bean 的构造函数参数值。
    -   getPropertyValues()：获取 Bean 的属性值。
-   **初始化和销毁方法相关方法**：
    -   setInitMethodName(String initMethodName)：设置 Bean 的初始化方法名称。
    -   getInitMethodName()：获取 Bean 的初始化方法名称。
    -   setDestroyMethodName(String destroyMethodName)：设置 Bean 的销毁方法名称。
    -   getDestroyMethodName()：获取 Bean 的销毁方法名称。
-   **其他属性相关方法**：
    -   setRole(int role)：设置 Bean 的角色。
    -   getRole()：获取 Bean 的角色。
    -   setDescription(String description)：设置 Bean 的描述信息。
    -   getDescription()：获取 Bean 的描述信息。
-   **只读属性相关方法**：
    -   isSingleton()：判断 Bean 是否是单例。
    -   isPrototype()：判断 Bean 是否是原型。
    -   isAbstract()：判断 Bean 是否是抽象。
    -   getResourceDescription()：获取 Bean 的资源描述信息。
    -   getOriginatingBeanDefinition()：获取 Bean 的原始 Bean 定义。

![](https://i-blog.csdnimg.cn/blog_migrate/711950a932689865d32d6407880ec1c0.png)

##### 1.4​​​​​​​.​​​​​​​3.3 AbstractBeanDefinition：定义BeanDefinition属性

AbstractBeanDefinition 是 BeanDefinition 接口的抽象实现类，提供了一些通用的属性和方法，用于描述 Spring Bean 的定义。它为其他具体的 BeanDefinition 实现类（如 RootBeanDefinition）提供了基础功能和结构。

AbstractBeanDefinition 实现了BeanDefinition的getter和setter方法，并声明了这些属性，同时新增了一些方法，例如getBeanClass()获取Bean的Class对象：

**属性：**

-   **beanClass**: 保存 Bean 的类对象。
-   **scope**: Bean 的作用域，如 singleton、prototype 等。
-   **lazyInit**: 指示 Bean 是否懒加载。
-   **dependsOn**: 保存 Bean 依赖的其他 Bean 的名称。
-   **autowireCandidate**: 指示 Bean 是否作为自动装配的候选者。
-   **primary**: 指示 Bean 是否为自动装配的首选项。
-   **factoryBeanName**: 工厂 Bean 的名称。
-   **factoryMethodName**: 工厂方法的名称。
-   **constructorArgumentValues**: 构造函数参数值列表。
-   **propertyValues**: 属性值列表。
-   **initMethodName**: 初始化方法的名称。
-   **destroyMethodName**: 销毁方法的名称。
-   **role**: Bean 的角色，可以是 APPLICATION、SUPPORT 或 INFRASTRUCTURE。
-   **resourceDescription**: Bean 定义的资源描述。
-   **description**: Bean 的描述信息。
-   **abstractFlag**: 指示是否是抽象 Bean。
-   **synthetic**: 指示是否是合成的 Bean。
-   **lazyInitResolved**: 懒加载是否已经解析。
-   **synthetic**: 指示是否是合成的 Bean。

**方法：**

org.springframework.beans.factory.support.AbstractBeanDefinition 

```java
    /**
     * 获取Bean的Class对象
     * @return {@link Class}<{@link ?}>
     * @throws IllegalStateException
     */
    public Class<?> getBeanClass() throws IllegalStateException {
        Object beanClassObject = this.beanClass;
        if (beanClassObject == null) {
            throw new IllegalStateException("No bean class specified on bean definition");
        }
        if (!(beanClassObject instanceof Class)) {
            throw new IllegalStateException(
                    "Bean class name [" + beanClassObject + "] has not been resolved into an actual Class");
        }
        return (Class<?>) beanClassObject;
    }

    /**
     * 获取Bean的作用域
     * @return {@link String}
     */
    @Override
    @Nullable
    public String getScope() {
        return this.scope;
    }
...
```

##### 1.4​​​​​​​.​​​​​​​3.4 后置处理器：PostProcessor

**PostProcessor：**一种特殊的bean，它可以拦截bean的创建过程，以提供一些额外的处理。PostProcessor的主要作用是在Spring容器初始化bean时，允许我们介入bean的创建过程，以实现一些自定义的逻辑。

**作用：**

-   **修改bean的定义：**通过实现BeanFactoryPostProcessor接口，我们可以在Spring容器加载bean定义之后，但在实例化bean之前，对bean定义进行修改。例如，我们可以修改bean的作用域，或者添加新的属性值。
-   **修改bean的实例：**通过实现BeanPostProcessor接口，我们可以在Spring容器实例化bean之后，但在返回bean之前，对bean进行额外的处理。例如，我们可以修改bean的属性，或者返回一个完全不同的bean实例。
-   **处理特定类型的bean：**通过实现BeanPostProcessor的子接口，例如InstantiationAwareBeanPostProcessor或DestructionAwareBeanPostProcessor，我们可以在bean实例化之前、之后或销毁之前，对特定类型的bean进行更详细的处理。
-   **处理占位符：**通过使用PropertyPlaceholderConfigurer或PropertySourcesPlaceholderConfigurer，我们可以在bean定义中使用占位符，并在实例化bean时，用实际的值替换这些占位符。

**常见PostProcessor：**

**BeanPostProcessor接口：**

-   **作用：**Bean实例化前后初始化Bean。
-   **使用方法：**实现该接口并重写postProcessBeforeInitialization()、postProcessAfterInitialization()方法。
-   **应用场景：**自定义的初始化逻辑、检查 Bean 的合法性等。

org.springframework.beans.factory.config.BeanPostProcessor  

```java
public interface BeanPostProcessor {

	@Nullable
	default Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}

	@Nullable
	default Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}

}
```

**BeanFactoryPostProcessor接口：**

-   **作用：**修改BeanDefinition元数据、修改Bean属性。
-   **使用方法：**实现该接口并重写postProcessBeanFactory()方法。
-   **应用场景：**修改属性值、添加额外的属性等。

org.springframework.beans.factory.config.BeanFactoryPostProcessor 

```java
@Component
public class MyBeanFactoryPostProcessor implements BeanFactoryPostProcessor {
	@Override
	public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {
		BeanDefinition bd = beanFactory.getBeanDefinition("userService");
		bd.getPropertyValues().addPropertyValue("name","keaizp");
	}
}
```

**InstantiationAwareBeanPostProcessor：**

-   **作用：**Bean实例化前后、Bean设置属性前后初始化Bean。
-   **使用方法：**继承了上面BeanPostProcessor，多了postProcessPropertyValues()方法，在Bean的属性注入之前调用。
-   **应用场景：**自定义的初始化逻辑、检查 Bean 的合法性、修改Bean的属性值或进行其他自定义操作

org.springframework.beans.factory.config.InstantiationAwareBeanPostProcessor 

```java
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {

	@Nullable
	default Object postProcessBeforeInstantiation(Class<?> beanClass, String beanName) throws BeansException {
		return null;
	}

	default boolean postProcessAfterInstantiation(Object bean, String beanName) throws BeansException {
		return true;
	}

	@Nullable
	default PropertyValues postProcessProperties(PropertyValues pvs, Object bean, String beanName)
			throws BeansException {

		return null;
	}

	@Deprecated
	@Nullable
	default PropertyValues postProcessPropertyValues(
			PropertyValues pvs, PropertyDescriptor[] pds, Object bean, String beanName) throws BeansException {

		return pvs;
	}

}
```

**DestructionAwareBeanPostProcessor：**

-   **作用：**在 Bean 销毁之前进行自定义操作。
-   **使用方法：**实现该接口并重写postProcessBeforeDestruction()方法。
-   **应用场景：**适用于需要在 Bean 销毁前执行清理逻辑、资源释放等操作。

org.springframework.beans.factory.config.DestructionAwareBeanPostProcessor 

```java
public interface DestructionAwareBeanPostProcessor extends BeanPostProcessor {

	void postProcessBeforeDestruction(Object bean, String beanName) throws BeansException;

	default boolean requiresDestruction(Object bean) {
		return true;
	}

}
```

**MergedBeanDefinitionPostProcessor：**

-   **作用：**在 BeanDefinition 合并之后、Bean 创建之前执行自定义逻辑。（合并BeanDefinition 详见doCreateBean()方法）
-   **使用方法：**实现该接口并重写postProcessMergedBeanDefinition()方法。
-   **应用场景：**修改合并后的属性值、添加额外的属性等。

org.springframework.beans.factory.config.MergedBeanDefinitionPostProcessor

```java
public interface MergedBeanDefinitionPostProcessor extends BeanPostProcessor {

	void postProcessMergedBeanDefinition(RootBeanDefinition beanDefinition, Class<?> beanType, String beanName);

	default void resetBeanDefinition(String beanName) {
	}

}
```

#### 1.4​​​​​​​.​​​​​​​5 finishBeanFactoryInitialization()：**初始化所有单例bean**

在上面refresh()的所有核心流程中，finishBeanFactoryInitialization()是最核心的流程，用于初始化所有单例bean，我们追进去，可以看到它其中有个getBean()方法：

org.springframework.context.support.AbstractApplicationContext  

```java
    /**
     * Finish the initialization of this context's bean factory,
     * 完成此上下文的bean工厂的初始化，
     * initializing all remaining singleton beans.
     * 初始化所有剩余的单例bean。
     */
    protected void finishBeanFactoryInitialization(ConfigurableListableBeanFactory beanFactory) {
        // 初始化名为ConversionService（转换服务）的Bean
        if (beanFactory.containsBean("conversionService") && beanFactory.isTypeMatch("conversionService", ConversionService.class)) {
            beanFactory.setConversionService((ConversionService)beanFactory.getBean("conversionService", ConversionService.class));
        }

        // 添加嵌入值解析器（EmbeddedValueResolver）到 BeanFactory 中，用于解析 ${...} 占位符的值，例如@Value("${db.driverClassName:com.mysql.jdbc.Driver}")
        if (!beanFactory.hasEmbeddedValueResolver()) {
            beanFactory.addEmbeddedValueResolver((strVal) -> {
                return this.getEnvironment().resolvePlaceholders(strVal);
            });
        }

        // 处理所有实现了 LoadTimeWeaverAware 接口的 Bean
        String[] weaverAwareNames = beanFactory.getBeanNamesForType(LoadTimeWeaverAware.class, false, false);
        for (String weaverAwareName : weaverAwareNames) {
            // 触发实例化每个 LoadTimeWeaverAware Bean，以确保其中的逻辑得以执行
            this.getBean(weaverAwareName);
        }

        // 禁用临时类加载器
        beanFactory.setTempClassLoader((ClassLoader)null);

        // 冻结配置，禁止再对已注册的beanDefinition做修改，因为接下来要开始创建bean了
        beanFactory.freezeConfiguration();

        // 实例化所有非懒加载的单例 Bean
        beanFactory.preInstantiateSingletons();
    }
```

#### 1.4​​​​​​​.​​​​​​​6 beanFactory.preInstantiateSingletons()：实例化所有非懒加载的单例 Bean

finishBeanFactoryInitialization()方法中，最核心的语句是最后一行，即beanFactory.preInstantiateSingletons()，用于实例化所有非懒加载的单例 Bean。

> **DefaultListableBeanFactory类：**这里beanFactory是DefaultListableBeanFactory类的对象，是Spring的默认BeanFactory。它实现了BeanDefinitionRegistry接口，可通过读取配置文件等方式，预先注册所有beanDefinition。

**核心流程：**

1.  获取所有已注册的beanDefinition名字，即获取Bean名称列表；
2.  遍历Bean名称列表：
    1.  如果该Bean是FactoryBean，则
        1.  获取 FactoryBean 实例；
        2.  判断实例是否实现了SmartFactoryBean 接口；
            1.  如果实现了，则调用isEagerInit()方法判断它是否是饥饿初始化，如果是则立刻调用**getBean()**初始化，否则等待容器启动完成后再初始化
            2.  如果没实现，直接**getBean()**
    2.  否则是普通Bean，直接调用**getBean()方法**获取Bean 

> **BeanFactory和FactoryBean的区别：**
> 
> -   **BeanFactory：**就是IOC容器，它有一些方法可以判断容器里Bean是否存在、是否单例等。
> -   **FactoryBean：**是接口，用来注册Bean。重写getObject()方法，返回的对象注册为Bean。

**详细流程：**

org.springframework.beans.factory.support.DefaultListableBeanFactory 

```java
    /**
     * 实例化所有非懒加载的单例 Bean
     * @throws BeansException Beans异常
     */
    @Override
    public void preInstantiateSingletons() throws BeansException {
        if (logger.isTraceEnabled()) {
            logger.trace("Pre-instantiating singletons in " + this);
        }

        // 获取所有已注册的beanDefinition名字
        List<String> beanNames = new ArrayList<>(this.beanDefinitionNames);

        // 循环每个beanDefinition名字，做初始化操作
        for (String beanName : beanNames) {
            // 合并父类的配置
            RootBeanDefinition bd = getMergedLocalBeanDefinition(beanName);
            // 非抽象、非懒加载的单例是需要初始化的，其他情况不需要初始化
            if (!bd.isAbstract() && bd.isSingleton() && !bd.isLazyInit()) {
                //如果是FactoryBean
                if (isFactoryBean(beanName)) {
                    //是FactoryBean的话直接在beanName之前加&获取到bean
                    Object bean = getBean(FACTORY_BEAN_PREFIX + beanName);
                    //保险起见，再判断一次
                    if (bean instanceof FactoryBean) {
                        //强转为FactoryBean
                        final FactoryBean<?> factory = (FactoryBean<?>) bean;
                        boolean isEagerInit;
                        //如果是SmartFactoryBean的实例，下面的判断确定isEagerInit标志符
                        if (System.getSecurityManager() != null && factory instanceof SmartFactoryBean) {
                            isEagerInit = AccessController.doPrivileged((PrivilegedAction<Boolean>)
                                            ((SmartFactoryBean<?>) factory)::isEagerInit,
                                    getAccessControlContext());
                        }
                        else {
                            isEagerInit = (factory instanceof SmartFactoryBean &&
                                    ((SmartFactoryBean<?>) factory).isEagerInit());
                        }
                        //如果需要立刻初始化，就调用getBean方法
                        if (isEagerInit) {
                            getBean(beanName);
                        }
                    }
                }
                else {
                    //如果是普通bean，直接调用getBean方法就可以了
                    getBean(beanName);
                }
            }
        }
        //截止到这里beanDefinition就变成了bean并注册了。

        //如果我们定义的bean实现SmartInitializingSingleton接口,
        //就执行afterSingletonsInstantiated方法
        for (String beanName : beanNames) {
            Object singletonInstance = getSingleton(beanName);
            if (singletonInstance instanceof SmartInitializingSingleton) {
                final SmartInitializingSingleton smartSingleton = (SmartInitializingSingleton) singletonInstance;
                if (System.getSecurityManager() != null) {
                    AccessController.doPrivileged((PrivilegedAction<Object>) () -> {
                        smartSingleton.afterSingletonsInstantiated();
                        return null;
                    }, getAccessControlContext());
                }
                else {
                    smartSingleton.afterSingletonsInstantiated();
                }
            }
        }
    }
```

## 二、Bean的创建流程 

### 2.1 核心流程和继承关系

**核心流程：** 

![](https://i-blog.csdnimg.cn/blog_migrate/e0e496c60d4a95ff1678e2ae88a8512b.png)

**继承关系：**

![](https://i-blog.csdnimg.cn/blog_migrate/e00cd2d67ebe68c35750d5c7fd7c266a.png)

### 2.2 getBean()：根据Bean名称获取Bean

#### 2.2.1 基本介绍

在上面beanFactory.preInstantiateSingletons()中，有多次用到getBean()方法，该方法用于获取Bean，在**AbstractBeanFactory类**下，它调用了doGetBean()方法。

org.springframework.beans.factory.support.AbstractBeanFactory

```java
	@Override
	public Object getBean(String name) throws BeansException {
		return doGetBean(name, null, null, false);
	}
```

#### 2.2.2  扩展

##### 2.2.2.1 AbstractBeanFactory类：抽象BeanFactory基类

**AbstractBeanFactory类：**

-   **介绍：**抽象BeanFactory的基类，它实现了BeanFactory接口（ConfigurableBeanFactory--->ConfigurableBeanFactory—>HierarchicalBeanFactory—>BeanFactory）。
-   **功能：**用于管理 BeanDefinition，并对Bean 进行创建、获取、销毁等操作。

```java
    /**
     * @Author: vince
     * @CreateTime: 2024/04/26
     * @Description: 抽象BeanFactory基类：用于管理 BeanDefinition，并支持 Bean 的创建、获取、销毁等操作。
     * @Version: 1.0
     */
public abstract class AbstractBeanFactory extends FactoryBeanRegistrySupport implements ConfigurableBeanFactory {
    ..
}
```

**核心方法：**

-   **BeanDefinition 注册和获取：**
    
    -   **getBeanDefinition(String beanName)**: 根据名称获取对应的 BeanDefinition。
    -   **containsBeanDefinition(String beanName)**: 判断是否包含指定名称的 BeanDefinition。
-   **Bean 创建和获取：**
    
    -   **getBean(String name)**: 根据名称获取 Bean 实例。
    -   **getBean(Class requiredType)**: 根据类型获取 Bean 实例。
    -   **createBean(Class<?> beanClass)**: 根据 Class 创建一个新的 Bean 实例。
-   **Bean 生命周期管理：**
    
    -   **addBeanPostProcessor(BeanPostProcessor beanPostProcessor)**: 注册一个 BeanPostProcessor。
    -   **destroyBean(String beanName, Object beanInstance)**: 销毁指定的 Bean 实例。
-   **Bean 作用域管理：**
    
    -   **getBean(String name, Object... args)**: 根据名称和参数获取 Bean 实例，支持原型作用域的 Bean。
    -   **isPrototype(String name)**: 判断指定名称的 Bean 是否为原型作用域。
-   **扩展点注册：**
    
    -   **addBeanPostProcessor(BeanPostProcessor beanPostProcessor)**: 注册 BeanPostProcessor，用于在 Bean 创建、初始化等过程中进行扩展操作。
-   **其他常用方法：**
    
    -   **containsBean(String name)**: 判断容器中是否包含指定名称的 Bean。
    -   **isTypeMatch(String name, ResolvableType typeToMatch)**: 判断指定名称的 Bean 是否与指定的类型匹配。
    -   **getType(String name)**: 获取指定名称的 Bean 的类型。
    -   **getAliases(String name)**: 获取指定名称的 Bean 的别名。

##### 2.2.2.2 **BeanFactory接口** ：IOC容器根接口，获取Bean的基础信息

**BeanFactory：**生产bean实例化对象的工厂接口，它的各种实现类，其实就是各种不同类型的容器，这些容器统称为IoC容器。

BeanFactory接口是IOC容器最顶级的接口，是所有IOC容器的根接口。所有管理、操作Bean的类最终都实现了这个接口，例如ApplicationContext接口（继承HierarchicalBeanFactory接口，它再继承BeanFactory接口）。

**具体功能：**

-   **获取 Bean：**
    
    -   **getBean(String name)**: 根据 Bean 的名称获取 Bean 实例。
    -   **getBean(String name, Class requiredType)**: 根据 Bean 的名称和类型获取 Bean 实例。
    -   **getBean(String name, Object... args)**: 根据 Bean 的名称和参数获取 Bean 实例。
    -   **getBean(Class requiredType)**: 根据 Bean 的类型获取 Bean 实例。
    -   **getBean(Class requiredType, Object... args)**: 根据 Bean 的类型和参数获取 Bean 实例。
    -   **getBeanProvider(Class requiredType)**: 获取指定 Bean 的提供者，支持延迟加载和唯一性选项。
    -   **getBeanProvider(ResolvableType requiredType)**: 获取指定 Bean 的提供者，支持延迟加载和唯一性选项。
-   **判断 Bean 是否存在：**
    
    -   **containsBean(String name)**: 判断是否存在指定名称的 Bean。
-   **获取 Bean 的类型、别名、是否单例信息：**
    
    -   **isSingleton(String name)**: 判断指定名称的 Bean 是否为单例。
    -   **isPrototype(String name)**: 判断指定名称的 Bean 是否为原型。
    -   **isTypeMatch(String name, ResolvableType typeToMatch)**: 判断指定名称的 Bean 是否与给定类型匹配。
    -   **isTypeMatch(String name, Class<?> typeToMatch)**: 判断指定名称的 Bean 是否与给定类型匹配。
    -   **getType(String name)**: 获取指定名称的 Bean 的类型。
    -   **getType(String name, boolean allowFactoryBeanInit)**: 获取指定名称的 Bean 的类型，允许 FactoryBean 初始化。
    -   **getAliases(String name)**: 获取指定名称的 Bean 的别名数组。

![](https://i-blog.csdnimg.cn/blog_migrate/bc9faf06558d31fd6f3bf13baafd6fc8.png)

> **BeanFactory和FactoryBean区别：**
> 
> -   **BeanFactory接口：**是一切IOC容器的根接口。它有一些方法可以判断容器里Bean是否存在、是否单例等
> -   **FactoryBean接口：**用于自定义注册Bean的逻辑的工厂接口。主要用于自定义注册Bean的逻辑，并且将其集成到 Spring 的 IoC 容器中。实现这个接口并重写getObject()方法，可以将返回的对象注册为Bean。**核心方法：**
>     -   **getObject()**: 返回由此工厂创建的对象实例，Spring 将使用这个方法返回的实例注册到容器中。
>     -   **getObjectType()**: 返回此工厂创建的对象的类型，这样 Spring 容器就可以在需要时自动识别出实际的类型。
>     -   **isSingleton()**: 返回由此工厂创建的对象是否是单例的。如果是单例的，Spring 容器将会缓存对象实例；否则，每次请求都会创建一个新的实例。

### 2.3 doGetBean()方法：getBean()的核心逻辑处理方法

上面getBean()只有一行代码，调用了doGetBean()一个方法。

> **do前缀的方法：**
> 
> 在Spring源码里边，有很多以do开头的方法，当你看到这些以do开头的方法时，应该意识到，在这个方法里边，往往才是真正的逻辑处理过程，即真正“干活”的方法。 

**作用：**根据给定的 Bean 名称、类型和参数获取 Bean 实例。

**参数：** 

-   **name (String)：**要获取的 Bean 的名称。  
    这个名称可能是原始的 Bean 名称，也可能是别名，或者是带有 & 前缀的 FactoryBean 名称。
-   **requiredType (Class<T>)：**指定要返回的 Bean 的类型。  
    如果不指定类型或者类型为 null，则返回任何类型的 Bean。
-   **args (Object\[\])：**构造方法参数数组。  
    如果 Bean 有构造方法，这些参数将传递给构造函数进行实例化。如果 Bean 没有构造函数或者不需要参数，这个参数可以为 null。
-   **typeCheckOnly (boolean)：**是否只检查类型。  
    表示是否只进行类型检查而不实际获取 Bean 实例。如果为 true，则只会检查 Bean 是否符合指定的类型，不会真正实例化 Bean。

**流程概述：** 

1.  提取beanName；
2.  **尝试从缓存获取Bean：**调用**getSingleton(String beanName)**，如果当前Bean已经被加载过获取因为循环依赖正咋被加载，这里将直接获取到Bean实例；
3.  循环依赖的判断。
4.  递归去父容器获取Bean实例。
5.  从当前容器获取BeanDefinition实例。
6.  递归实例化显式依赖的Bean。
7.  **根据不同的Scope采用不同的策略创建Bean实例：**调用**getSingleton(String beanName, ObjectFactory<?> singletonFactory)**，传参Lambda表达式中有createBean()去创建Bean。
8.  对Bean进行类型检查。 

**流程详解：**

org.springframework.beans.factory.support.AbstractBeanFactory 

```java
    protected <T> T doGetBean(
            String name, @Nullable Class<T> requiredType, @Nullable Object[] args, boolean typeCheckOnly)
            throws BeansException {

        // 1. 提取出对应的beanName。
        // 将参数name(1.FactoryBean要去掉前缀&，2.别名A指向B的Bean要转成B)转换成容器中真实的bean名称(获取容器中真实beanName)
        String beanName = transformedBeanName(name);
        Object bean;

        // 2.尝试直接从三级缓存中获取Bean 
        // 尝试从一级缓存中获取之前被实例化过了的单例bean或从三级缓存中获取ObjectFactory，执行Lambda表达式创建单例Bean。
        // 如果当前Bean已经被加载过，或者因为循环依赖处在加载中，就可以直接从这个getSingleton(beanName)中获取到Bean，
        // 否则就要执行后面第8步的getSingleton(beanName,包含createBean的Lambda)
        Object sharedInstance = getSingleton(beanName);
        // 如果之前已经创建过该单例bean,并且args为空(单例 bean不可以用这个args,它是为多例设计的)
        if (sharedInstance != null && args == null) {
            if (logger.isDebugEnabled()) {
                // 如果Bean还在创建中，则说明是循环依赖.
                if (isSingletonCurrentlyInCreation(beanName)) {
                    logger.debug("Returning eagerly cached instance of singleton bean '" + beanName +
                            "' that is not fully initialized yet - a consequence of a circular reference");
                }
                else {
                    logger.debug("Returning cached instance of singleton bean '" + beanName + "'");
                }
            }
            // 3. 检测处理FactoryBean类型的bean并返回实例。
            // 如果是普通的bean，直接返回,如果是factoryBean,则返回它的getObject. 这一步主要还是针对FactoryBean的处理。
            bean = getObjectForBeanInstance(sharedInstance, name, beanName, null);
        }
        // 如果scope->prototype,singleton.但是在缓存中无法找到
        else {
            // Fail if we're already creating this bean instance:
            // We're assumably within a circular reference.
            // 4. 先根据缓存判断一下当前的bean是否正在被创建，如果是的话表示依赖循环了;只有单例情况才会尝试解决循环依赖，原型模式直接抛出异常。因为原型模式无法解决循环依赖问题。
            if (isPrototypeCurrentlyInCreation(beanName)) {
                throw new BeanCurrentlyInCreationException(beanName);
            }

            // Check if bean definition exists in this factory.
            // 5. 获取父级的BeanFactory
            BeanFactory parentBeanFactory = getParentBeanFactory();
            // 如果在当前容器中无法找到指定名称的bean，此时递归去parentFactory查找.
            if (parentBeanFactory != null && !containsBeanDefinition(beanName)) {
                // Not found -> check parent.
                // 递归到BeanFactory中检测,针对FactoryBean,将Bean的&重新拼上
                String nameToLookup = originalBeanName(name);
                // 如果parentBeanFactory属于AbstractBeanFactory实例
                if (parentBeanFactory instanceof AbstractBeanFactory) {
                    // 递归查找
                    return ((AbstractBeanFactory) parentBeanFactory).doGetBean(
                            nameToLookup, requiredType, args, typeCheckOnly);
                }
                else if (args != null) {
                    // Delegation to parent with explicit args.
                    // 如果有参数,则委派父级容器根据指定名称和显式的参数查找.
                    return (T) parentBeanFactory.getBean(nameToLookup, args);
                }
                else {
                    // No args -> delegate to standard getBean method.
                    // 如果没有参数，委托父级容器根据指定名称和type进行查找
                    return parentBeanFactory.getBean(nameToLookup, requiredType);
                }
            }
            // 如果当前要获取的bean只是为了进行类型检查就标记bean已经被创建
            if (!typeCheckOnly) {
                // 这里是将 当前创建的beanName 保存到 alreadyCreated 集合中。alreadyCreated 中的bean表示当前bean已经创建了，在进行循环依赖判断的时候会使用
                markBeanAsCreated(beanName);
            }

            try {
                // 6. 将当前 beanName 的 BeanDefinition 和父类BeanDefinition 属性进行一个整合
                RootBeanDefinition mbd = getMergedLocalBeanDefinition(beanName);
                // 对合并的BeanDefiniton进行检测，主要判断是否为abstract.
                checkMergedBeanDefinition(mbd, beanName, args);

                // Guarantee initialization of beans that the current bean depends on.
                // 7. 寻找bean的依赖
                // 获取当前Bean所有依赖的Bean名称
                String[] dependsOn = mbd.getDependsOn();
                // 如果需要依赖，则递归实例化依赖bean
                if (dependsOn != null) {
                    for (String dep : dependsOn) {
                        // 判断是否有循环依赖的情况 ： A依赖B，B依赖A
                        if (isDependent(beanName, dep)) {
                            throw new BeanCreationException(mbd.getResourceDescription(), beanName,
                                    "Circular depends-on relationship between '" + beanName + "' and '" + dep + "'");
                        }
                        // 注册依赖信息，将依赖信息保存到 dependentBeanMap、dependenciesForBeanMap中
                        registerDependentBean(dep, beanName);
                        try {
                            // 获取依赖的bean，这一步又回到了最初的getBean
                            getBean(dep);
                        }
                        catch (NoSuchBeanDefinitionException ex) {
                            throw new BeanCreationException(mbd.getResourceDescription(), beanName,
                                    "'" + beanName + "' depends on missing bean '" + dep + "'", ex);
                        }
                    }
                }

                // Create bean instance.
                // 8 针对不同的Scope 进行bean的创建
                // 实例化依赖的bean便可以实例化mdb本身了
                // 如果BeanDefiniton为单例
                if (mbd.isSingleton()) {
                    // 匿名内部类，创建Bean实例对象,并且注册给所依赖的对象
                    // 关键方法:单例类实例化的入口
                    sharedInstance = getSingleton(beanName, () -> {
                        try {
                            // 创建单例bean的入口.
                            // =============关键===============
                            return createBean(beanName, mbd, args);
                        }
                        catch (BeansException ex) {
                            // Explicitly remove instance from singleton cache: It might have been put there
                            // eagerly by the creation process, to allow for circular reference resolution.
                            // Also remove any beans that received a temporary reference to the bean.
                            // 显性从单例缓存中删除bean实例.
                            // 因为单例模式下为了解决循环依赖，可能留有残余的信息，此处进行销毁
                            destroySingleton(beanName);
                            throw ex;
                        }
                    });
                    // 解决FactoryBean的问题
                    bean = getObjectForBeanInstance(sharedInstance, name, beanName, mbd);
                }

                else if (mbd.isPrototype()) {
                    // It's a prototype -> create a new instance.
                    // 原型模式的回调
                    // 如果是原型模式，创建一个实例,在原型模式下，每次getBean都会产生一个新的实例
                    Object prototypeInstance = null;
                    try {
                        // 保存当前线程正在创建的beanName 到 prototypesCurrentlyInCreation 中
                        beforePrototypeCreation(beanName);
                        // 直接创建bean
                        prototypeInstance = createBean(beanName, mbd, args);
                    }
                    finally {
                        // 完成创建后，从 prototypesCurrentlyInCreation 中移除当前线程正在创建的beanName
                        afterPrototypeCreation(beanName);
                    }
                    // 解决FactoryBean的问题
                    bean = getObjectForBeanInstance(prototypeInstance, name, beanName, mbd);
                }

                else {
                    // 指定scope上实例化bean
                    String scopeName = mbd.getScope();
                    if (!StringUtils.hasLength(scopeName)) {
                        throw new IllegalStateException("No scope name defined for bean ´" + beanName + "'");
                    }
                    Scope scope = this.scopes.get(scopeName);
                    if (scope == null) {
                        throw new IllegalStateException("No Scope registered for scope name '" + scopeName + "'");
                    }
                    try {
                        Object scopedInstance = scope.get(beanName, () -> {
                            // 保存当前线程正在创建的beanName 到 prototypesCurrentlyInCreation 中
                            beforePrototypeCreation(beanName);
                            try {
                                // 创建bean
                                return createBean(beanName, mbd, args);
                            }
                            finally {
                                // 移除当前线程正在创建的beanName 从 prototypesCurrentlyInCreation 中
                                afterPrototypeCreation(beanName);
                            }
                        });
                        //  解决FactoryBean的问题
                        bean = getObjectForBeanInstance(scopedInstance, name, beanName, mbd);
                    }
                    catch (IllegalStateException ex) {
                        throw new BeanCreationException(beanName,
                                "Scope '" + scopeName + "' is not active for the current thread; consider " +
                                        "defining a scoped proxy for this bean if you intend to refer to it from a singleton",
                                ex);
                    }
                }
            }
            catch (BeansException ex) {
                cleanupAfterBeanCreationFailure(beanName);
                throw ex;
            }
        }

        // Check if required type matches the type of the actual bean instance.
        // 9 类型转换
        // 检查需要的类型是否符合bean 的实际类型
        if (requiredType != null && !requiredType.isInstance(bean)) {
            try {
                T convertedBean = getTypeConverter().convertIfNecessary(bean, requiredType);
                if (convertedBean == null) {
                    throw new BeanNotOfRequiredTypeException(name, requiredType, bean.getClass());
                }
                return convertedBean;
            }
            catch (TypeMismatchException ex) {
                if (logger.isDebugEnabled()) {
                    logger.debug("Failed to convert bean '" + name + "' to required type '" +
                            ClassUtils.getQualifiedName(requiredType) + "'", ex);
                }
                throw new BeanNotOfRequiredTypeException(name, requiredType, bean.getClass());
            }
        }
        return (T) bean;
    }
```

### 2.4 **getSingleton(beanName,**objectFactory​​​​​​​**)方法：三级缓存获取单例Bean**

#### 2.4.1 基本介绍 

在上面doGetBean()方法的第8步， 针对不同的Scope 进行bean的创建时，会调用getSingleton()方法，这个方法主要作用是获取单例Bean，它会优先从一级缓存中获取Bean，如果一级缓存中找不到，则调用。

![](https://i-blog.csdnimg.cn/blog_migrate/b25d86fa1cf5d07f7a01ed6b44fcc7de.png)

**核心流程：**

1.   从一级缓存singletonObjects中获取Bean对象；
2.  如果一级缓存获取不到，则执行Lambda表达式，获取Bean对象
3.  Bean对象加入一级缓存，清空二级缓存、三级缓存

**代码详解：** 

org.springframework.beans.factory.support.DefaultSingletonBeanRegistry 

```java
   /**
     * 三级缓存获取Bean
     * @param beanName bean名称
     * @param singletonFactory ObjectFactory对象，实参是Lambda表达式，执行后创建Bean
     * @return {@link Object}
     */
    public Object getSingleton(String beanName, ObjectFactory<?> singletonFactory) {
        Assert.notNull(beanName, "Bean name must not be null");
        // 因为创建过程中需要操作 singletonObjects。所以需要加锁
        synchronized (this.singletonObjects) {
            // 1. 从一级缓存单例池中尝试获取bean，判断bean是否已经加载。如果加载直接返回。
            Object singletonObject = this.singletonObjects.get(beanName);
            if (singletonObject == null) {
                // 2. 判断，如果当前beanFactory正在被销毁则直接抛出异常，不允许创建单例bean
                if (this.singletonsCurrentlyInDestruction) {
                    throw new BeanCreationNotAllowedException(beanName,
                            "Singleton bean creation not allowed while singletons of this factory are in destruction " +
                                    "(Do not request a bean from a BeanFactory in a destroy method implementation!)");
                }
                if (logger.isDebugEnabled()) {
                    logger.debug("Creating shared instance of singleton bean '" + beanName + "'");
                }
                // 3. 做一些bean创建前的准备工作： 记录beanName 正在加载的状态(添加到 singletonsCurrentlyInCreation 缓存中)，若bean已经正在加载，则抛出异常。为了解决循环引用的问题
                beforeSingletonCreation(beanName);
                boolean newSingleton = false;
                boolean recordSuppressedExceptions = (this.suppressedExceptions == null);
                if (recordSuppressedExceptions) {
                    this.suppressedExceptions = new LinkedHashSet<>();
                }
                try {
                    // 4. 通过回调方式获取bean实例。调用ObjectFactory的getObject()方法，执行Lambda表达式，返回三级缓存Bean
                    singletonObject = singletonFactory.getObject();
                    newSingleton = true;
                }
                catch (IllegalStateException ex) {
                    // Has the singleton object implicitly appeared in the meantime ->
                    // if yes, proceed with it since the exception indicates that state.
                    singletonObject = this.singletonObjects.get(beanName);
                    if (singletonObject == null) {
                        throw ex;
                    }
                }
                catch (BeanCreationException ex) {
                    if (recordSuppressedExceptions) {
                        for (Exception suppressedException : this.suppressedExceptions) {
                            ex.addRelatedCause(suppressedException);
                        }
                    }
                    throw ex;
                }
                finally {
                    if (recordSuppressedExceptions) {
                        this.suppressedExceptions = null;
                    }
                    // 5. 加载单例后的处理方法调用 ： 删除bean正在创建的记录(从 singletonsCurrentlyInCreation  中移除 beanName)
                    afterSingletonCreation(beanName);
                }
                if (newSingleton) {
                    // 6. 加入到缓存中，并删除加载bean过程中所记录的各种辅助状态
                    addSingleton(beanName, singletonObject);
                }
            }
            return singletonObject;
        }
    }
 
	...

    /**
     * 添加一个单例bean到一级缓存中，清空二、三级缓存
     * @param beanName bean名称
     * @param singletonObject 单例对象
     */
    protected void addSingleton(String beanName, Object singletonObject) {
        // 加锁
        synchronized (this.singletonObjects) {
            // 添加到一级缓存中、清空二级缓存、三级缓存
            this.singletonObjects.put(beanName, singletonObject);
            this.singletonFactories.remove(beanName);
            this.earlySingletonObjects.remove(beanName);
            this.registeredSingletons.add(beanName);
        }
    }
```

#### 2.4.2 DefaultSingletonBeanRegistry类：注册和获取单例Bean

getSingleton()方法在DefaultSingletonBeanRegistry类中，该类继承了SimpleAliasRegistry类，实现了SingletonBeanRegistry接口，定义了三级缓存：

```java
    /**
     * 一级缓存，value是经过完整生命周期的Bean
     */
    private final Map<String, Object> singletonObjects = new ConcurrentHashMap<>(256);

    /**
     * 二级缓存，value是提前代理对象
     */
    private final Map<String, Object> earlySingletonObjects = new ConcurrentHashMap<>(16);
    /**
     * 三级缓存，value是Lambda表达式（ObjectFactory是一个函数式接口）
     * 函数式接口可以把匿名内部类、lambda表达式作为参数传递到方法中
     */
    private final Map<String, ObjectFactory<?>> singletonFactories = new HashMap<>(16);
```

**DefaultSingletonBeanRegistry类：**负责注册、获取、缓存、销毁单例 bean。

**核心方法：**

-   **注册单例 bean：**在容器启动时，将单例 bean 注册到注册表中。
    -   **registerSingleton(String beanName, Object singletonObject)**：将给定的单例对象注册到单例 bean 注册表中。
-   **获取单例 bean：**根据 bean 的名称从注册表中获取对应的单例 bean 实例。
    -   **getSingleton(String beanName)**：根据给定的 bean 名称从注册表中获取对应的单例 bean 实例。
-   **缓存单例 bean：**在首次获取单例 bean 后，将其缓存以供后续使用，避免重复创建。
    -   **containsSingleton(String beanName)**：检查注册表中是否包含指定名称的单例 bean。
-   **销毁单例 bean：**在容器关闭时，销毁注册表中所有单例 bean 实例。
    -   **destroySingletons()**：销毁注册表中所有单例 bean 的实例。

### 2.5 **createBean()方法：创建Bean**

#### **2.5.1 基本介绍**

我们可以详细看上面doGetBean()中，getSingleton()方法的实参，即Lambda表达式，这个Lambda表达式的核心逻辑是执行createBean()方法，创建Bean：

![](https://i-blog.csdnimg.cn/blog_migrate/e9e0155bb7f9a9f36890a7082fb0f15e.png)

**createBean()源码：**

**核心流程：**

1.  根据BeanDefinition和BeanName获取Bean的Class对象
2.  预先标记没有重载的方法
3.  如果Bean配置了初始化前和初始化后的处理器，则创建Bean的代理对象
4.  调用doCreateBean()，实际创建Bean

**详细流程：**

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory

```java
    protected Object createBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args)
            throws BeanCreationException {

        if (logger.isTraceEnabled()) {
            logger.trace("Creating instance of bean '" + beanName + "'");
        }
        //该参数是从AbstractBeanFactory的doGetBean传递过来的父子容器合并BeanDefinition
        RootBeanDefinition mbdToUse = mbd;


        //1.根据BeanDefinition和BeanName获取Bean的Class对象
        // 判断需要创建的Bean是否可以实例化，即是否可以通过当前的类加载器加载，如果可以实例化
        Class<?> resolvedClass = resolveBeanClass(mbd, beanName);
        if (resolvedClass != null && !mbd.hasBeanClass() && mbd.getBeanClassName() != null) {
            //克隆一份BeanDefinition，mbdToUse用来存储加载出来的class对象
            //之所以后续用该副本操作，是因为不希望将解析的class绑定到缓存里的BeanDefinition
            //因为class有可能是每次都需要动态解析出来的
            mbdToUse = new RootBeanDefinition(mbd);
            mbdToUse.setBeanClass(resolvedClass);
        }

        // Prepare method overrides.
        // 2.预先标记没有重载的方法
        // 校验和准备Bean中的方法覆盖
        try {
            //如果是0个则抛异常，如果是1个也就没有重载的必要
            mbdToUse.prepareMethodOverrides();
        }
        catch (BeanDefinitionValidationException ex) {
            throw new BeanDefinitionStoreException(mbdToUse.getResourceDescription(),
                    beanName, "Validation of method overrides failed", ex);
        }

        try {
            //3.如果Bean配置了初始化前和初始化后的处理器，则创建Bean的代理对象
            //resolveBeforeInstantiation只是针对有自定义的targetsource，
            //因为自定义的targetsource不是spring的bena，那么肯定不需要进行后续的一系列的实例化，初始化。
            //所以可以在resolveBeforeInstantiation直接进行proxy
            Object bean = resolveBeforeInstantiation(beanName, mbdToUse);
            if (bean != null) {
                //如果这里有处理器在bean创建的之前 给出了代理bean，则无需执行后续的逻辑，
                // 直接返回用户给出的bean
                return bean;
            }
        }
        catch (Throwable ex) {
            throw new BeanCreationException(mbdToUse.getResourceDescription(), beanName,
                    "BeanPostProcessor before instantiation of bean failed", ex);
        }

        try {
            //4.调用doCreateBean()，实际创建Bean。tip：do开头的方法才是真正处理逻辑的方法，即真正“干活”的方法。
            Object beanInstance = doCreateBean(beanName, mbdToUse, args);
            if (logger.isTraceEnabled()) {
                logger.trace("Finished creating instance of bean '" + beanName + "'");
            }
            return beanInstance;
        }
        catch (BeanCreationException | ImplicitlyAppearedSingletonException ex) {
            // A previously detected exception with proper bean creation context already,
            // or illegal singleton state to be communicated up to DefaultSingletonBeanRegistry.
            throw ex;
        }
        catch (Throwable ex) {
            throw new BeanCreationException(
                    mbdToUse.getResourceDescription(), beanName, "Unexpected exception during bean creation", ex);
        }
    }
```

#### 2.5.2 **AbstractAutowireCapableBeanFactory类：初始化Bean和自动装配**

**AbstractAutowireCapableBeanFactory类：**

createBean()方法在AbstractAutowireCapableBeanFactory类下， 该类实现了BeanFactory抽象基类AbstractBeanFactory，用于bean 初始化和自动装配。

```java
    /**
     * @Author: vince
     * @CreateTime: 2024/04/26
     * @Description: 抽象的可自动装配的BeanFactory基类，继承了AbstractBeanFactory，用于支持自动装配的BeanFactory。
     * @Version: 1.0
     */
    public abstract class AbstractAutowireCapableBeanFactory extends AbstractBeanFactory
            implements AutowireCapableBeanFactory {
...
    }
```

**AbstractAutowireCapableBeanFactory** 是 Spring Framework 中的一个重要类，它扩展了 **AbstractBeanFactory**，提供了对 Bean 自动装配的支持。

-   **自动装配（Autowiring）**：
    -   **autowireBean(Object existingBean)**：对现有的 bean 进行自动装配，包括属性注入、Aware 接口处理等。
    -   **autowireBeanProperties(Object existingBean, int autowireMode, boolean dependencyCheck)**：对现有的 bean 进行属性自动装配。
-   **Bean 初始化**：
    -   **initializeBean(String beanName, Object bean, @Nullable RootBeanDefinition mbd)**：初始化给定的 bean，包括执行各种初始化回调方法。
    -   **applyBeanPropertyValues(Object existingBean, String beanName)**：将给定 bean 名称对应的属性值应用到现有的 bean 实例中。
    -   **applyBeanPostProcessorsBeforeInitialization(Object existingBean, String beanName)**：在初始化前应用 BeanPostProcessors。
    -   **applyBeanPostProcessorsAfterInitialization(Object existingBean, String beanName)**：在初始化后应用 BeanPostProcessors。
-   **创建 Bean 实例**：
    -   **createBean(Class<?> beanClass, int autowireMode, boolean dependencyCheck)**：创建指定类的新 bean 实例。
    -   **createBean(String beanName, RootBeanDefinition mbd, @Nullable Object\[\] args)**：根据给定的 bean 定义创建新的 bean 实例。
    -   **doCreateBean(final String beanName, final RootBeanDefinition mbd, final @Nullable Object\[\] args)：**创建Bean的实际逻辑
-   **执行Bean 后置处理器（BeanPostProcessors）**：
    -   **applyBeanPostProcessorsBeforeInitialization(Object existingBean, String beanName)**：遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessBeforeInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
    -   **applyBeanPostProcessorsAfterInitialization(Object existingBean, String beanName)**：遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessAfterInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
-   **销毁 Bean 实例**：
    -   **destroyBean(String beanName, Object bean)**：销毁指定名称的 bean 实例。
-   **其他功能**：
    -   存入三级缓存和清理三级缓存。
    -   实现了对 Aware 接口的处理，如 **BeanNameAware**、**BeanClassLoaderAware** 等。
    -   支持 FactoryBean 的创建和处理。

通过这些功能和方法，**AbstractAutowireCapableBeanFactory** 实现了对 Bean 的自动装配、初始化和后处理等管理，是 Spring IoC 容器中的核心部分之一。

### 2.6 doCreateBean()方法：创建Bean的核心逻辑处理方法

在上面createBean()的第4步，是调用doCreateBean()方法，这个是创建Bean的核心方法。

> **do前缀的方法：**
> 
> 在Spring源码里边，有很多以do开头的方法，当你看到这些以do开头的方法时，应该意识到，在这个方法里边，往往才是真正的逻辑处理过程，即真正“干活”的方法。

#### 2.6.1 **核心流程**

1.  **判断单例：**创建一个BeanWrapper，如果是单例，则取出缓存赋值给它，并清除缓存
2.  **wrapper为空时实例化Bean：**调用createBeanInstance()方法，默认用无参构造方法实例化Bean，赋值给wrapper
3.  **合并处理BeanDefinition：**应用所有已注册的 MergedBeanDefinitionPostProcessor （用于修改或扩展BeanDefinition）到给定的 BeanDefinition 实例
4.  **放进三级缓存：**当Bean是单例、允许循环依赖时，将Lambda表达式放进三级缓存，以后如果执行这个Lambda表达式，生成的将是BService的提前代理对象；
5.  **属性填充：**填充注解@Autowired、@Resource、@Value等的属性
6.  **初始化bean：**调用initializeBean()方法，初始化和aop，通过JDK的Proxy.newProxyInstance()实现动态代理，返回目标对象的代理对象，对Bean进行增强。
    1.  **执行所有BeanPostProcessor的初始化前方法：**遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessBeforeInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
    2.  **初始化：**如果Bean实例实现了InitializingBean接口（通过instanceof判断），调用Bean重写的afterPropertiesSet()方法，处理初始化逻辑。afterPropertiesSet译为“在属性填充之后”
    3.  **执行所有BeanPostProcessor的初始化后方法：**遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessAfterInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
7.  **校验依赖注册为Bean：**获取所有注入属性，检查这些属性是否已被注册为Bean，如果存在依赖没注册为Bean，则抛出异常
8.  **注册销毁Bean：**调用registerDisposableBeanIfNecessary()方法，注册DisposableBean，以便在销毁bean 的时候可以运行指定的相关业务。
    1.  **判断实现DisposableBean接口：**当前Bean是否实现了DisposableBean接口，是则直接返回true；否则进行【推断销毁方法】流程
    2.  **推断销毁方法：**
        1.  寻找当前bean下是否有close方法或者shutdown方法，或者是否实现了AutoCloseable接口，是则直接返回销毁方法名称
        2.  感知销毁Bean后置处理器：如果【推断销毁方法】也没有结果，则调用【感知销毁Bean后置处理器】DestructionAwareBeanPostProcessor.requiresDestruction(bean)判断，如果当前bean是ApplicationListener子类需要销毁，拥有@PreDestroy注解了的方法就是需要销毁
    3.  **适配成DisposableBeanAdapter对象：**如果需要销毁，则适配成DisposableBeanAdapter对象，并存入disposableBeans中（一个LinkedHashMap<String, Object>）

![](https://i-blog.csdnimg.cn/blog_migrate/610621ce75bde5be79a9bc610efdd0b3.png)

#### 2.6​​​​​​​.2 **BeanWrapper及其与**BeanDefinition的区别

**BeanWrapper：Bean的打包类，用于获取Bean实例、Class对象和属性**

BeanWrapper是对Bean进行**封装打包**的类，Spring在对Bean封装打包得到BeanWrapper对象之后，我们就可以通过BeanWrapper访问Bean的属性和方法。它提供了访问和操作 Bean 实例属性的方法，允许对 Bean 实例进行属性的设置、获取以及类型转换等操作。

**作用：**

-   封装了 Bean 实例，并提供了对 Bean 属性的访问和操作方法。
-   允许对 Bean 实例的属性进行动态修改。

 ![](https://i-blog.csdnimg.cn/blog_migrate/475202acce4608fb013c4c43694c1e68.png)

**使用示例：**

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory

```java
        // 1.创建bean实例，赋值给instanceWrapper；
        // bean初始化第一步：默认调用无参构造实例化Bean
        // 构造参数依赖注入，就是发生在这一步
        if (instanceWrapper == null) {
            instanceWrapper = createBeanInstance(beanName, mbd, args);
        }
        // 实例化后的Bean对象
        final Object bean = instanceWrapper.getWrappedInstance();
        Class<?> beanType = instanceWrapper.getWrappedClass();
```

> 注意跟BeanDefinition做好区分。
> 
> **BeanDefinition：**  
> BeanDefinition 是 Spring 框架中用于描述 Bean 的元数据的接口。它包含了 Bean 的各种属性配置信息，如类名、作用域、构造函数参数、属性值、依赖关系等。
> 
> **区别：**
> 
> -   **功能不同：**
>     
>     -   **BeanWrapper：**主要用于对 Bean 实例的属性进行操作和管理。
>         
>     -   **BeanDefinition：**主要用于描述 Bean 的元数据信息，包括类名、作用域、属性值等配置信息。
>         
> -   **关注点不同：**
>     
>     -   **BeanWrapper：**关注于对 Bean 实例本身的操作，例如属性的设置和获取。
>         
>     -   **BeanDefinition：**关注于 Bean 的配置信息，定义了 Bean 的创建和初始化规则。
>         
> -   **用途不同：**
>     
>     -   **BeanWrapper：**主要用于在**运行时**动态地操作 Bean 实例的属性。
>         
>     -   **BeanDefinition：**主要用于在**容器启动时**描述和配置 Bean 的元数据信息。
>         

#### 2.6​​​​​​​.3 **详细流程**

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory

```java
    /**
     * 创建Bean的核心逻辑处理方法
     *
     * @param beanName bean名称
     * @param mbd      BeanDefinition对象
     * @param args     构造函数参数
     * @return {@link Object}
     * @throws BeanCreationException Bean创建异常
     */
    protected Object doCreateBean(final String beanName, final RootBeanDefinition mbd, final @Nullable Object[] args)
            throws BeanCreationException {

        // 1.判断单例：创建一个BeanWrapper，如果是单例，则取出缓存赋值给它，并清除缓存
        BeanWrapper instanceWrapper = null;
        // 如果BeanDefinition是单例模式，就先从缓存中清除
        if (mbd.isSingleton()) {
            instanceWrapper = this.factoryBeanInstanceCache.remove(beanName);
        }
        // 2.wrapper为空时实例化Bean：调用createBeanInstance()方法，默认用无参构造方法实例化Bean，赋值给wrapper
        // bean初始化第一步：默认调用无参构造实例化Bean
        // 构造参数依赖注入，就是发生在这一步
        if (instanceWrapper == null) {
            instanceWrapper = createBeanInstance(beanName, mbd, args);
        }
        // 实例化后的Bean对象
        final Object bean = instanceWrapper.getWrappedInstance();
        Class<?> beanType = instanceWrapper.getWrappedClass();
        if (beanType != NullBean.class) {
            // 将 解析类型 设置 为 beanType
            mbd.resolvedTargetType = beanType;
        }

        // Allow post-processors to modify the merged bean definition.
        // 使用后置处理器 对其进行处理
        synchronized (mbd.postProcessingLock) {
            if (!mbd.postProcessed) {
                try {
                    // 合并处理BeanDefinition：应用所有已注册的 MergedBeanDefinitionPostProcessor （用于修改或扩展BeanDefination）到给定的 BeanDefinition 实例
                    //对@Autowire,@Value等这些注解进行处理
                    applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
                } catch (Throwable ex) {
                    throw new BeanCreationException(mbd.getResourceDescription(), beanName,
                            "Post-processing of merged bean definition failed", ex);
                }
                mbd.postProcessed = true;
            }
        }

        // 3.存入三级缓存：当Bean是单例、允许循环依赖时，将Lambda表达式放进三级缓存，以后如果执行这个Lambda表达式，生成的将是BService的提前代理对象；
        // Eagerly cache singletons to be able to resolve circular references
        // even when triggered by lifecycle interfaces like BeanFactoryAware.
        /**是否需要提前曝光： 单例& 允许循环依赖 & 当前bean正在创建中， 检查循环依赖
         这里主要是调用 方法addSingletonFactory ，往缓存singletonFactories里面 放入一个 ObjectFactory
         当其他的bean 对该bean 有依赖时，可以提前获取到
         getEarlyBeanReference方法就是获取一个引用， 里面主要是
         调用了  SmartInstantiationAwareBeanPostProcessor，
         的 getEarlyBeanReference 方法，以便解决循环依赖问题, 这里 一般都是bean  本身，
         在 AOP时 是代理
         **/
        boolean earlySingletonExposure = (mbd.isSingleton() && this.allowCircularReferences &&
                isSingletonCurrentlyInCreation(beanName));
        if (earlySingletonExposure) {
            if (logger.isTraceEnabled()) {
                logger.trace("Eagerly caching bean '" + beanName +
                        "' to allow for resolving potential circular references");
            }
            // 将刚创建的bean放入三级缓存中，singleFactories(key是beanName，value是ObjectFactory)
            // 注意此处实参又是一个lambda表达式，
            // 即参数传入的是ObjectFactory类型一个匿名内部类对象，在后续再缓存中查找Bean时会触发匿名内部类getEarlyBeanReference()方法回调
            addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));
        }
        // 4.依赖处理

        // Initialize the bean instance.
        Object exposedObject = bean;
        // 下面就是初始化实例了
        try {
            // 5.填充属性（DI依赖注入发生在此步骤）
            // 对bean进行填充，将各个属性值注入，其中可能存在依赖于其他bean的属性,会递归初始化
            populateBean(beanName, mbd, instanceWrapper);
            // 6.初始化bean：初始化和aop，通过JDK的Proxy.newProxyInstance()实现动态代理，返回目标对象的代理对象，对Bean进行增强。
            // AOP是通过自动代理创建器AbstractAutoProxyCreator的postProcessAfterInitialization()
            //方法的执行进行代理对象的创建的,AbstractAutoProxyCreator是BeanPostProcessor接口的实现类
            //进一步初始化Bean
            //注入 Aware 相关的对象
            // 调用 后置处理器 BeanPostProcessor 里面的postProcessBeforeInitialization方法
            // 调用 initialzingBean，调用实现的 afterPropertiesSet()
            // 调用 init-mothod，调用相应的init方法
            // 调用 后置处理器 BeanPostProcessor 里面的调用实现的postProcessAfterInitialization方法
            exposedObject = initializeBean(beanName, exposedObject, mbd);
        } catch (Throwable ex) {
            if (ex instanceof BeanCreationException && beanName.equals(((BeanCreationException) ex).getBeanName())) {
                throw (BeanCreationException) ex;
            } else {
                throw new BeanCreationException(
                        mbd.getResourceDescription(), beanName, "Initialization of bean failed", ex);
            }
        }

        if (earlySingletonExposure) {
            Object earlySingletonReference = getSingleton(beanName, false);
            // earlySingletonReference 只有在检测到有循环依赖的情况下才会不为空
            if (earlySingletonReference != null) {
                //如果exposedObject 没有在初始化方法中被改变，也就是没有被增强
                if (exposedObject == bean) {
                    exposedObject = earlySingletonReference;
                } else if (!this.allowRawInjectionDespiteWrapping && hasDependentBean(beanName)) {
                    // 7.依赖检查：获取所有注入属性，检查这些属性是否已被注册为Bean
                    String[] dependentBeans = getDependentBeans(beanName);
                    Set<String> actualDependentBeans = new LinkedHashSet<>(dependentBeans.length);
                    // 检查依赖
                    for (String dependentBean : dependentBeans) {
                        if (!removeSingletonIfCreatedForTypeCheckOnly(dependentBean)) {
                            actualDependentBeans.add(dependentBean);
                        }
                    }
                    /**
                     因为 bean 创建后其所依赖的bean一定是已经创建，
                     actualDependentBeans 不为空则表示 当前bean 创建后其依赖的bean 却没有全部创建，
                     也就是说存在依赖
                     */
                    if (!actualDependentBeans.isEmpty()) {
                        throw new BeanCurrentlyInCreationException(beanName,
                                "Bean with name '" + beanName + "' has been injected into other beans [" +
                                        StringUtils.collectionToCommaDelimitedString(actualDependentBeans) +
                                        "] in its raw version as part of a circular reference, but has eventually been " +
                                        "wrapped. This means that said other beans do not use the final version of the " +
                                        "bean. This is often the result of over-eager type matching - consider using " +
                                        "'getBeanNamesOfType' with the 'allowEagerInit' flag turned off, for example.");
                    }
                }
            }
        }
        // 8.注册销毁Bean
        try {
            registerDisposableBeanIfNecessary(beanName, bean, mbd);
        } catch (BeanDefinitionValidationException ex) {
            throw new BeanCreationException(
                    mbd.getResourceDescription(), beanName, "Invalid destruction signature", ex);
        }

        return exposedObject;
    }
```

### 2.​​​7 createBeanInstance()：推断并实例化Bean

上面doCreateBean()方法的第2步，如果从缓存中没取到BeanWrapper（Bean包装器，用于获取Bean实例、Class对象和属性），则执行createBeanInstance()，推断构造方法、创建方式（工厂模式、生产者模式），并创建Bean实例。

**核心流程：**

-   **解析获取 Bean 的Class对象**：调用 resolveBeanClass(mbd, beanName)方法解析 Bean ，获取Bean 的Class对象，用于获取类的属性和调用newInstance()方法实例化。
-   **校验 Bean 必须非空且public**：如果 Bean 类型为null、或者不是公共类，则抛出异常。
-   **判断是否使用Supplier创建 Bean**：如果 BeanDefinition 中包含实例供应器Supplier（根据BeanDefiniton的instanceSupplier属性判断），则调用该实例供应器来创建 Bean 实例。
-   **判断是否使用工厂方法创建 Bean**： BeanDefinition 中配置了工厂方法，则尝试调用该工厂方法来创建 Bean 实例。
-   **判断构造函数是否缓存过**：如果已经解析过 Bean 类型的构造函数，并且不需要自动装配，则直接使用缓存的构造函数或默认构造函数来创建 Bean 实例。缓存位置在BeanDefinition 的resolvedConstructorOrFactoryMethod字段，缓存值的类型是Executable（代表可执行的程序单元，可以是普通方法或者构造方法，可以通过它获取方法的参数类型、个数等信息）
-   **判断构造函数是否需要自动装配**：如果存在可选构造函数、设置了构造参数值、有参与构造函数参数列表的参数或者配置了构造函数自动装配，则进入自动装配构造函数的流程。
-   **后置处理器中寻找候选构造函数**：从 Bean 的后置处理器中寻找候选构造函数，这些构造函数可能是通过 @Autowired 注解标注的构造函数或者是通过其他方式标注的。
-   **推断构造函数并自动装配**：根据候选构造函数和参数来确定最终的构造函数，并进行自动装配。

**详细流程：**

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory 

```java
    /**
     * 根据BeanDefinition中的信息，创建Bean实例
     *
     * @param beanName Bean的名称
     * @param mbd      Bean的定义信息
     * @param args     构造器参数
     * @return {@link BeanWrapper}
     */
    protected BeanWrapper createBeanInstance(String beanName, RootBeanDefinition mbd, @Nullable Object[] args) {
        // 1.获取Bean 的Class对象，用于获取类的属性和调用newInstance()方法实例化
        // 解析Bean的类型，确认需要创建的bean实例的类可以实例化。
        // 如果没有设置通过Class.forName获取Bean类型
        Class<?> beanClass = resolveBeanClass(mbd, beanName);

        // 2.校验 Bean 必须非空且public：如果 Bean 类型为null、或者不是公共类，则抛出异常。
        // 确保class不为空，并且访问权限是public
        if (beanClass != null && !Modifier.isPublic(beanClass.getModifiers()) && !mbd.isNonPublicAccessAllowed()) {
            throw new BeanCreationException(mbd.getResourceDescription(), beanName,
                    "Bean class isn't public, and non-public access not allowed: " + beanClass.getName());
        }

        // 3.判断是否使用Supplier创建 Bean：如果 BeanDefinition 中包含实例供应器Supplier，则调用该实例供应器来创建 Bean 实例。
        // ①Supplier方式创建Bean: 需要先有回调Bean
        // 判断当前beanDefinition中是否包含实例供应器，此处相当于一个回调方法，利用回调方法来创建bean
        Supplier<?> instanceSupplier = mbd.getInstanceSupplier();
        if (instanceSupplier != null) {
            return obtainFromSupplier(instanceSupplier, beanName);
        }
        // 4.判断是否使用工厂方法创建 Bean： BeanDefinition 中配置了工厂方法，则尝试调用该工厂方法来创建 Bean 实例。
        // ②FactoryMethod方式创建Bean: 需要在XML中配置factory-method
        // 判断是否有工厂方法，如果存在，会尝试调用该Bean定义信息中的工厂方法来获取实例
        if (mbd.getFactoryMethodName() != null) {
            return instantiateUsingFactoryMethod(beanName, mbd, args);
        }

        // 5.判断构造函数是否缓存过：
        // 如果已经解析过 Bean 类型的构造函数，并且不需要自动装配，则直接使用缓存的构造函数或默认构造函数来创建 Bean 实例。
        // 缓存位置在BeanDefinition 的resolvedConstructorOrFactoryMethod字段;
        // 缓存值的类型是Executable（代表可执行的程序单元，可以是普通方法或者构造方法，可以通过它获取方法的参数类型、个数等信息）
        // Shortcut when re-creating the same bean...
        //一个类可能有多个构造器，所以Spring得根据参数个数、类型确定需要调用的构造器，当多次构建同一个 bean 时就不需要重新判断应该使用那种方式构造Bean
        boolean resolved = false;
        //是否需要自动装配
        boolean autowireNecessary = false;
        if (args == null) {
            synchronized (mbd.constructorArgumentLock) {
                // 因为判断过程会比较慢，所以spring会将解析、确定好的构造函数缓存到BeanDefinition中的resolvedConstructorOrFactoryMethod字段中。
                // 在下次创建相同时直接从RootBeanDefinition中的属性resolvedConstructorOrFactoryMethod缓存的值获取，避免再次解析，导致循环依赖
                // 这个字段是一个包可见的字段，用于缓存已解析的构造函数或工厂方法。
                if (mbd.resolvedConstructorOrFactoryMethod != null) {
                    //标识以及解析过class的构造器
                    resolved = true;
                    autowireNecessary = mbd.constructorArgumentsResolved;
                }
            }
        }
        // 6.判断是否需要自动装配构造函数：如果存在可选构造函数、设置了构造参数值、有参与构造函数参数列表的参数或者配置了构造函数自动装配，则进入自动装配构造函数的流程。
        // 有构造参数的或者工厂
        if (resolved) {
            //已经解析过class的构造器，使用已经解析好的构造器
            if (autowireNecessary) {
                //构造函数自动注入
                return autowireConstructor(beanName, mbd, null, null);
            } else {
                //使用默认构造器
                return instantiateBean(beanName, mbd);
            }
        }



        // 7.后置处理器中寻找候选构造函数：从 Bean 的后置处理器中寻找候选构造函数，这些构造函数可能是通过 @Autowired 注解标注的构造函数或者是通过其他方式标注的。
        Constructor<?>[] ctors = determineConstructorsFromBeanPostProcessors(beanClass, beanName);
        // 8.推断构造函数并自动装配：根据候选构造函数和参数来确定最终的构造函数，并进行自动装配。
        // 从bean后置处理器中为自动装配寻找构造方法
        // 以下情况符合其一即可进入
        // 1、存在可选构造方法
        // 2、自动装配模型为构造函数自动装配
        // 3、给BeanDefinition中设置了构造参数值
        // 4、有参与构造函数参数列表的参数
        if (ctors != null || mbd.getResolvedAutowireMode() == AUTOWIRE_CONSTRUCTOR ||
                mbd.hasConstructorArgumentValues() || !ObjectUtils.isEmpty(args)) {
            return autowireConstructor(beanName, mbd, ctors, args);
        }

        // Preferred constructors for default construction?
        // 从bean后置处理器中为自动装配寻找构造方法, 有且仅有一个有参构造或者有且仅有@Autowired注解构造
        ctors = mbd.getPreferredConstructors();

        if (ctors != null) {
            // 构造函数自动注入
            // 二、有参构造创建Bean
            return autowireConstructor(beanName, mbd, ctors, null);
        }

        // No special handling: simply use no-arg constructor.
        // 使用默认无参构造函数创建对象，如果没有无参构造且存在多个有参构造且没有@AutoWired注解构造，会报错
        //三、无参构造创建Bean
        return instantiateBean(beanName, mbd);
    }
```

### 2.​​​8 instantiateBean()：实例化和包装Bean

在上面 createBeanInstance()方法中，确定构造方法后，会执行instantiateBean()方法，来实例化Bean，并将实例化的 Bean 包装成 BeanWrapper 对象。

> instantiate译为实例、实例化。

**核心流程：**

1.  调用instantiate()方法实例化Bean；
2.  将实例化后的Bean包装成 BeanWrapper 对象；
3.  调用 initBeanWrapper(bw) 方法对 BeanWrapper 进行初始化，关联转换服务并注册自定义编辑器；
4.  返回 BeanWrapper；

**详细流程：** 

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory 

```java
	/**
	 * Instantiate the given bean using its default constructor.
	 *
	 * 使用其默认构造函数实例化给定的 bean。
	 *
	 * @param beanName the name of the bean
	 * @param mbd the bean definition for the bean
	 * @return a BeanWrapper for the new instance
	 */
	protected BeanWrapper instantiateBean(final String beanName, final RootBeanDefinition mbd) {
		try {
			Object beanInstance;
			final BeanFactory parent = this;
			if (System.getSecurityManager() != null) {
				beanInstance = AccessController.doPrivileged((PrivilegedAction<Object>) () ->
						getInstantiationStrategy().instantiate(mbd, beanName, parent),
						getAccessControlContext());
			}
			else {
				// 使用默认的实例化策略来实例化对象，默认为 CglibSubclassingInstantiationStrategy 实现，但是instantiate()方法只在SimpleInstantiationStrategy里有实现逻辑
				beanInstance = getInstantiationStrategy().instantiate(mbd, beanName, parent);
			}
            // 包装成BeanWrapper：Bean的打包类，用于获取Bean实例、Class对象和属性
			BeanWrapper bw = new BeanWrapperImpl(beanInstance);
			initBeanWrapper(bw);
			return bw;
		}
		catch (Throwable ex) {
			throw new BeanCreationException(
					mbd.getResourceDescription(), beanName, "Instantiation of bean failed", ex);
		}
	}
```

### 2.​​​9 instantiate()：根据构造方法实例化Bean

**核心流程：**

1.  **检查BeanDefinition是否有重写：**如果没重写则直接实例化，否则执行下面步骤
    
2.  **获取要使用的构造方法进行实例化：**
    
    -   通过同步锁确保获取构造方法的线程安全。
        
    -   检查 RootBeanDefinition 是否含有构造方法，如果没有则获取无参构造方法后实例化，如果有则直接实例化
        

**详细流程：** 

org.springframework.beans.factory.support.SimpleInstantiationStrategy

```java
    /**
     * 实例化Bean
     * @param bd BeanDefinition
     * @param beanName Bean名称
     * @param owner BeanFactory
     * @return {@link Object}
     */
    public Object instantiate(RootBeanDefinition bd, @Nullable String beanName, BeanFactory owner) {
        // bd对象定义中，是否包含MethodOverride列表，spring中有两个标签参数会产生MethodOverrides,分别是lookup-method,replaced-method
        // 1.检查BeanDefinition是否有重写：如果没重写则直接实例化，否则执行下面步骤
        if (!bd.hasMethodOverrides()) {
            // 2. 获取实例化对象的构造方法
            Constructor<?> constructorToUse;
            // 2.1 锁定对象，使获得实例化构造方法线程安全
            synchronized (bd.constructorArgumentLock) {
                // 查看bd对象里是否含有构造方法
                constructorToUse = (Constructor<?>) bd.resolvedConstructorOrFactoryMethod;
                // 2.2 检查 RootBeanDefinition 是否含有构造方法，如果没有则获取无参构造方法后实例化，如果有则直接实例化
                // 如果bd对象里没有构造方法
                if (constructorToUse == null)   {
                    // 从bd中获取beanClass
                    final Class<?> clazz = bd.getBeanClass();
                    // 如果要实例化的beanDefinition是一个接口，则直接抛出异常
                    if (clazz.isInterface()) {
                        throw new BeanInstantiationException(clazz, "Specified class is an interface");
                    }
                    try {
                        // 获取系统安全管理器
                        if (System.getSecurityManager() != null) {
                            constructorToUse = AccessController.doPrivileged((PrivilegedExceptionAction<Constructor<?>>) clazz::getDeclaredConstructor);
                        }
                        else {
                            // 获取默认的无参构造器
                            constructorToUse = clazz.getDeclaredConstructor();
                        }
                        // 获取到构造器之后将构造器赋值给bd中的属性
                        bd.resolvedConstructorOrFactoryMethod = constructorToUse;
                    }
                    catch (Throwable ex) {
                        throw new BeanInstantiationException(clazz, "No default constructor found", ex);
                    }
                }
            }
            // 通过反射生成具体的实例化对象
            return BeanUtils.instantiateClass(constructorToUse);
        }
        else {
            // 必须生成cglib子类
            return instantiateWithMethodInjection(bd, beanName, owner);
        }
    }
```

### 2.​​​10 BeanUtils.instantiateClass()：基于反射实例化Bean

BeanUtils.instantiateClass()是具体的实例化方法，调用Class类的newInstance()方法，基于反射实例化Bean。

org.springframework.beans.BeanUtils

```java
    /**
     *  基于反射实例化Bean
     * @param ctor Bean的构造器
     * @param args Bean的参数
     * @return {@link T}
     */
public static <T> T instantiateClass(Constructor<T> ctor, Object... args) throws BeanInstantiationException {
		Assert.notNull(ctor, "Constructor must not be null");
		try {
			ReflectionUtils.makeAccessible(ctor);
			if (KotlinDetector.isKotlinReflectPresent() && KotlinDetector.isKotlinType(ctor.getDeclaringClass())) {
				return KotlinDelegate.instantiateClass(ctor, args);
			}
			else {
				Class<?>[] parameterTypes = ctor.getParameterTypes();
				Assert.isTrue(args.length <= parameterTypes.length, "Can't specify more arguments than constructor parameters");
				Object[] argsWithDefaultValues = new Object[args.length];
				for (int i = 0 ; i < args.length; i++) {
					if (args[i] == null) {
						Class<?> parameterType = parameterTypes[i];
						argsWithDefaultValues[i] = (parameterType.isPrimitive() ? DEFAULT_TYPE_VALUES.get(parameterType) : null);
					}
					else {
						argsWithDefaultValues[i] = args[i];
					}
				}
                //调用Class类的newInstance()方法，基于反射实例化Bean
				return ctor.newInstance(argsWithDefaultValues);
			}
		}
		catch (InstantiationException ex) {
			throw new BeanInstantiationException(ctor, "Is it an abstract class?", ex);
		}
		catch (IllegalAccessException ex) {
			throw new BeanInstantiationException(ctor, "Is the constructor accessible?", ex);
		}
		catch (IllegalArgumentException ex) {
			throw new BeanInstantiationException(ctor, "Illegal arguments for constructor", ex);
		}
		catch (InvocationTargetException ex) {
			throw new BeanInstantiationException(ctor, "Constructor threw exception", ex.getTargetException());
		}
	}
```

> **基于反射实例化Bean使用示例：**
> 
> ```java
> public class MyClass {
>     private String message;
> 
>     public MyClass() {
>         this.message = "Hello, world!";
>     }
> 
>     public MyClass(String message) {
>         this.message = message;
>     }
> 
>     public String getMessage() {
>         return message;
>     }
> }
> 
> public class Main {
>     public static void main(String[] args) {
>         // 实例化一个 MyClass 对象，使用默认的无参构造函数
>         MyClass instance1 = BeanUtils.instantiateClass(MyClass.class);
>         // Output: Hello, world!
>         System.out.println("Instance 1 message: " + instance1.getMessage()); 
> 
>         // 实例化一个 MyClass 对象，使用带参构造函数
>         MyClass instance2 = BeanUtils.instantiateClass(MyClass.class, "Custom message");
>         // Output: Custom message
>         System.out.println("Instance 2 message: " + instance2.getMessage()); 
>     }
> }
> ```

### 2.​​​11 initializeBean()： 初始化和调用前后置处理器

上面doCreateBean()方法第6步初始化Bean时，有调用initializeBean()方法，这个方法的主要作用是初始化和增强Bean。

**核心流程：**

1.  **执行 Aware 接口的回调方法：**先检查是否有安全管理器，如果有就以特权方式执行回调bean中Aware接口方法。
2.  **调用前置处理器：**执行所有BeanPostProcessor的初始化前方法：如果BeanDefinition是空或者不是合成（isSynthetic()，合成的 Bean 定义通常是在运行时由框架生成的，而不是由用户显式定义的。）的，则遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessBeforeInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。
3.  **初始化：**如果Bean实例实现了InitializingBean接口（通过instanceof判断），调用Bean重写的afterPropertiesSet()方法，处理初始化逻辑。afterPropertiesSet译为“在属性填充之后”
4.  **调用后置处理器：**执行所有BeanPostProcessor的初始化后方法：遍历所有BeanPostProcessor实现类所在的列表，执行每个BeanPostProcessor对象里的postProcessAfterInitialization()方法。本方法可以通过JDK的Proxy.newProxyInstance()实现动态代理返回目标对象的代理对象。

**详细流程：**

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory 

```java
    protected Object initializeBean(String beanName, Object bean, @Nullable RootBeanDefinition mbd) {
        // 1.执行 Aware 接口的回调方法：先检查是否有安全管理器，如果有就以特权方式执行回调bean中Aware接口方法
        // Aware 接口主要包括 BeanNameAware、BeanFactoryAware 和 ApplicationContextAware 接口。
        if (System.getSecurityManager() != null) {
            AccessController.doPrivileged((PrivilegedAction<Object>) () -> {
                invokeAwareMethods(beanName, bean);
                return null;
            }, getAccessControlContext());
        }
        else {
            invokeAwareMethods(beanName, bean);
        }

        Object wrappedBean = bean;
        // 2.前置处理器的调用
        if (mbd == null || !mbd.isSynthetic()) {
            wrappedBean = applyBeanPostProcessorsBeforeInitialization(wrappedBean, beanName);
        }

        // 3.初始化Bean
        try {
            invokeInitMethods(beanName, wrappedBean, mbd);
        }
        catch (Throwable ex) {
            throw new BeanCreationException(
                    (mbd != null ? mbd.getResourceDescription() : null),
                    beanName, "Invocation of init method failed", ex);
        }
        // 4.前置处理器的调用
        if (mbd == null || !mbd.isSynthetic()) {
            wrappedBean = applyBeanPostProcessorsAfterInitialization(wrappedBean, beanName);
        }

        return wrappedBean;
    }
```