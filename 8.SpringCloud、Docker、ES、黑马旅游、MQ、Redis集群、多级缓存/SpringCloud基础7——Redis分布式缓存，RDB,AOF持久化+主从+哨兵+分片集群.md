>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1.Redis持久化](#1.Redis%E6%8C%81%E4%B9%85%E5%8C%96)

[1.0.Redis持久化的意义](#1.0.Redis%E6%8C%81%E4%B9%85%E5%8C%96%E7%9A%84%E6%84%8F%E4%B9%89%C2%A0) 

[1.1.数据备份文件RDB持久化方案](#1.1.RDB%E6%8C%81%E4%B9%85%E5%8C%96)

[1.1.1.执行时机](#1.1.1.%E6%89%A7%E8%A1%8C%E6%97%B6%E6%9C%BA)

[1.1.2.RDB原理](#1.1.2.RDB%E5%8E%9F%E7%90%86)

[1.1.3.小结，bgsave流程、执行时间、缺点](#1.1.3.%E5%B0%8F%E7%BB%93)

[1.2.追加文件AOF持久化方案](#1.2.AOF%E6%8C%81%E4%B9%85%E5%8C%96)

[1.2.1.AOF原理](#1.2.1.AOF%E5%8E%9F%E7%90%86)

[1.2.2.AOF配置](#1.2.2.AOF%E9%85%8D%E7%BD%AE)

[1.2.3.AOF文件重写](#1.2.3.AOF%E6%96%87%E4%BB%B6%E9%87%8D%E5%86%99)

[1.3.RDB与AOF对比](#1.3.RDB%E4%B8%8EAOF%E5%AF%B9%E6%AF%94)

[2.Redis主从](#2.Redis%E4%B8%BB%E4%BB%8E)

[2.0.介绍](#2.1.%E6%90%AD%E5%BB%BA%E4%B8%BB%E4%BB%8E%E6%9E%B6%E6%9E%84)

[2.1.搭建主从集群](#2.1.%E6%90%AD%E5%BB%BA%E4%B8%BB%E4%BB%8E%E9%9B%86%E7%BE%A4)

[2.1.1.集群结构](#2.1.1.%E9%9B%86%E7%BE%A4%E7%BB%93%E6%9E%84)

[2.1.2.准备实例和配置](#2.1.2.%E5%87%86%E5%A4%87%E5%AE%9E%E4%BE%8B%E5%92%8C%E9%85%8D%E7%BD%AE)

[2.1.3.启动](#2.1.3.%E5%90%AF%E5%8A%A8)

[2.1.4.开启主从关系](#2.1.4.%E5%BC%80%E5%90%AF%E4%B8%BB%E4%BB%8E%E5%85%B3%E7%B3%BB)

[2.1.5.测试读写分离](#2.1.5.%E6%B5%8B%E8%AF%95)

[2.2.主从数据同步原理](#2.2.%E4%B8%BB%E4%BB%8E%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5%E5%8E%9F%E7%90%86)

[2.2.1.全量同步](#2.2.1.%E5%85%A8%E9%87%8F%E5%90%8C%E6%AD%A5)

[2.2.2.增量同步](#2.2.2.%E5%A2%9E%E9%87%8F%E5%90%8C%E6%AD%A5)

[2.2.3.repl\_backlog原理](#2.2.3.repl_backlog%E5%8E%9F%E7%90%86)

[2.3.主从同步优化](#2.3.%E4%B8%BB%E4%BB%8E%E5%90%8C%E6%AD%A5%E4%BC%98%E5%8C%96)

[2.4.小结，全量同步和增量同步区别、执行时间](#2.4.%E5%B0%8F%E7%BB%93)

[3.Redis哨兵](#3.Redis%E5%93%A8%E5%85%B5)

[3.1.哨兵原理](#3.1.%E5%93%A8%E5%85%B5%E5%8E%9F%E7%90%86)

[3.1.1.集群结构和作用](#3.1.1.%E9%9B%86%E7%BE%A4%E7%BB%93%E6%9E%84%E5%92%8C%E4%BD%9C%E7%94%A8)

[3.1.2.集群监控原理](#3.1.2.%E9%9B%86%E7%BE%A4%E7%9B%91%E6%8E%A7%E5%8E%9F%E7%90%86)

[3.1.3.集群故障恢复原理，选举、切换新master](#3.1.3.%E9%9B%86%E7%BE%A4%E6%95%85%E9%9A%9C%E6%81%A2%E5%A4%8D%E5%8E%9F%E7%90%86)

[3.1.4.小结，Sentinel健康、故障转移、通知](#3.1.4.%E5%B0%8F%E7%BB%93)

[3.2.搭建哨兵集群](#3.2.%E6%90%AD%E5%BB%BA%E5%93%A8%E5%85%B5%E9%9B%86%E7%BE%A4)

[3.2.1.集群结构](#3.2.1.%E9%9B%86%E7%BE%A4%E7%BB%93%E6%9E%84)

[3.2.2.准备实例和配置](#3.2.2.%E5%87%86%E5%A4%87%E5%AE%9E%E4%BE%8B%E5%92%8C%E9%85%8D%E7%BD%AE)

[3.2.3.启动3个redis实例](#3.2.3.%E5%90%AF%E5%8A%A83%E4%B8%AAredis%E5%AE%9E%E4%BE%8B)

[3.2.4.测试](#3.2.4.%E6%B5%8B%E8%AF%95)

[3.3.RedisTemplate](#3.3.RedisTemplate)

[3.3.1.导入Demo工程](#3.3.1.%E5%AF%BC%E5%85%A5Demo%E5%B7%A5%E7%A8%8B)

[3.3.2.引入redis的starter依赖](#3.3.2.%E5%BC%95%E5%85%A5%E4%BE%9D%E8%B5%96)

[3.3.3.配置Redis地址](#3.3.3.%E9%85%8D%E7%BD%AERedis%E5%9C%B0%E5%9D%80)

[3.3.4.配置读写分离](#3.3.4.%E9%85%8D%E7%BD%AE%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB)

[3.3.5.测试读写分离、主从自动切换](#3.3.5.%E6%B5%8B%E8%AF%95%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB%E3%80%81%E4%B8%BB%E4%BB%8E%E8%87%AA%E5%8A%A8%E5%88%87%E6%8D%A2)

[4.Redis分片集群](#4.Redis%E5%88%86%E7%89%87%E9%9B%86%E7%BE%A4)

[4.0.分片集群概述](#4.1.%E6%90%AD%E5%BB%BA%E5%88%86%E7%89%87%E9%9B%86%E7%BE%A4)

[4.1.搭建分片集群](#4.1.%E6%90%AD%E5%BB%BA%E5%88%86%E7%89%87%E9%9B%86%E7%BE%A4%C2%A0) 

[4.1.1.集群结构](#4.1.1.%E9%9B%86%E7%BE%A4%E7%BB%93%E6%9E%84)

[4.1.2.准备实例和配置](#4.1.2.%E5%87%86%E5%A4%87%E5%AE%9E%E4%BE%8B%E5%92%8C%E9%85%8D%E7%BD%AE)

[4.1.3.启动](#4.1.3.%E5%90%AF%E5%8A%A8)

[4.1.4.创建集群](#4.1.4.%E5%88%9B%E5%BB%BA%E9%9B%86%E7%BE%A4)

[4.1.5.集群常用命令](#4.1.5.%E6%B5%8B%E8%AF%95)

[4.1.6.集群模式下连接节点必须加“-c”](#4.1.6.%E9%9B%86%E7%BE%A4%E6%A8%A1%E5%BC%8F%E4%B8%8B%E8%BF%9E%E6%8E%A5%E8%8A%82%E7%82%B9%E5%BF%85%E9%A1%BB%E5%8A%A0%E2%80%9C-c%E2%80%9D)

[4.2.散列插槽](#4.2.%E6%95%A3%E5%88%97%E6%8F%92%E6%A7%BD)

[4.2.1.插槽原理](#4.2.1.%E6%8F%92%E6%A7%BD%E5%8E%9F%E7%90%86)

[4.2.1.小结，插槽流程、同类数据通过{}插槽绑定到同实例](#4.2.1.%E5%B0%8F%E7%BB%93)

[4.3.集群伸缩](#4.3.%E9%9B%86%E7%BE%A4%E4%BC%B8%E7%BC%A9)

[4.3.0.操作集群的命令](#4.3.0.%E6%93%8D%E4%BD%9C%E9%9B%86%E7%BE%A4%E7%9A%84%E5%91%BD%E4%BB%A4%C2%A0) 

[4.3.1.需求分析，添加节点到集群、分配插槽](#4.3.1.%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90)

[4.3.2.创建新的redis实例](#4.3.2.%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84redis%E5%AE%9E%E4%BE%8B)

[4.3.3.添加新节点到redis](#4.3.3.%E6%B7%BB%E5%8A%A0%E6%96%B0%E8%8A%82%E7%82%B9%E5%88%B0redis)

[4.3.4.转移插槽](#4.3.4.%E8%BD%AC%E7%A7%BB%E6%8F%92%E6%A7%BD)

[4.4.故障转移](#4.4.%E6%95%85%E9%9A%9C%E8%BD%AC%E7%A7%BB)

[4.4.1.自动故障转移](#4.4.1.%E8%87%AA%E5%8A%A8%E6%95%85%E9%9A%9C%E8%BD%AC%E7%A7%BB)

[4.4.2.手动故障转移、指定master实例](#4.4.2.%E6%89%8B%E5%8A%A8%E6%95%85%E9%9A%9C%E8%BD%AC%E7%A7%BB)

[4.5.RedisTemplate访问分片集群](#4.5.RedisTemplate%E8%AE%BF%E9%97%AE%E5%88%86%E7%89%87%E9%9B%86%E7%BE%A4)

--

## 1.Redis持久化

### 1.0.Redis持久化的意义 

redis持久化的意义，在于**数据备份和故障恢复**。

比如你部署了一个redis，作为cache缓存，当然也可以保存一些较为重要的数据。Redis数据存在内容中，如果没有持久化的话，redis遇到灾难性故障的时候，就会丢失所有的数据。如果通过**将数据持久化在磁盘上**，然后**定期同步和备份到一些云存储服务**上去，那么就可以保证数据不丢失全部，还是可以恢复一部分数据回来的。

![](https://i-blog.csdnimg.cn/blog_migrate/c120bd1f0021359f62538681cc3ac2e1.png)

**redis持久化+ 备份：**一般将redis数据从内存存储到磁盘。然后将磁盘数据备份一份即将数据上传到云服务器S3 或 ODPS上即可。如果左边的redis进程坏了并且磁盘也坏了，此时可以在另一台服务器启动该redis，然后将云服务器上的数据copy一份到磁盘上，redis进程在启动过程中会从磁盘加载到内存中。

Redis有**两种持久化方案：**

-   **RDB持久化**
-   **AOF持久化**

### 1.1.**数据备份文件**RDB持久化方案

RDB全称**Redis Database Backup file（Redis数据备份文件**，backup译为备份，支援**）**，也被叫做**Redis数据快照**。简单来说就是把内存中的所有**数据都记录到磁盘中**。当Redis实例**故障重启**后，**从磁盘读取快照文件**，恢复数据。快照文件称为RDB文件，**默认是保存在当前运行目录**。

#### 1.1.1.执行时机

RDB持久化在四种情况下会执行：

-   执行save命令
-   执行bgsave命令
-   Redis停机时
-   触发RDB条件时

**1）save命令**

执行下面的命令，可以立即执行一次RDB：

![image-20210725144536958](https://i-blog.csdnimg.cn/blog_migrate/1749430496736848f798489b18f68776.png)

save命令会导致**主进程执行RDB**，这个过程中**其它所有命令都会被阻塞**。只有在数据迁移时可能用到。

**2）bgsave命令**

下面的命令可以**异步**执行RDB：

![image-20210725144725943](https://i-blog.csdnimg.cn/blog_migrate/33b0da0bc397d1ca89df38530d5d073f.png)

这个命令执行后会**开启独立进程完成RDB**，**主进程**可以持续处理用户请求，**不受影响**。

**3）停机时**

Redis**停机时会执行一次save命令**，实现RDB持久化。

**4）触发RDB条件**

Redis**内部有触发RDB的机制**，可以在redis.conf文件中找到，格式如下：

```bash
cd /usr/local/redis-4.0.0
vim redis.conf
```

```bash
# 900秒内，如果至少有1个key被修改，则执行bgsave ， 如果是save "" 则表示禁用RDB
save 900 1  
save 300 10  
save 60 10000 
```

redis服务端自动RDB： 

![](https://i-blog.csdnimg.cn/blog_migrate/4166c46f8702b2c2875e7f3ddb41f71d.png) **RDB的其它配置**也可以在redis.conf文件中设置： 

```bash
# 是否压缩 ,建议不开启，压缩也会消耗cpu，磁盘的话不值钱
rdbcompression yes

# RDB文件名称
dbfilename dump.rdb  

# 文件保存的路径目录
dir ./ 
```

#### 1.1.2.RDB原理

**bgsave开始时会fork主进程得到子进程**，**子进程共享主进程的内存数据**。完成**fork后**读取内存数据并**写入 RDB 文件**。在fork时主进程是阻塞的。

**fork**采用的是**copy-on-write技术：**

-   当主进程执行读操作时，访问共享内存。在linux中，主进程只能操作**虚拟内存**，不能操作物理内存，操作系统会维护**虚拟内存到物理内存的映射关系表（即页表）**。当进行写操作时，物理内存会拷贝**数据副本**，主进程在数据副本实行读写。
-   当主进程执行写操作时，则会**拷贝一份页表到子进程**，实现了内存空间共享，根据页表的映射关系执行写操作。

![image-20210725151319695](https://i-blog.csdnimg.cn/blog_migrate/9da8783d93e5fedf97bf8a1ad5d5b225.png)

#### 1.1.3.小结，bgsave流程、执行时间、缺点

**RDB方式bgsave的基本流程？**

-   **fork主进程得到一个子进程**，共享内存空间
-   子进程读取内存数据并**写入新的RDB文件**
-   用新RDB文件**替换旧的RDB文件**

**RDB会在什么时候执行？save 60 1000代表什么含义？**

-   默认是服务停止时
-   代表60秒内至少执行1000次修改则触发RDB

**RDB的缺点？**

-   RDB执行**间隔时间长**，**两次RDB之间写入数据有丢失的风险**
-   fork子进程、压缩、写出RDB文件都比较**耗时**

### 1.2.追加文件AOF持久化方案

#### 1.2.1.AOF原理

AOF全称为**Append Only File（追加文件）**。**Redis**处理的**每一个写命令都会记录在AOF文件**，可以看做是**命令日志文件**。

![image-20210725151543640](https://i-blog.csdnimg.cn/blog_migrate/ec7ea1757768a376eb333b1b9f98149f.png)

#### 1.2.2.AOF配置

AOF**默认是关闭的**，需要修改redis.conf配置文件来开启AOF：

```bash
# 是否开启AOF功能，默认是no
appendonly yes
# AOF文件的名称
appendfilename "appendonly.aof"
```

AOF的命令记录的**频率**也可以通过redis.conf文件来配：

```bash
# 表示每执行一次写命令，立即记录到AOF文件。牺牲性能绝对保证数据安全性
#appendfsync always 
# 默认。写命令执行完先放入AOF缓冲区，然后表示每隔1秒将缓冲区数据写到AOF文件，是默认方案。内存方式读写，对性能有帮助，最多会丢失一秒钟内数据
appendfsync everysec 
# 写命令执行完先放入AOF缓冲区，由操作系统决定何时将缓冲区内容写回磁盘。安全性最差，还不如RDB用快照文件存读数据安全。
#appendfsync no
```

**三种策略对比：**

![image-20210725151654046](https://i-blog.csdnimg.cn/blog_migrate/03abb848c3c579ecbdae8d3ec8bbcde9.png)

**实现AOF：**

redis.conf先禁用RDB、删除RDB文件：

![](https://i-blog.csdnimg.cn/blog_migrate/df702e0b183b1f83f023fc556adbb7bc.png) ![](https://i-blog.csdnimg.cn/blog_migrate/0b383d1c9138ede9e309d00208db1920.png)

 配置AOF：

![](https://i-blog.csdnimg.cn/blog_migrate/b871ebbbfded52b7ed727a6919400ce4.png)

![](https://i-blog.csdnimg.cn/blog_migrate/bb0957f6ac3beffc952ac909dd66e289.png)

 存数据：

![](https://i-blog.csdnimg.cn/blog_migrate/e6c6ced5d5257f9580e2153ccf3f3a25.png)

出现了aof文件 

![](https://i-blog.csdnimg.cn/blog_migrate/84723725f652aefe56edd74be3ef82c1.png)

> aof是记录所有命令、rdb是记录各记录的值，所以**aof文件会比rdb文件大很多**。 

#### 1.2.3.AOF文件重写

因为是**记录命令**，**AOF文件会比RDB文件大的多**。而且AOF会记录**对同一个key的多次写操作**，但**只有最后一次写操作才有意义**。通过**执行bgrewriteaof命令**，可以**让AOF文件执行重写功能**，用最少的命令达到相同效果。

![](https://i-blog.csdnimg.cn/blog_migrate/8eddd022dcf26eb6a82a8e1b3e312d6b.png)

 如图，AOF原本有三个命令，但是`set num 123 和 set num 666`都是对num的操作，第二次会覆盖第一次的值，因此第一个命令记录下来没有意义。

所以**重写命令**后，AOF文件内容就是：**`mset name jack num 666`**

**Redis**也会在触发**阈值**时**自动去重写AOF文件**。阈值也可以在redis.conf中配置：

```
# AOF文件比上次文件 增长超过多少百分比则触发重写
auto-aof-rewrite-percentage 100
# AOF文件体积最小多大以上才触发重写 
auto-aof-rewrite-min-size 64mb 
```

### 1.3.RDB与AOF对比

RDB和AOF各有自己的优缺点，如果对数据安全性要求较高，在实际开发中往往会**结合**两者来使用。

![image-20210725151940515](https://i-blog.csdnimg.cn/blog_migrate/14f927e77f29bcae2d93444f398e04e6.png)

> 数据恢复优先级是两个方案同时用会优先使用aof文件恢复。 

## 2.Redis主从

### 2.0.介绍

**主从的好处：** 

1.  **数据备份**，主从复制实现了数据的热备，是除了持久化机制之外的另外一种数据备份方式。
2.  **读写分离**，使数据库能支撑更大的并发。在报表中尤其重要。由于部分报表sql语句非常的慢，导致锁表，影响前台服务。如果前台使用master，报表使用slave，那么报表sql将不会造成前台锁，保证了前台速度。
3.  **负载均衡**，在主从复制的基础上，配合读写分离机制，可以由主节点提供写服务，从节点提供服务。在读多写少的场景中，可以增加从节点来分担redis-server读操作的负载能力，从而大大提高redis-server的并发量
4.  **保证高可用**，作为后备数据库，如果主节点出现故障后，可以切换到从节点继续工作，保证redisserver的高可用。

### 2.1.搭建主从集群

#### 2.1.1.集群结构

我们搭建的主从集群结构如图：

![image-20210630111505799](https://i-blog.csdnimg.cn/blog_migrate/15a8f016cecbe63c03a525791bd55b5a.png)

共包含三个节点，一个主节点，两个从节点。

这里我们会在同一台虚拟机中开启3个redis实例，模拟主从集群，信息如下：

| IP | PORT | 角色 |
| --- | --- | --- |
| 192.168.150.101 | 7001 | master |
| 192.168.150.101 | 7002 | slave |
| 192.168.150.101 | 7003 | slave |

#### 2.1.2.准备实例和配置

要在同一台虚拟机开启3个实例，必须准备三份不同的配置文件和目录，配置文件所在目录也就是工作目录。

**1）创建目录**

我们在**Linux的tmp目录下创建三个文件夹**，名字分别叫**7001、7002、7003：**

```bash
# 进入/tmp目录
cd /tmp
# 创建目录
mkdir 7001 7002 7003
```

如图：

![image-20210630113929868](https://i-blog.csdnimg.cn/blog_migrate/593a5353c2cea54ee5b042c97c53741f.png)

**2）恢复原始配置**

修改redis-6.2.4/**redis.conf文件**，将其中的持久化模式改为**默认的RDB模式**，**AOF保持关闭状态**。

`# 开启RDB
# save ""
save 3600 1
save 300 100
save 60 10000

# 关闭AOF
appendonly no` 

**3）拷贝配置文件到每个实例目录**

然后将redis-6.2.4/redis.conf文件拷贝到三个目录中（在/tmp目录执行下列命令）：

`# 方式一：逐个拷贝
cp redis-6.2.4/redis.conf 7001
cp redis-6.2.4/redis.conf 7002
cp redis-6.2.4/redis.conf 7003
# 方式二：管道组合命令，一键拷贝
#echo 7001 7002 7003 | xargs -t -n 1 cp redis-6.2.4/redis.conf` 

**4）修改每个实例的端口、工作目录**

修改每个文件夹内的配置文件，将**端口分别修改**为7001、7002、7003，将**rdb文件保存位置**都修改为自己所在目录（在/tmp目录执行下列命令）：

`sed -i -e 's/6379/7001/g' -e 's/dir .\//dir \/tmp\/7001\//g' 7001/redis.conf
sed -i -e 's/6379/7002/g' -e 's/dir .\//dir \/tmp\/7002\//g' 7002/redis.conf
sed -i -e 's/6379/7003/g' -e 's/dir .\//dir \/tmp\/7003\//g' 7003/redis.conf`

> **sed**是快捷的对文档操作的命令。 

**5）修改每个实例的声明IP**

虚拟机本身有多个IP，为了避免将来混乱，我们需要在redis.conf文件中指定每一个实例的绑定ip信息，格式如下：

`# redis实例的声明 IP
replica-announce-ip 192.168.150.101` 

每个目录都要改，我们一键完成修改（在/tmp目录执行下列命令）：

`# 逐一执行
sed -i '1a replica-announce-ip 192.168.150.101' 7001/redis.conf
sed -i '1a replica-announce-ip 192.168.150.101' 7002/redis.conf
sed -i '1a replica-announce-ip 192.168.150.101' 7003/redis.conf

# 或者一键修改
#printf '%s\n' 7001 7002 7003 | xargs -I{} -t sed -i '1a replica-announce-ip 192.168.150.101' {}/redis.conf` 

#### 2.1.3.启动

为了方便查看日志，我们打开3个ssh窗口，分别启动3个redis实例，启动命令：

`# 第1个
redis-server 7001/redis.conf
# 第2个
redis-server 7002/redis.conf
# 第3个
redis-server 7003/redis.conf` 

启动后：

![image-20210630183914491](https://i-blog.csdnimg.cn/blog_migrate/f7c2fce104a56ac7cb42b80ba1c5a100.png)

如果要一键停止，可以运行下面命令：

`printf '%s\n' 7001 7002 7003 | xargs -I{} -t redis-cli -p {} shutdown` 

#### 2.1.4.开启主从关系

现在三个实例还没有任何关系，要配置主从可以使用**replicaof 或者slaveof（5.0以前）命令**。

**有临时和永久两种模式：**

-   修改配置文件（永久生效）
    
    -   在redis.conf中添加一行配置：`slaveof <masterip> <masterport>`
-   使用redis-cli客户端连接到redis服务，执行slaveof命令（重启后失效）：
    
    `slaveof 主机ip地址 主机端口` 
    

> **注意：**在5.0以后新增命令replicaof，与salveof效果一致。

这里我们为了演示方便，使用**方式二命令行**。

通过redis-cli命令连接7002，执行下面命令：

`# 连接 7002
redis-cli -p 7002
# 执行slaveof，将7002的主机设为7001
slaveof 192.168.150.101 7001` 

通过redis-cli命令连接7003，执行下面命令：

`# 连接 7003
redis-cli -p 7003
# 执行slaveof
slaveof 192.168.150.101 7001` 

然后连接 7001节点，查看集群状态：

`# 连接 7001
redis-cli -p 7001
# 查看状态
info replication` 

**结果：查看7001的从库：**

![image-20210630201258802](https://i-blog.csdnimg.cn/blog_migrate/bc2e71c907c4b519c7f7c1b5e792c47c.png)

#### 2.1.5.测试读写分离

执行下列操作以测试：

-   利用redis-cli连接**主库7001**，执行`set num 123`
    
-   利用redis-cli连接7002，执行`get num`，再执行`set num 666`
    
-   利用redis-cli连接7003，执行`get num`，再执行`set num 888。发现只能读不能写。`
    

![](https://i-blog.csdnimg.cn/blog_migrate/527217bb85e31aa620c5ec677f30253e.png)

可以发现，只有在7001这个master节点上可以执行写操作，7002和7003这两个slave节点只能执行读操作。

### 2.2.主从数据同步原理

#### 2.2.1.全量同步

主从**第一次建立连接时**，会执行**全量同步**，将master节点的所有数据都拷贝给slave节点，流程：

![image-20210725152222497](https://i-blog.csdnimg.cn/blog_migrate/fe4e55e1cae06f2c79e5ef1a53490bf6.png)

> repl\_backlog译为复制积压文件，底层是双向链表，存储发送rdb文件和加载rdb文件期间的所有命令。确保主从库永远一致。

这里有一个问题，**master如何得知salve是第一次来连接呢？**

有几个概念，可以作为判断依据：

-   **Replication Id**：简称**replid**，是**数据集的标记**，id一致则说明是同一数据集。**每一个master都有唯一的replid**，slave在**第一次同步**时两者replid不同，要做**全量同步**，**从库会继承master节点的replid**；以后同步两者replid相同，是同一数据集，做增量同步。replication译为复制、重复。
-   **offset**：**偏移量**，**随着**记录在**repl\_backlog中的数据增多而逐渐增大**。slave完成同步时也会记录当前同步的offset**。如果slave的offset小于master的offset**，说明slave**数据落后**于master，**需要更新**。

因此slave做数据同步，必须向master声明自己的replication id 和offset，master才可以判断到底需要同步哪些数据。

因为slave原本也是一个master，有自己的replid和offset，当第一次变成slave，与master建立连接时，发送的replid和offset是自己的replid和offset。

master判断发现slave发送来的replid与自己的不一致，说明这是一个全新的slave，就知道要做全量同步了。

master会将自己的replid和offset都发送给这个slave，slave保存这些信息。以后slave的replid就与master一致了。

因此，**master判断一个节点是否是第一次同步的依据，就是看replid是否一致**。

如图：

![image-20210725152700914](https://i-blog.csdnimg.cn/blog_migrate/fbfbf579838178c91b073afd1c28e928.png)

**完整流程描述：**

-   slave节点请求增量同步
-   master节点判断replid，发现不一致，拒绝增量同步
-   master将完整内存数据生成RDB，发送RDB到slave
-   slave清空本地数据，加载master的RDB
-   master将RDB期间的命令记录在repl\_backlog，并持续将log中的命令发送给slave
-   slave执行接收到的命令，保持与master之间的同步

#### 2.2.2.增量同步

全量同步需要先做RDB，然后将RDB文件通过网络传输个slave，成本太高了。因此除了第一次做全量同步，其它大多数时候slave与master都是做**增量同步**。

什么是增量同步？就是**根据偏移量offset只更新slave与master存在差异的部分数据**。如图：

![image-20210725153201086](https://i-blog.csdnimg.cn/blog_migrate/69847bbeb36ab68a339f4c9449198099.png)

那么master怎么知道slave与自己的数据差异在哪里呢?

#### 2.2.3.repl\_backlog原理

master怎么知道slave与自己的数据差异在哪里呢?

这就要说到全量同步时的repl\_backlog文件了。

这个文件是一个循环链表，也就是说**角标到达链表末尾后，会再次从0开始读写**，这样数组头部的数据就会被覆盖。

repl\_backlog中会记录Redis处理过的命令日志及offset，包括master当前的offset，和slave已经拷贝到的offset：

![image-20210725153359022](https://i-blog.csdnimg.cn/blog_migrate/9af4e328c2ca8e2d7cab60c54ab805f1.png)

slave与master的offset之间的差异，就是salve需要增量拷贝的数据了。

随着不断有数据写入，master的offset逐渐变大，slave也不断的拷贝，追赶master的offset：

![image-20210725153524190](https://i-blog.csdnimg.cn/blog_migrate/ce2a8c14c717be37a6983aa6992ef0b0.png)

直到链表被填满：

![image-20210725153715910](https://i-blog.csdnimg.cn/blog_migrate/4f31b042b5b2abf8110304f3f8a29f86.png)

此时，如果有新的数据写入，就会覆盖链表中的旧数据。不过，旧的数据只要是绿色的，说明是已经被同步到slave的数据，即便被覆盖了也没什么影响。因为未同步的仅仅是红色部分。

但是，如果slave出现网络阻塞，导致master的offset远远超过了slave的offset：

![image-20210725153937031](https://i-blog.csdnimg.cn/blog_migrate/ebb500afc2dccd7aeb1c8e0982e0236d.png)

如果master继续写入新数据，其offset就会覆盖旧的数据，直到将slave现在的offset也覆盖：

![image-20210725154155984](https://i-blog.csdnimg.cn/blog_migrate/c1985b82a822c41d63a5b16abd074314.png)

棕色框中的红色部分，就是尚未同步，但是却已经被覆盖的数据。此时如果slave恢复，需要同步，却发现自己的offset都没有了，无法完成增量同步了。只能做全量同步。

![image-20210725154216392](https://i-blog.csdnimg.cn/blog_migrate/be8ec958194f30698a0058b8dff696fc.png)

### 2.3.主从同步优化

主从同步可以保证主从数据的一致性，非常重要。

可以从以下几个方面来**优化Redis主从就集群：**

-   在master中配置repl-diskless-sync yes启用**无磁盘复制**，**避免全量同步时的磁盘IO。**
-   Redis**单节点上的内存占用不要太大**，减少RDB导致的过多磁盘IO
-   适当**提高repl\_backlog的大小**，发现**slave**宕机时**尽快实现故障恢复**，尽可能避免全量同步
-   限制一个master上的slave节点数量，如果实在是太多slave，则可以采用**主-从-从链式结构**，减少master压力

**主从从架构图：**

![image-20210725154405899](https://i-blog.csdnimg.cn/blog_migrate/b684dc027dd08363d52ac7440fc3457e.png)

### 2.4.小结，全量同步和增量同步区别、执行时间

**简述全量同步和增量同步区别？**

-   **全量同步：**master将完整内存数据生成**RDB**，发送RDB到slave。后续命令则记录在**repl\_backlog**，逐个发送给slave。
-   **增量同步：**slave提交自己的**offset**到master，master获取**repl\_backlog**中从**offset**之后的命令给slave

**什么时候执行全量同步？**

-   slave节点**第一次连接**master节点时
-   **slave节点断开时间太久，repl\_backlog中的offset已经被覆盖时**

**什么时候执行增量同步？**

-   slave节点断开又恢复，并且在repl\_backlog中**能找到offset时**

## 3.Redis哨兵

Redis提供了哨兵（Sentinel）机制来实现主从集群的自动故障恢复。

### 3.1.哨兵原理

#### 3.1.1.集群结构和作用

哨兵的结构如图：

![image-20210725154528072](https://i-blog.csdnimg.cn/blog_migrate/95638cdc05ead17bdd23c0f54a2dd9ea.png)

**哨兵的作用如下：**

-   **监控**：Sentinel 会不断**检查**您的master和slave**是否按预期工作**
-   **自动故障恢复**：如果**master故障**，Sentinel会**将一个slave提升为master**。当故障实例恢复后也以新的master为主
-   **通知**：Sentinel充当Redis客户端的服务发现来源，当**集群发生故障转移时**，会将**最新信息推送给Redis的客户端**

#### 3.1.2.集群监控原理

**Sentinel**基于**心跳机制监测服务状态**，**每隔1秒**向集群的每个实例**发送ping命令**：

**•主观下线：**如果某sentinel节点发现某实例**未在规定时间响应**，则认为该实例**主观下线**。

**•客观下线：**若**超过指定数量**quorum值（quorum译为法定人数、多数派）**的sentinel**都**认为**该实例**主观下线**，则该实例**客观下线**。quorum值最好超过Sentinel实例数量的一半。

![image-20210725154632354](https://i-blog.csdnimg.cn/blog_migrate/4087560a8c72083ee0cf106df1334c3b.png)

#### 3.1.3.集群故障恢复原理，选举、切换新master

**1.选举新master的依据：** 

一旦发现master故障，**sentinel需要在salve中选择一个作为新的master**，选择依据是这样的：

-   首先会判断**slave节点**与master节点**断开时间**长短，如果**超过指定值**（down-after-milliseconds \* 10）则会**排除该slave节点**
-   然后判断slave节点的**slave-priority值，越小优先级越高**，如果是0则永不参与选举
-   如果slave-prority一样，则判断slave节点的**offset值，越大说明数据越新，优先级越高**
-   最后是判断slave节点的**运行id**大小（这个运行id就很随机了，是Redis启动时自动生成的id），**越小优先级越高。**

**2.切换新master的方法：** 

-   **sentinel**给备选的**slave1节点发送slaveof no one命令**，让该节点**成为master**
-   **sentinel给所有其它slave发送slaveof 192.168.150.101 7002 命令**，让这些slave成为新master的从节点，开始从新的master上同步数据。
-   最后，sentinel将**故障节点标记为slave**，当故障节点恢复后会自动成为新的master的slave节点

![image-20210725154816841](https://i-blog.csdnimg.cn/blog_migrate/549f103e2c6deef65cfd09a58849190c.png)

#### 3.1.4.小结，Sentinel健康、故障转移、通知

**Sentinel对redis集群的三个作用是什么？**

-   监控
-   故障转移
-   通知

>  **Sentinel其他作用：**
> 
> [微服务保护、流量控制、隔离和降级、授权规则、规则持久化](https://blog.csdn.net/qq_40991313/article/details/126882045 "微服务保护、流量控制、隔离和降级、授权规则、规则持久化")

**Sentinel如何判断一个redis实例是否健康？**

-   **每隔1秒发送一次ping命令**，如果超过一定时间没有相向则认为是主观下线
-   如果**大多数sentinel都认为该实例主观下线**，则判定该实例客观下线
    

**故障转移步骤有哪些？**

-   首先选定一个slave作为**新的master**，执行**slaveof no one**
-   然后让**所有节点**都执行**slaveof 新master**
-   修改**故障的旧主节点**配置，添加**slaveof 新master**

### 3.2.搭建哨兵集群

#### 3.2.1.集群结构

这里我们**搭建一个三节点形成的Sentinel集群**，来**监管**之前的**Redis主从集群**。如图：

![image-20210701215227018](https://i-blog.csdnimg.cn/blog_migrate/fd4350f74786139d874d49dbe9cd3cd5.png)

三个sentinel实例信息如下：

| 节点 | IP | PORT |
| --- | --- | --- |
| s1 | 192.168.150.101 | 27001 |
| s2 | 192.168.150.101 | 27002 |
| s3 | 192.168.150.101 | 27003 |

#### 3.2.2.准备实例和配置

要在**同一台虚拟机开启3个实例**，必须准备**三份不同的配置文件和目录**，配置文件所在目录也就是工作目录。

我们创建三个文件夹，名字分别叫s1、s2、s3：

```
# 进入/tmp目录
cd /tmp
# 创建目录
mkdir s1 s2 s3
```

如图：

![image-20210701215534714](https://i-blog.csdnimg.cn/blog_migrate/f39942b3c9c40774d2e7dd2939124127.png)

然后我们在**s1目录创建一个sentinel.conf文件**，添加下面的内容：

```bash
port 27001
sentinel announce-ip 192.168.150.101
#mymaster：主节点名称，自定义，任意写
#192.168.150.101 7001：主节点的ip和端口
#2：选举master时的quorum值，也就是3台实例超过两台被主观下线则整个redis集群客观下线。
sentinel monitor mymaster 192.168.150.101 7001 2
#Sentinel 在多长时间内没有从主服务器（mymaster）中收到响应时，将该主服务器视为不可用。
sentinel down-after-milliseconds mymaster 5000
#指定 Sentinel 在多长时间后将尝试执行故障转移以恢复故障
sentinel failover-timeout mymaster 60000
dir "/tmp/s1"
```

> **解读：**
> 
> -   `port 27001`：是当前sentinel实例的端口
> -   `sentinel monitor mymaster 192.168.150.101 7001 2`：指定主节点信息，**只指定主节点信息sentinel就能监控到整个集群**
>     -   `mymaster`：主节点名称，自定义，任意写
>     -   `192.168.150.101 7001`：主节点的ip和端口
>     -   **`2`：**选举master时的**quorum值**，也就是3台实例超过两台被主观下线则整个redis集群客观下线。

然后将**s1/sentinel.conf文件拷贝到s2、s3两个目录中**（在**/tmp目录**执行下列命令）：

```bash
# 方式一：逐个拷贝
cp s1/sentinel.conf s2
cp s1/sentinel.conf s3
# 方式二：管道组合命令，一键拷贝
echo s2 s3 | xargs -t -n 1 cp s1/sentinel.conf
```

**修改s2、s3**两个文件夹内的**配置文件**，**将端口分别修改为27002、27003：**

```bash
sed -i -e 's/27001/27002/g' -e 's/s1/s2/g' s2/sentinel.conf
sed -i -e 's/27001/27003/g' -e 's/s1/s3/g' s3/sentinel.conf
```

#### 3.2.3.启动3个redis实例

为了方便查看日志，我们打开3个ssh窗口，分别**启动3个redis实例**，启动命令：

```bash
# 第1个
redis-sentinel s1/sentinel.conf
# 第2个
redis-sentinel s2/sentinel.conf
# 第3个
redis-sentinel s3/sentinel.conf
```

**启动后：**

![image-20210701220714104](https://i-blog.csdnimg.cn/blog_migrate/4a5f5cd65fb2941d8fbf23f2442dc692.png)

#### 3.2.4.测试

尝试让**master节点7001宕机（ctrl+c）**，查看sentinel日志：认为主库主观下线

![image-20210701222857997](https://i-blog.csdnimg.cn/blog_migrate/113c9f6ed073214d52ce72c517d25773.png)

**查看7003的日志：**认为主库主观下线

![image-20210701223025709](https://i-blog.csdnimg.cn/blog_migrate/35f5a20019813c7a56960bd70cd39134.png)

 也认为主库主观下线，超过2个实例认为7001主观下线，于是7001客观下线。**7002被选成master、让其他实例认主**

![image-20210701223131264](https://i-blog.csdnimg.cn/blog_migrate/8d9d5e098d4dcea54e4b5fb3222db9a4.png)

超过2个sentinel认为主库7001主观下线了，那么认为7001客观下线，进行故障修复。

### 3.3.RedisTemplate

在**Sentinel**集群监管下的**Redis主从集群**，其**节点会因为自动故障转移而发生变化**，Redis的客户端必须感知这种变化，及时更新连接信息。Spring的**RedisTemplate底层利用lettuce实现了节点的感知和自动切换。**

下面，我们通过一个测试来**实现RedisTemplate集成哨兵机制。**

#### 3.3.1.导入Demo工程

首先，我们引入课前资料提供的Demo工程：

![image-20210725155124958](https://i-blog.csdnimg.cn/blog_migrate/94edabb12280ac9372f1b94494b50c16.png)

![](https://i-blog.csdnimg.cn/blog_migrate/440ba7e81068e51499e46bf1c2f77879.png)

```java
@RestController
public class HelloController {

    @Autowired
    private StringRedisTemplate redisTemplate;

    @GetMapping("/get/{key}")
    public String hi(@PathVariable String key) {
        return redisTemplate.opsForValue().get(key);
    }

    @GetMapping("/set/{key}/{value}")
    public String hi(@PathVariable String key, @PathVariable String value) {
        redisTemplate.opsForValue().set(key, value);
        return "success";
    }
}
```

#### 3.3.2.引入redis的starter依赖

在项目的pom文件中引入依赖：

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

#### 3.3.3.配置Redis地址

然后在配置文件application.yml中指定**redis下的sentinel相关信息**，因为主库ip、端口、quorum值信息在sentinel的sentinel.conf里指定过了，所以**只用配置sentinel的相关信息：**

```bash
spring:
  redis:
    sentinel:
      master: mymaster    #与sentinel里的sentinel.conf配置文件的主库名一致
      nodes:
        - 192.168.150.101:27001
        - 192.168.150.101:27002
        - 192.168.150.101:27003
```

> 我们以前在三个sentinel目录下都创建一个sentinel.conf文件，添加了下面的内容，指定了主库信息：
> 
> ```bash
> port 27001
> sentinel announce-ip 192.168.150.101
> sentinel monitor mymaster 192.168.150.101 7001 2    #主节点名称，自定义，任意写
> sentinel down-after-milliseconds mymaster 5000
> sentinel failover-timeout mymaster 60000
> dir "/tmp/s1"
> ```

#### 3.3.4.配置读写分离

在项目的**启动类**中，添加一个**新的bean：**

```java
@Bean
public LettuceClientConfigurationBuilderCustomizer clientConfigurationBuilderCustomizer(){
    return clientConfigurationBuilder -> clientConfigurationBuilder.readFrom(ReadFrom.REPLICA_PREFERRED);
}
```

这个bean中配置的就是**读写策略**，包括四种：

-   MASTER：从主节点读取
-   MASTER\_PREFERRED：优先从master节点读取，master不可用才读取replica
-   REPLICA：从slave（replica）节点读取
-   **REPLICA \_PREFERRED（推荐）：**优先从slave（replica）节点读取，所有的slave都不可用才读取master

#### 3.3.5.测试读写分离、主从自动切换

**测试读：** 

![](https://i-blog.csdnimg.cn/blog_migrate/92413c9fc789865c876c5cc36f769ab6.png)

看idea日志：

先获取sentinel连接

![](https://i-blog.csdnimg.cn/blog_migrate/2cf58c6d51fb1eeba151683ef5a9b0d6.png)

挑中27001 

![](https://i-blog.csdnimg.cn/blog_migrate/7059cba052ed4a0ae5dcbb751e746d34.png)

得到主库信息：![](https://i-blog.csdnimg.cn/blog_migrate/1a6a5396bb2763d76b5e4fa7e8a247c3.png) 

得到从库信息：![](https://i-blog.csdnimg.cn/blog_migrate/614736d3590e2746f4b9149c0e5dbd80.png) 

连接主从节点：![](https://i-blog.csdnimg.cn/blog_migrate/4f259b5958c728e00e7ab5c5938b5008.png) 

可以看到查询请求给到了7003：![](https://i-blog.csdnimg.cn/blog_migrate/12d903707615884839d40a8b817d4f10.png) 

**测试写：**

![](https://i-blog.csdnimg.cn/blog_migrate/f1a961528203e744f208d65e6820f7ef.png)

交给了7002主节点处理：

![](https://i-blog.csdnimg.cn/blog_migrate/237554c991b33dc13010d150487507a0.png)

**测试故障修复：**

宕机7002![](https://i-blog.csdnimg.cn/blog_migrate/061a7863171f90a8222fa57982181454.png) 

sentinel日志显示切换主节点到7001：![](https://i-blog.csdnimg.cn/blog_migrate/9a0068149bdfe0b1d44dfbdc7919f800.png) 

## 4.Redis分片集群

### 4.0.分片集群概述

**主从和哨兵**可以解决高可用、高并发读的问题。但是依然有**两个问题没有解决：**

-   **海量数据存储问题**
    
-   **高并发写的问题**
    

使用**分片集群可以解决上述问题**，如图:

![image-20210725155747294](https://i-blog.csdnimg.cn/blog_migrate/e219ef2468fba149d5b0f0af0bd098b1.png)

**分片集群特征：**

-   **集群中有多个master，每个master保存不同数据**
    
-   每个master都可以有多个slave节点
    
-   **master之间通过ping监测彼此健康状态**
    
-   客户端请求可以访问集群任意节点，最终都会被转发到正确节点
    

### 4.1.搭建分片集群 

#### 4.1.1.集群结构

分片集群需要的节点数量较多，这里我们搭建一个最小的分片集群，包含3个master节点，每个master包含一个slave节点，结构如下：

![image-20210702164116027](https://i-blog.csdnimg.cn/blog_migrate/d3e71972535ba366cca0dcccaa6e7d55.png)

这里我们会在同一台虚拟机中开启6个redis实例，模拟分片集群，信息如下：

| IP | PORT | 角色 |
| --- | --- | --- |
| 192.168.150.101 | 7001 | master |
| 192.168.150.101 | 7002 | master |
| 192.168.150.101 | 7003 | master |
| 192.168.150.101 | 8001 | slave |
| 192.168.150.101 | 8002 | slave |
| 192.168.150.101 | 8003 | slave |

#### 4.1.2.准备实例和配置

删除之前的7001、7002、7003这几个目录，**重新创建出7001、7002、7003、8001、8002、8003目录：**

```bash
# 进入/tmp目录
cd /tmp
# 删除旧的，避免配置干扰
rm -rf 7001 7002 7003
# 创建目录
mkdir 7001 7002 7003 8001 8002 8003
```

在/tmp下准备一个新的redis.conf文件，内容如下：

```bash
port 6379
# 开启集群功能
cluster-enabled yes
# 集群的配置文件名称，不需要我们创建，由redis自己维护
cluster-config-file /tmp/6379/nodes.conf
# 节点心跳失败的超时时间
cluster-node-timeout 5000
# 持久化文件存放目录
dir /tmp/6379
# 绑定地址
bind 0.0.0.0
# 让redis后台运行
daemonize yes
# 注册的实例ip
replica-announce-ip 192.168.150.101
# 保护模式
protected-mode no
# 数据库数量
databases 1
# 日志
logfile /tmp/6379/run.log
```

将这个文件拷贝到每个目录下：

```bash
# 进入/tmp目录
cd /tmp
# 执行拷贝
echo 7001 7002 7003 8001 8002 8003 | xargs -t -n 1 cp redis.conf
```

修改每个目录下的redis.conf，将其中的6379修改为与所在目录一致：

```bash
# 进入/tmp目录
cd /tmp
# 修改配置文件
printf '%s\n' 7001 7002 7003 8001 8002 8003 | xargs -I{} -t sed -i 's/6379/{}/g' {}/redis.conf
```

#### 4.1.3.启动

因为已经配置了后台启动模式，所以可以直接启动服务：

```bash
# 进入/tmp目录
cd /tmp
# 一键启动所有服务
printf '%s\n' 7001 7002 7003 8001 8002 8003 | xargs -I{} -t redis-server {}/redis.conf
```

通过ps查看状态：

```
ps -ef | grep redis
```

发现服务都已经正常启动，此时互相之间还没有集群关系：

![image-20210702174255799](https://i-blog.csdnimg.cn/blog_migrate/c74fce8711b68bff2797f5044fae405e.png)

如果要关闭所有进程，可以执行命令：

```
ps -ef | grep redis | awk '{print $2}' | xargs kill
```

或者（推荐这种方式）：

```
printf '%s\n' 7001 7002 7003 8001 8002 8003 | xargs -I{} -t redis-cli -p {} shutdown
```

#### 4.1.4.创建集群

虽然服务启动了，但是目前每个服务之间都是独立的，没有任何关联。

我们需要执行命令来创建集群，在Redis5.0之前创建集群比较麻烦，5.0之后集群管理命令都集成到了redis-cli中。

**1）Redis5.0之前**

Redis5.0之前集群命令都是用redis安装包下的src/redis-trib.rb来实现的。因为redis-trib.rb是有ruby语言编写的所以需要安装ruby环境。

```bash
# 安装依赖
yum -y install zlib ruby rubygems
gem install redis
```

然后通过命令来管理集群：

```bash
# 进入redis的src目录
cd /tmp/redis-6.2.4/src
# 创建集群
./redis-trib.rb create --replicas 1 192.168.150.101:7001 192.168.150.101:7002 192.168.150.101:7003 192.168.150.101:8001 192.168.150.101:8002 192.168.150.101:8003
```

**2）Redis5.0以后**

我们使用的是Redis6.2.4版本，集群管理以及集成到了redis-cli中，格式如下：

```bash
redis-cli --cluster create --cluster-replicas 1 192.168.150.101:7001 192.168.150.101:7002 192.168.150.101:7003 192.168.150.101:8001 192.168.150.101:8002 192.168.150.101:8003
```

> **命令说明：**
> 
> -   `redis-cli --cluster`或者`./redis-trib.rb`：代表集群操作命令
> -   `create`：代表是创建集群
> -   `--replicas 1`或者`--cluster-replicas 1` ：指定集群中每个master的副本个数为1，此时`节点总数 ÷ (replicas + 1)` 得到的就是master的数量。因此节点列表中的前n个就是master，其它节点都是slave节点，随机分配到不同master

运行后的样子：

![image-20210702181101969](https://i-blog.csdnimg.cn/blog_migrate/cb1d68d1f33877da835cdd2956aa7b7d.png)

这里输入yes，则集群开始创建：

![image-20210702181215705](https://i-blog.csdnimg.cn/blog_migrate/91d1525cd54edccc15a3fb26bfcf8825.png)

通过命令可以查看集群状态：

```
redis-cli -p 7001 cluster nodes
```

![image-20210702181922809](https://i-blog.csdnimg.cn/blog_migrate/00cd144ff841a854a19f2da4051aa964.png)

#### 4.1.5.集群常用命令

redis-cli --cluster命令：

-   **redis-cli --cluster create：**创建集群
-   **info：**查看集群状态
-   **fix：**修复集群
-   **reshard：**迁移插槽
-   **add-node：**添加新节点
-   **del-node：**删除指定节点
-   **import：**导入数据到集群

```bash
redis-cli --cluster help
Cluster Manager Commands:
  create         host1:port1 ... hostN:portN   #创建集群
                 --cluster-replicas <arg>      #从节点个数
  check          host:port                     #检查集群
                 --cluster-search-multiple-owners #检查是否有槽同时被分配给了多个节点
  info           host:port                     #查看集群状态
  fix            host:port                     #修复集群
                 --cluster-search-multiple-owners #修复槽的重复分配问题
  reshard        host:port                     #指定集群的任意一节点进行迁移slot，重新分slots
                 --cluster-from <arg>          #需要从哪些源节点上迁移slot，可从多个源节点完成迁移，以逗号隔开，传递的是节点的node id，还可以直接传递--from all，这样源节点就是集群的所有节点，不传递该参数的话，则会在迁移过程中提示用户输入
                 --cluster-to <arg>            #slot需要迁移的目的节点的node id，目的节点只能填写一个，不传递该参数的话，则会在迁移过程中提示用户输入
                 --cluster-slots <arg>         #需要迁移的slot数量，不传递该参数的话，则会在迁移过程中提示用户输入。
                 --cluster-yes                 #指定迁移时的确认输入
                 --cluster-timeout <arg>       #设置migrate命令的超时时间
                 --cluster-pipeline <arg>      #定义cluster getkeysinslot命令一次取出的key数量，不传的话使用默认值为10
                 --cluster-replace             #是否直接replace到目标节点
  rebalance      host:port                                      #指定集群的任意一节点进行平衡集群节点slot数量 
                 --cluster-weight <node1=w1...nodeN=wN>         #指定集群节点的权重
                 --cluster-use-empty-masters                    #设置可以让没有分配slot的主节点参与，默认不允许
                 --cluster-timeout <arg>                        #设置migrate命令的超时时间
                 --cluster-simulate                             #模拟rebalance操作，不会真正执行迁移操作
                 --cluster-pipeline <arg>                       #定义cluster getkeysinslot命令一次取出的key数量，默认值为10
                 --cluster-threshold <arg>                      #迁移的slot阈值超过threshold，执行rebalance操作
                 --cluster-replace                              #是否直接replace到目标节点
  add-node       new_host:new_port existing_host:existing_port  #添加节点，把新节点加入到指定的集群，默认添加主节点
                 --cluster-slave                                #新节点作为从节点，默认随机一个主节点
                 --cluster-master-id <arg>                      #给新节点指定主节点
  del-node       host:port node_id                              #删除给定的一个节点，成功后关闭该节点服务
  call           host:port command arg arg .. arg               #在集群的所有节点执行相关命令
  set-timeout    host:port milliseconds                         #设置cluster-node-timeout
  import         host:port                                      #将外部redis数据导入集群
                 --cluster-from <arg>                           #将指定实例的数据导入到集群
                 --cluster-copy                                 #migrate时指定copy
                 --cluster-replace                              #migrate时指定replace
  help           

For check, fix, reshard, del-node, set-timeout you can specify the host and port of any working node in the cluster.
```

#### 4.1.6.集群模式下连接节点必须加“-c”

集群模式下，连接节点时必须加“-c” 。例如

```bash
redis-cli -c -p 7001
```

> 尝试连接7001节点，存储一个数据：
> 
> ```bash
> # 连接
> redis-cli -p 7001
> # 存储数据
> set num 123
> # 读取数据
> get num
> # 再次存储
> set a 1
> ```
> 
> 结果悲剧了：
> 
> ![image-20210702182343979](https://i-blog.csdnimg.cn/blog_migrate/d172a2cc14349cfc78a70b3adec17836.png)
> 
> 集群操作时，需要给`redis-cli`加上`-c`参数才可以：
> 
> ```
> redis-cli -c -p 7001
> ```
> 
> 这次可以了：
> 
> ![image-20210702182602145](https://i-blog.csdnimg.cn/blog_migrate/1f244c7a12e849f76116d2933710e67a.png)

### 4.2.散列插槽

#### 4.2.1.插槽原理

**Redis会把每一个master节点映射到0~16383共16384个插槽（hash slot）**上，查看集群信息时就能看到：

![image-20210725155820320](https://i-blog.csdnimg.cn/blog_migrate/b83b40d25c4856e72da78c5a034aade0.png)

**数据key不是与节点绑定，而是与插槽绑定。**redis会根据**key的有效部分计算插槽值**，分两种情况：

-   **key中包含"{}"，且“{}”中至少包含1个字符，“{}”中的部分是有效部分**
-   **key中不包含“{}”**，**整个key都是有效部分**

例如：key是num，那么就根据num计算，如果是{itcast}num，则根据itcast计算。计算方式是利用CRC16**算法得到一个hash值**，然后**对16384取余**，得到的结果就是slot值。

![](https://i-blog.csdnimg.cn/blog_migrate/c72fed2aa847e602d3785816aac4f492.png)

> **注意，集群下打开redis客户端要加-c** 

如图，在7001这个节点执行**set** a 1时，对a做**hash运算**，对16384**取余**，得到的结果是15495，因此要**存储**到103节点。

到了**7003节点**后，执行`**get** num`时，对num做**hash运算**，对16384**取余**，得到的结果是2765，因此需要**切换到7001节点**

#### 4.2.1.小结，插槽流程、同类数据通过{}插槽绑定到同实例

**Redis如何判断某个key应该在哪个实例？**

-   将16384个**插槽分配**到不同的实例
-   根据key的有效部分**计算哈希值**，对16384取余
-   **余数作为插槽**，寻找插槽所在实例即可

**如何将同一类数据固定的保存在同一个Redis实例？**

-   这一类数据使用相同的有效部分，**例如key都以{typeId}为前缀，有效值一样的key会存储在同一个插槽。**

>  **例如将num存到a所在插槽：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/219461ca15d8a34559ae02d53aefd960.png)

### 4.3.集群伸缩

#### 4.3.0.操作集群的命令 

**redis-cli --cluster**提供了很多**操作集群的命令**，可以通过下面方式查看：

![image-20210725160138290](https://i-blog.csdnimg.cn/blog_migrate/1c4ebd3f5b2465c45775dbf7451879c0.png)

比如，**添加节点的命令：**

![image-20210725160448139](https://i-blog.csdnimg.cn/blog_migrate/cfcf5eb6ecf14e11c93c9fddecf9a51b.png)

```bash
redis-cli --cluster add-node  192.168.150.101:7004 192.168.150.101:7001
#后面这个ip：端口是集群中任意已存在的实例地址
```

**插槽命令：**![](https://i-blog.csdnimg.cn/blog_migrate/82765a4a5663c3099942ce17dd8366be.png) 

#### 4.3.1.需求分析，添加节点到集群、分配插槽

**需求：向集群中添加一个新的master节点，并向其中存储 num = 10**

-   启动一个新的redis实例，端口为**7004**
-   添加7004到之前的集群，并作为一个master节点
-   给7004节点**分配插槽**，**使得num这个key可以存储到7004实例（num插槽算出来在7001）**

这里需要两个新的功能：

-   **添加一个节点到集群中**
-   **将部分插槽分配到新插槽**

#### 4.3.2.创建新的redis实例

创建一个文件夹：

```
mkdir 7004
```

拷贝配置文件：

```
cp redis.conf /7004
```

修改配置文件：

```
sed /s/6379/7004/g 7004/redis.conf
```

启动7004

```
redis-server 7004/redis.conf
```

#### 4.3.3.添加新节点到redis

添加节点的语法如下：

![image-20210725160448139](https://i-blog.csdnimg.cn/blog_migrate/cfcf5eb6ecf14e11c93c9fddecf9a51b.png)

**执行添加新节点命令：**

```bash
redis-cli --cluster add-node  192.168.150.101:7004 192.168.150.101:7001
#后面这个ip：端口是集群中任意已存在的实例地址
```

通过命令**查看集群状态：**

```
redis-cli -p 7001 cluster nodes
```

如图，7004加入了集群，并且默认是一个master节点：

![image-20210725161007099](https://i-blog.csdnimg.cn/blog_migrate/096d2bef755660626067fa5846c52536.png)

但是，可以看到7004节点的插槽数量为0，因此没有任何数据可以存储到7004上

#### 4.3.4.转移插槽

我们要将num存储到7004节点，因此需要**先看看num的插槽**是多少：

![image-20210725161241793](https://i-blog.csdnimg.cn/blog_migrate/cc14b2cb765de3032f01073474f59d96.png)

如上图所示，**num的插槽为2765.**

我们可以将0~3000的插槽从7001转移到7004，命令格式如下：

![image-20210725161401925](https://i-blog.csdnimg.cn/blog_migrate/2010e959fa04f68244595388f5a05163.png)

> reshard译为重新切分。 

具体命令如下：

**重新切分7001插槽**

![image-20210725161506241](https://i-blog.csdnimg.cn/blog_migrate/280393018b9278cb0486e1e179683a68.png)

得到下面的反馈：

![image-20210725161540841](https://i-blog.csdnimg.cn/blog_migrate/8549275330fe06cac5b3f4a8d4a8cdac.png)

**询问要移动多少个插槽**，我们计划是3000个：

新的问题来了：

![image-20210725161637152](https://i-blog.csdnimg.cn/blog_migrate/6b35a62d9b308ea6c32677b3a2fdc168.png)

**哪个node来接收这些插槽？**

显然是7004，那么7004节点的id是多少呢？

![image-20210725161731738](https://i-blog.csdnimg.cn/blog_migrate/4d6ad12e271ff790ce51e831328e2647.png)

**复制这个id，然后拷贝到刚才的控制台后：**

![image-20210725161817642](https://i-blog.csdnimg.cn/blog_migrate/b8ed0ffdaa46b7694549c916d0c91ab2.png)

这里询问，你的插槽是从哪里移动过来的？

-   all：代表全部，也就是三个节点各转移一部分
-   具体的id：目标节点的id
-   done：没有了

这里我们要**从7001获取，因此填写7001的id：**

![image-20210725162030478](https://i-blog.csdnimg.cn/blog_migrate/4653438175ce107a51be9778977fe6a4.png)

填完后，**点击done**，这样插槽转移就准备好了：

![image-20210725162101228](https://i-blog.csdnimg.cn/blog_migrate/a43d794abcbfa35cfb8e613d57187cb9.png)

确认要转移吗？输入**yes：**

然后，**通过命令查看结果：**

![image-20210725162145497](https://i-blog.csdnimg.cn/blog_migrate/b57543f92edb2664d7b37dad83e354f1.png)

可以看到：

![image-20210725162224058](https://i-blog.csdnimg.cn/blog_migrate/844a153582b438c74019ae9e0717e6d2.png)

目的达成。

### 4.4.故障转移

集群初识状态是这样的：

![image-20210727161152065](https://i-blog.csdnimg.cn/blog_migrate/8b49b979ccc5b57d41e3fadf35376358.png)

其中7001、7002、7003都是master，我们计划让7002宕机。

#### 4.4.1.自动故障转移

当集群中有一个master宕机会发生什么呢？

直接停止一个redis实例，例如7002：

```
redis-cli -p 7002 shutdown
```

1）首先是该实例与其它实例失去连接

2）然后是疑似宕机：

![image-20210725162319490](https://i-blog.csdnimg.cn/blog_migrate/40d007e00d80a76527ae36e7921657e9.png)

3）最后是确定下线，自动提升一个slave为新的master：

![image-20210725162408979](https://i-blog.csdnimg.cn/blog_migrate/73a88037aff5c27508e9d5ea365cebc3.png)

4）当7002再次启动，就会变为一个slave节点了：

![image-20210727160803386](https://i-blog.csdnimg.cn/blog_migrate/b617927f5df3d6e717b8f6b17188c8eb.png)

#### 4.4.2.手动故障转移、指定master实例

利用**cluster failover命令**可以**手动让集群中的某个master宕机**，切换到执行cluster failover命令的这个slave节点，实现无感知的数据迁移。其流程如下：

![image-20210725162441407](https://i-blog.csdnimg.cn/blog_migrate/7fc185c86741f3b21f9fa35ad50ec490.png)

这种failover命令可以指定三种模式：

-   缺省：默认的流程，如图1~6歩
-   force：省略了对offset的一致性校验
-   takeover：直接执行第5歩，忽略数据一致性、忽略master状态和其它master的意见

**案例需求**：在7002这个slave节点执行**手动故障转移，重新夺回master地位**

步骤如下：

1）利用redis-cli连接7002这个节点

2）执行cluster failover命令

**如图：**

![image-20210727160037766](https://i-blog.csdnimg.cn/blog_migrate/aa0efd9e3cce7e7964df1ff35932fd36.png)

**效果：**

![image-20210727161152065](https://i-blog.csdnimg.cn/blog_migrate/8b49b979ccc5b57d41e3fadf35376358.png)

### 4.5.RedisTemplate访问分片集群

RedisTemplate底层同样基于lettuce实现了分片集群的支持，而使用的步骤与哨兵模式基本一致：

**1）引入redis的starter依赖**

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

**2）配置分片集群地址**

与哨兵模式相比，其中只有分片集群的配置方式略有差异，**配置分片集群地址如下：**

```bash
spring:
  redis:
    cluster:
      nodes:
        - 192.168.150.101:7001
        - 192.168.150.101:7002
        - 192.168.150.101:7003
        - 192.168.150.101:8001
        - 192.168.150.101:8002
        - 192.168.150.101:8003
```

>  哨兵模式的配置：
> 
> ```bash
> spring:
>   redis:
>     sentinel:
>       master: mymaster    #与sentinel里的sentinel.conf配置文件的主库名一致
>       nodes:
>         - 192.168.150.101:27001
>         - 192.168.150.101:27002
>         - 192.168.150.101:27003
> ```

**3）配置读写分离**

```java
@Bean
public LettuceClientConfigurationBuilderCustomizer clientConfigurationBuilderCustomizer(){
    return clientConfigurationBuilder -> clientConfigurationBuilder.readFrom(ReadFrom.REPLICA_PREFERRED);
}
```