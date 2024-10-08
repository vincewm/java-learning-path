>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[一、JDBC](#JDBC)

[1.1 JDBC概述](#JDBC%E6%A6%82%E8%BF%B0)

[1.1.1 JDBC概念](#JDBC%E6%A6%82%E5%BF%B5)

[1.1.2 JDBC本质](#JDBC%E6%9C%AC%E8%B4%A8)

[1.1.3 JDBC好处](#JDBC%E5%A5%BD%E5%A4%84)

[1.2 JDBC步骤](#JDBC%E6%AD%A5%E9%AA%A4)

[1.2.1 标准代码](#%C2%A0%E6%A0%87%E5%87%86%E4%BB%A3%E7%A0%81)

[1.2.2 编写代码步骤](#%E7%BC%96%E5%86%99%E4%BB%A3%E7%A0%81%E6%AD%A5%E9%AA%A4)

[1.3 获取数据库连接的多种方式](#%E8%8E%B7%E5%8F%96%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E7%9A%84%E5%90%84%E7%A7%8D%E6%96%B9%E5%BC%8F)

[二、JDBC所有API](#JDBC%E6%89%80%E6%9C%89API)

[2.1 驱动管理类 DriverManager](#%E9%A9%B1%E5%8A%A8%E7%AE%A1%E7%90%86%E7%B1%BB%20DriverManager)

[2.2 数据库连接对象Connection](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E5%AF%B9%E8%B1%A1Connection)

[2.2.1 获取执行对象](#%E8%8E%B7%E5%8F%96%E6%89%A7%E8%A1%8C%E5%AF%B9%E8%B1%A1)

[2.2.2 事务管理](#%E4%BA%8B%E5%8A%A1%E7%AE%A1%E7%90%86)

[2.3 Statement](#Statement)

[2.3.1 结果集对象 ResultSet](#%E7%BB%93%E6%9E%9C%E9%9B%86%E5%AF%B9%E8%B1%A1%20ResultSet)

[2.3.2 SQL注入问题](#%C2%A0SQL%E6%B3%A8%E5%85%A5)

[2.4 PreparedStatement](#PreparedStatement)

[2.4.1 概述](#2.4.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[2.4.2 PreparedStatement原理](#PreparedStatement%E5%8E%9F%E7%90%86)

[2.5 数据库连接池DataSource](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E6%B1%A0DataSource)

[2.5.1 数据库连接池简介](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E6%B1%A0%E7%AE%80%E4%BB%8B)

[2.5.2 数据库连接池实现](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E6%B1%A0%E5%AE%9E%E7%8E%B0)

[2.5.3 Driud下载](#Driud%E4%B8%8B%E8%BD%BD)

[2.5.4 Driud使用](#%C2%A0Driud%E4%BD%BF%E7%94%A8)

[2.5.5 Druid配置文件详解](#Druid%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E8%AF%A6%E8%A7%A3)

[三、JDBC练习](#%C2%A0JDBC%E7%BB%83%E4%B9%A0)

[3.1 需求：完成商品品牌数据的增删改查操作](#%E9%9C%80%E6%B1%82%EF%BC%9A%E5%AE%8C%E6%88%90%E5%95%86%E5%93%81%E5%93%81%E7%89%8C%E6%95%B0%E6%8D%AE%E7%9A%84%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5%E6%93%8D%E4%BD%9C)

[3.2 案例实现](#%E6%A1%88%E4%BE%8B%E5%AE%9E%E7%8E%B0)

--

## 一、JDBC

### 1.1 JDBC概述

#### 1.1.1 JDBC概念

> **了解即可**，后面开发都用Mybatis框架。MyBatis是一个持久层ORM框架,底层是对JDBC的封装。
> 
> JDBC是Java提供的一个**操作数据库**的API; 
> 
> **全称：**( Java DataBase Connectivity ) **Java 数据库连接**

**为什么要用jdbc？**

我们开发的**同一套Java代码无法操作不同的关系型数据库**，因为每一个关系型数据库的底层实现细节都不一样。为了解决这个问题，JDBC中定义了**所有操作关系型数据库的规则（接口）**。

众所周知接口是无法直接使用的，我们需要使用接口的实现类，而这套**实现类（称之为：驱动）**就由各自的数据库厂商给出。

#### 1.1.2 JDBC本质

-   官方（sun公司）定义的一套**操作所有关系型数据库的规则，即接口**
    
-   各个数据库厂商去实现这套接口，提供**数据库驱动jar包**
    
-   我们可以使用这套接口（JDBC）编程，真正执行的代码是**驱动jar包中的实现类**
    

#### 1.1.3 JDBC好处

-   各数据库厂商使用相同的接口，Java代码不需要针对不同数据库分别开发
    
-   **可随时替换底层数据库**，访问数据库的Java代码基本不变
    

以后编写操作数据库的代码只需要面向JDBC（接口），操作哪儿个关系型数据库就需要导入该数据库的驱动包，如需要操作MySQL数据库，就需要再项目中导入MySQL数据库的驱动包。如下图就是MySQL驱动包：

![](https://i-blog.csdnimg.cn/blog_migrate/27f9f1a5915dad6216f38fdbd79a0de5.png)

### 1.2 JDBC步骤

 通过Java操作数据库的流程：

![](https://i-blog.csdnimg.cn/blog_migrate/63bb1089a5fffddfc4b7e41616c6f737.png)

第一步：编写Java代码

第二步：Java代码将SQL发送到MySQL服务端

第三步：MySQL服务端接收到SQL语句并执行该SQL语句

第四步：将SQL语句执行的结果返回给Java代码

#### 1.2.1 标准代码

>  jdbc整个技术点**了解即可**，后面更多用Mybatis框架简化了jdbc开发，Mybatis整合spring后代码还有改变。
> 
> **剧透Mybatis：**下面是Mybatis框架操作数据库代码，下一章详细讲，**现在看看就行**
> 
> [JavaWeb基础3——Maven&MyBatis\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/125818307?spm=1001.2014.3001.5501 "JavaWeb基础3——Maven&MyBatis_vincewm的博客-CSDN博客")
> 
> ```java
> 
> public class Demo {
>  
>     public static void main(String[] args) throws IOException {
>         //1. 加载mybatis的核心配置文件，获取 SqlSessionFactory
>         String resource = "mybatis-config.xml";
>         InputStream inputStream = Resources.getResourceAsStream(resource);
>         SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
>  
>         //2. 获取SqlSession对象，用它来执行sql
>         SqlSession sqlSession = sqlSessionFactory.openSession();
>         //3. 执行sql
>         //参数是一个字符串，该字符串必须是映射配置文件的namespace.id
> //        List<User> users = sqlSession.selectList("test.selectAll");
>         //3.1获取UserMapper接口的代理对象
>         UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
>         //3.2调用sql方法
>         List<User> users = userMapper.selectAll();
>         System.out.println(users);
>         //4. 释放资源
>         sqlSession.close();
>     }
> }
> ```

**简单版：**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

/**
 * 简单版
 */
public class Demo {

    public static void main(String[] args) throws Exception {
        //1. 注册驱动
        
        //Class.forName("com.mysql.jdbc.Driver");//通过反射获取Driver实现类对象，从而加载驱动，注册驱动语句DriverManager.registerDriver(driver)在Driver的静态代码块里做过了。
        //此句仅在mysql可省略，其他数据库不能省略
        //2. 获取连接
        String url = "jdbc:mysql://127.0.0.1:3306/db1?useSSL=false";    //?useSSL=false禁用安全连接方式，解决警告提示
        String username = "root";
        String passWord = "1234";
        Connection conn = DriverManager.getConnection(url, username, passWord);
        //3. 定义sql
        String sql = "update student set age = 80 where name='xiaohua'";
        //4. 获取执行sql的对象 Statement
        Statement stmt = conn.createStatement();
        //5. 执行sql
        int count = stmt.executeUpdate(sql);//受影响的行数
        //6. 处理结果
        System.out.println(count);
        //7. 释放资源
        stmt.close();
        conn.close();
    }
}
```

**优化版，**Properties和PreparedStatement：

```java
import java.io.FileReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.Statement;
import java.util.Properties;

/**
 * 优化版
 */
public class Demo {

    public static void main(String[] args) throws Exception {
        Properties prop=new Properties();
        //System.out.println(System.getProperty("user.dir")); //获取当前路径
        FileReader fileReader = new FileReader("module2/src/jdbc.properties");
        prop.load(fileReader);

        //1. 注册驱动
//        Class.forName(prop.getProperty("driverClass"));
        //2. 获取连接
        String url = prop.getProperty("url");
        String username = prop.getProperty("username");
        String password = prop.getProperty("password");
        Connection conn = DriverManager.getConnection(url, username, password);
        //3. 定义sql
        //4. 获取执行sql的对象 Statement
        PreparedStatement pstmt = conn.prepareStatement("update student set age = ? where name=?"); //PreparedStatement防止sql注入
        pstmt.setInt(1,30);pstmt.setString(2,"xiaoming");
        //5. 执行sql
        int count = pstmt.executeUpdate();//受影响的行数
        //6. 处理结果
        System.out.println(count);
        //7. 释放资源
        pstmt.close();
        conn.close();
    }
}
```

```bash
#jdbc.properties
username=root
password=1234
url=jdbc:mysql://127.0.0.1:3306/db1
driverClass=com.mysql.jdbc.Driver
```

#### 1.2.2 编写代码步骤

**0.导入驱动jar包**。

![](https://i-blog.csdnimg.cn/blog_migrate/27f9f1a5915dad6216f38fdbd79a0de5.png)

**为什么要导包？**

因为jdbc本质是关系型数据库接口，需要导入数据库的实现类的包才能连接数据库。

**方法**：将mysql的驱动包放在模块下的lib目录（随意命名）下，右键add as library，也就是将该jar包添加为库文件，选择模块有效，name为空就行。

**地址**：[MySQL :: Download Connector/J](https://dev.mysql.com/downloads/connector/j/ "MySQL :: Download Connector/J")，选择**Platform Independent。**

在添加为库文件的时候，有如下三个选项

Global Library ： 全局有效

Project Library : 项目有效

Module Library ： 模块有效

**1.加载并注册驱动**

```java
Class.forName("com.mysql.jdbc.Driver");    //把mysql的驱动类Driver的对象加载进内存并初始化
```

**驱动类Driver 的方法：**

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i3"><td><code>static <a href="../../java/lang/Class.html" rel="nofollow">类</a>&lt;?&gt;</code></td><td><code><a href="../../java/lang/Class.html#forName-java.lang.String-" rel="nofollow">forName</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;className)</code><p>返回与给定字符串名称的类或接口相关联的 <code>类</code>对象。</p></td></tr></tbody></table>
        

> JDBC中定义了所有操作关系型数据库的规则（接口），**驱动类就是这些接口的实现类。** 

 **Class.forName 方法的作用**：初始化驱动类。

**MySQL中此行代码可以省略：** 

而我们给定的 MySQL 的 Driver 类中，它在**静态代码块**中通过 JDBC 的 DriverManager 注册了一下驱动。我们也可以直接使用 JDBC 的驱动管理器DriverManager 注册 mysql 驱动，从而代替使用 Class.forName。

```java
DriverManager.registerDriver(new Driver());
```

**2.获取连接**（获取java与mysql服务端之间的连接）

```
Connection conn = DriverManager.getConnection(url, username, password);
```

驱动管理器类DriverManager的方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>static <a href="../../java/sql/Connection.html" rel="nofollow">Connection</a></code></td><td><code><a href="../../java/sql/DriverManager.html#getConnection-java.lang.String-java.lang.String-java.lang.String-" rel="nofollow">getConnection</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;url, <a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;user, <a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;password)</code><p>尝试建立与给定数据库URL的连接。</p></td></tr></tbody></table>
        

Java代码需要发送SQL给MySQL服务端，就需要先建立连接

**3.定义SQL语句**

```java
String sql =  “update…” ;
```

**4.获取执行SQL对象**

执行SQL语句需要SQL执行对象，而这个执行对象就是Statement对象

```java
Statement stmt = conn.createStatement();
```

**5.执行SQL**（把SQL语句发送到mysql服务器，mysql服务器执行SQL语句）

```java
stmt.executeUpdate(sql);  
```

6.java处理返回结果

7.释放资源

### 1.3 获取数据库连接的多种方式

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i1"><td><code><a href="../../java/sql/Connection.html" rel="nofollow">Connection</a></code></td><td><code><a href="../../java/sql/Driver.html#connect-java.lang.String-java.util.Properties-" rel="nofollow">connect</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;url, <a href="../../java/util/Properties.html" rel="nofollow">Properties</a>&nbsp;info)</code><p>尝试使数据库连接到给定的URL。</p></td></tr></tbody></table>
        

**方法一：**通过Driver对象获取： 

```java
        Driver driver=new com.mysql.jdbc.Driver();  //多态语句，driver是Driver接口对象，com.mysql.jdbc.Driver()是mysql的实现类
        String url="jdbc:mysql://127.0.0.1:3306/db1";   //jdbc是主协议，mysql是子协议，主协议:子协议://ip地址:端口/数据库名
        Properties info=new Properties();
        info.setProperty("user","root");
        info.setProperty("password","1234");
        Connection conn=driver.connect(url,info);
```

**方法二：**通过反射获取： 

```java
        Class c=Class.forName("com.mysql.jdbc.Driver");    //通过反射，获取Driver实现类对象c
        Driver driver=(Driver) c.newInstance();            //调用类对象c的构造方法，实现构造方法对象driver的创建
        String url="jdbc:mysql://127.0.0.1:3306/db1";   //jdbc是主协议，mysql是子协议，主协议:子协议://ip地址:端口/数据库名
        Properties info=new Properties();
        info.setProperty("user","root");
        info.setProperty("password","1234");
        Connection conn=driver.connect(url,info);
```

**方法三：**DriverManager替代Driver

DriverManager方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>static void</code></td><td><code><a href="../../java/sql/DriverManager.html#registerDriver-java.sql.Driver-" rel="nofollow">registerDriver</a>(<a href="../../java/sql/Driver.html" rel="nofollow">Driver</a>&nbsp;driver)</code><p>注册与给定的驱动程序 <code>DriverManager</code> 。</p></td></tr><tr><td><code>static <a href="../../java/sql/Connection.html" rel="nofollow">Connection</a></code></td><td><code><a href="../../java/sql/DriverManager.html#getConnection-java.lang.String-java.lang.String-java.lang.String-" rel="nofollow">getConnection</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;url, <a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;user, <a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;password)</code><p>尝试建立与给定数据库URL的连接。</p></td></tr></tbody></table>
        

![](https://i-blog.csdnimg.cn/blog_migrate/a325459d7aaf4c41dd77152e0b536456.png)

 **方法四：**可以只是加载驱动，注册驱动在mysql的Driver实现类静态代码块里做过了，故可以省略相关语句。

```java
        //1. 注册驱动
//        Class.forName("com.mysql.jdbc.Driver");
        //2. 获取连接
        String url = "jdbc:mysql://127.0.0.1:3306/db1";
        String username = "root";
        String passWord = "1234";
        Connection conn = DriverManager.getConnection(url, username, passWord);
```

 ![](https://i-blog.csdnimg.cn/blog_migrate/dd276542234b08323efaee71ac8ed092.png)

 **方法五：**

src下新建jdbc.properties:

![](https://i-blog.csdnimg.cn/blog_migrate/654d00a975f7e7a4f99681d6b2b68697.png)

![](https://i-blog.csdnimg.cn/blog_migrate/388d3f0932d8716ed7bbc755bdf9151a.png)

## 二、JDBC所有API

### 2.1 驱动管理类 DriverManager

**作用**：注册驱动和获取数据库连接

**注册驱动方法：**

![](https://i-blog.csdnimg.cn/blog_migrate/d9a25535d4a31f4aa12852ac9edfb46a.png)

 而在实际连接数据库的时候并不需要registerDriver，因为mysql的**Driver实现类**里有**静态代码块**已经registerDriver过了：

![](https://i-blog.csdnimg.cn/blog_migrate/5bfce81fe0b4cae3833cabf51b033e9d.png)

 因此我们只需要加载 `Driver` 类进内存，该静态代码块就会执行：

```java
// 将类Driver加载到内存，在内存会产生一个和类Driver对应的Class实例
Class class = Class.forName("com.mysql.jdbc.Driver");
```

> **提示：**mysql加载Driver类方法可以省略
> 
> -   MySQL 5之后的驱动包，可以省略注册驱动的步骤
>     
> -   自动加载jar包中META-INF/services/java.sql.Driver文件中的驱动类
>     

DriverManager类，**获取数据库连接**方法：

![](https://i-blog.csdnimg.cn/blog_migrate/c92fd8d3479e0ec7c40eebb923dad434.png)

> **url** ： 连接路径
> 
> **语法：**主协议jdbc:子协议mysql://ip地址(域名):端口号/数据库名称?参数键值对1&参数键值对2…
> 
> **示例：**jdbc:mysql://127.0.0.1:3306/db1
> 
> jdbc:mysql://localhost:3306/db1
> 
> **细节**：
> 
> -   **url简写依据：**如果连接的是本机mysql服务器，并且mysql服务默认端口是3306，则url可以**简写**为：jdbc:mysql:///数据库名称?参数键值对，示例：jdbc:mysql:///db1?useSSL=false
>     
> -   配置 **useSSL=false** 参数，禁用安全连接方式，解决警告提示，示例：jdbc:mysql://127.0.0.1:3306/db1?useSSL=false
>     

### 2.2 数据库连接对象Connection

```java
        //4. 获取执行sql的对象 Statement

        Statement stmt = conn.createStatement();
        //Statement对象：用于执行静态SQL语句并返回其生成的结果的对象。 
```

**Connection（数据库连接对象）作用：**

-   获取执行 SQL 的对象
    
-   管理事务
    

#### 2.2.1 获取执行对象

-   **普通执行SQL对象**
    
    ```java
    Statement createStatement()   
    
    ```
    
    标准代码中就是通过该方法获取的执行对象。
    
-   **预编译SQL的执行SQL对象：防止SQL注入**
    
    ```
    PreparedStatement  prepareStatement(sql)
    ```
    
    通过这种方式获取的 `PreparedStatement` SQL语句执行对象是我们一会重点要进行讲解的，它可以防止SQL注入。
    
-   执行存储过程的对象
    
    ```
    CallableStatement prepareCall(sql)
    ```
    
    通过这种方式获取的 `CallableStatement` 执行对象是用来执行存储过程的，而存储过程在MySQL中不常用，所以这个我们将不进行讲解。
    

#### 2.2.2 事务管理

![](https://i-blog.csdnimg.cn/blog_migrate/0107e1f8670d79cadf475ee408ef38c2.png)

先回顾一下MySQL事务管理的操作：

-   开启事务 ： BEGIN; 或者 START TRANSACTION;
    
-   提交事务 ： COMMIT;
    
-   回滚事务 ： ROLLBACK;
    

> **MySQL默认是自动提交事务**
> 
> 也可以通过下面语句查询默认提交方式：
> 
> ```sql
> SELECT @@autocommit;
> ```
> 
> 查询到的结果是1 则表示自动提交，结果是0表示手动提交。当然也可以通过下面语句修改提交方式
> 
> ```sql
> set @@autocommit = 0;
> ```

接下来学习JDBC事务管理的方法。

**Connection几口中定义了3个对应的方法：**

**开启事务**

![](https://i-blog.csdnimg.cn/blog_migrate/5b061c35355c2375e22b1847e2ff94df.png)

参与autoCommit 表示是否自动提交事务，true表示自动提交事务，false表示手动提交事务。而开启事务需要将该参数设为为false。

**提交事务**

![](https://i-blog.csdnimg.cn/blog_migrate/4cab114ffcc3e7f9258b2d75348cdb80.png)

**回滚事务**

![](https://i-blog.csdnimg.cn/blog_migrate/25e3846a57618ebef149b24713ffe78d.png)

**具体代码实现如下：**

```
/**
 * JDBC API 详解：Connection
 */
public class JDBCDemo3_Connection {

    public static void main(String[] args) throws Exception {
        //1. 注册驱动
        //Class.forName("com.mysql.jdbc.Driver");
        //2. 获取连接：如果连接的是本机mysql并且端口是默认的 3306 可以简化书写
        String url = "jdbc:mysql:///db1?useSSL=false";
        String username = "root";
        String passWord = "1234";
        Connection conn = DriverManager.getConnection(url, username, passWord );
        //3. 定义sql
        String sql1 = "update account set money = 3000 where id = 1";
        String sql2 = "update account set money = 3000 where id = 2";
        //4. 获取执行sql的对象 Statement
        Statement stmt = conn.createStatement();

        try {
            // ============开启事务==========
            conn.setAutoCommit(false);
            //5. 执行sql
            int count1 = stmt.executeUpdate(sql1);//受影响的行数
            //6. 处理结果
            System.out.println(count1);
            int i = 3/0;
            //5. 执行sql
            int count2 = stmt.executeUpdate(sql2);//受影响的行数
            //6. 处理结果
            System.out.println(count2);

            // ============提交事务==========
            //程序运行到此处，说明没有出现任何问题，则需求提交事务
            conn.commit();
        } catch (Exception e) {
            // ============回滚事务==========
            //程序在出现异常时会执行到这个地方，此时就需要回滚事务
            conn.rollback();
            e.printStackTrace();
        }

        //7. 释放资源
        stmt.close();
        conn.close();
    }
}
```

### 2.3 Statement

 Statement对象的**作用**就是用来**执行SQL语句**。

```
        String sql = "update student set age = 222 where name='xiaohua'";
        //4. 获取执行sql的对象 Statement
        Statement stmt = conn.createStatement();
        //5. 执行sql
        int count = stmt.executeUpdate(sql);//受影响的行数
```

> **注意：**
> 
> -   以后开发很少使用java代码操作DDL语句
>     

**执行DDL、DML语句**

 ![](https://i-blog.csdnimg.cn/blog_migrate/a39fd18b27f5ef0535dc36ed3364e607.png)

**DDL：**show,create,use,select,drop,alter

**DML：**insert,update,delete

 **执行DQL语句**

![](https://i-blog.csdnimg.cn/blog_migrate/5947707ba0c3f514d58561eeaafb2151.png)

 **DQL:**select,from,where,group by,having,order by,limit

#### 2.3.1 结果集对象 ResultSet

**作用：**封装了SQL查询语句的结果，执行了DQL语句后就会返回该对象。

**回顾Statement执行DQL语句的方法，返回值就是ResultSet对象：**

```java
ResultSet  executeQuery(sql)：执行DQL 语句，返回 ResultSet 对象
```

**方法：**

> boolean next()
> 
> -   将光标从当前位置向下移动一行，并判断当前行是否为有效行
>     
> 
> 方法返回值说明：
> 
> -   true ： 有效行，当前行有数据
>     
> -   false ： 无效行，当前行没有数据
>     

> xxx getXxx(参数)：获取数据
> 
> -   xxx : 数据类型；如： int getInt(参数) ；String getString(参数)
>     
> -   参数
>     
>     -   int类型的参数：列的编号，从1开始
>         
>     -   String类型的参数： 列的名称
>         

示例：

```java
import java.io.FileReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Properties;

/**
 * JDBC快速入门
 */
public class Demo {

    public static void main(String[] args) throws Exception {
        Properties prop=new Properties();
        FileReader fileReader = new FileReader("module2/src/jdbc.properties");
        prop.load(fileReader);

        //1. 注册驱动
        Class.forName(prop.getProperty("driverClass"));
        //2. 获取连接
        String url = prop.getProperty("url");
        String username = prop.getProperty("username");
        String password = prop.getProperty("password");
        Connection conn = DriverManager.getConnection(url, username, password);
        //3. 定义sql
        String sql = "select * from student";
        //4. 获取执行sql的对象 Statement
        Statement stmt = conn.createStatement();
        //5. 执行sql
        ResultSet resultSet = stmt.executeQuery(sql);
        while(resultSet.next()){
            System.out.println(resultSet.getInt("id")+" "+resultSet.getString("name"));
        }

        //7. 释放资源
        stmt.close();
        conn.close();
        resultSet.close();
    }
}
```

#### 2.3.2 SQL注入问题

SQL注入是通过操作输入来**修改事先定义好的SQL语句**，用以达到执行代码**对服务器进行攻击**的方法。

**SQL注入问题模拟：**

![](https://i-blog.csdnimg.cn/blog_migrate/f580b0afeaccd38cd5b9a61b42615cff.png)

这样只需要输入框写入'1' = '1就可以令拼接后sql语句条件判断为true，从而获取到所有用户信息。

**详细解释：**上面代码是将用户名和密码拼接到sql语句中，拼接后的sql语句如下

![](https://i-blog.csdnimg.cn/blog_migrate/5efc1f10a2a275f4044533a0e529a205.png)

从上面语句可以看出条件![](https://i-blog.csdnimg.cn/blog_migrate/26731053df823fb58fe5a9ed2494dbc5.png)不管是否满足， `or` 后面的 `'1' = '1'` 都是始终满足的，最终条件是成立的，就可以非法登陆成功。

**PreparedStatement对象可以预防sql注入。**

### 2.4 PreparedStatement

#### 2.4.1 概述 

**作用**：预编译SQL语句并执行，**预防SQL注入问题。**

```java
        PreparedStatement pstmt = conn.prepareStatement("update student set age = ? where name=?"); //PreparedStatement防止sql注入
        pstmt.setInt(1,30);pstmt.setString(2,"xiaoming");
```

通过这种方式，字符串内容如果有敏感字符，则会转义成符号，从而防止sql注入问题。

-   **获取 PreparedStatement 对象**
    
    ```java
    // SQL语句中的参数值，使用？占位符替代
    String sql = "select * from user where username = ? and password = ?";
    // 通过Connection对象获取，并传入对应的sql语句
    PreparedStatement pstmt = conn.prepareStatement(sql);
    ```
    
-   **设置参数值**
    
    上面的sql语句中参数使用 ? 进行占位，在之前之前肯定要设置这些 ? 的值。
    
    > **PreparedStatement对象：**setXxx(参数1，参数2)：给 ? 赋值
    > 
    > -   Xxx：数据类型 ； 如 setInt (1，234)为设置第一个问号值为234
    >     
    > -   参数：
    >     
    >     -   参数1： ？的位置编号，从1 开始
    >         
    >     -   参数2： ？的值
    >         
    
-   **执行SQL语句**
    
    > executeUpdate(); 执行DDL语句和DML语句
    > 
    > executeQuery(); 执行DQL语句
    > 
    > **注意：**
    > 
    > -   调用这两个方法时不需要传递SQL语句，因为获取SQL语句执行对象时已经对SQL语句进行预编译了。
    >     
    

#### 2.4.2 PreparedStatement原理

> **PreparedStatement 好处：**
> 
> -   预编译SQL，性能更高
>     
> -   防止SQL注入：**将敏感字符进行转义**
>     

**PreparedStatement开启预编译功能：**

在代码中编写url时需要加上以下参数。不开启预编译的情况下，PreparedStatement对象只是解决了SQL注入漏洞。

```
useServerPrepStmts=true
```

**为什么预编译性能更高？**

MySQL服务器检查SQL和编译SQL花费的时间比执行SQL的时间还要长。如果我们只是重新设置参数，那么**检查SQL语句和编译SQL语句将不需要重复执行**。这样就提高了性能。

**PrepareStatement预编译过程：**

-   在获取PreparedStatement对象时，将sql语句发送给mysql服务器进行检查，编译（这些步骤很耗时）
    
-   执行时就不用再进行这些步骤了，速度更快
    
-   **如果sql模板一样，则只需要进行一次检查、编译**
    

![](https://i-blog.csdnimg.cn/blog_migrate/23b79a838d1ef4f3868404c3b5644145.png)

### 2.5 数据库连接池**DataSource**

#### 2.5.1 数据库连接池简介

> -   数据库连接池是个**容器**，负责分配、管理数据库连接(Connection)。
>     
> -   它允许应用程序**重复使用一个现有的数据库连接**，而不是再重新建立一个；
>     
> -   释放空闲时间超过“最大空闲时间”的数据库连接，从而避免因为没有释放数据库连接而引起的数据库连接遗漏
>     
> 
> **好处**
> 
> -   资源重用
>     
> -   提升系统响应速度
>     
> -   避免数据库连接遗漏
>     

**之前**我们代码中使用连接是没有使用都创建一个Connection对象，使用完毕就会将其销毁。这样**重复创建销毁**的过程是特别耗费计算机的性能的及消耗时间的。

而数据库使用了数据库连接池后，就能达到**Connection对象的复用**，如下图

![](https://i-blog.csdnimg.cn/blog_migrate/a06c76a3d97d1eb0ec624fef97c6658e.png)  

**连接池是在一开始就创建好了一些连接（Connection）对象存储起来。**用户需要连接数据库时，不需要自己创建连接，而只需要**从连接池中获取一个连接进行使用**，使用完毕后再将连接对象归还给连接池；这样就可以起到资源重用，也节省了频繁创建连接销毁连接所花费的时间，从而提升了系统响应的速度。

#### 2.5.2 数据库连接池实现

**标准接口：DataSource**

官方(SUN) 提供的**数据库连接池标准接口**，由第三方组织实现此接口。该接口提供了获取连接的功能：

```
Connection getConnection()
```

那么以后就不需要通过 `DriverManager` 对象获取 `Connection` 对象，而是通过**连接池**（**DataSource**）**获取 `Connection` 对象**。

**常见的数据库连接池**

我们现在使用更多的是Druid，它的性能比其他两个会好一些。

-   DBCP
    
-   C3P0
    
-   Druid
    
-   **Druid（德鲁伊）**
    
    -   Druid连接池是阿里巴巴开源的数据库连接池项目
        
    -   功能强大，性能优秀，是Java语言最好的数据库连接池之一
        

#### 2.5.3 Driud下载

下载地址：

[Central Repository: com/alibaba/druid](https://repo1.maven.org/maven2/com/alibaba/druid/ "Central Repository: com/alibaba/druid")

选择版本：

![](https://i-blog.csdnimg.cn/blog_migrate/07c66affd724d8dd75c053cf8725ab8e.png)

选择jar包：

![](https://i-blog.csdnimg.cn/blog_migrate/08095e1c92c2463e870029b326c4235b.png)

#### 2.5.4 Driud使用

> -   导入jar包 
>     
> -   定义配置文件
>     
> -   加载配置文件
>     
> -   获取数据库连接池对象
>     
> -   获取连接
>     

**导入jar包**

跟mysql的jar包类似，复制粘贴到模块目录下lib文件夹下，右键add as library，level选择module library

**定义配置文件：**

在模块下新建druid.properties，编写配置文件，前四句跟jdbc.properties一样。示例：

```bash
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql:///db1?useSSL=false&useServerPrepStmts=true
username=root
password=1234


# 初始化连接数量
initialSize=5
# 最大连接数
maxActive=10
# 最大等待时间
maxWait=3000
```

**加载配置文件：**

Properties的load方法。

获取当前路径：

```java
System.out.println(System.getProperty("user.dir"));
```

**获取数据库连接池对象：**

使用德鲁伊连接池工厂类DruidDataSourceFactory的创建连接池方法createDataSource获取连接池对象。

```java
DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
```

 **获取数据库连接 Connection：**

```java
        Connection connection = dataSource.getConnection();
        System.out.println(connection); //获取到了连接后就可以继续做其他操作了
```

**代码示例：**

```java
/**
 * Druid数据库连接池演示
 */
public class DruidDemo {

    public static void main(String[] args) throws Exception {
        //1.导入jar包
        //2.定义配置文件
        //3. 加载配置文件
        Properties prop = new Properties();
        //System.out.println(System.getProperty("user.dir")); //获取当前路径
        prop.load(new FileInputStream("jdbc-demo/src/druid.properties"));
        //4. 获取连接池对象
        DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);

        //5. 获取数据库连接 Connection
        Connection connection = dataSource.getConnection();
        //System.out.println(connection); //获取到了连接后就可以继续做其他操作了
    }
}
```

> **剧透一下**spring框架的Jdbc.config配置文件使用druid：
> 
> ```java
> public class JdbcConfig {
>     @Value("${jdbc.driver}")
>     private String driver;
>     @Value("${jdbc.url}")
>     private String url;
>     @Value("${jdbc.username}")
>     private String userName;
>     @Value("${jdbc.password}")
>     private String password;
> 
>     @Bean
>     public DataSource dataSource(){
>         DruidDataSource ds = new DruidDataSource();
>         ds.setDriverClassName(driver);
>         ds.setUrl(url);
>         ds.setUsername(userName);
>         ds.setPassword(password);
>         return ds;
>     }
> 
>     //配置事务管理器，mybatis使用的是jdbc事务
>     @Bean
>     public PlatformTransactionManager transactionManager(DataSource dataSource){
>         DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
>         transactionManager.setDataSource(dataSource);
>         return transactionManager;
>     }
> }
> ```

**对比不使用连接池**

```java
        //1. 注册驱动
        
        //Class.forName("com.mysql.jdbc.Driver");//通过反射获取Driver实现类对象，从而加载驱动，注册驱动语句DriverManager.registerDriver(driver)在Driver的静态代码块里做过了。
        //此句仅在mysql可省略，其他数据库不能省略
        //2. 获取连接
        String url = "jdbc:mysql://127.0.0.1:3306/db1?useSSL=false";
        String username = "root";
        String passWord = "1234";
        Connection conn = DriverManager.getConnection(url, username, passWord);
```

#### 2.5.5 Druid配置文件详解

<table align="left" border="2"><tbody><tr><td>&nbsp;&nbsp;配置</td><td>缺省值</td><td>说明</td></tr><tr><td>name</td><td></td><td>配置这个属性的意义在于，如果存在多个数据源，监控的时候&nbsp;<br>可以通过名字来区分开来。如果没有配置，将会生成一个名字，&nbsp;<br>格式是："DataSource-" + System.identityHashCode(this)</td></tr><tr><td>jdbcUrl</td><td></td><td>连接数据库的url，不同数据库不一样。例如：&nbsp;<br>MYSQL :&nbsp; &nbsp; jdbc:mysql://10.20.153.104:3306/druid2&nbsp;&nbsp;<br>ORACLE :&nbsp; &nbsp;jdbc:oracle:thin:@10.20.149.85:1521:ocnauto</td></tr><tr><td>username</td><td></td><td>连接数据库的用户名</td></tr><tr><td>password</td><td></td><td>连接数据库的密码。如果你不希望密码直接写在配置文件中，&nbsp;<br>可以使用ConfigFilter。详细看这里：&nbsp;<br><a href="https://github.com/alibaba/druid/wiki/%E4%BD%BF%E7%94%A8ConfigFilter" title="使用ConfigFilter · alibaba/druid Wiki · GitHub">使用ConfigFilter · alibaba/druid Wiki · GitHub</a></td></tr><tr><td>driverClassName</td><td>根据url自动识别</td><td>这一项可配可不配，如果不配置druid会根据url自动识别dbType，然后选择相应的driverClassName</td></tr><tr><td>initialSize</td><td>0</td><td>初始化时建立物理连接的个数。初始化发生在显示调用init方法，或者第一次getConnection时</td></tr><tr><td>maxActive</td><td>8</td><td>最大连接池数量</td></tr><tr><td>maxIdle</td><td>8</td><td>已经不再使用，配置了也没效果</td></tr><tr><td>minIdle</td><td></td><td>最小连接池数量</td></tr><tr><td>maxWait</td><td></td><td>获取连接时最大等待时间，单位毫秒。配置了maxWait之后，&nbsp;<br>缺省启用公平锁，并发效率会有所下降，&nbsp;<br>如果需要可以通过配置useUnfairLock属性为true使用非公平锁。</td></tr><tr><td>poolPreparedStatements</td><td>false</td><td>是否缓存preparedStatement，也就是PSCache。&nbsp;<br>PSCache对支持游标的数据库性能提升巨大，比如说oracle。&nbsp;<br>在mysql5.5以下的版本中没有PSCache功能，建议关闭掉。<br>作者在5.5版本中使用PSCache，通过监控界面发现PSCache有缓存命中率记录，&nbsp;<br>该应该是支持PSCache。</td></tr><tr><td>maxOpenPreparedStatements</td><td>-1</td><td>要启用PSCache，必须配置大于0，当大于0时，&nbsp;<br>poolPreparedStatements自动触发修改为true。&nbsp;<br>在Druid中，不会存在Oracle下PSCache占用内存过多的问题，&nbsp;<br>可以把这个数值配置大一些，比如说100</td></tr><tr><td>validationQuery</td><td></td><td>用来检测连接是否有效的sql，要求是一个查询语句。&nbsp;<br>如果validationQuery为null，testOnBorrow、testOnReturn、&nbsp;<br>testWhileIdle都不会其作用。</td></tr><tr><td>testOnBorrow</td><td>true</td><td>申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。</td></tr><tr><td>testOnReturn</td><td>false</td><td>归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能</td></tr><tr><td>testWhileIdle</td><td>false</td><td>建议配置为true，不影响性能，并且保证安全性。&nbsp;<br>申请连接的时候检测，如果空闲时间大于&nbsp;<br>timeBetweenEvictionRunsMillis，&nbsp;<br>执行validationQuery检测连接是否有效。</td></tr><tr><td>timeBetweenEvictionRunsMillis</td><td></td><td>有两个含义：&nbsp;<br>1) Destroy线程会检测连接的间隔时间&nbsp;<br>2) testWhileIdle的判断依据，详细看testWhileIdle属性的说明</td></tr><tr><td>numTestsPerEvictionRun</td><td></td><td>不再使用，一个DruidDataSource只支持一个EvictionRun</td></tr><tr><td>minEvictableIdleTimeMillis</td><td></td><td></td></tr><tr><td>connectionInitSqls</td><td></td><td>物理连接初始化的时候执行的sql</td></tr><tr><td>exceptionSorter</td><td>根据dbType自动识别</td><td>当数据库抛出一些不可恢复的异常时，抛弃连接</td></tr><tr><td>filters</td><td></td><td>属性类型是字符串，通过别名的方式配置扩展插件，&nbsp;<br>常用的插件有：&nbsp;<br>监控统计用的filter:stat&nbsp;&nbsp;<br>日志用的filter:log4j&nbsp;<br>防御sql注入的filter:wall</td></tr><tr><td>proxyFilters</td><td></td><td>类型是List&lt;com.alibaba.druid.filter.Filter&gt;，&nbsp;<br>如果同时配置了filters和proxyFilters，&nbsp;<br>是组合关系，并非替换关系</td></tr></tbody></table>

## 三、JDBC练习

#### 3.1 需求：完成商品品牌数据的增删改查操作

-   查询：查询所有数据
    
-   添加：添加品牌
    
-   修改：根据id修改
    
-   删除：根据id删除
    

#### 3.2 案例实现

环境准备

-   数据库表 `tb_brand`
    
    ```sql
    -- 删除tb_brand表
    drop table if exists tb_brand;
    -- 创建tb_brand表
    create table tb_brand (
        -- id 主键
        id int primary key auto_increment,
        -- 品牌名称
        brand_name varchar(20),
        -- 企业名称
        company_name varchar(20),
        -- 排序字段
        ordered int,
        -- 描述信息
        description varchar(100),
        -- 状态：0：禁用  1：启用
        status int
    );
    -- 添加数据
    insert into tb_brand (brand_name, company_name, ordered, description, status)
    values ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
           ('华为', '华为技术有限公司', 100, '华为致力于把数字世界带入每个人、每个家庭、每个组织，构建万物互联的智能世界', 1),
           ('小米', '小米科技有限公司', 50, 'are you ok', 1);
    ```
    
-   在pojo包下实体类 Brand
    
    ```java
    /**
     * 品牌
     * alt + 鼠标左键：整列编辑
     * 在实体类中，基本数据类型建议使用其对应的包装类型
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
    ​
        public Integer getId() {
            return id;
        }
    ​
        public void setId(Integer id) {
            this.id = id;
        }
    ​
        public String getBrandName() {
            return brandName;
        }
    ​
        public void setBrandName(String brandName) {
            this.brandName = brandName;
        }
    ​
        public String getCompanyName() {
            return companyName;
        }
    ​
        public void setCompanyName(String companyName) {
            this.companyName = companyName;
        }
    ​
        public Integer getOrdered() {
            return ordered;
        }
    ​
        public void setOrdered(Integer ordered) {
            this.ordered = ordered;
        }
    ​
        public String getDescription() {
            return description;
        }
    ​
        public void setDescription(String description) {
            this.description = description;
        }
    ​
        public Integer getStatus() {
            return status;
        }
    ​
        public void setStatus(Integer status) {
            this.status = status;
        }
    ​
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
    

**查询所有**

```java
 /**
   * 查询所有
   * 1. SQL：select * from tb_brand;
   * 2. 参数：不需要
   * 3. 结果：List<Brand>
   */
​
@Test
public void testSelectAll() throws Exception {
    //1. 获取Connection
    //3. 加载配置文件
    Properties prop = new Properties();
    prop.load(new FileInputStream("jdbc-demo/src/druid.properties"));
    //4. 获取连接池对象
    DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
​
    //5. 获取数据库连接 Connection
    Connection conn = dataSource.getConnection();
    //2. 定义SQL
    String sql = "select * from tb_brand;";
    //3. 获取pstmt对象
    PreparedStatement pstmt = conn.prepareStatement(sql);
    //4. 设置参数
    //5. 执行SQL
    ResultSet rs = pstmt.executeQuery();
    //6. 处理结果 List<Brand> 封装Brand对象，装载List集合
    Brand brand = null;
    List<Brand> brands = new ArrayList<>();
    while (rs.next()){
        //获取数据
        int id = rs.getInt("id");
        String brandName = rs.getString("brand_name");
        String companyName = rs.getString("company_name");
        int ordered = rs.getInt("ordered");
        String description = rs.getString("description");
        int status = rs.getInt("status");
        //封装Brand对象
        brand = new Brand();
        brand.setId(id);
        brand.setBrandName(brandName);
        brand.setCompanyName(companyName);
        brand.setOrdered(ordered);
        brand.setDescription(description);
        brand.setStatus(status);
​
        //装载集合
        brands.add(brand);
    }
    System.out.println(brands);
    //7. 释放资源
    rs.close();
    pstmt.close();
    conn.close();
}
```

添加数据

```java
/**
  * 添加
  * 1. SQL：insert into tb_brand(brand_name, company_name, ordered, description, status) values(?,?,?,?,?);
  * 2. 参数：需要，除了id之外的所有参数信息
  * 3. 结果：boolean
  */
@Test
public void testAdd() throws Exception {
    // 接收页面提交的参数
    String brandName = "香飘飘";
    String companyName = "香飘飘";
    int ordered = 1;
    String description = "绕地球一圈";
    int status = 1;
​
    //1. 获取Connection
    //3. 加载配置文件
    Properties prop = new Properties();
    prop.load(new FileInputStream("jdbc-demo/src/druid.properties"));
    //4. 获取连接池对象
    DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
    //5. 获取数据库连接 Connection
    Connection conn = dataSource.getConnection();
    //2. 定义SQL
    String sql = "insert into tb_brand(brand_name, company_name, ordered, description, status) values(?,?,?,?,?);";
    //3. 获取pstmt对象
    PreparedStatement pstmt = conn.prepareStatement(sql);
    //4. 设置参数
    pstmt.setString(1,brandName);
    pstmt.setString(2,companyName);
    pstmt.setInt(3,ordered);
    pstmt.setString(4,description);
    pstmt.setInt(5,status);
​
    //5. 执行SQL
    int count = pstmt.executeUpdate(); // 影响的行数
    //6. 处理结果
    System.out.println(count > 0);
​
    //7. 释放资源
    pstmt.close();
    conn.close();
}
```

**修改数据**

```java
/**
  * 修改
  * 1. SQL：
​
     update tb_brand
         set brand_name  = ?,
         company_name= ?,
         ordered     = ?,
         description = ?,
         status      = ?
     where id = ?
​
   * 2. 参数：需要，所有数据
   * 3. 结果：boolean
   */
​
@Test
public void testUpdate() throws Exception {
    // 接收页面提交的参数
    String brandName = "香飘飘";
    String companyName = "香飘飘";
    int ordered = 1000;
    String description = "绕地球三圈";
    int status = 1;
    int id = 4;
​
    //1. 获取Connection
    //3. 加载配置文件
    Properties prop = new Properties();
    prop.load(new FileInputStream("jdbc-demo/src/druid.properties"));
    //4. 获取连接池对象
    DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
    //5. 获取数据库连接 Connection
    Connection conn = dataSource.getConnection();
    //2. 定义SQL
    String sql = " update tb_brand\n" +
        "         set brand_name  = ?,\n" +
        "         company_name= ?,\n" +
        "         ordered     = ?,\n" +
        "         description = ?,\n" +
        "         status      = ?\n" +
        "     where id = ?";
​
    //3. 获取pstmt对象
    PreparedStatement pstmt = conn.prepareStatement(sql);
​
    //4. 设置参数
    pstmt.setString(1,brandName);
    pstmt.setString(2,companyName);
    pstmt.setInt(3,ordered);
    pstmt.setString(4,description);
    pstmt.setInt(5,status);
    pstmt.setInt(6,id);
​
    //5. 执行SQL
    int count = pstmt.executeUpdate(); // 影响的行数
    //6. 处理结果
    System.out.println(count > 0);
​
    //7. 释放资源
    pstmt.close();
    conn.close();
}
```

**删除数据**

```java
/**
  * 删除
  * 1. SQL：
            delete from tb_brand where id = ?
  * 2. 参数：需要，id
  * 3. 结果：boolean
  */
@Test
public void testDeleteById() throws Exception {
    // 接收页面提交的参数
    int id = 4;
    //1. 获取Connection
    //3. 加载配置文件
    Properties prop = new Properties();
    prop.load(new FileInputStream("jdbc-demo/src/druid.properties"));
    //4. 获取连接池对象
    DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
    //5. 获取数据库连接 Connection
    Connection conn = dataSource.getConnection();
    //2. 定义SQL
    String sql = " delete from tb_brand where id = ?";
    //3. 获取pstmt对象
    PreparedStatement pstmt = conn.prepareStatement(sql);
    //4. 设置参数
    pstmt.setInt(1,id);
    //5. 执行SQL
    int count = pstmt.executeUpdate(); // 影响的行数
    //6. 处理结果
    System.out.println(count > 0);
​
    //7. 释放资源
    pstmt.close();
    conn.close();
}
```