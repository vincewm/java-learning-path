> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1 简介](#4.3.1%20%E7%AE%80%E4%BB%8B%C2%A0) 

[1.1 环境准备](#1.1%20%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)

[1.1.1 Redis下载和安装](#Redis%E4%B8%8B%E8%BD%BD%E5%92%8C%E5%AE%89%E8%A3%85%C2%A0) 

[1.1.1.1 下载](#1.1.1.1%C2%A0%E4%B8%8B%E8%BD%BD)

[1.1.1.2 linux版安装](#1.1.1%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B.2%C2%A0linux%E7%89%88%E5%AE%89%E8%A3%85)

[1.1.1​​​​​​​.3 windows版安装](#1.1.1%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B.3%C2%A0windows%E7%89%88%E5%AE%89%E8%A3%85)

[1.1.2 启动](#linux%E7%89%88%E5%90%AF%E5%8A%A8redis)

[1.1.2.1 linux版启动（前台版）](#1.1.2.1%20linux%E7%89%88%E5%90%AF%E5%8A%A8%EF%BC%88%E5%89%8D%E5%8F%B0%E7%89%88%EF%BC%89)

[1.1.2.2 Linux启动服务器（后台版）](#1.1.2.2%C2%A0Linux%E5%90%AF%E5%8A%A8%E6%9C%8D%E5%8A%A1%E5%99%A8%EF%BC%88%E5%90%8E%E5%8F%B0%E7%89%88%EF%BC%89)

[1.1.2.3 Windows版启动redis](#4.3.2%20%E5%9F%BA%E6%9C%AC%E6%93%8D%E4%BD%9C)

[1.2 Redis五种数据类型](#Redis%E4%BA%94%E7%A7%8D%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)

[1.3 Redis常用命令](#Redis%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)

[通用命令](#%E9%80%9A%E7%94%A8%E5%91%BD%E4%BB%A4)

[1.3.1 字符串类型string](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%B1%BB%E5%9E%8Bstring)

[1.3.2 哈希存储模型 hash](#%E5%93%88%E5%B8%8C%E5%AD%98%E5%82%A8%E6%A8%A1%E5%9E%8B%C2%A0hash)

[1.3.3 列表类型list](#%E5%88%97%E8%A1%A8%E7%B1%BB%E5%9E%8Blist)

[1.3.4 无序集合set](#%E6%97%A0%E5%BA%8F%E9%9B%86%E5%90%88set)

[1.3.4 有序集合sorted set](#%E6%9C%89%E5%BA%8F%E9%9B%86%E5%90%88sorted%20set)

[2 springboot整合redis](#4.3.3%20springboot%E6%95%B4%E5%90%88redis) 

[2.1 lettucs客户端技术操作Redis，默认](#lettucs%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%8A%80%E6%9C%AF%E6%93%8D%E4%BD%9CRedis%EF%BC%8C%E9%BB%98%E8%AE%A4)

[2.1.1 RedisTemplate对象](#RedisTemplate%E5%AF%B9%E8%B1%A1%C2%A0)

[2.1.2 序列化器问题](#%E5%BA%8F%E5%88%97%E5%8C%96%E5%99%A8%E9%97%AE%E9%A2%98)

[2.1.3 StringRedisTemplate对象，命令行模式默认](#StringRedisTemplate%E5%AF%B9%E8%B1%A1%EF%BC%8C%E5%91%BD%E4%BB%A4%E8%A1%8C%E6%A8%A1%E5%BC%8F%E9%BB%98%E8%AE%A4)

[2.2 切换jedis客户端技术](#jedis%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%8A%80%E6%9C%AF%E6%93%8D%E4%BD%9CRedis)

[2.2.1 RedisTemplate或者StringRedisTemplate](#RedisTemplate%E6%88%96%E8%80%85StringRedisTemplate%C2%A0) 

[2.2.2 lettcus与jedis区别](#lettcus%E4%B8%8Ejedis%E5%8C%BA%E5%88%AB)

[3 Spring Cache](#3%20Spring%20Cache)

[3.1 Spring Cache介绍](#3.1%20Spring%20Cache%E4%BB%8B%E7%BB%8D)

[3.2 Spring Cache常用注解](#3.2%20Spring%20Cache%E5%B8%B8%E7%94%A8%E6%B3%A8%E8%A7%A3)

[3.2.1 依赖、 yml配置、开启缓存](#3.2.1%20%E4%BE%9D%E8%B5%96%E3%80%81%20yml%E9%85%8D%E7%BD%AE%E3%80%81%E5%BC%80%E5%90%AF%E7%BC%93%E5%AD%98)

[3.2.2 key的命名方式](#3.2.2%20key%E7%9A%84%E5%91%BD%E5%90%8D%E6%96%B9%E5%BC%8F%C2%A0) 

[3.2.3 注解实现缓存](#3.2.3%20%E6%B3%A8%E8%A7%A3%E5%AE%9E%E7%8E%B0%E7%BC%93%E5%AD%98)

[3.3  Spring Cache使用各种缓存](#3.3%20%C2%A0Spring%20Cache%E4%BD%BF%E7%94%A8%E5%90%84%E7%A7%8D%E7%BC%93%E5%AD%98)

[3.3.1 SpringBoot内置缓存Simple](#SpringBoot%E5%86%85%E7%BD%AE%E7%BC%93%E5%AD%98%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)

[3.3.2 手机验证码模拟案例，@CachePut](#%E6%89%8B%E6%9C%BA%E9%AA%8C%E8%AF%81%E7%A0%81%E6%A1%88%E4%BE%8B)

[3.3.3 Spring Cache使用Redis](#3.3.3%C2%A0Spring%20Cache%E4%BD%BF%E7%94%A8Redis)

--

## 1 简介 

**Redis是一款c语言开发的、采用key-value数据存储格式的内存级NoSQL数据库**，重点关注数据存储格式，是key-value格式，也就是**键值对的存储形式**。与MySQL数据库不同，MySQL数据库有表、有字段、有记录，Redis没有这些东西，就是**一个名称对应一个值**，并且**数据以存储在内存中使用为主**。 

什么叫以存储在内存中为主？其实**Redis有它的数据持久化方案，分别是RDB和AOF**，但是**Redis自身并不是为了数据持久化而生的，主要是在内存中保存数据，加速数据访问的，所以说是一款内存级数据库。**

**Redis支持多种数据存储格式**，比如可以直接存字符串，也可以存一个map集合，list集合。 

**Redis优点：**

-   基于内存存储，性能高 
-   适用于存储热点数据（例如热点咨询、商品、秒杀）

**用途：**

-   数据库
-   **缓存**
-   任务队列
-   消息队列
-   分布式锁

**nosql（not only SQL）：泛指非关系型数据库。**

### 1.1 环境准备

#### 1.1.1 Redis下载和安装 

##### 1.1.1.1 **下载**

**windows版安装包下载地址：**[Releases · tporadowski/redis · GitHub](https://github.com/tporadowski/redis/releases "Releases · tporadowski/redis · GitHub")

**linux版下载**地址:[Index of /releases/](http://download.redis.io/releases/ "Index of /releases/")

##### 1.1.1​​​​​​​.2 **linux版安装**

这里下的是4.4.0版本，直接上传到root路径下，分别输入下面命令：

```
tar -zxvf redis-4.0.0.tar.gz -C /usr/local
cd /usr/local/redis-4.0.0
yum install gcc-c++ #安装redis的依赖环境gcc
cd /usr/local
make
cd src
make install
```

命令对应步骤： 

![](https://i-blog.csdnimg.cn/blog_migrate/602f93f426f6a44b3a3d223c2a1cdf28.png)​

##### 1.1.1​​​​​​​.3 **windows版安装**

下载的安装包有两种形式，这里采用的是msi一键安装的msi文件进行安装的。这里下msi，5.0.14版本。

啥是msi，其实就是一个文件安装包，不仅安装软件，还帮你把安装软件时需要的功能关联在一起，打包操作。比如如安装序列、创建和设置安装路径、设置系统依赖项、默认设定安装选项和控制安装过程的属性。说简单点就是一站式服务，安装过程一条龙操作一气呵成，就是为小白用户提供的软件安装程序。

安装时除了路径，其他配置都可以，直接一路next。

安装完毕后会得到如下文件，其中有两个文件对应两个命令，是启动Redis的核心命令，需要再CMD命令行模式执行。

![](https://i-blog.csdnimg.cn/blog_migrate/b0feaee508a0fd51abe0dadede8de8fb.png)​

#### 1.1.2 启动

##### 1.1.2.1 linux版启动**（前台版）**

**启动服务器（前台版）**

```
cd /usr/local/redis-4.0.0/src
./redis-server
```

> .命令：表示执行的意思，就是执行这个文件。
> 
> ./命令：表示执行当前目录下的某个文件，就比如当前目录有一个脚本a.sh，那么./a.sh就表示执行它。

![](https://i-blog.csdnimg.cn/blog_migrate/7f43d929b196c794c0efdacc0d21038a.png)​ 

**新建一个finalshell窗口，启动客户端：**

```
cd /usr/local/redis-4.0.0/src
./redis-cli
```

![](https://i-blog.csdnimg.cn/blog_migrate/582a4326becfbcbd0bbb544ab8b59983.png)​ 

**修改配置：** 

**修改为后台运行服务器：**

ctrl+c停止第一个窗口的服务器

```
cd /usr/local/redis-4.0.0
vim redis.conf
```

修改成后台运行（/dae回车查到后按i进入编辑模式）：

![](https://i-blog.csdnimg.cn/blog_migrate/ea44b0dc2fe2f107dd4962de35bad770.png)​ 

esc后:wq退出vim编辑器。

如果想**设置密码校验**， 就在redis.conf里取消注释：

![](https://i-blog.csdnimg.cn/blog_migrate/1756e431a1d7a4e7758362cf779c4ff5.png)​

登录客户端方式 ![](https://i-blog.csdnimg.cn/blog_migrate/0fc24b61a3b9b832d5c07fa77f49d8ce.png)​

##### 1.1.2.2 **Linux启动服务器（后台版）**

**1.配置**

**设置允许远程连接：**

redis.conf将这行注释掉：![](https://i-blog.csdnimg.cn/blog_migrate/33c91781e9432275e9e230d4d82e630a.png)​

关闭安全模式：

![](https://i-blog.csdnimg.cn/direct/566e8a729b3f4af4ab835a10f1dee8a4.png)

**2.开放端口**

```
firewall-cmd --zone=public --add-port=6379/tcp --permanent
firewall-cmd --reload
```

**3.远程连接：** 

在Windows的redis安装目录下：

```
.\redis-cli.exe -h 虚拟机ip地址 -p 6379 -a 123456 
```

![](https://i-blog.csdnimg.cn/blog_migrate/12b2ec3c96f2824c7d3704a464d4b644.png)​ 

**4.后台运行服务器：**

```

cd /usr/local/redis-4.0.0
src/redis-server ./redis.conf
```

![](https://i-blog.csdnimg.cn/blog_migrate/458b91f0cbff2e60d2bf49732177a523.png)​ 

> 杀掉后台运行的Redis服务器进程：
> 
> ```
> #查看进程号
> ps -ef | grep redis	
> kill -9 进程号
> ```

##### 1.1.2.3 **Windows版启动redis**

**启动服务器**

进入安装文件夹下cmd，命令行启动redis-server.exe并指定配置

```cmd
redis-server.exe redis.windows.conf
```

初学者无需调整服务器对外服务端口，**默认6379**。

> **报错：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/5700bc5c4f74cd65ce0d580e4566c43e.png)​
> 
>  **解决：**要先双击启动客户端redis-cli.exe，然后执行命令shutdown停止客户端、exit回车，再次启动服务器就可以了。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/eacb8f233dae9a2b223334596a505949.png)
> 
> 如果提示下图，则是Redis已经默认启动了：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3707dda073baa399e45fc7af3c57d0cb.png)
> 
> ，可以直接尝试下文的启动客户端。

![](https://i-blog.csdnimg.cn/blog_migrate/5bb391cd275504be1148fdcbfb65fdc7.png)​

**启动客户端**

打开另一个cmd窗口： 

```cmd
redis-cli.exe
```

>  也可以直接双击redis-cli.exe这个文件：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/e966588b9aa9b8a854d7634120393943.png)

如果启动redis服务器失败，可以先启动客户端，然后执行shutdown停止客户端操作后退出，此时redis服务器就可以正常执行了。

服务器启动后，使用客户端就可以连接服务器，类似于启动完MySQL数据库，然后启动SQL命令行操作数据库。

### 1.2 Redis五种数据类型

![](https://i-blog.csdnimg.cn/blog_migrate/df0878400a470158ebba863d9870cb47.png)

### **1.3 Redis常用命令**

#### 通用命令

![](https://i-blog.csdnimg.cn/blog_migrate/d6ec05f980109fa8e7f3427bc1a9eca0.png)​

**查看所有**

```
keys * 
```

删除所有key：

```
FLUSHALL
```

#### **1.3.1 字符串类型string**

**常用命令**

![](https://i-blog.csdnimg.cn/blog_migrate/1c69ec8cc994f36956476c2dab8fcd85.png)​ **更多命令请看官网。** 

**举例：** 

**放置一个字符串数据到redis中**，先为数据定义一个名称，比如name,age等，然后使用命令set设置数据到redis服务器中即可

```cmd
set name itheima
set age 12
```

 **从redis中取出已经放入的数据**，根据名称取，就可以得到对应数据。如果没有对应数据就会得到(nil)

```cmd
get name
get age
```

![](https://i-blog.csdnimg.cn/blog_migrate/b301c88f1f2dfa7f3addda1f25c7983c.png)​ 

#### **1.3.2 哈希存储模型** **hash**

哈希模型适合存储对象。 

 string的数据存储是一个名称对应一个值，如果要维护的数据过多，可以使用**hash哈希存储模型**，**它一个名称下可以存储多个数据**，**每个数据也可以有自己的二级存储名称**。 

**常用命令：**

![](https://i-blog.csdnimg.cn/blog_migrate/4177b5ee2d4aeeb30005a4dc199e26b8.png)​ 

**举例：**

```java
hset a a1 aa1		#对外key名称是a，在名称为哈希存储模型a中，a1这个key中保存了数据aa1
hset a a2 aa2
```

> 这里a可以理解成一个对象，它有a1、a2两个属性。

获取hash结构中的数据命令如下

```cmd
hget a a1			#得到aa1
hget a a2			#得到aa2
```

有关redis的基础操作就普及到这里，需要全面掌握redis技术，请参看相关教程学习。

![](https://i-blog.csdnimg.cn/blog_migrate/97e0b7fd22a881cfade1810249993108.png)​

#### 1.3.3 列表类型list

简单的字符串列表，按照插入 顺序排序。

**常用命令：**

![](https://i-blog.csdnimg.cn/blog_migrate/57b8b657357fb0abb2e9cd903b75253d.png)​![](https://i-blog.csdnimg.cn/blog_migrate/40d2a89d6ae467f7d62225db3c329595.png)​ 

**lpush意思是从左边头部插入 ，rpop意思是从右边尾部删除。**

> -   **在头部插入和遍历，在尾部删除。****对比队列是在队头删除，队尾插入。**
> -   **最后插入的元素在遍历时候排第一个。**

**举例：** 

![](https://i-blog.csdnimg.cn/blog_migrate/d8a061a4de65a419d6d0108d1a690f74.png)​ 

#### 1.3.4 无序集合set

**概念：**

![](https://i-blog.csdnimg.cn/blog_migrate/650445992e6c0fa1e7988f5218abdf0e.png)​ 

**常用命令：**

![](https://i-blog.csdnimg.cn/blog_migrate/bb85b9dba006a731cf2d378eb90da0ac.png)​

**举例：**

![](https://i-blog.csdnimg.cn/blog_migrate/b13d925fac5b0ee63f5da98268e916e0.png)​ 

#### 1.3.4 有序集合sorted set

![](https://i-blog.csdnimg.cn/blog_migrate/a9936b827a08621be0b454a8fb9e906b.png)​ **举例：**

![](https://i-blog.csdnimg.cn/blog_migrate/103a4d694091ad3adf46133ff20fc969.png)​ 

**zset（有序集合） ：**元素有序不可重复，每个元素关联一个可重复的double类型的分数，Redis是通过这个分数对元素排序的。分数可重复，元素

**zset底层存储结构：**ziplist（压缩列表）或skiplist（跳跃表）。

元素数量小于128个，且每个元素长度小于64字节时使用压缩列表，其他情况使用跳跃表。

-   **压缩列表：**本质是一个数组，数组首部存长度、偏移量、元素个数，尾部存结束标识。每个元素使用两个紧挨在一起的压缩列表节点来保存，第一个节点保存元素的成员，第二个节点保存元素的分值。
-   **跳跃表：**单向链表按序保存元素及分值，使用哈希表dict来保存元素和分值的映射关系。链表增加了多级索引，先从最上层索引跳跃查，再渐渐往下层到链表地查询，实现了快速查找元素，时间复杂度O(logn)，这种查询算法类似于链表版二分查找，是基于有序的。

**zset底层不使用红黑树的原因：**

-   **范围查找：**因为红黑树范围查找效率低，而跳跃表范围查找效率高，因为是链表结构。zset可以用zrange命令查指定范围内元素。
-   **实现难度：**跳跃表实现比红黑树简单。

> 压缩列表：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/9e71803405a9d680a2b9945970c5ae96.png)
> 
> 跳跃表zrange： 
> 
> ```bash
> #将a和b两个元素插入到名称为myzset的有序集合中，并为它们分别设置了分值为10和9
> zset myzset 10.0 a 9.0 b    
> #返回所有元素，并按照它们的分值从小到大排列。结果为b和a。0表示第一个元素，-1表示最后一个元素
> zrange myzset 0 -1  
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/00f55c4aa0bd18526884fcd536ec87a9.png)

## **2 springboot整合redis** 

### **2.1 lettucs客户端技术操作Redis，默认**

#### **2.1.1 RedisTemplate对象**

![](https://i-blog.csdnimg.cn/blog_migrate/dba5400542d8f82f7a2d753b1b4c99a8.png)

在进行整合之前先梳理一下整合的思想，**springboot整合任何技术其实就是在springboot中使用对应技术的API**。如果两个技术没有交集，就不存在整合的概念了。所谓**整合其实就是使用springboot技术去管理其他技术**，几个问题是躲不掉的。

**第一，需要先导入对应技术的坐标**，而整合之后，这些坐标都有了一些变化

**第二，任何技术通常都会有一些相关的设置信息**，整合之后，这些信息如何写，写在哪是一个问题

**第三**，没有整合之前操作如果是模式A的话，整合之后如果没有给开发者带来一些便捷操作，那整合将毫无意义，所以**整合后操作肯定要简化一些，那对应的操作方式自然也有所不同**

按照上面的三个问题去思考springboot整合所有技术是一种通用思想，在整合的过程中会逐步摸索出整合的套路，而且适用性非常强，经过若干种技术的整合后基本上可以总结出一套固定思维。

**springboot整合redis步骤：**

**步骤①**：**导入springboot整合redis的starter坐标**

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

上述坐标可以在创建模块的时候通过勾选的形式进行选择，归属NoSQL分类中

![](https://i-blog.csdnimg.cn/blog_migrate/daeb9e69f66a037eab7f0cfdedc1a403.png)​

> **tip:**第二行spring data reactive redis包含了第一行Redis的驱动和访问，现在阶段只用第一行就够了。

**步骤②**：**进行基础配置**

**默认配置：** 

```yaml
spring:
  data:
    redis:
      host: localhost
      port: 6379
```

**操作redis，最基本的信息就是操作哪一台redis服务器，所以服务器地址属于基础配置信息，不可缺少。**但是即便你不配置，目前也是可以用的。因为以上两组信息都是**默认配置值**，刚好就是上述配置值。

> **更丰富配置：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bfae40f9bf515151c7c17eca98e73b04.png)
> 
> **小贴士:**
> 
> -   这里database: 0的意思是使用0号数据库，在redis服务器启动后默认提供了16个数据库，不同数据库内容不互通，**默认使用0号数据库**。
> -   **修改Redis提供数据库数量：**
> 
> conf文件：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8e5d3e66f53c57318e9a81cb6436b0a0.png)
> 
> -   **切换成数据库1：**
> 
> 客户端命令行
> 
> ```XML
> select 1
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/038236bc67261f36933d1cf5e284cac6.png)

**步骤③：确保之前启动服务器后，自动注入Redis模板对象，获取值操作对象对数据增删改查。**

此处使用的是注入Redis模板对象RedisTemplate的opsForValue()方法获取值操作对象ValueOperations ，通过ValueOperations对象的get和set方法操作数据库。

```java
@SpringBootTest
class Springboot16RedisApplicationTests {
    //自动注入RedisTemplate对象
    @Autowired
    private RedisTemplate redisTemplate;
    //注意ValueOperations 添加是set，HashOperations 添加是put
    @Test
    void set() {
        //获取值简单k-v操作对象ValueOperations。如果想获取hash操作对象要用opsForHash()方法。
        ValueOperations ops = redisTemplate.opsForValue();
        ops.set("age",41);
    }
    @Test
    void get() {
        ValueOperations ops = redisTemplate.opsForValue();
        Object age = ops.get("name");
        System.out.println(age);
    }
    @Test
    void hset() {
        //获取hash类型操作对象HashOperations 
        HashOperations ops = redisTemplate.opsForHash();
        ops.put("info","b","bb");
    }
    @Test
    void hget() {
        HashOperations ops = redisTemplate.opsForHash();
        //hash操作对象的get返回值类型是Object，可以强转为String
        Object val = ops.get("info", "b");
        System.out.println(val);
        //获取keys
        System.out.println(ops.keys("*"));
        System.out.println(ops.keys("info"));
    }

```

**操作list类型数据：**

![](https://i-blog.csdnimg.cn/blog_migrate/96523ff0aae54c23bb4e8f0b7255b9ec.png) **操作set类型数据：**

 ![](https://i-blog.csdnimg.cn/blog_migrate/b5fa542f345ea758065c23f92497a9b5.png)

**操作zset类型数据：**

 ![](https://i-blog.csdnimg.cn/blog_migrate/943dfec4982082bf4fc223c8586ff43a.png)

![](https://i-blog.csdnimg.cn/blog_migrate/e525014848e25ef9eb1176a86bb525cf.png)

**通用命令：**

![](https://i-blog.csdnimg.cn/blog_migrate/8eafef21d95e8eeb19a6a5d4a19e1ac4.png) ![](https://i-blog.csdnimg.cn/blog_migrate/eab2cd7f8c9069a4e060e8a24c96cbc1.png)

在操作redis时，需要先确认操作何种数据，根据数据种类得到操作接口。例如使用opsForValue()获取string类型的数据操作接口，使用opsForHash()获取hash类型的数据操作接口，剩下的就是调用对应api操作了。各种类型的数据操作接口如下：

![](https://i-blog.csdnimg.cn/blog_migrate/eee77e511dccdaa3889df84f073dab9f.png)​![](https://i-blog.csdnimg.cn/blog_migrate/dba5400542d8f82f7a2d753b1b4c99a8.png)

#### **2.1.2 序列化器问题**

**RedisTemplate是以对象为操作的基本单元，存到数据库的实际内容是序列化后的。**

通过命令行看到是乱码的：

![](https://i-blog.csdnimg.cn/blog_migrate/1ba2fe757fa9a1a8282474ae424f78f6.png)​

**修改key的序列化器，由jdk序列化器修改为字符串序列化器：**

**方法一，配置类：**

```java
package com.jq.config;

import org.springframework.cache.annotation.CachingConfigurerSupport;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.StringRedisSerializer;
/**
 * Redis配置类
 */
@Configuration
public class RedisConfig extends CachingConfigurerSupport{
    
    @Bean
    public RedisTemplate<Object, Object> redisTemplate(RedisConnectionFactory connectionFactory) {

        RedisTemplate<Object, Object> redisTemplate = new RedisTemplate<>();

        //默认的Key序列化器为：JdkSerializationRedisSerializer
        redisTemplate.setKeySerializer(new StringRedisSerializer());
        redisTemplate.setHashKeySerializer(new StringRedisSerializer());

        redisTemplate.setConnectionFactory(connectionFactory);

        return redisTemplate;
    }

}

```

 测试后可以发现key已经成字符串序列化，而value依然还是jdk序列化，这里就不改了，不影响使用：

![](https://i-blog.csdnimg.cn/blog_migrate/0dea03b09277c31c7fa9227d048935e2.png)

 **方法二：使用下一节的StringRedisTemplate**

> **总结**
> 
> 1.  springboot整合redis步骤
>     
>     1.  导入springboot整合redis的starter坐标
>     2.  进行基础配置
>     3.  使用springboot整合redis的专用客户端接口RedisTemplate操作

#### **2.1.3 StringRedisTemplate对象，命令行模式默认**

>  **RedisTemplate**是以对象为操作的基本单元，存到数据库的实际内容是序列化后的。**StringRedisTemplate**是以字符串为操作的基本单元。两个类创建的对象获取数据是不通用的，命令行客户端redis-cli.exe默认使用**StringRedisTemplate。**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/1ba2fe757fa9a1a8282474ae424f78f6.png)​

**由于redis内部不提供java对象的存储格式，因此当操作的数据以对象的形式存在时，会进行转码，转换成字符串格式后进行操作。**为了方便开发者使用**基于字符串为数据的操作**，springboot整合redis时提供了**专用的API接口StringRedisTemplate**，你可以理解为这是RedisTemplate的一种指定数据泛型的操作API。

```java
@SpringBootTest
public class StringRedisTemplateTest {
    @Autowired
    private StringRedisTemplate stringRedisTemplate;
    @Test
    void get(){
        ValueOperations<String, String> ops = stringRedisTemplate.opsForValue();
        String name = ops.get("name");
        System.out.println(name);
    }
}
```

### **2.2 切换jedis客户端技术**

#### **2.2.1 RedisTemplate或者StringRedisTemplate** 

**springboot整合redis技术提供了多种客户端兼容模式，默认提供的是lettucs客户端技术**，也可以根据需要切换成指定客户端技术，例如jedis客户端技术。jedis是Redis传统的客户端技术。

**从默认客户端技术lettucs切换成jedis客户端技术：**  
**步骤①**：**导入jedis坐标。**不用加版本号，该坐标被springboot管理。

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
</dependency>
```

> 先确保导入了redis的starter坐标：
> 
> ```XML
> <dependency>
>     <groupId>org.springframework.boot</groupId>
>     <artifactId>spring-boot-starter-data-redis</artifactId>
> </dependency>
> ```

jedis坐标受springboot管理，无需提供版本号

**步骤②**：**配置客户端技术类型，设置为jedis**

```yaml
spring:
  redis:
    host: localhost
    port: 6379
    client-type: jedis
```

> **也可以根据需要设置对应的配置**
> 
> ```yaml
> spring:
>   redis:
>     host: localhost
>     port: 6379
>     client-type: jedis
>     lettuce:
>       pool:
>         max-active: 16
>     jedis:
>       pool:
>         max-active: 16
> ```

**步骤③： 整合方法和lettucs一样**

**使用RedisTemplate对象或者StringRedisTemplate对象。**

```java
@SpringBootTest
class Springboot16RedisApplicationTests {
    //自动注入RedisTemplate对象
    @Autowired
    private RedisTemplate redisTemplate;
    //注意ValueOperations 添加是set，HashOperations 添加是put
    @Test
    void set() {
        //获取值操作对象。如果想获取hash操作对象要用opsForHash()方法。
        ValueOperations ops = redisTemplate.opsForValue();
        ops.set("age",41);
    }
    @Test
    void get() {
        ValueOperations ops = redisTemplate.opsForValue();
        Object age = ops.get("name");
        System.out.println(age);
    }
    @Test
    void hset() {
        HashOperations ops = redisTemplate.opsForHash();
        ops.put("info","b","bb");
    }
    @Test
    void hget() {
        HashOperations ops = redisTemplate.opsForHash();
        Object val = ops.get("info", "b");
        System.out.println(val);
    }
}
 
```

> **非Maven项目使用jedis的方法：**
> 
> jedis以字符串为操作的基本单元，代码里添加的数据，在命令行模式也能查到。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/708bd25b0f79f3c3885b36adf9f83046.png)

#### **2.2.2 lettcus与jedis区别**

-   **jedis连接Redis服务器是直连模式，当多线程模式下使用jedis会存在线程安全问题**，解决方案可以通过配置连接池使每个连接专用，这样整体性能就大受影响
-   **lettcus基于Netty框架进行与Redis服务器连接**，底层设计中采用StatefulRedisConnection。 StatefulRedisConnection自身是**线程安全的，可以保障并发访问安全问题，所以一个连接可以被多线程复用。**当然lettcus也支持多连接实例一起工作

> **总结**
> 
> 1.  springboot整合redis提供了StringRedisTemplate对象，以字符串的数据格式操作redis
> 2.  如果需要切换redis客户端实现技术，可以通过配置的形式进行

## 3 Spring Cache

### 3.1 Spring Cache介绍

**Spring Cache是一个框架，实现了基于注解的缓存功能**，只需要简单地加一个注解，就能实现缓存功能。

Spring Cache提供了一层抽象，底层可以**切换不同的cache实现**。具体就是**通过CacheManager接口来统一不同的缓存技术。** CacheManager是Spring提供的各种缓存技术抽象接口。

![](https://i-blog.csdnimg.cn/blog_migrate/ba0350033b8f879ffceea4bad129ebf5.png)

前面学springboot3开发篇时候有简单讲过整合各种缓存技术：

[【黑马Java笔记】SpringBoot基础3——开发\_vincewm的博客-CSDN博客\_site:csdn.net](https://blog.csdn.net/qq_40991313/article/details/126526529?spm=1001.2014.3001.5501 "【黑马Java笔记】SpringBoot基础3——开发_vincewm的博客-CSDN博客_site:csdn.net")

### 3.2 Spring Cache常用注解

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/eac9c1c1175491611b099726ebc2f7b2.png)

#### 3.2.1 依赖、 yml配置、开启缓存

**环境准备**

**导入坐标：**

```XML
 <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-data-redis</artifactId>
 </dependency>
 <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-cache</artifactId>
 </dependency>
```

**yml配置端口：**

```bash
spring:
  redis:
    host: localhost
    port: 6379
  cache:
    type: redis
    redis:
#默认带缓存空间名前缀，例如"ssmCode::12345678"，不加前缀重复可能大，如"12345678"
      use-key-prefix: true
#指定前缀，默认是缓存空间名
      key-prefix: sms_
#是否缓存空值，防止缓存穿透。这个是全局的，也可以在@Cacheable的属性unless="#result==null"局部排除
      cache-null-values: false
#生存时间
      time-to-live: 10s
```

**主启动类开启缓存：**

```java
@SpringBootApplication
//开启过滤器。在SpringBootApplication上使用@ServletComponentScan注解后，Servlet、Filter、Listener可以直接通过@WebServlet、@WebFilter、@WebListener注解自动注册，无需其他代码。
@ServletComponentScan
@EnableTransactionManagement
//开启缓存
@EnableCaching
@Slf4j
public class ReggieApplication {

    public static void main(String[] args) {

        SpringApplication.run(ReggieApplication.class, args);
        log.info("引导类已经启动。。。。");
    }

}
```

> 在spring boot项目中，使用缓存技术只需在项目中**导入相关缓存技术的依赖包**，并在**启动类上使用`@EnableCaching`开启缓存**支持即可。 例如，使用Redis作为缓存技术，只需要导入Spring data Redis的maven坐标即可。

#### 3.2.2 key的命名方式 

**示例** 

```java
    //value是缓存名称，一个value下有多个key
    //key是缓存的key，key="#tele"是将方法返回值存到key里。
    @CachePut(value = "smsCode", key = "#tele")
```

**固定key：**

```java
@Cacheable(value="users", key="'key'")    

   public User find(Integer id) {

      returnnull;

   }
```

**变量key：**

**1.直接使用“#参数名”或者“#p参数index”：**

```java
@Cacheable(value="users", key="#id")    //也可以是key="#p0"

   public User find(Integer id) {

      returnnull;

   }


   @Cacheable(value="users", key="#user.id")    //也可以是key="#p0.id"

   public User find(User user) {

      returnnull;

   }
```

**2.root对象可以用来生成key** 

![](https://i-blog.csdnimg.cn/blog_migrate/eb1fab77d1fa4d5e5fa72f31a6040a74.png)

> 当我们要使用root对象的属性作为key时我们也可以**将“#root”省略**，因为Spring默认使用的就是root对象的属性。如：
> 
> ```java
>    @Cacheable(value={"users", "xxx"}, key="caches[1].name")
> 
>    public User find(User user) {
> 
>       returnnull;
> 
>    }
> ```

3.key="#result.tele"是将返回值存到key里，result.是默认可省略。 

#### 3.2.3 注解实现缓存

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/eac9c1c1175491611b099726ebc2f7b2.png)

```java
    @PostMapping
    //allEntries 属性是删除此命名空间下所有的key
    @CacheEvict(value = "setmealCache",allEntries = true)
    public R<String> save(@RequestBody SetmealDto setmealDto) {
        Setmeal setmeal = new Setmeal();
        if (setmealService.saveWithDish(setmealDto)) return R.success("保存成功");
        else return R.error("保存失败");
    }
```

![](https://i-blog.csdnimg.cn/blog_migrate/48872ce855614ee2564463b3d45b69a3.png)

> **注意：**
> 
> -   **@Cacheable和@CachePut都是方法注解，缓存的是返回值**
> -   **@CachePut只存不取**

### 3.3  Spring Cache使用各种缓存

在导入对应坐标后，**通过配置可以切换缓存方法。**

springboot提供了缓存的统一整合接口，方便缓存技术的开发和管理：

![](https://i-blog.csdnimg.cn/blog_migrate/0f15ac4f581e51353ae95c2e7712c89b.png)

#### 3.3.1 SpringBoot内置缓存Simple

springboot技术提供有内置的缓存解决方案，可以帮助开发者快速开启缓存技术，并使用缓存技术进行数据的快速操作，例如读取缓存数据和写入数据到缓存。

**步骤①**：**导入springboot提供的缓存技术对应的starter**

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

**步骤②**：**开启缓存功能**，在**引导类**上方标注注解**@EnableCaching**配置springboot程序中可以使用缓存

```java
@SpringBootApplication
//开启缓存功能
@EnableCaching
public class Springboot19CacheApplication {
    public static void main(String[] args) {
        SpringApplication.run(Springboot19CacheApplication.class, args);
    }
}
```

**步骤③**：**设置操作的数据是否使用缓存**

```java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    private BookDao bookDao;
    //Cacheable译为可缓存的，可缓冲的。@Cacheable的value属性是存储空间名，key属性是此方法返回值在存储空间内的键名。
    //key属性名必须和形参名一样才能缓存，别忘了#号
    @Cacheable(value="cacheSpace",key="#id")
    public Book getById(Integer id) {
        return bookDao.selectById(id);
    }
}
```

> **注意：**
> 
> -   **一定一定别忘了#号**
> -   **缓存的key属性名必须方法的形参名一样才能缓存。** **只要此key对应的缓存已存在，下次不管查询出什么数据，返回的结果都是直接从缓存的这个key里取。**
> -   **被注解@Cacheable声明的方法不能被本类中其他方法调用，原因是spring容器管理问题。**

**在业务方法上面使用注解@Cacheable声明当前方法的返回值放入缓存中，其中要指定缓存的存储位置，以及缓存中保存当前方法返回值对应的名称。**上例中value属性描述缓存的存储位置，可以理解为是一个存储空间名，key属性描述了缓存中保存数据的名称，使用**#id**读取形参中的id值作为缓存名称。

使用@Cacheable注解后，执行当前操作，**如果发现对应名称在缓存中没有数据，就正常读取数据，然后放入缓存；如果对应名称在缓存中有数据，就终止当前业务方法执行，直接返回缓存中的数据。**

**测试缓存已经实现：**

使用postman根据id查询：

![](https://i-blog.csdnimg.cn/blog_migrate/240c9f3f112e4e8471b6e212dd18c176.png)

 查询多次同一个id，会发现控制台只会输出第一次数据库查询日志：

![](https://i-blog.csdnimg.cn/blog_migrate/6512538f85609d4897a123975273a801.png)

#### 3.3.2 手机验证码模拟案例，@CachePut

为了便于下面演示各种各样的缓存技术，我们创建一个手机验证码的案例环境，模拟使用缓存保存手机验证码的过程。

> 手机验证码案例需求如下：
> 
> -   输入手机号获取验证码，组织文档以短信形式发送给用户（页面模拟）
> -   输入手机号和验证码验证结果

为了描述上述操作，我们制作两个表现层接口，一个用来模拟发送短信的过程，其实就是根据用户提供的手机号生成一个验证码，然后放入缓存，另一个用来模拟验证码校验的过程，其实就是使用传入的手机号和验证码进行匹配，并返回最终匹配结果。下面直接制作本案例的模拟代码，先以上例中springboot提供的内置缓存技术来完成当前案例的制作。

**步骤①**：**导入springboot提供的缓存技术对应的starter**

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

**步骤②**：**启用缓存，在引导类上方标注注解@EnableCaching配置springboot程序中可以使用缓存**

```java
@SpringBootApplication
//开启缓存功能
@EnableCaching
public class Springboot19CacheApplication {
    public static void main(String[] args) {
        SpringApplication.run(Springboot19CacheApplication.class, args);
    }
}
```

**步骤③**：**定义验证码对应的实体类，封装手机号与验证码两个属性**

```java
@Data
public class SMSCode {
    private String tele;
    private String code;
}
```

**步骤④**：**定义验证码功能的业务层接口与实现类**

这里是要新建另外一个工具类，把验证码的生成和获取写在工具类中，并加上缓存注解，然后通过service调用，从而实现缓存。**注意不能直接给service的获取和检查方法设置缓存注解**，因为检查时候它不能直接调用本类的获取方法，spring管理bean的问题。

```java
public interface SMSCodeService {
    public String sendCodeToSMS(String tele);
    public boolean checkCode(SMSCode smsCode);
}

@Service
public class SMSCodeServiceImpl implements SMSCodeService {
    @Autowired
    private CodeUtils codeUtils;
    

    public String sendCodeToSMS(String tele) {
        //使用工具类是为了使用后面的检查方法
        String code = codeUtils.generator(tele);
        return code;
    }
    //取出内存中的验证码与传递过来的验证码比对，如果相同，返回true。
    //参数是包括手机号和验证码的实体类
    public boolean checkCode(SMSCode smsCode) {
        //获取controller传来实体对象的验证码
        String code = smsCode.getCode();
        //获取缓存中的验证码，注意这里必须要使用工具类调用get方法，如果只设置service，直接调用本service里的get方法不是spring容器管理的。
        String cacheCode = codeUtils.get(smsCode.getTele());
        return code.equals(cacheCode);
    }
}
```

获取验证码后，当验证码失效时必须重新获取验证码，因此在获取验证码的功能上不能使用@Cacheable注解，**@Cacheable注解是缓存中没有值则放入值，缓存中有值则取值。**此处的功能仅仅是生成验证码并放入缓存，并不具有从缓存中取值的功能，因此不能使用@Cacheable注解，应该使用仅具有向缓存中保存数据的功能，使用@CachePut注解即可。

对于校验验证码的功能建议放入工具类中进行。

**步骤⑤**：**定义验证码的生成策略与根据手机号读取验证码的功能**

> **不能只用service就实现所检查验证码功能 ，因为被注解@Cacheable声明的方法不能被本类中其他方法调用，原因是spring容器管理问题。**

```java
@Component
public class CodeUtils {
    //补0，防止最终生成验证码转字符串后前几位是0
    private String [] patch = {"000000","00000","0000","000","00","0",""};
    //加密算法生成验证码
    //注解@CachePut是仅把返回值放到缓存里，而不自己取。如果还用@Cacheable多次发验证码，内存值都是第一次的缓存值。
    @CachePut(value = "smsCode", key = "#tele")
    public String generator(String tele){
        //获取手机号字符串的哈希码
        int hash = tele.hashCode();
        //定义加密码
        int encryption = 20206666;
        //哈希码加密码、时间戳分别异或，进行加密
        long result = hash ^ encryption;
        long nowTime = System.currentTimeMillis();
        result = result ^ nowTime;
        long code = result % 1000000;
        code = code < 0 ? -code : code;
        String codeStr = code + "";
        int len = codeStr.length();
        //防止验证码不到6位，补0
        return patch[len] + codeStr;
    }
    //获取缓存中的验证码。
    @Cacheable(value = "smsCode",key="#tele")
    //这里形参名必须和@Cacheable的key名一致。当缓存中对应key有值时，不管返回值是什么都会返回缓存中的值
    public String get(String tele){
        return null;
    }
}
```

**步骤⑥**：**定义验证码功能的web层接口，一个方法用于提供手机号获取验证码，一个方法用于提供手机号和验证码进行校验**

```java
@RestController
@RequestMapping("/sms")
public class SMSCodeController {
    @Autowired
    private SMSCodeService smsCodeService;
    
    @GetMapping
    public String getCode(String tele){
        String code = smsCodeService.sendCodeToSMS(tele);
        return code;
    }
    
    @PostMapping
    public boolean checkCode(SMSCode smsCode){
        return smsCodeService.checkCode(smsCode);
    }
}
```

#### 3.3.3 Spring Cache使用Redis

**引入maven依赖**

使用Redis作为缓存技术，只需要导入Spring data Redis的maven

```XML
 <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-cache</artifactId>
 </dependency>

 <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-data-redis</artifactId>
 </dependency>
```

**配置：**

```bash
spring:
  redis:
    host: localhost
    port: 6379
  cache:
    type: redis
    redis:
#默认带缓存空间名前缀，例如"ssmCode::12345678"，不加前缀重复可能大，如"12345678"
      use-key-prefix: true
#指定前缀，默认是缓存空间名
      key-prefix: sms_
#是否缓存空值，防止缓存穿透。这个是全局的，也可以在@Cacheable的属性unless="#result==null"局部排除
      cache-null-values: false
#生存时间
      time-to-live: 10s
```

**Java代码**

```java
@RestController
@RequestMapping("/user")
@Slf4j
public class UserController {

    @Autowired
    private CacheManager cacheManager;

    @Autowired
    private UserService userService;

    /**
      CachePut：将方法返回值放入缓存
      value：缓存的名称，每个缓存名称下面可以有多个key
      key：缓存的key
     /
    @CachePut(value = "userCache",key = "#user.id")
    @PostMapping
    public User save(User user){
        userService.save(user);
        return user;
    }

    /**
      CacheEvict：清理指定缓存
      value：缓存的名称，每个缓存名称下面可以有多个key
      key：缓存的key
     /
    @CacheEvict(value = "userCache",key = "#p0")
    //@CacheEvict(value = "userCache",key = "#root.args[0]")
    //@CacheEvict(value = "userCache",key = "#id")
    @DeleteMapping("/{id}")
    public void delete(@PathVariable Long id){
        userService.removeById(id);
    }

    //@CacheEvict(value = "userCache",key = "#p0.id")
    //@CacheEvict(value = "userCache",key = "#user.id")
    //@CacheEvict(value = "userCache",key = "#root.args[0].id")
    @CacheEvict(value = "userCache",key = "#result.id")
    @PutMapping
    public User update(User user){
        userService.updateById(user);
        return user;
    }

    /**
      Cacheable：在方法执行前spring先查看缓存中是否有数据，如果有数据，则直接返回缓存数据；若没有数据，调用方法并将方法返回值放到缓存中
      value：缓存的名称，每个缓存名称下面可以有多个key
      key：缓存的key
      condition：条件，满足条件时才缓存数据
      unless：满足条件则不缓存
     */
    @Cacheable(value = "userCache",key = "#id",unless = "#result == null")
    @GetMapping("/{id}")
    public User getById(@PathVariable Long id){
        User user = userService.getById(id);
        return user;
    }

    @Cacheable(value = "userCache",key = "#user.id + '_' + #user.name")
    @GetMapping("/list")
    public List<User> list(User user){
        LambdaQueryWrapper<User> queryWrapper = new LambdaQueryWrapper<>();
        queryWrapper.eq(user.getId() != null,User::getId,user.getId());
        queryWrapper.eq(user.getName() != null,User::getName,user.getName());
        List<User> list = userService.list(queryWrapper);
        return list;
    }
}
```