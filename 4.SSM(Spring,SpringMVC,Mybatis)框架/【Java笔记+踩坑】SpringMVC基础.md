>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1，SpringMVC简介](#1-springmvc-)

[1.1 三层架构、MVC、异步回顾](#1.1%20%E4%B8%89%E5%B1%82%E6%9E%B6%E6%9E%84%E3%80%81MVC%E3%80%81%E5%BC%82%E6%AD%A5%E5%9B%9E%E9%A1%BE)

[1.2 SpringMVC概述](#1.2%20SpringMVC%E6%A6%82%E8%BF%B0)

[1.3 所有SpringMvc注解整理](#1.3%20%E6%89%80%E6%9C%89SpringMvc%E6%B3%A8%E8%A7%A3%E6%95%B4%E7%90%86)

[2，SpringMVC入门案例](#2-springmvc-)

[2.1 需求分析](#2-1-)

[2.2 代码实现](#2-2-)

[知识点：@Controller@RequestMapping@ResponseBody](#%E7%9F%A5%E8%AF%86%E7%82%B9%EF%BC%9A%40Controller%40RequestMapping%40ResponseBody)

[2.3 案例总结](#2-3-)

[2.4 工作流程解析](#2-4-)

[2.4.1 启动服务器初始化过程](#2-4-1-)

[2.4.2 单次请求过程](#2-4-2-)

[2.5 bean加载控制，spring排除加载表现层的bean](#2-5-bean-)

[2.5.1 问题分析](#2-5-1-)

[2.5.2 思路分析](#2-5-2-)

[2.5.3 环境准备](#2-5-4-)

[2.5.5 设置bean加载控制](#2-5-5-bean-)

[知识点@ComponentScan的excludeFilters](#-1-componentscan)

[3，PostMan工具的使用](#3-postman-)

[3.1 PostMan简介](#3-1-postman-)

[3.2 PostMan安装](#3-2-postman-)

[3.3 PostMan使用](#3-3-postman-)

[3.3.1 创建WorkSpace工作空间](#3-3-1-workspace-)

[3.3.2 发送请求](#3-3-2-)

[3.3.3 保存当前请求](#3-3-3-)

[4，请求与响应](#4-)

[4.1 设置请求映射路径](#4-1-)

[4.1.1 环境准备](#4-1-1-)

[4.1.2 请求冲突问题分析](#4-1-2-)

[4.1.3 设置映射路径](#4-1-3-)

[4.2 普通请求参数传递入门](#4-2-)

[4.2.1 环境准备](#4-2-1-)

[4.2.2 请求参数传递和中文乱码解决](#4-2-2-)

[4.3 请求头的五种类型参数传递](#4-3-)

[4.3.1 普通请求参数，起别名，@RequestParam](#4-3-1-)

[4.3.2 POJO数据类型](#4-3-2-pojo-)

[4.3.3 嵌套POJO类型参数](#4-3-3-pojo-)

[4.3.4 数组类型参数](#4-3-4-)

[4.3.5 集合类型参数，@RequestParam](#4-3-5-)

[知识点@RequestParam](#-1-requestparam)

[4.4 请求体的JSON数据传输参数，@RequestBody](#4-4-json-)

[4.4.1 概述](#4.4.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[4.4.2 JSON普通数组，@EnableWebMvc](#json-)

[4.4.3 JSON对象数据](#4.1.3%20JSON%E5%AF%B9%E8%B1%A1%E6%95%B0%E6%8D%AE)

[4.4.4 JSON对象数组](#4.1.4%20JSON%E5%AF%B9%E8%B1%A1%E6%95%B0%E7%BB%84)

[知识点 @EnableWebMvc@RequestBody](#%E7%9F%A5%E8%AF%86%E7%82%B9%C2%A0%40EnableWebMvc%40RequestBody)

[4.4.5 @RequestBody与@RequestParam区别](#-requestbody-requestparam-)

[4.4.5 @RequestParam和@RequestPart的区别](#4.4.5%C2%A0%40RequestParam%E5%92%8C%40RequestPart%E7%9A%84%E5%8C%BA%E5%88%AB)

[4.5 日期类型参数传递@DateTimeFormat](#4-5-)

[4.5.1 具体代码](#4.5.1%20%E5%85%B7%E4%BD%93%E4%BB%A3%E7%A0%81)

[知识点@DateTimeFormat](#-1-datetimeformat)

[4.5.2 类型转换内部实现原理](#-)

[4.6 响应](#4-6-)

[4.6.1 环境准备，jackson-databind依赖](#4-6-1-)

[4.6.2 响应jsp页面\[了解\]](#4-6-2-)

[4.6.3 返回文本数据\[了解\]](#4-6-3-)

[4.6.4 响应JSON数据](#4-6-4-json-)

[知识点@ResponseBody](#-1-responsebody)

[5，Rest风格](#5-rest-)

[5.1 REST简介](#5-1-rest-)

[5.2 RESTful入门案例](#5-2-restful-)

[5.2.1 环境准备](#5-2-1-)

[5.2.2 思路分析](#5-2-2-)

[5.2.3 代码实现，@RequestMapping的method属性，@PathVariable](#5-2-3-restful-)

[5.2.4 目前学的参数占位符汇总](#5.2.4%20%E7%9B%AE%E5%89%8D%E5%AD%A6%E7%9A%84%E5%8F%82%E6%95%B0%E5%8D%A0%E4%BD%8D%E7%AC%A6%E6%B1%87%E6%80%BB)

[知识点@PathVariable](#-1-pathvariable)

[5.2.5 区别：@RequestBody、@RequestParam、@PathVariable](#%C2%A0%E5%8C%BA%E5%88%AB%EF%BC%9A%40RequestBody%E3%80%81%40RequestParam%E3%80%81%40PathVariable)

[5.3 RESTful优化，快速开发](#5-3-restful-)

[5.3.1 概述，@RestController，@GetMapping](#%C2%A0%E6%A6%82%E8%BF%B0%EF%BC%8C%40RestController) 

[知识点@RestController@GetMapping @PostMapping @PutMapping @DeleteMapping](#%E7%9F%A5%E8%AF%86%E7%82%B9%40RestController%40GetMapping%20%40PostMapping%20%40PutMapping%20%40DeleteMapping)

[5.4 RESTful案例](#5-4-restful-)

[5.4.1 需求分析](#5-4-1-)

[5.4.2 环境准备](#5-4-2-)

[5.4.2 后台接口开发](#5.4.2%20%E5%90%8E%E5%8F%B0%E6%8E%A5%E5%8F%A3%E5%BC%80%E5%8F%91)

[5.4.3 放行静态页面，WebMvcConfigurer配置类添加资源处理器](#5-4-3-)

--

## 1，SpringMVC简介

### 1.1 三层架构、MVC、异步回顾

**三层架构**

![](https://i-blog.csdnimg.cn/blog_migrate/b6ae895c69b4458b4031f9f4990307c0.png)

-   浏览器发送一个请求给后端服务器，后端服务器现在是使用Servlet来接收请求和数据
    
-   如果所有的处理都交给**Servlet**来处理的话，所有的东西都**耦合**在一起，对后期的维护和扩展极为不利
    
-   将**后端服务器Servlet拆分成三层**，分别是`web`、`service`和`dao`
    
    -   **web层（表现层）**主要由servlet来处理，负责页面**请求**和**数据的收集**以及**响应**结果给前端
    -   **service层（业务层）**主要负责**业务逻辑**的处理
    -   **dao层（数据访问层）**主要负责**数据**的增删改查操作
-   **servlet存在问题：**servlet处理请求和数据的时候，**一个servlet只能处理一个请求**

> **MVC模式是对三层架构中的web层的优化。** 

**MVC模式**

![](https://i-blog.csdnimg.cn/blog_migrate/a3f831089c39de8e3dba6345f14c1637.png)

-   **MVC设计模式：**针对**web层**进行了优化，采用了MVC设计模式，将其设计为控制器**`controller`、视图`view、`业务模型`Model`**
    -   **控制器**（例如serlvlet）用来**接收**浏览器发送过来的**请求**，**控制器调用模型**（例如JavaBean）来**获取数据**，比如从数据库查询数据；**控制器**获取到数据后再**交由视图**（例如JSP）进行**数据展示**。

**service**根据需要会**调用dao**对数据进行增删改查

**dao**把**数据处理**完后将结果交给service,service再交给controller

**控制器controller**根据需求**组装成Model和View**,Model和View组合起来**生成页面转发给前端浏览器。**这样做的好处就是controller可以处理多个请求，并对请求进行分发，执行不同的业务操作。

**异步取代同步**

随着互联网的发展，**MVC模式**因为是**同步调用**，性能慢慢的跟不是需求，所以**异步调用**慢慢的走到了前台，是现在比较流行的一种处理方式。

![](https://i-blog.csdnimg.cn/blog_migrate/f9c9359effda3dcf8b62ee94e919b919.png)

**vue异步调用的特点：** 

-   因为是**异步调用**，所以**后端不需要返回view视图**，将其去除。（回顾jsp就是Servlet响应到jsp页面展示；而vue是异步请求Servlet，通过JSON数据前后端交互的）
-   前端如果通过**异步调用**的方式进行交互，后台就需要将返回的数据转换成**json格式**进行返回

### 1.2 SpringMVC概述

**SpringMVC是隶属于Spring框架的一部**分，主要是用来进行**Web开发**，是**对Servlet进行了封装**。

springmvc功能和Servlet是一样的，只是更简洁。 

**SpringMVC主要负责的是：**

-   **controller**如何接收请求和数据
-   如何将请求和数据转发给业务层
-   如何将响应数据转换成json发回到前端

SpringMVC是处于**Web层的框架**，**主要作用：接收前端发过来的请求和数据然后经过处理并将处理的结果响应给前端**。

REST是一种软件架构风格，可以降低开发的复杂性，提高系统的可伸缩性，后期的应用也是非常广泛。

SSM整合是把咱们所学习的SpringMVC+Spring+Mybatis整合在一起来完成业务开发，是对我们所学习这三个框架的一个综合应用。

**学习目标:**

1.  **掌握基于SpringMVC获取请求参数和响应json数据操作**
2.  **熟练应用基于REST风格的请求路径设置与参数传递**
3.  能够根据实际业务建立前后端开发通信协议并进行实现
4.  **基于SSM整合技术开发任意业务模块功能**

介绍了这么多，对SpringMVC进行一个定义

-   SpringMVC是一种基于Java实现MVC模型的轻量级Web框架
    
-   优点
    
    -   使用简单、开发便捷(相比于Servlet)
    -   灵活性强
    
    这里所说的优点，就需要我们在使用的过程中慢慢体会。
    

### 1.3 所有SpringMvc注解整理

Controller 相关注解：

-   @Controller标注类为控制器，处理http请求。
-   @RequestMapping将请求路径映射到方法；
-   @RestController相当于@ResponseBody+@Controller；
-   @ResponseBody将方法返回的对象相映成JSON格式；
-   @RequestBody接收请求体JSON数据，并转为对象或对象数组。
-   @PathVariable获取请求路径中的数据；
-   @RequestParam根据value获取同名请求参数的值、获取集合类型参数；
-   @ControllerAdvice 统一处理异常；
-   @RestControllerAdvice注解Rest风格统一处理异常；
-   @ExceptionHandler 声明捕获异常类型；

## 2，SpringMVC入门案例

因为SpringMVC是一个Web框架，将来是要替换Servlet,所以先来回顾下以前Servlet是如何进行开发的?

1.创建web工程(Maven结构)

2.设置tomcat服务器，加载web工程(tomcat插件)

3.导入坐标(Servlet)

4.定义处理请求的功能类(UserServlet)

5.设置请求映射(配置映射关系)

SpringMVC的制作过程和上述流程几乎是一致的，具体的实现流程是什么?

1.创建web工程(Maven结构)

2.设置tomcat服务器，加载web工程(tomcat插件)

3.导入坐标(**SpringMVC**+Servlet)

4.定义处理请求的功能类(**UserController**)

5.**设置请求映射(配置映射关系)**

6.**将SpringMVC设定加载到Tomcat容器中**

### 2.1 需求分析

### 2.2 代码实现

**步骤1:创建Maven项目**

打开IDEA,创建一个新的web项目

![](https://i-blog.csdnimg.cn/blog_migrate/96ad00580ad22d7a1b71795bcca77335.png)

**步骤2:补全目录结构**

因为使用骨架创建的项目结构不完整，需要手动补全

![](https://i-blog.csdnimg.cn/blog_migrate/f35b3a37cca66589957b9372e8b35793.png)

**步骤3:导入jar包**

将pom.xml中多余的内容删除掉，再添加依赖spring-webmvc和javax.servlet-api

> **无需再导入spring-context，因为依赖spring-webmvc里包括了spring-context.**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.itheima</groupId>
  <artifactId>springmvc_01_quickstart</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <dependencies>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <configuration>
          <port>80</port>
          <path>/</path>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

> **回顾:servlet的坐标为什么需要添加`<scope>provided</scope>`?**
> 
> -   scope是maven中jar包依赖作用范围的描述，
> -   如果不设置默认是`compile`在在编译、运行、测试时均有效
> -   如果运行有效的话就会和tomcat中的servlet-api包发生冲突，导致启动报错
>     
> -   provided代表的是该包只在编译和测试的时候用，运行的时候无效直接使用tomcat中的，就避免冲突
>     

**步骤4:创建配置类**

```java
@Configuration
//扫描范围设为controller即可，因为springmvc容器只用管理表现层的bean即可，业务、数据层由spring管理
@ComponentScan("com.itheima.controller")
public class SpringMvcConfig {
}
```

**步骤5:创建Controller类**

```java
//设置springmvc的核心控制器bean
@Controller
public class UserController {
    //设置当前控制器方法请求访问路径
    @RequestMapping("/save")
    //@ResponseBody设置当前控制器方法响应内容为当前返回值，无需解析
    @ResponseBody
    public String save(){
        System.out.println("user save ...");
        //如果不加@ResponseBody，系统会根据返回值字符串寻找路径，例如return "index.jsp";会跳转到jsp页面
        //返回真正json只需要返回对象，在pom引入jackson，springmvcconfig配置类注解@@EnableWebMvc，下面注释的语句就是返回JSON数据
        //return new User("zhangsan",23);
        return "{'info':'springmvc'}";
    }
}
```

> -   当**方法上有@ReponseBody**注解后
>     -   方法的**返回值为字符串**，会将其作为**文本内容**直接**响应给前端**
>     -   方法的**返回值为对象**，会将对象**转换成JSON响应给前端**

**步骤6:使用Servlet容器配置类替换web.xml**

**方法一：复杂底层**

将web.xml删除，换成ServletContainersInitConfig，继承抽象转发Servlet初始化器类**AbstractDispatcherServletInitializer**，**alt+insert实现三个方法**。

```java
public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
    //创建Servlet容器时，加载springmvc的配置。将springmvc对应的bean并放入WebApplicationContext对象范围中。
    //最终返回web容器WebApplicationContext ，web容器就是springmvc最终体现的容器。ApplicationContext应用上下文，容器
    protected WebApplicationContext createServletApplicationContext() {
        //创建注解配置的web容器。使用AnnotationConfigWebApplicationContext，比前面Spring创建注解容器的类AnnotationConfigApplicationContext中间多了Web
        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        //加载springmvc的配置类字节码到web容器中，从而可以让web容器管理加载配置类管理的bean
        //因为AnnotationConfigWebApplicationContext类没有带参构造方法，所以要手动为容器加载指定配置类字节码文件
        ctx.register(SpringMvcConfig.class);
        return ctx;
    }

    //设置由springmvc拦截并处理的请求路径，即springmvc拦截哪些请求。
    //返回值String数组只有一个"/"，代表所有路径都由springmvc处理
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    //加载spring配置类，方法和加载springmvc方法相同，只是加载的配置类改成spring的配置文件
    //如果创建Servlet容器时需要加载非表现层的bean,使用当前方法进行，使用方式和createServletApplicationContext相同。
    protected WebApplicationContext createRootApplicationContext() {
      AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        ctx.register(SpringConfig.class);
        return ctx;
    }
}
```

**方法二：简单快速**

**继承Abstract**AnnotationConfig**DispatcherServletInitializer** ，跟之前抽象类外表区别是中间多了AnnotationConfig

```java
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
 
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }
 
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }
 
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
}
```

**步骤7:配置Tomcat环境**

我这里用的是Tomcat9，因为我Servlet和springmvc依赖都导入了最新的，和Tomcat7不兼容。

**步骤8:启动运行项目**

![](https://i-blog.csdnimg.cn/blog_migrate/0a4c9266788048395c25c738b5f866eb.png)

**步骤9:浏览器访问**

浏览器输入`http://localhost/save`进行访问

![](https://i-blog.csdnimg.cn/blog_migrate/08627e25807d64435d8b8b6ec12296a5.png)

至此SpringMVC的入门案例就已经完成。

> **注意事项**
> 
> -   **SpringMVC是基于Spring的**，在pom.xml**只导入了`spring-webmvc`**jar包的原因是它会**自动依赖spring相关坐标**
> -   **AbstractDispatcherServletInitializer**类是SpringMVC提供的**快速初始化Web3.0容器**的抽象类
> -   AbstractDispatcherServletInitializer提供了**三个接口方法**供用户实现
>     -   **createServletApplicationContext**方法，创建Servlet容器时，加载SpringMVC对应的bean并放入WebApplicationContext对象范围中，而WebApplicationContext的作用范围为ServletContext范围，即整个web容器范围
>     -   **getServletMappings**方法，设定SpringMVC对应的请求映射路径，即SpringMVC拦截哪些请求
>     -   **createRootApplicationContext**方法，如果创建Servlet容器时需要加载非SpringMVC对应的bean,使用当前方法进行，使用方式和createServletApplicationContext相同。
>     -   createServletApplicationContext用来加载SpringMVC环境，createRootApplicationContext用来加载Spring环境

### 知识点：@Controller@RequestMapping@ResponseBody

**知识点1：@Controller**

| 名称 | @Controller |
| --- | --- |
| 类型 | 类注解 |
| 位置 | SpringMVC控制器类定义上方 |
| 作用 | 设定SpringMVC的核心控制器bean |

**知识点2：@RequestMapping**

| 名称 | @RequestMapping |
| --- | --- |
| 类型 | 类注解或方法注解 |
| 位置 | SpringMVC控制器类或方法定义上方 |
| 作用 | 设置当前控制器方法请求访问路径 |
| 相关属性 | value(默认)，请求访问路径 |

**知识点3：@ResponseBody**

| 名称 | @ResponseBody |
| --- | --- |
| 类型 | 类注解或方法注解 |
| 位置 | SpringMVC控制器类或方法定义上方 |
| 作用 | **设置当前控制器方法响应内容为当前返回值，无需解析** |

### 2.3 案例总结

-   一次性工作
    -   创建工程，设置服务器，加载工程
    -   导入坐标
    -   创建**web容器启动类**，**加载SpringMVC配置**，并设置SpringMVC**请求拦截路径**
    -   SpringMVC核心配置类（设置配置类，扫描controller包，加载Controller控制器bean）
-   多次工作
    -   定义处理请求的控制器类
    -   定义处理请求的控制器方法，并配置映射路径（@RequestMapping）与返回json数据（@ResponseBody）

### 2.4 工作流程解析

为了更好的使用SpringMVC,我们将**SpringMVC的使用过程**总共分**两个阶段**来分析，分别是**`启动服务器初始化过程`和`单次请求过程`**

**web容器、Servletcontext、webApplicationContext、UserController关系：** 

![](https://i-blog.csdnimg.cn/blog_migrate/011d6f0fc9c44fcc45aecde59c5ff855.png)

#### 2.4.1 启动服务器初始化过程

1.  服务器启动，执行**ServletContainersInitConfig**类，**初始化web容器**。功能类似于以前的web.xml
    
2.  执行**createServletApplicationContext**方法，创建了**WebApplicationContext**对象。该方法加载SpringMVC的配置类SpringMvcConfig来**初始化SpringMVC的容器**
    
3.  加载SpringMvcConfig配置类
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/630e488f80537fe1ce9fbfce64ee6b22.png)
    
4.  执行@**ComponentScan**加载对应的bean。扫描指定包及其子包下所有类上的注解，如Controller类上的@Controller注解
    
5.  加载**UserController**，每个@RequestMapping的名称对应一个具体的方法。此时就建立了 `/save` 和 save方法的对应关系
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/6f92b4bc7be316541a0f7d18940cee70.png)
    

6.执行**getServletMappings**方法，设定SpringMVC拦截请求的路径规则。`/`代表所拦截请求的路径规则，只有被拦截后才能交给SpringMVC来处理请求

![](https://i-blog.csdnimg.cn/blog_migrate/6a51923a0774de0a76097daf50ff8cff.png)

#### 2.4.2 单次请求过程

1.  发送请求`http://localhost/save`
2.  web容器发现该请求满足SpringMVC拦截规则，将请求交给SpringMVC处理
3.  解析请求路径/save
4.  由/save匹配执行对应的方法save(）
    -   上面的第五步已经将请求路径和方法建立了对应关系，通过/save就能找到对应的save方法
5.  **执行save**()
6.  检测到有@**ResponseBody**直接将save()方法的返回值作为响应体返回给请求方

### 2.5 bean加载控制，spring排除加载表现层的bean

#### 2.5.1 问题分析

**项目目录结构:**

![](https://i-blog.csdnimg.cn/blog_migrate/ca12aa5e033d699666e29172f4263d1b.png)

**各目录存放内容：** 

-   **config**目录存入的是配置类,写过的配置类有:
    
    -   ServletContainersInitConfig
    -   SpringConfig
    -   SpringMvcConfig
    -   JdbcConfig
    -   MybatisConfig
-   **controller**目录存放的是SpringMVC的controller类
-   **service**目录存放的是service接口和实现类
-   **dao**目录存放的是dao/Mapper接口

**问题：controller、service和dao这些类都需要被容器管理成bean对象**，那么到底是该让SpringMVC加载还是让Spring加载呢?

**答案：**

-   **SpringMVC**加载其相关bean(表现层bean),也就是**controller包下的类**
-   **Spring控制的bean**
    -   **业务**bean(Service)
    -   **功能**bean(DataSource,SqlSessionFactoryBean,MapperScannerConfigurer等)

分析清楚谁该管哪些bean以后，接下来要解决的问题是如何让Spring和SpringMVC分开加载各自的内容。

在**SpringMVC**的配置类**`SpringMvcConfig`**中使用注解**`@ComponentScan`**，我们**只需要将其扫描范围**设置到**controller**即可，如

![](https://i-blog.csdnimg.cn/blog_migrate/2051b16eeb6257d722cf08ee3aa299c2.png)

在Spring的配置类**`SpringConfig`**中使用注解**`@ComponentScan`**,当时扫描的范围中其实是已经包含了controller,如:

![](https://i-blog.csdnimg.cn/blog_migrate/88b89e22b8d19d81045cfb666068dc81.png)

**现在的问题：**

**因为功能不同，如何避免Spring错误加载到SpringMVC的bean?**

 **答案：**

加载**Spring**控制的bean的时候**排除掉SpringMVC控制的bean**。Spring加载的bean设定扫描范围为com.itheima,排除掉controller包中的bean

#### 2.5.2 思路分析

针对上面的问题，解决方案也比较简单，就是:

-   加载Spring控制的bean的时候排除掉SpringMVC控制的bean

具体该如何排除：

-   方式一:Spring加载的bean设定扫描范围为精准范围，例如service包、dao包等
-   方式二:Spring加载的bean设定扫描范围为com.itheima,排除掉controller包中的bean
-   方式三:不区分Spring与SpringMVC的环境，加载到同一个环境中\[了解即可\]

#### 2.5.3 环境准备

-   创建一个Web的Maven项目
    
-   pom.xml添加Spring依赖springmvc相关javax.servlet-api,spring-webmvc（里面包括了spring-context），数据库相关mysql-java-connector,spring-jdbc,druid,mybatis,mybatis-spring
    
    ```XML
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
    
      <groupId>com.itheima</groupId>
      <artifactId>springmvc_02_bean_load</artifactId>
      <version>1.0-SNAPSHOT</version>
      <packaging>war</packaging>
    
      <dependencies>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>3.1.0</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.2.10.RELEASE</version>
        </dependency>
        <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>druid</artifactId>
          <version>1.1.16</version>
        </dependency>
    
        <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis</artifactId>
          <version>3.5.6</version>
        </dependency>
    
        <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>5.1.47</version>
        </dependency>
    
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-jdbc</artifactId>
          <version>5.2.10.RELEASE</version>
        </dependency>
    
        <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis-spring</artifactId>
          <version>1.3.0</version>
        </dependency>
      </dependencies>
    
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.1</version>
            <configuration>
              <port>80</port>
              <path>/</path>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    ```
    
-   创建servlet配置类
    
    ```java
    public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
        protected WebApplicationContext createServletApplicationContext() {
            AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
            ctx.register(SpringMvcConfig.class);
            return ctx;
        }
        protected String[] getServletMappings() {
            return new String[]{"/"};
        }
        protected WebApplicationContext createRootApplicationContext() {
          return null;
        }
    }
    
    @Configuration
    @ComponentScan("com.itheima.controller")
    public class SpringMvcConfig {
    }
    
    @Configuration
    @ComponentScan("com.itheima")
    public class SpringConfig {
    }
    ```
    
-   编写Controller，Service，Dao，Domain类
    
    ```java
    @Controller
    public class UserController {
    
        @RequestMapping("/save")
        @ResponseBody
        public String save(){
            System.out.println("user save ...");
            return "{'info':'springmvc'}";
        }
    }
    
    public interface UserService {
        public void save(User user);
    }
    
    @Service
    public class UserServiceImpl implements UserService {
        public void save(User user) {
            System.out.println("user service ...");
        }
    }
    
    public interface UserDao {
        @Insert("insert into tbl_user(name,age)values(#{name},#{age})")
        public void save(User user);
    }
    public class User {
        private Integer id;
        private String name;
        private Integer age;
        //setter..getter..toString略
    }
    ```
    

最终创建好的项目结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/39f22606dc17b4aebfed31c07e97619c.png)

#### 2.5.5 设置bean加载控制

**方式一:**修改**Spring**配置类，设定**扫描范围为精准**范围。

```java
@Configuration
@ComponentScan({"com.itheima.service","comitheima.dao"})
public class SpringConfig {
}
```

**说明:**

上述只是通过例子说明可以精确指定让Spring扫描对应的包结构，真正在做开发的时候，因为Dao最终是交给`MapperScannerConfigurer`对象来进行扫描处理的，我们只需要将其扫描到service包即可。

**方式二:**修改**Spring**配置类，设定扫描范围为com.itheima,**排除掉controller包中的bean**

@ComponentScan的 excludeFilters属性。

```java
@Configuration
@ComponentScan(value="com.itheima",
    excludeFilters=@ComponentScan.Filter(
        type = FilterType.ANNOTATION,
        classes = Controller.class
    )
)
public class SpringConfig {
}
```

-   **excludeFilters属性**：设置扫描加载bean时，排除的**过滤规则**
    
-   **type属性**：设置**排除规则**，当前使用按照bean定义时的注解类型进行排除
    
    -   **ANNOTATION**：**按照注解排除**
    -   ASSIGNABLE\_TYPE:按照指定的类型过滤
    -   ASPECTJ:按照Aspectj表达式排除，基本上不会用
    -   **REGEX**:按照**正则表达式**排除
    -   CUSTOM:按照自定义规则排除
    
    大家**只需要知道第一种ANNOTATION即可**
    
-   **classes属性：**设置**排除的具体注解类**，当前设置排除@Controller定义的bean
    

**测试controller类是否被排除掉了：创建spring容器获取表现层bean**

```java
public class App{
    public static void main (String[] args){
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        System.out.println(ctx.getBean(UserController.class));
    }
}
```

如果被排除了，该方法执行就会报bean未被定义的错误

![](https://i-blog.csdnimg.cn/blog_migrate/73c520f130617827a9e525c8a71b88e0.png)

> **注意:测试**的时候，需要把**SpringMvcConfig**配置类上的**@ComponentScan注解注释**掉，否则不会报错
> 
> 出现问题的原因是，
> 
> -   Spring配置类扫描的包是`com.itheima`
> -   SpringMVC的配置类，**`SpringMvcConfig`**上有一个**@Configuration注解**，也**会被Spring扫描到**
> -   SpringMvcConfig上又有一个@ComponentScan，把controller类又给扫描进来了
> -   所以如果不把@ComponentScan注释掉，Spring配置类将Controller排除，但是因为扫描到SpringMVC的配置类，又将其加载回来，演示的效果就出不来
> -   解决方案，也简单，把SpringMVC的配置类移出Spring配置类的扫描范围即可。

**Servlet容器配置类加载Spring配置类：** 

最后一个问题，有了Spring的配置类，要想在tomcat服务器启动将其加载，我们需要**修改ServletContainersInitConfig的createRootApplicationContext方法**

```java
public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
    protected WebApplicationContext createServletApplicationContext() {
        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        ctx.register(SpringMvcConfig.class);
        return ctx;
    }
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
    protected WebApplicationContext createRootApplicationContext() {
      AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        ctx.register(SpringConfig.class);
        return ctx;
    }
}
```

**Servlet容器配置类简单方法：**

对于上述的配置方式，Spring还提供了一种更简单的配置方式，可以不用再去创建`AnnotationConfigWebApplicationContext`对象，不用手动`register`对应的配置类。

```java
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {

    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
}
```

#### 知识点@ComponentScan的excludeFilters

| 名称 | @ComponentScan |
| --- | --- |
| 类型 | 类注解 |
| 位置 | 类定义上方 |
| 作用 | 设置spring配置类扫描路径，用于加载使用注解格式定义的bean |
| 相关属性 | excludeFilters:排除扫描路径中加载的bean,需要指定类别(type)和具体项(classes)  
includeFilters:加载指定的bean，需要指定类别(type)和具体项(classes) |

## 3，PostMan工具的使用

### 3.1 PostMan简介

代码编写完后，我们要想测试，只需要打开浏览器直接输入地址发送请求即可。发送的是`GET`请求可以直接使用浏览器，但是如果要发送的是`POST`请求呢?

**如果要求发送的是post请求**，我们就得准备页面在页面上准备form表单，测试起来比较**麻烦**。所以我们就需要**借助一些第三方工具，如PostMan.**

-   **PostMan**是一款功能强大的**网页调试与发送网页HTTP请求的Chrome插件**。
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/0c7ec86925d1a9acaa4a94d6674cb72e.png)
    
-   **作用：常用于进行接口测试，模拟浏览器发送请求**
    
-   特征
    
    -   简单
    -   实用
    -   美观
    -   大方

### 3.2 PostMan安装

**下载地址：**

[Download Postman | Get Started for Free](https://www.postman.com/downloads/ "Download Postman | Get Started for Free")

**9.1.2版本下载地址：**

[https://dl.pstmn.io/download/version/9.12.2/win64](https://dl.pstmn.io/download/version/9.12.2/win64 "https://dl.pstmn.io/download/version/9.12.2/win64")

**9.1.2汉化包地址：**

[Releases · hlmd/Postman-cn · GitHub](https://github.com/hlmd/Postman-cn/releases?page=1 "Releases · hlmd/Postman-cn · GitHub")

![](https://i-blog.csdnimg.cn/blog_migrate/d4c0883c98c47e7a7d042c8d776484fb.png)

双击`Postman-win64-8.3.1-Setup.exe`即可自动安装，

汉化包：[Releases · hlmd/Postman-cn · GitHub](https://github.com/hlmd/Postman-cn/releases "Releases · hlmd/Postman-cn · GitHub") 

安装汉化包后解压到postman的app-resources目录下，再次打开就已经汉化成功。

![](https://i-blog.csdnimg.cn/blog_migrate/fb1a11a0abde938553fca585170990cd.png)

安装完成后，如果需要注册，可以按照提示进行注册，如果底部有跳过测试的链接也可以点击跳过注册

![](https://i-blog.csdnimg.cn/blog_migrate/b8f47a4d513cd1b0b00e0b7d41eb7838.png)

看到如下界面，就说明已经安装成功。

![](https://i-blog.csdnimg.cn/blog_migrate/0362efeeb87ab67f4ad96837a1c05764.png)

### 3.3 PostMan使用

#### 3.3.1 创建WorkSpace工作空间

工作空间是可以云备份的。 

![](https://i-blog.csdnimg.cn/blog_migrate/e189150ebae873b70cae20c08aea4878.png)

#### 3.3.2 发送请求

点击+号新建请求：

 ![](https://i-blog.csdnimg.cn/blog_migrate/cf88588587a6cbb95e33ed4d98da82cd.png)

![](https://i-blog.csdnimg.cn/blog_migrate/ed70e2222af3cc890ff160fbd9035954.png)

#### 3.3.3 保存当前请求

![](https://i-blog.csdnimg.cn/blog_migrate/ddc49b1b7ed8a9d3c73897059446cdf3.png)

**注意:**第一次请求需要创建一个新的集合目录，后面就不需要创建新目录，直接保存到已经创建好的目录即可。

## 4，请求与响应

之前我们提到过，**SpringMVC是web层的框架**，**主要的作用**是**接收请求、接收数据、响应结果**，所以这一章节是学习SpringMVC的**重点**内容，我们主要会讲解四部分内容:

-   请求映射路径
-   请求参数
-   日期类型参数传递
-   响应json数据

### 4.1 设置请求映射路径

#### 4.1.1 环境准备

-   创建一个Web的Maven项目
    
-   pom.xml添加Spring依赖javax.servlet,spring-webmvc
    
    ```XML
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
    
      <groupId>com.itheima</groupId>
      <artifactId>springmvc_03_request_mapping</artifactId>
      <version>1.0-SNAPSHOT</version>
      <packaging>war</packaging>
    
      <dependencies>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>3.1.0</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.2.10.RELEASE</version>
        </dependency>
      </dependencies>
    
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.1</version>
            <configuration>
              <port>80</port>
              <path>/</path>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    ```
    
-   创建对应的配置类
    
    ```java
    public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    
        protected Class<?>[] getServletConfigClasses() {
            return new Class[]{SpringMvcConfig.class};
        }
        protected String[] getServletMappings() {
            return new String[]{"/"};
        }
        protected Class<?>[] getRootConfigClasses() {
            return new Class[0];
        }
    }
    
    @Configuration
    @ComponentScan("com.itheima.controller")
    public class SpringMvcConfig {
    }
    ```
    
-   编写**BookController和UserController**，**都有一个/save路径**
    
    ```java
    @Controller
    public class UserController {
    
        @RequestMapping("/save")
        @ResponseBody
        public String save(){
            System.out.println("user save ...");
            return "{'module':'user save'}";
        }
    
        @RequestMapping("/delete")
        @ResponseBody
        public String save(){
            System.out.println("user delete ...");
            return "{'module':'user delete'}";
        }
    }
    
    @Controller
    public class BookController {
    
        @RequestMapping("/save")
        @ResponseBody
        public String save(){
            System.out.println("book save ...");
            return "{'module':'book save'}";
        }
    }
    ```
    

项目结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/ffb2bf33d55be543ea0dd976c46fbe8b.png)

#### 4.1.2 请求冲突问题分析

因为**BookController和UserController**，**都有一个/save路径**，启动Tomcat服务器，后台会报错:

![](https://i-blog.csdnimg.cn/blog_migrate/aeb055e59dfa182a4ae2fc11d324740b.png)

从错误信息可以看出:

-   UserController有一个save方法，访问路径为`http://localhost/save`
-   BookController也有一个save方法，访问路径为`http://localhost/save`
-   当访问`http://localhost/saved`的时候，到底是访问UserController还是BookController?

**问题：团队多人开发，每人设置不同的请求路径，冲突问题该如何解决?**

**解决思路:**为不同模块设置**模块名作为请求路径前置**

对于Book模块的save,将其访问路径设置`http://localhost/book/save`

对于User模块的save,将其访问路径设置`http://localhost/user/save`

这样在同一个模块中出现命名冲突的情况就比较少了。

#### 4.1.3 设置映射路径

**方法一:笨方法，直接修改Controller方法上的@RequestMapping值**

```java
@Controller
public class UserController {

    @RequestMapping("/user/save")
    @ResponseBody
    public String save(){
        System.out.println("user save ...");
        return "{'module':'user save'}";
    }

    @RequestMapping("/user/delete")
    @ResponseBody
    public String save(){
        System.out.println("user delete ...");
        return "{'module':'user delete'}";
    }
}

@Controller
public class BookController {

    @RequestMapping("/book/save")
    @ResponseBody
    public String save(){
        System.out.println("book save ...");
        return "{'module':'book save'}";
    }
}
```

问题是解决了，但是每个方法前面都需要进行修改，写起来比较麻烦而且还有很多重复代码，如果/user后期发生变化，所有的方法都需要改，**耦合度太高**。

**方法二:优化版，给controller类另外配置@RequestMapping，值为模块名**

**优化方案:**

```java
@Controller
@RequestMapping("/user")
public class UserController {

    @RequestMapping("/save")
    @ResponseBody
    public String save(){
        System.out.println("user save ...");
        return "{'module':'user save'}";
    }

    @RequestMapping("/delete")
    @ResponseBody
    public String save(){
        System.out.println("user delete ...");
        return "{'module':'user delete'}";
    }
}

@Controller
@RequestMapping("/book")
public class BookController {

    @RequestMapping("/save")
    @ResponseBody
    public String save(){
        System.out.println("book save ...");
        return "{'module':'book save'}";
    }
}
```

> **注意:**
> 
> -   当**类上和方法上都添加了`@RequestMapping`注解**，前端发送请求的时候，要和两个注解的value值相加匹配才能访问到。
> -   @RequestMapping注解value属性前面**加不加`/`都可以**

扩展小知识:对于PostMan如何觉得字小不好看，可以使用`ctrl+=`调大，`ctrl+-`调小。

### 4.2 普通请求参数传递入门

> 了解即可，更多用JSON传数据。 

请求路径设置好后，只要确保页面发送请求地址和后台Controller类中配置的路径一致，就可以接收到前端的请求，接收到请求后，**如何接收页面传递的参数?**

关于请求参数的传递与接收是和请求方式有关系的，目前比较常见的两种请求方式为：

-   **GET**
-   **POST**

#### 4.2.1 环境准备

-   创建一个Web的Maven项目
    
-   pom.xml添加Spring依赖javax.servlet,spring-webmvc
    
    ```XML
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
    
      <groupId>com.itheima</groupId>
      <artifactId>springmvc_03_request_mapping</artifactId>
      <version>1.0-SNAPSHOT</version>
      <packaging>war</packaging>
    
      <dependencies>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>3.1.0</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.2.10.RELEASE</version>
        </dependency>
      </dependencies>
    
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.1</version>
            <configuration>
              <port>80</port>
              <path>/</path>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    ```
    
-   创建对应的配置类
    
    ```java
    public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    
        protected Class<?>[] getServletConfigClasses() {
            return new Class[]{SpringMvcConfig.class};
        }
        protected String[] getServletMappings() {
            return new String[]{"/"};
        }
        protected Class<?>[] getRootConfigClasses() {
            return new Class[0];
        }
    }
    
    @Configuration
    @ComponentScan("com.itheima.controller")
    public class SpringMvcConfig {
    }
    ```
    
-   **编写UserController**
    
    ```java
    @Controller
    public class UserController {
    
        @RequestMapping("/commonParam")
        @ResponseBody
        public String commonParam(){
            return "{'module':'commonParam'}";
        }
    }
    ```
    
-   **编写模型类，User和Address**
    
    ```java
    public class Address {
        private String province;
        private String city;
        //setter...getter...略
    }
    public class User {
        private String name;
        private int age;
        //setter...getter...略
    }
    ```
    

最终创建好的项目结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/a45d864a7446472298c6443e92bf58fc.png)

#### 4.2.2 请求参数传递和中文乱码解决

> **中文乱码问题：**
> 
> -   不管是**GET还是POST**，controller**代码都是一样的**，**形参传递**，不作区分。只是对于**中文乱码解决不同**，get是在Tomcat插件里配置编码utf-8，post是**Servlet容器配置类**使用**过滤器**设置编码。
> -   **json格式**传递**无中文乱码问题**，注意参数要加@RequestBody，返回值类型是对象和List<类>。return "{'save':'success'}" ;返回的是普通类型String。

**GET发送单个参数**

```
http://localhost/commonParam?name=itcast
```

![](https://i-blog.csdnimg.cn/blog_migrate/36f137e0144ad176a131d61a9bfcb06e.png)

**GET接收单个参数：**

controller里方法**形参名必须和请求参数名一致**：

```java
@Controller
public class UserController {

    @RequestMapping("/commonParam")
    @ResponseBody
    public String commonParam(String name){
        System.out.println("普通参数传递 name ==> "+name);
        return "{'module':'commonParam'}";
    }
}
```

**GET发送多个参数**

```
http://localhost/commonParam?name=itcast&age=15
```

![](https://i-blog.csdnimg.cn/blog_migrate/b50967defa2141493c854407634600e3.png)

**GET接收多个参数：**

```java
@Controller
public class UserController {

    @RequestMapping("/commonParam")
    @ResponseBody
    public String commonParam(String name,int age){
        System.out.println("普通参数传递 name ==> "+name);
        System.out.println("普通参数传递 age ==> "+age);
        return "{'module':'commonParam'}";
    }
}
```

**GET请求中文乱码**

如果Tomcat8.5之前版本，我们传递的参数中有中文，你会发现接收到的参数会出现中文乱码问题。

发送请求:`http://localhost/commonParam?name=张三&age=18`

控制台:

![](https://i-blog.csdnimg.cn/blog_migrate/7260113bc088ee644ec4c7b4ba4dd822.png)

**解决乱码：**

**Tomcat8.5以后的版本已经处理了中文乱码的问题**，但是IDEA中的Tomcat插件目前只到Tomcat7，所以需要修改pom.xml来解决GET请求中文乱码问题

```XML
<build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <configuration>
          <port>80</port><!--tomcat端口号-->
          <path>/</path> <!--虚拟目录-->
          <uriEncoding>UTF-8</uriEncoding><!--访问路径编解码字符集-->
        </configuration>
      </plugin>
    </plugins>
  </build>
```

**POST发送参数**

> -   一定别忘了地址栏左边选择POST请求，不然会500报错。
> -   选择x-www-form-urlencoded，对比之下，form-data表单是既能发表单，又能发文件

![](https://i-blog.csdnimg.cn/blog_migrate/255023085cf9b799a5bcd269a4e8bfaf.png)

**POST接收参数：**

和GET一致，不用做任何修改

```java
@Controller
public class UserController {

    @RequestMapping("/commonParam")
    @ResponseBody
    public String commonParam(String name,int age){
        System.out.println("普通参数传递 name ==> "+name);
        System.out.println("普通参数传递 age ==> "+age);
        return "{'module':'commonParam'}";
    }
}
```

**POST请求中文乱码：所有Tomcat版本都中文乱码**

发送请求与参数:

![](https://i-blog.csdnimg.cn/blog_migrate/91b4f6434e288b62b91424bca8291963.png)

接收参数:

控制台打印，会发现有中文乱码问题。

![](https://i-blog.csdnimg.cn/blog_migrate/ed95d26afbb516c90d1983da46ab776f.png)

**解决方案:配置过滤器**

在**Servlet容器配置类**里，alt+insert**重写getServletFilters**过滤器方法： 

```java
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }

    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    //重写getServletFilters过滤器方法，返回数组传入CharacterEncodingFilter过滤器对象，乱码处理
    @Override
    protected Filter[] getServletFilters() {
        //创建字符编码过滤器CharacterEncodingFilter对象
        CharacterEncodingFilter filter = new CharacterEncodingFilter();
        //设置编码
        filter.setEncoding("UTF-8");
        //返回过滤器数组，元素为CharacterEncodingFilter对象
        return new Filter[]{filter};
    }
}
```

> **注意：**
> 
> -   **过滤器方法只适用于post**请求方式的中文乱码，get中文乱码还是要Tomcat8以上，或Tomcat7的pom里设置Tomcat插件编码
> -   CharacterEncodingFilter是在spring-webmvc包中，所以用之前要确保导入对应的jar包。

### 4.3 请求头的五种类型参数传递

前面我们已经能够使用GET或POST来发送请求和数据，所携带的数据都是比较简单的数据，接下来在这个基础上，我们来研究一些比较复杂的参数传递，常见的参数种类有:

-   **普通参数**
-   **POJO类型参数**
-   **嵌套POJO类型参数**
-   **数组类型参数**
-   **集合类型参数**

#### 4.3.1 普通请求参数，起别名，**@RequestParam**

-   普通参数:url地址传参，地址参数名与形参变量名相同，定义形参即可接收参数。

![](https://i-blog.csdnimg.cn/blog_migrate/666e68c4d88658ee9dff7fa031d4fdba.png)

**问题：如果形参与地址参数名不一致该如何解决?**

**解决方案:使用@RequestParam注解，用法跟dao层传参@Param类似** 

发送请求与参数:

```
http://localhost/commonParamDifferentName?name=张三&age=18
```

后台接收参数:

```java
@RequestMapping("/commonParamDifferentName")
@ResponseBody
public String commonParamDifferentName(String userName , int age){
    System.out.println("普通参数传递 userName ==> "+userName);
    System.out.println("普通参数传递 age ==> "+age);
    return "{'module':'common param different name'}";
}
```

因为前端给的是`name`,后台接收使用的是`userName`,两个名称对不上，导致接收数据失败:

![](https://i-blog.csdnimg.cn/blog_migrate/7d6da64bfc2e48472ff9d11cf4d88fc9.png)

**解决方案:使用@RequestParam注解，用法跟dao层传参@Param类似**

```java
@RequestMapping("/commonParamDifferentName")
    @ResponseBody
    public String commonParamDifferentName(@RequestParam("name") String userName , int age){
        System.out.println("普通参数传递 userName ==> "+userName);
        System.out.println("普通参数传递 age ==> "+age);
        return "{'module':'common param different name'}";
    }
```

**注意:写上@RequestParam注解框架就不需要自己去解析注入，能提升框架处理性能**

#### 4.3.2 POJO数据类型

适用于参数多的情况，将参数封装成一个实体类中。 

简单数据类型一般处理的是参数个数比较少的请求，如果参数比较多，那么后台接收参数的时候就比较复杂，这个时候我们可以考虑使用POJO实体类数据类型。

-   **POJO实体类参数：请求参数名与形参对象的属性名相同**，定义POJO类型形参即可接收参数

此时需要使用前面准备好的POJO类，先来看下User

```java
public class User {
    private String name;
    private int age;
    //setter...getter...略
}
```

发送请求和参数:

![](https://i-blog.csdnimg.cn/blog_migrate/389fd7a5066ed4c69adf8c3aa6aa2c04.png)

后台接收参数:

```java
//POJO参数：请求参数与形参对象中的属性对应即可完成参数传递
@RequestMapping("/pojoParam")
@ResponseBody
public String pojoParam(User user){
    System.out.println("pojo参数传递 user ==> "+user);
    return "{'module':'pojo param'}";
}
```

> **注意:**
> 
> -   POJO参数接收，前端GET和POST发送请求数据的方式不变。
> -   **请求参数key的名称要和POJO中属性的名称一致，否则无法封装。**

#### 4.3.3 嵌套POJO类型参数

如果POJO对象中嵌套了其他的POJO类，如

```java
public class Address {
    private String province;
    private String city;
    //setter...getter...略
}
public class User {
    private String name;
    private int age;
    private Address address;
    //setter...getter...略
}
```

-   **嵌套POJO参数：请求参数名与形参对象属性名相同**，注意内嵌的pojo类在发送请求时参数要设成**内嵌类对象.属性名**，**形参**依然是传**外层类的对象**，按照对象层次结构关系即可接收嵌套POJO属性参数

发送请求和参数:

![](https://i-blog.csdnimg.cn/blog_migrate/19fed29448b3546650bf7186ddf852aa.png)

后台接收参数:

```java
//POJO参数嵌套：请求参数与形参对象中的属性对应即可完成参数传递
@RequestMapping("/pojoParam")
@ResponseBody
public String pojoParam(User user){
    System.out.println("pojo参数传递 user ==> "+user);
    return "{'module':'pojo param'}";
}
```

> **注意:**
> 
> **请求参数key的名称要和POJO中属性的名称一致，否则无法封装**

#### 4.3.4 数组类型参数

举个简单的例子，如果前端需要获取用户的爱好，爱好绝大多数情况下都是多个，如何发送请求数据和接收数据呢?

-   **数组参数：请求参数名与形参数组名相同，且请求参数为多个**，定义数组类型即可接收参数

发送请求和参数:

![](https://i-blog.csdnimg.cn/blog_migrate/e48a208e61fe9cb5980ed028d173d62c.png)

后台接收参数:

```java
  //数组参数：同名请求参数可以直接映射到对应名称的形参数组对象中
    @RequestMapping("/arrayParam")
    @ResponseBody
    public String arrayParam(String[] likes){
        System.out.println("数组参数传递 likes ==> "+ Arrays.toString(likes));
        return "{'module':'array param'}";
    }
```

#### 4.3.5 集合类型参数，**`@RequestParam`**

**结论：**请求参数跟上面数组一样，controller形参为**`@RequestParam`**注解的同名集合对象。

> **集合直接做形参会报错，报错演示：**
> 
> 发送请求和参数:
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8d2577b564acafae603d8079d1ba46f8.png)
> 
> 后台接收参数:
> 
> ```java
> //集合参数：同名请求参数可以使用@RequestParam注解映射到对应名称的集合对象中作为数据
> @RequestMapping("/listParam")
> @ResponseBody
> public String listParam(List<String> likes){
>     System.out.println("集合参数传递 likes ==> "+ likes);
>     return "{'module':'list param'}";
> }
> ```
> 
> 运行会报错，
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/97cfc6a6ae587ac706e9b5d36bce11c9.png)
> 
> **错误的原因是:**SpringMVC将**List看做**是一个**POJO对象**来处理，将其创建一个对象并准备把前端的数据封装到对象中，但是List是一个接口无法创建对象，所以报错。
> 
> **解决方案是:使用`@RequestParam`注解绑定参数关系**

**使用`@RequestParam`注解绑定参数关系**

```java
//集合参数：同名请求参数可以使用@RequestParam注解映射到对应名称的集合对象中作为数据
@RequestMapping("/listParam")
@ResponseBody
public String listParam(@RequestParam List<String> likes){
    System.out.println("集合参数传递 likes ==> "+ likes);
    return "{'module':'list param'}";
}
```

> **注意：**
> 
> -   **集合保存普通参数：请求参数名与形参集合对象名相同**且请求参数为多个，@RequestParam绑定参数关系
> -   对于简单数据类型使用**数组会比集合更简单**些。

#### 知识点@RequestParam

| 名称 | @RequestParam |
| --- | --- |
| 类型 | 形参注解 |
| 位置 | SpringMVC控制器方法形参定义前面 |
| 作用 | 绑定请求参数与处理器方法形参间的关系 |
| 相关参数 | required：是否为必传参数  
defaultValue：参数默认值 |

### 4.4 请求体的JSON数据传输参数，**@RequestBody**

#### 4.4.1 概述 

**@RequestBody接收请求体JSON数据，并转为对象或对象数组。**

前面我们说过，现在比较流行的开发方式为**异步调用**。前后台以异步方式进行交换，传输的数据使用的是**JSON**,所以前端如果发送的是JSON数据，后端该如何接收?

对于**JSON数据类型**，我们常见的有三种:

-   **json普通数组：**  \["value1","value2","value3",...\]
-   **json对象：** {key1:value1,key2:value2,...}
-   **json对象数组：** \[{key1:value1,...},{key2:value2,...}\]

使用josn数据传输参数要先导入**Jackson依赖**和 **@EnableWebMvc注解**

 **pom.xml添加依赖jackson-databind**

SpringMVC默认使用的是**jackson来处理json的转换**，所以需要在pom.xml添加jackson依赖

```XML
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.0</version>
</dependency>
```

 **开启SpringMVC注解支持@EnableWebMvc**

在SpringMVC的配置类中开启SpringMVC的注解支持**@EnableWebMvc**，这个注解功能很强大，里面**包含了将JSON转换成对象的功能**。

```java
@Configuration
@ComponentScan("com.itheima.controller")
//开启json数据类型自动转换
@EnableWebMvc
public class SpringMvcConfig {
}
```

#### 4.4.2 JSON普通数组，**@EnableWebMvc**

>  剧透，后面使用springboot和Rest风格后，给controller注解@RestController后就不用导入Jackson、@EnableWebMvc，直接参数前@RequestBody即可

**controller接收前端请求头的JSON数组并转为List：**

**步骤1:pom.xml添加依赖jackson-databind**

SpringMVC默认使用的是**jackson来处理json的转换**，所以需要在pom.xml添加jackson依赖

```XML
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.0</version>
</dependency>
```

**步骤2:PostMan发送JSON数据**

![](https://i-blog.csdnimg.cn/blog_migrate/b721dcce3d709383726927501a6be153.png)

**步骤3:开启SpringMVC注解支持@EnableWebMvc**

在SpringMVC的配置类中开启SpringMVC的注解支持，这里面就包含了将JSON转换成对象的功能。

```java
@Configuration
@ComponentScan("com.itheima.controller")
//开启json数据类型自动转换
@EnableWebMvc
public class SpringMvcConfig {
}
```

**步骤4:controller形参前添加@RequestBody**

```java

@RequestMapping("/listParamForJson")
@ResponseBody
//使用@RequestBody注解将前端请求体传递的json数组数据，传递并转换到形参的集合对象中作为数据
public String listParamForJson(@RequestBody List<String> likes){
    System.out.println("list common(json)参数传递 list ==> "+likes);
    return "{'module':'list common for json param'}";
}
```

**步骤5:启动运行程序**

![](https://i-blog.csdnimg.cn/blog_migrate/fb5e6f119cd59decf8cb4b5d53aac177.png)

#### 4.4.3 JSON对象数据

>  剧透，后面使用springboot和Rest风格后，给controller注解@RestController后就不用导入Jackson、@EnableWebMvc，直接参数前@RequestBody即可

> **回顾：**
> 
> **Servlet接收JSON对象：**
> 
> 1.Servlet的getParameter获取String形式的json对象
> 
> 2.fastjson的JSON.parseObject方法将json对象转为实体类对象
> 
> **Servlet响应JSON对象到前端：**
> 
> 1.将实体类对象通过fastjson的JSON.toJSONString方法转为String类型
> 
> 2.response.getWriter().write(jsonStr)

**controller接收前端JSON对象并转为实体类对象：**

**前端发送JSON对象数据:**

```java
{
    "name":"itcast",
    "age":15
}
```

![](https://i-blog.csdnimg.cn/blog_migrate/2fa4ed7521d9fca1cf464449616518e4.png)

**controller接收JSON对象数据：** 

带@RequestBody实体类对象的形参直接转换JSON对象

```java
@RequestMapping("/pojoParamForJson")
@ResponseBody
public String pojoParamForJson(@RequestBody User user){
    System.out.println("pojo(json)参数传递 user ==> "+user);
    return "{'module':'pojo for json param'}";
}
```

>  **记得开启SpringMVC注解@EnableWebMvc**
> 
> 在SpringMVC的配置类中开启SpringMVC的注解支持，这里面就包含了**将JSON转换成对象**的功能。
> 
> ```java
> @Configuration
> @ComponentScan("com.itheima.controller")
> //开启json数据类型自动转换
> @EnableWebMvc
> public class SpringMvcConfig {
> }
> ```

启动程序访问测试

![](https://i-blog.csdnimg.cn/blog_migrate/84d3cdb1c14cc634b16eb5b01ea1d0c2.png)

> **说明:**
> 
> address为null的原因是前端没有传递数据给后端。
> 
> 如果想要address也有数据，我们需求修改前端传递的数据内容:
> 
> ```java
> {
>     "name":"itcast",
>     "age":15,
>     "address":{
>         "province":"beijing",
>         "city":"beijing"
>     }
> }
> ```
> 
> 再次发送请求，就能看到address中的数据
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/ffcbd5b167f2ce04b8401a3837d50138.png)

#### 4.4.4 JSON对象数组

>  剧透，后面使用springboot和Rest风格后，给controller注解@RestController后就不用导入Jackson、@EnableWebMvc，直接参数前@RequestBody即可 

**controller接收前端JSON数组并转为List：**

前端发送JSON对象数组:

```java
[
    {"name":"itcast","age":15},
    {"name":"itheima","age":12}
]
```

![](https://i-blog.csdnimg.cn/blog_migrate/f4bfa6f9dafde7f871e137f9b861e5ca.png)

后端接收数据:

```java
@RequestMapping("/listPojoParamForJson")
@ResponseBody
public String listPojoParamForJson(@RequestBody List<User> list){
    System.out.println("list pojo(json)参数传递 list ==> "+list);
    return "{'module':'list pojo for json param'}";
}
```

启动程序访问测试

![](https://i-blog.csdnimg.cn/blog_migrate/6a4a90648833af9772648481533c9309.png)

> **小结**
> 
> SpringMVC接收JSON数据的实现步骤为:
> 
> (1)导入jackson包
> 
> (2)使用PostMan发送JSON数据
> 
> (3)开启SpringMVC注解驱动，在配置类上添加@EnableWebMvc注解
> 
> (4)Controller方法的参数前添加@RequestBody注解

#### 知识点 @EnableWebMvc@RequestBody

**知识点1：@EnableWebMvc**

| 名称 | @EnableWebMvc |
| --- | --- |
| 类型 | **配置类注解** |
| 位置 | SpringMVC配置类定义上方 |
| 作用 | 开启SpringMVC多项辅助功能 |

**知识点2：@RequestBody**

| 名称 | @RequestBody |
| --- | --- |
| 类型 | **形参注解** |
| 位置 | SpringMVC控制器方法形参定义前面 |
| 作用 | 将请求中请求体所包含的数据传递给请求参数，此注解一个处理器方法只能使用一次 |

#### **4.4.5 @RequestBody与@RequestParam区别**

-   **区别**
    
    -   @RequestParam用于集合类型传参，用于起别名【application/x-www-form-urlencoded】
    -   @RequestBody用于接收json数据【application/json】
-   **应用**
    
    -   后期开发中，发送json格式数据为主，@RequestBody应用较广
    -   如果发送非json格式数据，选用@RequestParam接收请求参数

#### **4.4.5** @RequestParam和@RequestPart的区别

当请求头中指定Content-Type:multipart/form-data时，传递的json参数，@RequestPart注解可以用对象来接收，@RequestParam只能用字符串接收

-   `@RequestPart`这个注解用在`multipart/form-data`表单提交请求的方法上。
-   支持的请求方法的方式`MultipartFile`，属于Spring的`MultipartResolver`类。这个请求是通过`http协议`传输的

### 4.5 日期类型参数传递@DateTimeFormat

前面我们处理过简单数据类型、POJO数据类型、数组和集合数据类型以及JSON数据类型，接下来我们还得处理一种开发中比较常见的一种数据类型，**`日期类型`**

日期类型比较特殊，因为对于**日期的格式有N多中输入方式**，比如:

-   2088-08-18
-   2088/08/18
-   08/18/2088
-   ......

#### 4.5.1 具体代码

20xx/xx/xx格式日期，controller可以自动转换成Date对象，其他格式日期要注解**@DateTimeFormat(pattern="yyyy-MM-dd")** ，pattern译为模式，图案

**步骤1:编写方法接收日期数据**

在UserController类中添加方法，把参数设置为日期类型

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date)
    System.out.println("参数传递 date ==> "+date);
    return "{'module':'data param'}";
}
```

**步骤2:启动Tomcat服务器**

查看控制台是否报错，如果有错误，先解决错误。

**步骤3:使用PostMan发送请求**

使用PostMan发送GET请求，并设置date参数

```java
http://localhost/dataParam?date=2088/08/08
```

![](https://i-blog.csdnimg.cn/blog_migrate/db41fda4f7bfffe8e268dbb5159b8217.png)

**步骤4:查看控制台**

![](https://i-blog.csdnimg.cn/blog_migrate/efdb49045f6784099a37c676cb8cf228.png)

通过打印，我们发现SpringMVC可以接收日期数据类型，并将其打印在控制台。

这个时候，我们就想如果把日期参数的格式改成其他的，SpringMVC还能处理么?

**步骤5:更换日期格式**

为了能更好的看到程序运行的结果，我们在方法中多添加一个日期参数

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,Date date1)
    System.out.println("参数传递 date ==> "+date);
    return "{'module':'data param'}";
}
```

使用PostMan发送请求，携带两个不同的日期格式，

```java
http://localhost/dataParam?date=2088/08/08&date1=2088-08-08
```

![](https://i-blog.csdnimg.cn/blog_migrate/c93bf271d334935e5d9d972682b52da7.png)

发送请求和数据后，页面会报400，控制台会报出一个错误

Resolved \[org.springframework.web.method.annotation.**MethodArgumentTypeMismatchException**: Failed to convert value of type 'java.lang.String' to required type 'java.util.Date'; nested exception is org.springframework.core.convert.**ConversionFailedException**: Failed to convert from type \[java.lang.String\] to type \[java.util.Date\] for value '2088-08-08'; nested exception is java.lang.IllegalArgumentException\]

从错误信息可以看出，错误的原因是在将`2088-08-08`转换成日期类型的时候失败了，原因是SpringMVC默认支持的字符串转日期的格式为`yyyy/MM/dd`,而我们现在传递的不符合其默认格式，SpringMVC就无法进行格式转换，所以报错。

解决方案也比较简单，需要使用`@DateTimeFormat`

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,
                        @DateTimeFormat(pattern="yyyy-MM-dd") Date date1)
    System.out.println("参数传递 date ==> "+date);
    System.out.println("参数传递 date1(yyyy-MM-dd) ==> "+date1);
    return "{'module':'data param'}";
}
```

重新启动服务器，重新发送请求测试，SpringMVC就可以正确的进行日期转换了

![](https://i-blog.csdnimg.cn/blog_migrate/2c3c7475030102ad137210e5c0ee9777.png)

**步骤6:携带时间的日期**

接下来我们再来发送一个携带时间的日期，看下SpringMVC该如何处理?

先修改UserController类，添加第三个参数

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,
                        @DateTimeFormat(pattern="yyyy-MM-dd") Date date1,
                        @DateTimeFormat(pattern="yyyy/MM/dd HH:mm:ss") Date date2)
    System.out.println("参数传递 date ==> "+date);
    System.out.println("参数传递 date1(yyyy-MM-dd) ==> "+date1);
    System.out.println("参数传递 date2(yyyy/MM/dd HH:mm:ss) ==> "+date2);
    return "{'module':'data param'}";
}
```

使用PostMan发送请求，携带两个不同的日期格式，

```java
http://localhost/dataParam?date=2088/08/08&date1=2088-08-08&date2=2088/08/08 8:08:08
```

![](https://i-blog.csdnimg.cn/blog_migrate/1bf1392ec6e61bc633137e321dcad9bb.png)

重新启动服务器，重新发送请求测试，SpringMVC就可以将日期时间的数据进行转换

![](https://i-blog.csdnimg.cn/blog_migrate/2ec5f3509c6179a0ff7e1c39154a592f.png)

#### 知识点@DateTimeFormat

| 名称 | @DateTimeFormat |
| --- | --- |
| 类型 | **形参注解** |
| 位置 | SpringMVC控制器方法形参前面 |
| 作用 | 设定日期时间型数据格式 |
| 相关属性 | pattern：指定日期时间格式字符串 |

#### 4.5.2 类型转换内部实现原理

> 讲解内部原理之前，我们需要先思考个问题:
> 
> -   前端传递字符串，后端使用日期Date接收
> -   前端传递JSON数据，后端使用对象接收
> -   前端传递字符串，后端使用Integer接收
> -   后台需要的数据类型有很多中
> -   在数据的传递过程中存在很多类型的转换
> 
> 问:谁来做这个类型转换?
> 
> 答:SpringMVC
> 
> 问:SpringMVC是如何实现类型转换的?
> 
> 答:SpringMVC中提供了很多类型转换接口和实现类

在框架中，有一些类型转换接口，其中有:

-   **(1) Converter接口**

```java
/**
*    S: the source type
*    T: the target type
*/
public interface Converter<S, T> {
    @Nullable
    //该方法就是将从页面上接收的数据(S)转换成我们想要的数据类型(T)返回
    T convert(S source);
}
```

**注意:Converter所属的包为`org.springframework.core.convert.converter`**

Converter接口的实现类

![](https://i-blog.csdnimg.cn/blog_migrate/3bd8000a8adacafea4287dd204f27a1d.png)

框架中有提供很多对应Converter接口的实现类，用来实现不同数据类型之间的转换,如:

请求参数年龄数据（String→Integer）

日期格式转换（String → Date）

-   **(2) HttpMessageConverter接口**

该接口是实现**对象与JSON之间的转换工作**

****注意:SpringMVC的配置类把@EnableWebMvc当做标配配置上去，不要省略****

### 4.6 响应

SpringMVC接收到请求和数据后，进行一些了的处理，当然这个处理可以是转发给Service，Service层再调用Dao层完成的，不管怎样，**处理完以后，都需要将结果告知给用户。**

**比如:根据用户ID查询用户信息、查询用户列表、新增用户等。**

对于响应，主要就包含两部分内容：

-   **响应页面**
-   **响应数据**
    -   **文本数据**
    -   **json数据**

因为**异步调用**是目前常用的主流方式，所以我们需要**更关注**的就是如何返回**JSON数据**，对于其他只需要认识了解即可。

#### 4.6.1 环境准备，jackson-databind依赖

-   创建一个Web的Maven项目
    
-   pom.xml添加Spring依赖javax.servlet-api,spring-webmvc,jackson-databind
    
    ```XML
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
    
      <groupId>com.itheima</groupId>
      <artifactId>springmvc_05_response</artifactId>
      <version>1.0-SNAPSHOT</version>
      <packaging>war</packaging>
    
      <dependencies>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>3.1.0</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.2.10.RELEASE</version>
        </dependency>
    <!--json解析工具-->
        <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-databind</artifactId>
          <version>2.9.0</version>
        </dependency>
      </dependencies>
    
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.1</version>
            <configuration>
              <port>80</port>
              <path>/</path>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    ```
    
-   创建servlet容器的配置类和springmvc配置类
    
    ```java
    public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
        protected Class<?>[] getRootConfigClasses() {
            return new Class[0];
        }
    
        protected Class<?>[] getServletConfigClasses() {
            return new Class[]{SpringMvcConfig.class};
        }
    
        protected String[] getServletMappings() {
            return new String[]{"/"};
        }
    
        //乱码处理
        @Override
        protected Filter[] getServletFilters() {
            CharacterEncodingFilter filter = new CharacterEncodingFilter();
            filter.setEncoding("UTF-8");
            return new Filter[]{filter};
        }
    }
    
    @Configuration
    @ComponentScan("com.itheima.controller")
    //开启json数据类型自动转换
    @EnableWebMvc
    public class SpringMvcConfig {
    }
    
    ```
    
-   编写模型类User
    

```java
public class User {
    private String name;
    private int age;
    //getter...setter...toString省略
}
```

-   webapp下创建page.jsp
    
    ```html
    <html>
    <body>
    <h2>Hello Spring MVC!</h2>
    </body>
    </html>
    ```
    

最终创建好的项目结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/00fa6eb5bf55bc8da0fd97044d3fe414.png)

#### 4.6.2 响应jsp页面\[了解\]

**步骤1:设置返回页面**

```java
@Controller
public class UserController {

    @RequestMapping("/toJumpPage")
    //注意
    //1.此处不能添加@ResponseBody,如果加了该注入，会直接将page.jsp当字符串返回前端
    //2.方法需要返回String
    public String toJumpPage(){
        System.out.println("跳转页面");
        return "page.jsp";
    }

}
```

> **注意：**
> 
> -   **方法不能添加@ResponseBody**,如果加了该注入，会直接将page.jsp当字符串返回前端。
> -   方法需要返回String

**步骤2:启动程序测试**

此处涉及到页面跳转，所以不适合采用PostMan进行测试，直接打开浏览器，输入

`http://localhost/toJumpPage`

![](https://i-blog.csdnimg.cn/blog_migrate/96bc9d06a1ad9ea08eaad8099137cf7f.png)

#### 4.6.3 返回文本数据\[了解\]

**步骤1:设置返回文本内容**

```java
@Controller
public class UserController {

       @RequestMapping("/toText")
    //注意此处该注解就不能省略，如果省略了,会把response text当前页面名称去查找，如果没有回报404错误
    @ResponseBody
    public String toText(){
        System.out.println("返回纯文本数据");
        return "response text";
    }

}
```

**步骤2:启动程序测试**

此处不涉及到页面跳转，因为我们现在发送的是GET请求，可以使用浏览器也可以使用PostMan进行测试，输入地址`http://localhost/toText`访问

![](https://i-blog.csdnimg.cn/blog_migrate/88305623ad1f11f022d90ac4b4b04182.png)

#### 4.6.4 响应JSON数据

**响应POJO对象：直接返回对象**

```java
@Controller
public class UserController {

    @RequestMapping("/toJsonPOJO")
    @ResponseBody
    @JsonFormat(pattern="yyyy-MM-dd HH:mm:ss", timezone = "GMT+8")    //导入jackson-databind后可以格式化日期格式
    public User toJsonPOJO(){
        System.out.println("返回json对象数据");
        User user = new User();
        user.setName("itcast");
        user.setAge(15);
        return user;
    }

}
```

返回值为实体类对象，设置返回值为实体类类型，即可实现返回对应对象的json数据，需要依赖**@ResponseBody**注解和**@EnableWebMvc**注解

重新启动服务器，访问

```java
http://localhost/toJsonPOJO
```

![](https://i-blog.csdnimg.cn/blog_migrate/ffa4ee195e683af5adb549dda2dea85c.png)

> 如果return字符串"{'zhang张三':32}"会存在中文乱码问题，所以返回对象自动转JSON比较好。

**响应POJO集合对象：直接返回集合类型**

```java
@Controller
public class UserController {

    @RequestMapping("/toJsonList")
    @ResponseBody
    public List<User> toJsonList(){
        System.out.println("返回json集合数据");
        User user1 = new User();
        user1.setName("传智播客");
        user1.setAge(15);

        User user2 = new User();
        user2.setName("黑马程序员");
        user2.setAge(12);

        List<User> userList = new ArrayList<User>();
        userList.add(user1);
        userList.add(user2);

        return userList;
    }

}
```

重新启动服务器，访问`http://localhost/toJsonList`

![](https://i-blog.csdnimg.cn/blog_migrate/4ce70e4ba2292887656347380765c4ae.png)

#### 知识点@ResponseBody

| 名称 | @ResponseBody |
| --- | --- |
| 类型 | **方法\\类注解** |
| 位置 | SpringMVC控制器方法定义上方和控制类上 |
| 作用 | **设置当前控制器返回值作为响应体,**  
写在类上，该类的所有方法都有该注解功能 |
| 相关属性 | pattern：指定日期时间格式字符串 |

**说明:**

-   该注解可以写在类上或者方法上
-   写在类上就是该类下的所有方法都有@ReponseBody功能
-   当**方法上有@ReponseBody**注解后
    -   方法的**返回值为字符串**，会将其作为**文本内容**直接**响应给前端**
    -   方法的**返回值为对象**，会将对象**转换成JSON响应给前端**

此处又使用到了类型转换，内部还是通过Converter接口的实现类完成的，所以Converter除了前面所说的功能外，它还可以实现:

-   对象转Json数据(POJO -> json)
-   集合转Json数据(Collection -> json)

## 5，Rest风格

### 5.1 REST简介

SpringMVC的Rest风格指的是以RESTful API实现在Web上，对外提供一个面向资源（resource）的接口设计。该风格下的API需要遵循如下约定：

-   使用HTTP协议中的GET、POST、PUT、DELETE方法来表示对资源的增删改查操作；
-   遵循URI只建议由小写字母、数字、连字符和点号`/`组成、“/”为层级关系的分隔符、名词使用复数形式等命名规则；
-   避免使用已经过期的HTTP Header信息，如“Accept-Charset”、“Accept-Encoding”、“Connection”。推荐参照HTTP1.1版本，使用应答首部文件中的"Content-Type"。

示例：

| 请求类型 | REST URL | 描述 |
| --- | --- | --- |
| GET | /users | 获取用户列表 |
| POST | /users | 创建新用户 |
| PUT | /users/{id} | 修改指定ID的用户 |
| DELETE | /users/{id} | 删除指定ID的用户 |

采用Rest风格的API其好处在于：可以简化接口调用，降低了与客户端之间开发的耦合度，同时也让数据更加直观易懂。同时，有助于降低服务端的开发制约，支持微服务架构，并且能够更好地支持各种移动设备和网络应用，可以更好地满足API设计的不断迭代、演进的需求。

-   **REST**（Representational State Transfer），**表现性状态转换**,它是一种**软件架构风格**
    
    当我们想**表示一个网络资源**的时候，可以使用两种方式:
    
    -   **传统风格资源描述形式**
        -   `http://localhost/user/getById?id=1` 查询id为1的用户信息
        -   `http://localhost/user/saveUser` 保存用户信息
    -   **REST风格描述形式**
        -   `http://localhost/user/1`
        -   `http://localhost/user`

传统方式一般是一个请求url对应一种操作，这样做不仅麻烦，也不安全，因为会程序的人读取了你的请求url地址，就大概知道该url实现的是一个什么样的操作。

查看REST风格的描述，你会发现请求地址变的简单了，并且**光看请求URL并不是很能猜出来该URL的具体功能**

所以**REST的优点**有:

-   **隐藏资源的访问行为**，无法通过地址得知对资源是何种操作
-   **书写简化**

**问题：**一个相同的**url地址**即可以是新增也可以是修改或者查询，我们该**如何区分**？

**答案： 使用请求方式区分，例如`GET`,`POST`,`PUT`,`DELETE。`**

-   按照REST风格访问资源时使用**请求方式**区分对资源进行了何种操作
    -   `http://localhost/users` 查询全部用户信息 **GET（查询）**
    -   `http://localhost/users/1` 查询指定用户信息 GET（查询）
    -   `http://localhost/users` 添加用户信息 **POST（新增/保存）**
    -   `http://localhost/users` 修改用户信息 **PUT（修改/更新）**
    -   `http://localhost/users/1` 删除用户信息 **DELETE（删除）**

请求的方式比较多，但是比较常用的就4种，分别是**`GET`,`POST`,`PUT`,`DELETE`**。

**常用的四种请求方式：**

-   发送**GET请求**是用来做**查询**
-   发送**POST请求**是用来做**新增**
-   发送**PUT请求**是用来做**修改**
-   发送**DELETE请求**是用来做**删除**

> **注意**:
> 
> -   上述行为是**约定方式，约定不是规范，可以打破**，所以称REST风格，而不是REST规范。虽然不是规范，但现在**基本都用rest风格**。
>     -   **REST提供了对应的架构方式**，按照这种架构设计项目可以降低开发的复杂性，提高系统的可伸缩性
>     -   REST中规定GET/POST/PUT/DELETE针对的是查询/新增/修改/删除，但是我们如果非要用GET请求做删除，这点在程序上运行是可以实现的
>     -   但是如果绝大多数人都遵循这种风格，你写的代码让别人读起来就有点莫名其妙了。
> -   描述**模块的名称**通常使用**复数**，也就是加s的格式描述，表示此类资源，而非单个资源，例如:users、books、accounts......

 **RESTful：**

清楚了什么是REST风格后，我们后期会经常提到一个概念叫`RESTful`，那什么又是RESTful呢?

-   **根据REST风格对资源进行访问**称为**RESTful**。

后期我们在进行开发的过程中，大多是都是遵从REST风格来访问我们的后台服务，所以可以说咱们以后都是**基于RESTful来进行开发**的。

### 5.2 RESTful入门案例

#### 5.2.1 环境准备

-   创建一个Web的Maven项目
    
-   pom.xml添加依赖javax.servlet-api,spring-webmvc,jackson-databind
    
    ```XML
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
    
      <groupId>com.itheima</groupId>
      <artifactId>springmvc_06_rest</artifactId>
      <version>1.0-SNAPSHOT</version>
      <packaging>war</packaging>
    
      <dependencies>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>3.1.0</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.2.10.RELEASE</version>
        </dependency>
        <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-databind</artifactId>
          <version>2.9.0</version>
        </dependency>
      </dependencies>
    
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.1</version>
            <configuration>
              <port>80</port>
              <path>/</path>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    ```
    
-   **创建对应的配置类**
    

```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }

      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }

      protected String[] getServletMappings() {
          return new String[]{"/"};
      }

      //乱码处理
      @Override
      protected Filter[] getServletFilters() {
          CharacterEncodingFilter filter = new CharacterEncodingFilter();
          filter.setEncoding("UTF-8");
          return new Filter[]{filter};
      }
  }

  @Configuration
  @ComponentScan("com.itheima.controller")
  //开启json数据类型自动转换
  @EnableWebMvc
  public class SpringMvcConfig {
  }
```

编写模型类User和Book

```java
  public class User {
      private String name;
      private int age;
      //getter...setter...toString省略
  }

  public class Book {
      private String name;
      private double price;
       //getter...setter...toString省略
  }
```

**编写UserController和BookController**

```java
  @Controller
  public class UserController {
      @RequestMapping("/save")
      @ResponseBody
      public String save(@RequestBody User user) {
          System.out.println("user save..."+user);
          return "{'module':'user save'}";
      }

      @RequestMapping("/delete")
      @ResponseBody
      public String delete(Integer id) {
          System.out.println("user delete..." + id);
          return "{'module':'user delete'}";
      }

      @RequestMapping("/update")
      @ResponseBody
      public String update(@RequestBody User user) {
          System.out.println("user update..." + user);
          return "{'module':'user update'}";
      }

      @RequestMapping("/getById")
      @ResponseBody
      public String getById(Integer id) {
          System.out.println("user getById..." + id);
          return "{'module':'user getById'}";
      }

      @RequestMapping("/findAll")
      @ResponseBody
      public String getAll() {
          System.out.println("user getAll...");
          return "{'module':'user getAll'}";
      }
  }


  @Controller
  public class BookController {

      @RequestMapping(value = "/books",method = RequestMethod.POST)
      @ResponseBody
      public String save(@RequestBody Book book){
          System.out.println("book save..." + book);
          return "{'module':'book save'}";
      }

      @RequestMapping(value = "/books/{id}",method = RequestMethod.DELETE)
      @ResponseBody
      public String delete(@PathVariable Integer id){
          System.out.println("book delete..." + id);
          return "{'module':'book delete'}";
      }

      @RequestMapping(value = "/books",method = RequestMethod.PUT)
      @ResponseBody
      public String update(@RequestBody Book book){
          System.out.println("book update..." + book);
          return "{'module':'book update'}";
      }

      @RequestMapping(value = "/books/{id}",method = RequestMethod.GET)
      @ResponseBody
      public String getById(@PathVariable Integer id){
          System.out.println("book getById..." + id);
          return "{'module':'book getById'}";
      }

      @RequestMapping(value = "/books",method = RequestMethod.GET)
      @ResponseBody
      public String getAll(){
          System.out.println("book getAll...");
          return "{'module':'book getAll'}";
      }

  }
```

最终创建好的项目结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/5b44ce7f1a036cdc491a1a8e61d8297d.png)

#### 5.2.2 思路分析

> **需求:**将之前的增删改查替换成RESTful的开发方式。
> 
> 1.之前不同的请求有不同的路径,现在要将其修改为统一的请求路径
> 
> 修改前: 新增: /save ,修改: /update,删除 /delete...
> 
> 修改后: 增删改查: /users
> 
> 2.根据GET查询、POST新增、PUT修改、DELETE删除对方法的请求方式进行限定
> 
> 3.发送请求的过程中如何设置请求参数?

#### 5.2.3 代码实现，@RequestMapping的method属性，@PathVariable

> **了解即可**，主要用5.3的优化方案 

**新增**

```java
@Controller
public class UserController {
    //设置当前请求方法为POST，表示REST风格中的添加操作
    @RequestMapping(value = "/users",method = RequestMethod.POST)
    @ResponseBody
    public String save() {
        System.out.println("user save...");
        return "{'module':'user save'}";
    }
}
```

-   将请求路径更改为`/users`
    
    -   访问该方法使用 POST: `http://localhost/users`
-   使用method属性限定该方法的访问方式为`POST`
    
    -   **如果发送的不是POST请求**，比如发送GET请求，**则会报错**
        
        ![](https://i-blog.csdnimg.cn/blog_migrate/633c2256d63b8729b318ee3e94e4337f.png)
        

**删除**

> **先不传递路径参数删除**
> 
> ```java
> @Controller
> public class UserController {
>     //设置当前请求方法为DELETE，表示REST风格中的删除操作
>     @RequestMapping(value = "/users",method = RequestMethod.DELETE)
>     @ResponseBody
>     public String delete(Integer id) {
>         System.out.println("user delete..." + id);
>         return "{'module':'user delete'}";
>     }
> }
> ```
> 
> -   将请求路径更改为`/users`
>     -   访问该方法使用 DELETE: `http://localhost/users`
> 
> 访问成功，但是删除方法没有携带所要删除数据的id,所以针对RESTful的开发，如何携带数据参数?

**传递路径参数删除，@PathVariable**

**@PathVariable**译作可变路径，**作用是声明这个参数来自于路径。**

前端发送请求的时候使用:`http://localhost/users/1`,路径中的`1`就是我们想要传递的参数。

后端获取参数，需要做如下修改:

-   修改@RequestMapping的value属性，将其中修改为`/users/{id}`，目的是和路径匹配
-   在方法的形参前添加@PathVariable注解

```java
@Controller
public class UserController {
    //设置当前请求方法为DELETE，表示REST风格中的删除操作
    @RequestMapping(value = "/users/{id}",method = RequestMethod.DELETE)
    @ResponseBody
    //@PathVariable声明此参数来自于路径。使参数和@RequestMapping中路径中的参数绑定。如果名称不一样，需要起别名再绑定
    public String delete(@PathVariable Integer id) {
        System.out.println("user delete..." + id);
        return "{'module':'user delete'}";
    }
}
```

> **思考:**
> 
> **(1)如果方法形参的名称和路径`{}`中的值不一致，该怎么办?**
> 
> **答：起别名。**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/1068f4f2b0b1b272f1860739fb6ebcc7.png)
> 
> **(2)如果有多个参数需要传递该如何编写?**
> 
> **答：路径后加斜杠新增参数。**
> 
> 前端发送请求的时候使用:`http://localhost/users/1/tom`,路径中的`1`和`tom`就是我们想要传递的两个参数。
> 
> 后端获取参数，需要做如下修改:
> 
> ```java
> @Controller
> public class UserController {
>     //设置当前请求方法为DELETE，表示REST风格中的删除操作
>     @RequestMapping(value = "/users/{id}/{name}",method = RequestMethod.DELETE)
>     @ResponseBody
>     public String delete(@PathVariable Integer id,@PathVariable String name) {
>         System.out.println("user delete..." + id+","+name);
>         return "{'module':'user delete'}";
>     }
> }
> ```

**修改**

```java
@Controller
public class UserController {
    //设置当前请求方法为PUT，表示REST风格中的修改操作
    @RequestMapping(value = "/users",method = RequestMethod.PUT)
    @ResponseBody
    public String update(@RequestBody User user) {
        System.out.println("user update..." + user);
        return "{'module':'user update'}";
    }
}
```

-   将请求路径更改为`/users`
    
    -   访问该方法使用 PUT: `http://localhost/users`
-   访问并携带参数:
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/1f1ee4cecc47cf49b59b696d8404f679.png)
    

**根据ID查询**

```java
@Controller
public class UserController {
    //设置当前请求方法为GET，表示REST风格中的查询操作
    @RequestMapping(value = "/users/{id}" ,method = RequestMethod.GET)
    @ResponseBody
    public String getById(@PathVariable Integer id){
        System.out.println("user getById..."+id);
        return "{'module':'user getById'}";
    }
}
```

将请求路径更改为`/users`

-   访问该方法使用 GET: `http://localhost/users/666`

**查询所有**

```java
@Controller
public class UserController {
    //设置当前请求方法为GET，表示REST风格中的查询操作
    @RequestMapping(value = "/users" ,method = RequestMethod.GET)
    @ResponseBody
    public String getAll() {
        System.out.println("user getAll...");
        return "{'module':'user getAll'}";
    }
}
```

将请求路径更改为`/users`

-   访问该方法使用 GET: `http://localhost/users`

> **小结**
> 
> RESTful入门案例，我们需要学习的内容如下:
> 
> (1)设定Http**请求动作**(动词)
> 
> **@RequestMapping**(value="",**method** = RequestMethod.**POST|GET|PUT|DELETE**)
> 
> (2)设定**请求参数**(路径变量)
> 
> @RequestMapping(value="/users/**{id}**",method = RequestMethod.DELETE)
> 
> @ReponseBody
> 
> public String delete(**@PathVariable** Integer **id**){
> 
> }

#### 5.2.4 目前学的参数占位符汇总

-   **mysql：**参数占位符${}（有sql注入问题）和#{} 
    
    ```java
        @Insert("insert into tbl_book values (null,#{type},#{name},#{description})")
        public void save(Book book);
    ```
    
-    **jsp中EL表达式：**参数占位符${}
    
    ```html
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
    </head>
    <body>
        ${brands}
    </body>
    </html>
    ```
    
-   **Vue：**参数占位符{{}}
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    <div id="app">
        <input v-model="username"><br>
        <!--插值表达式-->
        input里的值是：{{username}}
    </div>
    <script src="js/vue.js"></script>
    <script>
        //1. 创建Vue核心对象
        new Vue({
            el:"#app",
            data(){  // data() 是 ECMAScript 6 版本的新的写法
                return {
                    username:"默认值"
                }
            }
     
            /*data: function () {
                return {
                    username:""
                }
            }*/
        });
     
    </script>
    </body>
    </html>
    ```
    
-   **Spring的JdbcConfig注入properties：**参数占位符${}。记得SpringConfig的@PropertySource("jdbc.properties")
    
    ```java
        @Value("${jdbc.driver}")
        private String driver;
    ```
    
-   **SpringMVC的@RequestMapping或@PostMapping路径：**参数占位符{}
    
    ```java
        @DeleteMapping("/{id}")
        public String delete(@PathVariable Integer id){
            System.out.println("book delete..." + id);
            return "{'module':'book delete'}";
        }
    ```
    

#### 知识点@PathVariable

| 名称 | @PathVariable |
| --- | --- |
| 类型 | **形参注解** |
| 位置 | SpringMVC控制器方法形参定义前面 |
| 作用 | 绑定路径参数与处理器方法形参间的关系，要求路径参数名与形参名一一对应 |

### 5.2.5 区别：`@RequestBody`、`@RequestParam`、`@PathVariable`

关于接收参数，我们学过三个注解`@RequestBody`、`@RequestParam`、`@PathVariable`,这三个注解之间的区别和应用分别是什么?

-   **联系：**都是参数注解，都用于前端到controller的参数传递。 
-   **区别**
    -   **@RequestParam**用于**接收非JSON参数，除集合外其他类型都可以省略**，可以**起别名**。如果实参是集合则必须加这个注解。
        
        ```java
        @RequestMapping("/commonParamDifferentName")
            @ResponseBody
            public String commonParamDifferentName(@RequestParam("name") String userName , int age){
                System.out.println("普通参数传递 userName ==> "+userName);
                System.out.println("普通参数传递 age ==> "+age);
                return "{'module':'common param different name'}";
            }
        ```
        
        ```java
        //集合参数：同名请求参数可以使用@RequestParam注解映射到对应名称的集合对象中作为数据
        @RequestMapping("/listParam")
        @ResponseBody
        public String listParam(@RequestParam List<String> likes){
            System.out.println("集合参数传递 likes ==> "+ likes);
            return "{'module':'list param'}";
        }
        ```
        
    -   **@RequestBody**用于**接收json数据**（请求体参数），必须加上才能获取到前端传来的JSON数据。
        
        ```java
        @RequestMapping("/pojoParamForJson")
        @ResponseBody
        public String pojoParamForJson(@RequestBody User user){
            System.out.println("pojo(json)参数传递 user ==> "+user);
            return "{'module':'pojo for json param'}";
        }
        ```
        
    -   **@PathVariable**用于**接收路径参数**，**REST风格。**使用{参数名称}描述路径参数
        
        ```java
        @Controller
        public class UserController {
            //设置当前请求方法为GET，表示REST风格中的查询操作
            @RequestMapping(value = "/users/{id}" ,method = RequestMethod.GET)
            @ResponseBody
            public String getById(@PathVariable Integer id){
                System.out.println("user getById..."+id);
                return "{'module':'user getById'}";
            }
        }
        ```
        
-   **应用**
    -   后期开发中，发送请求参数超过1个时，**以json格式为主**，**@RequestBody**应用较广
    -   如果发送非json格式数据，选用@RequestParam接收请求参数
    -   采用**RESTful**进行开发，当参数数量较少时，例如1个，可以采用**@PathVariable**接收请求路径变量，通常用于**传递id值**

### 5.3 RESTful优化，快速开发

#### 5.3.1 概述，@RestController，@GetMapping  

**结论：**

**@RestController合并**@Controller和@ResponseBody

@GetMapping  @PostMapping  @PutMapping  @DeleteMapping**代替**@RequestMapping

> **RESTful开发麻烦的地方：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/b06b55cff9c28ddb8033ffd31b9a06fc.png)
> 
> **问题1：**每个方法的@RequestMapping注解中都定义了访问路径**/books**，**重复**性太高。
> 
> **问题2：**每个方法的@RequestMapping注解中都要使用**method**属性定义请求方式，**重复**性太高。
> 
> **问题3：**每个方法响应json都需要加上**@ResponseBody**注解，**重复**性太高。

**问题解决：**

```java
@RestController //@Controller + ReponseBody
@RequestMapping("/books")
public class BookController {

    //@RequestMapping(method = RequestMethod.POST)
    @PostMapping
    public String save(@RequestBody Book book){
        System.out.println("book save..." + book);
        return "{'module':'book save'}";
    }

    //@RequestMapping(value = "/{id}",method = RequestMethod.DELETE)
    @DeleteMapping("/{id}")
    public String delete(@PathVariable Integer id){
        System.out.println("book delete..." + id);
        return "{'module':'book delete'}";
    }

    //@RequestMapping(method = RequestMethod.PUT)
    @PutMapping
    public String update(@RequestBody Book book){
        System.out.println("book update..." + book);
        return "{'module':'book update'}";
    }

    //@RequestMapping(value = "/{id}",method = RequestMethod.GET)
    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println("book getById..." + id);
        return "{'module':'book getById'}";
    }

    //@RequestMapping(method = RequestMethod.GET)
    @GetMapping
    public String getAll(){
        System.out.println("book getAll...");
        return "{'module':'book getAll'}";
    }

}
```

对于刚才的问题，我们都有对应的解决方案：

**问题1：**每个方法的@RequestMapping注解中都定义了**访问路径/books**，**重复**性太高。

```
将@RequestMapping提到类上面，将@Controller和@RequestMapping合并为@RestController，用来定义所有方法共同的访问路径。
```

**问题2：**每个方法的@RequestMapping注解中都要使用**method**属性定义**请求方式**，**重复**性太高。

```
使用@GetMapping  @PostMapping  @PutMapping  @DeleteMapping代替
```

**问题3：**每个方法响应json都需要加上**@ResponseBody注解**，**重复**性太高。

```
1.将ResponseBody提到类上面，让所有的方法都有@ResponseBody的功能，即返回值是响应体，而不是路径
2.使用@RestController注解替换@Controller与@ResponseBody注解，简化书写
```

#### **知识点@RestController@GetMapping @PostMapping @PutMapping @DeleteMapping**

**知识点1：@RestController**

| 名称 | @RestController |
| --- | --- |
| 类型 | **类注解** |
| 位置 | 基于SpringMVC的RESTful开发控制器类定义上方 |
| 作用 | 设置当前控制器类为RESTful风格，  
等同于@Controller与@ResponseBody两个注解组合功能 |

**知识点2：@GetMapping @PostMapping @PutMapping @DeleteMapping**

| 名称 | @GetMapping @PostMapping @PutMapping @DeleteMapping |
| --- | --- |
| 类型 | **方法注解** |
| 位置 | 基于SpringMVC的RESTful开发控制器方法定义上方 |
| 作用 | 设置当前控制器方法请求访问路径与请求动作，每种对应一个请求动作，  
例如@GetMapping对应GET请求 |
| 相关属性 | value（默认）：请求访问路径 |

### 5.4 RESTful案例

#### 5.4.1 需求分析

**需求一:假数据图片列表查询**，从后台返回数据，将数据展示在页面上

![](https://i-blog.csdnimg.cn/blog_migrate/a149d7fff6bbea6db49fc446d1ff00c3.png)

**需求二:新增图片**，将新增图书的数据传递到后台，并在控制台打印

![](https://i-blog.csdnimg.cn/blog_migrate/187b2d5f4acd4bffaac28cce524240d3.png)

**说明:**此次案例的重点是在SpringMVC中如何使用RESTful实现前后台交互，所以本案例并没有和数据库进行交互，所有数据使用**`假`数据**来完成开发。

步骤分析:

> 1.搭建项目导入jar包
> 
> 2.编写Controller类，提供两个方法，一个用来做列表查询，一个用来做新增
> 
> 3.在方法上使用RESTful进行路径设置
> 
> 4.完成请求、参数的接收和结果的响应
> 
> 5.使用PostMan进行测试
> 
> 6.将前端页面拷贝到项目中
> 
> 7.页面发送ajax请求
> 
> 8.完成页面数据的展示

#### 5.4.2 环境准备

-   创建一个Web的Maven项目
    
-   pom.xml添加SpringMVC三大依赖javax.servlet-api,spring-webmvc,jackson-databind
    
    ```XML
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
    
      <groupId>com.itheima</groupId>
      <artifactId>springmvc_07_rest_case</artifactId>
      <version>1.0-SNAPSHOT</version>
      <packaging>war</packaging>
    
      <dependencies>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>3.1.0</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.2.10.RELEASE</version>
        </dependency>
        <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-databind</artifactId>
          <version>2.9.0</version>
        </dependency>
      </dependencies>
    
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.1</version>
            <configuration>
              <port>80</port>
              <path>/</path>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    ```
    

创建对应的配置类

```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }

      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }

      protected String[] getServletMappings() {
          return new String[]{"/"};
      }

      //乱码处理
      @Override
      protected Filter[] getServletFilters() {
          CharacterEncodingFilter filter = new CharacterEncodingFilter();
          filter.setEncoding("UTF-8");
          return new Filter[]{filter};
      }
  }

  @Configuration
  @ComponentScan("com.itheima.controller")
  //开启json数据类型自动转换
  @EnableWebMvc
  public class SpringMvcConfig {
  }
```

编写模型类Book

```java
  public class Book {
      private Integer id;
      private String type;
      private String name;
      private String description;
      //setter...getter...toString略
  }
```

**编写BookController**

```java
  @Controller
  public class BookController {


  }
```

最终创建好的项目结构如下:

![](https://i-blog.csdnimg.cn/blog_migrate/a7bbc3206a49762e2c1cf8853989d05b.png)

#### 5.4.2 后台接口开发

**步骤1:编写Controller类并使用RESTful进行配置**

```java
@RestController
@RequestMapping("/books")
public class BookController {

    @PostMapping
    public String save(@RequestBody Book book){
        System.out.println("book save ==> "+ book);
        return "{'module':'book save success'}";
    }

     @GetMapping
    public List<Book> getAll(){
        System.out.println("book getAll is running ...");
        List<Book> bookList = new ArrayList<Book>();

        Book book1 = new Book();
        book1.setType("计算机");
        book1.setName("SpringMVC入门教程");
        book1.setDescription("小试牛刀");
        bookList.add(book1);

        Book book2 = new Book();
        book2.setType("计算机");
        book2.setName("SpringMVC实战教程");
        book2.setDescription("一代宗师");
        bookList.add(book2);

        Book book3 = new Book();
        book3.setType("计算机丛书");
        book3.setName("SpringMVC实战教程进阶");
        book3.setDescription("一代宗师呕心创作");
        bookList.add(book3);

        return bookList;
    }

}
```

**步骤2：先测试后端，再开发前端。PostMan测试**

测试新增

```java
{
    "type":"计算机丛书",
    "name":"SpringMVC终极开发",
    "description":"这是一本好书"
}
```

![](https://i-blog.csdnimg.cn/blog_migrate/1bd80d38b8b32a0cfda7008439b9fbee.png)

测试查询

![](https://i-blog.csdnimg.cn/blog_migrate/0708dc1593de6322dde526eef96ebcbe.png)

#### 5.4.3 放行静态页面，WebMvcConfigurer配置类添加资源处理器

**步骤1:拷贝静态页面**

将资料\\功能页面 拷贝到项目的`webapp`目录下

![](https://i-blog.csdnimg.cn/blog_migrate/8cb16ad92cf6e3880ec7ec5acc89c8a9.png)

**步骤2:访问pages目录下的books.html，springmvc对静态资源放行，SpringMvcSupport配置类**

打开浏览器输入`http://localhost/pages/books.html`

![](https://i-blog.csdnimg.cn/blog_migrate/2bb31f344539fb88937136b2e7edddcd.png)

**(1)出现错误的原因?**

![](https://i-blog.csdnimg.cn/blog_migrate/8f0b1b5f39c00955b599f8ea52c6e36a.png)

**报错原因：SpringMVC拦截了静态资源**，根据/pages/books.html去controller找对应的方法，找不到所以会报404的错误。静态资源应该交给Tomcat处理，而不是springmvc处理。

**(2)SpringMVC为什么会拦截静态资源呢?**

![](https://i-blog.csdnimg.cn/blog_migrate/f93290b109315ce67c68115394954786.png)

**(3)解决方案：**SpringMVC将**静态资源进行放行**。

使用资源处理器，当访问**请求路径**/pages/????时候，从**文件**/pages目录下查找内容。

> 两种方法，主要用方法二。

> **方法一：麻烦底层（了解）**
> 
> **①创建 SpringMvcSupport 配置类**，设置静态资源访问过滤。
> 
> 继承WebMvcConfigurationSupport 类，重写addResourceHandlers方法。
> 
> ```java
> //注意有@Configuration，注解设为配置类。现在学到的配置类就它和springmvc和spring配置类有@Configuration
> @Configuration
> //继承webmvc配置支持类WebMvcConfigurationSupport
> public class SpringMvcSupport extends WebMvcConfigurationSupport {
>     //设置静态资源访问过滤，当前类需要设置为配置类，并被扫描加载
>     @Override
>     //addResourceHandlers译为添加资源处理器
>     protected void addResourceHandlers(ResourceHandlerRegistry registry) {
>         //addResourceHandler("/pages/**")是拦截请求路径，addResourceLocations("/pages/")是映射到文件真实地址。这样就可以让别人访问服务器的本地文件了
>         //当访问请求路径/pages/????时候，从文件/pages目录下查找内容。注意addResourceHandler里两个通配符，addResourceLocations后面是斜杠没通配符
>         registry.addResourceHandler("/pages/**").addResourceLocations("/pages/");
>         //当访问/js/????时候，从/js目录下查找内容
>         registry.addResourceHandler("/js/**").addResourceLocations("/js/");
>         registry.addResourceHandler("/css/**").addResourceLocations("/css/");
>         registry.addResourceHandler("/plugins/**").addResourceLocations("/plugins/");
>     }
> }
> ```
> 
> **②SpringMvcConfig扫描SpringMvcSupport配置类**
> 
> 注意：**SpringMvcSupport** 配置类是在config目录下，SpringMVC扫描的是controller包，所以该配置类还未生效，要想生效需要将SpringMvcConfig配置类进行修改
> 
> ```java
> @Configuration
> @ComponentScan({"com.itheima.controller","com.itheima.config"})
> @EnableWebMvc
> public class SpringMvcConfig {
> }
> 
> 或者
> 
> @Configuration
> @ComponentScan("com.itheima")
> @EnableWebMvc
> public class SpringMvcConfig {
> }
> ```

 **方法二：简单快速（推荐）**

 **SpringMvcConfig 实现WebMvcConfigurer 接口**，既**可以添加资源处理器**，也可以**添加拦截器**，拦截器在下一章ssm整合中具体讲。既然不用config的SpringMvcSupport了，springmvc配置类也就不用扫描config目录了

```java
@Configuration
@ComponentScan({"package1.controller"})
@EnableWebMvc
public class SpringMvcConfig implements WebMvcConfigurer {
    @Autowired
    private ProjectInterception projectInterception;
    //添加拦截器，配置本地资源映射路径，在访问A（虚拟的）的时候，需要到B（实际的）的位置去访问。
//    @Override
//    public void addInterceptors(InterceptorRegistry registry) {
//        registry.addInterceptor(projectInterception).addPathPatterns("/books","/books/*");
        //如果只拦截/books，发送http://localhost/books/100后会发现拦截器没有被执行
        //registry.addInterceptor(projectInterceptor).addPathPatterns("/books");
//    }
    //添加资源处理器
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/pages/**").addResourceLocations("/pages/");
        registry.addResourceHandler("/js/**").addResourceLocations("/js/");
        registry.addResourceHandler("/css/**").addResourceLocations("/css/");
        registry.addResourceHandler("/plugins/**").addResourceLocations("/plugins/");

    }
}
```

> 使用资源处理器，当访问**请求路径**/pages/????时候，从**文件**/pages目录下查找内容。

**步骤3:修改books.html页面**

```html
<!DOCTYPE html>

<html>
    <head>
        <!-- 页面meta -->
        <meta charset="utf-8">
        <title>SpringMVC案例</title>
        <!-- 引入样式 -->
        <link rel="stylesheet" href="../plugins/elementui/index.css">
        <link rel="stylesheet" href="../plugins/font-awesome/css/font-awesome.min.css">
        <link rel="stylesheet" href="../css/style.css">
    </head>

    <body class="hold-transition">

        <div id="app">

            <div class="content-header">
                <h1>图书管理</h1>
            </div>

            <div class="app-container">
                <div class="box">
                    <div class="filter-container">
                        <el-input placeholder="图书名称" style="width: 200px;" class="filter-item"></el-input>
                        <el-button class="dalfBut">查询</el-button>
                        <el-button type="primary" class="butT" @click="openSave()">新建</el-button>
                    </div>

                    <el-table size="small" current-row-key="id" :data="dataList" stripe highlight-current-row>
                        <el-table-column type="index" align="center" label="序号"></el-table-column>
                        <el-table-column prop="type" label="图书类别" align="center"></el-table-column>
                        <el-table-column prop="name" label="图书名称" align="center"></el-table-column>
                        <el-table-column prop="description" label="描述" align="center"></el-table-column>
                        <el-table-column label="操作" align="center">
                            <template slot-scope="scope">
                                <el-button type="primary" size="mini">编辑</el-button>
                                <el-button size="mini" type="danger">删除</el-button>
                            </template>
                        </el-table-column>
                    </el-table>

                    <div class="pagination-container">
                        <el-pagination
                            class="pagiantion"
                            @current-change="handleCurrentChange"
                            :current-page="pagination.currentPage"
                            :page-size="pagination.pageSize"
                            layout="total, prev, pager, next, jumper"
                            :total="pagination.total">
                        </el-pagination>
                    </div>

                    <!-- 新增标签弹层 -->
                    <div class="add-form">
                        <el-dialog title="新增图书" :visible.sync="dialogFormVisible">
                            <el-form ref="dataAddForm" :model="formData" :rules="rules" label-position="right" label-width="100px">
                                <el-row>
                                    <el-col :span="12">
                                        <el-form-item label="图书类别" prop="type">
                                            <el-input v-model="formData.type"/>
                                        </el-form-item>
                                    </el-col>
                                    <el-col :span="12">
                                        <el-form-item label="图书名称" prop="name">
                                            <el-input v-model="formData.name"/>
                                        </el-form-item>
                                    </el-col>
                                </el-row>
                                <el-row>
                                    <el-col :span="24">
                                        <el-form-item label="描述">
                                            <el-input v-model="formData.description" type="textarea"></el-input>
                                        </el-form-item>
                                    </el-col>
                                </el-row>
                            </el-form>
                            <div slot="footer" class="dialog-footer">
                                <el-button @click="dialogFormVisible = false">取消</el-button>
                                <el-button type="primary" @click="saveBook()">确定</el-button>
                            </div>
                        </el-dialog>
                    </div>

                </div>
            </div>
        </div>
    </body>

    <!-- 引入组件库 -->
    <script src="../js/vue.js"></script>
    <script src="../plugins/elementui/index.js"></script>
    <script type="text/javascript" src="../js/jquery.min.js"></script>
    <script src="../js/axios-0.18.0.js"></script>

    <script>
        var vue = new Vue({

            el: '#app',

            data:{
                dataList: [],//当前页要展示的分页列表数据
                formData: {},//表单数据
                dialogFormVisible: false,//增加表单是否可见
                dialogFormVisible4Edit:false,//编辑表单是否可见
                pagination: {},//分页模型数据，暂时弃用
            },

            //钩子函数，VUE对象初始化完成后自动执行
            created() {
                this.getAll();
            },

            methods: {
                // 重置表单
                resetForm() {
                    //清空输入框
                    this.formData = {};
                },

                // 弹出添加窗口
                openSave() {
                    this.dialogFormVisible = true;
                    this.resetForm();
                },

                //添加
                saveBook () {
                    axios.post("/books",this.formData).then((res)=>{

                    });
                },

                //主页列表查询
                getAll() {
                    axios.get("/books").then((res)=>{
                        this.dataList = res.data;
                    });
                },

            }
        })
    </script>
</html>
```