>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[一、基本区别](#%E5%9F%BA%E6%9C%AC)

[1.1 基本特性](#%E5%9F%BA%E6%9C%AC%E7%89%B9%E6%80%A7)

[1.2 Oracle和MySQL如何做技术选型？](#Oracle%E5%92%8CMySQL%E5%A6%82%E4%BD%95%E5%81%9A%E6%8A%80%E6%9C%AF%E9%80%89%E5%9E%8B%EF%BC%9F)

[1.3 RDBMS和ORDBMS的区别](#RDBMS%E5%92%8CORDBMS%E7%9A%84%E5%8C%BA%E5%88%AB)

[1.4 默认端口号和用户名](#%E9%BB%98%E8%AE%A4%E7%AB%AF%E5%8F%A3%E5%8F%B7%E5%92%8C%E7%94%A8%E6%88%B7%E5%90%8D)

[1.5 基本操作](#%E7%99%BB%E5%BD%95%E6%96%B9%E5%BC%8F)

[1.5.1 登录方式](#1.5.1%20%E7%99%BB%E5%BD%95%E6%96%B9%E5%BC%8F)

[1.5.2 修改用户名密码](#1.5.2%20%E4%BF%AE%E6%94%B9%E7%94%A8%E6%88%B7%E5%90%8D%E5%AF%86%E7%A0%81%C2%A0) 

[1.5.3 Oracle解锁账号](#1.5.3%20Oracle%E8%A7%A3%E9%94%81%E8%B4%A6%E5%8F%B7)

[1.5.4 Oracle内存优化](#1.5.4%20Oracle%E5%86%85%E5%AD%98%E4%BC%98%E5%8C%96)

[1.6 大小写是否敏感](#sql-%E8%AF%AD%E5%8F%A5)

[1.6.1 Oracle：双引号下大小写敏感](#oracle-1)

[1.6.2 MySQL：大小写不敏感](#mysql-1)

[二、常用字段类型](#%E5%B8%B8%E7%94%A8%E5%AD%97%E6%AE%B5%E7%B1%BB%E5%9E%8B)

[2.1 Oracle常用字段类型](#Oracle%E5%B8%B8%E7%94%A8%E5%AD%97%E6%AE%B5%E7%B1%BB%E5%9E%8B)

[2.2 MySQL常用字段类型](#MySQL%E5%B8%B8%E7%94%A8%E5%AD%97%E6%AE%B5%E7%B1%BB%E5%9E%8B)

[三、时间日期](#%E6%97%B6%E9%97%B4%E6%97%A5%E6%9C%9F)

[3.1 Oracle](#oracle-2)

[3.2 MySQL](#mysql-2)

[四、创建表空间/数据库](#%E5%88%9B%E5%BB%BA%E8%A1%A8%E7%A9%BA%E9%97%B4%2F%E6%95%B0%E6%8D%AE%E5%BA%93)

[4.1 Oracle创建表空间](#oracle%E5%88%9B%E5%BB%BA%E8%A1%A8%E7%A9%BA%E9%97%B4)

[4.2 MySQL创建数据库](#MySQL%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93)

[五、创建临时表](#%E5%88%9B%E5%BB%BA%E4%B8%B4%E6%97%B6%E8%A1%A8)

[5.1 Oracle创建临时表](#Oracle%E5%88%9B%E5%BB%BA%E4%B8%B4%E6%97%B6%E8%A1%A8)

[5.2 MySQL创建临时表](#MySQL%E5%88%9B%E5%BB%BA%E4%B8%B4%E6%97%B6%E8%A1%A8)

[六、删除表空间/数据库](#%E5%88%A0%E9%99%A4%E8%A1%A8%E7%A9%BA%E9%97%B4%2F%E6%95%B0%E6%8D%AE%E5%BA%93)

[6.1 Oracle删除表空间](#oracle%E5%88%A0%E9%99%A4%E8%A1%A8%E7%A9%BA%E9%97%B4)

[6.2 MySQL删除数据库](#MySQL%E5%88%A0%E9%99%A4%E6%95%B0%E6%8D%AE%E5%BA%93)

[七、数据备份恢复](#%E6%95%B0%E6%8D%AE%E5%A4%87%E4%BB%BD%E6%81%A2%E5%A4%8D)

[7.1 Oracle导入dmp文件](#oracle%E5%AF%BC%E5%85%A5dmp%E6%96%87%E4%BB%B6)

[7.2 MySQL备份迁移](#7.2%20MySQL%E5%A4%87%E4%BB%BD%E8%BF%81%E7%A7%BB)

[八、创建表和插入记录](#dml)

[8.1 Oracle创建表和插入记录](#oracle)

[8.2 MySQL创建表和插入记录](#mysql)

[九、事务提交方式](#%E4%BA%8B%E5%8A%A1%E6%8F%90%E4%BA%A4%E6%96%B9%E5%BC%8F)

[9.1 Oracle：完全支持事务，默认不自动提交](#Oracle%EF%BC%9A%E5%AE%8C%E5%85%A8%E6%94%AF%E6%8C%81%E4%BA%8B%E5%8A%A1%EF%BC%8C%E9%BB%98%E8%AE%A4%E4%B8%8D%E8%87%AA%E5%8A%A8%E6%8F%90%E4%BA%A4)

[9.2 MySQL：仅innoDB支持事务，默认自动提交](#MySQL%EF%BC%9A%E4%BB%85innoDB%E6%94%AF%E6%8C%81%E4%BA%8B%E5%8A%A1%EF%BC%8C%E9%BB%98%E8%AE%A4%E8%87%AA%E5%8A%A8%E6%8F%90%E4%BA%A4)

[十、分页](#%E5%88%86%E9%A1%B5)

[10.1 Oracle：利用rownum分类](#Oracle%EF%BC%9A%E5%88%A9%E7%94%A8rownum%E5%88%86%E7%B1%BB)

[10.2 MySQL：通过limit关键字分页](#MySQL%EF%BC%9A%E9%80%9A%E8%BF%87limit%E5%85%B3%E9%94%AE%E5%AD%97%E5%88%86%E9%A1%B5)

--

## 一、基本区别

### 1.1 基本特性

-   **数据库类型：**Oracle数据库是一个对象关系数据库管理系统（ORDBMS），MySQL是一个开源的关系数据库管理系统（RDBMS）。
    -   **对象关系 数据库管理系统：**基于对象模型，存储数据及其方法，数据存储在对象中。拥有对象类、对象标识、多态、封装和继承等特性。用于存储复杂的数据。
    -   **关系 数据库管理系统：**基于关系模型， 只存储数据，数据存储在实体里面，以包含特定信息的表格的形式存在。用于处理比较简单的数据
-   **客户规模：**Oracle主要面向大企业级级别的用户，而MySQL则更适合中小型企业和个人。根据Gartner的数据，截至2020年，Oracle占据了全球关系型数据库管理系统市场的超过40%的份额，而MySQL仅占5%。
-   **成本：**Oracle是一种专业的数据库管理系统，需要付费购买许可证。MySQL（社区版，支持基本功能）是一种免费的数据库管理系统，如果需要使用它的高级功能（如多线程复制、查询性能优化、物理备份和增量备份、安全和加密功能、管理和监控工具、官方服务等），可能需要购买许可证或商业版本（企业版）。
-   **可移植性和兼容性：**MySQL可以很容易地在各种平台上运行，并与其他许多开源软件集成。Oracle虽然也有跨平台支持，但更偏向于使用自己的技术堆栈和产品集成。 
-   **安全性：**Oracle使用了许多安全功能，如用户名，密码，配置文件，本地身份验证，外部身份验证，高级安全增强功能等。MySQL只使用三个参数来验证用户，即用户名，密码和位置。
-   **内存：**Oracle占有内存空间大（因为面对对象，并且还存储数据的方法）；MySQL占有内存空间比较小
-   **性能和扩展性：**由于MySQL的精简设计和管理方式，所以其性能通常比Oracle更高，尤其在读取和写入方面。MySQL的扩展性也相对较好，因为其社区活跃，有许多插件和工具可供选择和使用。
-   **支持并发量：**Oracle支持大并发访问量，是OLTP（联机事务处理）最好的工具；MySQL并发小，面对大访问量可以做分表分库优化。
    -   **OLTP（联机事务处理）：**表示事务性非常高的系统，一般都是高可用的在线系统，以小的事务以及小的查询为主，评估其系统的时候，一般看其每秒执行的Transaction以及Execute SQL的数量。典型的OLTP系统有电子商务系统、银行、证券等。 
-   **存储内容：**与Oracle相比，MySQL没有表空间，角色管理，快照，同义词和包以及自动存储管理。
-   **可移植性和兼容性：**MySQL可以很容易地在各种平台上运行，并与其他许多开源软件集成。Oracle虽然也有跨平台支持，但更偏向于使用自己的技术堆栈和产品集成。
-   **临时表特点：**Oracle临时表默认所有会话内可见，一旦创建就会存在，直到显式删除。可以设置临时表仅在当前会话内或事务内可见。MySQL临时表只在当前会话可见，一旦会话关闭，临时表会自动删除。

### 1.2 Oracle和MySQL如何做技术选型？

下面场景下适用于选择Oracle：

-   **对数据库有高级需求：**如果企业对数据库的高级需求较高，如存储复杂数据及其方法，要求高可用性、灾备恢复、安全性等，可以考虑用Oracle。
-   **大型企业应用：**Oracle在处理大规模、复杂的企业级应用方面表现出色。它能够处理海量的数据和高并发的访问请求，同时支持复杂的数据模型和关系。
-   **项目并发量高：**使用Oracle，它是是OLTP（联机事务处理）最好的工具。
-   **安全性要求高：**Oracle使用了许多安全功能，如用户名，密码，配置文件，本地身份验证，外部身份验证，高级安全增强功能等。像金融、银行等对安全性要求高的项目一般都选用Oracle作为数据库。
-   **高可用性和容灾需求：**Oracle提供了强大的高可用性和容灾解决方案，例如集群配置、数据复制和自动故障转移等，能够确保系统的连续性和数据的可靠性。MySQL付费版也支持，但可靠性不如Oracle。

### 1.3 RDBMS和ORDBMS的区别

| 标准 | RDBMS | OODBMS |
| --- | --- | --- |
| 缩写含义 | 关系数据库管理系统 | 面型对象数据库管理系统 |
| 数据存储方式 | 数据存储在实体里面，以包含特定信息的表格的形式存在 | 数据存储在对象中 |
| 数据复杂性 | 处理比较简单的数据 | 比 RDBMS 处理更大且更复杂的数据 |
| 分组 | 拥有公共定义的实体集合的不同实体类型 | 用类描述拥有公共的关系、行为和相似的属性的一组对象 |
| 数据处理 | RDBMS 只存储数据 | 存储数据以及方法 |
| 主要目标 | 数据独立于应用程序 | 数据封装 |
| 主键 | 主键可以明显的标识表中的对象 | 对象标识符 (object identifier, OID) 对于任何一个对象和实体都是明确且持久的 |

### 1.4 默认端口号和用户名

Oracle默认端口：1521 默认用户：system  
MySQL默认端口：3306 默认用户：root

### 1.5 基本操作

#### 1.5.1 登录方式

连接MySQL：

```sql
mysql -u root -p
-- 输入密码

-- 查询所有数据库
show databases;
-- 切换到 "test" 这个数据库
use test;
-- 查询该数据库所有表
show tables;
```

连接Oracle：

```sql
sqlplus
-- 输入用户名
-- 输入密码

-- 查询该用户的表
select TABLE_NAME from user_tables;
```

注意：Oracle 登录需要授予登录用户 session权限，建表需要分配限额

#### 1.5.2 修改用户名密码 

**MySQL修改密码：**

1\. win+r快捷键，输入cmd进入命令行：

```
cmd
```

![](https://i-blog.csdnimg.cn/blog_migrate/89b56d237bb6e0e1e1e0cfd84ff87305.png)

2.登录MySQL

```bash
mysql -u用户名 -p密码
```

3.修改MySQL的root用户密码

```bash
set password for 用户名@localhost = password('新密码')
```

示例： 

```bash
#将用户root的密码更改为hello；

set password for root@localhost = password('hello');
```

**Oracle修改密码：**

1.win+r快捷键，输入cmd进入命令行：

```
cmd
```

![](https://i-blog.csdnimg.cn/blog_migrate/89b56d237bb6e0e1e1e0cfd84ff87305.png)

2.sqlplus进入Oracle命令行：

```bash
sqlplus
```

3.输入用户名密码登录；

4.修改密码：

```bash
ALTER USER 用户名 IDENTIFIED BY 新密码;
```

**示例：**

![](https://i-blog.csdnimg.cn/blog_migrate/ab4c1886a9dec8de963d15c7d48a4c7c.png)

#### 1.5.3 Oracle解锁账号

Oracle 在多次输错密码的情况下，会锁定该账户，导致无法登录数据库。

查看被锁定的账号：

```sql
SELECT username, account_status
FROM dba_users
WHERE account_status LIKE '%LOCKED%';
```

解锁账号：

```sql
ALTER USER 用户名 ACCOUNT UNLOCK;
```

 恢复密码：

```sql
ALTER USER 用户名 IDENTIFIED BY 新密码 ACCOUNT UNLOCK;
```

> **示例：**解锁system用户：
> 
> ```sql
> -- 解锁。用户名不用引号
> ALTER USER SYSTEM ACCOUNT UNLOCK;
> -- 设置密码
> ALTER USER SYSTEM IDENTIFIED BY SYSTEM ACCOUNT UNLOCK;
> ```

#### 1.5.4 Oracle内存优化

**1.开启自动内存管理**Automatic Memory Management（AMM）

Oracle开启AMM后，会根据当前系统的内存情况动态地分配内存，直到达到指定的最大值。当系统需要更多内存时，AMM会自动减少内存使用量。

```sql
ALTER SYSTEM SET MEMORY_TARGET=2GB,SCOPE=SPFILE;

```

AMM还可以设置max\_memory\_target参数，以控制最大内存使用：

```sql
ALTER SYSTEM SET MEMORY_MAX_TARGET=3GB,SCOPE=SPFILE;
```

**2.开启自动共享内存管理**Automatic Shared Memory Management（ASMM）

ASMM会自动检测当前系统的内存使用情况，并根据需求分配和释放共享内存区域。

与AMM不同，ASMM只处理共享池、缓冲区高速缓存、Java池和辅助预留区的共享内存。

```sql
ALTER SYSTEM SET SGA_TARGET=1024M;

ALTER SYSTEM SET SGA_MAX_SIZE=2048M;
```

### 1.6 大小写是否敏感

#### 1.6.1 Oracle：双引号下大小写敏感

是Oracle大小写不敏感的前提条件是在**没有使用双引号 "" 的前提下**（表名、字段名）

```sql
CREATE TABLE "TableName"("id" number); // 如果创建表的时候是这样写的，那么就必须严格区分大小写

SELECT * FROM "TableName"; // 不仅要区分大小写而且要加双引号，以便和上面的第三种查询方式区分开
```

  
Oracle默认是大写，对字段的具体值是敏感的

#### 1.6.2 MySQL：大小写不敏感

大小写不敏感(关键字和字段名都不区分)

阿里巴巴Java开发手册，在MySQL建表规约里有：  
【强制】表名、字段名必须使用小写字母或数字 ， 禁止出现数字开头，禁止两个下划线中间只出现数字。数据库字段名的修改代价很大，因为无法进行预发布，所以字段名称需要慎重考虑

**Windows 大小写不敏感，文件名同名大小写不同会覆盖**

MySQL 在 Windows 下不区分大小写，但在 Linux 下默认是区分大小写。因此，数据库名、 表名、字段名，都不允许出现任何大写字母，避免节外生枝  
MySQL 的字段 大小写都可以查到

## 二、常用字段类型

### 2.1 Oracle常用字段类型

-   **数值：**number number(10) number(10,2)
-   **字符串：**CHAR，NCHAR，VARCHAR2和NVARCHAR2。四种字符类型都需要至少1个字节长; CHAR和NCHAR最大可以是2000个字节，NVARCHAR2和VARCHAR2的最大限制是4000个字节。
-   **日期：**date

### 2.2 MySQL常用字段类型

-   **数值：**tinyint smallint mediumint int bigint decimal
-   **字符串：**char、varchar(10) 。最大长度允许为65,535字节（CHAR最多可以为255字节，VARCHAR为65.535字节）。
-   **日期：**date time datetime timestamp year

## 三、时间日期

### 3.1 Oracle

对于常见的时间格式： "2021-02-03 16:25:48"

-   **Java中的表示方式：**
    
    ```java
     "yyyy-MM-dd HH:mm;ss"
    ```
    
-   **Oracle 中的表示方式：**
    
    ```java
    'yyyy-mm-dd hh24:mi:ss'
    ```
    

> **示例-Java：**
> 
> ```java
>         // 定义日期格式
>         String inputPattern = "yyyy-MM-dd HH:mm:ss";
>         String outputPattern = "yyyy-MM-dd HH:mm:ss";
> 
>         // 待格式化的日期字符串
>         String inputDateStr = "2021-02-03 16:25:48";
> 
>         try {
>             // 将待格式化的日期字符串解析为 Date 对象
>             SimpleDateFormat inputFormat = new SimpleDateFormat(inputPattern);
>             Date date = inputFormat.parse(inputDateStr);
> 
>             // 创建目标日期格式
>             SimpleDateFormat outputFormat = new SimpleDateFormat(outputPattern);
> 
>             // 格式化日期
>             String outputDateStr = outputFormat.format(date);
> 
>             // 打印格式化后的日期
>             System.out.println("Formatted Date: " + outputDateStr);
>         } catch (Exception e) {
>             e.printStackTrace();
>         }
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3960c837890dd26fc6172b4f86d1a5b6.png)

> 示例-Oracle：
> 
> ```sql
> SELECT TO_CHAR(date, 'yyyy-mm-dd hh24:mi:ss') AS formatted_date
> FROM your_table;
> ```

### 3.2 MySQL

```sql
-- 获取当前时间戳 
select unix_timestamp(); 
-- 1612340981

-- 获取当前日期时间
select now();
2021-02-03 16:30:22

-- 获取当前日期
select date(now());
-- 2021-02-03

-- timestamp -> datetime
select FROM_UNIXTIME(1612340981);
-- 2021-02-03 16:29:41

-- datetime -> varchar  (time与之类似：time_format(time,format))
select  DATE_FORMAT('2008-08-08 22:23:01','%Y %m %d %H %i %s');
-- 2008 08 08 22 23 01

-- varchar -> date   str_to_date(str, format)
select str_to_date('08.09.2008 08:09:30', '%m.%d.%Y %h:%i:%s'); 
-- 2008-08-09 08:09:30
```

## 四、创建表空间/数据库

### 4.1 Oracle创建表空间

sqlplus：

创建表空间

```sql
 create tablespace 表空间名称 logging datafile '路径\名称.dbf' size 2000m autoextend on next 500m maxsize 30720m extent management local;
```

> 示例： 
> 
> ```sql
> create tablespace NWZC logging datafile 'D:\javautils\oracle1\oradata\ORCL\zuigaofa.dbf' size 2000m autoextend on next 500m maxsize 30720m extent management local;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/a24354476ff4ea0b1c474edfd578e282.png)

创建用户

```sql
   create user 用户名 identified by 密码 default tablespace 表空间名;
```

  
修改用户默认表空间：  
 

```sql
alter user 用户名 default tablespace 表空间名
```

> 示例： 
> 
> ```sql
> alter database  default tablespace NWZC;
> ```

授权 

```sql
grant exp_full_database to 用户名 ;
grant imp_full_database to 用户名 ;
grant resource to 用户名 ;
grant connect to 用户名 ;
grant dba to 用户名 ;
```

> 示例：
> 
> ```sql
> grant exp_full_database to NWZC;
> grant imp_full_database to NWZC;
> grant resource to NWZC;
> grant connect to NWZC;
> grant dba to NWZC;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/57760fe2e5613f408f9b698fb70a1447.png)

### 4.2 MySQL创建数据库

```sql
-- 查询数据库
SHOW DATABASES;
-- 创建数据库
CREATE DATABASE 数据库名称;
-- 创建数据库(判断，如果不存在则创建)
CREATE DATABASE IF NOT EXISTS 数据库名称;

-- 查看当前使用的数据库
SELECT DATABASE();
-- 使用数据库
USE 数据库名称;
```

## 五、创建临时表

### 5.1 Oracle创建临时表

Oracle临时表默认所有会话内可见，一旦创建就会存在，直到显式删除。可以设置临时表仅在当前会话内或事务内可见。

```sql
CREATE GLOBAL TEMPORARY TABLE temp_table (
    id NUMBER,
    name VARCHAR2(50)
) ON COMMIT DELETE ROWS;
```

ON COMMIT DELETE ROWS指定了当事务提交时，临时表中的所有行都会被删除。这保证了当会话结束时，所有临时数据都会被清除。 

**设置临时表消失的时机：**

-   ON COMMIT DELETE ROWS ：数据行只有在当前事务中可见，也是默认值,事务提交后数据行将消失
-   ON COMMIT PRESERVE ROWS ：数据行仅在当前会话中可见

**临时表中数据的增删改查，跟普通表一致：**

```sql
Insert into tmp_gttable (id,name) values(1,'test');
Update tmp_gttable set name = 'test_update' where id = 1；
Delete from tmp_gttable where id = 1;
```

### 5.2 MySQL创建临时表

MySQL临时表只在当前会话可见，一旦会话关闭，临时表会自动删除。

```sql
CREATE TEMPORARY TABLE 表名 (字段列表);
```

示例如下：

```sql
CREATE TEMPORARY TABLE tmp_table (

id INT NOT NULL AUTO_INCREMENT,

name VARCHAR(50) NOT NULL,

PRIMARY KEY (id)

) ENGINE=InnoDB;
```

临时表创建成功后，可以使用SELECT、INSERT、UPDATE、DELETE等语句对其进行操作，与普通表的语法相同。 

## 六、删除表空间/数据库

### 6.1 Oracle删除表空间

1、删除无任何数据对象的[表空间](https://so.csdn.net/so/search?q=%E8%A1%A8%E7%A9%BA%E9%97%B4&spm=1001.2101.3001.7020 "表空间")：

```sql
drop tablespace xxx
```

2、删除有任何数据对象的表空间

```sql
drop tablespace xxx including contents and datafiles;
```

### 6.2 MySQL删除数据库

```sql
-- 删除数据库
DROP DATABASE 数据库名称;
-- 删除数据库(判断，如果存在则删除)
DROP DATABASE IF EXISTS 数据库名称;
```

## 七、数据备份恢复

### 7.1 Oracle导入dmp文件

1.首先确保dmp版本和本地oracle版本一致

2.将需要导入的dmp文件放在oracle11g的安装目录里面的`./admin/orcl/dpdump`目录下面

![](https://i-blog.csdnimg.cn/blog_migrate/bcfb778122f6fc8008b80211d86b0fc9.png)

3.右键dmp用notepad++打开，在第二行找到版本号，改成自己的oracle版本，例如我的版本是19c：

![](https://i-blog.csdnimg.cn/blog_migrate/40529a7ce2dd87c64bb22c0b36fa00f0.png)

3.sqlplus：用system账号创建用户并授权

```sql
create user ZHANGSAN identified by 1234;
grant connect , dba to ZHANGSAN ;
grant resource to ZHANGSAN ;
grant imp_full_database to ZHANGSAN ;
grant exp_full_database to ZHANGSAN ;
```

4.cmd命令行：迁移

```sql
impdp ZHANGSAN/1234 dumpfile = XXX.dmp
```

![](https://i-blog.csdnimg.cn/blog_migrate/1e7bbc18496ccc8a3451c78d2e28df23.png)

### 7.2 MySQL备份迁移

直接用navicat转储和运行SQL文件即可：

![](https://i-blog.csdnimg.cn/blog_migrate/a956f52bdb1571b43249d25e55cda276.png)

## 八、创建表和插入记录

### 8.1 Oracle创建表和插入记录

```sql
create table t_student(
    sid int primary key ,
    sname varchar2(10) not null ,
    enterdate date,
    gender char(2),
    mail unique,
    age number check (age>19 and age<30)
)
insert into t_student values(stuseq.nextval,'Test',to_date('1990-3-4','YYYY-MM-DD'),'男','1@outlook.com',20);
commit;
```

### 8.2 MySQL创建表和插入记录

```sql
create table t_student(
    sid int primary key auto_increment,
    sname varchar(1) not null ,
    enterdate date,
    gender char(1),
    age int,
    mail varchar(10) UNIQUE
)

insert into t_student values(null,'Test','1990-3-4','男',30,'2@outlook.com')
```

MySQL插入日期使用now() 或 sysdate()，可以插入多条，使用逗号隔开  
删表数据：Oracle可以省略from：delete from t\_student; (删除所有数据)

**外键约束：**Oracle是constraints,MySQL是constraint

级联操作：

-   Oracle：on delete set null 或者on delete cascade
-   MySQL: on delete set null on update CASCADE

## 九、事务提交方式

### 9.1 Oracle：**完全支持事务**，默认不自动提交

oracle默认不自动提交，需要用户手动提交，提交可以通过以下几个命令实现：

-   **BEGIN：**事务块开始的标志。事务块里的SQL语句要么全部执行成功，要么全部失败回滚。
-   COMMIT：提交事务。执行成功时，事务将被提交，并且对数据库的修改是可见的。
-   ROLLBACK：ROLLBACK用于取消尚未提交的事务，并将数据库恢复到事务开始之前的状态。当ROLLBACK语句执行成功时，事务中的所有修改都将被撤销。
-   SAVEPOINT：SAVEPOINT用于在事务中创建一个保存点，以便在事务执行过程中可以回滚到该保存点。它可以在事务中设置一个中间点，以便在需要时回滚到该点。
-   SET TRANSACTION：SET TRANSACTION用于设置事务的属性。通过该命令，可以设置事务的隔离级别、读写权限等属性。

示例：

```sql
BEGIN
    SAVEPOINT sp;
    
    -- 向学生表插入数据
    INSERT INTO student_table (student_name, student_age) VALUES ('John', 18);
    INSERT INTO student_table (student_name, student_age) VALUES ('Emma', 19);
    
    -- 向班级表插入数据
    INSERT INTO class_table (class_name, class_size) VALUES ('Class A', 30);
    INSERT INTO class_table (class_name, class_size) VALUES ('Class B', 28);
    
    COMMIT;
EXCEPTION
    WHEN OTHERS THEN
        ROLLBACK TO sp;
        RAISE;
END;
```

### 9.2 MySQL：仅innoDB支持事务，默认自动提交

查看事务提交状态

```sql
SHOW STATUS LIKE 'Innodb_trx_id'

```

关闭事务提交：

```sql
set AutoCommit = 0;
```

手动提交事务：

```sql
START TRANSACTION;        -- 开始事务
INSERT INTO student (name,age) VALUES ('Tom',18); -- 执行一些数据操作
INSERT INTO score (student_id,score) VALUES (1,90);
COMMIT;       -- 手动提交事务
```

## 十、分页

### 10.1 Oracle：利用rownum分类

```sql
-- 利用rownum。rownum从0开始
select * from
(select rownum rr,stu.* from (select * from t_student order by sid desc) stu )
where rr>=1 and rr<=5;
```

### 10.2 MySQL：通过limit关键字分页

```sql
-- 记录从0开始
-- 从第0条开始，取5条数据
select * from test2 order by sid desc  limit 0,5
```