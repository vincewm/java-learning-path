>  **导航：**
>
> [【Java笔记+踩坑汇总】JavaSE+JavaWeb+SSM+SpringBoot+瑞吉外卖+SpringCloud/SpringCloudAlibaba+黑马旅游+谷粒商城](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})

[TOC]



# 一、Request&Response概述

**Request是请求对象，Response是响应对象。**

> 思考：
>
> 这两个对象在我们使用Servlet的时候有看到，此时，我们就需要思考一个问题request和response这两个参数的作用是什么?
>
> ![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\848827677914460fa944799d9af81a3a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **request:获取请求数据**
  - 浏览器会发送HTTP请求到后台服务器[Tomcat]
  - HTTP的请求中会包含很多请求数据[请求行+请求头+请求体]
  - **后台服务器**[Tomcat]会对HTTP请求中的数据进行**解析**并把解析结果存入到**request****对象**中
  - 我们可以从request对象中获取请求的相关参数
  - 获取到数据后就可以继续后续的业务，比如获取用户名和密码就可以实现登录操作的相关业务
- **response:设置响应数据**
  - 业务处理完后，**后台就需要给前端返回业务处理的结果**即响应数据
  - 把响应数据封装到**response对象**中
  - 后台服务器[Tomcat]会**解析**response对象,按照[响应行+响应头+响应体]格式拼接结果
  - **浏览器**最终解析结果，把内容展示在浏览器给用户浏览

**案例：** 

对于上述所讲的内容，我们通过一个案例来初步体验下request和response对象的使用。

```java
@WebServlet("/demo3")
public class ServletDemo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //使用request对象 获取请求数据
        String name = request.getParameter("name");//url?name=zhangsan

        //使用response对象 设置响应数据
        response.setHeader("content-type","text/html;charset=utf-8");
        response.getWriter().write("<h1>"+name+",欢迎您！</h1>");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("Post...");
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动成功后就可以通过浏览器来访问，并且根据传入参数的不同就可以在页面上展示不同的内容:

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\deebef704b984b5d8014d5106719bb3f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **小结**
>
> 在这节中，我们主要认识了下request对象和reponse对象:
>
> - request对象是用来封装请求数据的对象
> - response对象是用来封装响应数据的对象



# 二、Request对象

## 2.1 Request继承体系

- **Tomcat需要解析请求数据，封装为request对象,并且创建request对象传递到service方法**

> **思考**
>
> - ServletRequest和HttpServletRequest的关系是什么?
> - request对象是有谁来创建的?
> - request提供了哪些API,这些API从哪里查?

**Request的继承体系:**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\524cfbc81bde458d9e00b7dbe059457f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**`RequestFacade类`**:

- 该类是Tomcat定义的实现类，**实现了HttpServletRequest接口**，也间接实现了ServletRequest接口。
- Servlet类中的service方法、doGet方法或者是doPost方法最终都是由Web服务器[Tomcat]来调用的，所以**Tomcat提供了方法参数接口的具体实现类`RequestFacade`**，并完成了对象的创建
- 要想了解RequestFacade中都提供了哪些方法，我们可以直接查看JavaEE的API文档中关于ServletRequest和HttpServletRequest的接口文档，因为RequestFacade实现了其接口就需要重写接口中的方法



## 2.2 Request获取请求数据的方法

### 2.2.0 简述 

HTTP请求数据总共分为三部分内容，分别是**请求行、请求头、请求体**。

HTTP请求数据中包含了`请求行`、`请求头`和`请求体`，针对这三部分内容，Request对象都提供了对应的API方法来获取对应的值:

- **请求行**
  - getMethod()获取请求方式
  - getContextPath()获取项目访问路径
  - getRequestURL()获取请求URL
  - getRequestURI()获取请求URI
  - getQueryString()获取GET请求方式的请求参数
- **请求头**
  - getHeader(String name)根据请求头名称获取其对应的值
- **请求体**
  - 注意: **POST请求有请求体，GET请求无请求体**
  - 如果是纯文本数据:getReader()
  - 如果是字节数据如文件数据:getInputStream()

### **2.2.1 获取请求行数据**

请求行包含三块内容，分别是`请求方式`、`请求资源路径`、`HTTP协议及版本`![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\1afafada0208470ab51aec745f89f092.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



对于这三部分内容，request对象都提供了对应的API方法来获取，具体如下:

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\d7a3ef59ca63473f93e8f076ba9320d8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **获取请求方式**: `GET`

```
String getMethod()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **获取虚拟目录**(项目名/项目访问路径): `/request-demo`

```
String getContextPath()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **获取URL**(统一资源定位符): `http://localhost:8080/request-demo/req1`

```
StringBuffer getRequestURL()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **获取URI**(统一资源标识符): `/request-demo/req1`

```
String getRequestURI()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **获取请求参数**(GET方式): `username=zhangsan&password=123`

```
String getQueryString()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

介绍完上述方法后，咱们通过代码把上述方法都使用下:

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\94ea20a9095b40a6b79217c313119c60.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="/request-demo/req1" method="get" target="_blank">
    <input name="username"/><input type="submit"/>
</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```java
/**
 * request 获取请求数据
 */
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // String getMethod()：获取请求方式： GET
        String method = req.getMethod();
        System.out.println(method);//GET
        // String getContextPath()：获取虚拟目录(项目访问路径)：/request-demo
        String contextPath = req.getContextPath();
        System.out.println(contextPath);
        // StringBuffer getRequestURL(): 获取URL(统一资源定位符)：http://localhost:8080/request-demo/req1
        StringBuffer url = req.getRequestURL();
        System.out.println(url.toString());
        // String getRequestURI()：获取URI(统一资源标识符)： /request-demo/req1
        String uri = req.getRequestURI();
        System.out.println(uri);
        // String getQueryString()：获取请求参数（GET方式）： username=zhangsan
        String queryString = req.getQueryString();
        System.out.println(queryString);
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动服务器，访问`http://localhost:8080/request-demo/req1?username=zhangsan&passwrod=123`，获取的结果如下:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\5983c12fe66a4903b18e13b36c49891a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **2.2.2 获取请求头数据**

对于请求头的数据，格式为`key: value`如下:

```
Host: 表示请求的主机名
User-Agent: 浏览器版本,例如Chrome浏览器的标识类似Mozilla/5.0 ...Chrome/79，IE浏览器的标识类似Mozilla/5.0 (Windows NT ...)like Gecko；
Accept：表示浏览器能接收的资源类型，如text/*，image/*或者*/*表示所有；
Accept-Language：表示浏览器偏好的语言，服务器可以据此返回不同语言的网页；
Accept-Encoding：表示浏览器可以支持的压缩类型，例如gzip, deflate等。
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\40cea659a6bb48649bb0cc2d7efce43d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 

所以根据请求头名称获取对应值的方法为:

```java
String getHeader(String name)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

接下来，在代码中如果想要获取客户端浏览器的版本信息，则可以使用

```java
/**
 * request 获取请求数据
 */
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求头: user-agent: 浏览器的版本信息
        String agent = req.getHeader("user-agent");
		System.out.println(agent);
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```

```

重新启动服务器后，`http://localhost:8080/request-demo/req1?username=zhangsan&passwrod=123`，获取的结果如下:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\28cf9a7e49f3400898ea0500acede9da.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **2.2.3 获取请求体数据**

浏览器在发送GET请求的时候是没有请求体的，请求参数在请求行里。

所以需要把请求方式变更为POST，请求参数QueryString在请求体里。请求体中的数据格式如下:

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\2111a1ae8f9c4bfb827f6eabb4cced4f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

Request对象**获取请求体数据方式：**

- **获取字节输入流**，如果前端发送的是字节数据，比如传递的是文件数据，则使用该方法

```
ServletInputStream getInputStream()
该方法可以获取字节
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **获取字符输入流**，如果前端发送的是纯文本数据，则使用该方法

```
BufferedReader getReader()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**示例：** 

1.在项目的webapp目录下添加一个html页面，名称为：`req.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!-- 
    action:form表单提交的请求地址
    method:请求方式，指定为post
-->
<form action="/request-demo/req1" method="post">
    <input type="text" name="username">
    <input type="password" name="password">
    <input type="submit">
</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.调用getReader()或者getInputStream()方法，因为目前前端传递的是纯文本数据，所以我们采用getReader()方法来获取

```java
/**
 * request 获取请求数据
 */
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
         //获取post 请求体：请求参数
        //1. 获取字符输入流
        BufferedReader br = req.getReader();
        //2. 读取数据，读一行即可，因为请求体只有一行。所有请求参数会用＆符号拼接成一行
        String line = br.readLine();    
        System.out.println(line);
        //br.close();//可以不写，因为销毁request后br也就跟着销毁了
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> BufferedReader流是通过request对象来获取的，当**请求完成后request对象就会被销毁**，request对象被销毁后，**BufferedReader流就会自动关闭**，所以此处就不需要手动关闭流了。

3.启动服务器，通过浏览器访问`http://localhost:8080/request-demo/req.html`![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\eb3e882514f24fe5a8b9e05d32c8685a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



点击`提交`按钮后，就可以在控制台看到前端所发送的请求数据![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\4c26f7601c6d4e16b4ae7b73f0fff818.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.2.4 获取请求参数的通用方式



**1.什么是请求参数?**

我们拿用户登录的例子来说明，**用户名和密码其实就是我们所说的请求参数**。

**2.什么是请求数据?**

**请求数据则是包含请求行、请求头和请求体的所有数据**

获取请求参数的两种方法： 

**方法一：获取连体参数，get和post不同**

- GET方式:

```java
String getQueryString()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- POST方式:

```java
BufferedReader getReader();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**示例：**

（1）发送一个GET请求并携带用户名，后台接收后打印到控制台

（2）发送一个POST请求并携带用户名，后台接收后打印到控制台

代码如下:

```java
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        String result = req.getQueryString();
        System.out.println(result);

    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        BufferedReader br = req.getReader();
        String result = br.readLine();
        System.out.println(result);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

因为get和post请求参数分别在请求行和请求体，故存在代码重复问题![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\4cecd1aafd0e4ce29acb2c1f2d0366f4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**方法二:通用方法获取分割后的参数，get和post通用**

request对象把分割后的请求参数，存入到一个Map集合中:

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\8fc35addea01416fbd85eb06046d870c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**注意**:因为参数的值可能是一个，也可能有多个，所以Map的值的类型为String数组。

基于上述理论，request对象为我们提供了如下方法:

- **获取所有参数Map集合**

```java
Map<String,String[]> getParameterMap()    //标签的name：value。值是数组，因为有时传来的同name键对应多个value，例如checkbox。
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **根据名称获取参数值（数组）**

```java
String[] getParameterValues(String name)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **根据名称获取参数值(单个值)，最常用**

```java
String getParameter(String name)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> 用方法一获取后，再用方法一还能获取数值，再用方法二会返回不到数值。 
>
> 用方法二获取后，再用方法二还能获取数值，再用方法一会返回不到数值。

**案例演示：**

1.修改req.html页面，添加爱好选项，爱好可以同时选多个

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="/request-demo/req2" method="get">
    <input type="text" name="username"><br>
    <input type="password" name="password"><br>
    <input type="checkbox" name="hobby" value="1"> 游泳
    <input type="checkbox" name="hobby" value="2"> 爬山 <br>
    <input type="submit">

</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\2b59716e257f45f38cb468d875633ba6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



2.在Servlet代码中获取页面传递GET请求的参数值

2.1获取GET方式的所有请求参数

```java
/**
 * request 通用方式获取请求参数
 */
@WebServlet("/req2")
public class RequestDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //GET请求逻辑
        System.out.println("get....");
        //1. 获取所有参数的Map集合
        Map<String, String[]> map = req.getParameterMap();
        for (String key : map.keySet()) {
            // username:zhangsan lisi
            System.out.print(key+":");

            //获取值
            String[] values = map.get(key);
            for (String value : values) {
                System.out.print(value + " ");
            }

            System.out.println();
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req,resp);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

获取的结果为:

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\9c88f405bdb7487fbfc91edad92730b8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



2.2获取GET请求参数中的爱好，结果是数组值

```java
/**
 * request 通用方式获取请求参数
 */
@WebServlet("/req2")
public class RequestDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //GET请求逻辑
        //...
        System.out.println("------------");
        String[] hobbies = req.getParameterValues("hobby");
        for (String hobby : hobbies) {
            System.out.println(hobby);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

获取的结果为:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\4491124abc10497e9992d137a339638a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



2.3获取GET请求参数中的用户名和密码，结果是单个值

```java
/**
 * request 通用方式获取请求参数
 */
@WebServlet("/req2")
public class RequestDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //GET请求逻辑
        //...
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println(username);
        System.out.println(password);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

获取的结果为:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\6c1381f4e99941b8be1d2603d27a3735.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



post与get一样，在Servlet代码中获取页面传递POST请求的参数值；将req.html页面form表单的提交方式改成post；将doGet方法中的内容**直接复制**到doPost方法中即可

> **小结**
>
> - req.getParameter()方法使用的频率会比较高
> - **以后**我们再写代码的时候，就**只需要按照如下格式来编写:**
>
> ```java
> public class RequestDemo1 extends HttpServlet {
>     @Override
>     protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>        //采用request提供的获取请求参数的通用方式来获取请求参数
>        //编写其他的业务代码...
>     }
>     @Override
>     protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>         this.doGet(req,resp);
>     }
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 2.3 IDEA使用模板创建Servlet（继承HttpServlet版）

使用通用方式获取请求参数后，屏蔽了GET和POST的请求方式代码的不同，则代码可以定义如下格式:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\33703be6b5e748cab13a15126b08a4af.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



由于格式固定，所以我们可以使用IDEA提供的模板来制作一个Servlet的模板，这样我们后期在创建Servlet的时候就会更高效，具体如何实现:

(1)按照自己的需求，修改Servlet创建的模板内容。annotated译为带注释的

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\d5bd500d65884e76a11e8afcdc947570.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 主要改动注解和加this使代码简洁：

```java
@WebServlet("/${Entity_Name}")
public class ${Class_Name} extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request,response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

（2）使用servlet模板创建Servlet类![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\9e3f65bef9a544739627210ad5374313.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**IDEA中new 没有\**[servlet](https://so.csdn.net/so/search?q=servlet&spm=1001.2101.3001.7020)\** 的选项解决方法：**

首先检查Servlet的依赖是否导入pom.xml

```XML
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
    </dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

file-项目结构（注意main文件夹下要有java和resources目录）：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\c9bb1e807484474aaf5509b3dd6d774e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





## 2.4 请求参数中文乱码问题

### 2.4.1 乱码原因和解决思路 

**getParameter方法**

**post乱码原因：**获取参数底层是获取请求体方法getReader()，获取到的**参数编码为**I**SO-8859-1**。

**解决思路：设置请求编码为utf-8**，或者将请求参数的字符串解码为utf-8。

**get乱码原因：**提交表单后，get请求参数会进行SO-8859-1的url编码追加到地址栏链接后面，Tomcat7获取到的**参数编码为**I**SO-8859-1的url编码**，Tomcat8获取到的参数编码为**utf-8的URL编码**。

**解决思路：**使用Tomcat8、9、10，或者先ISO-8859-1的url解码成字符数组，再utf-8编码。

- **POST请求解决方案是:**设置输入流的编码

  ```java
  request.setCharacterEncoding("UTF-8");    //注意HTML页面head里设置编码也要是utf-8
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **GET请求解决方案：**使用Tomcat8及以上版本。

- 通用方式（GET/POST）：需要先解码，再编码

  ```
  new String(username.getBytes("ISO-8859-1"),"UTF-8");
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**总结：Tomcat8只setCharacterEncoding就可以解决所有编码中文问题。**

getQueryString和getReader方法：

```
URLDecoder.decode(request.getQueryString(),"utf-8")
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **问题展示:**

(1)将req.html页面的请求方式修改为get

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="/request-demo/req2" method="get">
    <input type="text" name="username"><br>
    <input type="password" name="password"><br>
    <input type="checkbox" name="hobby" value="1"> 游泳
    <input type="checkbox" name="hobby" value="2"> 爬山 <br>
    <input type="submit">

</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(2)在Servlet方法中获取参数，并打印

```java
/**
 * 中文乱码问题解决方案
 */
@WebServlet("/req4")
public class RequestDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       //1. 获取username
       String username = request.getParameter("username");
       System.out.println(username);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

（3）启动服务器，页面上输入中文参数，提交后会发现控制台中文乱码：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\a4667dc7960f401ea8e24393b9fee047.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





### 2.4.2 POST请求**getParameter**解决方案 

-  设置输入流的编码

  ```
  request.setCharacterEncoding("UTF-8");
  注意:设置的字符集要和页面保持一致
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 

- 分析出现中文乱码的**原因**：

  - POST的请求参数是通过request的**getReader()**来获取流中的数据
  - 在**获取流**的时候解码方式是ISO-8859-1
  - **ISO-8859-1**编码是**不支持中文**的，所以会出现乱码

- **解决方案：**

  - 页面设置的编码格式为UTF-8
  - 把TOMCAT在获取流数据之前的编码设置为UTF-8
  - 通过request.setCharacterEncoding("UTF-8")设置编码,UTF-8也可以写成小写

**getParameter代码:**

```java
/**
 * 中文乱码问题解决方案
 */
@WebServlet("/req4")
public class RequestDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 解决乱码: POST getReader()
        //设置字符输入流的编码，设置的字符集要和页面保持一致
        request.setCharacterEncoding("UTF-8");    //Tomcat8可以注释这句
       //2. 获取username
       String username = request.getParameter("username");
       System.out.println(username);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**getReader代码:** 

```java
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        BufferedReader br = request.getReader();
        String string=br.readLine();
        System.out.println(URLDecoder.decode(string,"utf-8"));
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



至此POST请求中文乱码的问题就已经解决，但是这种方案**不适用于GET请求**，这个原因是什么呢，咱们下面再分析。

> **如果还是中文乱码，检查HTML，要设置编码为utf-8，浏览器使用谷歌浏览器，要ctrl+f5清缓存刷新测试页面。**
>
> ```html
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <title>Title</title>
> </head>
> <body>
> <!--
>     action:form表单提交的请求地址
>     method:请求方式，指定为post
> -->
> <form action="/untitled/servletDemo" method="post">
>     <input type="text" name="username">
>     <input type="password" name="password">
>     <input type="submit">
> </form>
> </body>
> </html>
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **2.4.3 GET请求getParameter解决方案**

在Tomcat7要new String(username.getBytes("ISO-8859-1"),"UTF-8");**Tomcat8直接用不会乱码**。



**`POST请求的中文乱码解决方案为什么不适用GET请求？`**

- request.**setCharacterEncoding**("utf-8")是设置request处理**流**的编码
- **getQueryString**方法并**没有**通过**流**的方式获取数据

所以GET请求不能用设置编码的方式来解决中文乱码问题。

**GET请求中文参数乱码的原因**

- 浏览器把中文参数按照`UTF-8`进行URL编码（URL编码示例：%E9%9D%9E。Chrome地址栏会把URL编码转成utf-8方便阅读，i传到服务器的还是URL编码）
- Tomcat对获取到的内容进行了`ISO-8859-1`的URL解码
- 在控制台就会出现类上`å¼ ä¸`的乱码，最后一位是个空格

> **思考:**
>
> 如果把`req.html`页面的`<meta>`标签的charset属性改成`ISO-8859-1`,后台不做操作，能解决中文乱码问题么?
>
> 答案是否定的，因为**`ISO-8859-1`本身是不支持中文展示**的，所以改了<meta>标签的charset属性后，会导致页面上的中文内容都无法正常展示。

### **2.4.4 URL编码解码**

这块知识了解即可。

具体编码过程分两步，分别是:

(1)将字符串按照**编码**方式转为**二进制**

(2)每个字节转为2个16进制数并在前边加上%

`例如，张三`按照UTF-8的方式转换成二进制的结果为:

```
1110 0101 1011 1100 1010 0000 1110 0100 1011 1000 1000 1001
```

**计算utf-8字符串二进制方法**

使用`http://www.mytju.com/classcode/tools/encode_utf8.asp`，输入`张三`![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\d3554e93521844baa712f112ce17859e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



就可以获取张和三分别对应的16进制。在计算的十六进制结果中，每两位前面加一个%,就可以获取到`%E5%BC%A0%E4%B8%89`。

但是对于上面的计算过程，如果没有工具，纯手工计算的话，相对来说还是比较复杂的，我们也不需要进行手动计算，在Java中已经为我们提供了编码和解码的API工具类可以让我们更快速的进行编码和解码:

Java中url**编码和解码的API工具类**

**编码:**

```
java.net.URLEncoder.encode("需要被编码的内容","字符集(UTF-8)")
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**解码:**

```
java.net.URLDecoder.decode("需要被解码的内容","字符集(UTF-8)")
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

接下来咱们对`张三`来进行编码和解码

```java
import java.io.UnsupportedEncodingException;
import java.net.URLDecoder;
import java.net.URLEncoder;
public class URLDemo {

  public static void main(String[] args) throws UnsupportedEncodingException {
        String username = "张三";
        //1. URL编码
        String encode = URLEncoder.encode(username, "utf-8");
        System.out.println(encode); //打印:%E5%BC%A0%E4%B8%89

       //2. URL解码
       //String decode = URLDecoder.decode(encode, "utf-8");//打印:张三
       String decode = URLDecoder.decode(encode, "ISO-8859-1");//打印:`å¼ ä¸ `
       System.out.println(decode);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**分析解决乱码原理：**

- 在进行编码和解码的时候，不管使用的是哪个字符集，他们对应的`%E5%BC%A0%E4%B8%89`是一致的

- 那他们对应的二进制值也是一样的，为:

  - ```
    1110 0101 1011 1100 1010 0000 1110 0100 1011 1000 1000 1001
    ```

- 所以我们可以考虑**把`å¼ ä¸`转换成字节，在把字节转换成`张三`**，使转换的过程中是它们的编码一致，就可以解决中文乱码问题。

**具体的实现步骤为:**

> 1.按照ISO-8859-1编码获取乱码`å¼ ä¸`对应的字节数组
>
> 2.按照UTF-8编码获取字节数组对应的字符串



**解决代码**

```java
/**
 * 中文乱码问题解决方案
 */
@WebServlet("/req4")
public class RequestDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 解决乱码：POST，getReader()
        //request.setCharacterEncoding("UTF-8");//设置字符输入流的编码


        //3. GET,获取参数的方式：getQueryString
        // 乱码原因：tomcat进行URL解码，默认的字符集ISO-8859-1
       /* //3.1 先对乱码数据进行编码：转为字节数组
        byte[] bytes = username.getBytes(StandardCharsets.ISO_8859_1);
        //3.2 字节数组解码
        username = new String(bytes, StandardCharsets.UTF_8);*/

        username  = new String(username.getBytes(StandardCharsets.ISO_8859_1),StandardCharsets.UTF_8);

        System.out.println("解决乱码后："+username);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意**
>
> 把`request.setCharacterEncoding("UTF-8")`代码注释掉后，会发现GET请求参数乱码解决方案同时也可也把POST请求参数乱码的问题也解决了。
>
> 只不过对于POST请求参数一般都会比较多，采用这种方式解决乱码起来比较麻烦，所以对于POST请求还是建议使用设置编码的方式进行。

另外需要说明一点的是**Tomcat8.0之后，已将GET请求乱码问题解决，设置默认的解码方式为UTF-8**

> **小结**
>
> **中文乱码解决方案**
>
> POST请求和GET请求的参数中如果有中文，后台接收数据就会出现中文乱码问题
>
> GET请求在Tomcat8.0以后的版本就不会出现了
>
> POST请求解决方案是:设置输入流的编码
>
> ```
> request.setCharacterEncoding("UTF-8");
> 注意:设置的字符集要和页面保持一致
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 所有Tomcat版本通用方式（GET/POST）：需要先解码，再编码
>
> ```
> new String(username.getBytes("ISO-8859-1"),"UTF-8");
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> **URL编码实现方式:**
>
> - 编码:
>
>   ```
>   URLEncoder.encode(str,"UTF-8");
>   ```
>
>   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
>   
>
> - 解码:
>
>   ```
>   URLDecoder.decode(s,"ISO-8859-1");
>   ```
>
>   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
>   

## 2.5 Request请求转发

**请求转发(forward):**一种在**服务器内部**的资源跳转方式。

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\8da494a87b324285a09f0cdc97f2b5ab.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\1f49ef8cfa4849aa962d27f0d737703f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



(1)浏览器发送请求给服务器，服务器中对应的资源A接收到请求

(2)资源A处理完请求后将请求**发给**资源B

(3)资源B处理完后将结果响应给浏览器，**继续执行A剩下代码**

(4)请求从资源A到资源B的过程就叫**请求转发**

**请求转发的实现方式:**

```java
req.getRequestDispatcher("资源B路径").forward(req,resp);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**请求转发的特点：**

- **浏览器地址栏路径不发生变化**

  虽然后台从`/req5`转发到`/req6`,但是浏览器的地址一直是`/req5`,未发生变化

- **只能转发到当前服务器的内部资源。**不能从一个服务器通过转发访问另一台服务器

- **一次请求**，可以在转发资源间使用**request共享数据**

  虽然后台从`/req5`转发到`/req6`，但是这个只有一次请求

**案例：** 

具体如何来使用，我们先来看下需求:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\f52244a814d64366ab23ebab1507f4c7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



针对上述需求，具体的实现步骤为:

(1)创建RequestDemo5类

```java
/**
 * 请求转发
 */
@WebServlet("/req5")
public class RequestDemo5 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo5...");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(2)创建RequestDemo6类

```java
/**
 * 请求转发
 */
@WebServlet("/req6")
public class RequestDemo6 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo6...");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(3)在RequestDemo5的doGet方法中进行请求转发

```java
/**
 * 请求转发
 */
@WebServlet("/req5")
public class RequestDemo5 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo5...");
        //请求转发
        request.getRequestDispatcher("/req6").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(4)启动测试

访问`http://localhost:8080/request-demo/req5`,就可以在控制台看到如下内容:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\aadb22240c3641b6849f8ac12e3e9248.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



说明请求已经转发到了`/req6`



**请求转发资源间共享数据:使用Request对象**

此处主要解决的问题是把请求从`/req5`转发到`/req6`的时候，如何传递数据给`/req6`。

需要使用**request对象**提供的三个**方法**:

- 存储数据到request域[范围,数据是存储在request对象]中

```
void setAttribute(String name,Object o);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 根据key获取值

```
Object getAttribute(String name);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 根据key删除该键值对

```
void removeAttribute(String name);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**代码示例：**![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\fd77d7c4e662498aac6d4d8cf04437af.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> 1.在RequestDemo5的doGet方法中转发请求之前，将数据存入request域对象中
>
> 2.在RequestDemo6的doGet方法从request域对象中获取数据，并将数据打印到控制台
>
> 3.启动访问测试

(1)修改RequestDemo5中的方法

```java
@WebServlet("/req5")
public class RequestDemo5 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo5...");
        //存储数据
        request.setAttribute("msg","hello");
        //请求转发
        request.getRequestDispatcher("/req6").forward(request,response);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(2)修改RequestDemo6中的方法

```java
/**
 * 请求转发
 */
@WebServlet("/req6")
public class RequestDemo6 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo6...");
        //获取数据
        Object msg = request.getAttribute("msg");
        System.out.println(msg);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(3)启动测试

访问`http://localhost:8080/request-demo/req5`,就可以在控制台看到如下内容:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\c04d251727c6472c8e18528d27a1015a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



此时就可以实现在转发多个资源之间共享数据。





# 三、Response对象



- **Request:**使用request对象来**获取请求数据**
- **Response:**使用response对象来**设置响应数据**

**Reponse的继承体系:**![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\0e6ca9d87f774764924ba325ecc75442.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 3.1 Response设置响应数据

HTTP响应数据总共分为三部分内容，分别是**响应行、响应头、响应体**，对于这三部分内容的数据，respone对象都提供了哪些方法来进行设置?

**响应行**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\e6d47b1f246e488d8d22d09cadbb50a7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



常用的就是设置响应状态码:

```
void setStatus(int sc);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**响应头**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\95c80e51e82848cbb4407dab197fc162.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



设置响应头键值对：

```
void setHeader(String name,String value);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**响应体**![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\1036b66f373d4f5abb3f337dd1cd14dd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



对于响应体，是通过字符、字节**输出流**的方式往浏览器写，

获取字符输出流:

```
PrintWriter getWriter();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

获取字节输出流

```
ServletOutputStream getOutputStream();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 3.2 Respones请求重定向

### 3.2.1 重定向

**Response重定向(redirect):一种资源跳转方式。**

重定向只是向response中添加了一条重定向地址，并不会立即响应给浏览器，只有当doFilter()或者**service()执行完毕**才会将响应信息封装起来发送给浏览器。

**省流：浏览器请求资源A，A处理不了说B能处理，浏览器再请求资源B。**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\f521cd7bb58f49dba8e2be9b6f315424.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\eaa432637c7f45d4843ad8b0fc87c52a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



(1)浏览器发送请求给服务器，服务器中对应的资源A接收到请求

(2)资源A现在无法处理该请求，就会先将A中代码运行完毕，再给浏览器响应一个**302的状态码+location**的一个访问资源B的路径

(3)**浏览器（对比，请求转发是直接资源a到资源b）**接收到响应状态码为302就会重新**发送请求**到location对应的访问地址去**访问资源B**

(4)资源B接收到请求后进行处理并最终给浏览器响应结果，这整个过程就叫**重定向**

**状态码分类**   说明
 1xx   响应中——临时状态码，表示请求已经接受，告诉客户端应该继续请求或者如果它已经完成则忽略它
 2xx   成功——表示请求已经被成功接收，处理已完成
 3xx   重定向——重定向到其它地方：它让客户端再发起一个请求以完成整个处理。
 4xx   客户端错误——处理发生错误，责任在客户端，如：客户端的请求一个不存在的资源，客户端未被授权，禁止访问等
 5xx   服务器端错误——处理发生错误，责任在服务端，如：服务端抛出异常，路由出错，HTTP版本不支持等

**重定向的实现方式一:**

```
resp.setStatus(302);
resp.setHeader("location","资源B的访问路径");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**重定向的实现方式二：推荐**

```java
        resposne.sendRedirect("/request-demo/resp2")
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```java
//动态获取项目虚拟目录更好
        String contextPath = request.getContextPath();
        response.sendRedirect(contextPath+"/resp2");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**案例：**![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\4817f185f5ed47f094cc922b98d89748.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



针对上述需求，具体的实现步骤为:

> 1.创建一个ResponseDemo1类，接收/resp1的请求，在doGet方法中打印`resp1....`
>
> 2.创建一个ResponseDemo2类，接收/resp2的请求，在doGet方法中打印`resp2....`
>
> 3.在ResponseDemo1的方法中使用
>
> response.setStatus(302);
>
> response.setHeader("Location","/request-demo/resp2") 来给前端响应结果数据
>
> 4.启动测试

(1)创建ResponseDemo1类

```java
@WebServlet("/resp1")
public class ResponseDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp1....");
        //重定向
        //1.设置响应状态码 302
        response.setStatus(302);
        //2. 设置响应头 Location
        response.setHeader("Location","/request-demo/resp2");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(2)创建ResponseDemo2类

```java
@WebServlet("/resp2")
public class ResponseDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp2....");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(3)启动测试

访问`http://localhost:8080/request-demo/resp1`,就可以在控制台看到如下内容:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\98da4af110a94878b322083508707da8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



说明`/resp1`和`/resp2`都被访问到了。到这重定向就已经完成了。

**简化的重定向编写方式**为:

```
resposne.sendRedirect("/request-demo/resp2")
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

所以第1步中的代码就可以简化为：

```java
@WebServlet("/resp1")
public class ResponseDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp1....");
        //重定向
        resposne.sendRedirect("/request-demo/resp2")；
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**重定向的特点：（与请求转发正好相反）**

- 浏览器**地址栏**路径发送**变化**

  当进行重定向访问的时候，由于是由浏览器发送的两次请求，所以地址会发生变化

- 可以重定向到任何位置的资源(服务**内容**、**外部**均可)

  因为第一次响应结果中包含了浏览器下次要跳转的路径，所以这个路径是可以任意位置资源。

- **两次请求**，**不能**在多个资源使用**request共享**数据

  因为浏览器发送了两次请求，是两个不同的request对象，就无法通过request对象进行共享数据

- **重定向刷新不会重新提交表单，效率低，适用于不同业务间。**

介绍完**请求重定向**和**请求转发**以后，接下来需要把这两个放在一块对比下:![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\b05c3587595a4a5da2b5bc4d5572c7be.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



以后到底用哪个，还是需要根据具体的业务来决定。

### 3.2.2 对比转发和重定向，区别和应用场景

**区别** 

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\b05c3587595a4a5da2b5bc4d5572c7be.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**1.跳转的范围不同**
 由于转发是在服务器内部进行的，跳转的范围被限制在当前服务器的当前应用。

而重定向由浏览器发送URL请求完成，范围是所有服务器的所有应用

**2.“/”标识符代表的含义不同**
 由于转发是在服务器内部进行的，在指定转发的URL中，“/”代表当前应用

而重定向的“/”则代表当前服务器。

**3.刷新后是否会重新提交表单/参数**
 转发：对于转发而言，通过Request对象携带的**参数会继续存在**，若刷新当前页面，则会导致已经提交的表单**再次提交**，对于主流浏览器而言，此时会弹出**是否重复提交表单**的确认弹窗。

重定向：而重定向**不会携带**这些数据，刷新时安全的。

**6.效率不同**
 对于**转发**而言，过程发生在服务器内部，不经过重定向的二次网络过程和请求，因此**效率更高**

**7.携带参数的方式不同**
 对于转发而言，携带参数跳转的方式是通过方法request.setParameter来绑定。

而对于重定向，一种可行的办法是用?key=value&key2=value2的方式在URL后面增加显性参数。

**应用场景：**

**重定向刷新不会重新提交表单，效率低，适用于不同业务间。**
 建议一：

对于**竭力避免表单重复提交**的场景下选择**重定向**方式，防止不断刷新页面引起的重复提交表单。

建议二：

对于效率要求更高的场景选择服务器内转发

建议三：

若**携带较多参数**则选择服务器内**转发**，一般是同一业务内需要携带参数多。

请求转发偏向于、**为同一业务功能服务**
 重定向偏向于、**不同业务功能之间的跳转**

## 3.3 是否加虚拟目录的依据，动态配置虚拟目录



**问题1：**

转发的时候路径上没有加虚拟目录(项目访问路径)`/request-demo`而重定向加了虚拟目录。

那么到底**什么时候需要加，什么时候不需要加呢?**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\2c6e3b4923e7442fa6928268f96fcec3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**答案：是否加虚拟目录(项目访问路径)的依据**

- **浏览器使用:需要加虚拟目录(项目访问路径)**
- **服务端使用:不需要加虚拟目录**

转发是只能在同一服务器内跳转，虚拟目录是不变的，不加编译器能猜出来；重定向可以是不同服务器跳转，就需要指定虚拟目录。 

对于转发来说，因为是在服务端直接从资源a发送到b，所以不需要加虚拟目录

对于重定向来说，路径最终是由浏览器来发送请求到location地址去访问资源B，就需要添加虚拟目录。

> **练习：下面是否需要加虚拟目录**
>
> - `<a href='路劲'>`
> - `<form action='路径'>`
> - req.getRequestDispatcher("路径")
> - resp.sendRedirect("路径")

> **答案:**
>
> ```
> 1.超链接，从浏览器发送，需要加
> 2.表单，从浏览器发送，需要加
> 3.转发，是从服务器内部跳转，不需要加
> 4.重定向，是由浏览器进行跳转，需要加。
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 目前学的也就转发不加虚拟目录。 

**问题2：**

**如何动态配置项目虚拟目录。**

防止后期通过Tomcat插件配置了项目的访问路径，那么所有需要重定向的地方都需要重新修改 ![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\65b76f3d24a147148dfbac95c4ea5d15.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



答案也比较简单，我们可以在代码中**动态去获取项目访问的虚拟目录**，使用request对象中的请求行获取虚拟目录方法**getContextPath**()，修改后的代码如下:

```java
@WebServlet("/resp1")
public class ResponseDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp1....");

        //简化方式完成重定向
        //动态获取虚拟目录
        String contextPath = request.getContextPath();
        response.sendRedirect(contextPath+"/resp2");    //使用指定的重定向位置URL向客户端发送一个临时重定向响应，并清除缓冲区。
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

重新启动访问测试，功能依然能够实现，此时就可以动态获取项目访问的虚拟路径，从而降低代码的耦合度。

## 3.4 Response响应字符数据

> 了解即可，实际应用一般是把request转发到前端页面JSP中展示，每行用write写太复杂，并且前后端不分离。

**响应字符数据到浏览器**

- 先设置内容类型contentType和编码

  ```java
  response.setContentType("text/html;charset=utf-8");  
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 通过Response对象获取字符输出流： PrintWriter writer = resp.**getWriter**();

- 通过字符输出流写数据: writer.write("aaa");

 PrintWriter是字符打印流

**示例：**

1.返回一个简单的字符串`aaa`

```java
/**
 * 响应字符数据：设置字符数据的响应体
 */
@WebServlet("/resp3")
public class ResponseDemo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //必须设置编码，否则中文会乱码
        response.setContentType("text/html;charset=utf-8");    
        //1. 获取字符输出流
        PrintWriter writer = response.getWriter();
		 writer.write("aaa");
    }
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\f45d65c057db415db01086a39f802243.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**返回一串html字符串**，并且能被浏览器解析

```java
PrintWriter writer = response.getWriter();
//content-type，告诉浏览器返回的数据类型是HTML类型数据，这样浏览器才会解析HTML标签
//设置字符集防止乱码中文
response.setHeader("content-type","text/html;charset=utf-8");
//response.setContentType("text/html;charset=utf-8");//或者直接设置content-type
writer.write("<h1>aaa</h1>");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\ed21ea925a3b4bcdb2bb010d6cebf507.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**注意:**一次请求响应结束后，**response**对象就会被**销毁**掉，所以不**要手动关闭流**。

2.返回一个中文的字符串`你好`，需要注意设置响应数据的编码为`utf-8`

```java
//设置响应的数据格式及数据的编码
response.setContentType("text/html;charset=utf-8");
writer.write("你好");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\5c8fce5d4886485cbf339be97b38cb28.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 3.5 Response响应字节数据

**响应字节数据到浏览器**

- 通过Response对象获取字节输出流：ServletOutputStream outputStream = resp.**getOutputStream**();
- 通过字节输出流写数据: outputStream.**write**(字节数据);

**示例：**

**返回一个图片文件到浏览器**

```java
/**
 * 响应字节数据：设置字节数据的响应体
 */
@WebServlet("/resp4")
public class ResponseDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 读取文件
        FileInputStream fis = new FileInputStream("d://a.jpg");
        //2. 获取response字节输出流
        ServletOutputStream os = response.getOutputStream();
        //3.1. 方法一，完成流的copy
        byte[] buff = new byte[1024];
        int len = 0;
        while ((len = fis.read(buff))!= -1){
            os.write(buff,0,len);
        }
        //3.2.  方法二，工具类快速流的复制，需要pom导坐标commons-io
        //IOUtils.copy(fis,os);
        fis.close();
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\2bb75d4dfaa2409598a41e62dbe92e16.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**使用IOUtils.copy(fis,os)进行流的复制（推荐）**

(1)pom.xml添加依赖

```XML
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

(2)调用工具类方法实现复制

```java
//fis:输入流
//os:输出流
IOUtils.copy(fis,os);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

优化后的代码:

```java
/**
 * 响应字节数据：设置字节数据的响应体
 */
@WebServlet("/resp4")
public class ResponseDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 读取文件
        FileInputStream fis = new FileInputStream("d://a.jpg");
        //2. 获取response字节输出流
        ServletOutputStream os = response.getOutputStream();
        //3. 完成流的copy
      	IOUtils.copy(fis,os);
        fis.close();
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 四、Request、Response、Mybatis、前端注册登录小项目

## 4.1 代码

**需求：**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\63a9592c256c49baa465d4dac8785c80.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\c515d524432e4d1bb3869c99a75e30e3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**项目结构**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\ddf48b9597a34a779bb296244e2e9aea.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 **数据库准备**

```sql
-- 创建用户表，在db1数据库下创建
CREATE TABLE tb_user(
	id int primary key auto_increment,
	username varchar(20) unique,
	password varchar(32)
);

-- 添加数据
INSERT INTO tb_user(username,password) values('zhangsan','123'),('lisi','234');

SELECT * FROM tb_user;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **代码**

[Request、Response、Mybatis、前端注册登录小项目-Java文档类资源-CSDN下载](https://download.csdn.net/download/qq_40991313/86267342)

## 4.2 SqlSessionFactory工具类抽取

```java
String resource = "mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new 
	SqlSessionFactoryBuilder().build(inputStream);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

注册登录Servlet.java在使用Mybatis时候中都用到了上面代码，这些重复代码就会造成一些**问题:**

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
>  虽然上面语句也重复，但不能抽取到工具类里。因为SqlSession是一个连接、**会话**，每次连接数据库时候创建一次会话是合适，如果所有连接都共用一个会话会互相影响。
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

# 五、JSP

## 5.1 JSP 概述

> **了解即可**，现在基本都不用jsp了，新技术都是用vue、axios，前后端分离。jsp算旧技术，但有些项目是用jsp开发的，所以还是学一下。

**JSP（全称：Java Server Pages）：Java 服务端页面。**

是一种**动态的网页技术**，其中既可以定义 HTML、JS、CSS等静态内容，还可以定义 Java代码的动态内容，也就是 `JSP = HTML + Java`。

JSP和JavaScript是两码事，JSP是java服务端页面，JavaScript是脚本语言的一种。 

**jsp代码示例：**

```html
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <h1>JSP,Hello World</h1>
        <%
        	System.out.println("hello,jsp~");
        %>
    </body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面代码 `h1` 标签内容是展示在页面上，而 Java 的输出语句是**输出在 idea 的控制台**。

**JSP 作用：**

简化开发，避免了在Servlet中直接输出HTML标签，前后端分离。

如果只用 `servlet`，实现页面动态显示用户名：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\7ea0cc3f6630436a86c881f15477c760.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\83d8f078f5d84961b11a8d209d55de36.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



上面的代码有大量使用到 `writer` 对象向页面写标签内容，这样我们的代码就显得很麻烦；将来如果展示的效果出现了问题，排错也显得有点力不从心。

**用JSP**实现页面动态显示用户名：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\8d0f509d0664412181c6e62014cc4d65.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





上面代码可以看到里面基本都是 `HTML` 标签，而动态数据使用 Java 代码进行展示；这样操作看起来要比用 `servlet` 实现要舒服很多。

JSP 作用：简化开发，避免了在Servlet中直接输出HTML标签。

## 5.2 helloworld

接下来我们做一个简单的快速入门代码。

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\2654955a3d4048f2b151f5eb71b34973.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**创建maven的 web 项目**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\739965d4947f44fa81978c97bfb5f5a3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**导入JSP依赖**

```XML
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.2</version>
    <scope>provided</scope>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



`pom.xml` 文件内容如下：导入Servlet和JSP依赖，Tomcat插件

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>jsp-demo</artifactId>
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
            </plugin>
        </plugins>
    </build>
</project>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



该依赖的 `scope` 必须设置为 `provided`，因为 tomcat 中有这个jar包了，所以在打包时我们是不希望将该依赖打进到我们工程的war包中。

**创建 jsp 页面**

在项目的 `webapp` 下创建jsp页面

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\83eb4340d46947359e7fba7095182bee.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





通过上面方式创建一个名为 `hello.jsp` 的页面。

**编写代码**

在 `hello.jsp` 页面中书写 `HTML` 标签和 `Java` 代码，如下

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>hello jsp</h1>

    <%
        System.out.println("hello,jsp~");
    %>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**测试**

启动服务器并在浏览器地址栏输入 `http://localhost:8080/jsp-demo/hello.jsp`，我们可以在页面上看到如下内容：![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\6e203aaa2e70401eba68910363fc4424.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



>  **注意：**Tomcat版本和jdk版本不能差太大，例如jdk18、Tomcat8.5运行jsp就会报错HTTP 500-Unable to compile class for JSP，jdk18和Tomcat10会Servlet页面打不开400，**jdk18和Tomcat9正常。**



同时也可以看到在 `idea` 的控制台看到输出的 `hello,jsp~` 内容。

## 5.3 JSP 原理



**JSP 本质上就是一个 Servlet，**所以可以写 `Java` 代码**。**

**访问jsp时的流程**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\37c21c1529724295b81001ea24937154.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 最终对外提供服务的就是jsp转换、编译成的字节码文件。



1. 浏览器第一次访问 `hello.jsp` 页面
2. `tomcat` 会将 `hello.jsp` 转换为名为 **`hello_jsp.java`** 的一个 `Servlet`
3. `tomcat` 再将转换的 `servlet` 编译成字节码文件 **`hello_jsp.class`**
4. `tomcat` 会执行该字节码文件，向外提供服务

**验证jsp文件转成Servlet类** 

我们可以到项目所在磁盘目录下找 `target\tomcat\work\Tomcat\localhost\jsp-demo\org\apache\jsp` 目录，而这个目录下就能看到转换后的 `servlet`

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\705e023645f94f2aa0da9cb8ce048b76.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





打开 **`hello_jsp.java`** 文件，来查看里面的代码：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\af01e811b0944ff48967820dc79ee010.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





可以看到这个由jsp转成的**Servlet类继承**了名为 **`HttpJspBase`** 这个类，而通过Tomcat源码可以发现**`HttpJspBase`** 继承了 `HttpServlet` ：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\2093293fc94d47a0ace2d574b1b1f67b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

那么 `hello_jsp` 这个由jsp转换的类就间接的继承了 `HttpServlet` ，也就说明 **`hello_jsp` 是一个 `servlet`**。



`hello_jsp` 类有一个名为 **`_jspService()`** 的方法，该方法就是每次访问 `jsp` 时自动执行的方法，和 `servlet` 中的 `service` 方法一样 。

而在 `_jspService()` 方法中可以看到往浏览器写标签的代码：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\cb9131d785d247d7b6cdd3aacb0bdba4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





以前我们自己写 `servlet` 时，这部分代码是由我们自己来写，现在有了 `jsp` 后，由tomcat完成这部分功能。

## 5.4 JSP 脚本

JSP脚本用于在 JSP页面内定义 Java代码。

### 5.4.1 JSP脚本分类

JSP 脚本有如下三个分类：

- **<%...%>      ：**内容会直接放到_jspService()方法之中，中间内容在服务器运行
- **<%="…"%>     ：**内容会放到out.print()中，作为out.print()的参数，中间内容会打印在网页
- **<%!…%>      ：**内容会放到_jspService()方法之外，被类直接包含，中间定义成员变量、方法

> `jsp转成的Servlet类中的`**`_jspService()` 方法**就是每次访问 `jsp` 时自动执行的方法，和 `servlet` 中的 `service` 方法一样 。 

**代码演示：**

**<%...%>** 

在 `hello.jsp` 中书写

```Delphi
<%
    System.out.println("hello,jsp~");
    int i = 3;
%>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

通过浏览器访问 `hello.jsp` 后，查看转换的 `hello_jsp.java` 文件，i 变量定义在了 `_jspService()` 方法中![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\15826bd8aab84cc9980afdce49016b39.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 **<%=…%>**



在 `hello.jsp` 中书写

```Delphi
<%="hello"%>
<%=i%>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

通过浏览器访问 `hello.jsp` 后，查看转换的 `hello_jsp.java` 文件，该脚本的内容作为参数放在了 `out.print()` 中：

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\5f8ce4fd84324b8b90543b5ee97f4b1f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 **<%!…%>**



在 `hello.jsp` 中书写

```Delphi
<%!
    void  show(){}
	String name = "zhangsan";
%>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

通过浏览器访问 `hello.jsp` 后，查看转换的 `hello_jsp.java` 文件，该脚本的内容被放在了成员位置

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\f2b974bc79a2421bbcaac2578d4db8b1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





### 5.4.2 案例,使用JSP脚本展示品牌数据

**需求**

使用JSP脚本展示品牌数据

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\780df4531aa54f69890f57c8da879b96.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**素材**

静态的jsp

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>

<%
    // 查询数据库
    List<Brand> brands = new ArrayList<Brand>();
    brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
    brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
    brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));

%>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<input type="button" value="新增"><br>
<hr>
<table border="1" cellspacing="0" width="800">
    <tr>
        <th>序号</th>
        <th>品牌名称</th>
        <th>企业名称</th>
        <th>排序</th>
        <th>品牌介绍</th>
        <th>状态</th>
        <th>操作</th>

    </tr>
    <tr align="center">
        <td>1</td>
        <td>三只松鼠</td>
        <td>三只松鼠</td>
        <td>100</td>
        <td>三只松鼠，好吃不上火</td>
        <td>启用</td>
        <td><a href="#">修改</a> <a href="#">删除</a></td>
    </tr>

    <tr align="center">
        <td>2</td>
        <td>优衣库</td>
        <td>优衣库</td>
        <td>10</td>
        <td>优衣库，服适人生</td>
        <td>禁用</td>

        <td><a href="#">修改</a> <a href="#">删除</a></td>
    </tr>

    <tr align="center">
        <td>3</td>
        <td>小米</td>
        <td>小米科技有限公司</td>
        <td>1000</td>
        <td>为发烧而生</td>
        <td>启用</td>

        <td><a href="#">修改</a> <a href="#">删除</a></td>
    </tr>


</table>

</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**实体类Brand.java**

```java
package com.itheima.pojo;

/**
 * 品牌实体类
 */

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


    public Brand() {
    }

    public Brand(Integer id, String brandName, String companyName, String description) {
        this.id = id;
        this.brandName = brandName;
        this.companyName = companyName;
        this.description = description;
    }

    public Brand(Integer id, String brandName, String companyName, Integer ordered, String description, Integer status) {
        this.id = id;
        this.brandName = brandName;
        this.companyName = companyName;
        this.ordered = ordered;
        this.description = description;
        this.status = status;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getBrandName() {
        return brandName;
    }

    public void setBrandName(String brandName) {
        this.brandName = brandName;
    }

    public String getCompanyName() {
        return companyName;
    }

    public void setCompanyName(String companyName) {
        this.companyName = companyName;
    }

    public Integer getOrdered() {
        return ordered;
    }

    public void setOrdered(Integer ordered) {
        this.ordered = ordered;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public Integer getStatus() {
        return status;
    }

    public void setStatus(Integer status) {
        this.status = status;
    }

    @Override
    public String toString() {
        return "Brand{" +
                "id=" + id +
                ", brandName='" + brandName + '\'' +
                ", companyName='" + companyName + '\'' +
                ", ordered=" + ordered +
                ", description='" + description + '\'' +
                ", status=" + status +
                '}';
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**将 `brand.jsp` 页面改为动态的**

> ```
> for循环后面可以用JSP标准标签库JSTL的foreach标签优化
> ```

```Delphi
<%@ page import="com.itheima.pojo.Brand" %>
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>

<%
    // 查询数据库
    List<Brand> brands = new ArrayList<Brand>();
    brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
    brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
    brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));

%>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<input type="button" value="新增"><br>
<hr>
<table border="1" cellspacing="0" width="800">
    <tr>
        <th>序号</th>
        <th>品牌名称</th>
        <th>企业名称</th>
        <th>排序</th>
        <th>品牌介绍</th>
        <th>状态</th>
        <th>操作</th>
    </tr>
    <%
        for (int i = 0; i < brands.size(); i++) {
            Brand brand = brands.get(i);
    %>

    <tr align="center">
        <td><%=brand.getId()%></td>
        <td><%=brand.getBrandName()%></td>
        <td><%=brand.getCompanyName()%></td>
        <td><%=brand.getOrdered()%></td>
        <td><%=brand.getDescription()%></td>
		<td><%=brand.getStatus() == 1 ? "启用":"禁用"%></td>
        <td><a href="#">修改</a> <a href="#">删除</a></td>
    </tr>

    <%
        }
    %>
</table>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**测试**



在浏览器地址栏输入 `http://localhost:8080/jsp-demo/brand.jsp` ，页面展示效果如下

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\6fc1d1c218714b0d98de3a3d50d1eaf9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 5.4.3 JSP 缺点

通过上面的案例，我们可以看到 JSP 的很多缺点。

由于 JSP页面内，既可以定义 HTML 标签，又可以定义 Java代码，造成了以下问题：

难写难读难维护。

- **书写麻烦**：特别是复杂的页面

  既要写 HTML 标签，还要写 Java 代码

- 阅读麻烦

  上面案例的代码，相信你后期再看这段代码时还需要花费很长的时间去梳理

- 复杂度高：运行需要依赖于各种环境，JRE，JSP容器，JavaEE…

- 占内存和磁盘：JSP会自动生成.java和.class文件占磁盘，运行的是.class文件占内存

- **调试困难**：出错后，需要找到自动生成的.java文件进行调试

- 不利于团队协作：前端人员不会 Java，后端人员不精 HTML

  如果页面布局发生变化，前端工程师对静态页面进行修改，然后再交给后端工程师，由后端工程师再将该页面改为 JSP 页面

由于上述的问题， **JSP 已逐渐退出历史舞台，**以后开发更多的是使用 **HTML + Ajax** 来替代。Ajax 是异步的JavaScript。有个这个技术后，前端工程师负责前端页面开发，而后端工程师只负责前端代码开发。

**技术的发展过程**

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\3cca217276ea4c1bada5314ba7a1be4e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





1. 第一阶段：使用 `servlet` 即实现逻辑代码编写，也对页面进行拼接。这种模式我们之前也接触过

2. 第二阶段：随着技术的发展，出现了 `JSP` ，人们发现 `JSP` 使用起来比 `Servlet` 方便很多，但是还是要在 `JSP` 中嵌套 `Java` 代码，也不利于后期的维护

3. 第三阶段：使用 `Servlet` 进行逻辑代码开发，而使用 `JSP` 进行数据展示![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\81fa0038bd424d41ab476d0138ab2468.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

   

4. 第四阶段：使用 `servlet` 进行后端逻辑代码开发，而使用 `HTML` 进行数据展示。而这里面就存在问题，`HTML` 是静态页面，怎么进行动态数据展示呢？这就是 `ajax` 的作用了。

那既然 JSP 已经逐渐的退出历史舞台，那我们**为什么还要学习 `JSP` 呢**？原因有两点：

- 一些公司可能**有些老项目还在用** `**JS**P` ，所以要求我们必须动 `JSP`
- 我们如果不经历这些复杂的过程，就不能体现后面阶段开发的简单

接下来我们来学习第三阶段，使用 `EL表达式` 和 `JSTL` 标签库替换 `JSP` 中的 `Java` 代码。

## 5.5 EL 表达式

### 5.5.1 概述

EL（全称**Expression Language** ）表达式语言。

**作用：**

1.用于简化 JSP 页面内的 Java 代码。

2.主要作用是 **获取数据**。其实就是从**域对象**中获取数据，然后将数据展示在页面上。

**用法：**

page标签设置不忽略EI表达式

```Delphi
<%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**${表达式}** 。



例如：${brands} 就是获取域中存储的 key 为 brands 的数据。

> **回顾：**
>
> ${} ：学Mybatis时参数占位符：拼接SQL。底层使用的是 `Statement`，会存在SQL注入问题。

### 5.5.2 代码演示，**把Servlet的List转发给jsp页面输出**

- 定义servlet，在 servlet 中封装一些数据并存储到 request 域对象中并转发到 `el-demo.jsp` 页面。

  ```java
  @WebServlet("/demo1")
  public class ServletDemo1 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //1. 准备数据
          List<Brand> brands = new ArrayList<Brand>();
          brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
          brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
          brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));
  
          //2. 存储到request域中
          request.setAttribute("brands",brands);
  
          //3. 转发到 el-demo.jsp
          request.getRequestDispatcher("/el-demo.jsp").forward(request,response);
      }
  
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          this.doGet(request, response);
      }
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > **注意：** 此处需要用转发，因为**转发才可以使用 request 对象作为域对象进行数据共享**

- 在 `el-demo.jsp` 中通过 EL表达式 获取数据

  ```Delphi
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

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 在浏览器的地址栏输入 `http://localhost:8080/jsp-demo/demo1` ，页面效果如下：![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\ad56df4339214eff9333e4b7b01647ec.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

  

### 5.5.3 域对象

JavaWeb中有四大域对象，分别是：

- page：当前页面有效
- request：当前请求有效
- session：当前会话有效
- application：当前应用有效

el 表达式获取数据，会依次从这4个域中寻找，直到找到为止。而这四个域对象的作用范围如下图所示

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\51a5dfd530b74357a081240b37402c68.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





例如： ${brands}，el 表达式获取数据，会先从page域对象中获取数据，如果没有再到 requet 域对象中获取数据，如果再没有再到 session 域对象中获取，如果还没有才会到 application 中获取数据。

## 5.6 JSTL（JSP标准标签库）标签

### 5.6.1 概述

JSP标准标签库(Jsp Standarded Tag Library) ，**使用标签取代JSP页面上的Java代码。**

**示例**

```Delphi
<c:if test="${flag == 1}">
    男
</c:if>
<c:if test="${flag == 2}">
    女
</c:if>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面代码看起来比 JSP 中嵌套 Java 代码看起来舒服好了。

JSTL 提供了很多标签，如下图

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\a8ca611beb3e4900b8b1483374bc9e7e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**最常用的标签：**

`<c:forEach>` 标签和 `<c:if>` 标签。

**JSTL 使用**

- 导入坐标

  ```Delphi
  <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
  </dependency>
  <dependency>
      <groupId>taglibs</groupId>
      <artifactId>standard</artifactId>
      <version>1.1.2</version>
  </dependency>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 在JSP页面上引入JSTL标签库

  ```Delphi
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  要使用EL表达式记得isELIgnored="false"

- 使用标签

### 5.6.2 if 标签

`<c:if>`：相当于 if 判断，条件渲染

- 属性：test，用于定义条件表达式，**表达式要在$里判断**。test="${flag == 1}"可以，test="${flag }== 1"不行。

```Delphi
<c:if test="${flag == 1}">
    男
</c:if>
<c:if test="${flag == 2}">
    女
</c:if>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**代码演示：**

- 定义一个 `servlet` ，在该 `servlet` 中向 request 域对象中添加 键是 `status` ，值为 `1` 的数据

  ```java
  package web;
  
  import javax.servlet.*;
  import javax.servlet.http.*;
  import javax.servlet.annotation.*;
  import java.io.IOException;
  
  @WebServlet("/ServletDemo1")
  public class ServletDemo1 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //1. 存储数据到request域中
          request.setAttribute("status",1);
  
          //2. 转发到 jstl-if.jsp
          request.getRequestDispatcher("/hello.jsp").forward(request,response);
      }
  
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          this.doGet(request, response);
      }
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 定义 `hello.jsp` 页面，在该页面使用 `<c:if>` 标签

  ```Delphi
  <%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
  <%--<%@ page contentType="text/html;charset=UTF-8" language="java" %>--%>
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
  <html>
  <head>
    <title>Title</title>
  </head>
  <body>
  <%--
      c:if：来完成逻辑判断，替换java  if else，别忘了isELIgnored="false"
  --%>
  <c:if test="${status ==1}">
    启用
  </c:if>
  查看${status}
  <%
    System.out.println(request.getAttribute("status"));;
  %>
  <c:if test="${status ==0}">
    禁用
  </c:if>
  </body>
  </html>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > **注意：** 在该页面已经要引入 JSTL核心标签库
  >
  > `<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`

### 5.6.3 forEach 标签

`<c:forEach>`：相当于 for 循环。java中有增强for循环和普通for循环。



**用法一**

类似于 Java 中的增强for循环。涉及到的 `<c:forEach>` 中的属性如下

- items：被遍历的容器
- var：遍历产生的临时变量
- varStatus：遍历状态对象，用于自动生成序号，status.index是从0开始，status.count是从1开始

如下代码，是从域对象中获取名为 brands 数据，该数据是一个集合；遍历遍历，并给该集合中的每一个元素起名为 `brand`，是 Brand对象。在循环里面使用 EL表达式获取每一个Brand对象的属性值

```Delphi
<c:forEach items="${brands}" var="brand">
    <tr align="center">
        <td>${brand.id}</td>
        <td>${brand.brandName}</td>
        <td>${brand.companyName}</td>
        <td>${brand.description}</td>
    </tr>
</c:forEach>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```Delphi
    <c:forEach items="${brands}" var="brand" varStatus="status">
        <tr align="center">
            <td>${status.count}</td>
            <td>${brand.id}</td>
            <td>${brand.brandName}</td>
            <td>${brand.companyName}</td>
            <td>${brand.description}</td>
        </tr>
    </c:forEach>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **注意：** <td>${brand.id}</td>是给id转getId，调用Brand对象里的getId()方法，不是直接id成员变量。

**代码演示：**

- `servlet` 还是使用之前的名为 `ServletDemo1` 。

- 定义名为 `jstl-foreach.jsp` 页面，内容如下：

  ```Delphi
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
  
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
  <input type="button" value="新增"><br>
  <hr>
  <table border="1" cellspacing="0" width="800">
      <tr>
          <th>序号</th>
          <th>品牌名称</th>
          <th>企业名称</th>
          <th>排序</th>
          <th>品牌介绍</th>
          <th>状态</th>
          <th>操作</th>
      </tr>
  
      <c:forEach items="${brands}" var="brand" varStatus="status">
          <tr align="center">
              <%--<td>${brand.id}</td>--%>
              <td>${status.count}</td>
              <td>${brand.brandName}</td>
              <td>${brand.companyName}</td>
              <td>${brand.ordered}</td>
              <td>${brand.description}</td>
              <c:if test="${brand.status == 1}">
                  <td>启用</td>
              </c:if>
              <c:if test="${brand.status != 1}">
                  <td>禁用</td>
              </c:if>
              <td><a href="#">修改</a> <a href="#">删除</a></td>
          </tr>
      </c:forEach>
  </table>
  </body>
  </html>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**用法二**

类似于 Java 中的普通for循环。涉及到的 `<c:forEach>` 中的属性如下

- begin：开始数
- end：结束数
- step：步长

**实例代码：**

从0循环到10，变量名是 `i` ，每次自增1，可以配合a标签进行分页展示。

```Delphi
<c:forEach begin="0" end="10" step="1" var="i">
    ${i}
</c:forEach>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 5.7 MVC模式和三层架构

提高代码维护性和扩展性。

### 5.7.1 MVC模式

MVC 是一种分层开发的模式，其中：

- M：Model，**模型**。**处理业务**
- V：View，**视图**。界面展示
- C：Controller，**控制器**。获取并处理请求，调用模型来获取数据，发送数据给视图View展示

视图和控制器是表现层， 模型是业务层和数据访问层（持久层，dao层）。

**流程：** 

![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\b91cac07abf34fc2a9e8b09390b456cd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**控制器**（serlvlet）用来接收浏览器发送过来的请求，控制器调用模型（JavaBean）来获取数据，比如从数据库查询数据；控制器获取到数据后再交由视图（JSP）进行数据展示。

**MVC 好处：**

- 职责单一，互不影响。每个角色做它自己的事，各司其职。
- 有利于分工协作。
- 有利于组件重用

### 5.7.2 三层架构

三层架构是将我们的项目分成了三个层面，分别是 `表现层`、`业务逻辑层`、`数据访问层`。![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\7e7379bdb16945ce8c3ab54379382562.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **数据访问层**（也叫**持久层**，dao层）**：**对数据库的CRUD基本操作
- **业务逻辑层（业务层）：**对业务逻辑进行封装，组合数据访问层层中基本功能，形成复杂的业务逻辑功能。例如 `注册业务功能` ，我们会先调用 `数据访问层` 的 `selectByName()` 方法判断该用户名是否存在，如果不存在再调用 `数据访问层` 的 `insert()` 方法进行数据的添加操作
- **表现层：**接收请求，封装数据，调用业务逻辑层，响应数据

而整个流程是，**浏览器**发送请求，**表现层**的Servlet接收请求并调用**业务逻辑层**的方法进行业务逻辑处理，而业务逻辑层方法调用数据访问层方法进行数据的操作，依次返回到serlvet，然后servlet将数据交由 JSP 进行展示。

三层架构的每一层都有特有的**包名称：**

- 表现层： `com.itheima.controller` 或者 `com.itheima.web`
- 业务逻辑层：`com.itheima.service`
- 数据访问层：`com.itheima.dao` 或者 `com.itheima.mapper`

后期我们还会学习一些框架，不同的框架是对不同层进行封装的![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\9c868393cf4c43f68a00b338e36627ea.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 5.7.3 MVC和三层架构

 MVC 和 三层架构有什么**区别和联系**？

通过控制器连接，控制器获取并处理请求，调用模型（访问数据库，处理业务）来获取数据，发送数据给视图展示![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\237ddb80e1fd41a4b72890d21cb94a91.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



如上图上半部分是 MVC 模式，上图下半部分是三层架构。

`MVC 模式` 中的 C（控制器）和 V（视图）就是 `三层架构` 中的表现层，而 `MVC 模式` 中的 M（模型）就是 `三层架构` 中的 业务逻辑层 和 数据访问层。

可以将 `MVC 模式` 理解成是一个大的概念，而 `三层架构` 是对 `MVC 模式` 实现架构的思想。 那么我们以后按照要求将不同层的代码写在不同的包下，每一层里功能职责做到单一，将来如果将表现层的技术换掉，而业务逻辑层和数据访问层的代码不需要发生变化。

## 5.8 品牌数据增删改查案例

### 5.8.1 **需求：完成品牌数据的增删改查操作**

```html
    排序：<input name="ordered" value="${brand.ordered}"><br>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**需求：完成品牌数据的增删改查操作**![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\b6c73db213414f6096145081d72e49ce.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



这个功能我们之前一直在做，而这个案例是将今天学习的所有的内容（包含 MVC模式 和 三层架构）进行应用，并将整个流程贯穿起来。

### 5.8.2 主要坑点

1.input标签的value里不能有空格，特别是要String转Integer的。

```html
    排序：<input name="ordered" value="${brand.ordered}"><br>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 2.添加、修改数据别忘了在服务层提交事务。

```
sqlSession.commit();
```

3.Servlet使用post方式别忘了设置编码

```java
 request.setCharacterEncoding("utf-8");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

4.请求转发路径没有虚拟目录（项目名） ，目前学到的路径只有它没有虚拟目录

```java
request.getRequestDispatcher("/brand.jsp").forward(request,response);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 5.8.3 环境准备

环境准备工作，我们分以下步骤实现：

- 1.创建新的模块 brand_demo，引入坐标
- 2.创建三层架构的包结构
- 3.数据库表 tb_brand
- 4.实体类 Brand
- 5.MyBatis 基础环境
  - Mybatis-config.xml
  - BrandMapper.xml
  - BrandMapper接口

**1.创建新的模块 brand_demo，引入坐标**

创建新的模块 brand_demo，引入坐标。我们只要分析出要用到哪儿些技术，那么需要哪儿些坐标也就明确了

- 需要操作数据库。**mysql**的驱动包
- 要使用mybatis框架。**mybaits**的依赖包
- web项目需要用到servlet和jsp。**servlet**和**jsp**的依赖包
- 需要使用 jstl 进行数据展示。**jstl**的依赖包

`pom.xml` 内容如下：

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.example</groupId>
    <artifactId>brand-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.5</version>
        </dependency>

        <!--mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.34</version>
        </dependency>

        <!--servlet-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>

        <!--jsp-->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
            <scope>provided</scope>
        </dependency>

        <!--jstl-->
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
            </plugin>
        </plugins>
    </build>
</project>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2.创建三层架构的包结构**

创建不同的包结构，用来存储不同的类。包结构如下![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\3a7ed5813d15456ba389fc18f2089643.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 mapper下BrandMapper.java接口，pojo下Brand.java实体类，service下BrandService.java业务类，util下SqlSessionFactoryUtils.java工具类，web下SelectAllServlet.java、AddServlet.java等Servlet类

**3.数据库表 tb_brand**

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

**4.创建实体类**

在 `pojo` 包下创建名为 `Brand` 的类。

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


    public Brand() {
    }

    public Brand(Integer id, String brandName, String companyName, String description) {
        this.id = id;
        this.brandName = brandName;
        this.companyName = companyName;
        this.description = description;
    }

    public Brand(Integer id, String brandName, String companyName, Integer ordered, String description, Integer status) {
        this.id = id;
        this.brandName = brandName;
        this.companyName = companyName;
        this.ordered = ordered;
        this.description = description;
        this.status = status;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getBrandName() {
        return brandName;
    }

    public void setBrandName(String brandName) {
        this.brandName = brandName;
    }

    public String getCompanyName() {
        return companyName;
    }

    public void setCompanyName(String companyName) {
        this.companyName = companyName;
    }

    public Integer getOrdered() {
        return ordered;
    }

    public void setOrdered(Integer ordered) {
        this.ordered = ordered;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public Integer getStatus() {
        return status;
    }

    public void setStatus(Integer status) {
        this.status = status;
    }

    @Override
    public String toString() {
        return "Brand{" +
                "id=" + id +
                ", brandName='" + brandName + '\'' +
                ", companyName='" + companyName + '\'' +
                ", ordered=" + ordered +
                ", description='" + description + '\'' +
                ", status=" + status +
                '}';
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**5.准备mybatis环境**

定义核心配置文件 `Mybatis-config.xml` ，并将该文件放置在 `resources` 下

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--起别名，映射配置文件resultType后就可省略包名-->
    <typeAliases>
        <package name="package1.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///db1?useSSL=false&amp;useServerPrepStmts=true"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <!--扫描mapper-->
        <package name="package1.mapper"/>
    </mappers>
</configuration>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在 `resources` 下创建放置映射配置文件的目录结构 `com/itheima/mapper`，并在该目录下创建映射配置文件 `BrandMapper.xml`

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.BrandMapper">
    
</mapper>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 5.8.4 查询所有![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\d1e598e524294f01ac67d0fb0ad8f2c2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



当我们点击 `index.html` 页面中的 `查询所有` 这个超链接时，就能查询到上图右半部分的数据。

对于上述的功能，点击 `查询所有` 超链接是需要先请后端的 `servlet` ，由 `servlet` 跳转到对应的页面进行数据的动态展示。而整个流程如下图：![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\6b77e330cf454dcfa5192a57b6be8ae5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 之前代码是直接用web层直接调用数据访问层方法，加上业务层是为了提高代码复用性。如果用Servlet实现包含多个Dao层方法的业务，其他Servlet想使用这个业务就得重新写，不如直接调用业务层方法方便。

**编写BrandMapper**

在 `mapper` 包下创建创建 `BrandMapper` 接口，在接口中定义 `selectAll()` 方法

```java
/**
  * 查询所有
  * @return
  */
//sql语句简单，直接注解开发，替代配置文件开发
@Select("select * from tb_brand")
List<Brand> selectAll();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写工具类**

在 `com.itheima` 包下创建 `utils` 包，并在该包下创建名为 `SqlSessionFactoryUtils` 工具类

```java
package package1.util;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

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

**编写BrandService**

在 `service` 包下创建 `BrandService` 类

```java
public class BrandService {
    SqlSessionFactory factory = SqlSessionFactoryUtils.getSqlSessionFactory();

    /**
     * 查询所有
     * @return
     */
    public List<Brand> selectAll(){
        //调用BrandMapper.selectAll()

        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

        //4. 调用方法
        List<Brand> brands = mapper.selectAll();
        //一定别忘了关闭会话
        sqlSession.close();

        return brands;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写Servlet**

在 `web` 包下创建名为 `SelectAllServlet` 的 `servlet`，该 `servlet` 的逻辑如下：

- 调用 `BrandService` 的 `selectAll()` 方法进行业务逻辑处理，并接收返回的结果
- 将上一步返回的结果存储到 `request` 域对象中
- 跳转到 `brand.jsp` 页面进行数据的展示

具体的代码如下：

```java
@WebServlet("/selectAllServlet")
public class SelectAllServlet extends HttpServlet {
    //在这里创建服务对象
    private  BrandService service = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 调用BrandService完成查询
        List<Brand> brands = service.selectAll();
        //2. 存入request域中
        request.setAttribute("brands",brands);
        //3. 转发到brand.jsp
        request.getRequestDispatcher("/brand.jsp").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写brand.jsp页面**

将资料 `资料\2. 品牌增删改查案例\静态页面` 下的 `brand.html` 页面拷贝到项目的 `webapp` 目录下，并将该页面改成 `brand.jsp` 页面，而 `brand.jsp` 页面在表格中使用 `JSTL` 和 `EL表达式` 从request域对象中获取名为 `brands` 的集合数据并展示出来。页面内容如下：

```Delphi
<%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<hr>
<table border="1" cellspacing="0" width="80%">
    <tr>
        <th>序号</th>
        <th>品牌名称</th>
        <th>企业名称</th>
        <th>排序</th>
        <th>品牌介绍</th>
        <th>状态</th>
        <th>操作</th>
    </tr>

    <c:forEach items="${brands}" var="brand" varStatus="status">
        <tr align="center">
                <%--<td>${brand.id}</td>--%>
            <td>${status.count}</td>
            <td>${brand.brandName}</td>
            <td>${brand.companyName}</td>
            <td>${brand.ordered}</td>
            <td>${brand.description}</td>
            <c:if test="${brand.status == 1}">
                <td>启用</td>
            </c:if>
            <c:if test="${brand.status != 1}">
                <td>禁用</td>
            </c:if>
            <td><a href="/brand-demo/selectByIdServlet?id=${brand.id}">修改</a> <a href="#">删除</a></td>
        </tr>
    </c:forEach>
</table>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**测试**

启动服务器，并在浏览器输入 `http://localhost:8080/brand-demo/index.html`，看到如下 `查询所有` 的超链接，点击该链接就可以查询出所有的品牌数据![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\8436f8c9c5ff4489bb219243ec69f4c4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



为什么出现这个问题呢？是因为查询到的字段名和实体类对象的属性名没有一一对应。相比看到这大家一定会解决了，就是在映射配置文件中使用 `resultMap` 标签定义映射关系。映射配置文件内容如下：

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.BrandMapper">

    <resultMap id="brandResultMap" type="brand">
        <result column="brand_name" property="brandName"></result>
        <result column="company_name" property="companyName"></result>
    </resultMap>
</mapper>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

并且在 `BrandMapper` 接口中的 `selectAll()` 上使用 `@ResuleMap` 注解指定使用该映射

```java
/**
  * 查询所有
  * @return
  */
@Select("select * from tb_brand")
@ResultMap("brandResultMap")
List<Brand> selectAll();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

重启服务器，再次访问就能看到我们想要的数据了![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\b48e627266d64ed5b2b258a9c539ae38.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 5.8.5 添加![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\08cc402da419464dae02b349e0395eec.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



上图是做 添加 功能流程。点击 `新增` 按钮后，会先跳转到 `addBrand.jsp` 新增页面，在该页面输入要添加的数据，输入完毕后点击 `提交` 按钮，需要将数据提交到后端，而后端进行数据添加操作，并重新将所有的数据查询出来。整个流程如下：![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\a6282ab7202e4b57a0a5474c9f8f243a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



接下来我们根据流程来实现功能：

**编写BrandMapper方法**

在 `BrandMapper` 接口，在接口中定义 `add(Brand brand)` 方法

```java
@Insert("insert into tb_brand values(null,#{brandName},#{companyName},#{ordered},#{description},#{status})")
void add(Brand brand);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写BrandService方法**

在 `BrandService` 类中定义添加品牌数据方法 `add(Brand brand)`

```java
 	/**
     * 添加
     * @param brand
     */
    public void add(Brand brand){

        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

        //4. 调用方法
        mapper.add(brand);

        //提交事务，一定别忘了
        sqlSession.commit();
        //释放资源
        sqlSession.close();
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**改进brand.jsp页面**

我们需要在该页面表格的上面添加 `新增` 按钮

```html
<input type="button" value="新增" id="add"><br>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

并给该按钮绑定单击事件，当点击了该按钮需要跳转到 `brand.jsp` 添加品牌数据的页面

```html
<script>
    document.getElementById("add").onclick = function (){
        location.href = "/brand-demo/addBrand.jsp";
    }
</script>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**该 `script` 标签建议放在 `body` 结束标签前面。

**编写addBrand.jsp页面**

 `addBrand.jsp` 动态页面

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>添加品牌</title>
</head>
<body>
<h3>添加品牌</h3>
<form action="/brand-demo/addServlet" method="post">
    品牌名称：<input name="brandName"><br>
    企业名称：<input name="companyName"><br>
    排序：<input name="ordered"><br>
    描述信息：<textarea rows="5" cols="20" name="description"></textarea><br>
    状态：
    <input type="radio" name="status" value="0">禁用
    <input type="radio" name="status" value="1">启用<br>

    <input type="submit" value="提交">
</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写servlet**

在 `web` 包下创建 `AddServlet` 的 `servlet`，该 `servlet` 的逻辑如下:

- 设置处理post请求乱码的字符集
- 接收客户端提交的数据
- 将接收到的数据封装到 `Brand` 对象中
- 调用 `BrandService` 的`add()` 方法进行添加的业务逻辑处理
- 跳转到 `selectAllServlet` 资源重新查询数据

具体的代码如下：

```java
@WebServlet("/addServlet")
public class AddServlet extends HttpServlet {
    private BrandService service = new BrandService();


    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //处理POST请求的乱码问题，Tomcat8及以后版本默认utf-8
        request.setCharacterEncoding("utf-8");

        //1. 接收表单提交的数据，封装为一个Brand对象
        String brandName = request.getParameter("brandName");
        String companyName = request.getParameter("companyName");
        String ordered = request.getParameter("ordered");
        String description = request.getParameter("description");
        String status = request.getParameter("status");

        //封装为一个Brand对象
        Brand brand = new Brand();
        brand.setBrandName(brandName);
        brand.setCompanyName(companyName);
        brand.setOrdered(Integer.parseInt(ordered));
        brand.setDescription(description);
        brand.setStatus(Integer.parseInt(status));

        //2. 调用service 完成添加
        service.add(brand);

        //3. 转发到查询所有Servlet
        request.getRequestDispatcher("/selectAllServlet").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**测试**

点击 `brand.jsp` 页面的 `新增` 按钮，会跳转到 `addBrand.jsp`页面![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\8b7acab966bc4367b1b8a00dd5f5dca7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



点击 `提交` 按钮，就能看到如下页面，里面就包含我们刚添加的数据![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\40a141c254bc4b358ac6773e25201879.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 5.8.6 修改（回显数据）![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\12648ef09ec44bfcaa08309854fca30c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



点击每条数据后面的 `编辑` 按钮会跳转到修改页面，如下图：![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\a2489e95c42f41dbb2c6aae5e6ab6e31.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



在该修改页面我们可以看到将 `编辑` 按钮所在行的数据 **回显** 到表单，然后需要修改那个数据在表单中进行修改，然后点击 `提交` 的按钮将数据提交到后端，后端再将数据存储到数据库中。

从上面的例子我们知道 `修改` 功能需要从两方面进行实现，数据回显和修改操作。

**回显数据**![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\ef39744f09694924a2e11af86b86c739.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



上图就是回显数据的效果。要实现这个效果，那当点击 `修改` 按钮时不能直接跳转到 `update.jsp` 页面，而是需要先带着当前行数据的 `id` 请求后端程序，后端程序根据 `id` 查询数据，将数据存储到域对象中跳转到 `update.jsp` 页面进行数据展示。整体流程如下![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\d5e8198fe1554e8ab3606a9e72bbe720.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**编写BrandMapper方法**

在 `BrandMapper` 接口，在接口中定义 `selectById(int id)` 方法

```java
	/**
     * 根据id查询
     * @param id
     * @return
     */
    @Select("select * from tb_brand where id = #{id}")
    @ResultMap("brandResultMap")
    Brand selectById(int id);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写BrandService方法**

在 `BrandService` 类中定义根据id查询数据方法 `selectById(int id)`

```java
    /**
     * 根据id查询
     * @return
     */
    public Brand selectById(int id){
        //调用BrandMapper.selectAll()
        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);
        //4. 调用方法
        Brand brand = mapper.selectById(id);
        sqlSession.close();
        return brand;
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写servlet**

在 `web` 包下创建 `SelectByIdServlet` 的 `servlet`，该 `servlet` 的逻辑如下:

- 获取请求数据 `id`
- 调用 `BrandService` 的 `selectById()` 方法进行数据查询的业务逻辑
- 将查询到的数据存储到 request 域对象中
- 跳转到 `update.jsp` 页面进行数据真实

具体代码如下：

```java
@WebServlet("/selectByIdServlet")
public class SelectByIdServlet extends HttpServlet {
    private  BrandService service = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接收id
        String id = request.getParameter("id");
        //2. 调用service查询
        Brand brand = service.selectById(Integer.parseInt(id));
        //3. 存储到request中
        request.setAttribute("brand",brand);
        //4. 转发到update.jsp
        request.getRequestDispatcher("/update.jsp").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写update.jsp页面**

拷贝 `addBrand.jsp` 页面，改名为 `update.jsp` 并做出以下修改：

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>修改品牌</title>
</head>
<body>
<h3>修改品牌</h3>
<form action="/brand-demo/updateServlet" method="post">

    品牌名称：<input name="brandName" value="${brand.brandName}"><br>
    企业名称：<input name="companyName" value="${brand.companyName}"><br>
    排序：<input name="ordered" value="${brand.ordered}"><br>
    描述信息：<textarea rows="5" cols="20" name="description">${brand.description} </textarea><br>
    状态：
    <c:if test="${brand.status == 0}">
        <input type="radio" name="status" value="0" checked>禁用
        <input type="radio" name="status" value="1">启用<br>
    </c:if>

    <c:if test="${brand.status == 1}">
        <input type="radio" name="status" value="0" >禁用
        <input type="radio" name="status" value="1" checked>启用<br>
    </c:if>

    <input type="submit" value="提交">
</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**修改数据**

做完回显数据后，接下来我们要做修改数据了，而下图是修改数据的效果：![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\373a607d12da44fba84a9a791f0b093c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



在修改页面进行数据修改，点击 `提交` 按钮，会将数据提交到后端程序，后端程序会对表中的数据进行修改操作，然后重新进行数据的查询操作。整体流程如下：![img](JavaWeb基础6——Request,Response,JSP&MVC.assets\3951bcee73ca4b1e8cbb274ed96b1827.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**编写BrandMapper方法**

在 `BrandMapper` 接口，在接口中定义 `update(Brand brand)` 方法

```html
/**
  * 修改
  * @param brand
  */
@Update("update tb_brand set brand_name = #{brandName},company_name = #{companyName},ordered = #{ordered},description = #{description},status = #{status} where id = #{id}")
void update(Brand brand);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写BrandService方法**

在 `BrandService` 类中定义根据id查询数据方法 `update(Brand brand)`

```java
	/**
     * 修改
     * @param brand
     */
    public void update(Brand brand){
        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);
        //4. 调用方法
        mapper.update(brand);
        //提交事务
        sqlSession.commit();
        //释放资源
        sqlSession.close();
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**编写servlet**

在 `web` 包下创建 `AddServlet` 的 `servlet`，该 `servlet` 的逻辑如下:

- 设置处理post请求乱码的字符集
- 接收客户端提交的数据
- 将接收到的数据封装到 `Brand` 对象中
- 调用 `BrandService` 的`update()` 方法进行添加的业务逻辑处理
- 跳转到 `selectAllServlet` 资源重新查询数据

具体的代码如下：

```java
@WebServlet("/updateServlet")
public class UpdateServlet extends HttpServlet {
    private BrandService service = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //处理POST请求的乱码问题
        request.setCharacterEncoding("utf-8");
        //1. 接收表单提交的数据，封装为一个Brand对象
        String id = request.getParameter("id");
        String brandName = request.getParameter("brandName");
        String companyName = request.getParameter("companyName");
        String ordered = request.getParameter("ordered");
        String description = request.getParameter("description");
        String status = request.getParameter("status");

        //封装为一个Brand对象
        Brand brand = new Brand();
        brand.setId(Integer.parseInt(id));
        brand.setBrandName(brandName);
        brand.setCompanyName(companyName);
        brand.setOrdered(Integer.parseInt(ordered));
        brand.setDescription(description);
        brand.setStatus(Integer.parseInt(status));

        //2. 调用service 完成修改
        service.update(brand);

        //3. 转发到查询所有Servlet
        request.getRequestDispatcher("/selectAllServlet").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**存在问题：update.jsp 页面提交数据时是没有携带主键数据的，而后台修改数据需要根据主键进行修改。**

针对这个问题，我们不希望页面将主键id展示给用户看，但是又希望在提交数据时能将主键id提交到后端。此时我们就想到了在学习 HTML 时学习的隐藏域，在 `update.jsp` 页面的表单中添加如下代码：

```html
<%--隐藏域，提交id--%>
<input type="hidden" name="id" value="${brand.id}">
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

`update.jsp` 页面的最终代码如下：

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>修改品牌</title>
</head>
<body>
<h3>修改品牌</h3>
<form action="/brand-demo/updateServlet" method="post">

    <%--隐藏域，提交id--%>
    <input type="hidden" name="id" value="${brand.id}">

    品牌名称：<input name="brandName" value="${brand.brandName}"><br>
    企业名称：<input name="companyName" value="${brand.companyName}"><br>
    排序：<input name="ordered" value="${brand.ordered}"><br>
    描述信息：<textarea rows="5" cols="20" name="description">${brand.description} </textarea><br>
    状态：
    <c:if test="${brand.status == 0}">
        <input type="radio" name="status" value="0" checked>禁用
        <input type="radio" name="status" value="1">启用<br>
    </c:if>

    <c:if test="${brand.status == 1}">
        <input type="radio" name="status" value="0" >禁用
        <input type="radio" name="status" value="1" checked>启用<br>
    </c:if>
    <input type="submit" value="提交">
</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)