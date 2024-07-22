>  **导航：**
>
> [【Java笔记+踩坑汇总】JavaSE+JavaWeb+SSM+SpringBoot+瑞吉外卖+SpringCloud/SpringCloudAlibaba+黑马旅游+谷粒商城](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})

[TOC]



# 一、Web概述

(1)**Request**是从客户端向服务端发出的请求对象，

(2)**Response**是从服务端响应给客户端的结果对象，

(3)**JSP**是动态网页技术,

(4)**会话技术**(Cookie、Session) 是用来存储客户端和服务端交互所产生的数据，

(5)**过滤器**Filter 是用来拦截客户端的请求,

(6)**监听器**Listener 是用来监听特定事件,

(7)Ajax、Vue、ElementUI都是属于前端技术

## 1.1 Web和JavaWeb的概念

**Web**是全球广域网，也称为万维网(www)，能够通过浏览器访问的网站。

在我们日常的生活中，经常会使用浏览器去访问`百度`、`京东`、`传智官网`等这些网站，这些网站统称为Web网站。

**JavaWeb**就是用Java技术来解决相关web互联网领域的技术栈。

## 1.2 JavaWeb技术栈

### **1.2.1 B/S 架构**

**B/S 架构：**Browser/Server，浏览器/服务器 架构模式，它的特点是，客户端只需要浏览器，应用程序的逻辑和数据都存储在服务器端。

浏览器只需要请求服务器，获取Web资源，服务器把Web资源发送给浏览器即可。

大家可以通过下面这张图来回想下我们平常的上网过程:

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\32229065e44b4f359e60e3d6b020a093.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**B/S架构的好处:**

易于维护升级：服务器端升级后，客户端无需任何部署就可以使用到新的版本。

作为后台开发工程师的我们将来主要关注的是服务端的开发和维护工作。在服务端将来会放很多资源,包括...

### **1.2.2** 静态资源

**静态资源：**可以理解为前端的固定页面，这里面包含HTML、CSS、JS、图片等等，不需要查数据库也不需要程序处理，直接就能够显示的页面，如果想修改内容则必须修改页面，但是访问效率相当高。

由于做出来的这些内容都是静态的，这就会导致所有的人看到的内容将是一模一样。

**动态内容：**

在日常上网的过程中，我们除了看到这些好看的页面以外，还会碰到很多**动态内容**，比如我们常见的百度登录效果:

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\e79a0c35a7504f7aba65f52d0532d1eb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



`张三`登录以后在网页的右上角看到的是 `张三`，而`李四`登录以后看到的则是`李四`。所以不同的用户访问相同的资源看到的内容大多数是不一样的，要想实现这样的效果，光靠静态资源是无法实现的。

### **1.2.3** 动态资源

**动态资源：**需要程序处理或者从数据库中读数据，能够根据不同的条件在页面显示不同的数据，内容更新不需要修改页面但是访问速度不及静态页面。

**内容和作用：**动态资源主要包含**Servlet、JSP**等，主要用来**负责逻辑处理**。

动态资源处理完逻辑后会把得到的结果交给静态资源来进行展示，动态资源和静态资源要结合一起使用。

### **1.2.4** 数据库

数据库主要**负责存储数据**。

整个Web的访问过程就如下图所示:

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\a0e095e64d584f8ba57552eb6f815ddf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **请求：**

(1)浏览器发送一个请求到服务端，去请求所需要的相关资源;

(2)资源分为动态资源和静态资源,动态资源可以是使用Java代码按照Servlet和JSP的规范编写的内容;

(3)在Java代码可以进行业务处理也可以从数据库中读取数据;

**响应：**

(1)拿到数据后，把数据交给HTML页面进行展示,再结合CSS和JavaScript使展示效果更好;

(2)服务端将静态资源响应给浏览器;

(3)浏览器将这些资源进行解析;

(4)解析后将效果展示在浏览器，用户就可以看到最终的结果。

### **1.2.5** HTTP协议

- **HTTP协议:**主要定义通信规则
- 浏览器发送请求给服务器，服务器响应数据给浏览器，这整个过程都需要遵守一定的**规则**，之前大家学习过TCP、UDP，这些都属于规则，这里我们需要使用的是HTTP协议，这也是一种规则。

### **1.2.6** Web服务器

- **Web服务器:**负责解析 HTTP 协议，解析请求数据，并发送响应数据
- 浏览器按照HTTP协议发送请求和数据，后台就需要一个Web服务器软件来根据HTTP协议解析请求和数据，然后把处理结果再按照HTTP协议发送给浏览器
- Web服务器软件有很多，目前最为常用的是**Tomcat服务器**

到这为止，关于JavaWeb中用到的技术栈我们就介绍完了，这里面就只有HTTP协议、Servlet、JSP以及Tomcat这些知识是没有学习过的，所以整个Web核心主要就是来学习这些技术。

# 二、HTTP超文本传输协议

## 2.1 概述

HyperText Transfer Protocol，超文本传输协议，规定了浏览器和服务器之间**数据传输的规**则。

- **数据传输的规则**指的是请求数据和响应数据需要按照指定的格式进行传输。

如果想知道具体的格式，可以打开浏览器，点击`F12`打开开发者工具，点击`Network`来查看某一次请求的请求数据和响应数据具体的格式内容，



> **注意:**在浏览器中如果看不到上述内容，需要清除浏览器的浏览数据。chrome浏览器可以使用ctrl+shift+Del进行清除。

所以学习HTTP主要就是学习请求和响应数据的具体格式内容。

**HTTP协议特点**

HTTP协议有它自己的一些特点，分别是:

- **基于TCP协议**: 面向连接，安全

  TCP是一种面向连接的(建立连接之前是需要经过三次握手)、可靠的、基于字节流的传输层通信协议，在数据传输方面更安全。

- **基于请求-响应模型的:**一次请求对应一次响应

  请求和响应是一一对应关系

- HTTP协议是**无状态协议**:对于事物处理没有记忆能力。每次请求-响应都是独立的

  **无状态：**指的是客户端发送HTTP请求给服务端之后，服务端根据请求响应数据，响应完后，**不会记录任何信息**。这种特性有优点也有缺点，

  - **缺点:**多次请求间不能共享数据，使用**`会话技术(Cookie、Session)`**来解决这个问题
  - **优点:**速度快

  > 请求之间无法共享数据会引发的问题，如:
  >
  > - 某东购物，`加入购物车`和`去购物车结算`是两次请求，
  > - HTTP协议的无状态特性，加入购物车请求响应结束后，并未记录加入购物车是何商品
  > - 发起去购物车结算的请求后，因为**无法获取哪些商品加入了购物车**，会导致此次请求无法正确展示数据
  >
  > 具体使用的时候，我们发现某东是可以正常展示数据的，原因是Java早已考虑到这个问题，并提出了使用**`会话技术(Cookie、Session)`来解决这个问题**。具体如何来做，我们后面会详细讲到。

## 2.2 请求数据格式

### 2.2.1 请求行、头、体

请求数据总共分为三部分内容，分别是请求行、请求头、请求体

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\fb7a660f97a54ea981f802a64fd3551b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





- **请求行:** HTTP请求中的第一行数据，请求行包含三块内容，分别是 GET[请求方式] /[请求URL路径] HTTP/1.1[HTTP协议及版本]

  请求方式有七种,最常用的是GET和POST

- **请求头:** 第二行开始，格式为key: value形式

  请求头中会包含若干个属性，常见的HTTP请求头有:

  ```bash
  Host: 表示请求的主机名
  User-Agent: 浏览器版本,译为用户代理。例如Chrome浏览器的标识类似Mozilla/5.0 ...Chrome/79，IE浏览器的标识类似Mozilla/5.0 (Windows NT ...)like Gecko；
  Accept：表示浏览器能接收的资源类型，如text/*，image/*或者*/*表示所有；
  Accept-Language：表示浏览器偏好的语言，服务器可以据此返回不同语言的网页；
  Accept-Encoding：表示浏览器可以支持的压缩类型，例如gzip, deflate等。
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  **这些数据有什么用处?**

  **举例说明:**服务端可以根据请求头中的内容来获取客户端的相关信息，有了这些信息服务端就可以处理不同的业务需求，比如:

  - 不同浏览器解析HTML和CSS标签的结果会有不一致，所以就会导致相同的代码在不同的浏览器会出现不同的效果
  - 服务端根据客户端请求头中的数据获取到客户端的浏览器类型，就可以**根据不同的浏览器设置不同的代码来达到一致的效果**
  - 这就是我们常说的**浏览器兼容问题**

- **请求体:** POST请求的最后一部分，存储请求参数

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\329f5ec9b1fb4c5cb85f16b052e87efe.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



如上图红线框的内容就是请求体的内容，请求体和请求头之间是有一个空行隔开。此时浏览器发送的是POST请求，为什么不能使用GET呢?这时就需要回顾**GET和POST两个请求之间的区别**了:

- **GET请求请求参数在请求行中，没有请求体，POST请求请求参数在请求体中**
- **GET请求请求参数大小有限制，POST没有**



示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="#" method="get">
    <input type="input" name="username">
    <input type="submit">
</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\51744169e3784bdd924ce3aa7471695f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.2 get和post区别

POST和GET本质是一样的，都是HTTP请求的基本方法。

- **get：**
  - **默认值**。如果不设置method属性则默认就是该值
  - 请求参数会拼接在URL后边，暴露不安全，在浏览器刷新或者回退的时候是无害的，可以保存在书签、历史记录
  - 编码：url编码
  - 长度：url的长度有限制 4KB
- **post：**
  - 浏览器会将数据放到http请求消息体中，隐藏在请求体安全。在浏览器刷新或者回退的时候数据会被重新提交，不能保存在书签、历史记录
  - 编码：支持多种编码方式
  - 长度：请求参数无大小限制的





**GET 和POST在请求的时候**
 GET 是将数据中的header 和 data 一起发送给服务端，返回200code
 POST 是先将hearder发给服务器返回100continue，再发送data给到服务器，返回200
 GET 就发送了一个TCP数据包给服务器而POST发送了两次TCP数据包给服务器
 GET和POST是已经有定义好的说明的，最好不要混用。

## 2.3 响应数据格式

**格式介绍**

响应数据总共分为三部分内容，分别是响应行、响应头、响应体

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\f0b9125f17774d668a4ac609684d7192.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





- **响应行**：响应数据的第一行。响应行包含三块内容，分别是 HTTP/1.1[HTTP协议及版本] 200[响应状态码] ok[状态码的描述]

- **响应头**：第二行开始，格式为key：value形式

  响应头中会包含若干个属性，常见的HTTP响应头有:

  ```
  Content-Type：表示该响应内容的类型，例如text/html，image/jpeg；
  Content-Length：表示该响应内容的长度（字节数）；
  Content-Encoding：表示该响应压缩算法，例如gzip；
  Cache-Control：指示客户端应如何缓存，例如max-age=300表示可以最多缓存300秒
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **响应体**： 最后一部分。存放响应数据

  上图中<html>...</html>这部分内容就是响应体，它和响应头之间有一个空行隔开。

## **2.4 响应状态码**

关于响应状态码，我们先主要认识三个状态码，其余的等后期用到了再去掌握:

- 200 ok 客户端请求成功
- 404 Not Found 请求资源不存在
- 500 Internal Server Error 服务端发生不可预期的错误

### 2.4.1 状态码分类



| 状态码分类 | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| 1xx        | **响应中**——临时状态码，表示请求已经接受，告诉客户端应该继续请求或者如果它已经完成则忽略它 |
| 2xx        | **成功**——表示请求已经被成功接收，处理已完成                 |
| 3xx        | **重定向**——重定向到其它地方：它让客户端再发起一个请求以完成整个处理。 |
| 4xx        | **客户端错误**——处理发生错误，责任在客户端，如：408客户端的请求一个不存在的资源，客户端未被授权，禁止访问等 |
| 5xx        | **服务器端错误**——处理发生错误，责任在服务端，如：服务端抛出异常，路由出错，HTTP版本不支持等 |

状态码大全：[状态 | Status - HTTP 中文开发手册 - 开发者手册 - 腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/chapter/13553)



### 2.4.2 常见的响应状态码

| 状态码 | 英文描述                              | 解释                                                         |
| ------ | ------------------------------------- | ------------------------------------------------------------ |
| 200    | **`OK`**                              | 客户端请求成功，即**处理成功**，这是我们最想看到的状态码     |
| 302    | **`Found`**                           | 指示所请求的资源已移动到由`Location`响应头给定的 URL，浏览器会自动重新访问到这个页面 |
| 304    | **`Not Modified`**                    | 告诉客户端，你请求的资源至上次取得后，服务端并未更改，你直接用你本地缓存吧。隐式重定向 |
| 400    | **`Bad Request`**                     | 客户端请求有**语法错误**，不能被服务器所理解                 |
| 403    | **`Forbidden`**                       | 服务器收到请求，但是**拒绝提供服务**，比如：没有权限访问相关资源 |
| 404    | **`Not Found`**                       | **请求资源不存在**，一般是URL输入有误，或者网站资源被删除了  |
| 428    | **`Precondition Required`**           | **服务器要求有条件的请求**，告诉客户端要想访问该资源，必须携带特定的请求头 |
| 429    | **`Too Many Requests`**               | **太多请求**，可以限制客户端请求某个资源的数量，配合 Retry-After(多长时间后可以请求)响应头一起使用 |
| 431    | **`Request Header Fields Too Large`** | **请求头太大**，服务器不愿意处理请求，因为它的头部字段太大。请求可以在减少请求头域的大小后重新提交。 |
| 405    | **`Method Not Allowed`**              | 请求方式有误，比如应该用GET请求方式的资源，用了POST          |
| 500    | **`Internal Server Error`**           | **服务器发生不可预期的错误**。服务器出异常了，赶紧看日志去吧 |
| 503    | **`Service Unavailable`**             | **服务器尚未准备好处理请求**，服务器刚刚启动，还未初始化好   |
| 511    | **`Network Authentication Required`** | **客户端需要进行身份验证才能获得网络访问权限**               |



# 三、Tomcat

## 3.1 简介

**Tomcat是一个Web服务器。**支持Servlet/JSP少量JavaEE规范，也称为Web容器，Servlet容器。

**什么是Web服务器？**

Web服务器是一个应用程序（软件），**对HTTP协议的操作进行封装**，使得程序员不必直接对协议进行操作，让Web开发更加便捷。

**主要作用**：

1.封装HTTP协议操作，简化开发

2.可以将Web项目部署到服务器中，对外提供网上浏览服务



Web服务器是安装在服务器端的一款软件，将来我们把自己写的Web项目部署到Web Tomcat服务器软件中，当Web服务器软件启动后，部署在Web服务器软件中的页面就可以直接通过浏览器来访问了。

**Web服务器软件使用步骤**

- 准备静态资源
- 下载安装Web服务器软件
- 将静态资源部署到Web服务器上
- 启动Web服务器使用浏览器访问对应的资源

对于Web服务器来说，实现的方案有很多，Tomcat只是其中的一种，而除了Tomcat以外，还有很多优秀的Web服务器，比如:

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\64ed10a011c144fcb6a73ff84b4c238a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**Tomcat**

Tomcat的相关概念:

- **Tomcat**是Apache软件基金会一个核心项目，**是一个**开源免费的轻量级**Web服务器**，支持Servlet/JSP少量JavaEE规范。

- 概念中提到了**JavaEE规范**，那什么又是JavaEE规范呢?

  JavaEE: Java Enterprise Edition,Java企业版。指Java企业级开发的技术规范总和。包含13项技术规范:JDBC、JNDI、EJB、RMI、JSP、Servlet、XML、JMS、Java IDL、JTS、JTA、JavaMail、JAF。

- 因为Tomcat支持Servlet/JSP规范，所以**Tomcat也被称为Web容器、Servlet容器**。Servlet需要依赖Tomcat才能运行。

- Tomcat的官网: [Apache Tomcat® - Welcome!](https://tomcat.apache.org/) 从官网上可以下载对应的版本进行使用。

**Tomcat的LOGO**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\851d966fb21643198a8a1c112417f8f3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 3.2 基本使用

### 3.2.1 下载安装

下载：[Apache Tomcat® - Which Version Do I Want?](https://tomcat.apache.org/whichversion.html)

这里选择8版本：

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\eee7f4226e354be2aa6416b9648c1402.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

下载解压到非中文空格目录下。 

**目录结构**，每个目录中包含的内容需要认识下,

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\82dc6fb263674547ab1fc39a26d57f9b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





bin:目录下有两类文件，一种是以`.bat`结尾的，是Windows系统的可执行文件，一种是以`.sh`结尾的，是Linux系统的可执行文件。

webapps:就是以后项目部署的目录

到此，Tomcat的安装就已经完成。

### 3.2.2 启动、关闭、配置

**启动** 

双击: bin\startup.bat

启动后，通过浏览器访问 `http://localhost:8080`能看到Apache Tomcat自带项目的内容就说明Tomcat已经启动成功。

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\15c970d8ba6c4aa589fbf99317e1f35a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**注意:** 启动的过程中，控制台有中文乱码，需要修改conf/logging.prooperties

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\f252b1bae0e944a88581b76345389461.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\7f81144bf10c46a58f96ee7726073809.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**关闭**

关闭有三种方式

- 直接x掉运行窗口:强制关闭[不建议]
- bin\shutdown.bat：正常关闭
- ctrl+c： 正常关闭

**修改端口**

- Tomcat默认的端口是8080，要想修改Tomcat启动的端口号，需要修改 conf/server.xml

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\bf7d561712bd4259996bf73ff76a2f4b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





> **注:** HTTP协议默认端口号为80，如果将Tomcat端口号改为80，则将来访问Tomcat时，直接输入localhost不加端口即可访问项目。

**启动时可能出现的错误**

- Tomcat的端口号取值范围是0-65535之间任意未被占用的端口，如果设置的端口号被占用，启动的时候就会包如下的错误![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\258667fc3a204604a51a007c3bfd4d71.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

  

- Tomcat启动的时候，启动窗口一闪而过: 需要检查JAVA_HOME环境变量是否正确配置

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\2f4d5029f70c4b32a707f4fef3c4cb6e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.2.3 部署

将项目文件夹或war压缩包放置到webapps目录下，即部署完成。

## 3.3 Maven创建Web项目

使用Maven工具能更加简单快捷的把Web项目给创建出来。

### **3.3.1 Web项目结构**

Web项目的结构分为:开发中的项目和开发完可以部署的Web项目,这两种项目的结构是不一样的，我们一个个来介绍下:

- Maven Web项目结构: 开发中的项目![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\8f636c4684e24b4e86442ed86686633d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 开发完成部署的Web项目![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\57adbcc0e313403a862976a8f13f36e6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

  

  - 开发项目通过执行Maven**打包命令package**,可以获取到部署的Web项目目录
  - 编译后的Java字节码文件和resources的资源文件，会被放到WEB-INF下的classes目录下
  - pom.xml中依赖坐标对应的jar包，会被放入WEB-INF下的lib目录下

### **3.3.2** idea创建Maven Web项目

介绍完Maven Web的项目结构后，接下来使用Maven来创建Web项目，创建方式有两种:使用骨架和不使用骨架。

**方法一：使用骨架（推荐使用方法一）**

> 具体的步骤包含:
>
> 1.创建Maven项目
>
> 2.选择使用Web项目骨架
>
> 3.输入Maven项目坐标创建项目
>
> 4.确认Maven相关的配置信息后，完成项目创建
>
> 5.删除pom.xml中多余内容
>
> 6.补齐Maven Web项目缺失的目录结构

0.每次创建项目前检查一下设置：

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\0a8ca4d7b38b4971b6b61d4d70a37e58.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



1. 创建Maven项目

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\24804d92a0f84b00aa36ad601789d9e4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

2. 选择使用Web项目骨架

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\4bd8b81df92d46d3bcf9b1536492f591.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

3. 输入Maven项目坐标创建项目

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\b4bf60c4a0c9493184f7b571735fbba8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

4. 确认Maven相关的配置信息后，完成项目创建

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\72b6a79a7ff742f9b28f92f8f3caff77.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

5. 删除pom.xml中多余内容，只留下面的这些内容，注意打包方式 jar和war的区别

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\474b40aa97604c95b969067da8b6bf6f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

6. 补齐Maven Web项目缺失的目录结构，默认没有java和resources目录，需要手动完成创建补齐，最终的目录结果如下

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\d96a53e05372450f9009a271ddbf8612.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   



**方法二：不使用骨架**

> 具体的步骤包含:
>
> 1.创建Maven项目
>
> 2.选择不使用Web项目骨架
>
> 3.输入Maven项目坐标创建项目
>
> 4.在pom.xml设置打包方式为war
>
> 5.补齐Maven Web项目缺失webapp的目录结构
>
> 6.补齐Maven Web项目缺失WEB-INF/web.xml的目录结构

1. 创建Maven项目

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\e754a8d175c04dd7b04916056e6bf8e3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

2. 选择不使用Web项目骨架

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\4b53db93ce5c4bd6aab7aa12635c1485.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

3. 输入Maven项目坐标创建项目

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\b9cb6ef4552e4d658c6adc4339b99371.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

4. 在pom.xml设置打包方式为war,默认是不写代表打包方式为jar

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\d6b33ac4748a4a9dad93731a106cbc0c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

    **注意：**如果要用Maven run package，需要在配置文件里加入下面代码，否则**报错Cannot access defaults field of Properties**

   ```XML
           <plugin>
             <artifactId>maven-war-plugin</artifactId>
             <version>3.2.2</version>
           </plugin>
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

5. 补齐Maven Web项目缺失webapp的目录结构

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\97dd4eb57e05420088542faadea2d5fc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

6. 补齐Maven Web项目缺失WEB-INF/web.xml的目录结构

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\de4fa3108e0e47f2a232b3697251aa7b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

7. 补充完后，最终的项目结构如下:

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\dd02b33c84c5466c94ba16fbc1a84d1a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

上述两种方式，创建的web项目，都不是很全，需要手动补充内容，至于最终采用哪种方式来创建Maven Web项目，都是可以的，根据各自的喜好来选择使用即可。

### **3.3.3** IDEA部署Tomcat

Maven Web项目创建成功后，通过Maven的package命令可以将项目打包成war包，将war文件拷贝到Tomcat的webapps目录下，启动Tomcat就可以将项目部署成功，然后通过浏览器进行访问即可。

然而我们在开发的过程中，项目中的内容会经常发生变化，如果按照上面这种方式来部署测试，是非常不方便的。

**如何在IDEA中能快速使用Tomcat呢?**

在IDEA中集成使用Tomcat有两种方式，分别是**集成本地Tomcat和Tomcat Maven插件。**

> **选用哪种方法？：** 
>
> - **第一种集成本地Tomcat：麻烦缓慢，但支持Tomcat8、9/10。**但是每次打开新项目要重新配置，较麻烦。
> - **插件方法：更简单，部署更快，但只支持Tomcat7。**如果对于Tomcat的版本有比较高的要求，要在Tomcat7以上，这个时候就只能用第一种了，例如Tomcat8解决get普通参数请求中文乱码问题，详细看下一篇request，但也不用太在意，用jsp时候确实需要request.getParameter有乱码问题，在学JSON后都是用获取JSON格式请求体，不用在意中文乱码问题。

[JavaWeb基础6——Request,Response,JSP&MVC_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126024588?spm=1001.2014.3001.5501)

**方法一：集成本地Tomcat**

目标: 将刚才本地安装好的Tomcat8集成到IDEA中，完成项目部署。

具体的实现步骤

1. 打开添加本地Tomcat的面板![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\6869d4051d61450db1f76ce7b9b598f5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2. 指定本地Tomcat的具体路径![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\e1573b01c05e4250a46b45ffb30f8620.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

   

3. 修改Tomcat的名称，更新操作改成重新部署，切出idea改成更新资源（切出idea自动更新前端资源）。HTTP port中的端口也可以进行修改，比如把8080改成80

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\99c3a805a5ab40e39b15ff6c1030acbc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

4. 将开发项目部署项目到Tomcat中，选war exploded![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\d4d69d4cfa534667b3ed06fb5d1cb551.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

5. 两种部署模式区别：

   > 扩展内容： **xxx.war和 xxx.war exploded这两种部署项目模式的区别?**
   >
   > - war模式是将WEB工程打成war包，把war包发布到Tomcat服务器上
   > - war exploded模式是将WEB工程以当前文件夹的位置关系发布到Tomcat服务器上
   > - war模式部署成功后，Tomcat的webapps目录下会有部署的项目内容
   > - war exploded模式部署成功后，Tomcat的webapps目录下没有，而使用的是项目的target目录下的内容进行部署
   > - 建议大家都选war模式进行部署，更符合项目部署的实际情况
   > - 建议开发时候选war exploded，可以选择更新类和资源，更快速开发。

6. 部署成功后，就可以启动项目，为了能更好的看到启动的效果，可以在webapp目录下添加a.html页面![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\3ccd85a1ab5b4a4dbfcc24eb99b280ec.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

   

7. 启动成功后，可以通过浏览器进行访问测试，访问路径可修改，如下：![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\2deede9bc6a04c759d4198af53db7a4b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\b9212babef244ddaafa9713310a50aa2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

   

   

8. 最终的注意事项

   ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\2aefde0dc893439b84965ffca05330de.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

   

   

至此，IDEA中集成本地Tomcat进行项目部署的内容我们就介绍完了，整体步骤如下，大家需要按照流程进行部署操作练习。

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\96a2f5e1429044d6b18696d00c181936.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**重启tomcat服务和重新部署和热部署**

1.重启tomcat服务：只会重新编译java目录下的文件（相当于更新.classes文件）
 2.重新部署：将java目录下文件和.xml等配置文件都复制到tomcat的运行环境中（相当于既更新.classes文件又更新web.xml等配置文件）
 3.热部署：在运行时修改jsp文件可以在不重服务器的情况下让修改生效，但是对修改配置文件（例如.xml）和java目录下代码无效！
 **总结：**开启热部署后，
 只改.jsp文件，不需要重新部署，直接刷新页面即可看到更改
 改配置文件和java目录下代码，就需要重新部署。

**IDEA Tomcat开启热部署方法：**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\618c666b98b6435a9b00a419c207b250.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**方法二：Tomcat Maven插件**

在IDEA中使用本地Tomcat进行项目部署，相对来说步骤比较繁琐，所以我们需要一种更简便的方式来替换它，那就是直接使用Maven中的Tomcat插件来部署项目，具体的实现步骤，只需要两步，分别是:

1. 在pom.xml中添加Tomcat插件（alt+insert插入插件模板）

   ```XML
   <build>
       <plugins>
       	<!--Tomcat插件 -->
           <plugin>
               <groupId>org.apache.tomcat.maven</groupId>
               <artifactId>tomcat7-maven-plugin</artifactId>
               <version>2.2</version>
           </plugin>
       </plugins>
   </build>
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

2. 使用Maven Helper插件快速启动项目，选中项目，右键-->Run Maven --> tomcat7:run![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\43329d02f3e04990bb96f92b21bccdf9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   



注意:

- 如果选中项目并右键点击后，看不到Run Maven和Debug Maven，这个时候就需要在IDEA中下载Maven Helper插件，具体的操作方式为: File --> Settings --> Plugins --> Maven Helper ---> Install,安装完后按照提示重启IDEA，就可以看到了。![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\0e7d38dc78eb496cae63f09c90a536a0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  



- Maven Tomcat插件目前只有Tomcat7版本，没有更高的版本可以使用
- 使用Maven Tomcat插件，要想修改Tomcat的端口和访问路径，可以直接修改pom.xml

```XML
<build>
    <plugins>
    	<!--Tomcat插件 -->
        <plugin>
            <!--第一次写可能显红，自动导入插件后，运行一次就好了 -->
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <!--配置访问端口号，也可以不配置，会使用Tomcat安装时配置的端口 -->
            	<port>80</port><!--访问端口号 -->
                <!--项目访问路径
					未配置访问路径: http://localhost:80/Maven模块名/a.html
					配置/后访问路径: http://localhost:80/a.html
					如果配置成 /hello,访问路径会变成什么?
						答案: http://localhost:80/hello/a.html
				-->
                <path>/</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**小结**

在IDEA中使用Tomcat的两种方式，集成本地Tomcat和使用Maven的Tomcat插件。后者更简单，推荐使用，但是如果对于Tomcat的版本有比较高的要求，要在Tomcat7以上，这个时候就只能用前者了。

## **3.4** Maven Web各种报错汇总

### 3.4.1 不再支持源选项 5。请使用 7 或更高版本。

**问题出现的原因**
 使用的JDK版本可能过高，不符合Maven中配置文件的要求
 此时，可以找的Maven安装目录conf文件夹下的settings.xml文件查看
 ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\bb027b9e3d3c4678a61ef03d99bb025f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​编辑
 **彻底解决**
 在Maven安装目录conf文件夹下的settings.xml配置文件中添加以下代码到<profiles>标签内部：

```XML
	  <profile>  
		 <id>jdk-11</id>  
		 <activation>  
			 <activeByDefault>true</activeByDefault>  
			 <jdk>11</jdk>  
		 </activation>
		 <properties>
			 <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
			 <maven.compiler.source>11</maven.compiler.source>  
			 <maven.compiler.target>11</maven.compiler.target>   
		 </properties>   
		</profile>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 也可以**单文件解决**，在pom.xml配置如下代码，适用于项目要在不同项目移动：

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

### 3.4.2 编码问题File encoding has not been set, using platform encoding GBK, i.e. build is p和Compilation failure

**彻底解决：**

idea设置里全部改成utf-8

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\b7afe9fc52a8446396a6d797beed3fa8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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



# 四、Servlet

## 4.1 简介

 **Servlet译为小服务程序，是一个接口（JavaEE规范之一），是一门动态web资源开发技术，是JavaWeb最为核心的内容。**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\fed85b0047dc451ab976b79d27d28aa2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- Servlet是JavaWeb最为核心的内容，它是Java提供的一门**动态web资源开发技术**。

- 使用Servlet就可以实现，根据不同的登录用户在页面上动态显示不同内容。

- Servlet是JavaEE规范之一，其实就是一个接口（规范一般都是接口，例如JDBC也是），将来我们需要定义Servlet类实现Servlet接口，并由web服务器运行Servlet。

  

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\c4dcd3f8cbff4dd6a99ab5d2273843c3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 4.2 快速入门

### 4.2.1 helloworld

> 了解即可，后面都是用模板开发、继承HttpServlet创建Servlet。

需求分析: 编写一个Servlet类，并使用IDEA中Tomcat插件进行部署，最终通过浏览器访问所编写的Servlet程序。

具体的实现步骤为:

**1.导入Servlet依赖坐标：**创建Maven Web项目`web-demo`，在pom.xml导入Servlet依赖坐标

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

**2.实现Servlet接口**:在src-main-java-package1下定义一个类，实现Servlet接口（alt+enter可自动生成所有实现的方法），并重写接口中所有方法，并在service方法中输入一句话。

```java
package com.itheima.web;

import javax.servlet.*;
import java.io.IOException;
@WebServlet("/demo1")
public class ServletDemo1 implements Servlet {

    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("servlet hello world~");
    }
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    public ServletConfig getServletConfig() {
        return null;
    }

    public String getServletInfo() {
        return null;
    }

    public void destroy() {

    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3.别忘了配置Servlet的访问路径:**在Servlet实现类上使用@WebServlet注解，配置该Servlet的访问路径，注意别忘了斜杠。

```java
@WebServlet("/demo1")
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**4.访问:**启动Tomcat,浏览器中输入URL地址访问该Servlet

```html
http://localhost:8080/web-demo/demo1
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> url里“web-demo” 看Tomcat部署里的应用程序上下文：
>
> ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\7a7332a76ea24115a29d539a8efb3e58.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

浏览器访问后，在控制台会打印`servlet hello world~` 说明servlet程序已经成功运行。

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\6c5fcd76f8bb4ca79f92facab9f8a3b3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

至此，Servlet的入门案例就已经完成，大家可以按照上面的步骤进行练习了。

### **4.2.2 报错解决：java: 警告: 源发行版 11 需要目标发行版 11**

**原因：**
 这是因为导入的项目创建时使用的是jdk11，而你的IDEA没有设置这个版本。

**解决方案：**
 1、点击左上角文件->设置-> 构建、执行、部署->java编译器，然后找到报错的项目（若没有显示，点击+），右边下拉框选择版本8

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\9e17921ae4a7405daec28f187db4640c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 项目结构里也都设置成jdk1.8：

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\7d3c49ee122d432589a6550e750607d7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\f15234a820c14a1db22ecd541eb3648a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 4.3 执行流程

Servlet程序已经能正常运行，但是我们需要思考个问题: 我们并没有创建ServletDemo1类的对象，也没有调用对象中的service方法，为什么在控制台就打印了`servlet hello world~`这句话呢?

要想回答上述问题，我们就需要对Servlet的执行流程进行一个学习。

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\b7374b9be80e427693bc3ced9a763d47.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **Servlet执行过程：**



- 1.浏览器发出`http://localhost:8080/web-demo/demo1`请求，从请求中可以解析出三部分内容，分别是`localhost:8080`、`web-demo`、`demo1`
  - 根据`localhost:8080`可以找到要访问的Tomcat Web服务器
  - 根据`web-demo`可以找到部署在Tomcat服务器上的web-demo项目
  - 根据`demo1`可以找到要访问的是项目中的哪个Servlet类，根据@WebServlet后面的值进行匹配
- 2.找到ServletDemo1这个类后，**Tomcat Web服务器**就会**为ServletDemo1这个类创建**一个**对象**，然后**调用对象中的service方法**
  - ServletDemo1实现了Servlet接口，所以类中必然会重写service方法供Tomcat Web服务器进行调用
  - service方法中有ServletRequest和ServletResponse两个参数，ServletRequest封装的是请求数据，ServletResponse封装的是响应数据，后期我们可以通过这两个参数实现前后端的数据交互

> **小结**
>
> 介绍完Servlet的执行流程，需要大家掌握两个问题：
>
> **1.Servlet对象由谁创建?Servlet方法由谁调用?**
>
> Servlet对象由web服务器Tomcat创建，Servlet方法由web服务器调用
>
> **2.服务器怎么知道Servlet中一定有service方法?**
>
> 因为我们自定义的Servlet,必须实现Servlet接口并复写其方法，而Servlet接口中有service方法



## 4.4 生命周期

介绍完Servlet的执行流程后，我们知道Servlet是由Tomcat Web服务器帮我们创建的。

接下来咱们再来思考一个问题:Tomcat什么时候创建的Servlet对象?

要想回答上述问题，我们就需要对Servlet的生命周期进行一个学习。

**生命周期:** 对象的生命周期指一个对象从被创建到被销毁的整个过程。

**Servlet运行在Servlet容器(web服务器)中，其生命周期由容器来管理**，分为4个阶段：

**1.加载和实例化：**默认情况下，当Servlet第一次被访问时，由容器创建Servlet对象

```bash
默认情况，Servlet会在第一次访问被容器创建，但是如果创建Servlet比较耗时的话，那么第一个访问的人等待的时间就比较长，用户的体验就比较差，那么我们能不能把Servlet的创建放到服务器启动的时候来创建，具体如何来配置?
urlPatterns和value都可以
@WebServlet(urlPatterns = "/demo1",loadOnStartup = 1)
loadOnstartup的取值有两类情况
	（1）负整数:第一次访问时创建Servlet对象
	（2）0或正整数:服务器启动时创建Servlet对象，数字越小优先级越高
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2.初始化：**在Servlet实例化之后，容器将调用Servlet的**init()方法初始化这个对象**，完成一些如加载配置文件、创建连接等初始化的工作。该方法只调用一次  

**3.请求处理：**每次请求Servlet（也就是访问浏览器）时，Servlet容器都会调用Servlet的**service()方法**对请求进行处理 

**4.服务终止：**当需要释放内存或者容器关闭时，容器就会调用Servlet实例的**destroy()方法**完成资源的释放。在destroy()方法调用之后，容器会释放这个Servlet实例，该实例随后会被Java的垃圾收集器所回收。

> **注意：**红色正方形按钮是强制停止进程，不会调用destroy（）方法，要打开底部终端使用命令停止。
>
> ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\4acc06333b5346778c2aa08f296743a2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\1dc4fe9574cc484989e4b0320e83f8f7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
>  开启：在Maven模块目录下mvn tomcat7:run
>
> 关闭：ctrl+c

- 通过案例演示下上述的生命周期

  ```java
  package com.itheima.web;
  
  import javax.servlet.*;
  import javax.servlet.annotation.WebServlet;
  import java.io.IOException;
  /**
  * Servlet生命周期方法，loadOnStartup非负，在服务器启动时创建servlet对象
  */
  @WebServlet(urlPatterns = "/demo2",loadOnStartup = 1)
  public class ServletDemo2 implements Servlet {
  
      /**
       *  初始化方法
       *  1.调用时机：默认情况下，Servlet被第一次访问（刷新一次网址就是访问一次）时，调用
       *      * loadOnStartup: 默认为-1，修改为0或者正整数，则会在服务器启动的时候，调用
       *  2.调用次数: 1次
       * @param config
       * @throws ServletException
       */
      public void init(ServletConfig config) throws ServletException {
          System.out.println("init...");
      }
  
      /**
       * 提供服务
       * 1.调用时机:每一次Servlet被访问时，调用
       * 2.调用次数: 多次
       * @param req
       * @param res
       * @throws ServletException
       * @throws IOException
       */
      public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
          System.out.println("servlet hello world~");
      }
  
      /**
       * 销毁方法
       * 1.调用时机：内存释放或者服务器关闭的时候，Servlet对象会被销毁，调用
       * 2.调用次数: 1次
       */
      public void destroy() {
          System.out.println("destroy...");
      }
      public ServletConfig getServletConfig() {
          return null;
      }
  
      public String getServletInfo() {
          return null;
      }
  
  
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  注意:如何才能让Servlet中的destroy方法被执行？![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\70d1a447cad54d8d9556833e063e3e9f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

  

在Terminal命令行中，先使用`mvn tomcat7:run`启动，然后再使用`ctrl+c`关闭tomcat

**小结**

这节中需要掌握的内容是:

1. Servlet对象在什么时候被创建的?

> 默认是第一次访问的时候被创建，可以使用@WebServlet(urlPatterns = "/demo2",loadOnStartup = 1)的loadOnStartup 修改成在服务器启动的时候创建。

1. Servlet生命周期中涉及到的三个方法，这三个方法是什么?什么时候被调用?调用几次?

> 涉及到三个方法，分别是 init()、service()、destroy()
>
> init方法在Servlet对象被创建的时候执行，只执行1次
>
> service方法在Servlet被访问的时候调用，每访问1次就调用1次
>
> destroy方法在Servlet对象被销毁的时候调用，只执行1次



## 4.5 Servlet接口的方法介绍

getServletInfo()和getServletConfig()这两个方法使用的不是很多，了解即可。

我们先来回顾下前面讲的三个方法，分别是:

- 初始化方法，在Servlet被创建时执行，只执行一次

```
void init(ServletConfig config) 
```

- 提供服务方法， 每次Servlet被访问，都会调用该方法

```
void service(ServletRequest req, ServletResponse res)
```

- 销毁方法，当Servlet被销毁时，调用该方法。在内存释放或服务器关闭时销毁Servlet

```
void destroy() 
```

剩下的两个方法是:

- **获取Servlet信息**

```java
String getServletInfo() 
//该方法用来返回Servlet的相关信息，没有什么太大的用处，一般我们返回一个空字符串即可
public String getServletInfo() {
    return "";
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **获取ServletConfig对象**

```java
ServletConfig getServletConfig()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

init(ServletConfig servletConfig)方法的参数为ServletConfig对象，Tomcat Web服务器在创建Servlet对象的时候会调用init方法，并传入一个ServletConfig对象。

我们只需要将服务器传过来的ServletConfig对象定义，并在init方法中通过this赋值即可。

```java
package com.itheima.web;

import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import java.io.IOException;

/**
 * Servlet方法介绍
 */
@WebServlet(urlPatterns = "/demo3",loadOnStartup = 1)
public class ServletDemo3 implements Servlet {

    private ServletConfig servletConfig;
    /**
     *  初始化方法
     *  1.调用时机：默认情况下，Servlet被第一次访问时，调用
     *      * loadOnStartup: 默认为-1，修改为0或者正整数，则会在服务器启动的时候，调用
     *  2.调用次数: 1次
     * @param config
     * @throws ServletException
     */
    public void init(ServletConfig servletConfig) throws ServletException {
        this.servletConfig = servletConfig ;
        System.out.println("init...");
    }
    public ServletConfig getServletConfig() {
        return servletConfig;
    }
    
    /**
     * 提供服务
     * 1.调用时机:每一次Servlet被访问时，调用
     * 2.调用次数: 多次
     * @param req
     * @param res
     * @throws ServletException
     * @throws IOException
     */
    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        System.out.println("servlet hello world~");
    }

    /**
     * 销毁方法
     * 1.调用时机：内存释放或者服务器关闭的时候，Servlet对象会被销毁，调用
     * 2.调用次数: 1次
     */
    public void destroy() {
        System.out.println("destroy...");
    }
    
    public String getServletInfo() {
        return "";
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 4.6 HttpServlet，**Servlet的继承体系结构**



**Servlet的体系结构:**![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\4f450be31468489b807741053d5abe2e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**更简单方式来创建Servlet**

```java
@WebServlet("/demo4")
public class ServletDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //TODO GET 请求方式处理逻辑
        System.out.println("get...");
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //TODO Post 请求方式处理逻辑
        System.out.println("post...");
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- 要想发送一个GET请求，请求该Servlet，只需要通过浏览器发送`http://localhost:8080/web-demo/demo4`,就能看到doGet方法被执行了
- 要想发送一个POST请求，请求该Servlet，单单通过浏览器是无法实现的，这个时候就需要编写一个form表单来发送请求，在webapp下创建一个`a.html`页面，内容如下:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="/web-demo/demo4" method="post">
        <input name="username"/><input type="submit"/>
    </form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动测试，即可看到doPost方法被执行了。



> Servlet的简化编写就介绍完了，接着需要思考两个问题:
>
> 1. HttpServlet中为什么要根据请求方式的不同，调用不同的方法?
> 2. 如何调用?

**HttpServlet底层** 

针对问题一，我们需要回顾之前的知识点前端发送GET和POST请求的时候，参数的位置不一致，GET请求参数在请求行中，POST请求参数在请求体中。

为了能处理不同的请求方式，我们得在service方法中进行判断，然后写不同的业务处理，这样能实现。

**Servlet类判断请求方式：**

```java
package com.itheima.web;

import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;


@WebServlet("/demo5")
public class ServletDemo5 implements Servlet {

    public void init(ServletConfig config) throws ServletException {

    }

    public ServletConfig getServletConfig() {
        return null;
    }

    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        //如何调用?
        //获取请求方式，根据不同的请求方式进行不同的业务处理
        HttpServletRequest request = (HttpServletRequest)req;
       //1. 获取请求方式
        String method = request.getMethod();
        //2. 判断
        if("GET".equals(method)){
            // get方式的处理逻辑
        }else if("POST".equals(method)){
            // post方式的处理逻辑
        }
    }

    public String getServletInfo() {
        return null;
    }

    public void destroy() {

    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

要解决上述问题，我们可以对Servlet接口进行继承封装，来简化代码开发。

**封装Servlet接口（模拟HttpServlet）：**

```java
package com.itheima.web;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;

public class MyHttpServlet implements Servlet {
    public void init(ServletConfig config) throws ServletException {

    }

    public ServletConfig getServletConfig() {
        return null;
    }

    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        HttpServletRequest request = (HttpServletRequest)req;
        //1. 获取请求方式
        String method = request.getMethod();
        //2. 判断
        if("GET".equals(method)){
            // get方式的处理逻辑
            doGet(req,res);
        }else if("POST".equals(method)){
            // post方式的处理逻辑
            doPost(req,res);
        }
    }

    protected void doPost(ServletRequest req, ServletResponse res) {
    }

    protected void doGet(ServletRequest req, ServletResponse res) {
    }

    public String getServletInfo() {
        return null;
    }

    public void destroy() {

    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```

```

有了MyHttpServlet这个类，以后我们再编写Servlet类的时候，只需要继承MyHttpServlet，重写父类中的doGet和doPost方法，就可以用来处理GET和POST请求的业务逻辑。接下来，可以把ServletDemo5代码进行改造

```java
@WebServlet("/demo5")
public class ServletDemo5 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {
        System.out.println("get...");
    }

    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
        System.out.println("post...");
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```

```

将来页面发送的是GET请求，则会进入到doGet方法中进行执行，如果是POST请求，则进入到doPost方法。这样代码在编写的时候就相对来说更加简单快捷。



类似MyHttpServlet这样的类Servlet中已经为我们提供好了，就是**HttpServlet**,翻开源码，大家可以搜索`service()`方法，你会发现HttpServlet做的事更多，**不仅可以处理GET和POST还可以处理其他五种请求方式**。

```java
protected void service(HttpServletRequest req, HttpServletResponse resp)
        throws ServletException, IOException
    {
        String method = req.getMethod();

        if (method.equals(METHOD_GET)) {
            long lastModified = getLastModified(req);
            if (lastModified == -1) {
                // servlet doesn't support if-modified-since, no reason
                // to go through further expensive logic
                doGet(req, resp);
            } else {
                long ifModifiedSince = req.getDateHeader(HEADER_IFMODSINCE);
                if (ifModifiedSince < lastModified) {
                    // If the servlet mod time is later, call doGet()
                    // Round down to the nearest second for a proper compare
                    // A ifModifiedSince of -1 will always be less
                    maybeSetLastModified(resp, lastModified);
                    doGet(req, resp);
                } else {
                    resp.setStatus(HttpServletResponse.SC_NOT_MODIFIED);
                }
            }

        } else if (method.equals(METHOD_HEAD)) {
            long lastModified = getLastModified(req);
            maybeSetLastModified(resp, lastModified);
            doHead(req, resp);

        } else if (method.equals(METHOD_POST)) {
            doPost(req, resp);
            
        } else if (method.equals(METHOD_PUT)) {
            doPut(req, resp);
            
        } else if (method.equals(METHOD_DELETE)) {
            doDelete(req, resp);
            
        } else if (method.equals(METHOD_OPTIONS)) {
            doOptions(req,resp);
            
        } else if (method.equals(METHOD_TRACE)) {
            doTrace(req,resp);
            
        } else {
            //
            // Note that this means NO servlet supports whatever
            // method was requested, anywhere on this server.
            //

            String errMsg = lStrings.getString("http.method_not_implemented");
            Object[] errArgs = new Object[1];
            errArgs[0] = method;
            errMsg = MessageFormat.format(errMsg, errArgs);
            
            resp.sendError(HttpServletResponse.SC_NOT_IMPLEMENTED, errMsg);
        }
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**小结**

通过这一节的学习，要掌握:

**1.HttpServlet的使用步骤**

> 继承HttpServlet
>
> 重写doGet和doPost方法

**2.HttpServlet原理**

> 获取请求方式，并根据不同的请求方式，调用不同的doXxx方法

## 4.7 IDEA使用模板创建Servlet

使用通用方式获取请求参数后，屏蔽了GET和POST的请求方式代码的不同，则代码可以定义如下格式:![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\33703be6b5e748cab13a15126b08a4af.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



由于格式固定，所以我们可以使用IDEA提供的模板来制作一个Servlet的模板，这样我们后期在创建Servlet的时候就会更高效，具体如何实现:

(1)按照自己的需求，修改Servlet创建的模板内容。annotated译为带注释的

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\d5bd500d65884e76a11e8afcdc947570.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

（2）使用servlet模板创建Servlet类![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\9e3f65bef9a544739627210ad5374313.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

示例：

```java
@WebServlet("/servletDemo")
public class ServletDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("hellohah");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **IDEA中new 没有\**\*\*\*\*[servlet](https://so.csdn.net/so/search?q=servlet&spm=1001.2101.3001.7020)\*\*\*\*\** 的选项解决方法：**
>
> 首先检查Servlet的依赖是否导入pom.xml
>
> ```XML
>     <dependency>
>       <groupId>javax.servlet</groupId>
>       <artifactId>javax.servlet-api</artifactId>
>       <version>3.1.0</version>
>     </dependency>
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> file-项目结构（注意main文件夹下要有java和resources目录）：
>
> ![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\c9bb1e807484474aaf5509b3dd6d774e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 4.8 @WebServlet的urlPattern配置规则

Servlet类编写好后，要想被访问到，就需要配置其访问路径@WebServlet（urlPattern）

**一个Servlet,可以配置多个urlPattern**![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\ff1d3c72523b477fba4a3539218714bc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 示例：



```java
package com.itheima.web;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

/**
* urlPattern: 一个Servlet可以配置多个访问路径
*/
@WebServlet(urlPatterns = {"/demo7","/demo8"})
public class ServletDemo7 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {
        
        System.out.println("demo7 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在浏览器上输入`http://localhost:8080/web-demo/demo7`,`http://localhost:8080/web-demo/demo8`这两个地址都能访问到ServletDemo7的doGet方法。

**urlPattern配置规则**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\04dff13d7d30412699a2b0ec9fb3725b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**精确匹配（常用）**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\cf16eb83243d4848beea9a97e5578421.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

示例： 



```java
/**
 * UrlPattern:
 * * 精确匹配
 */
@WebServlet(urlPatterns = "/user/select")
public class ServletDemo8 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {

        System.out.println("demo8 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问路径`http://localhost:8080/web-demo/user/select`

**目录匹配（通配符）**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\83ebeed9a0ed43d9a1ee73a9fa59b0f4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

示例： 



```java
package com.itheima.web;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

/**
 * UrlPattern:
 * * 目录匹配: /user/*
 */
@WebServlet(urlPatterns = "/user/*")
public class ServletDemo9 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {

        System.out.println("demo9 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问路径`http://localhost:8080/web-demo/user/任意`

> **思考:**
>
> **答案是:** 能、能、demo8，进而我们可以得到的结论是：`/user/*`中的**`/\*`代表的是零或多个层级访问目录，同时精确匹配优先级要高于目录匹配。**
>
> 1. 访问路径`http://localhost:8080/web-demo/user`是否能访问到demo9的doGet方法?
> 2. 访问路径`http://localhost:8080/web-demo/user/a/b`是否能访问到demo9的doGet方法?
> 3. 访问路径`http://localhost:8080/web-demo/user/select`是否能访问到demo9还是demo8的doGet方法?

**扩展名匹配**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\73fab3d41eb546469e7bc6f5d8caa51a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

示例： 



```java
package com.itheima.web;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

/**
 * UrlPattern:
 * * 扩展名匹配: *.do注意前面没斜杠
 */
@WebServlet(urlPatterns = "*.do")
public class ServletDemo10 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {

        System.out.println("demo10 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问路径`http://localhost:8080/web-demo/任意.do`

**注意:**



如果路径配置的是`*.do`,那么在*.do的前面不能加`/`,否则会报错![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\c3d946a748a244a1a506526ca35436bb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**任意匹配（不建议用）**

![img](JavaWeb基础5——HTTP，Tomcat&Servlet.assets\195876a54c3b4ca68fb3bd1f6d061c42.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**"/" ：覆盖DefaultServlet**

```java
package com.itheima.web;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

/**
 * UrlPattern:
 * * 任意匹配： /
 */
@WebServlet(urlPatterns = "/")
public class ServletDemo11 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {

        System.out.println("demo11 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问路径`http://localhost:8080/demo-web/任意`

**"/\*" ：优先度高于斜杠**

```java
package com.itheima.web;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

/**
 * UrlPattern:
 * * 任意匹配： /*
 */
@WebServlet(urlPatterns = "/*")
public class ServletDemo12 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {

        System.out.println("demo12 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```

```

访问路径`http://localhost:8080/demo-web/任意

> **注意:/和/\*的区别?**
>
> 1. 当我们的项目中的Servlet配置了 "/",会覆盖掉tomcat中的**DefaultServlet**,当其他的url-pattern都匹配不上时都会走这个Servlet
> 2. 当我们的项目中配置了"/*",意味着匹配任意访问路径
>
> DefaultServlet是用来处理静态资源，如果配置了"/"会把默认的覆盖掉，就会引发请求静态资源的时候没有走默认的而是走了自定义的Servlet类，最终导致静态资源不能被访问

**小结**

1. urlPattern总共有四种配置方式，分别是精确匹配、目录匹配、扩展名匹配、任意匹配
2. 五种配置的优先级为 精确匹配 > 目录匹配> 扩展名匹配 > /* > / ,无需记，以最终运行结果为准。

## 4.9 老版本Servlet通过XML配置路径

Servlet从3.0版本后开始支持注解配置@WebServlet，**3.0版本前只支持XML配置文件的配置方法**。

对于XML的配置步骤有两步:

- 编写Servlet类

```java
package com.itheima.web;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

public class ServletDemo13 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {

        System.out.println("demo13 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 在web.xml中配置该Servlet

```XML
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    
    
    
    <!-- 
        Servlet 通过名字配置全类名
    -->
    <servlet>
        <!-- servlet的名称，名字任意，不是访问路径-->
        <servlet-name>demo13</servlet-name>
        <!--servlet的带包类全名-->
        <servlet-class>com.itheima.web.ServletDemo13</servlet-class>
    </servlet>

    <!-- 
        Servlet 通过名字配置访问路径
    -->
    <servlet-mapping>
        <!-- servlet的名称，要和上面的名称一致-->
        <servlet-name>demo13</servlet-name>
        <!-- servlet的访问路径-->
        <url-pattern>/demo13</url-pattern>
    </servlet-mapping>
</web-app>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这种配置方式和注解比起来，确认麻烦很多，所以建议大家使用注解来开发。但是大家要认识上面这种配置方式，因为并不是所有的项目都是基于注解开发的。