> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[一、概念准备](#%E4%B8%80%E3%80%81%E6%A6%82%E5%BF%B5%E5%87%86%E5%A4%87%C2%A0) 

[1.1 循环依赖](#1.1%20%E5%BE%AA%E7%8E%AF%E4%BE%9D%E8%B5%96)

[1.2 Bean的生命周期](#1.2%20Bean%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

[二、环境准备](#%E4%BA%8C%E3%80%81%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)

[2.1 代码准备](#2.1%20%E4%BB%A3%E7%A0%81%E5%87%86%E5%A4%87)

[2.2 如何给Spring源码添加注释？](#2.2%20%E5%A6%82%E4%BD%95%E7%BB%99Spring%E6%BA%90%E7%A0%81%E6%B7%BB%E5%8A%A0%E6%B3%A8%E9%87%8A%EF%BC%9F)

[2.2.1 方法一：IDEA插件Private Notes](#2.2.1%20%E6%96%B9%E6%B3%95%E4%B8%80%EF%BC%9AIDEA%E6%8F%92%E4%BB%B6Private%20Notes)

[2.2.2 方法二（推荐）：覆盖类（基于双亲委派模型）](#2.2.2%20%E6%96%B9%E6%B3%95%E4%BA%8C%EF%BC%88%E6%8E%A8%E8%8D%90%EF%BC%89%EF%BC%9A%E8%A6%86%E7%9B%96%E7%B1%BB%EF%BC%88%E5%9F%BA%E4%BA%8E%E5%8F%8C%E4%BA%B2%E5%A7%94%E6%B4%BE%E6%A8%A1%E5%9E%8B%EF%BC%89)

[三、三级缓存介绍](#%E4%B8%89%E3%80%81%E4%B8%89%E7%BA%A7%E7%BC%93%E5%AD%98%E4%BB%8B%E7%BB%8D)

[3.1 简介](#3.1%20%E7%AE%80%E4%BB%8B)

[3.2 源码位置：DefaultSingletonBeanRegistry类](#3.2%20%E6%BA%90%E7%A0%81%E4%BD%8D%E7%BD%AE%EF%BC%9ADefaultSingletonBeanRegistry%E7%B1%BB)

[3.3 详解ObjectFactory](#3.3%20%E8%AF%A6%E8%A7%A3ObjectFactory)

[3.3.1 函数式接口回顾](#3.3.1%20%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3%E5%9B%9E%E9%A1%BE)

[3.3.2 ObjectFactory](#3.3.2%20ObjectFactory)

[四、三级缓存解决循环依赖](#%E5%9B%9B%E3%80%81%E4%B8%89%E7%BA%A7%E7%BC%93%E5%AD%98%E8%A7%A3%E5%86%B3%E5%BE%AA%E7%8E%AF%E4%BE%9D%E8%B5%96)

[4.0 核心流程简化版](#4.1%20%E6%A0%B8%E5%BF%83%E6%B5%81%E7%A8%8B%E7%AE%80%E5%8C%96%E7%89%88)

[4.1 前置流程](#4.0%20%E5%89%8D%E7%BD%AE%E6%B5%81%E7%A8%8B)

[4.1.1 方法调用链：getBean() -> doGetBean() -> getSingleton() -> createBean() -> doCreateBean()](#4.0.1%20%E6%96%B9%E6%B3%95%E8%B0%83%E7%94%A8%E9%93%BE%EF%BC%9AgetBean%28%29%C2%A0-%3E%20doGetBean%28%29%20-%3E%C2%A0getSingleton%28%29%20-%3E%C2%A0createBean%28%29%20-%3E%20doCreateBean%28%29)

[4.1.2 详解doCreateBean()方法](#4.0.2%20%E8%AF%A6%E8%A7%A3doCreateBean%28%29%E6%96%B9%E6%B3%95)

[4.2 推断并实例化Bean](#4.1%20%E6%8E%A8%E6%96%AD%E5%B9%B6%E5%AE%9E%E4%BE%8B%E5%8C%96Bean)

[4.2.1 核心流程](#4.1.1%20%E6%A0%B8%E5%BF%83%E6%B5%81%E7%A8%8B%C2%A0) 

[4.2.2 详解createBeanInstance()：推断构造方法并实例化Bean](#4.1.2%20%E8%AF%A6%E8%A7%A3createBeanInstance%28%29%EF%BC%9A%E6%8E%A8%E6%96%AD%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95%E5%B9%B6%E5%AE%9E%E4%BE%8B%E5%8C%96Bean)

[4.3 存入第三级缓存](#4.2%20%E5%AD%98%E5%85%A5%E7%AC%AC%E4%B8%89%E7%BA%A7%E7%BC%93%E5%AD%98%C2%A0) 

[4.3.1 概述](#4.2.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[4.3.2 addSingletonFactory()：存入第三级缓存](#4.2.2%20addSingletonFactory%28%29%EF%BC%9A%E5%AD%98%E5%85%A5%E7%AC%AC%E4%B8%89%E7%BA%A7%E7%BC%93%E5%AD%98)

[4.3.3 getEarlyBeanReference()：生成提前代理对象](#4.2.3%C2%A0getEarlyBeanReference%28%29%EF%BC%9A%E7%94%9F%E6%88%90%E6%8F%90%E5%89%8D%E4%BB%A3%E7%90%86%E5%AF%B9%E8%B1%A1)

[4.4 属性填充：解决循环依赖在这一步完成](#4.3%20%E5%B1%9E%E6%80%A7%E5%A1%AB%E5%85%85%EF%BC%9A%E8%A7%A3%E5%86%B3%E5%BE%AA%E7%8E%AF%E4%BE%9D%E8%B5%96%E5%9C%A8%E8%BF%99%E4%B8%80%E6%AD%A5%E5%AE%8C%E6%88%90)

[4.4.1 概述](#4.3.1%20%E6%A6%82%E8%BF%B0)

[4.4.2 populateBean()：属性填充](#4.3.2%20populateBean%28%29%EF%BC%9A%E5%B1%9E%E6%80%A7%E5%A1%AB%E5%85%85)

[4.4.3 applyPropertyValues()：解析、转换所有属性](#applyPropertyValues%28%29%EF%BC%9A%E8%A7%A3%E6%9E%90%E3%80%81%E8%BD%AC%E6%8D%A2%E6%89%80%E6%9C%89%E5%B1%9E%E6%80%A7)

[4.4.4 resolveValueIfNecessary()：根据类型解析属性](#4.3.3%20resolveValueIfNecessary%28%29%EF%BC%9A%E6%A0%B9%E6%8D%AE%E7%B1%BB%E5%9E%8B%E8%A7%A3%E6%9E%90%E5%B1%9E%E6%80%A7)

[4.4.4.1 基本介绍](#4.3.3.1%20%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D)

[4.4.4.2 BeanDefinitionValueResolver类： 解析Bean的属性](#4.3.3.2%20BeanDefinitionValueResolver%E7%B1%BB%EF%BC%9A%C2%A0%E8%A7%A3%E6%9E%90Bean%E7%9A%84%E5%B1%9E%E6%80%A7)

[4.4.5 resolveReference()：调用getBean()解析属性为Bean](#4.3.4%20resolveReference%28%29%EF%BC%9A%E8%B0%83%E7%94%A8getBean%28%29%E8%A7%A3%E6%9E%90%E5%B1%9E%E6%80%A7%E4%B8%BABean)

[4.4.6 属性获取Bean流程：getBean() -> doGetBean()](#4.3.5%20%E5%B1%9E%E6%80%A7%E8%8E%B7%E5%8F%96Bean%E6%B5%81%E7%A8%8B%EF%BC%9AgetBean%28%29%20-%3E%20doGetBean%28%29)

[4.4.6.1 直接从缓存中获取到AService](#4.3.5.1%20%E7%9B%B4%E6%8E%A5%E4%BB%8E%E7%BC%93%E5%AD%98%E4%B8%AD%E8%8E%B7%E5%8F%96%E5%88%B0AService)

[4.4.6.2 getSingleton(beanName) ：从缓存中获取单例Bean](#4.3.5.2%20getSingleton%28beanName%29%20%EF%BC%9A%E4%BB%8E%E7%BC%93%E5%AD%98%E4%B8%AD%E8%8E%B7%E5%8F%96%E5%8D%95%E4%BE%8BBean)

[4.4.6.3 getSingleton(beanName,true)：从缓存中获取单例Bean（是否允许循环依赖）](#4.3.5.3%20getSingleton%28beanName%2Ctrue%29%EF%BC%9A%E4%BB%8E%E7%BC%93%E5%AD%98%E4%B8%AD%E8%8E%B7%E5%8F%96%E5%8D%95%E4%BE%8BBean%EF%BC%88%E6%98%AF%E5%90%A6%E5%85%81%E8%AE%B8%E5%BE%AA%E7%8E%AF%E4%BE%9D%E8%B5%96%EF%BC%89)

[4.4.6.4 回顾doGetBean()：getBean()的核心逻辑处理方法](#4.3.5.4%20%E5%9B%9E%E9%A1%BEdoGetBean%28%29%EF%BC%9AgetBean%28%29%E7%9A%84%E6%A0%B8%E5%BF%83%E9%80%BB%E8%BE%91%E5%A4%84%E7%90%86%E6%96%B9%E6%B3%95)

[4.5 doCreateBean的其他逻辑](#4.4%C2%A0doCreateBean%E7%9A%84%E5%85%B6%E4%BB%96%E9%80%BB%E8%BE%91)

--

## 一、概念准备 

### 1.1 循环依赖

**Spring循环依赖：**在Spring应用程序中两个或多个Bean彼此之间存在直接或间接的依赖关系，并且这种依赖关系形成了一个循环。

简而言之，循环依赖就是Bean A注入了Bean B，同时Bean B注入了Bean A，那么这两个Bean就形成了一个依赖关系。

**举例：**

举个例子，以下代码中，AService和BService就形成了一个循环依赖关系：

AService注入BService： 

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/15
 * @Description: AService
 * @Version: 1.0
 */
@Component
public class AService {
    /**
     * 注入BService
     */
    @Resource
    private BService bService;
}
```

 BService注入AService：

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/15
 * @Description: BService
 * @Version: 1.0
 */
@Component
public class BService {
    /**
     * 注入AService
     */
    @Resource
    private AService aService;
}
```

### 1.2 Bean的生命周期

> **源码解析：**
> 
> [Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/137231482?spm=1001.2014.3001.5501 "Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客")

**Bean的生命周期：**指从Bean的创建到销毁的整个过程，主要包括Bean的创建、初始化、使用和销毁等阶段。

**生命周期的详细阶段：** 

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

## 二、环境准备

### 2.1 代码准备

准备循环依赖所需的代码：

 AService注入BService： 

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/15
 * @Description: AService
 * @Version: 1.0
 */
@Component
public class AService {
    /**
     * 注入BService
     */
    @Resource
    private BService bService;
}
```

 BService注入AService：

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/15
 * @Description: BService
 * @Version: 1.0
 */
@Component
public class BService {
    /**
     * 注入AService
     */
    @Resource
    private AService aService;
}
```

测试类获取Bean

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/20
 * @Description: 测试类：循环依赖
 * @Version: 1.0
 */
public class Test {
    public static void main(String[] args) {
        // 1.获取Spring容器，加载配置类
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        // 2.从容器中获取AService对象
        AService aService = context.getBean("AService", AService.class);
    }
}
```

### 2.2 如何给Spring源码添加注释？

当我们进行debug时候，想要给Spring源码加注释，而源码都在项目引的依赖的jar包里，无法直接加注释，这就需要采取以下两种方法。

#### 2.2.1 方法一：IDEA插件Private Notes

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

#### 2.2.2 方法二（推荐）：覆盖类（基于双亲委派模型）

> **类加载机制和双亲委派模型：**
> 
> [Java的类是怎样在虚拟机中加载的？详细阐述JVM的加载、验证和解析过程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/135250030 "Java的类是怎样在虚拟机中加载的？详细阐述JVM的加载、验证和解析过程-CSDN博客")

双亲委派模型这里不再过多赘述，详情看上面文章。

基于双亲委派模型，我们可以在本地创建一个与原始类路径、全限定名完全一致的类，就可以实现对原类的覆盖，代码debug时，也会进入我们覆盖的类，而不是原类：

例如我们覆盖AbstractAutowireCapableBeanFactory类，代码内容也完全拷贝过来，仅修改doCreateBean()方法，加上断点，debug可以发现断点进了我们覆盖的类：

![](https://i-blog.csdnimg.cn/blog_migrate/f5a072ed8d1f0df33732916cdec55658.png)

![](https://i-blog.csdnimg.cn/blog_migrate/e62291e2c39a368483932eec2b1270c8.png)

## 三、三级缓存介绍

Spring通过三级缓存解决了循环依赖问题。

### 3.1 简介

**三级缓存：** 

在Spring Bean的生命周期中，"三级缓存"用于解决循环依赖问题。当Spring容器创建Bean时，会将Bean的实例放置到三级缓存中，以确保在解决循环依赖问题时能够正确地获取已经创建的Bean实例。

-   **singletonObjects（单例池）：**缓存的是已经经历了完整生命周期的bean对象。
-   **earlySingletonObjects：**缓存未经过完整生命周期的bean，也就是提前代理对象。用于循环依赖时，直接从二级缓存找提前代理对象。
-   **singletonFactories：**缓存的是一个Lambda表达式，参数包括原始对象，执行结果是提前代理对象。在Bean实例化后立刻存Lambda表达式到三级缓存里。发生循环依赖且二级缓存找不到提前代理对象时，会获取并执行Lambda表达式，将生成的提前代理对象先存入二级缓存再填充属性。

### 3.2 源码位置：DefaultSingletonBeanRegistry类

三级缓存在DefaultSingletonBeanRegistry类中声明，格式是三个Map：

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

![](https://i-blog.csdnimg.cn/blog_migrate/fc564f4e6c3cb62378aaf4a1dde161e1.png)

![](https://i-blog.csdnimg.cn/blog_migrate/d1e662778fccadf267c843bd77209a05.png)

> **DefaultSingletonBeanRegistry类：**负责注册、获取、缓存、销毁单例 bean。
> 
> **核心方法：**
> 
> -   **注册单例 bean：**在容器启动时，将单例 bean 注册到注册表中。
>     -   **registerSingleton(String beanName, Object singletonObject)**：将给定的单例对象注册到单例 bean 注册表中。
> -   **获取单例 bean：**根据 bean 的名称从注册表中获取对应的单例 bean 实例。
>     -   **getSingleton(String beanName)**：根据给定的 bean 名称从注册表中获取对应的单例 bean 实例。
> -   **缓存单例 bean：**在首次获取单例 bean 后，将其缓存以供后续使用，避免重复创建。
>     -   **containsSingleton(String beanName)**：检查注册表中是否包含指定名称的单例 bean。
> -   **销毁单例 bean：**在容器关闭时，销毁注册表中所有单例 bean 实例。
>     -   **destroySingletons()**：销毁注册表中所有单例 bean 的实例。

### **3.3 详解ObjectFactory**

#### 3.3.1 函数式接口回顾

函数式接口是Java 8的一个新特性。 

**函数式接口：**有且仅有一个抽象方法的接口。实际使用时，函数式接口是方法的形参，实参是Lambda表达式。

**注解：**@FunctionalInterface

**示例：**java.util包下的生产者接口Supplier

```java
package java.util.function;

/**
 * Represents a supplier of results.
 */
@FunctionalInterface
public interface Supplier<T> {

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```

**应用案例：**使用Supplier，获取数组中的最大值：

```java
/**
 * @Author: vince
 * @CreateTime: 2024/03/20
 * @Description: 测试类
 * @Version: 1.0
 */
public class Test {
    /**
     * 主方法
     * @param args 参数
     */
    public static void main(String[] args) {
        // 定义一个int数组
        int[] arr = {19, 50, 28, 37, 46};
        // 调用getMax方法，方法的形参是函数式接口（单方法接口），
        // 实参Lambda表达式（接口方法的逻辑，相当于创建了一个Supplier对象）
        // 返回值是Lambda表达式的返回值，sup.get()
        int maxValue = getMax(() -> {
            int max = arr[0];
            for (int i = 1; i < arr.length; i++) {
                if (arr[i] > max) {
                    max = arr[i];
                }
            }
            return max;
        });
        System.out.println(maxValue);
    }

    /**
     * 返回一个int数组中的最大值，具体的逻辑由实参Lambda表达式决定
     * @param sup 供应商
     * @return int 最大值
     */
    private static int getMax(Supplier<Integer> sup) {
        return sup.get();
    }
}
```

#### 3.3.2 **ObjectFactory**

**第三级缓存：** 

首先我们看第三级缓存，它的value是ObjectFactory接口

```java
    /**
     * 三级缓存，value是Lambda表达式（ObjectFactory是一个函数式接口）
     * 函数式接口可以把匿名内部类、lambda表达式作为参数传递到方法中
     */
    private final Map<String, ObjectFactory<?>> singletonFactories = new HashMap<>(16);
```

> **什么是ObjectFactory？**
> 
> ObjectFactory是一个函数式接口，因为它包含@FunctionalInterface注解。
> 
> 它只有一个getObject()方法，用于获取实参Lambda表达式生成的Bean对象。
> 
> ```java
> @FunctionalInterface
> public interface ObjectFactory<T> {
> 
> 	/**
> 	 * Return an instance (possibly shared or independent)
> 	 * of the object managed by this factory.
> 	 * @return the resulting instance
> 	 * @throws BeansException in case of creation errors
> 	 */
> 	T getObject() throws BeansException;
> 
> }
> ```
> 
> **使用示例：**
> 
> **将获取存储进三级缓存：**
> 
> 函数式接口是一般都是形参，可以把匿名内部类、lambda表达式作为实参传递到方法中，例如下面语句是三级缓存实参示例：
> 
> ```java
> singletonFactories.put("AService",()-> getEarlyBeanReference(beanName,mbd,AService);
> ```
> 
> 这个语句中，实参“()-> getEarlyBeanReference(beanName,mbd,AService)”是一个Lambda表达式，它指定了ObjectFactory的getObject()方法的具体逻辑，是调用getEarlyBeanReference()方法。
> 
> 以后如果根据Bean名从三级缓存Map中取出这个Lambda表达式（实际是ObjectFactory类型），调用它的get()方法，将执行aop并生成AService的代理对象。

## 四、三级缓存解决循环依赖

### 4.0 核心流程简化版

**AService这个Bean的创建过程：**

1.  推断和实例化；
2.  存入三级缓存；
3.  属性填充BService，BService创建流程：
    1.  推断和实例化
    2.  存入三级缓存
    3.  属性填充AService
        1.  单例池找
        2.  判断循环依赖
        3.  二级缓存找
        4.  三级缓存找到，生成提前代理对象、存二级缓存
    4.  执行三级缓存
    5.  存入单例池
4.  AOP包裹初始化
5.  存入单例池

**解释：** **AService创建过程：**

-   **推断和实例化：**推断构造方法，实例化AService原始对象；
-   **存入三级缓存：**生成Lambda表达式，并放入三级缓存。Lambda表达式参数包括原始对象，以后如果执行这个Lambda表达式，将执行aop并生成AService代理对象；singletonFactories.put('AService',()-> getEarlyBeanReference(beanName，mbd，AService普通对象)
-   **属性填充BService：**去一级缓存、二级缓存找BService；如果没找到，则创建BService对象。**BService创建流程：**
    -   **推断和实例化：**推断构造方法和实例化BService原始对象；
    -   **存入三级缓存：**基于原始对象生成BService的Lambda表达式，并放入三级缓存。以后如果根据Bean名从三级缓存Map中取出这个Lambda表达式（实际是ObjectFactory类型），调用它的get()方法，将执行aop并生成AService的代理对象。
    -   **属性填充AService：**基于反射给AService属性填充AService代理对象；
        -   **单例池找：**先去一级缓存（单例池）找AService，若找到，则代表AService已经历完整生命周期，没有发生循环依赖。一级缓存中存的是完整生命周期的Bean。
        -   **判断循环依赖：**若没找到，就代表AService还未经过完整生命周期，要判断循环依赖。判断方法是在creattingSet<>中寻找AService，若找到则说明AService正在创建中，发生了循环依赖。
        -   **二级缓存找：**从二级缓存中找AService。二级缓存是earlySingletonObjects，存的就是未经历完整生命周期、提前aop的Bean。
        -   **三级缓存找到，生成提前代理对象、存二级缓存：**若没找到，就执行三级缓存AService的Lambda表达式，生成AService提前代理对象，将其存入二级缓存并返回；
    -   **执行三级缓存：**执行三级缓存BService的Lambda表达式，得到BService代理对象；
    -   **存入单例池**：BService代理对象放入一级缓存；
-   **AOP包裹初始化：**执行BeanPostProcessor的postProcessBeforeInitialization()方法；执行**初始化方法：**Bean重写InitializingBean接口的afterPropertiesSet()；执行BeanPostProcessor的postProcessAfterInitialization()方法
-   **存入单例池**：AService代理对象放入一级缓存；

### 4.1 前置流程

#### 4.1.1 方法调用链：getBean() **\-> doGetBean() ->** getSingleton() -> **createBean() -> doC**reateBean()

> 我们正常加载Spring容器，需要使用应用容器上下文加载配置类：
> 
> ```java
> /**
>  * @Author: vince
>  * @CreateTime: 2024/03/20
>  * @Description: 测试类：循环依赖
>  * @Version: 1.0
>  */
> public class Test {
>     public static void main(String[] args) {
>         // 1.注解方式启动IOC容器，加载配置类
>         ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
>         // 2.调用TestService的test()方法
>         TestService testService = context.getBean(TestService.class, "testService");
>         testService.test();
>     }
> }
> ```

AnnotationConfigApplicationContext的构造方法会调用this.refresh();，它会调用finishBeanFactoryInitialization()方法初始化所有单例bean，然后调用preInstantiateSingletons()方法，它调用了getBean()。 

> 这个调用链此处不再累述，详细参考下文：
> 
> [Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/137231482 "Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客")

这个getBean()方法将是Bean生命周期的主要方法。

**getBean():**

在Bean的生命周期中，主要有以下方法的调用：

![](https://i-blog.csdnimg.cn/blog_migrate/fadcced1d45e1ce04241e41175257c52.png)

-   **getBean()：**
    -   **作用：**根据Bean名称获取Bean
    -   **所属类：**AbstractBeanFactory类：即抽象BeanFactory基类，它实现了BeanFactory接口，用于管理 BeanDefinition，并对Bean 进行创建、获取、销毁等操作。
    -   它调用了doGetBean()方法
-   **doGetBean()方法：**
    -   **作用：**getBean()的核心逻辑处理方法
    -   **所属类：**AbstractBeanFactory类：抽象BeanFactory基类。
    -   它调用了getSingleton()方法
-   **getSingleton()方法：**
    -   **作用：**获取单例Bean
    -   **所属类：**DefaultSingletonBeanRegistry类：用于注册、获取、缓存、销毁单例 bean
    -   它调用了createBean()方法
-   **createBean()方法：**
    -   **作用：**创建Bean
    -   **所属类：**AbstractAutowireCapableBeanFactory类：继承了AbstractBeanFactory类，提供了Bean初始化和依赖注入的实现。
    -   它调用了doCreateBean()方法
-   **doCreateBean()方法：**创建Bean的核心逻辑处理方法
    -   **作用：**创建Bean的核心逻辑处理方法
    -   **所属类：**AbstractAutowireCapableBeanFactory类：用于Bean初始化和依赖注入
    -   它调用了addSingletonFactory()方法，将刚创建的bean放入第三级缓存中（第三级缓存singleFactories(key是beanName，value是ObjectFactory)）

#### 4.1.2 详解**doCreateBean()方法**

> 具体参考下文的2.6小节， doCreateBean()方法：创建Bean的核心逻辑处理方法
> 
> [Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/137231482 "Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客")

### 4.2 推断并实例化Bean

#### 4.2.1 核心流程 

1.  **判断单例：**创建一个BeanWrapper，如果是单例，则取出缓存赋值给它，并清除缓存
2.  **wrapper为空时实例化Bean：**调用createBeanInstance()方法，默认用无参构造方法实例化Bean，赋值给wrapper

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory

>  AbstractAutowireCapableBeanFactory是上面定义三级缓存的类DefaultSingletonBeanRegistry的子类，用于bean 初始化和自动装配（使用三级缓存解决了循环依赖），核心方法是autowireBean()、createBean()、doCreateBean()。
> 
> **详见下文2.5.2：**
> 
> [Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/137231482 "Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客")

```java
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
```

上面代码中核心代码是下面一行，调用调用createBeanInstance()方法，推断和实例化Bean：

![](https://i-blog.csdnimg.cn/blog_migrate/e7e31aa47c11c28c4f6c8d35394042e6.png)

#### 4.2.2 详解createBeanInstance()：推断构造方法并实例化Bean

上面doCreateBean()方法的第2步，如果从缓存中没取到BeanWrapper（Bean包装器，用于获取Bean实例、Class对象和属性），则执行createBeanInstance()创建Bean实例。

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

### 4.3 存入第三级缓存 

#### 4.3.1 概述 

在上面doCreateBean()的第四步——"依赖处理"阶段，调用了下面这一行代码，将实例化后的Bean存入三级缓存，key是beanName，value是ObjectFactory（形参是这个函数式接口，实参是Lambda表达式）：

```java
addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, bean));

```

![](https://i-blog.csdnimg.cn/blog_migrate/c7a1ab5ca5c9bf66de6ffb4988ba5b78.png)

实参“()-> getEarlyBeanReference(beanName,mbd,AService)”是一个Lambda表达式，它指定了ObjectFactory的getObject()方法的具体逻辑，是调用getEarlyBeanReference()方法。

以后如果根据Bean名从三级缓存Map中取出这个Lambda表达式（实际是ObjectFactory类型），调用它的get()方法，将执行aop并生成AService的代理对象。

#### 4.3.2 addSingletonFactory()：存入第三级缓存

![](https://i-blog.csdnimg.cn/blog_migrate/e1bd0a0a13a689144d15a9e9aa61e8a7.png)

**核心逻辑：**

-   **存入三级缓存：**如果一级缓存里没有该Bean，就放入三级缓存、移除二级缓存、添加到已注册Bean集合；如果一级缓存有该Bean，就代表这个Bean被加载过，无需操作

**具体代码：** 

org.springframework.beans.factory.support.DefaultSingletonBeanRegistry 

```java
    /**
     * 为指定的 bean 名称的Bean，添加到第三级缓存。
     *
     * @param beanName        bean 的名称
     * @param singletonFactory bean 的单例工厂
     * @throws IllegalArgumentException 如果单例工厂为 {@code null}
     */
    protected void addSingletonFactory(String beanName, ObjectFactory<?> singletonFactory) {
        Assert.notNull(singletonFactory, "Singleton factory must not be null");
        synchronized (this.singletonObjects) {
            // 1.如果一级缓存里没有这个Bean，就放入三级缓存、移除二级缓存；如果有就代表这个Bean被加载过，无需操作
            if (!this.singletonObjects.containsKey(beanName)) {
                // 放入三级缓存
                this.singletonFactories.put(beanName, singletonFactory);
                // 从二级缓存移除
                this.earlySingletonObjects.remove(beanName);
                // 添加到已注册单例的集合中
                this.registeredSingletons.add(beanName);
            }
        }
    }
```

#### 4.3.3 getEarlyBeanReference()：生成提前代理对象

![](https://i-blog.csdnimg.cn/blog_migrate/5ed9a56dcc7e69acc2efb35a0445387f.png)

**核心逻辑：**

-   **生成提前代理对象：**执行Lambda表达式，遍历所有后置处理器BeanPostProcessor，生产提前代理对象。因为这个对象还不是经历完整生命周期的Bean，还没有被IOC容器管理，只是用于解决循环依赖问题，所以称他为“提前代理对象”。

**具体代码：**  

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory 

```java
    /**
     * 获取指定 bean 的提前代理对象，通常用于解决循环引用的目的。
     *
     * @param beanName bean 的名称（用于错误处理目的）
     * @param mbd      bean 的合并后的 BeanDefinition
     * @param bean     原始的 bean 实例
     * @return 要暴露为 bean 引用的对象
     */
    protected Object getEarlyBeanReference(String beanName, RootBeanDefinition mbd, Object bean) {
        // 默认情况下，暴露对象(即提前代理对象)为原始的 bean 实例
        Object exposedObject = bean;
        // 遍历所有后置处理器BeanPostProcessor，增强暴露对象
        if (!mbd.isSynthetic() && hasInstantiationAwareBeanPostProcessors()) {
            // 遍历所有 BeanPostProcessor
            for (SmartInstantiationAwareBeanPostProcessor bp : getBeanPostProcessorCache().smartInstantiationAware) {
                exposedObject = bp.getEarlyBeanReference(exposedObject, beanName);
            }
        }
        return exposedObject;
    }
```

### 4.4 属性填充：解决循环依赖在这一步完成

#### 4.4.1 概述

Bean创建过程的核心方法doCreateBean()，第5步是依赖填充，将当前Bean注入的各个包含@Value,@Autowired,@Resource等注解的属性进行填充，这些注入的Bean可能还没有初始化，也可能初始化过并且它们的属性也包含当前Bean，这就产生了循环依赖，这个步骤使用三级缓存解决了循环依赖。

```java
            // 5.填充属性（DI依赖注入发生在此步骤）
            // 对bean进行填充，将各个属性值注入，其中可能存在依赖于其他bean的属性,会递归初始化
            populateBean(beanName, mbd, instanceWrapper);
```

![](https://i-blog.csdnimg.cn/blog_migrate/e2c12abd3238f1513cbeed5444ff99df.png)

#### 4.4.2 populateBean()：属性填充

**核心流程：**

1.  **执行所有后置处理器（实例化后）：**判断当前Bean是否实现了后置处理器InstantiationAwareBeanPostProcessor接口，如果实现了，则执行postProcessPropertyValues()方法，这个方法专门在Bean的属性注入之前调用；
2.  **自动装配：**判断根据名称注入，还是按类型自动注入，然后调用autowireByName()或autowireByType()注入；
3.  **依赖检查：**如果依赖注入后的属性值为空，并且没有过滤需要进行依赖检查的 PropertyDescriptor 集合，则过滤并检查；
4.  **将属性应用到bean中：**对属性值解析和转换，确保属性值能够正确地应用到 Bean 实例中；

```java
/**
 * 属性填充方法，给定一个bean名称，根Bean定义和Bean包装器，为Bean设置属性值。
 *
 * @param beanName  bean的名称
 * @param mbd       bean的根Bean定义
 * @param bw        bean的Bean包装器
 */
protected void populateBean(String beanName, RootBeanDefinition mbd, @Nullable BeanWrapper bw) {
        // 空值校验
        if (bw == null) {
            if (mbd.hasPropertyValues()) {
                throw new BeanCreationException(
                        mbd.getResourceDescription(), beanName, "Cannot apply property values to null instance");
            }
            else {
                // Skip property population phase for null instance.
                return;
            }
        }
        /**
         * 1.执行属性注入前后置处理器
         * 这里调用了 InstantiationAwareBeanPostProcessor.postProcessAfterInstantiation方法
         * 给InstantiationAwareBeanPostProcessor最后一次机会在属性设置前来改变bean
         * 注意：如果实现这个类并且在postProcessAfterInstantiation()返回 false 可以导致其他实例无法注入
         */
        if (!mbd.isSynthetic() && hasInstantiationAwareBeanPostProcessors()) {
            for (BeanPostProcessor bp : getBeanPostProcessors()) {
                if (bp instanceof InstantiationAwareBeanPostProcessor) {
                    InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
                    if (!ibp.postProcessAfterInstantiation(bw.getWrappedInstance(), beanName)) {
                        return;
                    }
                }
            }
        }
        PropertyValues pvs = (mbd.hasPropertyValues() ? mbd.getPropertyValues() : null);
        int resolvedAutowireMode = mbd.getResolvedAutowireMode();
        // 2.按名或类型自动装配：
        // 根据名称或类型自动注入，从Spring2.5开始，开始支持使用注解（@Autowired）来自动装配Bean的属性
        if (resolvedAutowireMode == AUTOWIRE_BY_NAME || resolvedAutowireMode == AUTOWIRE_BY_TYPE) {
            MutablePropertyValues newPvs = new MutablePropertyValues(pvs);
            // Add property values based on autowire by name if applicable.
            if (resolvedAutowireMode == AUTOWIRE_BY_NAME) {
                // 名称注入
                autowireByName(beanName, mbd, bw, newPvs);
            }
            // Add property values based on autowire by type if applicable.
            if (resolvedAutowireMode == AUTOWIRE_BY_TYPE) {
                // 类型注入
                autowireByType(beanName, mbd, bw, newPvs);
            }
            pvs = newPvs;
        }
        boolean hasInstAwareBpps = hasInstantiationAwareBeanPostProcessors();
        // 3.依赖检查
        boolean needsDepCheck = (mbd.getDependencyCheck() != AbstractBeanDefinition.DEPENDENCY_CHECK_NONE);
        PropertyDescriptor[] filteredPds = null;
        if (hasInstAwareBpps) {
            if (pvs == null) {
                pvs = mbd.getPropertyValues();
            }
            for (BeanPostProcessor bp : getBeanPostProcessors()) {
                // 对于每一个后置处理器，如果是 InstantiationAwareBeanPostProcessor 的实现类，则调用其 postProcessProperties 方法来进行依赖注入过程。
                if (bp instanceof InstantiationAwareBeanPostProcessor) {
                    InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
                    // 依赖注入过程
                    PropertyValues pvsToUse = ibp.postProcessProperties(pvs, bw.getWrappedInstance(), beanName);
                    if (pvsToUse == null) {
                        if (filteredPds == null) {
                            // 过滤出需要进行依赖检查的PropertyDescriptor集合，用于：
                            // 1、若存在InstantiationAwareBeanPostProcessor类型的后置处理器，
                            // 则各属性调用postProcessPropertyValues 方法（在Bean的属性注入之前调用），这些属性是由上述的过滤方法过滤得到；
                            // 2、后续检查需要设置值的属性是否已经初始化；作用也是用于筛选需要处理的属性，个人感觉这部分使用是扩展和辅助检查，更重要的是“第一处”中的使用。
                            filteredPds = filterPropertyDescriptorsForDependencyCheck(bw, mbd.allowCaching);
                        }
                        // 老版本用这个方式去注入
                        pvsToUse = ibp.postProcessPropertyValues(pvs, filteredPds, bw.getWrappedInstance(), beanName);
                        if (pvsToUse == null) {
                            return;
                        }
                    }
                    pvs = pvsToUse;
                }
            }
        }
        if (needsDepCheck) {
            if (filteredPds == null) {


                filteredPds = filterPropertyDescriptorsForDependencyCheck(bw, mbd.allowCaching);
            }
            // 依赖检查，对应 depends-on 属性，3.0 已弃用，这里不在分析
            checkDependencies(beanName, mbd, filteredPds, pvs);
        }
        if (pvs != null) {
            // 4.将属性应用到bean中：
            // 对属性值解析和转换，确保属性值能够正确地应用到 Bean 实例中；
            applyPropertyValues(beanName, mbd, bw, pvs);
        }
    }
```

#### 4.4.3 applyPropertyValues()：解析、转换所有属性

上面populateBean()方法第四步调用了 applyPropertyValues()方法，这个方法主要作用是将所有属性统一注册为Bean。它遍历所有属性并解析加到深拷贝列表，解析完所有属性后应用到bean。为了不影响到BeanDefinition的属性集合才使用深拷贝。

**核心逻辑：**

1.  **非空校验：**如果属性值列表是空的，结束注入流程；
2.  **判断属性值列表的类型：**将转换过的属性赋值到BeanWrapper的对应属性中，然后转为List集合，交给original；
3.  **遍历属性值列表：**如果每个属性转换过则直接加入深拷贝列表中，如果没转换过则将属性解析、转换后加入deepCopy；
4.  **将解析后的属性值列表赋值给BeanWrapper：**将解析后的深拷贝列表转为MutablePropertyValues类型后，set到BeanWrapper中；

**具体代码：**

org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory  

```java
    /**
     * 将所有属性统一注册为Bean：遍历所有属性并解析加到深拷贝列表，解析完所有属性后应用到bean。
     * 将给定的属性值应用到 Bean 实例中，同时解析任何运行时引用到此 Bean 工厂中的其他 Bean。
     * 在这个过程中，必须进行深度拷贝，以避免永久修改属性。
     *
     * @param beanName Bean的名称
     * @param mbd     Bean的定义信息
     * @param bw       BeanWrapper对象
     * @param pvs     属性值列表
     */
    protected void applyPropertyValues(String beanName, BeanDefinition mbd, BeanWrapper bw, PropertyValues pvs) {
        // 1.非空校验：如果属性值列表是空的，结束注入流程
        if (pvs.isEmpty()) {
            return;
        }

        if (System.getSecurityManager() != null && bw instanceof BeanWrapperImpl) {
            ((BeanWrapperImpl) bw).setSecurityContext(getAccessControlContext());
        }

        MutablePropertyValues mpvs = null;
        List<PropertyValue> original;
        // 2.判断属性值列表的类型：将转换过的属性赋值到BeanWrapper的对应属性中，然后转为List集合，交给original
        // 它可能是MutablePropertyValues类型的，也可能是PropertyValues类型的
        // 2.1 如果是MutablePropertyValues类型的，则将转换过的属性列表直接set到BeanWrapper中，然后将属性值列表转换为List集合
        // 2.2 如果不是，则将属性值列表转换为List集合
        if (pvs instanceof MutablePropertyValues) {
            mpvs = (MutablePropertyValues) pvs;
            // 如果属性值列表已经被转换过，将其直接set到BeanWrapper中
            if (mpvs.isConverted()) {
                // Shortcut: use the pre-converted values as-is.
                try {
                    bw.setPropertyValues(mpvs);
                    return;
                } catch (BeansException ex) {
                    throw new BeanCreationException(
                            mbd.getResourceDescription(), beanName, "Error setting property values", ex);
                }
            }
            original = mpvs.getPropertyValueList();
        } else {
            // 如果不是，则将属性值列表转换为List集合，交给original
            original = Arrays.asList(pvs.getPropertyValues());
        }
        // 获取自定义类型转换器
        TypeConverter converter = getCustomTypeConverter();
        if (converter == null) {
            converter = bw;
        }
        // 创建一个BeanDefinitionValueResolver对象
        // 用于解析属性值。该对象接收当前的 BeanDefinition 对象、bean 的名称、自定义的类型转换器作为参数
        BeanDefinitionValueResolver valueResolver = new BeanDefinitionValueResolver(this, beanName, mbd, converter);
        // 创建一个深拷贝列表deepCopy，用于存储解析转换过的属性
        List<PropertyValue> deepCopy = new ArrayList<>(original.size());
        boolean resolveNecessary = false;
        // 3.遍历属性值列表：如果每个属性转换过则直接加入deepCopy中，如果没转换过则将属性解析、转换后加入deepCopy
        // 每一个属性值都是一个键值对
        for (PropertyValue pv : original) {
            if (pv.isConverted()) {
                // 如果属性值已经被转换过，直接保存
                deepCopy.add(pv);
            } else {
                // 如果没转换过
                // 获取键值对
                String propertyName = pv.getName();
                Object originalValue = pv.getValue();
                // 判断该属性是否是自动装配的标记
                if (originalValue == AutowiredPropertyMarker.INSTANCE) {
                    // 获取该方法的写方法（setter方法）
                    Method writeMethod = bw.getPropertyDescriptor(propertyName).getWriteMethod();
                    // 非空校验这个写方法
                    if (writeMethod == null) {
                        throw new IllegalArgumentException("Autowire marker for property without write method: " + pv);
                    }
                    // 将属性值替换为一个新的DependencyDescriptor对象，该对象表示对属性的依赖描述
                    originalValue = new DependencyDescriptor(new MethodParameter(writeMethod, 0), true);
                }
                // 解析该对象的属性值
                Object resolvedValue = valueResolver.resolveValueIfNecessary(pv, originalValue);
                // 创建convertedValue，保存解析后的属性值，默认就是解析值
                Object convertedValue = resolvedValue;
                // 判断属性是否可转换，并且不是嵌套或索引属性。
                boolean convertible = bw.isWritableProperty(propertyName) &&
                        !PropertyAccessorUtils.isNestedOrIndexedProperty(propertyName);
                if (convertible) {
                    // 如果属性可转换，将解析后的属性值进行类型转换。
                    convertedValue = convertForProperty(resolvedValue, propertyName, bw, converter);
                }

                // 可能将转换后的值存储在合并的bean定义中，以避免对每个创建的bean实例进行重新转换。
                if (resolvedValue == originalValue) {
                    // 如果解析后的值与原值相同
                    if (convertible) {
                        // 如果该属性可转换
                        // 保存转换后的值进入pv
                        pv.setConvertedValue(convertedValue);
                    }
                    // 将pv存入深拷贝数组
                    deepCopy.add(pv);
                } else if (convertible && originalValue instanceof TypedStringValue &&
                        !((TypedStringValue) originalValue).isDynamic() &&
                        !(convertedValue instanceof Collection || ObjectUtils.isArray(convertedValue))) {
                    // 如果属性可转换且原始值是 TypedStringValue 类型且不是动态值，并且转换后的值不是集合或数组类型，
                    // 则保存转换后的属性值，保存到深拷贝列表
                    pv.setConvertedValue(convertedValue);
                    deepCopy.add(pv);
                } else {
                    // 标记需要解析，然后存到深拷贝列表
                    resolveNecessary = true;
                    deepCopy.add(new PropertyValue(pv, convertedValue));
                }
            }
        }
        // 如果mpvs不为空，且不需要解析，则标记为已转换
        if (mpvs != null && !resolveNecessary) {
            mpvs.setConverted();
        }

        // 4.将解析后的深拷贝列表set到BeanWrapper中
        try {
            bw.setPropertyValues(new MutablePropertyValues(deepCopy));
        } catch (BeansException ex) {
            throw new BeanCreationException(
                    mbd.getResourceDescription(), beanName, "Error setting property values", ex);
        }
    }
```

#### 4.4.4 resolveValueIfNecessary()：根据类型解析属性

##### 4.4.4.1 基本介绍

上面applyPropertyValues()方法调用了resolveValueIfNecessary()方法，该方法主要对当前属性的类型进行判断，根据实际的类型对属性进行解析。

又因为上面applyPropertyValues()方法调用本方式时，传参的属性是RuntimeBeanReference类型的，所以会执行下面逻辑，调用resolveReference()方法：

org.springframework.beans.factory.support.BeanDefinitionValueResolver

![](https://i-blog.csdnimg.cn/blog_migrate/64a9fe0b9bdfc815589097300de90270.png)

##### 4.4.4.2 BeanDefinitionValueResolver类： 解析Bean的属性

BeanDefinitionValueResolver类位于org.springframework.beans.factory.support包下，主要用于解析 Bean 定义中的属性值。

![](https://i-blog.csdnimg.cn/blog_migrate/0a142215f9238c5b1c4f40aa8ea6d2a4.png)

**具体功能：**

1.  解析属性值是否需要引用其他 Bean 或 Bean 名称，并进行相应的解析。对应方法resolveValueIfNecessary()、resolveReference();
2.  解析包含的内部 Bean。对应方法resolveInnerBean()；
3.  解析数组、列表、集合、映射、属性等特殊类型的属性值。对应方法resolveManagedList()等；
4.  将属性值转换为目标类型。对应方法resolveTargetType()等；

#### 4.4.5 resolveReference()：调用getBean()解析属性为Bean

上面 resolveValueIfNecessary()方法调用了resolveReference()方法，对属性进行解析。

本方法主要调用了getBean()方法，注册属性为Bean，然后获取到这个Bean。

**核心流程：**

1.  **获取Bean名：**获取运行时 Bean 引用的名称。
2.  **获取Bean：**根据引用的名称，调用 `getBean()` 方法从 BeanFactory 中获取对应的 Bean 实例。
3.  **空值校验、异常处理：**如果没有获取到Bean返回空，如果有异常，加上错误信息并抛出异常；

**详细流程：**

org.springframework.beans.factory.support.BeanDefinitionValueResolver 

```java
/**
 * 在该方法中，会为当前初始化bean主要为属性注入另外一个bean，调用getBean()方法获取需要注入的bean，最终注入到属性中
 */
private Object resolveReference(Object argName, RuntimeBeanReference ref) {
	try {
		Object bean;
		String refName = ref.getBeanName();
		refName = String.valueOf(doEvaluate(refName));
		if (ref.isToParent()) {
			if (this.beanFactory.getParentBeanFactory() == null) {
				throw new BeanCreationException(
						this.beanDefinition.getResourceDescription(), this.beanName,
						"Can't resolve reference to bean '" + refName +
								"' in parent factory: no parent factory available");
			}
			bean = this.beanFactory.getParentBeanFactory().getBean(refName);
		}
		else {
		    // 当前初始化bean主要为属性注入另外一个bean，调用getBean()方法获取需要注入的bean，最终注入到属性中
			bean = this.beanFactory.getBean(refName);
			this.beanFactory.registerDependentBean(refName, this.beanName);
		}
		if (bean instanceof NullBean) {
			bean = null;
		}
		return bean;
	}
	catch (BeansException ex) {
		throw new BeanCreationException(
				this.beanDefinition.getResourceDescription(), this.beanName,
				"Cannot resolve reference to bean '" + ref.getBeanName() + "' while setting " + argName, ex);
	}
}
```

#### 4.4.6 属性获取Bean流程：getBean() -> doGetBean()

##### 4.4.6.1 直接从缓存中获取到AService

上面方法解析Bean的时候，调用了getBean()方法。

你可能在想，这不是无限套娃了吗？先调用getBean()获取AService，获取过程中，又调用getBean()获取属性BService，然后又调用getBean()获取AService属性，无限循环。

> **详细Bean加载流程参考：**
> 
> [Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/137231482 "Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客")

事实不是这样的。

这次执行doGetBean()的逻辑跟之前有所不同，主要原因是AService之前已经存入到第三级缓存中了，所以可以直接取到。

这是第二次获取AService了：

![](https://i-blog.csdnimg.cn/blog_migrate/8c5c7f569b475d451ff77ed4af9d328f.png)

> 之前第一次获取AService的时候，上面getSingleton(String beanName)是没获取到数据的，是在doGetBean()后面执行getSingleton(String beanName, ObjectFactory<?> singletonFactory)，这次就不再执行了，也就**不再执行createBean()了：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8db8784d87b5cdb5bffd400c2d23349d.png)

##### 4.4.6.2 getSingleton(beanName) ：从缓存中获取单例Bean

本方法只有一行。

**核心逻辑：**

-   调用getSingleton(String beanName, boolean allowEarlyReference)方法，传参true，代表允许循环依赖

```java
	@Override
	@Nullable
	public Object getSingleton(String beanName) {
		return getSingleton(beanName, true);
	}
```

##### 4.4.6.3 getSingleton(beanName,true)：从缓存中获取单例Bean（是否允许循环依赖）

**核心逻辑：**

1.  尝试从一级缓存中获取；
2.  **判断循环依赖：**如果从一级缓存没取到，并且发生了循环依赖，则加锁执行下面逻辑：
3.  尝试从二级缓存中获取；
4.  **从三级缓存中获取：**如果获取到则执行Lambda表达式，生成提前代理对象，然后将其从三级缓存删除、存入二级缓存并返回；

> **提前代理对象：**
> 
> 提前代理对象是这一步执行第三级缓存的value，即一个Lambda表达式生成的（具体的实参参考上文的“存入第三级缓存”），因为这个对象还不是经历完整生命周期的Bean，还没有被IOC容器管理，只是用于解决循环依赖问题，所以称他为“提前代理对象”。

**详细代码：**

```java
   protected Object getSingleton(String beanName, boolean allowEarlyReference) { 
   // 从一级缓存获取BeanName对应的单例对象 
  Object singletonObject = this.singletonObjects.get(beanName); 
   // 如果没有获取到，但是当前 BeanName对应的单例对象又处于创建中 
  if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) { 
   synchronized (this.singletonObjects) { 
        // 从二级缓存中获取当前BeanName对应的单例对象 
    singletonObject = this.earlySingletonObjects.get(beanName); 
        // 二级缓存中没有，但是allowEarlyReference为true，在doCreateBean方法中已经设置，所以这里为true 
    if (singletonObject == null && allowEarlyReference) { 
          // 从三级缓存中获取 
     ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName); 
     if (singletonFactory != null) { 
            // 这里就是三级缓存函数方法，同过Factory创建一个单例对象 
      singletonObject = singletonFactory.getObject(); 
            // 添加到二级缓存中，半成品对象 
      this.earlySingletonObjects.put(beanName, singletonObject); 
            // 同时删除三级缓存 
      this.singletonFactories.remove(beanName); 
     } 
    } 
   } 
  } 
   // 返回当前半成品对象 
  return singletonObject; 
 } 
```

##### 4.4.6.4 回顾doGetBean()：getBean()的核心逻辑处理方法

> **详细参考下文：** [Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/137231482 "Spring框架中Bean是如何加载的？从底层源码入手，详细解读Bean的创建流程-CSDN博客")

getBean()只有一行代码，调用了doGetBean()一个方法。

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

### 4.5 doCreateBean的其他逻辑

在属性填充后，AService将执行doCreateBean()剩余的逻辑，即AOP增强、校验依赖注册、注册销毁Bean，也就是下面流程中的6，7，8，执行完后，这个Bean以及它的依赖都已经注册完毕：

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

**详细解析：**

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