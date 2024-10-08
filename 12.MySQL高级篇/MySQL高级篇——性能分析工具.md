>  **导航：** 
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1\. 数据库服务器的优化步骤](#1.%20%E6%95%B0%E6%8D%AE%E5%BA%93%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E4%BC%98%E5%8C%96%E6%AD%A5%E9%AA%A4)

[2\. 查看系统性能参数](#2.%20%E6%9F%A5%E7%9C%8B%E7%B3%BB%E7%BB%9F%E6%80%A7%E8%83%BD%E5%8F%82%E6%95%B0)

[2.1 SHOW STATUS LIKE '参数'](#2.1%20SHOW%20STATUS%20LIKE%20'%20rel=)

[2.2 查看SQL的查询成本](#2.2%C2%A0%E6%9F%A5%E7%9C%8BSQL%E7%9A%84%E6%9F%A5%E8%AF%A2%E6%88%90%E6%9C%AC)

[3\. 定位执行慢的 SQL：慢查询日志](#4.%20%E5%AE%9A%E4%BD%8D%E6%89%A7%E8%A1%8C%E6%85%A2%E7%9A%84%20SQL%EF%BC%9A%E6%85%A2%E6%9F%A5%E8%AF%A2%E6%97%A5%E5%BF%97)

[3.0 介绍](#4.0%20%E4%BB%8B%E7%BB%8D%C2%A0) 

[3.1 开启慢查询日志参数](#4.1%20%E5%BC%80%E5%90%AF%E6%85%A2%E6%9F%A5%E8%AF%A2%E6%97%A5%E5%BF%97%E5%8F%82%E6%95%B0)

[3.2 查看慢查询次数](#4.2%20%E6%9F%A5%E7%9C%8B%E6%85%A2%E6%9F%A5%E8%AF%A2%E6%AC%A1%E6%95%B0)

[3.5 慢查询日志分析工具：mysqldumpslow](#4.5%20%E6%85%A2%E6%9F%A5%E8%AF%A2%E6%97%A5%E5%BF%97%E5%88%86%E6%9E%90%E5%B7%A5%E5%85%B7%EF%BC%9Amysqldumpslow)

[3.6 关闭慢查询日志](#4.6%20%E5%85%B3%E9%97%AD%E6%85%A2%E6%9F%A5%E8%AF%A2%E6%97%A5%E5%BF%97)

[3.7 删除慢查询日志](#4.7%20%E5%88%A0%E9%99%A4%E6%85%A2%E6%9F%A5%E8%AF%A2%E6%97%A5%E5%BF%97)

[4\. 定位慢查询语句、查看 SQL 执行成本：show profile](#5.%20%E5%AE%9A%E4%BD%8D%E6%85%A2%E6%9F%A5%E8%AF%A2%E8%AF%AD%E5%8F%A5%E3%80%81%E6%9F%A5%E7%9C%8B%20SQL%20%E6%89%A7%E8%A1%8C%E6%88%90%E6%9C%AC%EF%BC%9Ashow%20profile)

[5\. 执行计划表：EXPLAIN](#6.%20%E6%89%A7%E8%A1%8C%E8%AE%A1%E5%88%92%E8%A1%A8%EF%BC%9AEXPLAIN)

[5.1 简介](#6.1%20%E7%AE%80%E4%BB%8B)

[5.2 基本语法](#6.2%20%E5%9F%BA%E6%9C%AC%E8%AF%AD%E6%B3%95)

[5.3 执行计划表介绍](#6.3%20%E6%89%A7%E8%A1%8C%E8%AE%A1%E5%88%92%E8%A1%A8%E4%BB%8B%E7%BB%8D%C2%A0) 

[5.3.1 执行计划各个列的作用（概述）](#5.3.1%20%E6%89%A7%E8%A1%8C%E8%AE%A1%E5%88%92%E5%90%84%E4%B8%AA%E5%88%97%E7%9A%84%E4%BD%9C%E7%94%A8%EF%BC%88%E6%A6%82%E8%BF%B0%EF%BC%89)

[5.3.2 详细介绍](#5.3.2%20%E8%AF%A6%E7%BB%86%E4%BB%8B%E7%BB%8D)

[5.3.2.1 select\_type](#5.3.2.1%20select_type)

[5.3.2.2 key](#5.3.2.2%20key)

[5.3.2.3 type](#5.3.2.3%20type)

[5.3.2.4 Extra](#5.3.2.4%20Extra)

[5.4 EXPLAIN四种输出格式](#7.%20EXPLAIN%E7%9A%84%E8%BF%9B%E4%B8%80%E6%AD%A5%E4%BD%BF%E7%94%A8)

[5.5 SHOW WARNINGS的使用](#7.2%20SHOW%20WARNINGS%E7%9A%84%E4%BD%BF%E7%94%A8)

[6\. 分析优化器执行计划：trace](#%C2%A08.%20%E5%88%86%E6%9E%90%E4%BC%98%E5%8C%96%E5%99%A8%E6%89%A7%E8%A1%8C%E8%AE%A1%E5%88%92%EF%BC%9Atrace)

[7\. MySQL监控分析视图-sys schema](#9.%20MySQL%E7%9B%91%E6%8E%A7%E5%88%86%E6%9E%90%E8%A7%86%E5%9B%BE-sys%20schema)

[7.1 简介](#9.1%20%E7%AE%80%E4%BB%8B)

[7.2 使用场景](#9.2%20%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)

--

## 1\. 数据库服务器的优化步骤

在数据库调优中，我们的目标就是**响应时间更快，吞吐量更大**。利用宏观的**监控工具**和微观的**日志分析**可以帮我们快速找到调优的思路和方式。 

**调优流程：**

1.  **SHOW STATUS**观察服务器状态，是否存在周期性波动；如果存在的话就**缓存优化**；
2.  如果还存在不规则延迟或卡顿的话，就**开启慢查询、explan分析查询语句**；
3.  如果发现sql等待时间长，就**调优服务器参数**；如果发现sql执行时间长，就**索引优化、表优化；**
4.  如果还存在不规则延迟或卡顿的话，就**观察**sql查询是否到瓶颈了；是的话就**读写分离、分库分表。**

**三种分析工具（SQL调优三步骤）：**慢查询、EXPLAN、SHOW PROFLING 

![](https://i-blog.csdnimg.cn/blog_migrate/a213a62cd6ec42230fa2ff016473a895.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/8f4904bc0442115bc6744202d0902b23.png)

整个流程划分成了观察（Show status） 和行动（Action） 两个部分。字母 S 的部分代表观察（会使用相应的分析工具），字母 A 代表的部分是行动（对应分析可以采取的行动）。

![](https://i-blog.csdnimg.cn/blog_migrate/4dbb59ec440592dda70a14e9758d1858.png)

## 2\. 查看系统性能参数

### 2.1 **SHOW STATUS** LIKE '参数'

在MySQL中，可以使用**SHOW STATUS** 语句查询一些MySQL**数据库服务器**的**性能参数**、执行频率。

SHOW STATUS语句语法如下：

```sql
SHOW [GLOBAL|SESSION] STATUS LIKE '参数';
```

示例，查看数据库连接次数和运行时长： 

![](https://i-blog.csdnimg.cn/blog_migrate/342371a77ab8a9a81a5d7f4253ca4623.png)

>  中括号代表可省略。
> 
> 一些常用的性能参数如下：
> 
> **•　Connections：**连接MySQL服务器的次数。
> 
> **•　Uptime：**MySQL服务器的上线时间。重启服务器后会重置。
> 
> •　**Slow\_queries：慢查询的次数**。查询时长超过指定时间，次数越少越好。
> 
> •　Innodb\_rows\_read：Select查询返回的行数
> 
> •　Innodb\_rows\_inserted：执行INSERT操作插入的行数
> 
> •　Innodb\_rows\_updated：执行UPDATE操作更新的行数
> 
> •　Innodb\_rows\_deleted：执行DELETE操作删除的行数
> 
> •　Com\_select：查询操作的次数。
> 
> •　Com\_insert：插入操作的次数。对于批量插入的 INSERT 操作，只累加一次。
> 
> •　Com\_update：更新操作的次数。
> 
> •　Com\_delete：删除操作的次数。
> 
> •　**last\_query\_cost：查询优化器上一个查询的成本**，最近一次删除用到数据页数量。

### 2.2 查看SQL的查询成本

```sql
SHOW STATUS LIKE 'last_query_cost';
```

SQL查询是一个动态的过程，从页加载的角度来看:

**1.缓冲池查询效率优于从磁盘查**

如果页就在数据库**缓冲池**中，那么**效率是最高**的，否则还需要从内存或者磁盘中进行读取，当然针对单个页的读取来说，如果页存在于内存中，会比在磁盘中读取效率高很多.

> MySQL的缓冲池被分为多个不同的缓存池，其中包括：
> 
> -   查询缓存：用来缓存查询结果。
> -   InnoDB缓存池：用来缓存热点表和索引数据页。
> -   MyISAM缓存池：用来缓存表数据块。
> 
> 当缓冲池中已经存储了较多的数据时，MySQL会使用一种叫做缓冲池替换算法的方法，将部分缓存数据替换出去，以腾出空间为新的数据做缓存。
> 
> **MySQL的缓冲池使用的是LRU（最近最少使用）算法**，它会优先缓存最近使用的数据。当缓冲池的空间不足时，MySQL会将最不常用的数据从缓冲池中替换出去，以腾出空间缓存新的数据。

**2.批量顺序查询平均下来每页查询更高**

如果我们从磁盘中对单一页进行随机读，那么效率是很低的(差不多10ms)，而采用**顺序读取**的方式，**批量对页进行读取**，**平均一页的读取效率就会提升**很多，甚至要快于单个页面在内存中的随机读取。

所以说，遇到IO并不用担心，方法找对了，效率还是很高的。我们首先要考虑数据存放的位置，如果是**经常使用的数据就要尽量放到缓冲池**中，其次我们可以充分利用磁盘的吞吐能力，一次性**批量读取数据**，这样单个页的读取效率也就得到了提升。 

> **测试缓冲池缓存已使用的表和索引到内存中，效率高：**查询900001和 900001~9000100查询成本差很多，查询速度差不多
> 
> 学生信息表为例：
> 
> ```sql
> CREATE TABLE `student_info` (
> `id` INT(11) NOT NULL AUTO_INCREMENT,
> `student_id` INT NOT NULL ,
> `name` VARCHAR(20) DEFAULT NULL,
> `course_id` INT NOT NULL ,
> `class_id` INT(11) DEFAULT NULL,
> `create_time` DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
> PRIMARY KEY (`id`)
> ) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
> ```
> 
> 如果我们想要查询 **id=900001** 的记录，然后看下查询成本，我们可以直接在聚簇索引上进行查找：
> 
> ```sql
> SELECT student_id, class_id, NAME, create_time FROM student_info
> WHERE id = 900001;
> ```
> 
> 运行结果（1 条记录，运行时间为 0.042s ）
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3a1f187661400f9367bd3d96f671fc6b.png)
> 
>  然后再看下**查询优化器的成本**，实际上我们**只需要检索一个页**即可：
> 
> ```sql
> SHOW STATUS LIKE 'last_query_cost';
> ```
> 
> ```sql
> 
> +-----------------+----------+
> | Variable_name | Value |
> +-----------------+----------+
> | Last_query_cost | 1.000000 |
> +-----------------+----------+
> ```
> 
> 如果我们想要查询 id 在 **900001** 到 **9000100** 之间的学生记录呢？
> 
> ```sql
> SELECT student_id, class_id, NAME, create_time FROM student_info
> WHERE id BETWEEN 900001 AND 900100;
> ```
> 
> 运行结果（100 条记录，运行时间为 0.046s ）：
> 
> 然后**再看下查询优化器的成本**，这时我们大概需要进行 20 个页的查询。
> 
> ```sql
> mysql> SHOW STATUS LIKE 'last_query_cost';
> +-----------------+-----------+
> | Variable_name | Value |
> +-----------------+-----------+
> | Last_query_cost | 21.134453 |
> +-----------------+-----------+
> ```
> 
> 你能看到页的数量是刚才的 20 倍，但是**查询的效率并没有明显的变化**，实际上这两个 SQL 查询的时间基本上一样，就是因为采用了**顺序读取**的方式将页面一次性加载到**缓冲池**中，然后再进行查找。虽然**页数量**（last\_query\_cost）**增加了不少**，但是通过缓冲池的机制，并**没有增加多少查询时间。**
> 
> **为什么第二次是直接从缓冲池查？**
> 
> 因为mysql缓存淘汰策略lru最近最少使用，会优先缓存最近查询数据，优先淘汰最近最少使用数据。
> 
> 使用场景：它对于比较开销是非常有用的，特别是我们有好几种查询方式可选的时候。

## 3\. 定位执行慢的 SQL：慢查询日志

### 3.0 介绍 

MySQL的慢查询日志，用来**记录**在MySQL中**响应时间超过阀值的语句**，具体指运行时间超过 **long-query\_time值**的SQL，则会被记录到慢查询日志中。 long\_query\_time的默认值为 10，意思是运行10秒以上(不含10秒)的语句，认为是超出了我们的最大忍耐时间值。

它的主要作用是，帮助我们发现那些执行时间特别长的 SOL 查询，并且有针对性地进行优化，从而提高系统的整体效率。当我们的数据库服务器发生阻塞、运行变慢的时候，检查一下慢查询日志，找到那些慢查询，对解决问题很有帮助。比如一条sq执行超过5秒钟，我们就算慢SQL，希望能收集超过5秒的sql，结合explain进行全面分析

默认情况下，MySQL数据库 没有开启慢查询日志 ，需要我们手动来设置这个参数。**如果不是调优需要的话，一般不建议启动该参数**，因为开启慢查询日志会或多或少带来一定的**性能影响**  
慢查询日志支持将日志记录写入文件 

### 3.1 开启慢查询日志参数

**0.慢查询是否开启** 

```sql
show variables like '%slow_query_log';
```

![](https://i-blog.csdnimg.cn/blog_migrate/aeae5053ed5c44070f5f91e2670a443f.png)

> 慢查询日志位置：
> 
> ```sql
> show variables like '%slow_query_log%';
> ```
> 
>  ![](https://i-blog.csdnimg.cn/blog_migrate/807bf3c5782ea4729f4382808c410bb8.png)
> 
>  慢查询阈值：

**1\. 开启慢查询日志slow\_query\_log**

```sql
set global slow_query_log='ON';
```

> 然后我们再来查看下慢查询日志是否开启，以及慢查询日志文件的位置：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/d4af8c55f011ad96e5cecfee8011fb9c.png)
> 
> 你能看到这时慢查询分析已经开启，同时文件保存在 /var/lib/mysql/atguigu02-slow.log 文件
> 
> 中。

**2\. 修改慢查询阈值long\_query\_time**

> 查看慢查询的时间阈值：
> 
> ```sql
> show variables like '%long_query_time%';
> ```
> 
> 查看全局慢查询的时间阈值：
> 
> ```sql
> show global variables like '%long_query_time%';
> ```
> 
>  ![](https://i-blog.csdnimg.cn/blog_migrate/7f93ed884a60ed493e71949e5c7affe9.png)

**临时修改慢查询的时间阈值：** 

当前会话：

```sql
set long_query_time = 1; 
```

全局：

```sql
set global long_query_time = 1; 
```

> 对于 “global” 选项，是全局级别的配置参数。它可以在 MySQL 服务器启动时或 MySQL 安装时在 MySQL 配置文件中设置，或者通过 SET GLOBAL 命令在运行时更改。全局级别的配置参数对所有的 MySQL 连接都有效。

永久修改（重启数据库后依然有效，**不建议永久修改**，仅在优化时候打开，慢查询拖性能） ：

修改my.cnf

```bash
[mysqld]
slow_query_log=ON # 开启慢查询日志的开关
slow_query_log_file=/var/lib/mysql/atguigu-slow.log #慢查询日志的目录和文件名信息
long_query_time=3 #设置慢查询的闽值为3秒，超出此设定值的SQL即被记录到慢查询日志
log_output=FILE
```

> 注意： 
> 
> ```bash
> #测试发现：设置global的方式对当前session的long_query_time失效。对新连接的客户端有效。所以可以一并
> 执行下述语句
> set global long_query_time = 1;    #设置全局慢查询阈值1s
> show global variables like '%long_query_time%';    #全局1s
> set long_query_time=1;
> show variables like '%long_query_time%';    #当前会话10s
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/9a7de620d73478beecbd1292d82942da.png)

### 3.2 查看慢查询次数

查询当前系统中有多少条慢查询记录

```sql
SHOW GLOBAL STATUS LIKE '%Slow_queries%';
```

### 3.5 慢查询日志分析工具：mysqldumpslow

\`mysqldumpslow\`是一个用于分析MySQL慢查询日志的命令行工具。通过解析慢查询日志，可以了解到数据库的性能问题，从而进行优化。

> **查看mysqldumpslow的帮助信息**
> 
> ```
> mysqldumpslow --help
> ```

> mysqldumpslow 命令的具体参数如下：
> 
> -   \-a: 不将数字抽象成N，字符串抽象成S
>     
> -   **\-s: 是表示按照何种方式排序：**
>     
>     -   c: 访问次数
>     -   l: 锁定时间
>     -   r: 返回记录
>     -   **t: 查询时间**
>     -   al:平均锁定时间
>     -   ar:平均返回记录数
>     -   **at:平均查询时间 （默认方式）**
>     -   ac:平均查询次数
> -   **\-t: 即为返回前面多少条的数据；**
>     
> -   \-g: 后边搭配一个正则匹配模式，大小写不敏感的；
>     

> **案例：**
> 
> 举例：按照查询时间排序，查看前五条 慢查询SQL 语句，这样写即可：
> 
> ```sql
> mysqldumpslow -s t -t 5 /var/lib/mysql/atguigu01-slow.log
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/fe72aa1a9171d60a0cc0bf6626f682c7.png)
> 
> 举例，假设想查看最慢的10个查询，可以使用如下命令：
> 
> ```sql
> mysqldumpslow -s t -t 10 /var/log/mysql/mysql-slow.log
> ```
> 
> 这条命令表示按照时间排序，显示最慢的10个查询，/var/log/mysql/mysql-slow.log是MySQL慢查询日志的路径。
> 
> 另外，如果需要筛选特定的查询，可以使用 \`-g\` 参数，比如：
> 
> ```sql
> mysqldumpslow -s t -t 10 -g "SELECT * FROM user" /var/log/mysql/mysql-slow.log
> ```
> 
> 这条命令表示按照时间排序，显示最慢的10个查询，其中关键字为 "SELECT \* FROM user"。
> 
> 总的来说，\`mysqldumpslow\` 命令提供了一种简单快捷的方式帮助开发人员、DBA等分析MySQL慢查询问题，优化数据库的性能。

 **其他常用案例：**

```bash
#得到返回记录集最多的10个SQL
mysqldumpslow -s r -t 10 /var/lib/mysql/atguigu-slow.log

#得到访问次数最多的10个SQL
mysqldumpslow -s c -t 10 /var/lib/mysql/atguigu-slow.log

#得到按照时间排序的前10条里面含有左连接的查询语句
mysqldumpslow -s t -t 10 -g "left join" /var/lib/mysql/atguigu-slow.log

#另外建议在使用这些命令时结合 | 和more 使用 ，否则有可能出现爆屏情况
mysqldumpslow -s r -t 10 /var/lib/mysql/atguigu-slow.log | more
```

### 3.6 关闭慢查询日志

MySQL服务器停止慢查询日志功能有两种方法：

**方式1：永久性方式**

```bash
[mysqld]
slow_query_log=OFF
```

**mysql默认关闭慢查询日志**，或者，把slow\_query\_log一项注释掉 或 删除

```bash
[mysqld]
#slow_query_log =OFF
```

重启MySQL服务，执行如下语句查询慢日志功能。

```bash
SHOW VARIABLES LIKE '%slow%'; #查询慢查询日志所在目录
SHOW VARIABLES LIKE '%long_query_time%'; #查询超时时长
```

**方式2：临时性方式**

使用SET语句来设置。

停止MySQL慢查询日志功能，具体SQL语句如下。

```
SET GLOBAL slow_query_log=off;
```

> golbal全局有效。
> 
> **重启MySQL服务**，使用SHOW语句查询慢查询日志功能信息，发现慢查询日志已经关闭成功。
> 
> ```bash
> SHOW VARIABLES LIKE '%slow%';    #发现关闭成功
> #慢查询阈值
> SHOW VARIABLES LIKE '%long_query_time%';   #10s。前面改的时候没有加global，所以重启服务器后阈值恢复10s。
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/6cf94ae3ed8965bee133ffb5e7e09cbd.png)

### 3.7 删除慢查询日志

**手动删除** 

使用SHOW语句显示慢查询日志信息，具体SQL语句如下。

```
SHOW VARIABLES LIKE `slow_query_log%`;
```

![](https://i-blog.csdnimg.cn/blog_migrate/6c76e7fe9e5f8ee1d98ec571aee1e4ed.png)

从执行结果可以看出，慢查询日志的目录默认为MySQL的数据目录，在该目录下 手动删除慢查询日志文件 即可。

**自动删除** 

使用命令 mysqladmin flush-logs 来重新生成查询日志文件，执行完毕会在数据目录下重新生成慢查询日志文件。

**重新生成慢查询日志文件（直接删除旧的）**

```
mysqladmin -uroot -p flush-logs slow
```

> **提示**
> 
> 慢查询日志都是使用mysqladmin flush-logs命令来**删除重建**的。使用时一定要注意，一旦执行了这个命令，慢查询日志都只存在新的日志文件中，如果需要旧的查询日志，就必须事先备份。

## 4\. 定位慢查询语句、查看 SQL 执行成本：show profile

show profile 是 MySQL 提供的可以用来分析**当前会话中** **SQL 都做了什么、执行的资源消耗工具的情况**，可用于 sql 调优的测量。默认情况下处于关闭状态，并保存最近15次的运行结果。

`SHOW PROFILE` 是一个用于查看会话执行的查询的性能分析信息的 MySQL 命令。它可以帮助开发人员和 DBA **分析查询语句执行时的瓶颈**，并找出哪些部分需要优化。 

**查看配置是否开启profile：** 

```sql
mysql > show variables like 'profiling';
```

> -   **SHOW VARIABLES** 显示了 MySQL 服务器的当前配置变量，包括全局配置变量和会话配置变量，以及它们的值。SHOW VARIABLES 用于查看 MySQL 配置系统参数的详细信息并进行系统参数的修改。
> -   SHOW STATUS 显示服务器的性能参数，包括连接、线程、查询等方面的状态信息，以及它们的值。 

![](https://i-blog.csdnimg.cn/blog_migrate/4175300f4d7caeea1fe02cbcb3d309c0.png)

**开启 show profile:**

```sql
mysql > set profiling = 'ON';
```

![](https://i-blog.csdnimg.cn/blog_migrate/c469b267b74b241c916f7bd6f68ba312.png)

 然后执行相关的查询语句:

```sql
select * from employees
```

**show profiles; 查询当前会话所有查询语句持续时间**

```sql
mysql > show profiles;
```

![](https://i-blog.csdnimg.cn/blog_migrate/733ed2b3203f125609465635472bc518.png)

 **show profile;查询当前会话最近sql语句的执行成本：**

你能看到当前会话一共有 2 个查询。如果我们想要查看最近一次查询的开销，可以使用：

```sql
mysql > show profile;
```

![](https://i-blog.csdnimg.cn/blog_migrate/970823ad7d12dc6ffd4bf75548ae679d.png)

**show profile cpu for 2;查询指定QueryID的cpu信息：**

可以查看指定的 QueryID 的开销，比如 show profile for query 2 。在SHOW PROFILE 中可以查看不同部分的开销，比如 cpu、block.io 等:

```sql
mysql> show profile cpu,block io for query 2
```

![](https://i-blog.csdnimg.cn/blog_migrate/c83b5fb0a2b64ee05516ff42e6542422.png)

 **show profile的常用查询参数：**

① ALL：显示所有的开销信息。

② BLOCK IO：显示块IO开销。

③ CONTEXT SWITCHES：上下文切换开销。

④ CPU：显示CPU开销信息。

⑤ IPC：显示发送和接收开销信息。

⑥ MEMORY：显示内存开销信 息。

⑦ PAGE FAULTS：显示页面错误开销信息。

⑧ SOURCE：显示和Source\_function，Source\_file， Source\_line相关的开销信息。

⑨ SWAPS：显示交换次数开销信息。

**日常开发需注意：**

① `converting HEAP to MyISAM`: 查询结果太大，内存不够，数据往磁盘上搬了。

② `Creating tmp table`：创建临时表。先拷贝数据到临时表，用完后再删除临时表。

③ `Copying to tmp table on disk`：把内存中临时表复制到磁盘上，警惕！

④ `locked`。

如果在show profile诊断结果中出现了以上4条结果中的任何一条，则sql语句需要优化。

> **注意：**
> 
> 不过**SHOW PROFILE命令将被弃用**，我们可以从 **information\_schema 中的 profiling 数据表**进行查看。

## 5\. 执行计划表：EXPLAIN

### 5.1 简介

MySQL的EXPLAIN是一种**分析SQL语句查询性能的工具**。当我们在MySQL中执行SELECT语句时，EXPLAIN可以帮助我们**查看MySQL如何执行这个查询，即执行计划**，包括**使用哪些索引、选择哪些表、以及如何读取数据**等信息。通过分析EXPLAIN的输出结果，我们可以更好地**优化查询语句**，提高查询效率。

EXPLAIN的使用方式非常简单，只需要在执行**SELECT语句**时在**前面加上EXPLAIN关键字**即可，例如：

```sql
EXPLAIN SELECT * FROM my_table WHERE my_column = 'my_value';
```

执行以上命令后，MySQL会返回一张查询执行计划表，其中包含了MySQL执行这个查询的详细信息。我们可以通过分析查询执行计划表来**了解查询的性能瓶颈**，以及如何优化查询语句，从而提高查询性能。  

**注意：** 

-   EXPLAIN不考虑各种Cache
    
-   EXPLAIN不能显示MySQL在执行查询时所作的优化工作
    
-   EXPLAIN不会告诉你关于触发器、存储过程的信息或用户自定义函数对查询的影响情况
    
-   部分统计信息是估算的，并非精确值
    

> **上一步用show profile定位了查询慢的 SQL 之后**，我们就可以使用 **EXPLAIN** 或 DESCRIBE 工具做针对性的**分析查询语句**。DESCRIBE语句的使用方法与EXPLAIN语句是一样的，并且分析结果也是一样的。
> 
> **MySQL中有专门负责优化SELECT语句的优化器模块**，主要功能: 通过计算分析系统中收集到的统计信息，为客户端请求的Query提供**它认为最优的 执行计划** (他认为最优的数据检索方式，但不见得是DBA（数据库管理员）认为是最优的，这部分最耗费时间)。
> 
> 这个**执行计划展示了接下来具体执行查询的方式**，比如多表连接的顺序是什么，对于每个表采用什么访问方法来具体执行查询等等。MySOL为我们提供了 EXPLAIN 语句来帮助我们查看某个查询语句的具体执行计划，大家看懂EXPLAIN 语句的各个输出项，可以有针对性的提升我们查询语句的性能。 

**1\. 能做什么？**

-   表的读取顺序
-   数据读取操作的操作类型
-   哪些索引可以使用
-   哪些索引被实际使用
-   表之间的引用
-   每张表有多少行被优化器查询

**2\. 官网介绍**

[MySQL :: MySQL 5.7 Reference Manual :: 8.8.2 EXPLAIN Output Format](https://dev.mysql.com/doc/refman/5.7/en/explain-output.html "MySQL :: MySQL 5.7 Reference Manual :: 8.8.2 EXPLAIN Output Format")

[MySQL :: MySQL 8.0 Reference Manual :: 8.8.2 EXPLAIN Output Format](https://dev.mysql.com/doc/refman/8.0/en/explain-output.html "MySQL :: MySQL 8.0 Reference Manual :: 8.8.2 EXPLAIN Output Format")

**3\. 版本情况**

-   **MySQL 5.6.3以前只能 EXPLAIN SELECT** ；**MYSQL 5.6.3以后**就可以 EXPLAIN SELECT，**UPDATE， DELETE**
-   在5.7以前的版本中，想要显示 partitions 需要使用 explain partitions 命令；想要显示 filtered 需要使用 explain extended 命令。在5.7版本后，默认explain直接显示partitions和 filtered中的信息。

### 5.2 基本语法

EXPLAIN 或 DESCRIBE语句的语法形式如下：

```sql
EXPLAIN SELECT select_options
#一般指定在查询时不使用缓存
EXPLAIN SELECT SQL_NO_CACHE select_options
#或者
DESCRIBE SELECT select_options
```

> 如果我们想看看某个查询的执行计划的话，可以在具体的查询语句前边加一个 EXPLAIN ，就像这样：
> 
> ```sql
> EXPLAIN SELECT SQL_NO_CACHE * FROM course_base;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/c363c0ed7ca43546e52d578462a07c72.png)
> 
> 输出的上述信息就是所谓的 执行计划。在这个执行计划的辅助下，我们需要知道应该怎样改进自己的查询语句以使查询执行起来更高效。其实除了以 SELECT 开头的查询语句，其余的 DELETE、INSERT、REPLACE 以及UPDATE 语句等都可以加上EXPLAIN，用来查看这些语句的执行计划，只是**平时我们对 SELECT 语句更感兴趣** 

### 5.3 执行计划表介绍 

#### **5.3.1 执行计划各个列的作用（概述）**

<table border="1" cellpadding="1" cellspacing="1" style="width:700px;"><tbody><tr><td style="text-align:center;">id</td><td>每个SELECT子句或者join操作都会被分配一个唯一的编号，编号越小优先级越高，id相同的语句可以被认为是一组。id为NULL表示独立的子查询，子查询优先级都比主查询高。</td></tr><tr><td style="text-align:center;">select_type</td><td>查询的类型。主查询(primary)、普通查询(simple)、联合查询、子查询(subquery)、derived(from表临时子查询)、union(union后查询)、union result()</td></tr><tr><td style="text-align:center;">table</td><td>表名。显示当前这行的数据是哪个表的。</td></tr><tr><td style="text-align:center;">partitions</td><td>匹配的分区信息。如果表未分区则为NULL。</td></tr><tr><td style="text-align:center;"><strong>type</strong></td><td><strong>访问类型，根据索引、全表扫描等方法来执行查询的优化策略。</strong>all（全表扫描），ref（命中非唯一索引），index(没命中索引，扫描索引树再回表)、const（命中主键/唯一索引）、range(范围索引查询)、index_merge(使用多个索引)、&nbsp;system(一行记录时,快速查询)。</td></tr><tr><td style="text-align:center;">possible_keys</td><td><p>可能用到的索引。列出MySQL能够使用哪些索引来查询。</p><p>如果该列只有一个possible_keys，通常意味着这个查询是高效的。</p><p>如果这个列有多个possible_keys，并且MySQL只使用了其中一个，则需要考虑是否需要在该列上增加一个联合索引。</p></td></tr><tr><td style="text-align:center;"><strong>key</strong></td><td><strong>实际上使用的索引。</strong>如果没有明确的指定KEY，MySQL会根据查询条件自动选择最优的索引。</td></tr><tr><td style="text-align:center;"><strong>key_len</strong></td><td>实际使用到索引的字节数长度。越短表示越快，一般表示索引字段越小越好。</td></tr><tr><td style="text-align:center;">ref</td><td>当使用索引列等值查询时，与索引列进行等值匹配的对象信息。常量等值查询const, 表达式/函数使用到时func,关联查询显示关联字段名</td></tr><tr><td style="text-align:center;"><strong>rows</strong></td><td>预估的需要读取的记录条数。数值越小越好，表示结果集越小，查询越高效。</td></tr><tr><td style="text-align:center;">filtered</td><td>某个表经过搜索条件过滤后剩余记录条数的百分比。这个值越小越好，说明可通过索引直接返回数据。</td></tr><tr><td style="text-align:center;"><strong>Extra</strong></td><td>额外信息。看有没有走索引，还是全表扫描了。一般搭配type字段看。Using index(使用到覆盖索引)、Using where(未完全命中索引)、Using temporary(临时表存储结果集.排序/分组会使用)、Using filesort(排序操作未用索引)、Using join buffer(连接条件未用索引)、Impossible where(where约束语句可能有问题导致没有结果集)</td></tr></tbody></table>

#### **5.3.2 详细介绍**

##### **5.3.2.1 select\_type**

**select\_type：**查询的类型，有以下几种取值：

-   SIMPLE：不使用子查询或UNION，不包含UNION ALL的简单SELECT查询。
-   PRIMARY：最外层的SELECT查询。
-   DERIVED：以FROM子句中的子查询方式出现的SELECT语句。
-   UNION：UNION中的第二个或之后的SELECT查询。
-   UNION RESULT：从UNION的结果集中获取数据的SELECT查询。
-   SUBQUERY：不在FROM子句中出现的子查询，通常在SELECT语句中使用。
-   DEPENDENT SUBQUERY：子查询依赖外层查询的结果集。

##### **5.3.2.2 key**

**key：**实际上使用的索引。在MySQL中创建索引时使用的是INDEX关键字，但在EXPLAIN执行计划表中，显示的是KEY，这是因为**MySQL允许在创建索引时指定统计信息**，例如最小值、最大值等，这些**统计信息**在索引中被视为**索引键**（Index key），所以在执行计划表中，显示为KEY。

##### **5.3.2.3 type**

**type：**访问类型，根据索引、全表扫描等方法来执行查询的优化策略。当 type 列的取值不是 Const 时，我们需要重点关注有关索引、缓存的性能调优，对 SQL 语句进行优化，适当修复可能的数据设计问题。

-   **system：一行记录时,快速查询。**只有一行数据即将被查询。这是最快的查询类型，通常出现在系统表的查询中。
-   **const：命中主键或唯一索引。**使用主键或唯一索引查找单个行时使用，此时查询只能返回一行数据。这是一种非常快的查询类型。
-   eq\_ref：连接使用唯一索引查找符合查询条件的数据时使用，每个连接类型都需要使用唯一索引进行访问，比ref执行速度更快。
-   **ref：命中非唯一索引。**使用非唯一索引查找数据时使用，查询结果比eq\_ref大，但仍很快。
-   **range：范围索引查询。**使用索引范围查找数据时使用，可能会查找一定范围内的数据，如使用 BETWEEN 或 > 或 > < 等操作时的查询。
-   **index：没命中索引，扫描非聚簇索引树再回表。**
    -   直接在某个索引树上做条件判断，并且不需要回表。全表扫描没有好的索引适用时使用，相比于全表扫描速度更快。
    -   index是另外一种形式的全表扫描，扫描已有索引树然后回表取数据。和all相比，他要回表随机取数据，因此index不可能会比all快（取同一个表数据），官方手册说它的效率说的比all好，唯一可能的原因在于，按照索引扫描全表的数据是有序的。这样一来，结果不同，也就没法比效率的问题了。
    -   比如：select t3.key1 from t3 where t3.key2 =6 ;当我们创建了联合索引idx\_key1\_key2(key1,key2)时，判断条件key2=6时，其虽然不满足索引的最左前缀原则，但是我们可以遍历idx\_key1\_key2这颗索引树，找到key2=6的记录即可。由于查询结果需要的key1在这个联合索引上，也不需要回表，此时就可以使用index。
-   **all：全表扫描。**扫描整个表以获得需要的数据，速度最慢，必须尽量避免使用。
-   unique\_subquery：在对查询结果进行过滤或使用 IN 操作时，优化器会选择使用此类型的查询，使用了 In 操作符的子查询依赖于外层查询的唯一索引。
-   index\_subquery：使用了 In 操作符但子查询使用的普通索引，而不是唯一索引。
-   range\_check：在使用索引来检查外键参照时使用。
-   index\_merge：使用多个索引。

##### **5.3.2.4 Extra**

-   **using index：**使用了覆盖索引，即不需要回表。查询的几个列正好都在这个聚簇索引树上。覆盖索引参考：[MySQL高级篇——覆盖索引、前缀索引、索引下推、SQL优化、主键设计\_mysql前缀索引-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130804019 "MySQL高级篇——覆盖索引、前缀索引、索引下推、SQL优化、主键设计_mysql前缀索引-CSDN博客")
-   **Using where：**通过where过滤。没完全命中索引，需要回表。例如index(a)，查的是where a=2 and b=3，查b=3时就要回表过滤。
-   **Using index condition：**使用了索引下推。
-   Using temporary：临时表存储结果集.排序/分组会使用
-   Using filesort：排序操作未用索引
-   Using join buffer：连接条件未用索引
-   Impossible where：where约束语句可能有问题导致没有结果集

### 5.4 EXPLAIN四种输出格式

这里谈谈EXPLAIN的输出格式。EXPLAIN可以输出四种格式： `传统格式` ，`JSON格式` ， `TREE格式` 以及 `可视化输出` 。用户可以根据需要选择适用于自己的格式。

1\. 传统格式

传统格式简单明了，输出是一个表格形式，概要说明查询计划。

```
mysql> EXPLAIN SELECT s1.key1, s2.key1 FROM s1 LEFT JOIN s2 ON s1.key1 = s2.key1 WHERE s2.common_field IS NOT NULL;
```

2\. JSON格式

第1种格式中介绍的`EXPLAIN`语句输出中缺少了一个衡量执行好坏的重要属性 —— `成本`。而JSON格式是四种格式里面输出`信息最详尽`的格式，里面包含了执行的成本信息。

-   JSON格式：在EXPLAIN单词和真正的查询语句中间加上 FORMAT=JSON 。

```
EXPLAIN FORMAT=JSON SELECT ....
```

-   id：查询所对应的唯一标识符（id）
-   select\_type：查询类型（type）
-   table：正在访问的表（table\_name）
-   partitions：正在访问的分区（partition\_name）
-   type：使用的访问方法（access\_type）
-   possible\_keys：可能使用的索引（possible\_keys）
-   key：实际使用的索引（key）
-   key\_len：索引长度（key\_length）
-   ref：与索引匹配的列或常数（ref）
-   rows：估计的检索行数（rows）
-   filtered：使用WHERE筛选后，剩余行数的百分比（filtered）
-   Extra：其他信息（extra）

3\. TREE格式

TREE格式是8.0.16版本之后引入的新格式，主要根据查询的 `各个部分之间的关系` 和 `各部分的执行顺序` 来描述如何查询。

```
mysql> EXPLAIN FORMAT=tree SELECT * FROM s1 INNER JOIN s2 ON s1.key1 = s2.key2 WHERE
s1.common_field = 'a'\G
*************************** 1. row ***************************
EXPLAIN: -> Nested loop inner join (cost=1360.08 rows=990)
-> Filter: ((s1.common_field = 'a') and (s1.key1 is not null)) (cost=1013.75
rows=990)
-> Table scan on s1 (cost=1013.75 rows=9895)
-> Single-row index lookup on s2 using idx_key2 (key2=s1.key1), with index
condition: (cast(s1.key1 as double) = cast(s2.key2 as double)) (cost=0.25 rows=1)
1 row in set, 1 warning (0.00 sec)
```

4\. 可视化输出

可视化输出，可以通过MySQL Workbench可视化查看MySQL的执行计划。通过点击Workbench的放大镜图标，即可生成可视化的查询计划。

3\. TREE格式

TREE格式是8.0.16版本之后引入的新格式，主要根据查询的 `各个部分之间的关系` 和 `各部分的执行顺序` 来描述如何查询。

```
mysql> EXPLAIN FORMAT=tree SELECT * FROM s1 INNER JOIN s2 ON s1.key1 = s2.key2 WHERE
s1.common_field = 'a'\G
*************************** 1. row ***************************
EXPLAIN: -> Nested loop inner join (cost=1360.08 rows=990)
-> Filter: ((s1.common_field = 'a') and (s1.key1 is not null)) (cost=1013.75
rows=990)
-> Table scan on s1 (cost=1013.75 rows=9895)
-> Single-row index lookup on s2 using idx_key2 (key2=s1.key1), with index
condition: (cast(s1.key1 as double) = cast(s2.key2 as double)) (cost=0.25 rows=1)
1 row in set, 1 warning (0.00 sec)
```

4\. 可视化输出

可视化输出，可以通过MySQL Workbench可视化查看MySQL的执行计划。通过点击Workbench的放大镜图标，即可生成可视化的查询计划。

![](https://i-blog.csdnimg.cn/blog_migrate/827c593ae22e6dcd4eb524e97d48b31f.png)

上图按从左到右的连接顺序显示表。红色框表示 \`全表扫描\` ，而绿色框表示使用 \`索引查找\` 。对于每个表， 显示使用的索引。还要注意的是，每个表格的框上方是每个表访问所发现的行数的估计值以及访问该表的成本。 

### 5.6 自测练习

#### 5.6**.1 练习题和答案解析**

> 看不懂看参考：
> 
> [MySQL高级篇——性能分析工具\_mysql分析工具-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130355955 "MySQL高级篇——性能分析工具_mysql分析工具-CSDN博客")

**假设：**表a,b,c,d四个字段，创建索引(a),(b),(c),(a,b),(a,c)(a,b,c)

```sql
explain select * from test + 下面条件
```

| Where语句 | 索引是否被使用 | 使用到哪些列 |
| --- | --- | --- |
| where a = 3 | 
Y。命中非唯一索引。

如果是select a，则命中覆盖索引

 | a, b, c |
| where a = 3 and b =5 | Y。命中非唯一索引。

如果是select a,b，则命中覆盖索引

 | a, b, c |
| where a = 3 and b = 5 and c =4 | Y。命中非唯一索引。

如果是select a,b,c，则命中覆盖索引

 | a, b, c |
| where b=3 | N。不符合最佳左前缀原则 |  |
| where b=3 and c= 4 | Y。没完全命中索引，即using where | b |
| where d = 4 | N。没命中索引，不符合最佳左前缀原则 |  |
| where c = 3 and d =5 | Y。没完全命中索引 | c |
| where a = 3 and b> 4 and c= 5 | 

Y。范围查询+索引下推

（idx\_abc树上a精准,b范围过滤后条件判断c，

然后回表查a,b,c,d）

 | a, b, c |
| where a is null and b is not null | 

Y。索引下推。如果是select a,b,c,，

则Using where; Using index，没完全命中索引，

is not null导致索引失效

 | a, b, c |
| where a <>3 | 

N。全表扫描。

没覆盖索引时，不等于导致索引失效

 |  |
| where abs(a)=3 | N。全表扫描。函数导致索引失效 |  |
| 

**b改为varchar类型后：**

where a =3 and b like 'kk%' and c=4

 | Y。范围查询+索引下推 | a, b, c |
| 

where a = 3 and b like 'kk' and c = 4

 | 

Y。索引下推。

注意like后没有通配符所以不是范围查询

 | a, b, c |
| where a = 3 and b like '%kk%' and c= 4 | Y。索引下推。如果是select a,b,c,，

则Using where; Using index，没完全命中索引，

左模糊查询导致索引失效。

 | a, b, c |
| where a = 3 and b like 'k%kk%' | Y。索引下推。 | a, b, c |

#### 5.6**.2 验证**

##### 5.6.2.1 准备数据 

准备表和数据： 

```sql
-- 删除test表（如果存在）
DROP TABLE IF EXISTS test;

-- 创建test表
CREATE TABLE test (
    id INT PRIMARY KEY AUTO_INCREMENT,
    a INT,
    b INT,
    c INT,
    d INT
);

-- 插入20条数据
INSERT INTO test (a, b, c, d) VALUES
(1, 10, 100, 1000),
(2, 20, 200, 2000),
(3, 30, 300, 3000),
(4, 40, 400, 4000),
(5, 50, 500, 5000),
(6, 60, 600, 6000),
(7, 70, 700, 7000),
(8, 80, 800, 8000),
(9, 90, 900, 9000),
(10, 100, 1000, 10000),
(11, 110, 1100, 11000),
(12, 120, 1200, 12000),
(13, 130, 1300, 13000),
(14, 140, 1400, 14000),
(15, 150, 1500, 15000),
(16, 160, 1600, 16000),
(17, 170, 1700, 17000),
(18, 180, 1800, 18000),
(19, 190, 1900, 19000),
(20, 200, 2000, 20000);
```

创建索引：

```sql
-- 创建单列索引
CREATE INDEX idx_a ON test(a);
CREATE INDEX idx_b ON test(b);
CREATE INDEX idx_c ON test(c);

-- 创建复合索引
CREATE INDEX idx_a_b ON test(a, b);
CREATE INDEX idx_a_c ON test(a, c);
CREATE INDEX idx_a_b_c ON test(a, b, c);
```

查看所有索引：

```sql
SHOW INDEX FROM test;
```

##### 5.6.2.2 **测试1：命中**覆盖索引

```sql
EXPLAIN SELECT
	a,b,c
FROM
	test 
WHERE
	a = 3 
	AND b = 5 
	AND c =4
```

![](https://i-blog.csdnimg.cn/blog_migrate/4e5f79df086ae8520fdd6a595e095f61.png)

> **解读：**
> 
> -   **ref：**命中了非唯一索引；
> -   **using index：**使用了覆盖索引，即不需要回表；
> -   **key是idx\_a\_b\_c：**命中了idx\_a\_b\_c这个索引

##### 5.6.2.3 测试2：命中索引，需要回表

```sql
EXPLAIN SELECT
	*
FROM
	test 
WHERE
	a = 3 
	AND b = 5 
	AND c =4
```

![](https://i-blog.csdnimg.cn/blog_migrate/06c073492c53902221c9594185610b94.png)

> **解读：**
> 
> -   **ref：**命中了非唯一索引；
> -   **key是idx\_a\_b\_c：**命中了idx\_a\_b\_c这个索引

### 5.5 SHOW WARNINGS的使用

在MySQL中，SHOW WARNINGS是一个可以查看最近一次执行的语句中产生的警告信息的命令。当MySQL执行语句时，如果发现一些不符合预期的情况，会产生一些警告信息。这些警告信息可以包括非致命性错误，例如某些类型的数据不能隐式转换或某些数据截断等。

当我们执行SHOW WARNINGS命令时，MySQL会返回警告信息的详细列表，包括：

-   Warning：该警告的类型
-   Level：该警告的级别，通常为Note、Warning或Error
-   Code：警告的返回代码
-   Message：警告信息的内容

可以使用SELECT的方式来查看最近一次操作的警告信息：

```sql
SHOW WARNINGS;
```

也可以配合使用INSERT、UPDATE、DELETE、ALTER TABLE等命令，检查某个具体操作产生的警告信息：

```sql
INSERT INTO my_table (name, age) VALUES ('John Doe', 150);
SHOW WARNINGS;
```

在开发和调试的过程中，SHOW WARNINGS对于定位和解决某些问题非常有用，例如数据截断、类型转换等问题。

## 6\. 分析优化器执行计划：trace

在MySQL中，可以使用trace命令来进行优化器执行计划的跟踪和分析。trace命令可以显示MySQL优化器在生成执行计划时所采取的决策，包括哪些表被处理，以及使用哪些索引、算法等。

使用trace命令需要先启用general\_log和performance\_schema两个系统变量，其次需要使用SET语句来设置一些参数，例如trace-unique-check、trace-max-protocol、trace-protocol、trace-feature、trace-feature-check等。设置完成后，可以通过SET global trace\_format='json'语句来选择输出结果的格式。

下面是对使用trace命令的一个简单示例：

首先，设置参数：

```sql
SET @trace_feature = 'qa';
SET @max_execution_time=50000;
SET @trace_level = '+ddl,+engine';
SET @trace_feature_check = 1;
SET @trace_unique_check = 1;
SET @trace_protocol = 1;
SET @trace_max_protocol = 6;
```

然后，启用general\_log和performance\_schema：

```sql
SET global general_log = on;
SET global performance_schema = on;
```

接着，执行查询并查看结果：

```sql
SELECT *
FROM my_table
WHERE my_column = 'some_value';
SHOW SESSION STATUS LIKE 'Last_Query_Plan';
```

最后，关闭general\_log和performance\_schema：

```sql
SET global general_log = off;
SET global performance_schema = off;
```

在trace输出中，我们可以看到优化器在执行计划中使用的索引、执行算法、行数估计等细节信息。通过分析trace结果，我们可以找到一些性能问题的根源，并进行相应的调整和优化。但要注意，trace命令可能会带来额外的性能消耗和IO开销，不应该在生产环境中长期启用。

## 7\. MySQL监控分析视图-sys schema

### 7.1 简介

MySQL在8.0版本引入了sys schema，该模式包含用于监视和分析MySQL服务器性能的视图和函数。sys schema提供了一组易于使用的视图和函数，可以帮助我们更好地理解和分析MySQL数据库的行为和性能。

以下是sys schema中一些常用的监控分析视图：

-   sys.statements\_with\_sorting: 显示哪些语句使用了排序操作，包括使用哪些排序操作、每个语句排序的次数以及排序操作的资源消耗。
-   sys.statements\_with\_runtimes\_in\_95th\_percentile: 显示执行时间最长的语句。
-   sys.io\_global\_by\_file\_by\_bytes: 显示每个文件的磁盘IO字节数，可以用来检测IO瓶颈。
-   sys.memory\_by\_host\_by\_current\_bytes: 显示每个客户端的当前内存使用情况，可以用于检测内存泄漏或内存占用高的情况。
-   sys.waits\_global\_by\_latency: 显示哪些等待操作最耗费时间，可以帮助我们找到性能问题的瓶颈所在。
-   sys.processlist: 显示当前正在运行的线程和进程的信息，包括执行的语句、查询ID、用户、主机、线程ID和状态等信息。

总的来说，sys schema中包含的视图和函数为我们提供了更深入的MySQL性能分析和监控功能，可以帮助我们更好地理解MySQL数据库的行为和性能瓶颈。 

1.  **主机相关**：以host\_summary开头，主要汇总了IO延迟的信息。
2.  **Innodb相关**：以innodb开头，汇总了innodb buffer信息和事务等待innodb锁的信息。
3.  **I/o相关**：以io开头，汇总了等待I/O、I/O使用量情况。
4.  **内存使用情况**：以memory开头，从主机、线程、事件等角度展示内存的使用情况
5.  **连接与会话信息**：processlist和session相关视图，总结了会话相关信息。
6.  **表相关**：以schema\_table开头的视图，展示了表的统计信息。
7.  **索引信息**：统计了索引的使用情况，包含冗余索引和未使用的索引情况。
8.  **语句相关**：以statement开头，包含执行全表扫描、使用临时表、排序等的语句信息。
9.  **用户相关**：以user开头的视图，统计了用户使用的文件I/O、执行语句统计信息。
10.  **等待事件相关信息**：以wait开头，展示等待事件的延迟情况。

### 7.2 使用场景

索引情况

```sql
#1. 查询冗余索引
select * from sys.schema_redundant_indexes;
#2. 查询未使用过的索引
select * from sys.schema_unused_indexes;
#3. 查询索引的使用情况
select index_name,rows_selected,rows_inserted,rows_updated,rows_deleted
from sys.schema_index_statistics where table_schema='dbname';
```

表相关

```sql
# 1. 查询表的访问量
select table_schema,table_name,sum(io_read_requests+io_write_requests) as io from
sys.schema_table_statistics group by table_schema,table_name order by io desc;
# 2. 查询占用bufferpool较多的表
select object_schema,object_name,allocated,data
from sys.innodb_buffer_stats_by_table order by allocated limit 10;
# 3. 查看表的全表扫描情况
select * from sys.statements_with_full_table_scans where db='dbname';
```

语句相关

```sql
#1. 监控SQL执行的频率
select db,exec_count,query from sys.statement_analysis
order by exec_count desc;
#2. 监控使用了排序的SQL
select db,exec_count,first_seen,last_seen,query
from sys.statements_with_sorting limit 1;
#3. 监控使用了临时表或者磁盘临时表的SQL
select db,exec_count,tmp_tables,tmp_disk_tables,query
from sys.statement_analysis where tmp_tables>0 or tmp_disk_tables >0
order by (tmp_tables+tmp_disk_tables) desc;
```

IO相关

```sql
#1. 查看消耗磁盘IO的文件
select file,avg_read,avg_write,avg_read+avg_write as avg_io
from sys.io_global_by_file_by_bytes order by avg_read limit 10;
```

Innodb 相关

```sql
#1. 行锁阻塞情况
select * from sys.innodb_lock_waits;
```