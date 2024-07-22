>  **导航：**
>
> [【Java笔记+踩坑汇总】JavaSE+JavaWeb+SSM+SpringBoot+瑞吉外卖+SpringCloud/SpringCloudAlibaba+黑马旅游+谷粒商城](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})

[TOC]



# 一、概念

![img](JavaWeb基础1——MySQL.assets\3fafbaaee1204e73a9d8559b5b52e05b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**常用关系型数据库管理系统：** 

![img](JavaWeb基础1——MySQL.assets\18d0337f064b4f23a2247ce4d5cdad64.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 二、MySQL下载安装配置

**第一步：去官网下载安装**

[MySQL :: Download MySQL Community Server (Archived Versions)](https://downloads.mysql.com/archives/community/)
 ![img](JavaWeb基础1——MySQL.assets\5b91c4e6af7d4d54adde1647de055cd6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​

**第二步：配置**

先解压，然后在mysql下创建一个**my.ini**文件，更改my.ini文件里面的前两行安装目录，第二行加上\data。注意my.ini文件不能多一个符号或者少一个符号，第二行第三行改成自己的MySQL路径

![img](JavaWeb基础1——MySQL.assets\07ad376c8be446b4b8ea620694031b09.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```bash
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
# basedir=D:\\mysql\\mysql-8.0.26-winx64
basedir=D:\\ajavautils\\mysql-5.7.41-winx64 # 切记此处要么双斜杠\\，要么单斜杠/，单斜杠\会出错
# 设置mysql数据库的数据的存放目录，MySQL 8+ 可以不需要以下配置，系统自己生成即可，否则有可能报错
datadir=D:\\ajavautils\\mysql-5.7.41-winx64\\data # 此处同上
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在path（**环境变量**里面）加上mysql的bin路径（D:\ajavautils\mysql-5.7.41-winx64\bin）
 (填写自己的mysql安装路径)

![img](JavaWeb基础1——MySQL.assets\5be048935d8c4f5190eae32f95b1659f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
 ![img](JavaWeb基础1——MySQL.assets\3086dbd9261c4aa396ec17df84e82073.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​

**第三步：初始化**

进入命令指示符（在bin目录下运行cmd）

![img](JavaWeb基础1——MySQL.assets\4835b494c8864e0ba541a5badbdcebb3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
 输入下面命令初始化数据库，并设置默认root为空，初始化完成后，在mysql根目录中会自动生成data文件

```bash
# 设置数据目录和创建系统数据库和表。
# initialize-insecure指示 MySQL 初始化数据目录，但不会设置 root 用户的密码。这意味着初始化后的数据库实例将没有 root 密码，用户可以直接连接到 MySQL 服务器并设置密码。
mysqld --initialize-insecure --user=mysql
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)


 再输入mysqld -install,为windows安装mysql服务，默认服务名为mysql

```
mysqld -install
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)


 出现service successfully installed.表示配置完成
 ![img](JavaWeb基础1——MySQL.assets\6210716990fb43a291743fd1737701b4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​

**第四步：启动数据库**

```
net start mysql
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **解决发生系统错误 2。系统找不到指定的文件**
>
> 如果报错“发生系统错误 2。系统找不到指定的文件。”，则以下方法解决：
>
> ![img](JavaWeb基础1——MySQL.assets\c5cefc7a82a042039c67b7aa0563ee2b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 1. Win+R输入regedit打开注册表
> 2. HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MySQL 在该路径下找到MySQL映像文件ImagePath。
> 3. 查看ImagePath里面本地安装MySQL的路径是否有误，如果有误修改相应的路径即可。
>
> ![img](JavaWeb基础1——MySQL.assets\6c6b67b8ed034dbd8d4b1c614de6d72e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**第五步：初始化密码**

输入mysql -u root -p进行登录 。

> **命令解读：**
>
> - mysql是安装目录bin下的mysql.exe与服务mysql间进行通信
> - -u后跟账户名root
> - -p后先不设置密码

```
mysql -u root -p
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

不用输入密码直接回车 

![img](JavaWeb基础1——MySQL.assets\027bd0c850ef464eba2efa83ad3e7884.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
 出现mysql>配置完成
 **修改密码：**

```bash
alter user user() identified by "你要设置的密码，例如1234";
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\889bf78ec1d94b8087a4d66466d4b1a2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
 mysql退出 mysql>quit;

```
exit;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **其他命令（慎用）：**
>
>  **关闭数据库**
>
> ```
> net stop mysql
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> ![img](JavaWeb基础1——MySQL.assets\0bcce6c060b24cadbfa4aa0b99d7f7ea.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> **卸载**
>
> cmd先停止服务
>
> ```
> net stop mysql
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 再卸载服务
>
> ```
> mysqld -remove mysql
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 最后删除目录和环境变量



# 三、关系型数据库

![img](JavaWeb基础1——MySQL.assets\71d13a2f344d48688b48a88a2901fcbe.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

例如下面关系模型的二维表： 

![img](JavaWeb基础1——MySQL.assets\9c14c94f0a54428685fafd9d2534a0d4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

数据库在mysql的data目录下。 

# 四、SQL语句

## 4.1 概述

 ![img](JavaWeb基础1——MySQL.assets\34a5f6704fe64e5b88b24de5c20287f8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](JavaWeb基础1——MySQL.assets\1eac223a7dd44da994c9b74d920529b9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 注意单行注释--后有空格。

![img](JavaWeb基础1——MySQL.assets\f037bed50bf4422a93ce6814a30499a4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](JavaWeb基础1——MySQL.assets\c822a978c3704ae596c430a2fe084338.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 4.2 DDL数据定义语言

### 4.2.0 mysql自带数据库

![img](JavaWeb基础1——MySQL.assets\53afd00277fa4989bcbe24fe4b65aaa1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**information_schema 是信息数据库。**

其中保存着关于MySQL服务器所维护的所有其他数据库的信息。如数据库名，数据库的表，表栏的数据类型与访问权 限等。在INFORMATION_SCHEMA中，有数个只读表。它们实际上是视图，而不是基本表，因此，你将无法看到与之相关的任何文件。

**mysql核心数据库**，存储MySQL数据库里最核心的信息，例如权限、安全。

**sys：系统数据库。**

**performance_schema**主要用于收集数据库服务器性能参数（研究性能调优要用到）

### 4.2.1 数据库的增删查、使用

![img](JavaWeb基础1——MySQL.assets\d7f8ecad8ca248c1932f5d8bdfb905c1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.2.2 DDL查询表



**查询当前数据库下所有表名称**

```
SHOW TABLES;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**查询表结构**

```sql
DESC 表名称;        #desc是describe缩写，译为描述
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.2.3 DDL创建表

```
CREATE TABLE 表名 (
	字段名1  数据类型1,
	字段名2  数据类型2,
	…
	字段名n  数据类型n
);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  注意：字段名是列名。
>
> 最后一行末尾，不能加逗号

```
create table tb_user (
	id int,
    username varchar(20),    #sql语句中字符串是char和varchar类型
    password varchar(32)
);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\7557f33b994e4652ac6a80d2e6cf9696.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 4.2.4 三类数据类型，数值、日期、字符串



- **数值**

  ```
  tinyint : 小整数型，占一个字节
  int ： 大整数类型，占四个字节
      eg ： age int
  double ： 浮点类型
      使用格式： 字段名 double(总长度,小数点后保留的位数)
      eg ： score double(5,2)   
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **日期**

  ```bash
  date ： 日期值要带引号。只包含年月日
      eg ：birthday date 
  time :  时间值或持续时间
  year :  年分值
  datetime ： 混合日期和时间值。包含年月日时分秒
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **字符串。要带引号**

  ```bash
  char ： 定长字符串。
      优点：存储性能高
      缺点：浪费空间
      eg ： name char(10)  如果存储的数据字符个数不足10个，也会占10个的空间，汉字占1个字符
  varchar ： 变长字符串。
      优点：节约空间
      缺点：存储性能底
      eg ： name varchar(10) 如果存储的数据字符个数不足10个，那就数据字符个数是几就占几个的空间    
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

### 4.2.5 DDL删除表

- **删除表**

```
DROP TABLE 表名;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **删除表时判断表是否存在**

```
DROP TABLE IF EXISTS 表名;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.2.6 DDL修改表

关键字rename，add，modify，change，drop

- **修改表名**

```
ALTER TABLE 表名 RENAME TO 新的表名;

-- 将表名student修改为stu
alter table student rename to stu;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **添加一列**

```
ALTER TABLE 表名 ADD 列名 数据类型;

-- 给stu表添加一列address，该字段类型是varchar(50)
alter table stu add address varchar(50);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **修改数据类型**

```
ALTER TABLE 表名 MODIFY 列名 新数据类型;

-- 将stu表中的address字段的类型改为 char(50)
alter table stu modify address char(50);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **修改列名和数据类型**

```
ALTER TABLE 表名 CHANGE 列名 新列名 新数据类型;

-- 将stu表中的address字段名改为 addr，类型改为varchar(50)
alter table stu change address addr varchar(50);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **删除列**

```
ALTER TABLE 表名 DROP 列名;

-- 将stu表中的addr字段 删除
alter table stu drop addr;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **删除外键约束**

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 4.3 Navicat下载安装使用

下载地址：

```bash
https://wwo.lanzouj.com/b00jddp8za
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

密码:fx4h

注意注册时要管理员运行和断网，版本必须是我这个版本的16，最新的版本只能购买。

主机那里填localhost或127.0.0.1，端口3306。

可以通过“美化sql”格式化代码：

![img](JavaWeb基础1——MySQL.assets\06681c1bbee746a8a19b9bc1cca47d5a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\d245f2378e234c1393fd5a85ab34b628.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\ac4b66f7fc164233af4617ce940a7813.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## **4.4 数据操作语言DML**

### 4.4.1 DML添加数据

- **给指定列添加数据**

```sql
INSERT INTO 表名(列名1,列名2,…) VALUES(值1,值2,…);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **给全部列添加数据**

```sql
INSERT INTO 表名 VALUES(值1,值2,…);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **批量添加数据**

```sql
INSERT INTO 表名(列名1,列名2,…) VALUES(值1,值2,…),(值1,值2,…),(值1,值2,…)…;
INSERT INTO 表名 VALUES(值1,值2,…),(值1,值2,…),(值1,值2,…)…;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 注意添加字符串时候要加引号

```sql
-- 给指定列添加数据
INSERT INTO stu (id, NAME) VALUES (1, '张三');
-- 给所有列添加数据，列名的列表可以省略的
INSERT INTO stu (id,NAME,sex,birthday,score,email,tel,STATUS) VALUES (2,'李四','男','1999-11-11',88.88,'lisi@itcast.cn','13888888888',1);

INSERT INTO stu VALUES (2,'李四','男','1999-11-11',88.88,'lisi@itcast.cn','13888888888',1);

-- 批量添加数据
INSERT INTO stu VALUES 
	(2,'李四','男','1999-11-11',88.88,'lisi@itcast.cn','13888888888',1),
	(2,'李四','男','1999-11-11',88.88,'lisi@itcast.cn','13888888888',1),
	(2,'李四','男','1999-11-11',88.88,'lisi@itcast.cn','13888888888',1);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 4.4.2 修改数据



```sql
UPDATE 表名 SET 列名1=值1,列名2=值2,… [WHERE 条件] ;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> 1. 修改语句中如果不加条件，则将所有记录都修改！
> 2. 像上面的语句中的中括号，表示在写sql语句中可以省略这部分

```sql
update stu set sex = '女' where name = '张三';
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.4.3 删除数据

- **删除数据**

```sql
DELETE FROM 表名 [WHERE 条件] ;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **练习**

```sql
-- 删除张三记录
delete from stu where name = '张三';

-- 删除stu表中所有的数据
delete from stu;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> 1. 和上面一样，删除语句中如果不加条件，所有记录都将被删除，慎重！
> 2. 中括号，表示在写sql语句中可以省略的部分

## 4.5 数据查询语言DQL

### 4.5.1 **查询的完整语法**

查询最重要，最常用。

```sql
SELECT 
    字段列表
FROM 
    表名列表 
WHERE 
    条件列表
GROUP BY
    分组字段
HAVING
    分组后条件
ORDER BY
    排序字段
LIMIT
    分页限定

```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.5.2 创建练习查询的表

```sql
-- 删除stu表
drop table if exists stu;


-- 创建stu表
CREATE TABLE stu (
 id int, -- 编号
 name varchar(20), -- 姓名
 age int, -- 年龄
 sex varchar(5), -- 性别
 address varchar(100), -- 地址
 math double(5,2), -- 数学成绩
 english double(5,2), -- 英语成绩
 hire_date date -- 入学时间
);

-- 添加数据
INSERT INTO stu(id,NAME,age,sex,address,math,english,hire_date) 
VALUES 
(1,'马运',55,'男','杭州',66,78,'1995-09-01'),
(2,'马花疼',45,'女','深圳',98,87,'1998-09-01'),
(3,'马斯克',55,'男','香港',56,77,'1999-09-02'),
(4,'柳白',20,'女','湖南',76,65,'1997-09-05'),
(5,'柳青',20,'男','湖南',86,NULL,'1998-09-01'),
(6,'刘德花',57,'男','香港',99,99,'1998-09-01'),
(7,'张学右',22,'女','香港',99,99,'1998-09-01'),
(8,'德玛西亚',18,'男','南京',56,65,'1994-09-02');
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.5.3 基础查询

- **示例**

```sql
SELECT DISTINCT name AS '名字',age AS '年龄' FROM stu;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\3ab152b845974c18be6b0e1acaae2527.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **查询多个字段**

```sql
SELECT 字段列表 FROM 表名;
SELECT * FROM 表名; -- 查询所有数据
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **查询字段并去除重复记录**

```sql
SELECT DISTINCT 字段列表 FROM 表名;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 ![img](JavaWeb基础1——MySQL.assets\315c2e2ee0624a669c86e0b1d2d60fae.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)去重后![img](JavaWeb基础1——MySQL.assets\a32778c2a1e343ff9efd5bdb308c40a5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **起别名**

```sql
AS: AS 也可以省略
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.5.4 条件查询（包括模糊查询）

```sql
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

举例： 

```sql
SELECT DISTINCT name AS '名字',age AS '年龄' FROM stu WHERE age>20 && age<=40;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\ddc740c79210457b98b79dd575e0bf62.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 **模糊查询：**

```sql
SELECT  * FROM stu WHERE name LIKE '_斯%';
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\c39edd4068e44107acea7ae3aa1aaa7f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**模糊查询替换符：** 

下划线是必须一个字符，百分号替换0-多个字符

- **条件**

![img](JavaWeb基础1——MySQL.assets\2c69ca66aefc4553844df2c244c782bb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> 1.  null不能和等号运算，要 IS NULL或 IS NOT NULL，而不是=null
> 2. SQL语句没有==，相等是=，没有赋值的概念。

### 4.5.5 排序查询

```sql
SELECT 字段列表 FROM 表名 ORDER BY 排序字段名1 [排序方式1],排序字段名2 [排序方式2] …;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 查询学生信息，按照数学成绩降序排列，如果数学成绩一样，再按照英语成绩升序排列

  ```sql
  select * from stu order by math desc , english asc ;
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  ![img](JavaWeb基础1——MySQL.assets\89f64c7fde47401fbdcb59187de0eb27.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

上述语句中的排序方式有两种，分别是：

- **ASC ：** 升序排列 **（默认值）***ascending* /əˈsendɪŋ/ 
- **DESC ：** 降序排列，descending /dɪˈsendɪŋ/ 

> **注意：**如果有多个排序条件，当前边的条件值一样时，才会根据第二条件进行排序

### 4.5.6 聚合函数

```sql
SELECT 聚合函数名(列名) FROM 表;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

示例：

```bash
select count(id) from stu;    #统计id字段非null的记录数量
select count(*) from stu;# 统计“存在非null字段”的记录数量，* 表示所有字段数据，只要某行有一个非空数据，就会被统计在内
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\7ad711a9b074461480c36b47e45de626.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](JavaWeb基础1——MySQL.assets\0c23e9ada91b4fbc87b54c2c6d81b960.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](JavaWeb基础1——MySQL.assets\d44c872e2b454a9999a5e52603b96b0d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> ![img](JavaWeb基础1——MySQL.assets\0783e43c712647fe910cc9520ff74c7a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **聚合函数：**

| 函数名      | 功能                         |
| ----------- | ---------------------------- |
| count(列名) | 统计数量（选用不为null的列） |
| max(列名)   | 最大值                       |
| min(列名)   | 最小值                       |
| sum(列名)   | 求和                         |
| avg(列名)   | 平均值                       |

> **注意：null 值不参与所有聚合函数运算**

### 4.5.7 带条件的聚合函数：count(name='abcd' or null)

统计所有名字为‘abcd’的学生：

```bash
SELECT count(name='abcd' or null) FROM student;#使用count带条件统计数量必须or null
SELECT count(date  between '2019-01-01' and '2019-03-31' or null) #使用count带条件统计数量必须or null
SELECT count(distinct name) FROM student;#注意distinct不能or null

#使用sum带条件统计数量不用or null。尽量别用sum，因为sum主要用来取和，如果这个name字段是数字型，则会是取和。
SELECT sum(name='abcd') FROM student;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

第一个和第四个结果都是1：

![img](JavaWeb基础1——MySQL.assets\af23963217614601879e5c0210a0e0f2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **注意：**
>
> - 使用count带条件统计数量必须or null，否则是统计总数量（条件是distinct除外）
> - 使用sum带条件统计数量不用or null
>
> 示例：使用count带条件统计数量如果不加or null，就会统计这个字段总数量
>
> ```bash
> SELECT count(name='abcd') FROM student;
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> ![img](JavaWeb基础1——MySQL.assets\158cd1a13cc047638cb96538552332c1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.5.7 分组查询

常常和聚合函数一起用。 

```sql
SELECT 字段列表 FROM 表名 [WHERE 分组前条件限定] GROUP BY 分组字段名 [HAVING 分组后条件过滤];
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**分组之后，查询的字段为聚合函数和分组字段，查询其他字段无任何意义

**练习：**

查询男同学和女同学各自的数学平均分：

```sql
#根据性别分组，每组统计平均值
select sex, avg(math) from stu group by sex;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\942c5b4a5b2147fb8907c53715b2d120.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**在分组的情况下，查询字段为聚合函数时，这个聚合函数统计的将是**每组的信息**

查询男同学和女同学各自的数学平均分，以及各自人数；要求：分数低于70分的不参与分组，分组之后人数大于2个。

```sql
#根据性别分组，每组统计数学平均值、人数；分组前过滤math > 70，分组后过滤只展示人数>2的分组
select sex, avg(math),count(*) from stu where math > 70 group by sex having count(*)>2;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\054c49471721496c9d488a41bea8cb92.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 因为分组后男性人数没满足having条件，所以男性分组没展示。

> **where 和 having 区别：**
>
> - 执行时机不一样：where 是分组之前进行限定，不满足where条件，则不参与分组，而having是分组之后对结果进行过滤。
> - 可判断的条件不一样：where 不能对聚合函数进行判断，having 可以。执行顺序where>聚合函数>having，不可能判断后面执行的条件。

### 4.5.8 分页查询

```sql
SELECT 字段列表 FROM 表名 LIMIT  起始索引 , 查询条目数;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**练习：**

起始索引 = (当前页码 - 1) * 每页显示的条数

- 从0开始查询，查询3条数据

  ```sql
  select * from stu limit 0 , 3;
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 每页显示3条数据，查询第1页数据

  ```sql
  select * from stu limit 0 , 3;
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

# 五、约束

## 5.1 概念

- 约束是作用于表中**列上的规则**，**用于限制加入表的数据**

  例如：我们可以给id列加约束，让其值不能重复，不能为null值。

- 添加约束可以在添加数据的时候就限制不正确的数据。例如把年龄是3000，数学成绩是-5分这样无效的数据限制掉，继而保障数据的完整性。

## **5.2 常用约束**

### 5.2.1 介绍

| 约束名            | 约束关键字               | 说明                                |
| ----------------- | ------------------------ | ----------------------------------- |
| 主键              | primary key              | 唯一，非空                          |
| 唯一              | unique                   | 不能重复，最多只有一个非空记录      |
| 默认              | default                  | 没有输入值，使用默认值              |
| 非空              | not null                 | 必须输入                            |
|                   |                          |                                     |
| 外键              | foreign key … references | 外键在从表 主表：1方 从表：多方     |
| 自增              | auto_increment           | 从1开始自增，只有唯一和主键约束能用 |
| 检查(mysql不支持) | check                    | 保证列中的值满足某一条件。          |

### 5.2.2 常用命令

查询表中所有约束

```sql
SELECT 
    TABLE_NAME,
    COLUMN_NAME,
    CONSTRAINT_NAME,
    REFERENCED_TABLE_NAME,
    REFERENCED_COLUMN_NAME
FROM
    INFORMATION_SCHEMA.KEY_COLUMN_USAGE
WHERE
    TABLE_SCHEMA = '表名'
    AND TABLE_NAME = '表名';
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

删除约束（DROP CONSTRAINT）:

```sql
ALTER TABLE table_name
DROP PRIMARY KEY; 
-- 或 DROP FOREIGN KEY, DROP UNIQUE, 等等
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## **5.3 增删约束**

![img](JavaWeb基础1——MySQL.assets\a750fe19b6b340dab79c0312e7d04e19.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **示例：**

![img](JavaWeb基础1——MySQL.assets\1fc52f436f004b128852ccbcf0fbd766.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





## 5.4 外键约束

### 5.4.1 概述 

```sql
-- 创建表时添加外键约束
CREATE TABLE 表名(
   列名 数据类型,
   …
   [CONSTRAINT] [外键取名名称] FOREIGN KEY(外键列名) REFERENCES 主表(主表列名) 
); 

-- 创建表时添加外键约束，constraint译作限制，束缚；references译作关联，参考，提及
create table 表名(
   列名 数据类型,
   …
   [constraint] [外键取名名称] foreign key(外键列名) references 主表(主表列名) 
); 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```sql
-- 建完表后添加外键约束
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);

-- 建完表后添加外键约束
alter table 表名 add constraint 外键名称 foreign key (外键字段名称) references 主表名称(主表列名称);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 删除外键约束

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 5.4.2 练习

![img](JavaWeb基础1——MySQL.assets\613b5552b3774d08a530317d3765e45b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```
-- 删除表
DROP TABLE IF EXISTS emp;
DROP TABLE IF EXISTS dept;

-- 部门表
CREATE TABLE dept(
	id int primary key auto_increment,
	dep_name varchar(20),
	addr varchar(20)
);
-- 员工表 
CREATE TABLE emp(
	id int primary key auto_increment,
	name varchar(20),
	age int,
	dep_id int,

	-- 添加外键 dep_id,关联 dept 表的id主键
	CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES dept(id)	
);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

添加数据

```sql
-- 添加 2 个部门
insert into dept(dep_name,addr) values
('研发部','广州'),('销售部', '深圳');

-- 添加员工,dep_id 表示员工所在的部门
INSERT INTO emp (name, age, dep_id) VALUES 
('张三', 20, 1),
('李四', 20, 1),
('王五', 20, 1),
('赵六', 20, 2),
('孙七', 22, 2),
('周八', 18, 2);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

此时删除 `研发部` 这条数据，会发现无法删除。

删除外键

```sql
alter table emp drop FOREIGN key fk_emp_dept;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

重新添加外键

```sql
alter table emp add CONSTRAINT fk_emp_dept FOREIGN key(dep_id) REFERENCES dept(id);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\16d3b20347d94303967400fd0f3adfd7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

右键逆向到表模型，可以查看关系:![img](JavaWeb基础1——MySQL.assets\b16d241d741c4aa98e86e8b2f064b776.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 六、数据库设计

## 6.1 概念

- 软件的研发步骤![img](JavaWeb基础1——MySQL.assets\0e7e23a46ca74b9f80638597a48a38aa.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- **数据库设计概念**

  - 设计方向：有哪些表？表里有哪些字段？表和表之间有什么关系？
  - **数据库设计就是根据业务系统的具体需求，结合我们所选用的DBMS，为这个业务系统构造出最优的数据存储模型。**
  - 建立数据库中的**表结构**以及**表与表之间的关联关系**的过程。

- **数据库设计的步骤**

  - 需求分析（数据是什么? 数据具有哪些属性? 数据与属性的特点是什么）

  - 逻辑分析（通过ER图对数据库进行逻辑建模，不需要考虑我们所选用的数据库管理系统）

    如下图就是ER(Entity/Relation)图：![img](JavaWeb基础1——MySQL.assets\962a7371d24d4fbba06293c85fe4e784.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

    

- - 物理设计（根据数据库自身的特点把逻辑设计转换为物理设计）
  - 维护设计（1.对新的需求进行建表；2.表优化）

## 6.2 表关系



### 6.2.1 一对多

如：部门 和 员工

一个部门对应多个员工，一个员工对应一个部门。

**实现方式**

**在多的一方建立外键，指向一的一方的主键**

![img](JavaWeb基础1——MySQL.assets\cdb45d19fb044983b1c2747fd51ff67b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 建表语句：

```sql
-- 删除表
DROP TABLE IF EXISTS tb_emp;
DROP TABLE IF EXISTS tb_dept;

-- 部门表
CREATE TABLE tb_dept(
	id int primary key auto_increment,
	dep_name varchar(20),
	addr varchar(20)
);
-- 员工表 
CREATE TABLE tb_emp(
	id int primary key auto_increment,
	name varchar(20),
	age int,
	dep_id int,

	-- 添加外键 dep_id,关联 dept 表的id主键
	CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES tb_dept(id)	
);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 6.2.2 多对多

如：商品 和 订单

一个商品对应多个订单，一个订单包含多个商品。

**实现方式：**

建立第三张**中间表**，中间表至少包含**两个外键**，分别**关联两方主键**。

**案例：**

![img](JavaWeb基础1——MySQL.assets\fe300ef5aeaa4a70a056fa0f884311b9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



建表语句：

```
-- 删除表
DROP TABLE IF EXISTS tb_order_goods;
DROP TABLE IF EXISTS tb_order;
DROP TABLE IF EXISTS tb_goods;

-- 订单表
CREATE TABLE tb_order(
	id int primary key auto_increment,
	payment double(10,2),
	payment_type TINYINT,
	status TINYINT
);

-- 商品表
CREATE TABLE tb_goods(
	id int primary key auto_increment,
	title varchar(100),
	price double(10,2)
);

-- 订单商品中间表
CREATE TABLE tb_order_goods(
	id int primary key auto_increment,
	order_id int,
	goods_id int,
	count int
);

-- 建完表后，添加外键
alter table tb_order_goods add CONSTRAINT fk_order_id FOREIGN key(order_id) REFERENCES tb_order(id);
alter table tb_order_goods add CONSTRAINT fk_goods_id FOREIGN key(goods_id) REFERENCES tb_goods(id);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 表结构模型：

![img](JavaWeb基础1——MySQL.assets\d7a0bf88cd8445a6a78890582e87ee27.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 6.2.3 一对一



如：用户 和 用户详情

一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另一张表，用于提升查询性能。

**实现方式：**

在任意一方加入外键，关联另一方主键，并且设置外键为唯一(UNIQUE)

**案例：**

![img](JavaWeb基础1——MySQL.assets\87326bacb5d2471c94c5584426387029.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 而在真正使用过程中发现 id、photo、nickname、age、gender 字段比较常用，此时就可以将这张表查分成两张表：

![img](JavaWeb基础1——MySQL.assets\5506c47719e243908d809b725abb9eee.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**建表语句如下：**

```sql
create table tb_user_desc (
    id int primary key auto_increment,
    city varchar(20),
    edu varchar(10),
    income int,
    status char(2),
    des varchar(100)
);

create table tb_user (
    id int primary key auto_increment,
    photo varchar(100),
    nickname varchar(50),
    age int,
    gender char(1),
    desc_id int unique,
    -- 添加外键
    CONSTRAINT fk_user_desc FOREIGN KEY(desc_id) REFERENCES tb_user_desc(id)    
);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**查看表结构模型图：**

![img](JavaWeb基础1——MySQL.assets\17fe81e5ded34f0e809f84d956c7b500.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 七、多表查询

## 7.1 创建练习的表

```sql
DROP TABLE IF EXISTS emp;
DROP TABLE IF EXISTS dept;


# 创建部门表
	CREATE TABLE dept(
        did INT PRIMARY KEY AUTO_INCREMENT,
        dname VARCHAR(20)
    );

	# 创建员工表
	CREATE TABLE emp (
        id INT PRIMARY KEY AUTO_INCREMENT,
        NAME VARCHAR(10),
        gender CHAR(1), -- 性别
        salary DOUBLE, -- 工资
        join_date DATE, -- 入职日期
        dep_id INT,
        FOREIGN KEY (dep_id) REFERENCES dept(did) -- 外键，关联部门表(部门表的主键)
    );
	-- 添加部门数据
	INSERT INTO dept (dNAME) VALUES ('研发部'),('市场部'),('财务部'),('销售部');
	-- 添加员工数据
	INSERT INTO emp(NAME,gender,salary,join_date,dep_id) VALUES
	('孙悟空','男',7200,'2013-02-24',1),
	('猪八戒','男',3600,'2010-12-02',2),
	('唐僧','男',9000,'2008-08-08',2),
	('白骨精','女',5000,'2015-10-07',3),
	('蜘蛛精','女',4500,'2011-03-14',1),
	('小白龙','男',2500,'2011-02-14',null);	
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

员工表：

![img](JavaWeb基础1——MySQL.assets\e809a1e401dd4864b48a88a9718cb9b7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

部门表：

![img](JavaWeb基础1——MySQL.assets\55da6b0f18194baba285e9c25410c834.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 7.2 连接查询

### 7.2.1 概念 

![img](JavaWeb基础1——MySQL.assets\06e8d376006348d2aef052eddb179858.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 内连接查询 ：相当于查询AB交集数据
- 外连接查询
  - 左外连接查询 ：相当于查询A表所有数据和交集部门数据
  - 右外连接查询 ： 相当于查询B表所有数据和交集部分数据

**关联查询结果行数：**假设a表x行，b表y行；

- **a左连接b：**x行~x*y行
- **a右连接b：**y行~y*x行
- **内连接：**0行~min(x,y)行



### 7.2.2 内连接查询

相当于查询AB交集数据。

**语句：**

```sql
-- 隐式内连接。没有JOIN关键字，条件使用WHERE指定。书写简单，多表时效率低
SELECT 字段列表 FROM 表1,表2… WHERE 条件;

-- 显示内连接。使用INNER JOIN ... ON语句, 可以省略INNER。书写复杂，多表时效率高
SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 条件;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 隐式连接好理解好书写，语法简单，担心的点较少。
>
> 但是**显式连接**可以减少字段的扫描，有**更快的执行速度**。这种速度优势在3张或更多表连接时比较明显 

 **示例：**

```sql
#隐式内连接
SELECT
	emp. NAME,
	emp.gender,
	dept.dname
FROM
	emp,
	dept
WHERE
	emp.dep_id = dept.did;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```sql
#显式内连接
select * from emp inner join dept on emp.dep_id = dept.did;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](JavaWeb基础1——MySQL.assets\c8944eb2480a4b2a9c80fdab4b0e81c0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 员工表：
>
> ![img](JavaWeb基础1——MySQL.assets\e809a1e401dd4864b48a88a9718cb9b7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 部门表：
>
> ![img](JavaWeb基础1——MySQL.assets\55da6b0f18194baba285e9c25410c834.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 7.2.3 自连接

自连接是一种特殊的[内连接](https://baike.baidu.com/item/内连接?fromModule=lemma_inlink)，它是指相互连接的表在物理上为同一张表，但可以在**逻辑上**分为两张表。

> **注意：自连接查询的列名必须是“表名.\*”，而不是直接写“\*”**

案例：

要求检索出学号为**20210**的学生的同班同学的信息

```sql
SELECT stu.*        #一定注意是stu.*，不是*

FROM stu JOIN stu AS stu1 ON stu.grade= stu1.grade

WHERE stu1.id='20210'
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 7.2.4 递归查询

with语法：

```sql
   WITH [RECURSIVE]
        cte_name [(col_name [, col_name] ...)] AS (subquery)
        [, cte_name [(col_name [, col_name] ...)] AS (subquery)] ...
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> recurslve译为递归。
>
> **with：**在mysql中被称为**公共表达式**,可以作为一个**临时表**然后在其他结构中调用.如果是自身调用那么就是后面讲的递归.
>
> cte_name :公共表达式的名称,可以理解为表名,用来表示as后面跟着的子查询
>
> col_name :公共表达式包含的列名,可以写也可以不写

**例子：使用MySQL临时表遍历1~5**

```sql
with RECURSIVE t1  AS    #这里t1函数名，也是临时表的表名
(
  SELECT 1 as n        #n是列的别名，1是初始记录
  UNION ALL        #把递归结果（2,3,4,5）合并到t1表中
  SELECT n + 1 FROM t1 WHERE n < 5    #n+1是参数，t1是函数名，n<5是遍历终止条件
)
SELECT * FROM t1;        #正常查询t1这个临时表，相当于调用这个函数。
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](JavaWeb基础1——MySQL.assets\b00f80066b59494bbceda2ae669aab7d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **说明：**
>
> t1 相当于一个表名
>
> select 1 相当于这个表的初始值，这里使用UNION ALL 不断将每次递归得到的数据加入到表中。
>
> n<5为递归执行的条件，当n>=5时结束递归调用。

**案例，递归查询课程多级分类：**

```sql
with recursive t1 as (        #t1是函数名、临时表名
select * from  course_category where  id= '1'   #初始记录，也就是根节点
union all         #把递归结果合并到t1表中
 select t2.* from course_category as t2 inner join t1 on t1.id = t2.parentid    #递归，用分类表t和临时表t1内连接查询
)

select *  from t1 order by t1.id, t1.orderby    #查t1表，相当于调用这个函数。
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\53252175022343bdab773c9da2f9b5ac.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**mysql递归特点，对比Java递归的优势**

**mysql递归次数限制：**

mysql为了避免无限递归默认递归次数为1000，可以通过设置cte_max_recursion_depth参数增加递归深度，还可以通过max_execution_time限制执行时间，超过此时间也会终止递归操作。

**对比Java递归的优势：**

mysql递归相当于在存储过程中执行若干次sql语句，java程序仅与数据库建立一次链接执行递归操作。相比之下，Java递归性能就很差，每次递归都会建立一次数据库连接。



### 7.2.5 外连接查询

**语句：**

```sql
-- 左外连接
SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件;

-- 右外连接
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

一般都用左外连接，因为右外连接可用左外连接实现，可读性更好。 

**示例：**

查询emp表所有数据和对应的部门信息（左外连接）

```sql
select * from emp left join dept on emp.dep_id = dept.did;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础1——MySQL.assets\0b998abdac6b44afa91caa195373e2b3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

查询dept表所有数据和对应的员工信息（右外连接）

```sql
select * from emp right join dept on emp.dep_id = dept.did;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](JavaWeb基础1——MySQL.assets\a8ffd61c9099421f85d687cb6556d290.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 7.3 子查询

查询中嵌套查询，称嵌套查询为子查询。

> 注意：子语句没有分号。

**子查询根据查询结果不同，作用不同，可分为：**

- **子查询语句结果是单行单列**，子查询语句作为条件值，使用 = != > < 等进行条件判断

![img](JavaWeb基础1——MySQL.assets\cfe891f0e64549b69f5598cbbe269745.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 示例：

查询比猪八戒薪水高的员工：

```sql
SELECT * FROM emp WHERE salary >(SELECT salary FROM emp WHERE name='猪八戒');
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **子查询语句结果是多行单列**，子查询语句作为条件值，使用 in 等关键字进行条件判断

![img](JavaWeb基础1——MySQL.assets\ae2bd8e4ad7941ca90f5d6e9651231ef.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 示例：

查询 '财务部' 和 '市场部' 所有的员工信息：

```sql
SELECT * FROM emp WHERE dep_id in (SELECT did FROM dept WHERE dname IN ('财务部','市场部'));
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **子查询语句结果是多行多列**，子查询语句作为虚拟表

![img](JavaWeb基础1——MySQL.assets\4d0d116169a74593bc53007763749519.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

示例：

 查询入职日期是 '2011-11-11' 之后的员工信息和部门信息：

```sql
select * from (select * from emp where join_date > '2011-11-11' ) AS t1, dept where t1.dep_id = dept.did;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 7.4 多表查询练习题：

```sql
DROP TABLE IF EXISTS emp;
DROP TABLE IF EXISTS dept;
DROP TABLE IF EXISTS job;
DROP TABLE IF EXISTS salarygrade;

-- 部门表
CREATE TABLE dept (
  did INT PRIMARY KEY PRIMARY KEY, -- 部门id
  dname VARCHAR(50), -- 部门名称
  loc VARCHAR(50) -- 部门所在地
);

-- 职务表，职务名称，职务描述
CREATE TABLE job (
  id INT PRIMARY KEY,
  jname VARCHAR(20),
  description VARCHAR(50)
);

-- 员工表
CREATE TABLE emp (
  id INT PRIMARY KEY, -- 员工id
  ename VARCHAR(50), -- 员工姓名
  job_id INT, -- 职务id
  mgr INT , -- 上级领导
  joindate DATE, -- 入职日期
  salary DECIMAL(7,2), -- 工资
  bonus DECIMAL(7,2), -- 奖金
  dept_id INT, -- 所在部门编号
  CONSTRAINT emp_jobid_ref_job_id_fk FOREIGN KEY(job_id) REFERENCES job(id),
  CONSTRAINT emp_deptid_ref_dept_id_fk FOREIGN KEY(dept_id) REFERENCES dept(did)
);
-- 工资等级表
CREATE TABLE salarygrade (
  grade INT PRIMARY KEY,   -- 级别
  losalary INT,  -- 最低工资
  hisalary INT -- 最高工资
);
				
-- 添加4个部门
INSERT INTO dept(did,dname,loc) VALUES 
(10,'教研部','北京'),
(20,'学工部','上海'),
(30,'销售部','广州'),
(40,'财务部','深圳');

-- 添加4个职务
INSERT INTO job (id, jname, description) VALUES
(1, '董事长', '管理整个公司，接单'),
(2, '经理', '管理部门员工'),
(3, '销售员', '向客人推销产品'),
(4, '文员', '使用办公软件');


-- 添加员工
INSERT INTO emp(id,ename,job_id,mgr,joindate,salary,bonus,dept_id) VALUES 
(1001,'孙悟空',4,1004,'2000-12-17','8000.00',NULL,20),
(1002,'卢俊义',3,1006,'2001-02-20','16000.00','3000.00',30),
(1003,'林冲',3,1006,'2001-02-22','12500.00','5000.00',30),
(1004,'唐僧',2,1009,'2001-04-02','29750.00',NULL,20),
(1005,'李逵',4,1006,'2001-09-28','12500.00','14000.00',30),
(1006,'宋江',2,1009,'2001-05-01','28500.00',NULL,30),
(1007,'刘备',2,1009,'2001-09-01','24500.00',NULL,10),
(1008,'猪八戒',4,1004,'2007-04-19','30000.00',NULL,20),
(1009,'罗贯中',1,NULL,'2001-11-17','50000.00',NULL,10),
(1010,'吴用',3,1006,'2001-09-08','15000.00','0.00',30),
(1011,'沙僧',4,1004,'2007-05-23','11000.00',NULL,20),
(1012,'李逵',4,1006,'2001-12-03','9500.00',NULL,30),
(1013,'小白龙',4,1004,'2001-12-03','30000.00',NULL,20),
(1014,'关羽',4,1007,'2002-01-23','13000.00',NULL,10);


-- 添加5个工资等级
INSERT INTO salarygrade(grade,losalary,hisalary) VALUES 
(1,7000,12000),
(2,12010,14000),
(3,14010,20000),
(4,20010,30000),
(5,30010,99990);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



需求

1. 查询所有员工信息。查询员工编号，员工姓名，工资，职务名称，职务描述

   ```sql
   /*
       分析：
           1. 员工编号，员工姓名，工资 信息在emp 员工表中
           2. 职务名称，职务描述 信息在 job 职务表中
           3. job 职务表 和 emp 员工表 是 一对多的关系 emp.job_id = job.id
   */
   -- 方式一 ：隐式内连接
   SELECT
       emp.id,
       emp.ename,
       emp.salary,
       job.jname,
       job.description
   FROM
       emp,
       job
   WHERE
       emp.job_id = job.id;
   
   -- 方式二 ：显式内连接
   SELECT
       emp.id,
       emp.ename,
       emp.salary,
       job.jname,
       job.description
   FROM
       emp
   INNER JOIN job ON emp.job_id = job.id;
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

2. 查询员工编号，员工姓名，工资，职务名称，职务描述，部门名称，部门位置

   ```sql
   /*
       分析：
           1. 员工编号，员工姓名，工资 信息在emp 员工表中
           2. 职务名称，职务描述 信息在 job 职务表中
           3. job 职务表 和 emp 员工表 是 一对多的关系 emp.job_id = job.id
   
           4. 部门名称，部门位置 来自于 部门表 dept
           5. dept 和 emp 一对多关系 dept.id = emp.dept_id
   */
   
   -- 方式一 ：隐式内连接
   SELECT
       emp.id,
       emp.ename,
       emp.salary,
       job.jname,
       job.description,
       dept.dname,
       dept.loc
   FROM
       emp,
       job,
       dept
   WHERE
       emp.job_id = job.id
       and dept.id = emp.dept_id
   ;
   
   -- 方式二 ：显式内连接
   SELECT
       emp.id,
       emp.ename,
       emp.salary,
       job.jname,
       job.description,
       dept.dname,
       dept.loc
   FROM
       emp
   INNER JOIN job ON emp.job_id = job.id
   INNER JOIN dept ON dept.id = emp.dept_id
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

3. 查询员工姓名，工资，工资等级

   ```sql
   /*
       分析：
           1. 员工姓名，工资 信息在emp 员工表中
           2. 工资等级 信息在 salarygrade 工资等级表中
           3. emp.salary >= salarygrade.losalary  and emp.salary <= salarygrade.hisalary
   */
   SELECT
       emp.ename,
       emp.salary,
       t2.*
   FROM
       emp,
       salarygrade t2
   WHERE
       emp.salary >= t2.losalary
   AND emp.salary <= t2.hisalary
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

4. 查询员工姓名，工资，职务名称，职务描述，部门名称，部门位置，工资等级

   ```sql
   /*
       分析：
           1. 员工编号，员工姓名，工资 信息在emp 员工表中
           2. 职务名称，职务描述 信息在 job 职务表中
           3. job 职务表 和 emp 员工表 是 一对多的关系 emp.job_id = job.id
   
           4. 部门名称，部门位置 来自于 部门表 dept
           5. dept 和 emp 一对多关系 dept.id = emp.dept_id
           6. 工资等级 信息在 salarygrade 工资等级表中
           7. emp.salary >= salarygrade.losalary  and emp.salary <= salarygrade.hisalary
   */
   SELECT
       emp.id,
       emp.ename,
       emp.salary,
       job.jname,
       job.description,
       dept.dname,
       dept.loc,
       t2.grade
   FROM
       emp
   INNER JOIN job ON emp.job_id = job.id
   INNER JOIN dept ON dept.id = emp.dept_id
   INNER JOIN salarygrade t2 ON emp.salary BETWEEN t2.losalary and t2.hisalary;
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

# 八、事务

## 8.1 概念

数据库的事务（Transaction）是一种机制、一个操作序列，包含了**一组数据库操作命令**。

事务把所有的命令作为一个整体一起向系统提交或撤销操作请求，即这一组数据库命令**要么同时成功，要么同时失败**。

事务是一个不可分割的工作逻辑单元。

**示例：**

![img](JavaWeb基础1——MySQL.assets\b95bc735a1b64e5285565707a24acc4f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 在转账前开启事务，如果出现了异常回滚事务，三步正常执行就提交事务，这样就可以完美解决问题。

## 8.2 语法

- 开启事务

  ```sql
  START TRANSACTION;        --transaction译为事务，业务，交易
  或者  
  BEGIN;
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 提交事务

  ```sql
  commit;
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**示例：**

```
-- 开启事务
BEGIN;
-- 转账操作
-- 1. 查询李四账户金额是否大于500

-- 2. 李四账户 -500
UPDATE account set money = money - 500 where name = '李四';

出现异常了...  -- 此处不是注释，在整体执行时会出问题，后面的sql则不执行
-- 3. 张三账户 +500
UPDATE account set money = money + 500 where name = '张三';

-- 提交事务
COMMIT;

-- 回滚事务
ROLLBACK;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面sql中的执行成功进选择执行提交事务，而出现问题则执行回滚事务的语句。以后我们肯定不可能这样操作，而是在java中进行操作，在java中可以抓取异常，没出现异常提交事务，出现异常回滚事务。  

## 8.3 事务的四大特征

- 原子性（Atomicity）: 事务是不可分割的最小操作单位，要么同时成功，要么同时失败
- 一致性（Consistency） :事务完成时，必须使所有的数据都保持一致状态
- 隔离性（Isolation） :多个事务之间，操作的可见性
- 持久性（Durability） :事务一旦提交或回滚，它对数据库中的数据的改变就是永久的

> **说明**：
>
> mysql中事务是自动提交的。
>
> 也就是说我们不添加事务执行sql语句，语句执行完毕会自动的提交事务。
>
> 
>
> 可以通过下面语句查询默认提交方式：
>
> ```
> SELECT @@autocommit;
> ```
>
> 查询到的结果是1 则表示自动提交，结果是0表示手动提交。当然也可以通过下面语句修改提交方式
>
> ```
> set @@autocommit = 0;
> ```

# 九、函数

## 9.1 数值型函数 

| 函数名称                                                     | 作 用                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [ABS](http://c.biancheng.net/mysql/abc.html)                 | 求绝对值                                                     |
| [SQRT](http://c.biancheng.net/mysql/sqrt.html)               | 求二次方根                                                   |
| [MOD](http://c.biancheng.net/mysql/mod.html)                 | 求余数                                                       |
| [CEIL 和 CEILING](http://c.biancheng.net/mysql/ceil_celing.html) | 两个函数功能相同，都是返回不小于参数的最小整数，即向上取整   |
| [FLOOR](http://c.biancheng.net/mysql/floor.html)             | 向下取整，返回值转化为一个BIGINT                             |
| [RAND](http://c.biancheng.net/mysql/rand.html)               | 生成一个0~1之间的随机数，传入整数参数是，用来产生重复序列    |
| [ROUND](http://c.biancheng.net/mysql/round.html)             | 对所传参数进行四舍五入。例如round(3.1415926,3)是四舍五入保留三位小数 |
| [SIGN](http://c.biancheng.net/mysql/sign.html)               | 返回参数的符号                                               |
| [POW 和 POWER](http://c.biancheng.net/mysql/pow_power.html)  | 两个函数的功能相同，都是所传参数的次方的结果值               |
| [SIN](http://c.biancheng.net/mysql/sin.html)                 | 求正弦值                                                     |
| [ASIN](http://c.biancheng.net/mysql/asin.html)               | 求反正弦值，与函数 SIN 互为反函数                            |
| [COS](http://c.biancheng.net/mysql/cos.html)                 | 求余弦值                                                     |
| [ACOS](http://c.biancheng.net/mysql/acos.html)               | 求反余弦值，与函数 COS 互为反函数                            |
| [TAN](http://c.biancheng.net/mysql/tan.html)                 | 求正切值                                                     |
| [ATAN](http://c.biancheng.net/mysql/atan.html)               | 求反正切值，与函数 TAN 互为反函数                            |
| [COT](http://c.biancheng.net/mysql/cot.html)                 | 求余切值                                                     |

## 9.2 字符串函数

| 函数名称                                                 | 作 用                                                        |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| [LENGTH](http://c.biancheng.net/mysql/length.html)       | 计算字符串长度函数，返回字符串的字节长度                     |
| [CONCAT](http://c.biancheng.net/mysql/concat.html)       | 合并字符串函数，返回结果为连接参数产生的字符串，参数可以使一个或多个 |
| [INSERT](http://c.biancheng.net/mysql/insert.html)       | 替换字符串函数                                               |
| [LOWER](http://c.biancheng.net/mysql/lower.html)         | 将字符串中的字母转换为小写                                   |
| [UPPER](http://c.biancheng.net/mysql/upper.html)         | 将字符串中的字母转换为大写                                   |
| [LEFT](http://c.biancheng.net/mysql/left.html)           | 从左侧字截取符串，返回字符串左边的若干个字符                 |
| [RIGHT](http://c.biancheng.net/mysql/right.html)         | 从右侧字截取符串，返回字符串右边的若干个字符                 |
| [TRIM](http://c.biancheng.net/mysql/trim.html)           | 删除字符串左右两侧的空格                                     |
| [REPLACE](http://c.biancheng.net/mysql/replace.html)     | 字符串替换函数，返回替换后的新字符串                         |
| [SUBSTRING](http://c.biancheng.net/mysql/substring.html) | 截取字符串，返回从指定位置开始的指定长度的字符换             |
| [REVERSE](http://c.biancheng.net/mysql/reverse.html)     | 字符串反转（逆序）函数，返回与原始字符串顺序相反的字符串     |

## 9.3 日期和时间函数

| 函数名称                                                     | 作 用                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [CURDATE 和 CURRENT_DATE](http://c.biancheng.net/mysql/curdate_current_date.html) | 两个函数作用相同，返回当前系统的日期值                       |
| [CURTIME 和 CURRENT_TIME](http://c.biancheng.net/mysql/curtime_current_time.html) | 两个函数作用相同，返回当前系统的时间值                       |
| [NOW 和 SYSDATE](http://c.biancheng.net/mysql/now_sysdate.html) | 两个函数作用相同，返回当前系统的日期和时间值                 |
| [UNIX_TIMESTAMP](http://c.biancheng.net/mysql/unix_timestamp.html) | 获取UNIX时间戳函数，返回一个以 UNIX 时间戳为基础的无符号整数 |
| [FROM_UNIXTIME](http://c.biancheng.net/mysql/from_unixtime.html) | 将 UNIX 时间戳转换为时间格式，与UNIX_TIMESTAMP互为反函数     |
| [MONTH](http://c.biancheng.net/mysql/month.html)             | 获取指定日期中的月份                                         |
| [MONTHNAME](http://c.biancheng.net/mysql/monthname.html)     | 获取指定日期中的月份英文名称                                 |
| [DAYNAME](http://c.biancheng.net/mysql/dayname.html)         | 获取指定曰期对应的星期几的英文名称                           |
| [DAYOFWEEK](http://c.biancheng.net/mysql/dayofweek.html)     | 获取指定日期对应的一周的索引位置值                           |
| [WEEK](http://c.biancheng.net/mysql/week.html)               | 获取指定日期是一年中的第几周，返回值的范围是否为 0〜52 或 1〜53 |
| [DAYOFYEAR](http://c.biancheng.net/mysql/dayofyear.html)     | 获取指定曰期是一年中的第几天，返回值范围是1~366              |
| [DAYOFMONTH](http://c.biancheng.net/mysql/dayofmonth.html)   | 获取指定日期是一个月中是第几天，返回值范围是1~31             |
| [YEAR](http://c.biancheng.net/mysql/year.html)               | 获取年份，返回值范围是 1970〜2069                            |
| [TIME_TO_SEC](http://c.biancheng.net/mysql/time_to_sec.html) | 将时间参数转换为秒数                                         |
| [SEC_TO_TIME](http://c.biancheng.net/mysql/sec_to_time.html) | 将秒数转换为时间，与TIME_TO_SEC 互为反函数                   |
| [DATE_ADD 和 ADDDATE](http://c.biancheng.net/mysql/date_add_adddate.html) | 两个函数功能相同，都是向日期添加指定的时间间隔               |
| [DATE_SUB 和 SUBDATE](http://c.biancheng.net/mysql/date_sub_subdate.html) | 两个函数功能相同，都是向日期减去指定的时间间隔               |
| [ADDTIME](http://c.biancheng.net/mysql/addtime.html)         | 时间加法运算，在原始时间上添加指定的时间                     |
| [SUBTIME](http://c.biancheng.net/mysql/subtime.html)         | 时间减法运算，在原始时间上减去指定的时间                     |
| [DATEDIFF](http://c.biancheng.net/mysql/datediff.html)       | 获取两个日期之间间隔，返回参数 1 减去参数 2 的值             |
| [DATE_FORMAT](http://c.biancheng.net/mysql/date_format.html) | 格式化指定的日期，根据参数返回指定格式的值                   |
| [WEEKDAY](http://c.biancheng.net/mysql/weekday.html)         | 获取指定日期在一周内的对应的工作日索引                       |

## 9.4 聚合函数

| 函数名称                                         | 作用                             |
| ------------------------------------------------ | -------------------------------- |
| [MAX](http://c.biancheng.net/mysql/max.html)     | 查询指定列的最大值               |
| [MIN](http://c.biancheng.net/mysql/min.html)     | 查询指定列的最小值               |
| [COUNT](http://c.biancheng.net/mysql/count.html) | 统计查询结果的行数               |
| [SUM](http://c.biancheng.net/mysql/sum.html)     | 求和，返回指定列的总和           |
| [AVG](http://c.biancheng.net/mysql/avg.html)     | 求平均值，返回指定列数据的平均值 |

## 9.5 流程控制函数

| 函数名称                                                     | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [IF(expr1,expr2,expr3)](http://c.biancheng.net/mysql/if.html) | 判断，流程控制。expr1 的值为 TRUE，则返回值为 expr2 。否则返回 expr3 |
| [IFNULL](http://c.biancheng.net/mysql/ifnull.html)（expr1,expr2） | 判断是否为空。例如select ifnull(age,0) from stu where id=0;如果这个学生年龄是null则返回0 |
| [CASE](http://c.biancheng.net/mysql/case.html)               | 搜索语句                                                     |

# 十、SQL练习题：高频 SQL 50 题（基础版）

初学者可以每天做一道，或者每周做一道，提高自己写SQL的能力。

[高频 SQL 50 题（基础版） - 学习计划 - 力扣（LeetCode）全球极客挚爱的技术成长平台](https://leetcode.cn/studyplan/sql-free-50/)