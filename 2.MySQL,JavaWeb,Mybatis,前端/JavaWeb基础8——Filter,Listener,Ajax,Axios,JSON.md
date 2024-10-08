>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1，Filter过滤器](#1%EF%BC%8CFilter)

[1.1 Filter概述](#1.1%20Filter%E6%A6%82%E8%BF%B0)

[1.2 Filter快速入门](#1.2%20Filter%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)

[1.2.1 开发步骤](#1.2.1%20%E5%BC%80%E5%8F%91%E6%AD%A5%E9%AA%A4)

[1.2.2 代码演示](#1.2.2%20%E4%BB%A3%E7%A0%81%E6%BC%94%E7%A4%BA)

[1.2.5 登录拦截标准代码](#1.2.5%C2%A0%E7%99%BB%E5%BD%95%E6%8B%A6%E6%88%AA%E6%A0%87%E5%87%86%E4%BB%A3%E7%A0%81)

[1.3 Filter执行流程](#1.3%20Filter%E6%89%A7%E8%A1%8C%E6%B5%81%E7%A8%8B)

[1.4 Filter拦截路径配置](#1.4%20Filter%E6%8B%A6%E6%88%AA%E8%B7%AF%E5%BE%84%E9%85%8D%E7%BD%AE)

[1.5 过滤器链](#1.5%20%E8%BF%87%E6%BB%A4%E5%99%A8%E9%93%BE)

[1.6 案例，优化商品展示项目未登录拦截](#1.6%20%E6%A1%88%E4%BE%8B)

[2，Listener监听器](#2%EF%BC%8CListener)

[2.1 概述](#2.1%20%E6%A6%82%E8%BF%B0)

[2.2 分类](#2.2%20%E5%88%86%E7%B1%BB)

[2.3 代码演示](#2.3%20%E4%BB%A3%E7%A0%81%E6%BC%94%E7%A4%BA)

[3，AJAX](#3%EF%BC%8CAjax)

[3.1 概述](#3.1%20%E6%A6%82%E8%BF%B0)

[3.2 同步、异步优点和使用场景](#3.1.2%20%E5%90%8C%E6%AD%A5%E5%92%8C%E5%BC%82%E6%AD%A5)

[3.3. 快速入门](#3.2%20%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)

[3.4 案例，AJAX校验用户名是否已存在](#3.3%20%E6%A1%88%E4%BE%8B)

[4，Axios异步框架](#4%EF%BC%8Caxios)

[4.1 概述](#%E6%A6%82%E8%BF%B0%C2%A0) 

[4.2 axios基本使用](#4.1%20%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8)

[4.2.1 引入js文件、发送请求](#%E5%BC%95%E5%85%A5%E5%92%8C%E5%8F%91%E9%80%81%E8%AF%B7%E6%B1%82)

[4.2.2 请求方法别名方式发请求](#4.3%20%E8%AF%B7%E6%B1%82%E6%96%B9%E6%B3%95%E5%88%AB%E5%90%8D)

[4.3 快速入门，请求用户名](#4.2%20%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)

[5，JSON](#5%EF%BC%8CJSON)

[5.1 概述](#5.1%20%E6%A6%82%E8%BF%B0)

[5.2 JSON 基础语法](#5.2%20JSON%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95)

[5.2.1 定义格式](#5.2.1%20%E5%AE%9A%E4%B9%89%E6%A0%BC%E5%BC%8F)

 [5.2.2 js和JSON转换](#%C2%A05.2.2%C2%A0js%E5%92%8CJSON%E8%BD%AC%E6%8D%A2)

[5.2.3 axios携带JSON发送异步请求](#5.2.3%20%E5%8F%91%E9%80%81%E5%BC%82%E6%AD%A5%E8%AF%B7%E6%B1%82%E6%90%BA%E5%B8%A6%E5%8F%82%E6%95%B0)

[5.3 Fastjson，JSON串和Java对象的转换](#5.3%20JSON%E4%B8%B2%E5%92%8CJava%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%9B%B8%E4%BA%92%E8%BD%AC%E6%8D%A2)

[6，案例，Axios + JSON 品牌列表查询和添加](#6%EF%BC%8C%E6%A1%88%E4%BE%8B)

[6.0 需求](#6.1%20%E9%9C%80%E6%B1%82)

[6.1 坑点](#6.1%20%E5%9D%91%E7%82%B9)

[6.2 查询所有功能](#6.2%20%E6%9F%A5%E8%AF%A2%E6%89%80%E6%9C%89%E5%8A%9F%E8%83%BD)

[6.3 添加品牌功能，异步提交表单](#6.3%20%E6%B7%BB%E5%8A%A0%E5%93%81%E7%89%8C%E5%8A%9F%E8%83%BD)

--

## 1，Filter过滤器

### 1.1 Filter概述

Filter 表示**过滤器**，是 **JavaWeb 三大组件(Servlet、Filter、Listener)**之一。

主要对配置的拦截路径页面进行拦截，先运行拦截页面代码，放行后再运行原页面，之后再回到Filter页面执行剩余代码。

**作用：**

过滤器可以把对资源的请求**拦截**下来，从而实现一些特殊的功能。

如下图所示，浏览器可以访问服务器上的所有的资源（servlet、jsp、html等）

![](https://i-blog.csdnimg.cn/blog_migrate/6248b3981b77670a06eb0ca27c645cfc.png)

而在访问到这些资源之前可以使过滤器拦截来下，也就是说在访问资源之前会先经过 Filter，如下图

![](https://i-blog.csdnimg.cn/blog_migrate/54bdc476f6caf61095d8c2f29d1bb42e.png)

**拦截器拦截到后可以做什么功能呢？**

过滤器一般完成一些通用的操作，比如**权限控制、统一字符编码、敏感字符处理。**

当每个资源都要写一些代码完成某个功能时，为了实现代码复用，我们可以将这些代码写在过滤器中，因为请求每一个资源都要经过过滤器。

> **举例：** 
> 
> 比如进入商品展示页面，用户如果登陆过了就跳转到品牌数据展示的页面；如果没有登陆就跳转到登陆页面让用户进行登陆。
> 
> 要实现这个效果需要在每一个资源中都写上这段逻辑，而像这种**通用的操作**，我们就可以放在过滤器中进行实现。
> 
> 这个就是**权限控制**，以后我们还会进行**细粒度权限控制**。过滤器还可以做 **`统一编码处理`、 `敏感字符处理`** 等等…

### 1.2 Filter快速入门

#### 1.2.1 开发步骤

进行 `Filter` 开发分成以下三步实现

**1.定义类，实现 Filter接口**，并重写其所有方法。**注意**导Filter包要选javax.servlet

**2.配置Filter拦截资源的路径：**在类上定义 `@WebFilter` 注解。而注解的 `value` 属性值 `/*` 表示拦截所有的资源

**3.在doFilter方法中输出**一句话，并放行

```java
package web.filter;

import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import java.io.IOException;
@WebFilter("/*")
public class FilterDemo implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("filter demo...");
        //放行
        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

> 上述代码中的 `chain.doFilter(request,response);` 就是放行，也就是让其访问本该访问的资源。

也可以快速创建，跟创建Servlet一样，要先在项目结构facet设置源根：

![](https://i-blog.csdnimg.cn/blog_migrate/6110aae512b61cf7c43fe05970f8bf34.png)

#### 1.2.2 代码演示

创建一个项目，项目下有一个 `hello.jsp` 页面，项目结构如下：

![](https://i-blog.csdnimg.cn/blog_migrate/2dcdc47570d01aad4ef8bba9aa9545e9.png)

`pom.xml` 配置文件内容如下：导入依赖Servlet、插件Tomcat

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>filter-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
                <configuration>
                    <port>80</port>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

`hello.jsp` 页面内容如下：

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>hello JSP~</h1>
</body>
</html>
```

接下来编写过滤器。过滤器是 Web 三大组件之一，所以我们将 `filter` 创建在 `com.itheima.web.filter` 包下，起名为 `FilterDemo`

```java
@WebFilter("/*")
public class FilterDemo implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("FilterDemo...");
    }

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
    }

    @Override
    public void destroy() {
    }
}
```

​

重启启动服务器，再次重新访问 `hello.jsp` 页面，这次发现页面没有任何效果，但是在 `idea` 的控制台可以看到如下内容![](https://i-blog.csdnimg.cn/blog_migrate/e9065b8111d7e37d215f97e35cf83dcb.png)

上述效果说明 `FilterDemo` 这个过滤器的 `doFilter()` 方法执行了，但是没有放行，所以jsp页面是空白的。

必须在 `doFilter()` 方法中添加**放行的方法**才能访问到 `hello.jsp` 页面。

**放行的代码**

```java
//放行
 chain.doFilter(request,response);
```

再次重启服务器并访问 `hello.jsp` 页面，发现这次就可以在浏览器上看到页面效果。

**`FilterDemo` 过滤器完整代码如下：**

```java
@WebFilter("/*")
public class FilterDemo implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("1.FilterDemo...");
        //放行
        chain.doFilter(request,response);
    }

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
    }

    @Override
    public void destroy() {
    }
}
```

放行后jsp页面就可以打开了。 

### 1.2.5 登录拦截标准代码

```java
//坑点，路径是"/*"，别忘了*
@WebFilter(filterName = "loginCheckFilter",urlPatterns = "/*")
@Slf4j
public class LoginCheckFilter implements Filter{
    //路径匹配器，支持通配符，别忘了
    public static final AntPathMatcher PATH_MATCHER = new AntPathMatcher();
 
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        //0.要先把请求响应ServletXxx转成它的子接口HttpServletXxx，从而多了一些针对于Http协议的方法
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        HttpServletResponse response = (HttpServletResponse) servletResponse;
 
        //1、获取本次请求的URI
        String requestURI = request.getRequestURI();// /backend/index.html
 
        log.info("拦截到请求：{}",requestURI);
 
        //定义不需要处理的请求路径，前端页面可以放行，只是除登录登出的后端拦截就行。
        String[] urls = new String[]{
                "/employee/login",
                "/employee/logout",
                "/backend/**",
                "/front/**"
        };
 
 
        //2、判断本次请求是否需要处理
        boolean check = check(urls, requestURI);
 
        //3、如果不需要处理，则直接放行
        if(check){
            log.info("本次请求{}不需要处理",requestURI);
            filterChain.doFilter(request,response);
            return;
        }
 
        //4、判断登录状态，如果已登录，则直接放行
        if(request.getSession().getAttribute("employee") != null){
            log.info("用户已登录，用户id为：{}",request.getSession().getAttribute("employee"));
            filterChain.doFilter(request,response);
            return;
        }
 
        log.info("用户未登录");
        //5、如果未登录则返回未登录结果，通过输出流方式向客户端页面响应数据
        //必须错误信息NOTLOGIN，因为前端根据msg==“NOTLOGIN”和code==0判断未登录
        response.getWriter().write(JSON.toJSONString(R.error("NOTLOGIN")));
        return;
 
    }
 
    /**
     * 路径匹配，检查本次请求是否需要放行
     * @param urls
     * @param requestURI
     * @return
     */
    public boolean check(String[] urls,String requestURI){
        for (String url : urls) {
            //这里是坑点，不能用equals
            boolean match = PATH_MATCHER.match(url, requestURI);
            if(match){
                return true;
            }
        }
        return false;
    }
}
```

### 1.3 Filter执行流程

![](https://i-blog.csdnimg.cn/blog_migrate/b0129da79113d146a94847f305eeccc0.png)

**Filter的执行流程：**

放行会**携带request资源**访问对应资源，资源访问完成后， 会带着响应数据**回到Filter**中，**继续执行**下面的代码。

![](https://i-blog.csdnimg.cn/blog_migrate/0c0e9e76e0f0eb92f58416af7b08ccae.png)

> 回顾转发和重定向，1.转发执行后会继续执行转发语句下面的代码， 重定向是先执行完重定向前的所有代码，再跳转到新页面。
> 
> 2.转发携带request资源，重定向不携带，想携带要用问号追加在链接后面实现参数携带。

 **代码验证**

接下来我们通过代码验证一下，在 `doFilter()` 方法前后都加上输出语句，如下![](https://i-blog.csdnimg.cn/blog_migrate/158bbbcb66c72f519755d54a181cd332.png)

同时在 `hello.jsp` 页面加上输出语句，如下![](https://i-blog.csdnimg.cn/blog_migrate/d78a13aca7410400a64200f9f147141a.png)

执行访问该资源打印的顺序是按照我们标记的标号进行打印的话，说明我们上边总结出来的流程是没有问题的。启动服务器访问 `hello.jsp` 页面，在控制台打印的内容如下：![](https://i-blog.csdnimg.cn/blog_migrate/0959da51a8ea3f606476975f9adb9a00.png)

以后我们可以将**对请求进行处理的代码**放在**放行之前进行处理**，而如果请求完资源后还要对响应的数据进行处理时可以在放行后进行逻辑处理。

### 1.4 Filter拦截路径配置

拦截路径表示 Filter 会对请求的哪些资源进行拦截，使用 `@WebFilter` 注解进行配置。如：`@WebFilter("拦截路径")`

拦截路径有如下四种配置方式：

-   **拦截具体的资源：**/index.jsp：只有访问index.jsp时才会被拦截
    
-   目录拦截：/user/\*：访问/user下的所有资源，都会被拦截
    
-   后缀名拦截：\*.jsp：访问后缀名为jsp的资源，都会被拦截
    
-   拦截所有：/\*：访问所有资源，都会被拦截
    

通过上面拦截路径的学习，大家会发现拦截路径的配置方式和 **`Servlet`** 的请求资源路径配置**方式一样**，但是表示的**含义不同**。含义分别为拦截路径和项目访问路径。

> **回顾：Servlet的urlPattern配置规则**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/144895f8ae669021c9db91b83686f21c.png)

### 1.5 过滤器链

**1.5.1 概述**

过滤器链是指在一个Web应用，可以配置**多个过滤器**，这多个过滤器称为过滤器链。

过滤器链中的过滤器的优先级根据类名字母序排列。

如下图就是一个过滤器链，我们学习过滤器链主要是学习过滤器链执行的流程![](https://i-blog.csdnimg.cn/blog_migrate/7d07d660d95873957f68454efe7b748e.png)

上图中的过滤器链执行是按照以下**流程**执行：

1.  执行 `Filter1` 的放行前逻辑代码
    
2.  执行 `Filter1` 的放行代码
    
3.  执行 `Filter2` 的放行前逻辑代码
    
4.  执行 `Filter2` 的放行代码
    
5.  访问到资源
    
6.  执行 `Filter2` 的放行后逻辑代码
    
7.  执行 `Filter1` 的放行后逻辑代码
    

以上流程串起来就像一条链子，故称之为过滤器链。

**1.5.2 代码演示**

-   编写第一个过滤器 `FilterDemo` ，配置成拦截所有资源
    
    ```java
    @WebFilter("/*")
    //FilterDemo 字母序在FilterDemo2前，会优先拦截
    public class FilterDemo implements Filter {
    
        @Override
        public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
    
            //1. 放行前，对 request数据进行处理
            System.out.println("1.FilterDemo...");
            //放行
            chain.doFilter(request,response);
            //2. 放行后，对Response 数据进行处理
            System.out.println("3.FilterDemo...");
        }
    
        @Override
        public void init(FilterConfig filterConfig) throws ServletException {
        }
    
        @Override
        public void destroy() {
        }
    }
    ```
    
-   编写第二个过滤器 `FilterDemo2` ，配置拦截所有资源
    
    ```java
    @WebFilter("/*")
    public class FilterDemo2 implements Filter {
    
        @Override
        public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
    
            //1. 放行前，对 request数据进行处理
            System.out.println("2.FilterDemo...");
            //放行
            chain.doFilter(request,response);
            //2. 放行后，对Response 数据进行处理
            System.out.println("4.FilterDemo...");
        }
    
        @Override
        public void init(FilterConfig filterConfig) throws ServletException {
        }
    
        @Override
        public void destroy() {
        }
    }
    ```
    
    ​
    
-   修改 `hello.jsp` 页面中脚本的输出语句
    
    ```html
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <h1>hello JSP~</h1>
        <%
            System.out.println("3.hello jsp");
        %>
    </body>
    </html>
    ```
    
-   启动服务器，在浏览器输入 `http://localhost/filter-demo/hello.jsp` 进行测试，在控制台打印内容如下![](https://i-blog.csdnimg.cn/blog_migrate/4c8c7be942fd998a487b6c6ef77ce8d7.png)
    
    从结果可以看到确实是按照我们之前说的执行流程进行执行的。
    

**1.5.3 问题**

**为什么是先执行 `FilterDemo2` ，后执行 `FilterDemo2` 呢？**

我们现在使用的是注解配置Filter，而这种配置方式的**优先级**是按照**过滤器类名(字符串)的自然排序。**

比如有如下两个名称的过滤器 ： `BFilterDemo` 和 `AFilterDemo` 。那一定是 `AFilterDemo` 过滤器先执行。

### 1.6 案例，优化商品展示项目未登录拦截

**1.6.1 需求**

访问服务器资源时，需要先进行登录验证，如果没有登录，则自动跳转到登录页面

**1.6.2 分析**

创建过滤器拦截所有非登录注册相关资源，在过滤器中进行登陆状态校验即可。而在该 `Filter` 中逻辑如下：![](https://i-blog.csdnimg.cn/blog_migrate/429a5855f03af90dcaf2c26cc769ebf9.png)

 **注意：**一定要先判断拦截内容是不是登录注册相关资源，例如登录页面的css、js、img等资源要放行。

**1.6.3 代码实现**

**1.6.3.1 创建Filter**

在 `brand-demo` 工程创建 `com.itheima.web.filter` 包，在该下创建名为 `LoginFilter` 的过滤器

```java
@WebFilter("/*")
public class LoginFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws ServletException, IOException {
      
    }

    public void init(FilterConfig config) throws ServletException {
    }

    public void destroy() {
    }
}
```

**1.6.3.2 编写逻辑代码**

在 `doFilter()` 方法中编写登陆状态校验的逻辑代码。

我们首先需要从 `session` 对象中获取用户信息，但是 **`ServletRequest` 类型的 requset 对象没有获取 session 对象的方法**，所以此时需要将 request对象强转成 `HttpServletRequest` 对象。

```java
HttpServletRequest req = (HttpServletRequest) request;
```

然后完成以下逻辑

-   获取Session对象
    
-   从Session对象中获取名为 `user` 的数据
    
-   判断获取到的数据是否是 null
    
    -   如果不是，说明已经登陆，放行
        
    -   如果是，说明尚未登陆，将提示信息存储到域对象中并跳转到登陆页面
        

代码如下：

```java
@WebFilter("/*")
public class LoginFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws ServletException, IOException {
        HttpServletRequest req = (HttpServletRequest) request;
   
        //1. 判断session中是否有user
        HttpSession session = req.getSession();
        Object user = session.getAttribute("user");

        //2. 判断user是否为null
        if(user != null){
            // 登录过了
            //放行
            chain.doFilter(request, response);
        }else {
            // 没有登陆，存储提示信息，跳转到登录页面

            req.setAttribute("login_msg","您尚未登陆！");
            req.getRequestDispatcher("/login.jsp").forward(req,response);
        }
    }

    public void init(FilterConfig config) throws ServletException {
    }

    public void destroy() {
    }
}
```

**1.6.3.3 测试并抛出问题**

清除浏览器缓存后，在浏览器上输入 `http://localhost:8080/brand-demo/` ，可以看到如下页面效果：

![](https://i-blog.csdnimg.cn/blog_migrate/724b795e21b4e26f1e5ed5d46e249de0.png)

从上面效果可以看出没有登陆确实是跳转到登陆页面了，但是登陆页面为什么展示成这种效果了呢？

**1.6.3.4 问题分析及解决**

因为登陆页面需要 `css/login.css` 这个文件进行样式的渲染，下图是登陆页面引入的css文件图解![](https://i-blog.csdnimg.cn/blog_migrate/7a004225a60dff5f7cbcd18aafb7005d.png)

而在请求这个css资源时被过滤器拦截，就相当于没有加载到样式文件导致的。解决这个问题，只需要对所以的登陆、注册相关的资源进行放行即可。

> 回顾：
> 
> **获取请求行里的URL方法：**
> 
> ```java
> StringBuffer getRequestURL()
> ```

```java
//判断访问资源路径是否和登录注册相关
//1,在数组中存储登陆和注册相关的资源路径
String[] urls = {"/login.jsp","/imgs/","/css/","/loginServlet","/register.jsp","/registerServlet","/checkCodeServlet"};
//2,获取当前访问的资源路径
String url = req.getRequestURL().toString(); 

//3,遍历数组，获取到每一个需要放行的资源路径
for (String u : urls) {
    //4,判断当前访问的资源路径字符串是否包含要放行的的资源路径字符串
    /*
    	比如当前访问的资源路径是  /brand-demo/login.jsp
    	而字符串 /brand-demo/login.jsp 包含了  字符串 /login.jsp ，所以这个字符串就需要放行
    */
    if(url.contains(u)){
        //找到了，放行
        chain.doFilter(request, response);
        //break;
        return;
    }
}
```

**1.6.3.5 过滤器完整代码**

```java
@WebFilter("/*")
public class LoginFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws ServletException, IOException {
        //ServletRequest对象没有getSession方法，要强转成HttpServletRequest 
        HttpServletRequest req = (HttpServletRequest) request;
        
        //判断访问资源路径是否和登录注册相关
        //1,在数组中存储登陆和注册相关的资源路径
        String[] urls = {"/login.jsp","/imgs/","/css/","/loginServlet","/register.jsp","/registerServlet","/checkCodeServlet"};
        //2,获取当前访问的资源路径
        String url = req.getRequestURL().toString(); 

        //3,遍历数组，获取到每一个需要放行的资源路径
        for (String u : urls) {
            //4,判断当前访问的资源路径字符串是否包含要放行的的资源路径字符串
            /*
                比如当前访问的资源路径是  /brand-demo/login.jsp
                而字符串 /brand-demo/login.jsp 包含了  字符串 /login.jsp ，所以这个字符串就需要放行
            */
            if(url.contains(u)){
                //找到了，放行
                chain.doFilter(request, response);
                //break;
                return;
            }
        }
   
        //1. 判断session中是否有user
        HttpSession session = req.getSession();
        Object user = session.getAttribute("user");

        //2. 判断user是否为null
        if(user != null){
            // 登录过了
            //放行
            //参数是强转前后的无所谓
            chain.doFilter(request, response);
        }else {
            // 没有登陆，存储提示信息，跳转到登录页面

            req.setAttribute("login_msg","您尚未登陆！");
            //参数是强转前后的无所谓
            req.getRequestDispatcher("/login.jsp").forward(req,response);
        }
    }

    public void init(FilterConfig config) throws ServletException {
    }

    public void destroy() {
    }
}
```

## 2，Listener监听器

### 2.1 概述

Listener 表示**监听器**，是 JavaWeb 三大组件(Servlet、Filter、Listener)之一。了解即可，后面学Spring时候会用到。

**监听器就是在 `application`，`session`，`request` 三个对象创建、销毁或者往其中添加修改删除属性时，自动执行代码的功能组件。**

**`application` ：**

**`application`** 是 `ServletContext` 类型的对象。

**`ServletContext` ：**

**`ServletContext`** 代表**整个web应用**，在服务器启动的时候，tomcat会**自动创建该对象**。在服务器关闭时会自动销毁该对象。

### 2.2 分类

JavaWeb 提供了8个监听器：

![](https://i-blog.csdnimg.cn/blog_migrate/2a1d56da4fe58cbb6deb844bac468278.png)

这里面只有 **`ServletContextListener`** 这个监听器后期我们会接触到，`ServletContextListener` 是用来**监听 `ServletContext` 对象的创建和销毁**。

**`ServletContextListener`** 接口中有以下两个**方法**

-   `void contextInitialized(ServletContextEvent sce)`：`ServletContext` 对象被创建了会自动执行的方法
    
-   `void contextDestroyed(ServletContextEvent sce)`：`ServletContext` 对象被销毁时会自动执行的方法
    

### 2.3 代码演示

我们只演示一下 `ServletContextListener` 监听器

-   1.定义一个类，实现`ServletContextListener` 接口
    
-   2.重写所有的抽象方法
    
-   3.使用 `@WebListener` 进行配置
    

代码如下：

```java
@WebListener
//实现ServletContextListener 接口，用于对ServletContext对象的创建和销毁进行监听，
//ServletContext代表整个web应用，在服务器启动的时候，tomcat会自动创建该对象。在服务器关闭时会自动销毁该对象。
public class ContextLoaderListener implements ServletContextListener {
    @Override
    //ServletContext对象创建时执行方法
    public void contextInitialized(ServletContextEvent sce) {
        //加载资源
        System.out.println("ContextLoaderListener...");
    }

    @Override
    //ServletContext对象销毁时执行方法
    public void contextDestroyed(ServletContextEvent sce) {
        //释放资源
    }
}
```

启动服务器，就可以在启动的日志信息中看到 `contextInitialized()` 方法输出的内容，同时也说明了 `ServletContext` 对象在服务器启动的时候被创建了。

## 3，AJAX

### 3.1 概述

> _/_ˈeɪdʒæks_/_
> 
> **了解即可**，平时使用都用其异步框架Axios，其封装了AJAX。
> 
> [axios](https://so.csdn.net/so/search?q=axios&spm=1001.2101.3001.7020 "axios")是通过promise实现对ajax技术的一种封装，就像jQuery实现ajax封装一样。  
> **简单来说：** [ajax](https://so.csdn.net/so/search?q=ajax&spm=1001.2101.3001.7020 "ajax")技术实现了网页的局部数据刷新，axios实现了对ajax的封装。

**`AJAX` (Asynchronous JavaScript And XML)：异步的 JavaScript 和 XML。**

`JavaScript` 表明该技术和前端相关；`XML` 是指以此进行**数据交换**。

AJAX和HTML替代JSP，是前端工程师的任务。

[AJAX - XMLHttpRequest 对象](https://www.w3school.com.cn/js/js_ajax_http.asp "AJAX - XMLHttpRequest 对象")

> **回顾：**
> 
> XML 指可扩展标记语言（eXtensible Markup Language）。 被设计用来**传输和存储数据。** 

**作用**

AJAX 作用有以下两方面：

**1.与服务器进行数据交换**：**通过AJAX可以给服务器发送请求，服务器将数据直接响应回给浏览器。**

> **之前用JSP做功能的流程：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/aff0536565ca2d2467a84c5c942c714e.png)
> 
> 如上图，`Servlet` 调用完业务逻辑层后将数据存储到域对象中，然后跳转到指定的 `jsp` 页面，在页面上使用 `EL表达式` 和 `JSTL` 标签库进行数据的展示。
> 
> **使用AJAX后做功能的流程：** 
> 
> html+AJAX替换jsp。 
> 
> 而我们学习了AJAX 后，就可以**使用AJAX和服务器进行通信，以达到使用 HTML+AJAX来替换JSP页面**了。
> 
> 如下图，浏览器发送请求servlet，servlet 调用完业务逻辑层后将数据直接响应回给浏览器页面，页面使用 HTML 来进行数据展示。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8457c526153ad509fceea440927d61c6.png)

**2.异步交互**：可以在**不重新加载整个页面**的情况下，与服务器交换数据并**更新部分网页**的技术，如：搜索联想、用户名是否可用校验，等等…

![](https://i-blog.csdnimg.cn/blog_migrate/2ff1e4b3470a597402eeb11698579960.png)

上图所示的效果我们经常见到，在我们输入一些关键字（例如 `奥运`）后就会在下面联想出相关的内容，而联想出来的这部分数据肯定是存储在百度的服务器上，**此时页面并没有重新刷新**，这就是 **更新局部页面** 的效果。再如下图：

![](https://i-blog.csdnimg.cn/blog_migrate/38b6658ffcf99e4122d58f9f3c412b72.png)

我们在用户名的输入框输入用户名，当输入框一失去焦点，如果用户名已经被占用就会在下方展示提示的信息；在这整个过程中也**没有页面的刷新**，只是在局部展示出了提示信息，这就是 **更新局部页面** 的效果。

### 3.2 同步、异步优点和使用场景

知道了局部刷新后，接下来我们再聊聊同步和异步:

**同步：** 

-   同步发送请求过程如下![](https://i-blog.csdnimg.cn/blog_migrate/9d7dfa0568819b64803910cecec2807d.png)
    

浏览器页面在发送请求给服务器，在服务器处理请求的过程中，浏览器页面**必须等到服务器响应结束**后才能继续做其他的操作。

**异步：** 

-   异步发送请求过程如下![](https://i-blog.csdnimg.cn/blog_migrate/deb1642afdb99078e3aedfed1f62a6c1.png)
    
    浏览器页面发送请求给服务器，在服务器处理请求的过程中，浏览器页面还**可以做其他的操作**。
    

**异步的使用场景：**

1、不涉及共享资源，或对共享资源只读，即非互斥操作

2、没有时序上的严格关系

3、不需要原子操作，或可以通过其他方式控制原子性

4、常用于IO操作等耗时操作，因为比较影响客户体验和使用性能

5、不影响主线程逻辑

  
**同步的使用场景：**不使用异步的时候

  
**同步的好处：**

1、同步流程对结果处理通常更为简单，可以就近处理。

2、同步流程对结果的处理始终和前文保持在一个上下文内。

3、同步流程可以很容易捕获、处理异常。

4、同步流程是最天然的控制过程顺序执行的方式。

**异步的好处：**

1、异步流程可以立即给调用方返回初步的结果。

2、异步流程可以延迟给调用方最终的结果数据，在此期间可以做更多额外的工作，例如结果记录等等。

3、异步流程在执行的过程中，可以释放占用的线程等资源，避免阻塞，等到结果产生再重新获取线程处理。

4、异步流程可以等多次调用的结果出来后，再统一返回一次结果集合，提高响应效率。

### 3.3. 快速入门

![](https://i-blog.csdnimg.cn/blog_migrate/e730961f5ec6527503be60924dedeb8e.png)

**服务端实现**

**创建Servlet：**在项目的创建 `com.itheima.web.servlet` ，并在该包下创建名为 `AjaxServlet` 的servlet

```java
@WebServlet("/ajaxServlet")
public class AjaxServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 响应数据
        response.getWriter().write("hello ajax~");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

**客户端实现**

在 `webapp` 下创建名为 `01-ajax-demo1.html` 的页面，在该页面书写 `ajax` 代码

-   创建核心对象，不同的浏览器创建的对象是不同的。代码固定，不用背。
    
    ```javascript
     var xhttp;
    if (window.XMLHttpRequest) {
        xhttp = new XMLHttpRequest();
    } else {
        // code for IE6, IE5
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    ```
    
-   发送请求
    
    ```javascript
    //建立连接
    xhttp.open("GET", "http://localhost:8080/ajax-demo/ajaxServlet");
    //发送请求
    xhttp.send();
    ```
    
-   获取响应
    
    ```javascript
    //onreadystatechange 就绪状态发生改变
    xhttp.onreadystatechange = function() {
         //当就绪状态==4，请求发送成功，接收到响应后的状态
            //status响应状态码==200，代表受到响应成功
        if (this.readyState == 4 && this.status == 200) {
            // 通过 this.responseText 可以获取到服务端响应的数据
            alert(this.responseText);
        }
    };
    ```
    

**完整代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script>
    //1. 创建核心对象
    var xhttp;
    if (window.XMLHttpRequest) {
        xhttp = new XMLHttpRequest();
    } else {
        // code for IE6, IE5
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    //2. 发送请求
    xhttp.open("GET", "http://localhost:8080/ajax-demo/ajaxServlet");
    xhttp.send();

    //3. 获取响应
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            alert(this.responseText);
        }
    };
</script>
</body>
</html>
```

**测试**

在浏览器地址栏输入 `http://localhost:8080/ajax-demo/01-ajax-demo1.html` ，在 `01-ajax-demo1.html`加载的时候就会发送 `ajax` 请求，效果如下![](https://i-blog.csdnimg.cn/blog_migrate/e48ea0d6eee167cbc186f542e55ec260.png)

我们可以通过 `开发者模式` 查看发送的 AJAX 请求。在浏览器上按 `F12` 快捷键![](https://i-blog.csdnimg.cn/blog_migrate/0064bb67c092228c274ca475ff1601b9.png)

这个是查看所有的请求，如果我们只是想看 **异步请求**的话，点击上图中 `All` 旁边的 `XHR`，会发现只展示 **Type 是 `xhr` 的请求**。如下图：![](https://i-blog.csdnimg.cn/blog_migrate/629206d0504793ce38ac5a7f33f3840a.png)

### 3.4 案例，AJAX校验用户名是否已存在

需求：在完成用户注册时，当用户名输入框失去焦点时，校验用户名是否在数据库已存在![](https://i-blog.csdnimg.cn/blog_migrate/142a0fca9c39211ecc7ecfb80f6fd553.png)

**分析**

-   **前端完成的逻辑**
    
    1.  给用户名输入框绑定光标失去焦点事件 `onblur`
        
    2.  发送 ajax请求，携带username参数
        
    3.  处理响应：是否显示提示信息
        
-   **后端完成的逻辑**
    
    1.  接收用户名
        
    2.  调用service查询User。此案例是为了演示前后端异步交互，所以此处我们不做业务逻辑处理
        
    3.  返回标记
        

整体流程如下：![](https://i-blog.csdnimg.cn/blog_migrate/fb93a0bd71cbc4c2e2038ada82ce1205.png)

**后端实现**

在 `com.ithiema.web.servlet` 包中定义名为 `SelectUserServlet` 的servlet。代码如下：

```java
@WebServlet("/selectUserServlet")
public class SelectUserServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接收用户名
        String username = request.getParameter("username");
        //2. 调用service查询User对象，此处不进行业务逻辑处理，直接给 flag 赋值为 true，表明用户名占用
        boolean flag = true; //省略调用业务方法，调用mapper的selectByUsername返回User对象
        //3. 响应标记到前端
        response.getWriter().write("" + flag);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

**前端实现**

将 `04-资料\1. 验证用户名案例\1. 静态页面` 下的文件整体拷贝到项目下 `webapp` 下。并在 `register.html` 页面的 `body` 结束标签前编写 `script` 标签，在该标签中实现如下逻辑

**第一步：给用户名输入框绑定光标失去焦点事件 `onblur`**

```javascript
//1. 给用户名输入框绑定 失去焦点事件
document.getElementById("username").onblur = function () {
    
}
```

**第二步：发送 ajax请求，携带username参数**

在 `第一步` 绑定的匿名函数中书写发送 ajax 请求的代码

```javascript
//2. 发送ajax请求
//2.1. 创建核心对象
var xhttp;
if (window.XMLHttpRequest) {
    xhttp = new XMLHttpRequest();
} else {
    // code for IE6, IE5
    xhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
//2.2. 发送请求
xhttp.open("GET", "http://localhost:8080/ajax-demo/selectUserServlet);
xhttp.send();

//2.3. 获取响应
xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        //处理响应的结果
    }
};
```

由于我们发送的是 GET 请求，所以需要在 URL 后拼接从输入框获取的用户名数据。而我们在 `第一步` 绑定的匿名函数中通过以下代码可以获取用户名数据

```java
// 获取用户名的值
var username = this.value;  //this ： 给谁绑定的事件，this就代表谁
```

而携带数据需要将 URL 修改为：

```java
xhttp.open("GET", "http://localhost:8080/ajax-demo/selectUserServlet?username="+username);
```

**第三步：处理响应：是否显示提示信息**

当 `this.readyState == 4 && this.status == 200` 条件满足时，说明已经成功响应数据了。

此时需要判断响应的数据是否是 "true" 字符串，如果是说明用户名已经占用给出错误提示；如果不是说明用户名未被占用清除错误提示。代码如下

```java
//判断
if(this.responseText == "true"){
    //用户名存在，显示提示信息
    document.getElementById("username_err").style.display = '';
}else {
    //用户名不存在 ，清楚提示信息
    document.getElementById("username_err").style.display = 'none';
}
```

**综上所述，前端完成代码如下：**

```java
//1. 给用户名输入框绑定 失去焦点事件
document.getElementById("username").onblur = function () {
    //2. 发送ajax请求
    // 获取用户名的值
    var username = this.value;

    //2.1. 创建核心对象
    var xhttp;
    if (window.XMLHttpRequest) {
        xhttp = new XMLHttpRequest();
    } else {
        // code for IE6, IE5
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    //2.2. 发送请求
    xhttp.open("GET", "http://localhost:8080/ajax-demo/selectUserServlet?username="+username);
    xhttp.send();

    //2.3. 获取响应
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            //alert(this.responseText);
            //判断
            if(this.responseText == "true"){
                //用户名存在，显示提示信息
                document.getElementById("username_err").style.display = '';
            }else {
                //用户名不存在 ，清楚提示信息
                document.getElementById("username_err").style.display = 'none';
            }
        }
    };
}
```

## 4，Axios异步框架

### 4.1 概述 

**Axios是什么？**

Axios 是一个基于 _[promise](https://javascript.info/promise-basics "promise")_ 的网络请求库，作用于[node.js](https://nodejs.org/ "node.js") 和浏览器中。 它是 _[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application "isomorphic")_ 的(即同一套代码可以运行在浏览器和node.js中)。

在服务端它使用原生 node.js `http` 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests。

> [axios](https://so.csdn.net/so/search?q=axios&spm=1001.2101.3001.7020 "axios")是通过promise实现对ajax技术的一种封装，就像jQuery实现ajax封装一样。  
> 简单来说： [ajax](https://so.csdn.net/so/search?q=ajax&spm=1001.2101.3001.7020 "ajax")技术实现了网页的局部数据刷新，axios实现了对ajax的封装。

**Axios作用：**

Axios 对原生的AJAX进行封装，简化书写。

Axios官网是：`https://www.axios-http.cn`

[起步 | Axios 中文文档 | Axios 中文网](https://www.axios-http.cn/docs/intro "起步 | Axios 中文文档 | Axios 中文网")

### 4.2 **axios**基本使用

#### 4.2.1 引入js文件、发送请求

axios 使用是比较简单的，分为以下两步：

**1.引入 axios 的 js 文件**

```html
<!--  注意是两对script标签-->
<script src="js/axios-0.18.0.js"></script>
<script>
    axios({
        ...
    }).then(function (response){
        ...
    })
</script>
```

js目录下的axios-0.18.0.js

```javascript
/* axios v0.18.0 | (c) 2018 by Matt Zabriskie */
!function(e,t){"object"==typeof exports&&"object"==typeof module?module.exports=t():"function"==typeof define&&define.amd?define([],t):"object"==typeof exports?exports.axios=t():e.axios=t()}(this,function(){return function(e){function t(r){if(n[r])return n[r].exports;var o=n[r]={exports:{},id:r,loaded:!1};return e[r].call(o.exports,o,o.exports,t),o.loaded=!0,o.exports}var n={};return t.m=e,t.c=n,t.p="",t(0)}([function(e,t,n){e.exports=n(1)},function(e,t,n){"use strict";function r(e){var t=new s(e),n=i(s.prototype.request,t);return o.extend(n,s.prototype,t),o.extend(n,t),n}var o=n(2),i=n(3),s=n(5),u=n(6),a=r(u);a.Axios=s,a.create=function(e){return r(o.merge(u,e))},a.Cancel=n(23),a.CancelToken=n(24),a.isCancel=n(20),a.all=function(e){return Promise.all(e)},a.spread=n(25),e.exports=a,e.exports.default=a},function(e,t,n){"use strict";function r(e){return"[object Array]"===R.call(e)}function o(e){return"[object ArrayBuffer]"===R.call(e)}function i(e){return"undefined"!=typeof FormData&&e instanceof FormData}function s(e){var t;return t="undefined"!=typeof ArrayBuffer&&ArrayBuffer.isView?ArrayBuffer.isView(e):e&&e.buffer&&e.buffer instanceof ArrayBuffer}function u(e){return"string"==typeof e}function a(e){return"number"==typeof e}function c(e){return"undefined"==typeof e}function f(e){return null!==e&&"object"==typeof e}function p(e){return"[object Date]"===R.call(e)}function d(e){return"[object File]"===R.call(e)}function l(e){return"[object Blob]"===R.call(e)}function h(e){return"[object Function]"===R.call(e)}function m(e){return f(e)&&h(e.pipe)}function y(e){return"undefined"!=typeof URLSearchParams&&e instanceof URLSearchParams}function w(e){return e.replace(/^\s*/,"").replace(/\s*$/,"")}function g(){return("undefined"==typeof navigator||"ReactNative"!==navigator.product)&&("undefined"!=typeof window&&"undefined"!=typeof document)}function v(e,t){if(null!==e&&"undefined"!=typeof e)if("object"!=typeof e&&(e=[e]),r(e))for(var n=0,o=e.length;n<o;n++)t.call(null,e[n],n,e);else for(var i in e)Object.prototype.hasOwnProperty.call(e,i)&&t.call(null,e[i],i,e)}function x(){function e(e,n){"object"==typeof t[n]&&"object"==typeof e?t[n]=x(t[n],e):t[n]=e}for(var t={},n=0,r=arguments.length;n<r;n++)v(arguments[n],e);return t}function b(e,t,n){return v(t,function(t,r){n&&"function"==typeof t?e[r]=E(t,n):e[r]=t}),e}var E=n(3),C=n(4),R=Object.prototype.toString;e.exports={isArray:r,isArrayBuffer:o,isBuffer:C,isFormData:i,isArrayBufferView:s,isString:u,isNumber:a,isObject:f,isUndefined:c,isDate:p,isFile:d,isBlob:l,isFunction:h,isStream:m,isURLSearchParams:y,isStandardBrowserEnv:g,forEach:v,merge:x,extend:b,trim:w}},function(e,t){"use strict";e.exports=function(e,t){return function(){for(var n=new Array(arguments.length),r=0;r<n.length;r++)n[r]=arguments[r];return e.apply(t,n)}}},function(e,t){function n(e){return!!e.constructor&&"function"==typeof e.constructor.isBuffer&&e.constructor.isBuffer(e)}function r(e){return"function"==typeof e.readFloatLE&&"function"==typeof e.slice&&n(e.slice(0,0))}/*!
 * Determine if an object is a Buffer
 *
 * @author   Feross Aboukhadijeh <https://feross.org>
 * @license  MIT
 */
    e.exports=function(e){return null!=e&&(n(e)||r(e)||!!e._isBuffer)}},function(e,t,n){"use strict";function r(e){this.defaults=e,this.interceptors={request:new s,response:new s}}var o=n(6),i=n(2),s=n(17),u=n(18);r.prototype.request=function(e){"string"==typeof e&&(e=i.merge({url:arguments[0]},arguments[1])),e=i.merge(o,{method:"get"},this.defaults,e),e.method=e.method.toLowerCase();var t=[u,void 0],n=Promise.resolve(e);for(this.interceptors.request.forEach(function(e){t.unshift(e.fulfilled,e.rejected)}),this.interceptors.response.forEach(function(e){t.push(e.fulfilled,e.rejected)});t.length;)n=n.then(t.shift(),t.shift());return n},i.forEach(["delete","get","head","options"],function(e){r.prototype[e]=function(t,n){return this.request(i.merge(n||{},{method:e,url:t}))}}),i.forEach(["post","put","patch"],function(e){r.prototype[e]=function(t,n,r){return this.request(i.merge(r||{},{method:e,url:t,data:n}))}}),e.exports=r},function(e,t,n){"use strict";function r(e,t){!i.isUndefined(e)&&i.isUndefined(e["Content-Type"])&&(e["Content-Type"]=t)}function o(){var e;return"undefined"!=typeof XMLHttpRequest?e=n(8):"undefined"!=typeof process&&(e=n(8)),e}var i=n(2),s=n(7),u={"Content-Type":"application/x-www-form-urlencoded"},a={adapter:o(),transformRequest:[function(e,t){return s(t,"Content-Type"),i.isFormData(e)||i.isArrayBuffer(e)||i.isBuffer(e)||i.isStream(e)||i.isFile(e)||i.isBlob(e)?e:i.isArrayBufferView(e)?e.buffer:i.isURLSearchParams(e)?(r(t,"application/x-www-form-urlencoded;charset=utf-8"),e.toString()):i.isObject(e)?(r(t,"application/json;charset=utf-8"),JSON.stringify(e)):e}],transformResponse:[function(e){if("string"==typeof e)try{e=JSON.parse(e)}catch(e){}return e}],timeout:0,xsrfCookieName:"XSRF-TOKEN",xsrfHeaderName:"X-XSRF-TOKEN",maxContentLength:-1,validateStatus:function(e){return e>=200&&e<300}};a.headers={common:{Accept:"application/json, text/plain, */*"}},i.forEach(["delete","get","head"],function(e){a.headers[e]={}}),i.forEach(["post","put","patch"],function(e){a.headers[e]=i.merge(u)}),e.exports=a},function(e,t,n){"use strict";var r=n(2);e.exports=function(e,t){r.forEach(e,function(n,r){r!==t&&r.toUpperCase()===t.toUpperCase()&&(e[t]=n,delete e[r])})}},function(e,t,n){"use strict";var r=n(2),o=n(9),i=n(12),s=n(13),u=n(14),a=n(10),c="undefined"!=typeof window&&window.btoa&&window.btoa.bind(window)||n(15);e.exports=function(e){return new Promise(function(t,f){var p=e.data,d=e.headers;r.isFormData(p)&&delete d["Content-Type"];var l=new XMLHttpRequest,h="onreadystatechange",m=!1;if("undefined"==typeof window||!window.XDomainRequest||"withCredentials"in l||u(e.url)||(l=new window.XDomainRequest,h="onload",m=!0,l.onprogress=function(){},l.ontimeout=function(){}),e.auth){var y=e.auth.username||"",w=e.auth.password||"";d.Authorization="Basic "+c(y+":"+w)}if(l.open(e.method.toUpperCase(),i(e.url,e.params,e.paramsSerializer),!0),l.timeout=e.timeout,l[h]=function(){if(l&&(4===l.readyState||m)&&(0!==l.status||l.responseURL&&0===l.responseURL.indexOf("file:"))){var n="getAllResponseHeaders"in l?s(l.getAllResponseHeaders()):null,r=e.responseType&&"text"!==e.responseType?l.response:l.responseText,i={data:r,status:1223===l.status?204:l.status,statusText:1223===l.status?"No Content":l.statusText,headers:n,config:e,request:l};o(t,f,i),l=null}},l.onerror=function(){f(a("Network Error",e,null,l)),l=null},l.ontimeout=function(){f(a("timeout of "+e.timeout+"ms exceeded",e,"ECONNABORTED",l)),l=null},r.isStandardBrowserEnv()){var g=n(16),v=(e.withCredentials||u(e.url))&&e.xsrfCookieName?g.read(e.xsrfCookieName):void 0;v&&(d[e.xsrfHeaderName]=v)}if("setRequestHeader"in l&&r.forEach(d,function(e,t){"undefined"==typeof p&&"content-type"===t.toLowerCase()?delete d[t]:l.setRequestHeader(t,e)}),e.withCredentials&&(l.withCredentials=!0),e.responseType)try{l.responseType=e.responseType}catch(t){if("json"!==e.responseType)throw t}"function"==typeof e.onDownloadProgress&&l.addEventListener("progress",e.onDownloadProgress),"function"==typeof e.onUploadProgress&&l.upload&&l.upload.addEventListener("progress",e.onUploadProgress),e.cancelToken&&e.cancelToken.promise.then(function(e){l&&(l.abort(),f(e),l=null)}),void 0===p&&(p=null),l.send(p)})}},function(e,t,n){"use strict";var r=n(10);e.exports=function(e,t,n){var o=n.config.validateStatus;n.status&&o&&!o(n.status)?t(r("Request failed with status code "+n.status,n.config,null,n.request,n)):e(n)}},function(e,t,n){"use strict";var r=n(11);e.exports=function(e,t,n,o,i){var s=new Error(e);return r(s,t,n,o,i)}},function(e,t){"use strict";e.exports=function(e,t,n,r,o){return e.config=t,n&&(e.code=n),e.request=r,e.response=o,e}},function(e,t,n){"use strict";function r(e){return encodeURIComponent(e).replace(/%40/gi,"@").replace(/%3A/gi,":").replace(/%24/g,"$").replace(/%2C/gi,",").replace(/%20/g,"+").replace(/%5B/gi,"[").replace(/%5D/gi,"]")}var o=n(2);e.exports=function(e,t,n){if(!t)return e;var i;if(n)i=n(t);else if(o.isURLSearchParams(t))i=t.toString();else{var s=[];o.forEach(t,function(e,t){null!==e&&"undefined"!=typeof e&&(o.isArray(e)?t+="[]":e=[e],o.forEach(e,function(e){o.isDate(e)?e=e.toISOString():o.isObject(e)&&(e=JSON.stringify(e)),s.push(r(t)+"="+r(e))}))}),i=s.join("&")}return i&&(e+=(e.indexOf("?")===-1?"?":"&")+i),e}},function(e,t,n){"use strict";var r=n(2),o=["age","authorization","content-length","content-type","etag","expires","from","host","if-modified-since","if-unmodified-since","last-modified","location","max-forwards","proxy-authorization","referer","retry-after","user-agent"];e.exports=function(e){var t,n,i,s={};return e?(r.forEach(e.split("\n"),function(e){if(i=e.indexOf(":"),t=r.trim(e.substr(0,i)).toLowerCase(),n=r.trim(e.substr(i+1)),t){if(s[t]&&o.indexOf(t)>=0)return;"set-cookie"===t?s[t]=(s[t]?s[t]:[]).concat([n]):s[t]=s[t]?s[t]+", "+n:n}}),s):s}},function(e,t,n){"use strict";var r=n(2);e.exports=r.isStandardBrowserEnv()?function(){function e(e){var t=e;return n&&(o.setAttribute("href",t),t=o.href),o.setAttribute("href",t),{href:o.href,protocol:o.protocol?o.protocol.replace(/:$/,""):"",host:o.host,search:o.search?o.search.replace(/^\?/,""):"",hash:o.hash?o.hash.replace(/^#/,""):"",hostname:o.hostname,port:o.port,pathname:"/"===o.pathname.charAt(0)?o.pathname:"/"+o.pathname}}var t,n=/(msie|trident)/i.test(navigator.userAgent),o=document.createElement("a");return t=e(window.location.href),function(n){var o=r.isString(n)?e(n):n;return o.protocol===t.protocol&&o.host===t.host}}():function(){return function(){return!0}}()},function(e,t){"use strict";function n(){this.message="String contains an invalid character"}function r(e){for(var t,r,i=String(e),s="",u=0,a=o;i.charAt(0|u)||(a="=",u%1);s+=a.charAt(63&t>>8-u%1*8)){if(r=i.charCodeAt(u+=.75),r>255)throw new n;t=t<<8|r}return s}var o="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";n.prototype=new Error,n.prototype.code=5,n.prototype.name="InvalidCharacterError",e.exports=r},function(e,t,n){"use strict";var r=n(2);e.exports=r.isStandardBrowserEnv()?function(){return{write:function(e,t,n,o,i,s){var u=[];u.push(e+"="+encodeURIComponent(t)),r.isNumber(n)&&u.push("expires="+new Date(n).toGMTString()),r.isString(o)&&u.push("path="+o),r.isString(i)&&u.push("domain="+i),s===!0&&u.push("secure"),document.cookie=u.join("; ")},read:function(e){var t=document.cookie.match(new RegExp("(^|;\\s*)("+e+")=([^;]*)"));return t?decodeURIComponent(t[3]):null},remove:function(e){this.write(e,"",Date.now()-864e5)}}}():function(){return{write:function(){},read:function(){return null},remove:function(){}}}()},function(e,t,n){"use strict";function r(){this.handlers=[]}var o=n(2);r.prototype.use=function(e,t){return this.handlers.push({fulfilled:e,rejected:t}),this.handlers.length-1},r.prototype.eject=function(e){this.handlers[e]&&(this.handlers[e]=null)},r.prototype.forEach=function(e){o.forEach(this.handlers,function(t){null!==t&&e(t)})},e.exports=r},function(e,t,n){"use strict";function r(e){e.cancelToken&&e.cancelToken.throwIfRequested()}var o=n(2),i=n(19),s=n(20),u=n(6),a=n(21),c=n(22);e.exports=function(e){r(e),e.baseURL&&!a(e.url)&&(e.url=c(e.baseURL,e.url)),e.headers=e.headers||{},e.data=i(e.data,e.headers,e.transformRequest),e.headers=o.merge(e.headers.common||{},e.headers[e.method]||{},e.headers||{}),o.forEach(["delete","get","head","post","put","patch","common"],function(t){delete e.headers[t]});var t=e.adapter||u.adapter;return t(e).then(function(t){return r(e),t.data=i(t.data,t.headers,e.transformResponse),t},function(t){return s(t)||(r(e),t&&t.response&&(t.response.data=i(t.response.data,t.response.headers,e.transformResponse))),Promise.reject(t)})}},function(e,t,n){"use strict";var r=n(2);e.exports=function(e,t,n){return r.forEach(n,function(n){e=n(e,t)}),e}},function(e,t){"use strict";e.exports=function(e){return!(!e||!e.__CANCEL__)}},function(e,t){"use strict";e.exports=function(e){return/^([a-z][a-z\d\+\-\.]*:)?\/\//i.test(e)}},function(e,t){"use strict";e.exports=function(e,t){return t?e.replace(/\/+$/,"")+"/"+t.replace(/^\/+/,""):e}},function(e,t){"use strict";function n(e){this.message=e}n.prototype.toString=function(){return"Cancel"+(this.message?": "+this.message:"")},n.prototype.__CANCEL__=!0,e.exports=n},function(e,t,n){"use strict";function r(e){if("function"!=typeof e)throw new TypeError("executor must be a function.");var t;this.promise=new Promise(function(e){t=e});var n=this;e(function(e){n.reason||(n.reason=new o(e),t(n.reason))})}var o=n(23);r.prototype.throwIfRequested=function(){if(this.reason)throw this.reason},r.source=function(){var e,t=new r(function(t){e=t});return{token:t,cancel:e}},e.exports=r},function(e,t){"use strict";e.exports=function(e){return function(t){return e.apply(null,t)}}}])});
//# sourceMappingURL=axios.min.map
```

**2.使用axios 发送请求，并获取响应结果**

**发送 get 请求**

方法一： 

```javascript
axios({
    method:"get",
    url:"http://localhost:8080/ajax-demo1/aJAXDemo1?username=zhangsan"
}).then(function (resp){
    alert(resp.data);
})
```

**方法二（推荐，请求方法别名方式发请求和箭头函数）：**

```javascript
//箭头函数可以让then里this指向vue，而不是窗口。可以直接this.data而不是_this.data
axios.get("http://localhost:8080/books").then((res)=>{
      console.log(res.data)
});
```

> 箭头函数可以让then里this指向vue，而不是窗口。可以直接this.data而不是\_this.data 

**发送 post 请求**

```javascript
axios({
    method:"post",
    url:"http://localhost:8080/ajax-demo1/aJAXDemo1",
    data:"username=zhangsan"
}).then(function (resp){
    alert(resp.data);
});
```

也可以请求方法别名方式发请求 

```javascript
    axios.post("http://localhost:8080/ajax-demo/axiosServlet","username=zhangsan").then(function (resp) {
        alert(resp.data);
    })
```

`axios()` 是用来发送异步请求的，小括号中使用 js 对象传递请求相关的参数：

-   `method` 属性：用来设置请求方式的。取值为 `get` 或者 `post`。
    
-   `url` 属性：用来书写请求的资源路径。如果是 `get` 请求，需要将请求参数拼接到路径的后面，格式为： `url?参数名=参数值&参数名2=参数值2`。
    
-   `data` 属性：作为请求体被发送的数据。也就是说如果是 `post` 请求的话，数据需要作为 `data` 属性的值。
    

`then()` 需要传递一个匿名函数。我们将 `then()` 中传递的匿名函数称为 **回调函数**，意思是该匿名函数在发送请求时不会被调用，而是在成功响应后调用的函数。而该回调函数中的 `resp` 参数是对响应的数据进行封装的对象，通过 `resp.data` 可以获取到响应的数据。

#### 4.2.2 **请求方法别名方式发请求**

为了方便起见， Axios 已经为所有支持的请求方法提供了别名。如下：

-   `get` 请求 ： `axios.get(url[,config])`
    
-   `post` 请求：`axios.post(url[,data[,config])`
    

-   `delete` 请求 ： `axios.delete(url[,config])`
    
-   `head` 请求 ： `axios.head(url[,config])`
    
-   `options` 请求 ： `axios.option(url[,config])`
    
-   `put` 请求：`axios.put(url[,data[,config])`
    
-   `patch` 请求：`axios.patch(url[,data[,config])`
    

而我们只关注 `get` 请求和 `post` 请求。

入门案例中的 `get` 请求代码可以改为如下：

```javascript
axios.get("http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan").then(function (resp) {
    alert(resp.data);
});
```

入门案例中的 `post` 请求代码可以改为如下：

```javascript
axios.post("http://localhost:8080/ajax-demo/axiosServlet","username=zhangsan").then(function (resp) {
    alert(resp.data);
})
```

### 4.3 快速入门，请求用户名

**后端实现**

定义一个用于接收请求的servlet，代码如下：

```java
@WebServlet("/axiosServlet")
public class AxiosServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("get...");
        //1. 接收请求参数
        String username = request.getParameter("username");
        System.out.println(username);
        //2. 响应数据
        response.getWriter().write("hello Axios~");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("post...");
        this.doGet(request, response);
    }
}
```

**前端实现**

-   引入 js 文件
    
    ```html
    <script src="js/axios-0.18.0.js"></script>
    <script>
    </script>
    ```
    
-   发送 ajax 请求
    
    -   get 请求
        
        ```javascript
        axios({
            method:"get",
            url:"http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan"
        }).then(function (resp) {
            alert(resp.data);
        })
        ```
        
    -   post 请求
        
        ```javascript
        axios({
            method:"post",
            url:"http://localhost:8080/ajax-demo/axiosServlet",
            data:"username=zhangsan"
        }).then(function (resp) {
            alert(resp.data);
        })
        ```
        
        ```javascript
            axios.post("http://localhost:8080/ajax-demo/axiosServlet","username=zhangsan").then(function (resp) {
                alert(resp.data);
            })
        ```
        

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--  注意是两对script标签-->
<script src="js/axios-0.18.0.js"></script>
<script>
    //1. get
   /* axios({
        method:"get",
        url:"http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan"
    }).then(function (resp) {
        alert(resp.data);
    })*/

    //2. post  在js中{} 表示一个js对象，而这个js对象中有三个属性
    axios({
        method:"post",
        url:"http://localhost:8080/ajax-demo/axiosServlet",
        data:"username=zhangsan"
    }).then(function (response){
        console.log(response);
    })
    //3.  请求方法别名
    // axios.post("http://localhost:8080/ajax-demo/axiosServlet","username=zhangsan").then(function (resp) {
    //     alert(resp.data);
    // })
</script>
</body>
</html>
```

![](https://i-blog.csdnimg.cn/blog_migrate/972b6f2648bef3c8bc85fb15bbff27cc.png)

## 5，JSON

### 5.1 概述

**概念：`JavaScript Object Notation`。JavaScript 对象表示法.**

notation译为符号、表示法。 

**`JSON` 的格式：**

```javascript
let json={
	"name":"zhangsan",
	"age":23,
	"city":"北京"
}
```

  **JSON字符串的格式：**大括号外必须是单引号

```javascript
var 变量名 = '{"key":value,"key":value,...}';
```

> **回顾JavaScript对象的定义格式**：
> 
> ```javascript
> let js={
> 	name:"zhangsan",
> 	age:23,
> 	city:"北京"
> }
> ```

通过上面 js 对象格式和 json 格式进行对比，发现两个格式特别像。

js 对象中的键可以使用引号（可以是单引号，也可以是双引号）；而 `json` 格式中的键要求**必须使用双引号**括起来，这是 `json` 格式的规定。

**JSON作用：**

由于其语法格式简单，层次结构鲜明，现多用于作为**数据载体**，在网络中进行数据传输。

以后我们会以 json 格式的数据进行**前后端交互**。前端发送请求时，如果是复杂的数据就会**以 json 提交给后端**；而后端如果需要响应一些复杂的数据时，也需要以 **json 格式将数据响应**回给浏览器。

**服务端给浏览器响应简单数据：**

![](https://i-blog.csdnimg.cn/blog_migrate/eac40ea1b9edcc71b080991a914b760b.png)

**xml描述数据的写：**

```XML
<student>
    <name>张三</name>
    <age>23</age>
    <city>北京</city>
</student>
```

**`json` 描述数据的写法：**

```javascript
{	
	"name":"张三",
    "age":23,
    "city":"北京"
}
```

上面两种格式进行对比后就会发现 `json` 格式数据的简单，以及所占的字节数少等优点。

### 5.2 JSON 基础语法

#### 5.2.1 定义格式

**定义JSON：**

```javascript
    let json={"name":"zhangsan","age":32};
    console.log(json.name)
```

**定义JSON字符串：**大括号外必须是单引号

```javascript
var 变量名 = '{"key":value,"key":value,...}';
```

> **注意：**
> 
> **`JSON` 串的键要求必须使用双引号括起来**，而值根据要表示的类型确定。value 的数据类型分为如下
> 
> -   数字（整数或浮点数）
>     
> -   字符串（使用双引号括起来）
>     
> -   逻辑值（true或者false）
>     
> -   数组（在方括号中）
>     
> -   对象（在花括号中）
>     
> -   null
>     
> 
> 示例：
> 
> ```javascript
> var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","上海","西安"]}'
> ```

**代码演示**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script>
    //定义JSON字符串
    var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","上海","西安"]}'
    //定义JavaScript字符串
    //var jsonStr = {name:"zhangsan",age:23,addr:["北京","上海","西安"]}
    alert(jsonStr);

</script>
</body>
</html>
```

通过浏览器打开，页面效果如下图所示

![](https://i-blog.csdnimg.cn/blog_migrate/510c0498607c068653bd75729041a53a.png)

####  5.2.2 js和JSON转换

**axios可以自动转换“js对象”或“JSON串”成JSON。**

-   `parse(str)` ：**将 JSON串转换为 js 对象**。
    
    ```javascript
    var jsObject = JSON.parse(jsonStr);
    ```
    

 **代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script>
    //1. 定义JSON字符串
    var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","上海","西安"]}'
    alert(jsonStr);

    //2. 将 JSON 字符串转为 JS 对象
    let jsObject = JSON.parse(jsonStr);
    alert(jsObject)
    alert(jsObject.name)
    //3. 将 JS 对象转换为 JSON 字符串
    let jsonStr2 = JSON.stringify(jsObject);
    alert(jsonStr2)
</script>
</body>
</html>
```

**axios也可以自动将js对象或JSON串转成JSON：** 

`axios` 是一个很强大的工具。我们只需要将需要提交的参数封装成 js 对象，并将该 js 对象作为 `axios` 的 `data` 属性值进行，它会自动将 js 对象转换为 `JSON` 串进行提交。如下：

```javascript
//这里定义JavaScript对象，而不是JSON对象。axios可以自动将js对象转JSON对象。
var jsObject = {name:"张三"};

axios({
    //必须是post，JSON必须放在请求体
    method:"post",
    url:"http://localhost:8080/ajax-demo/axiosServlet",
    data:jsObject  //这里 axios 会将该js对象转换为 json 串的
}).then(function (resp) {
    alert(resp.data);
})
```

#### 5.2.3 axios携带JSON发送异步请求

> **`axios` 直接携带请求参数发送请求**
> 
> ```javascript
> axios({
>     method:"post",
>     url:"http://localhost:8080/ajax-demo/axiosServlet",
>     data:"username=zhangsan"
> }).then(function (resp) {
>     alert(resp.data);
> })
> ```

 **`axios` 携带JSON请求参数发送请求**

提前定义一个 js 对象，用来封装需要提交的参数，然后使用 `JSON.stringify(js对象)` 转换为 `JSON` 串，再**将该 `JSON` 串**作为 `axios` 的 `data` 属性值**进行请求参数的提交**。如下：

```javascript
var jsObject = {name:"张三"};

axios({
    //必须是post，JSON必须放在请求体
    method:"post",
    url:"http://localhost:8080/ajax-demo/axiosServlet",
    data: JSON.stringify(jsObject)
}).then(function (resp) {
    alert(resp.data);
})
```

**axios也可以自动将js对象或JSON串转成JSON：** 

`axios` 是一个很强大的工具。我们只需要将需要提交的参数封装成 js 对象，并将该 js 对象作为 `axios` 的 `data` 属性值进行，它会自动将 js 对象转换为 `JSON` 串进行提交。如下：

```javascript
var jsObject = {name:"张三"};

axios({
    //必须是post，JSON必须放在请求体
    method:"post",
    url:"http://localhost:8080/ajax-demo/axiosServlet",
    data:jsObject  //这里 axios 会将该js对象转换为 json 串的
}).then(function (resp) {
    alert(resp.data);
})
```

> **注意：**
> 
> -   js 提供的 `JSON` 对象我们只需要了解一下即可。因为 **`axios` 会自动对 js 对象和 `JSON` 串进行想换转换**。
>     
> -   发送异步请求时，**如果请求参数是 `JSON` 格式，那请求方式必须是 `POST`。**因为 **`JSON` 串需要放在请求体中**。
>     

### 5.3 Fastjson，JSON串和Java对象的转换

> JSON不能用request.getParameter()接收，要获取请求体request.getReader()，再通过fastJSON转换成java对象。

**json 的作用：**

**以后我们会以 json 格式的数据进行前后端交互**。前端发送请求时，如果是复杂的数据就会**以 json 提交给后端**；而后端如果需要响应一些复杂的数据时，也需要以 **json 格式将数据响应**回给浏览器。![](https://i-blog.csdnimg.cn/blog_migrate/45e46d614bacea0b59ba447521f3d5eb.png)

**使用axios，请求响应数据的获取方式：**

-   **请求数据：**先获取请求体request.getReader()，再JSON字符串转为Java对象
    
-   **响应数据：**Java对象转为JSON字符串，用response.setContentType("text/json;charset=utf-8")和getWriter().write(jsonString)设置响应数据，axios的then里就可以获取到响应信息。
    

**Fastjson 概述**

**`Fastjson` 是**阿里巴巴提供的**一个**Java语言编写的高性能功能完善的 **`JSON` 库**，是目前Java语言中最快的 `JSON` 库，可以**实现 `Java` 对象和 `JSON` 字符串的相互转换。**

**Fastjson 使用**

`Fastjson` 使用也是比较简单的，分为以下三步完成

1.  **导入坐标**
    
    ```XML
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.62</version>
    </dependency>
    ```
    
2.  **Java对象转JSON**
    
    ```java
    String jsonStr = JSON.toJSONString(obj);
    ```
    
    将 Java 对象转换为 JSON 串，只需要使用 `Fastjson` 提供的 `JSON` 类中的 `toJSONString()` 静态方法即可。
    
3.  **JSON字符串转Java对象**
    
    ```java
    User user = JSON.parseObject(jsonStr, User.class);
    ```
    
    将 json 转换为 Java 对象，只需要使用 `Fastjson` 提供的 `JSON` 类中的 `parseObject()` 静态方法即可。
    

**代码演示，将Java对象和JSON字符串互相转换：**

-   引入坐标
    
-   创建一个类，专门用来测试 Java 对象和 JSON 串的相互转换，代码如下：
    
    ```java
    public class FastJsonDemo {
    
        public static void main(String[] args) {
            //1. 将Java对象转为JSON字符串
            User user = new User();
            user.setId(1);
            user.setUsername("zhangsan");
            user.setPassWord("123");
    
            String jsonString = JSON.toJSONString(user);
            System.out.println(jsonString);//{"id":1,"passWord":"123","username":"zhangsan"}
    
    
            //2. 将JSON字符串转为Java对象
            User u = JSON.parseObject("{\"id\":1,\"passWord\":\"123\",\"username\":\"zhangsan\"}", User.class);
            System.out.println(u);
        }
    }
    ```
    

## 6，案例，Axios + JSON 品牌列表查询和添加

### 6.0 需求

> 仅用于学习axios+json，下一节讲vue框架时候会优化循环渲染和条件渲染 

使用Axios + JSON 完成品牌列表数据查询和添加。页面效果还是下图所示：![](https://i-blog.csdnimg.cn/blog_migrate/0824dbe2368e873491b447c2ebee97e3.png)

### 6.1 坑点

js中定义JSON串要记得属性名有转义后的双引号。

报错：java.sql.SQLException: Could not retrieve transation read-only status server

mysql版本很高，你驱动很低，所以使用版本差不多的驱动，pom.xml更改依赖版本。

### 6.2 查询所有功能

![](https://i-blog.csdnimg.cn/blog_migrate/27f914af6ab2ffc9a3f6d3be46e58650.png)

如上图所示就该功能的整体流程。前后端需以 JSON 格式进行数据的传递；由于此功能是查询所有的功能，前端发送 ajax 请求不需要携带参数，而后端响应数据需以如下格式的 json 数据![](https://i-blog.csdnimg.cn/blog_migrate/0619bb5007cbf9b4b13661c65b2c7c3e.png)

> **jsp方案：**
> 
> 过去使用 jsp方案是Servlet调用业务中selectAll方法获取List<Brand>对象brands，将其setAtrribute后转发到brand.jsp。brand.jsp通过el表达式展示请求域数据，通过jstl语句循环、条件渲染。
> 
> **axios+html方案：**
> 
> axios+html方案是Servlet调用业务中selectAll方法获取List<Brand>对象brands，将其转json串响应。brand.html通过axios请求后台url，then里获取到响应的json，通过innerHTML填写表格内数据。

**环境准备**

`brand-demo`工程目录结构如下：是上上一节的讲JSP时的项目[JavaWeb基础6——Request,Response,JSP&MVC\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126024588?spm=1001.2014.3001.5501 "JavaWeb基础6——Request,Response,JSP&MVC_vincewm的博客-CSDN博客")

![](https://i-blog.csdnimg.cn/blog_migrate/af2a65736fb96b8a38a967273de11b82.png)

 pom.xml导入依赖Mybatis、mysql、Servlet、

**注意：**

-   在给定的原始工程中已经给定一些代码。而在此案例中我们只关注前后端交互代码实现
    
-   要根据自己的数据库环境去修改连接数据库的信息，在 `mybatis-config.xml` 核心配置文件中修改
    

**后端实现**

在 `com.itheima.web` 包下创建名为 `SelectAllServlet` 的 `servlet`，具体的逻辑如下：

-   调用 service 的 `selectAll()` 方法进行查询所有的逻辑处理
    
-   将查询到的集合数据转换为 json 数据。我们将此过程称为 **序列化**；如果是将 json 数据转换为 Java 对象，我们称之为 **反序列化**
    
-   将 json 数据响应回给浏览器。这里一定要设置响应数据的类型及字符集 `response.setContentType("text/json;charset=utf-8");`
    

`SelectAllServlet` 代码如下：

```java
@WebServlet("/selectAllServlet")
public class SelectAllServlet extends HttpServlet {
    private BrandService brandService = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 调用Service查询
        List<Brand> brands = brandService.selectAll();

        //2. 将集合转换为JSON数据   序列化
        String jsonString = JSON.toJSONString(brands);

        //3. 响应数据  application/json   text/json
        response.setContentType("text/json;charset=utf-8");
        //后端发JSON串，前端then里的响应数据是json数组
        response.getWriter().write(jsonString);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

启动Tomcat，查看后端页面/selectAllServlet，可以看到响应的JSON数据：

![](https://i-blog.csdnimg.cn/blog_migrate/4259a2dd18ef610a878286b5f0ff33b3.png)

**前端实现**

**1.引入 js 文件**

在 `brand.html` 页面引入 `axios` 的 js 文件

```html
<script src="js/axios-0.18.0.js"></script>
```

**2.绑定 `页面加载完毕` 事件**

在 `brand.html` 页面绑定加载完毕事件，该事件是在页面加载完毕后被触发，代码如下

```javascript
//页面加载完毕事件
window.onload = function() {
	
}
```

**3.发送异步请求**

在页面加载完毕事件绑定的匿名函数中发送异步请求，代码如下：

```javascript
 //2. 发送ajax请求
axios({
    method:"get",
    url:"http://localhost:8080/brand-demo/selectAllServlet"
}).then(function (resp) {

});
```

**4.处理响应数据**

在 `then` 中的回调函数中通过 `resp.data` 可以获取响应回来的数据，而数据格式如下![](https://i-blog.csdnimg.cn/blog_migrate/0eaade82e1345d5748dbdbd3fcae1e04.png)

现在我们需要拼接字符串，将下面表格中的所有的 `tr` 拼接到一个字符串中，然后使用 `document.getElementById("brandTable").innerHTML = 拼接好的字符串` 就可以动态的展示出用户想看到的数据![](https://i-blog.csdnimg.cn/blog_migrate/3903d392a760980782d207fcee2d1ecf.png)

而表头行是固定的，所以先定义初始值是表头行数据的字符串，如下

```javascript
//获取数据
let brands = resp.data;
let tableData = " <tr>\n" +
    "        <th>序号</th>\n" +
    "        <th>品牌名称</th>\n" +
    "        <th>企业名称</th>\n" +
    "        <th>排序</th>\n" +
    "        <th>品牌介绍</th>\n" +
    "        <th>状态</th>\n" +
    "        <th>操作</th>\n" +
    "    </tr>";
```

接下来遍历响应回来的数据 `brands` ，拿到每一条品牌数据

```javascript
for (let i = 0; i < brands.length ; i++) {
    let brand = brands[i];
	
}
```

紧接着就是从 `brand` 对象中获取数据并且拼接 `数据行`，累加到 `tableData` 字符串变量中

```javascript
tableData += "\n" +
    "    <tr align=\"center\">\n" +
    "        <td>"+(i+1)+"</td>\n" +
    "        <td>"+brand.brandName+"</td>\n" +
    "        <td>"+brand.companyName+"</td>\n" +
    "        <td>"+brand.ordered+"</td>\n" +
    "        <td>"+brand.description+"</td>\n" +
    "        <td>"+brand.status+"</td>\n" +
    "\n" +
    "        <td><a href=\"#\">修改</a> <a href=\"#\">删除</a></td>\n" +
    "    </tr>";
```

最后再将拼接好的字符串写到表格中

```javascript
// 设置表格数据
document.getElementById("brandTable").innerHTML = tableData;
```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<a href="addBrand.html"><input type="button" value="新增"></a><br>
<hr>
<table id="brandTable" border="1" cellspacing="0" width="100%">
   
</table>

<script src="js/axios-0.18.0.js"></script>

<script>
    //1. 当页面加载完成后，发送ajax请求
    window.onload = function () {
        //2. 发送ajax请求
        axios({
            method:"get",
            url:"http://localhost:8080/brand-demo/selectAllServlet"
        }).then(function (resp) {
            //获取数据
            let brands = resp.data;
            //先这样循环渲染，后面用vue后会优化
            let tableData = " <tr>\n" +
                "        <th>序号</th>\n" +
                "        <th>品牌名称</th>\n" +
                "        <th>企业名称</th>\n" +
                "        <th>排序</th>\n" +
                "        <th>品牌介绍</th>\n" +
                "        <th>状态</th>\n" +
                "        <th>操作</th>\n" +
                "    </tr>";
        //后端发JSON串，前端then里的响应数据是json数组
            for (let i = 0; i < brands.length ; i++) {
                let brand = brands[i];

                tableData += "\n" +
                    "    <tr align=\"center\">\n" +
                    "        <td>"+(i+1)+"</td>\n" +
                    "        <td>"+brand.brandName+"</td>\n" +
                    "        <td>"+brand.companyName+"</td>\n" +
                    "        <td>"+brand.ordered+"</td>\n" +
                    "        <td>"+brand.description+"</td>\n" +
                    "        <td>"+brand.status+"</td>\n" +
                    "\n" +
                    "        <td><a href=\"#\">修改</a> <a href=\"#\">删除</a></td>\n" +
                    "    </tr>";
            }
            // 设置表格数据
            document.getElementById("brandTable").innerHTML = tableData;
        })
    }
</script>
</body>
</html>
```

> 先这样循环渲染，后面用vue后会优化 

### 6.3 添加品牌功能，异步提交表单

![](https://i-blog.csdnimg.cn/blog_migrate/73973411446c931bf8bb9df1760a5269.png)

如上所示，当我们点击 `新增` 按钮，会跳转到 `addBrand.html` 页面。在 `addBrand.html` 页面输入数据后点击 `提交` 按钮，就会将数据提交到后端，而后端将数据保存到数据库中。

具体的前后端交互的流程如下：![](https://i-blog.csdnimg.cn/blog_migrate/6098117752caf0c491ebcc35c7bd4cc3.png)

**说明：**

前端需要将用户输入的数据提交到后端，这部分数据需要以 json 格式进行提交，数据格式如下：![](https://i-blog.csdnimg.cn/blog_migrate/82e2fd64b660b97024574d5ee60ded0a.png)

> submit提交表单：<input type="submit">，是同步的
> 
> button提交表单：点击事件提交，是异步的

**后端实现**

在 `com.itheima.web` 包下创建名为 `AddServlet` 的 `servlet`，具体的逻辑如下：

-   获取请求参数
    
    由于前端提交的是 json 格式的数据，所以我们不能使用 `request.getParameter()` 方法获取请求参数
    
    -   如果提交的数据格式是 `username=zhangsan&age=23` ，后端就可以使用 `request.getParameter()` 方法获取
        
    -   如果提交的数据格式是 json，后端就需要通过 request 对象获取输入流，再通过输入流读取数据
        
-   将获取到的请求参数（json格式的数据）转换为 `Brand` 对象
    
-   调用 service 的 `add()` 方法进行添加数据的逻辑处理
    
-   将 json 数据响应回给浏览器。
    

`AddServlet` 代码如下：

```java
@WebServlet("/addServlet")
public class AddServlet extends HttpServlet {

    private BrandService brandService = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 接收数据,request.getParameter 不能接收json的数据
       /* String brandName = request.getParameter("brandName");
        System.out.println(brandName);*/

        // 获取请求体数据
        BufferedReader br = request.getReader();
        String params = br.readLine();
        // 将JSON字符串转为Java对象
        Brand brand = JSON.parseObject(params, Brand.class);
        //2. 调用service 添加
        brandService.add(brand);
        //3. 响应成功标识
        response.getWriter().write("success");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

**前端实现**

在 `addBrand.html` 页面给 `提交` 按钮绑定点击事件，并在绑定的匿名函数中发送异步请求，代码如下：

```javascript
//1. 给按钮绑定单击事件
document.getElementById("btn").onclick = function () {
    //2. 发送ajax请求
    axios({
        method:"post",
        url:"http://localhost:8080/brand-demo/addServlet",
        data:???
    }).then(function (resp) {
        // 判断响应数据是否为 success
        if(resp.data == "success"){
            location.href = "http://localhost:8080/brand-demo/brand.html";
        }
    })
}
```

现在我们只需要考虑如何获取页面上用户输入的数据即可。

首先我们先定义如下的一个 js 对象，该对象是用来封装页面上输入的数据，并将该对象作为上面发送异步请求时 `data` 属性的值。

```javascript
// 将表单数据转为json
var formData = {
    brandName:"",
    companyName:"",
    ordered:"",
    description:"",
    status:"",
};
```

接下来获取输入框输入的数据，并将获取到的数据赋值给 `formData` 对象指定的属性。比如获取用户名的输入框数据，并把该数据赋值给 `formData` 对象的 `brandName` 属性

```javascript
// 获取表单数据
let brandName = document.getElementById("brandName").value;
// 设置数据
formData.brandName = brandName;
```

**说明：其他的输入框都用同样的方式获取并赋值。**但是有一个比较特殊，就是状态数据，如下图是页面内容![](https://i-blog.csdnimg.cn/blog_migrate/55945ad6cb7bb55f137ef4b0aba519ec.png)

我们需要判断哪儿个被选中，再将选中的单选框数据赋值给 `formData` 对象的 `status` 属性，代码实现如下：

```javascript
let status = document.getElementsByName("status");
for (let i = 0; i < status.length; i++) {
    if(status[i].checked){
        //
        formData.status = status[i].value ;
    }
}
```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>添加品牌</title>
</head>
<body>
<h3>添加品牌</h3>
<form action="" method="post">
    品牌名称：<input id="brandName" name="brandName"><br>
    企业名称：<input id="companyName" name="companyName"><br>
    排序：<input id="ordered" name="ordered"><br>
    描述信息：<textarea rows="5" cols="20" id="description" name="description"></textarea><br>
    状态：
    <input type="radio" name="status" value="0">禁用
    <input type="radio" name="status" value="1">启用<br>

    <input type="button" id="btn"  value="提交">
</form>

<script src="js/axios-0.18.0.js"></script>

<script>
    //1. 给按钮绑定单击事件
    document.getElementById("btn").onclick = function () {
        // 将表单数据转为json
        var formData = {
            brandName:"",
            companyName:"",
            ordered:"",
            description:"",
            status:"",
        };
        // 获取表单数据
        let brandName = document.getElementById("brandName").value;
        // 设置数据
        formData.brandName = brandName;

        // 获取表单数据
        let companyName = document.getElementById("companyName").value;
        // 设置数据
        formData.companyName = companyName;

        // 获取表单数据
        let ordered = document.getElementById("ordered").value;
        // 设置数据
        formData.ordered = ordered;

        // 获取表单数据
        let description = document.getElementById("description").value;
        // 设置数据
        formData.description = description;

        let status = document.getElementsByName("status");
        for (let i = 0; i < status.length; i++) {
            if(status[i].checked){
                //
                formData.status = status[i].value ;
            }
        }
        //console.log(formData);
        //2. 发送ajax请求
        axios({
            method:"post",
            url:"http://localhost:8080/brand-demo/addServlet",
            //data后放JSON，js会自动转成JSON字符串
            data:formData
        }).then(function (resp) {
            // 判断响应数据是否为 success
            if(resp.data == "success"){
                location.href = "http://localhost:8080/brand-demo/brand.html";
            }
        })
    }
</script>
</body>
</html>
```

**说明：**

`查询所有` 功能和 `添加品牌` 功能就全部实现，大家肯定会感觉前端的代码很复杂；而这只是暂时的，后面学习了 `vue` 前端框架后，这部分前端代码就可以进行很大程度的简化。