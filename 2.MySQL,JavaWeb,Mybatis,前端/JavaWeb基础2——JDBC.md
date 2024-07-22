>  **导航：**
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})

[TOC]



# 一、JDBC

## 1.1 JDBC概述

### 1.1.1 JDBC概念

> **了解即可**，后面开发都用Mybatis框架。MyBatis是一个持久层ORM框架,底层是对JDBC的封装。
>
> JDBC是Java提供的一个**操作数据库**的API; 
>
> **全称：**( Java DataBase Connectivity ) **Java 数据库连接**

**为什么要用jdbc？**

我们开发的**同一套Java代码无法操作不同的关系型数据库**，因为每一个关系型数据库的底层实现细节都不一样。为了解决这个问题，JDBC中定义了**所有操作关系型数据库的规则（接口）**。

众所周知接口是无法直接使用的，我们需要使用接口的实现类，而这套**实现类（称之为：驱动）**就由各自的数据库厂商给出。

### 1.1.2 JDBC本质

- 官方（sun公司）定义的一套**操作所有关系型数据库的规则，即接口**
- 各个数据库厂商去实现这套接口，提供**数据库驱动jar包**
- 我们可以使用这套接口（JDBC）编程，真正执行的代码是**驱动jar包中的实现类**

### 1.1.3 JDBC好处

- 各数据库厂商使用相同的接口，Java代码不需要针对不同数据库分别开发
- **可随时替换底层数据库**，访问数据库的Java代码基本不变

以后编写操作数据库的代码只需要面向JDBC（接口），操作哪儿个关系型数据库就需要导入该数据库的驱动包，如需要操作MySQL数据库，就需要再项目中导入MySQL数据库的驱动包。如下图就是MySQL驱动包：

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\2604a4e8cccc49c186239b9b890a02fe.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 1.2 JDBC步骤

 通过Java操作数据库的流程：

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\ace0fc8cbe2a46c9acc8ca24ae177b88.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



第一步：编写Java代码

第二步：Java代码将SQL发送到MySQL服务端

第三步：MySQL服务端接收到SQL语句并执行该SQL语句

第四步：将SQL语句执行的结果返回给Java代码

### 1.2.1 标准代码

>  jdbc整个技术点**了解即可**，后面更多用Mybatis框架简化了jdbc开发，Mybatis整合spring后代码还有改变。
>
> **剧透Mybatis：**下面是Mybatis框架操作数据库代码，下一章详细讲，**现在看看就行**
>
> [JavaWeb基础3——Maven&MyBatis_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/125818307?spm=1001.2014.3001.5501)
>
> ```java
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
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```bash
#jdbc.properties
username=root
password=1234
url=jdbc:mysql://127.0.0.1:3306/db1
driverClass=com.mysql.jdbc.Driver
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 1.2.2 编写代码步骤

**0.导入驱动jar包**。

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\2604a4e8cccc49c186239b9b890a02fe.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**为什么要导包？**

因为jdbc本质是关系型数据库接口，需要导入数据库的实现类的包才能连接数据库。

**方法**：将mysql的驱动包放在模块下的lib目录（随意命名）下，右键add as library，也就是将该jar包添加为库文件，选择模块有效，name为空就行。

**地址**：[MySQL :: Download Connector/J](https://dev.mysql.com/downloads/connector/j/)，选择**Platform Independent。**

在添加为库文件的时候，有如下三个选项

Global Library ： 全局有效

Project Library : 项目有效

Module Library ： 模块有效

**1.加载并注册驱动**

```java
Class.forName("com.mysql.jdbc.Driver");    //把mysql的驱动类Driver的对象加载进内存并初始化
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**驱动类Driver 的方法：**

- - | `static 类<?>` | `forName(String className)` 				返回与给定字符串名称的类或接口相关联的 `类`对象。 |
    | -------------- | ------------------------------------------------------------ |
    |                |                                                              |

> JDBC中定义了所有操作关系型数据库的规则（接口），**驱动类就是这些接口的实现类。** 

 **Class.forName 方法的作用**：初始化驱动类。

**MySQL中此行代码可以省略：** 

而我们给定的 MySQL 的 Driver 类中，它在**静态代码块**中通过 JDBC 的 DriverManager 注册了一下驱动。我们也可以直接使用 JDBC 的驱动管理器DriverManager 注册 mysql 驱动，从而代替使用 Class.forName。

```java
DriverManager.registerDriver(new Driver());
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2.获取连接**（获取java与mysql服务端之间的连接）

```
Connection conn = DriverManager.getConnection(url, username, password);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

驱动管理器类DriverManager的方法：

- - | `static Connection` | `getConnection(String url, String user, String password)` 				尝试建立与给定数据库URL的连接。 |
    | ------------------- | ------------------------------------------------------------ |
    |                     |                                                              |



Java代码需要发送SQL给MySQL服务端，就需要先建立连接

**3.定义SQL语句**

```java
String sql =  “update…” ;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**4.获取执行SQL对象**

执行SQL语句需要SQL执行对象，而这个执行对象就是Statement对象

```java
Statement stmt = conn.createStatement();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**5.执行SQL**（把SQL语句发送到mysql服务器，mysql服务器执行SQL语句）

```java
stmt.executeUpdate(sql);  
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

6.java处理返回结果

7.释放资源

## 1.3 获取数据库连接的多种方式

- - | `Connection` | `connect(String url, Properties info)` 				尝试使数据库连接到给定的URL。 |
    | ------------ | ------------------------------------------------------------ |
    |              |                                                              |

**方法一：**通过Driver对象获取： 

```java
        Driver driver=new com.mysql.jdbc.Driver();  //多态语句，driver是Driver接口对象，com.mysql.jdbc.Driver()是mysql的实现类
        String url="jdbc:mysql://127.0.0.1:3306/db1";   //jdbc是主协议，mysql是子协议，主协议:子协议://ip地址:端口/数据库名
        Properties info=new Properties();
        info.setProperty("user","root");
        info.setProperty("password","1234");
        Connection conn=driver.connect(url,info);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**方法三：**DriverManager替代Driver

DriverManager方法：

- - | `static void`       | `registerDriver(Driver driver)` 				注册与给定的驱动程序 `DriverManager` 。 |
    | ------------------- | ------------------------------------------------------------ |
    | `static Connection` | `getConnection(String url, String user, String password)` 				尝试建立与给定数据库URL的连接。 |

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\f522b814179d471184aeae5fa4cbc854.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\e3f20b83302a4f248178fac856a8580f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **方法五：**

src下新建jdbc.properties:

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\ec16e3bf80ca470384034bf9c0090f92.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\c1b293421abe4aeeb9d3afac6195cfe8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 二、JDBC所有API

## 2.1 驱动管理类 DriverManager

**作用**：注册驱动和获取数据库连接

**注册驱动方法：**

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\fd99525650cd48f0afff1fbaaf885acf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 而在实际连接数据库的时候并不需要registerDriver，因为mysql的**Driver实现类**里有**静态代码块**已经registerDriver过了：

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\e261d4ac2ba84470a577ffcf05d1fb04.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 因此我们只需要加载 `Driver` 类进内存，该静态代码块就会执行：

```java
// 将类Driver加载到内存，在内存会产生一个和类Driver对应的Class实例
Class class = Class.forName("com.mysql.jdbc.Driver");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **提示：**mysql加载Driver类方法可以省略
>
> - MySQL 5之后的驱动包，可以省略注册驱动的步骤
> - 自动加载jar包中META-INF/services/java.sql.Driver文件中的驱动类

DriverManager类，**获取数据库连接**方法：

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\8fd2de2680194107bc89c4d88969b2f7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **url** ： 连接路径
>
> **语法：**主协议jdbc:子协议mysql://ip地址(域名):端口号/数据库名称?参数键值对1&参数键值对2…
>
> **示例：**jdbc:mysql://127.0.0.1:3306/db1
>
> jdbc:mysql://localhost:3306/db1
>
> 
>
> **细节**：
>
> - **url简写依据：**如果连接的是本机mysql服务器，并且mysql服务默认端口是3306，则url可以**简写**为：jdbc:mysql:///数据库名称?参数键值对，示例：jdbc:mysql:///db1?useSSL=false
> - 配置 **useSSL=false** 参数，禁用安全连接方式，解决警告提示，示例：jdbc:mysql://127.0.0.1:3306/db1?useSSL=false

## 2.2 数据库连接对象Connection

```java
        //4. 获取执行sql的对象 Statement

        Statement stmt = conn.createStatement();
        //Statement对象：用于执行静态SQL语句并返回其生成的结果的对象。 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**Connection（数据库连接对象）作用：**

- 获取执行 SQL 的对象
- 管理事务

### 2.2.1 获取执行对象

- **普通执行SQL对象**

  ```java
  Statement createStatement()   
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  标准代码中就是通过该方法获取的执行对象。

- **预编译SQL的执行SQL对象：防止SQL注入**

  ```
  PreparedStatement  prepareStatement(sql)
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  通过这种方式获取的 `PreparedStatement` SQL语句执行对象是我们一会重点要进行讲解的，它可以防止SQL注入。

- 执行存储过程的对象

  ```
  CallableStatement prepareCall(sql)
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  通过这种方式获取的 `CallableStatement` 执行对象是用来执行存储过程的，而存储过程在MySQL中不常用，所以这个我们将不进行讲解。



### 2.2.2 事务管理

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\76a5546f5b4b4e579d8467a55789c324.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



先回顾一下MySQL事务管理的操作：

- 开启事务 ： BEGIN; 或者 START TRANSACTION;
- 提交事务 ： COMMIT;
- 回滚事务 ： ROLLBACK;

> **MySQL默认是自动提交事务**
>
> 
>
> 也可以通过下面语句查询默认提交方式：
>
> ```sql
> SELECT @@autocommit;
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 查询到的结果是1 则表示自动提交，结果是0表示手动提交。当然也可以通过下面语句修改提交方式
>
> ```sql
> set @@autocommit = 0;
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

接下来学习JDBC事务管理的方法。

**Connection几口中定义了3个对应的方法：**

**开启事务**

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\a8bb75b91c5a48948bb06088882f1ae1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





参与autoCommit 表示是否自动提交事务，true表示自动提交事务，false表示手动提交事务。而开启事务需要将该参数设为为false。

**提交事务**

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\79cd5aea086946ba9131c76e1a1d2f9e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**回滚事务**

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\9a7064f7a71c46e78392dea65889547a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)







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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.3 Statement

 Statement对象的**作用**就是用来**执行SQL语句**。

```
        String sql = "update student set age = 222 where name='xiaohua'";
        //4. 获取执行sql的对象 Statement
        Statement stmt = conn.createStatement();
        //5. 执行sql
        int count = stmt.executeUpdate(sql);//受影响的行数
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - 以后开发很少使用java代码操作DDL语句

**执行DDL、DML语句**

 ![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\5b1259dd3b434538a7ace52709714309.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**DDL：**show,create,use,select,drop,alter

**DML：**insert,update,delete

 **执行DQL语句**

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\e2f15301ba294c86a9f8f272fd8e65aa.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **DQL:**select,from,where,group by,having,order by,limit

### 2.3.1 结果集对象 ResultSet



**作用：**封装了SQL查询语句的结果，执行了DQL语句后就会返回该对象。

**回顾Statement执行DQL语句的方法，返回值就是ResultSet对象：**

```java
ResultSet  executeQuery(sql)：执行DQL 语句，返回 ResultSet 对象
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**方法：**

> boolean next()
>
> - 将光标从当前位置向下移动一行，并判断当前行是否为有效行
>
> 方法返回值说明：
>
> - true ： 有效行，当前行有数据
> - false ： 无效行，当前行没有数据

> xxx getXxx(参数)：获取数据
>
> - xxx : 数据类型；如： int getInt(参数) ；String getString(参数)
> - 参数
>   - int类型的参数：列的编号，从1开始
>   - String类型的参数： 列的名称

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.3.2 SQL注入问题

SQL注入是通过操作输入来**修改事先定义好的SQL语句**，用以达到执行代码**对服务器进行攻击**的方法。

**SQL注入问题模拟：**

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\26556e7551f2428cb0086035a885601d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



这样只需要输入框写入'1' = '1就可以令拼接后sql语句条件判断为true，从而获取到所有用户信息。

**详细解释：**上面代码是将用户名和密码拼接到sql语句中，拼接后的sql语句如下

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\aaf8fc5802314a9a9693faef259310a7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



从上面语句可以看出条件![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\0f878c074895420d9d02a2b3644358c4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)不管是否满足， `or` 后面的 `'1' = '1'` 都是始终满足的，最终条件是成立的，就可以非法登陆成功。



**PreparedStatement对象可以预防sql注入。**

## 2.4 PreparedStatement

### 2.4.1 概述 

**作用**：预编译SQL语句并执行，**预防SQL注入问题。**

```java
        PreparedStatement pstmt = conn.prepareStatement("update student set age = ? where name=?"); //PreparedStatement防止sql注入
        pstmt.setInt(1,30);pstmt.setString(2,"xiaoming");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



通过这种方式，字符串内容如果有敏感字符，则会转义成符号，从而防止sql注入问题。

- **获取 PreparedStatement 对象**

  ```java
  // SQL语句中的参数值，使用？占位符替代
  String sql = "select * from user where username = ? and password = ?";
  // 通过Connection对象获取，并传入对应的sql语句
  PreparedStatement pstmt = conn.prepareStatement(sql);
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **设置参数值**

  上面的sql语句中参数使用 ? 进行占位，在之前之前肯定要设置这些 ? 的值。

  > **PreparedStatement对象：**setXxx(参数1，参数2)：给 ? 赋值
  >
  > - Xxx：数据类型 ； 如 setInt (1，234)为设置第一个问号值为234
  > - 参数：
  >   - 参数1： ？的位置编号，从1 开始
  >   - 参数2： ？的值

- **执行SQL语句**

  > executeUpdate(); 执行DDL语句和DML语句
  >
  > executeQuery(); 执行DQL语句
  >
  > **注意：**
  >
  > - 调用这两个方法时不需要传递SQL语句，因为获取SQL语句执行对象时已经对SQL语句进行预编译了。

### 2.4.2 PreparedStatement原理

> **PreparedStatement 好处：**
>
> - 预编译SQL，性能更高
> - 防止SQL注入：**将敏感字符进行转义**

**PreparedStatement开启预编译功能：**

在代码中编写url时需要加上以下参数。不开启预编译的情况下，PreparedStatement对象只是解决了SQL注入漏洞。

```
useServerPrepStmts=true
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**为什么预编译性能更高？**

MySQL服务器检查SQL和编译SQL花费的时间比执行SQL的时间还要长。如果我们只是重新设置参数，那么**检查SQL语句和编译SQL语句将不需要重复执行**。这样就提高了性能。

**PrepareStatement预编译过程：**

- 在获取PreparedStatement对象时，将sql语句发送给mysql服务器进行检查，编译（这些步骤很耗时）
- 执行时就不用再进行这些步骤了，速度更快
- **如果sql模板一样，则只需要进行一次检查、编译**

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\55589ab8185644288d6da8ffbed5a59e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.5 数据库连接池**DataSource**

### 2.5.1 数据库连接池简介

> - 数据库连接池是个**容器**，负责分配、管理数据库连接(Connection)。
> - 它允许应用程序**重复使用一个现有的数据库连接**，而不是再重新建立一个；
> - 释放空闲时间超过“最大空闲时间”的数据库连接，从而避免因为没有释放数据库连接而引起的数据库连接遗漏
>
> **好处**
>
> - 资源重用
> - 提升系统响应速度
> - 避免数据库连接遗漏

**之前**我们代码中使用连接是没有使用都创建一个Connection对象，使用完毕就会将其销毁。这样**重复创建销毁**的过程是特别耗费计算机的性能的及消耗时间的。

而数据库使用了数据库连接池后，就能达到**Connection对象的复用**，如下图

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\df205f0ee86245b5bb40ffbc54ce8fc5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 



**连接池是在一开始就创建好了一些连接（Connection）对象存储起来。**用户需要连接数据库时，不需要自己创建连接，而只需要**从连接池中获取一个连接进行使用**，使用完毕后再将连接对象归还给连接池；这样就可以起到资源重用，也节省了频繁创建连接销毁连接所花费的时间，从而提升了系统响应的速度。

### 2.5.2 数据库连接池实现

**标准接口：DataSource**

官方(SUN) 提供的**数据库连接池标准接口**，由第三方组织实现此接口。该接口提供了获取连接的功能：

```
Connection getConnection()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

那么以后就不需要通过 `DriverManager` 对象获取 `Connection` 对象，而是通过**连接池**（**DataSource**）**获取 `Connection` 对象**。

**常见的数据库连接池**

我们现在使用更多的是Druid，它的性能比其他两个会好一些。

- DBCP
- C3P0
- Druid
- **Druid（德鲁伊）**
  - Druid连接池是阿里巴巴开源的数据库连接池项目
  - 功能强大，性能优秀，是Java语言最好的数据库连接池之一



### 2.5.3 Driud下载

下载地址：

[Central Repository: com/alibaba/druid](https://repo1.maven.org/maven2/com/alibaba/druid/)

选择版本：

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\b4fd3746b1d74220a7295d9c540abd3a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

选择jar包：

![img](D:\workspace\my-workspace\JavaJourney\MySQL,JavaWeb,Mybatis,前端\JavaWeb基础2——JDBC.assets\9046356da4dc410ab40b7728df0995fa.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.5.4 Driud使用

> - 导入jar包 
> - 定义配置文件
> - 加载配置文件
> - 获取数据库连接池对象
> - 获取连接

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**加载配置文件：**

Properties的load方法。

获取当前路径：

```java
System.out.println(System.getProperty("user.dir"));
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**获取数据库连接池对象：**

使用德鲁伊连接池工厂类DruidDataSourceFactory的创建连接池方法createDataSource获取连接池对象。

```java
DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **获取数据库连接 Connection：**

```java
        Connection connection = dataSource.getConnection();
        System.out.println(connection); //获取到了连接后就可以继续做其他操作了
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.5.5 Druid配置文件详解



| 配置                          | 缺省值             | 说明                                                         |
| ----------------------------- | ------------------ | ------------------------------------------------------------ |
| name                          |                    | 配置这个属性的意义在于，如果存在多个数据源，监控的时候   		可以通过名字来区分开来。如果没有配置，将会生成一个名字，   		格式是："DataSource-" + System.identityHashCode(this) |
| jdbcUrl                       |                    | 连接数据库的url，不同数据库不一样。例如：   		MYSQL :  jdbc:mysql://10.20.153.104:3306/druid2   		ORACLE :  jdbc:oracle:thin:@10.20.149.85:1521:ocnauto |
| username                      |                    | 连接数据库的用户名                                           |
| password                      |                    | 连接数据库的密码。如果你不希望密码直接写在配置文件中，   		可以使用ConfigFilter。详细看这里：   		[使用ConfigFilter · alibaba/druid Wiki · GitHub](https://github.com/alibaba/druid/wiki/使用ConfigFilter) |
| driverClassName               | 根据url自动识别    | 这一项可配可不配，如果不配置druid会根据url自动识别dbType，然后选择相应的driverClassName |
| initialSize                   | 0                  | 初始化时建立物理连接的个数。初始化发生在显示调用init方法，或者第一次getConnection时 |
| maxActive                     | 8                  | 最大连接池数量                                               |
| maxIdle                       | 8                  | 已经不再使用，配置了也没效果                                 |
| minIdle                       |                    | 最小连接池数量                                               |
| maxWait                       |                    | 获取连接时最大等待时间，单位毫秒。配置了maxWait之后，   		缺省启用公平锁，并发效率会有所下降，   		如果需要可以通过配置useUnfairLock属性为true使用非公平锁。 |
| poolPreparedStatements        | false              | 是否缓存preparedStatement，也就是PSCache。   		PSCache对支持游标的数据库性能提升巨大，比如说oracle。   		在mysql5.5以下的版本中没有PSCache功能，建议关闭掉。  		作者在5.5版本中使用PSCache，通过监控界面发现PSCache有缓存命中率记录，   		该应该是支持PSCache。 |
| maxOpenPreparedStatements     | -1                 | 要启用PSCache，必须配置大于0，当大于0时，   		poolPreparedStatements自动触发修改为true。   		在Druid中，不会存在Oracle下PSCache占用内存过多的问题，   		可以把这个数值配置大一些，比如说100 |
| validationQuery               |                    | 用来检测连接是否有效的sql，要求是一个查询语句。   		如果validationQuery为null，testOnBorrow、testOnReturn、   		testWhileIdle都不会其作用。 |
| testOnBorrow                  | true               | 申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。 |
| testOnReturn                  | false              | 归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能 |
| testWhileIdle                 | false              | 建议配置为true，不影响性能，并且保证安全性。   		申请连接的时候检测，如果空闲时间大于   		timeBetweenEvictionRunsMillis，   		执行validationQuery检测连接是否有效。 |
| timeBetweenEvictionRunsMillis |                    | 有两个含义：   		1) Destroy线程会检测连接的间隔时间   		2) testWhileIdle的判断依据，详细看testWhileIdle属性的说明 |
| numTestsPerEvictionRun        |                    | 不再使用，一个DruidDataSource只支持一个EvictionRun           |
| minEvictableIdleTimeMillis    |                    |                                                              |
| connectionInitSqls            |                    | 物理连接初始化的时候执行的sql                                |
| exceptionSorter               | 根据dbType自动识别 | 当数据库抛出一些不可恢复的异常时，抛弃连接                   |
| filters                       |                    | 属性类型是字符串，通过别名的方式配置扩展插件，   		常用的插件有：   		监控统计用的filter:stat   		日志用的filter:log4j   		防御sql注入的filter:wall |
| proxyFilters                  |                    | 类型是List<com.alibaba.druid.filter.Filter>，   		如果同时配置了filters和proxyFilters，   		是组合关系，并非替换关系 |





























































































# 三、JDBC练习

### 3.1 需求：完成商品品牌数据的增删改查操作

- 查询：查询所有数据
- 添加：添加品牌
- 修改：根据id修改
- 删除：根据id删除

### 3.2 案例实现

环境准备

- 数据库表 `tb_brand`

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

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 在pojo包下实体类 Brand

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

  

**查询所有**

```java
 /**
   * 查询所有
   * 1. SQL：select * from tb_brand;
   * 2. 参数：不需要
   * 3. 结果：List<Brand>
   */

@Test
public void testSelectAll() throws Exception {
    //1. 获取Connection
    //3. 加载配置文件
    Properties prop = new Properties();
    prop.load(new FileInputStream("jdbc-demo/src/druid.properties"));
    //4. 获取连接池对象
    DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

    //5. 执行SQL
    int count = pstmt.executeUpdate(); // 影响的行数
    //6. 处理结果
    System.out.println(count > 0);

    //7. 释放资源
    pstmt.close();
    conn.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**修改数据**

```java
/**
  * 修改
  * 1. SQL：

     update tb_brand
         set brand_name  = ?,
         company_name= ?,
         ordered     = ?,
         description = ?,
         status      = ?
     where id = ?

   * 2. 参数：需要，所有数据
   * 3. 结果：boolean
   */

@Test
public void testUpdate() throws Exception {
    // 接收页面提交的参数
    String brandName = "香飘飘";
    String companyName = "香飘飘";
    int ordered = 1000;
    String description = "绕地球三圈";
    int status = 1;
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
    String sql = " update tb_brand\n" +
        "         set brand_name  = ?,\n" +
        "         company_name= ?,\n" +
        "         ordered     = ?,\n" +
        "         description = ?,\n" +
        "         status      = ?\n" +
        "     where id = ?";

    //3. 获取pstmt对象
    PreparedStatement pstmt = conn.prepareStatement(sql);

    //4. 设置参数
    pstmt.setString(1,brandName);
    pstmt.setString(2,companyName);
    pstmt.setInt(3,ordered);
    pstmt.setString(4,description);
    pstmt.setInt(5,status);
    pstmt.setInt(6,id);

    //5. 执行SQL
    int count = pstmt.executeUpdate(); // 影响的行数
    //6. 处理结果
    System.out.println(count > 0);

    //7. 释放资源
    pstmt.close();
    conn.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

    //7. 释放资源
    pstmt.close();
    conn.close();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)