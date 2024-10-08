>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1.分布式事务问题](#1.%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1%E9%97%AE%E9%A2%98)

[1.1.本地事务](#1.1.%E6%9C%AC%E5%9C%B0%E4%BA%8B%E5%8A%A1)

[1.1.1.MySQL事务的ACID原则](#1.1.1.ACID%E5%8E%9F%E5%88%99%C2%A0) 

[1.1.2.MySQL事务的隔离级别](#1.1.2.%E4%BA%8B%E5%8A%A1%E7%9A%84%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB%C2%A0) 

[1.1.3.事务的传播行为](#1.1.3.%E4%BA%8B%E5%8A%A1%E7%9A%84%E4%BC%A0%E6%92%AD%E8%A1%8C%E4%B8%BA)

[1.1.4.本地事务代理对象、事务传播行为不生效问题](#1.1.4.%E6%9C%AC%E5%9C%B0%E4%BA%8B%E5%8A%A1%E4%BB%A3%E7%90%86%E5%AF%B9%E8%B1%A1%E3%80%81%E4%BA%8B%E5%8A%A1%E4%BC%A0%E6%92%AD%E8%A1%8C%E4%B8%BA%E4%B8%8D%E7%94%9F%E6%95%88%E9%97%AE%E9%A2%98)

[1.2.分布式事务](#1.2.%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1)

[1.3.演示分布式事务问题](#1.3.%E6%BC%94%E7%A4%BA%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1%E9%97%AE%E9%A2%98)

[2.理论基础](#2.%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80)

[2.1.CAP定理](#2.1.CAP%E5%AE%9A%E7%90%86)

[2.1.1.一致性C：数据同步](#2.1.1.%E4%B8%80%E8%87%B4%E6%80%A7)

[2.1.2.可用性A：节点正常访问](#2.1.2.%E5%8F%AF%E7%94%A8%E6%80%A7)

[2.1.3.分区容错P：分区后也要对外提供服务](#2.1.3.%E5%88%86%E5%8C%BA%E5%AE%B9%E9%94%99)

[2.1.4.矛盾](#2.1.4.%E7%9F%9B%E7%9B%BE)

[2.2.BASE理论](#2.2.BASE%E7%90%86%E8%AE%BA)

[2.3.解决分布式事务的思路，最终一致和强一致](#2.3.%E8%A7%A3%E5%86%B3%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1%E7%9A%84%E6%80%9D%E8%B7%AF)

[3.初识Seata](#3.%E5%88%9D%E8%AF%86Seata)

[3.1.Seata的架构，TC,TM,RM](#3.1.Seata%E7%9A%84%E6%9E%B6%E6%9E%84)

[3.2.部署Seata的TC（事务协调者）服务，tc-server](#3.2.%E9%83%A8%E7%BD%B2TC%E6%9C%8D%E5%8A%A1)

[1.下载](#1.%E4%B8%8B%E8%BD%BD)

[2.解压](#2.%E8%A7%A3%E5%8E%8B)

[3.registry.conf修改Seata的注册中心、配置中心](#3.%E4%BF%AE%E6%94%B9%E9%85%8D%E7%BD%AE)

[4.在nacos添加配置](#4.%E5%9C%A8nacos%E6%B7%BB%E5%8A%A0%E9%85%8D%E7%BD%AE)

[5.创建数据库表，分支事务表和全局事务表](#5.%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A1%A8)

[6.启动TC服务](#6.%E5%90%AF%E5%8A%A8TC%E6%9C%8D%E5%8A%A1)

[3.3.微服务集成Seata](#%E4%BA%8C%E3%80%81%E5%BE%AE%E6%9C%8D%E5%8A%A1%E9%9B%86%E6%88%90seata)

[3.3.1.引入依赖](#3.3.1.%E5%BC%95%E5%85%A5%E4%BE%9D%E8%B5%96)

[3.3.2.配置TC地址](#3.3.2.%E9%85%8D%E7%BD%AETC%E5%9C%B0%E5%9D%80)

[3.3.3.其它服务](#3.3.3.%E5%85%B6%E5%AE%83%E6%9C%8D%E5%8A%A1)

[4.详解Seata的四种分布式事务方案](#4.%E5%8A%A8%E6%89%8B%E5%AE%9E%E8%B7%B5)

[4.1.XA模式，两阶段都加锁](#4.1.XA%E6%A8%A1%E5%BC%8F)

[4.1.1.两阶段提交](#4.1.1.%E4%B8%A4%E9%98%B6%E6%AE%B5%E6%8F%90%E4%BA%A4)

[4.1.2.Seata的XA模型](#4.1.2.Seata%E7%9A%84XA%E6%A8%A1%E5%9E%8B)

[4.1.3.优缺点](#4.1.3.%E4%BC%98%E7%BC%BA%E7%82%B9)

[4.1.4.实现XA模式](#4.1.4.%E5%AE%9E%E7%8E%B0XA%E6%A8%A1%E5%BC%8F)

[4.2.AT模式：一阶段直接提交，二阶段统一回滚](#4.2.AT%E6%A8%A1%E5%BC%8F)

[4.2.1.Seata的AT模型](#4.2.1.Seata%E7%9A%84AT%E6%A8%A1%E5%9E%8B)

[4.2.2.流程梳理](#4.2.2.%E6%B5%81%E7%A8%8B%E6%A2%B3%E7%90%86)

[4.2.3.AT与XA的区别](#4.2.3.AT%E4%B8%8EXA%E7%9A%84%E5%8C%BA%E5%88%AB)

[4.2.4.脏写问题，全局锁](#4.2.4.%E8%84%8F%E5%86%99%E9%97%AE%E9%A2%98)

[4.2.5.优缺点](#4.2.5.%E4%BC%98%E7%BC%BA%E7%82%B9)

[4.2.6.实现AT模式（完整流程）](#4.2.6.%E5%AE%9E%E7%8E%B0AT%E6%A8%A1%E5%BC%8F)

[4.2.7.@Transactional和@GlobalTransactional对比](#4.2.7.%40Transactional%E5%92%8C%40GlobalTransactional%E5%AF%B9%E6%AF%94)

[4.3.TCC模式：基于资源预留](#4.3.TCC%E6%A8%A1%E5%BC%8F)

[4.3.1.流程分析](#4.3.1.%E6%B5%81%E7%A8%8B%E5%88%86%E6%9E%90)

[4.3.2.Seata的TCC模型](#4.3.2.Seata%E7%9A%84TCC%E6%A8%A1%E5%9E%8B)

[4.3.3.优缺点](#4.3.3.%E4%BC%98%E7%BC%BA%E7%82%B9)

[4.3.4.事务悬挂和空回滚](#4.3.4.%E4%BA%8B%E5%8A%A1%E6%82%AC%E6%8C%82%E5%92%8C%E7%A9%BA%E5%9B%9E%E6%BB%9A)

[4.3.5.下单代码实现TCC模式，@TwoPhaseBusinessAction，@BusinessActionContextParameter，](#4.3.5.%E5%AE%9E%E7%8E%B0TCC%E6%A8%A1%E5%BC%8F)

[4.4.SAGA模式：基于一系列本地事务](#4.4.SAGA%E6%A8%A1%E5%BC%8F)

[4.4.1.原理](#4.4.1.%E5%8E%9F%E7%90%86)

[4.4.2.优缺点](#4.4.2.%E4%BC%98%E7%BC%BA%E7%82%B9)

[4.5.四种模式对比，XA,AT,TCC,SAGA](#4.5.%E5%9B%9B%E7%A7%8D%E6%A8%A1%E5%BC%8F%E5%AF%B9%E6%AF%94)

[5.其他分布式事务方案（不使用Seata）](#5.%E5%85%B6%E4%BB%96%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1%E6%96%B9%E6%A1%88%EF%BC%88%E4%B8%8D%E4%BD%BF%E7%94%A8Seata%EF%BC%89)

[5.1.柔性事务方法实现最终一致性](#4.6.%E6%9F%94%E6%80%A7%E4%BA%8B%E5%8A%A1%E6%96%B9%E6%B3%95%E8%A7%A3%E5%86%B3%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A1%EF%BC%88%E4%B8%8D%E4%BD%BF%E7%94%A8Seata%EF%BC%89)

[5.1.1.柔性事务-最大努力通知型方案](#4.6.1.%E6%9F%94%E6%80%A7%E4%BA%8B%E5%8A%A1-%E6%9C%80%E5%A4%A7%E5%8A%AA%E5%8A%9B%E9%80%9A%E7%9F%A5%E5%9E%8B%E6%96%B9%E6%A1%88)

[5.1.2.柔性事务-可靠消息+最终一致性方案（异步确保型）](#4.6.2.%E6%9F%94%E6%80%A7%E4%BA%8B%E5%8A%A1-%E5%8F%AF%E9%9D%A0%E6%B6%88%E6%81%AF%2B%E6%9C%80%E7%BB%88%E4%B8%80%E8%87%B4%E6%80%A7%E6%96%B9%E6%A1%88%EF%BC%88%E5%BC%82%E6%AD%A5%E7%A1%AE%E4%BF%9D%E5%9E%8B%EF%BC%89)

[5.2.xxl-job和消息组件实现最终一致性](#5.2.xxl-job%E5%92%8C%E6%B6%88%E6%81%AF%E7%BB%84%E4%BB%B6%E5%AE%9E%E7%8E%B0%E6%9C%80%E7%BB%88%E4%B8%80%E8%87%B4%E6%80%A7)

[6.高可用](#5.%E9%AB%98%E5%8F%AF%E7%94%A8)

[6.1.高可用架构模型](#5.1.%E9%AB%98%E5%8F%AF%E7%94%A8%E6%9E%B6%E6%9E%84%E6%A8%A1%E5%9E%8B)

[6.2.实现高可用，异地容灾](#5.2.%E5%AE%9E%E7%8E%B0%E9%AB%98%E5%8F%AF%E7%94%A8)

[6.2.1.模拟异地容灾的TC集群](#1.%E6%A8%A1%E6%8B%9F%E5%BC%82%E5%9C%B0%E5%AE%B9%E7%81%BE%E7%9A%84TC%E9%9B%86%E7%BE%A4)

[6.2.2.将事务组映射配置到nacos](#2.%E5%B0%86%E4%BA%8B%E5%8A%A1%E7%BB%84%E6%98%A0%E5%B0%84%E9%85%8D%E7%BD%AE%E5%88%B0nacos)

[3.微服务读取nacos配置](#3.%E5%BE%AE%E6%9C%8D%E5%8A%A1%E8%AF%BB%E5%8F%96nacos%E9%85%8D%E7%BD%AE)

--

## 1.分布式事务问题

### 1.1.本地事务

#### 1.1.1.MySQL事务的ACID原则 

只要是事务，就必须要**满足四个原则：**

ACID是指事务四个特性：原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）和持久性（Durability）。

**原子性：**事务的所有操作，要么全部成功，要么全部失败。 

**一致性：**事务前后，数据库的约束没有被破坏，保持前后一致。

**隔离性：**操作同一资源的并发事务之间相互隔离，不会互相干扰。

**持久性：**事务的结果最终一定会持久化到数据库，宕机等故障也无法影响。

![image-20210724165045186](https://i-blog.csdnimg.cn/blog_migrate/01ffdd7e7da7754804164f689a586620.png)

#### 1.1.2.MySQL**事务的隔离级别** 

事务隔离级别是指操作同一资源的并发事务之间的隔离度。隔离级别越高，事务之间的相互干扰就越小，安全性就越高。

**读问题：**

-   **脏读：**读到了脏数据。当前事务读到另一个未提交事务刚改的数据。只有读未提交会脏读。
-   **不可重复读：**前后重复读的数据不一样。前后两次读同数据，这期间数据被其他事务改了，导致前后读取的数据不同。
-   **幻读：**前后读的数据是一样，但多了几行或少了几行，像幻觉一样。事务前后读的数据集合不同，导致出现“幻像”行。仅串行化能解决幻读问题。

**事务隔离级别**

-   **读未提交：**事务能读到所有未提交事务的数据。压根不加锁、没隔离，性能最高。
-   **读提交：**事务能读到已提交事务的数据。底层由MVVC实现 。解决脏读问题。
-   **可重复读（默认）：**前后读的数据相同。底层由MVVC实现 。解决脏读、不可重复读问题。
-   **串行化：**事务一拿到锁阻塞其他事务，直到释放锁。读时共享锁，写时排它锁。阻塞导致性能最差。解决脏读、不可重复读、幻读问题。

MVVC：多版本并发控制。

共享锁：在共享锁下，多个线程可以同时读取数据，但只有一个线程能够修改数据。当一个线程在修改数据时，必须获得独占锁，以便其他线程不能访问数据。

排它锁：在排它锁下，只有一个线程可以修改数据，其他线程不允许访问数据。

> SQL 标准定义了四种隔离级别，这四种隔离级别分别是：
> 
> \- 读未提交（READ UNCOMMITTED）
> 
> \- 读提交 （READ COMMITTED）；
> 
> \- 可重复读 （REPEATABLE READ）；
> 
> \- 串行化 （SERIALIZABLE）。
> 
> 4种隔离级别MySQL都支持，并且**InnoDB**存储引擎**默认**的支持隔离级别是**可重复读**REPEATABLE READ，但是与标准SQL不同的是，InnoDB存储引擎在REPEATABLE READ事务隔离级别下，使用Next-Key Lock的锁算法，因此避免了幻读的产生。所以，InnoDB存储引擎在默认的事务隔离级别下已经能完全保证事务的隔离性要求，即达到SQL标准的SERIALIZABLE隔离级别； 
> 
> 下面是四种隔离级别在解决脏读、不可重复读、幻读问题方面的情况：
> 
> | 隔离级别 | 脏读 | 不可重复读 | 幻读 |
> | --- | --- | --- | --- |
> | 读未提交 | 存在 | 存在 | 存在 |
> | 读已提交 | 不存在 | 存在 | 存在 |
> | 可重复读 | 不存在 | 不存在 | 存在 |
> | 串行化 | 不存在 | 不存在 | 不存在 |
> 
> 脏读（Dirty Read）：指一个事务读取了另一个未提交的事务所写入的数据，如果隔离级别越高，则越不容易出现脏读问题。
> 
> 不可重复读（Non-Repeatable Read）：指一个事务在读取同一数据时，由于另外一个事务的修改或删除，导致两次读取的数据不同。如果隔离级别越高，则越不容易出现不可重复读问题。
> 
> 幻读（Phantom Read）：指一个事务多次执行同一个查询，但每次返回的数据集合都不同，导致出现“幻像”行。如果隔离级别越高，则越不容易出现幻读问题。

#### 1.1.3.事务的传播行为

**PROPAGATION\_REQUIRED（默认）：** 如果当前没有事务， 就创建一个新事务， 如果当前存在事务，就加入该事务， 该设置是**最常用**的设置。

![](https://i-blog.csdnimg.cn/blog_migrate/081ba92182c07b458e3d4af628149751.png)  
PROPAGATION\_SUPPORTS： 支持当前事务， 如果当前存在事务， 就加入该事务， 如果当前不存在事务， 就以非事务执行。  
PROPAGATION\_MANDATORY： 支持当前事务， 如果当前存在事务， 就加入该事务， 如果当前不存在事务， 就抛出异常。  
**PROPAGATION\_REQUIRES\_NEW：** 创建新事务， 无论当前存不存在事务， 都创建新事务。  
PROPAGATION\_NOT\_SUPPORTED： 以非事务方式执行操作， 如果当前存在事务， 就把当前事务挂起。  
PROPAGATION\_NEVER： 以非事务方式执行， 如果当前存在事务， 则抛出异常。  
PROPAGATION\_NESTED： 如果当前存在事务， 则在嵌套事务内执行。 如果当前没有事务，则执行与 PROPAGATION\_REQUIRED 类似的操作。

#### 1.1.4.本地事务代理对象、**事务传播行为不生效问题**

**理论上，**下面代码，执行a方法，因为事务失败，b会回滚、c不会回滚；a,b共用一个事务，a的超时时间会覆盖b的超时时间。

**但是**，因为方法a、b、c都在同一个service里面，**事务传播行为不生效**，他们之间只是一个简单的方法调用，共享一个事务  
**原理：**事务是用代理对象来控制的，内部调用b(),c(),就相当于直接调用没有经过事务【**绕过了代理对象】**

```java
//1、如果方法a、b、c都在同一个service里面，事务传播行为不生效，共享一个事务
//	原理：事务是用代理对象来控制的，内部调用b(),c(),就相当于直接调用没有经过事务【绕过了代理对象】
//	解决：不能使用this.b()；也不能注入自己【要使用代理对象来调用事务方法】
		
		
@Transactional(timeout=30)
public void a() {
	b();// a事务传播给了b事务，并且b事务的设置失效
	c();// c单独创建一个新事务
}

@Transactional(propagation = Propagation.REQUIRED, timeout=2)
public void b() {

}

@Transactional(propagation = Propagation.REQUIRES_NEW)
public void c() {

}
```

**解决：要使用代理对象来调用事务方法。**不能使用this.b()；也不能注入自己

 1.引入aop的starter依赖，里面有aspectj依赖

```XML
        <!-- 引入aop，解决本地事务失效问题 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
        </dependency
```

2、开启动态代理【默认使用jdk动态代理，需要有接口】 

```java
@EnableAspectJAutoProxy(exposeProxy = true)  //开启了aspect动态代理模式,对外暴露代理对象
```

3、获取动态代理对象

```java
OrderServiceImpl orderService = (OrderServiceImpl)AopContext.currentProxy(); 
orderService.b(); 
orderService.c(); 
```

### 1.2.分布式事务

 _分布式事务_是指事务的参与者、支持事务的服务器、资源服务器以及事务管理器分别位于不同的分布式系统的**不同节点**之上。

**分布式事务的场景：**

**跨JVM进程：**微服务架构下，远程调用

![](https://i-blog.csdnimg.cn/blog_migrate/00d47e51d63ab8ff812628a019bc322c.png)

**跨数据库：**单服务操作多个数据库：

> 注意这里说的是多个数据库，而不是同一个数据库下的多个表

![](https://i-blog.csdnimg.cn/blog_migrate/828921d085d566d2cda8bc8a5e1f5e21.png)

**多服务单数据库:**

![](https://i-blog.csdnimg.cn/blog_migrate/ad32b8f1ca5174b47ce6f854803c09d7.png)

**分布式事务**，就是指不是在单个服务或单个数据库架构下，产生的事务，例如：

-   跨数据源的分布式事务
-   跨服务的分布式事务
-   综合情况

在数据库水平拆分、服务垂直拆分之后，一个业务操作通常要跨多个数据库、服务才能完成。例如电商行业中比较常见的下单付款案例，包括下面几个行为：

-   创建新订单
-   扣减商品库存
-   从用户账户余额扣除金额

完成上面的操作**需要访问三个不同的微服务和三个不同的数据库。**

![image-20210724165338958](https://i-blog.csdnimg.cn/blog_migrate/41d841dc36fb47a4e845303d881668e7.png)

订单的创建、库存的扣减、账户扣款在每一个服务和数据库内是一个本地事务，可以保证ACID原则。

但是当我们把三件事情看做一个"业务"，要满足保证“业务”的原子性，**要么所有操作全部成功，要么全部失败**，不允许出现部分成功部分失败的现象，这就是**分布式系统下的事务**了。

此时ACID难以满足，这是分布式事务要解决的问题

### 1.3.演示分布式事务问题

我们通过一个案例来演示分布式事务的问题：

1）**创建数据库，名为seata\_demo，然后导入课前资料提供的SQL文件：**

![image-20210724165634571](https://i-blog.csdnimg.cn/blog_migrate/72d2d1e1d642227b8b6f2cbf4c3cc939.png)

**订单表order\_tbl**

![](https://i-blog.csdnimg.cn/blog_migrate/e94faa3ec6bd293076f2a35796fbd7d8.png)

**账户表account\_tbl** 

![](https://i-blog.csdnimg.cn/blog_migrate/78d8b4f0ed2c16b40092a469e8e5e932.png)

**库存表storage\_tbl：**

![](https://i-blog.csdnimg.cn/blog_migrate/e37abc39f55178f5b4f1ae06e6e526b6.png)

2）**导入课前资料提供的微服务：**

![image-20210724165709994](https://i-blog.csdnimg.cn/blog_migrate/e3a6de28ac34fe020076b382337d554c.png)

微服务结构如下：

![image-20210724165729273](https://i-blog.csdnimg.cn/blog_migrate/64aa80c858bc84b9654f520d8d6df568.png)

> **记得改一下yml中数据库密码** 

其中：

**seata-demo：**父工程，负责管理项目依赖

-   **account-service：**账户服务，负责管理用户的资金账户。提供扣减余额的接口
-   **storage-service：**库存服务，负责管理商品库存。提供扣减库存的接口
-   **order-service：**订单服务，负责管理订单。创建订单时，需要调用account-service和storage-service

**3）启动nacos、所有微服务**

```
startup.cmd -m standalone
```

**4）测试下单功能，发出Post请求：**

请求如下：

> **坑点：**
> 
> -   feign报错解决:添加feign的httpclient连接池;    在orderservice添加spring.cloud.loadbalancer.retry.enabled=true
>     
> -   报错几次后，每次检查数据库，账户金额别小于200，库存数量别少于2.因为这里微服务还没有实现分布式事务问题，下单、扣钱、减库存，哪一环节出错其他环节的数据都不会回滚。

 **测试正确操作：**

```
http://localhost:8082/order?userId=user202103032042012&commodityCode=100202003032041&count=2&money=200
```

发现订单新增成功、钱减少了200，数量少了2。

![](https://i-blog.csdnimg.cn/blog_migrate/b0eaf31260b96f73b7ae2d2779312121.png)

**测试报错操作、分布式事务不会滚问题**（减库存后库存是负数，报错、回滚）： 

```
http://localhost:8082/order?userId=user202103032042012&commodityCode=100202003032041&count=20&money=200
```

如图：

![image-20210724170113404](https://i-blog.csdnimg.cn/blog_migrate/9ba5ebff23f77ac068e171d251f82248.png)

 测试发现，当库存不足时，如果余额已经扣减，**并不会回滚，出现了分布式事务问题。**

![](https://i-blog.csdnimg.cn/blog_migrate/cb09f4a5a330b4f09cdd09cf412f7300.png)

## 2.理论基础

解决分布式事务问题，需要一些分布式系统的基础知识作为理论指导。

### 2.1.CAP定理

1998年，加州大学的计算机科学家 Eric Brewer 提出，分布式系统有三个指标，**三个指标不可能同时做到**。

> -   **Consistency（一致性）**
> -   **Availability（可用性）**
> -   **Partition tolerance （分区容错性）**

![image-20210724170517944](https://i-blog.csdnimg.cn/blog_migrate/b356bd3f85f3be3f486d82ff11df42f9.png)

它们的第一个字母分别是 C、A、P。

Eric Brewer 说，这**三个指标不可能同时做到，最多只能同时满足两个。这个结论就叫做 CAP 定理。**

#### 2.1.1.一致性C：数据同步

**Consistency（一致性）：**用户访问分布式系统中的任意节点，得到的数据必须一致。

比如现在包含两个节点，其中的初始数据是一致的：

![image-20210724170704694](https://i-blog.csdnimg.cn/blog_migrate/c2661a67cd3169bfb2a27a47b2371e78.png)

当我们修改其中一个节点的数据时，两者的数据产生了差异：

![image-20210724170735847](https://i-blog.csdnimg.cn/blog_migrate/5fc15095b7f4c254799dd081b127a038.png)

要想保住一致性，就必须实现node01 到 node02的数据 同步：

![image-20210724170834855](https://i-blog.csdnimg.cn/blog_migrate/46dc76175e0adc605d5afe44e37b6a7c.png)

#### 2.1.2.可用性A：节点正常访问

**Availability （可用性）：**用户访问集群中的任意**健康节点**，**必须能得到响应**，**而不是超时或拒绝**。

如图，有三个节点的集群，访问任何一个都可以及时得到响应：

![image-20210724170932072](https://i-blog.csdnimg.cn/blog_migrate/546a3cb5f04790fb704376fc6d553650.png)

当有部分节点因为**网络故障或其它原因无法访问时，代表节点不可用：**

![image-20210724171007516](https://i-blog.csdnimg.cn/blog_migrate/121769c63779dc80ade7bff875ea51dd.png)

#### 2.1.3.分区容错P：分区后也要对外提供服务

**Partition（分区）**：因为**网络故障或其它原因**导致分布式系统中的**部分节点**与其它节点**失去连接**，**形成独立分区。**

![image-20210724171041210](https://i-blog.csdnimg.cn/blog_migrate/91b327f6dc3c512bcffc1bb783636fee.png)

**Tolerance（容错）**：在集群出现分区时，整个系统也要持续对外提供服务

#### 2.1.4.矛盾

在分布式系统中，系统间的**网络不能100%保证健康**，一定会有故障的时候，而服务有必须对外保证服务。因此**Partition Tolerance不可避免。**

当节点接收到新的数据变更时，就会出现问题了：

![image-20210724171546472](https://i-blog.csdnimg.cn/blog_migrate/28f656bacfc0976e6b45aab586388295.png)

如果此时要保证**一致性**，就必须等待网络恢复，完成数据同步后，整个集群才对外提供服务，服务处于阻塞状态，不可用。

如果此时要保证**可用性**，就不能等待网络恢复，那node01、node02与node03之间就会出现数据不一致。

也就是说，**在P一定会出现的情况下，A和C之间只能实现一个。**要么让node1、node2停掉，使三个节点保持同步，要么让node1、node2组成新分区，对外提供服务。

### 2.2.BASE理论

BASE理论是对CAP的**一种解决思路**，包含三个思想：

-   **Basically Available** **（基本可用）**：分布式系统在出现**故障**时，允许损失部分可用性，即**保证核心可用。**
-   **Soft State（软状态）：**在一定时间内，允许出现中间状态，比如**临时的不一致状态**。
-   **Eventually Consistent（最终一致性）**：虽然无法保证强一致性，但是在**软状态结束后**，**最终达到数据一致。**

### 2.3.解决分布式事务的思路，最终一致和强一致

分布式事务最大的问题是各个子事务的一致性问题，因此可以借鉴CAP定理和BASE理论，有两种解决思路：

-   **AP模式（最终一致）：**各子事务分别执行和提交，允许出现结果不一致，然后采用弥补措施恢复数据即可，实现**最终一致**。
    
-   **CP模式（强一致）：**各个子事务执行后互相等待，**同时提交，同时回滚**，达成**强一致**。但事务**等待过程**中，处于**弱可用状态**。
    

但不管是哪一种模式，都需要在子系统事务之间互相通讯，协调事务状态，也就是需要一个**事务协调者(TC)**：

![image-20210724172123567](https://i-blog.csdnimg.cn/blog_migrate/d4ffc5131eb556c42a8421f8f5fb40ce.png)

这里的子系统事务，称为**分支事务**；有关联的各个分支事务在一起称为**全局事务**。

## 3.初识Seata

Seata是 2019 年 1 月份蚂蚁金服和阿里巴巴共同开源的分布式事务解决方案。致力于提供高性能和简单易用的分布式事务服务，为用户打造一站式的分布式解决方案。

**官网地址：**http://seata.io/，其中的文档、播客中提供了大量的使用说明、源码分析。

![image-20210724172225817](https://i-blog.csdnimg.cn/blog_migrate/a5da8a990e758552551133fdfb2f2350.png)

### 3.1.Seata的架构，TC,**TM,RM**

Seata事务管理中有三个重要的角色：

-   **TC (Transaction Coordinator) -** **事务协调者：**维护全局和分支事务的状态，**协调全局事务提交或回滚**。
    
-   **TM (Transaction Manager) -** **事务管理器：定义**全局事务的**范围**、**开始**全局事务、**提交或回滚**全局事务。
    
-   **RM (Resource Manager) -** **资源管理器：**管理分支事务处理的资源，与TC交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。
    

**整体的架构如图：**

![image-20210724172326452](https://i-blog.csdnimg.cn/blog_migrate/6f8272213c763216bf5b03f854a8d0f5.png)

Seata基于上述架构提供了四种不同的**分布式事务解决方案：**

-   **XA模式：**强一致性分阶段事务模式，牺牲了一定的可用性，无业务侵入
-   **TCC模式：**最终一致的分阶段事务模式，有业务侵入
-   **AT模式（默认）：**最终一致的分阶段事务模式，无业务侵入，也是Seata的默认模式
-   **SAGA模式：**长事务模式，有业务侵入

无论哪种方案，都离不开TC，也就是事务的协调者。

### 3.2.部署Seata的TC（事务协调者）服务，tc-server

#### 1.下载

首先我们要下载seata-server包，地址在[http](http://seata.io/zh-cn/blog/download.html "http")[😕/seata.io/zh-cn/blog/download](http://seata.io/zh-cn/blog/download.html "😕/seata.io/zh-cn/blog/download")[.](http://seata.io/zh-cn/blog/download.html ".")[html](http://seata.io/zh-cn/blog/download.html "html")

当然，课前资料也准备好了：

![image-20210622202357640](https://i-blog.csdnimg.cn/blog_migrate/2f459d12e083f9077beca5d70f05865e.png)

#### 2.解压

在非中文目录解压缩这个zip包，其目录结构如下：

![image-20210622202515014](https://i-blog.csdnimg.cn/blog_migrate/e346d87938da2b9192b41c1ee2bdf463.png)

#### 3.registry.conf修改Seata的注册中心、配置中心

修改conf目录下的registry.conf文件：

![image-20210622202622874](https://i-blog.csdnimg.cn/blog_migrate/2643b3345dc440a7b7d9eec2e3634ef1.png)

内容如下：

```bash
registry {
  ## tc服务的注册中心类，这里选择nacos，也可以是eureka、zookeeper等
  type = "nacos"    #注册中心类型是nacos

                    
  nacos {
    ## seata tc 服务注册到 nacos的服务名称，可以自定义
    application = "seata-tc-server"
    serverAddr = "127.0.0.1:8848"
    group = "DEFAULT_GROUP"
    namespace = ""
    cluster = "SH"
    username = "nacos"
    pass改成自己的密码word = "nacos"
  }
}

config {
  ## 读取tc服务端的配置文件的方式，这里是从nacos配置中心读取，这样如果tc是集群，可以共享配置
  type = "nacos"    #也可以设置成file类型配置，会从本目录下找"file.conf"读取配置
  ## 配置nacos地址等信息
  nacos {
    serverAddr = "127.0.0.1:8848"
    namespace = ""
    group = "SEATA_GROUP"
    username = "nacos"
    pass改成自己的密码word = "nacos"
    dataId = "seataServer.properties"
  }
}
```

#### 4.在nacos添加配置

特别注意，为了让tc服务的集群可以共享配置，我们选择了nacos作为统一配置中心。因此服务端配置文件seataServer.properties文件需要在nacos中配好。

格式如下：

![image-20210622203609227](https://i-blog.csdnimg.cn/blog_migrate/2c5926b55ef043de5cb8b460c6668366.png)

配置内容如下（要修改数据库信息）：

```bash
#store事务日志存在哪里，这里设成数据库。也可以设成file类型
# 数据存储方式，db代表数据库
store.mode=db
store.db.datasource=druid
store.db.dbType=mysql
store.db.driverClassName=com.mysql.jdbc.Driver
store.db.url=jdbc:mysql://127.0.0.1:3306/seata?useUnicode=true&rewriteBatchedStatements=true
store.db.user=root
store.db.password=123
store.db.minConn=5
store.db.maxConn=30
store.db.globalTable=global_table    #全局事务的表
store.db.branchTable=branch_table    #分支事务的表
store.db.queryLimit=100
store.db.lockTable=lock_table        #锁的表
store.db.maxWait=5000
## 事务、日志等配置
server.recovery.committingRetryPeriod=1000
server.recovery.asynCommittingRetryPeriod=1000
server.recovery.rollbackingRetryPeriod=1000
server.recovery.timeoutRetryPeriod=1000
server.maxCommitRetryTimeout=-1
server.maxRollbackRetryTimeout=-1
server.rollbackRetryTimeoutUnlockEnable=false
server.undo.logSaveDays=7
server.undo.logDeletePeriod=86400000

## 客户端与服务端传输方式
transport.serialization=seata
transport.compressor=none
## 关闭metrics功能，提高性能
metrics.enabled=false
metrics.registryType=compact
metrics.exporterList=prometheus
metrics.exporterPrometheusPort=9898
```

其中的数据库地址、用户名、密码都需要修改成你自己的数据库信息。

> 也可以在文件中配置，需要registry.conf设置配置方式为file：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8927adbfe92ecd7208fd2d6abb41e795.png)
> 
>  file.conf
> 
> ```bash
> transport {
>   # tcp udt unix-domain-socket
>   type = "TCP"
>   #NIO NATIVE
>   server = "NIO"
>   #enable heartbeat
>   heartbeat = true
>   #thread factory for netty
>   thread-factory {
>     boss-thread-prefix = "NettyBoss"
>     worker-thread-prefix = "NettyServerNIOWorker"
>     server-executor-thread-prefix = "NettyServerBizHandler"
>     share-boss-worker = false
>     client-selector-thread-prefix = "NettyClientSelector"
>     client-selector-thread-size = 1
>     client-worker-thread-prefix = "NettyClientWorkerThread"
>     # netty boss thread size,will not be used for UDT
>     boss-thread-size = 1
>     #auto default pin or 8
>     worker-thread-size = 8
>   }
>   shutdown {
>     # when destroy server, wait seconds
>     wait = 3
>   }
>   serialization = "seata"
>   compressor = "none"
> }
> service {
>   #vgroup->rgroup
>   vgroup_mapping.gulimall-order-fescar-service-group = "default"
>   #only support single node
>   default.grouplist = "127.0.0.1:8091"
>   #degrade current not support
>   enableDegrade = false
>   #disable
>   disable = false
>   #unit ms,s,m,h,d represents milliseconds, seconds, minutes, hours, days, default permanent
>   max.commit.retry.timeout = "-1"
>   max.rollback.retry.timeout = "-1"
> }
> 
> client {
>   async.commit.buffer.limit = 10000
>   lock {
>     retry.internal = 10
>     retry.times = 30
>   }
>   report.retry.count = 5
> }
> 
> ## transaction log store
> store {
>   ## store mode: file、db
>   mode = "file"
> 
>   ## file store
>   file {
>     dir = "sessionStore"
> 
>     # branch session size , if exceeded first try compress lockkey, still exceeded throws exceptions
>     max-branch-session-size = 16384
>     # globe session size , if exceeded throws exceptions
>     max-global-session-size = 512
>     # file buffer size , if exceeded allocate new buffer
>     file-write-buffer-cache-size = 16384
>     # when recover batch read size
>     session.reload.read_size = 100
>     # async, sync
>     flush-disk-mode = async
>   }
> 
>   ## database store
>   db {
>     ## the implement of javax.sql.DataSource, such as DruidDataSource(druid)/BasicDataSource(dbcp) etc.
>     datasource = "dbcp"
>     ## mysql/oracle/h2/oceanbase etc.
>     db-type = "mysql"
>     url = "jdbc:mysql://127.0.0.1:3306/seata"
>     user = "mysql"
>     passw改成自己密码ord = "mysql"
>     min-conn = 1
>     max-conn = 3
>     global.table = "global_table"
>     branch.table = "branch_table"
>     lock-table = "lock_table"
>     query-limit = 100
>   }
> }
> lock {
>   ## the lock store mode: local、remote
>   mode = "remote"
> 
>   local {
>     ## store locks in user's database
>   }
> 
>   remote {
>     ## store locks in the seata's server
>   }
> }
> recovery {
>   committing-retry-delay = 30
>   asyn-committing-retry-delay = 30
>   rollbacking-retry-delay = 30
>   timeout-retry-delay = 30
> }
> 
> transaction {
>   undo.data.validation = true
>   undo.log.serialization = "jackson"
> }
> 
> ## metrics settings
> metrics {
>   enabled = false
>   registry-type = "compact"
>   # multi exporters use comma divided
>   exporter-list = "prometheus"
>   exporter-prometheus-port = 9898
> }
> ```

#### 5.创建数据库表，分支事务表和全局事务表

特别注意：tc服务在管理分布式事务时，需要记录事务相关数据到数据库中，你需要提前创建好这些表。

新建一个名为seata的数据库，运行课前资料提供的sql文件：

![image-20210622204145159](https://i-blog.csdnimg.cn/blog_migrate/af53f58accfed744b25cab39d3e9393e.png)

这些表主要记录全局事务、分支事务、全局锁信息：

```sql
SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- 分支事务表
-- ----------------------------
DROP TABLE IF EXISTS `branch_table`;
CREATE TABLE `branch_table`  (
  `branch_id` bigint(20) NOT NULL,
  `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `transaction_id` bigint(20) NULL DEFAULT NULL,
  `resource_group_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `resource_id` varchar(256) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `branch_type` varchar(8) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `status` tinyint(4) NULL DEFAULT NULL,
  `client_id` varchar(64) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `gmt_create` datetime(6) NULL DEFAULT NULL,
  `gmt_modified` datetime(6) NULL DEFAULT NULL,
  PRIMARY KEY (`branch_id`) USING BTREE,
  INDEX `idx_xid`(`xid`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Compact;

-- ----------------------------
-- 全局事务表
-- ----------------------------
DROP TABLE IF EXISTS `global_table`;
CREATE TABLE `global_table`  (
  `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `transaction_id` bigint(20) NULL DEFAULT NULL,
  `status` tinyint(4) NOT NULL,
  `application_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `transaction_service_group` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `transaction_name` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `timeout` int(11) NULL DEFAULT NULL,
  `begin_time` bigint(20) NULL DEFAULT NULL,
  `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `gmt_create` datetime NULL DEFAULT NULL,
  `gmt_modified` datetime NULL DEFAULT NULL,
  PRIMARY KEY (`xid`) USING BTREE,
  INDEX `idx_gmt_modified_status`(`gmt_modified`, `status`) USING BTREE,
  INDEX `idx_transaction_id`(`transaction_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Compact;

SET FOREIGN_KEY_CHECKS = 1;
```

#### 6.启动TC服务

进入bin目录，运行其中的seata-server.bat即可：

![image-20210622205427318](https://i-blog.csdnimg.cn/blog_migrate/dba83440766d863db71906c7bbedf819.png)

启动成功后，seata-server应该已经注册到nacos注册中心了。

打开浏览器，访问nacos地址：http://localhost:8848，然后进入服务列表页面，可以看到seata-tc-server的信息：

![image-20210622205901450](https://i-blog.csdnimg.cn/blog_migrate/9f1e26903ac969f9fe2ba7d86d8cf380.png)

### 3.3.微服务集成**Seata**

我们以order-service为例来演示。

#### 3.3.1.引入依赖

首先，在order-service中引入依赖：

```XML
<!--seata-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
    <exclusions>
        <!--版本较低，1.3.0，因此排除--> 
        <exclusion>
            <artifactId>seata-spring-boot-starter</artifactId>
            <groupId>io.seata</groupId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>io.seata</groupId>
    <artifactId>seata-spring-boot-starter</artifactId>
    <!--seata starter 采用1.4.2版本-->
    <version>${seata.version}</version>
</dependency>
```

#### 3.3.2.配置TC地址

在order-service中的application.yml中，配置TC服务信息，通过注册中心nacos，结合服务名称获取TC地址：

```bash
seata:
  registry: # TC服务注册中心的配置，微服务根据这些信息去注册中心获取tc服务地址
    type: nacos # 注册中心类型 nacos
    nacos:
      server-addr: 127.0.0.1:8848 # nacos地址
      namespace: "" # namespace，默认为空
      group: DEFAULT_GROUP # 分组，默认是DEFAULT_GROUP
      application: seata-tc-server # seata服务名称
      username: nacos
      password: nacos
  tx-service-group: seata-demo # 事务组名称
  service:
    vgroup-mapping: # 事务组与cluster的映射关系
      seata-demo: SH
```

微服务如何根据这些配置寻找TC的地址呢？

我们知道注册到Nacos中的微服务，确定一个具体实例需要四个信息：

-   namespace：命名空间
-   group：分组
-   application：服务名
-   cluster：集群名

以上四个信息，在刚才的yaml文件中都能找到：

![image-20210724173654258](https://i-blog.csdnimg.cn/blog_migrate/a3ede2816665ed64abfadef720950dfc.png)

namespace为空，就是默认的public

结合起来，TC服务的信息就是：public@DEFAULT\_GROUP@seata-tc-server@SH，这样就能确定TC服务集群了。然后就可以去Nacos拉取对应的实例信息了。

#### 3.3.3.其它服务

其它两个微服务也都参考order-service的步骤来做，完全一样。

## 4.详解Seata的四种分布式事务方案

下面我们就一起学习下Seata中的四种不同的事务模式。

### 4.1.XA模式，两阶段都加锁

XA 规范 是 X/Open 组织定义的分布式事务处理（DTP，Distributed Transaction Processing）标准，XA 规范 描述了全局的TM与局部的RM之间的接口，**几乎所有主流的数据库都对 XA 规范 提供了支持。**

#### 4.1.1.两阶段提交

XA是规范，目前主流数据库都实现了这种规范，实现的原理都是基于两阶段提交。

**正常情况：**

![image-20210724174102768](https://i-blog.csdnimg.cn/blog_migrate/dcf55c7cfee50f4bdd73ca311cefd1fe.png)

**异常情况：**

![image-20210724174234987](https://i-blog.csdnimg.cn/blog_migrate/286ba995c18875fe13fec0ad39f03b14.png)

**一阶段：**

-   **事务协调者通知每个事务参与者执行本地事务**
-   本地事务执行完成后**报告事务执行状态给事务协调者**，此时事务不提交，继续持有数据库锁

**二阶段：**

-   **事务协调者基于一阶段的报告来判断下一步操作**
    -   如果一阶段都成功，则通知所有事务参与者，提交事务
    -   如果一阶段**任意一个参与者失败**，则**通知所有事务参与者回滚事务**

#### 4.1.2.Seata的XA模型

Seata对原始的XA模式做了简单的封装和改造，以适应自己的事务模型，基本架构如图：

![image-20210724174424070](https://i-blog.csdnimg.cn/blog_migrate/408faf737323e2a9df63629bd3606097.png)

**资源管理者RM一阶段的工作：**

​ ① 注册分支事务到TC

​ ② 执行分支业务sql但不提交

​ ③ 报告执行状态到TC

**业务协调者TC二阶段的工作：**

-   TC检测各分支事务执行状态
    
    a.如果都成功，通知所有RM提交事务
    
    b.如果有失败，**通知所有RM回滚事务**
    

**RM二阶段的工作：**

-   接收TC指令，提交或回滚事务

#### 4.1.3.优缺点

**XA模式的优点是什么？**

-   事务的**强一致性**，满足ACID原则。
-   **常用数据库都支持**，实现简单，并且**没有代码侵入**

**XA模式的缺点是什么？**

-   因为**一阶段需要锁定数据库资源**，等待二阶段结束才释放，**性能较差**
-   **依赖关系型数据库**实现事务

#### 4.1.4.实现XA模式

Seata的starter已经完成了XA模式的自动装配，实现非常简单，步骤如下：

**1）修改application.yml文件（每个参与事务的微服务），开启XA模式：**

```bash
seata:
  data-source-proxy-mode: XA    #开启数据源代理的XA模式。代理数据源，拦截业务sql操作
```

**2）给发起全局事务的入口方法添加@GlobalTransactional注解:**

本例中是OrderServiceImpl中的create方法，把@Transactional改成**@GlobalTransactional**

![image-20210724174859556](https://i-blog.csdnimg.cn/blog_migrate/7299723437f60d160fbe0688c3405f29.png)

**3）重启服务并测试**

重启order-service，再次测试，发现无论怎样出错（例如操作完成后钱或库存是负数），**三个微服务都能成功回滚。**

### 4.2.AT模式：一阶段直接提交，二阶段统一回滚

AT模式同样是分阶段提交的事务模型，不过**弥补了XA模型中资源锁定周期过长的缺陷**。

#### 4.2.1.Seata的AT模型

基本流程图：

![image-20210724175327511](https://i-blog.csdnimg.cn/blog_migrate/73d120911ead92f2297ce74ad2b1f65c.png)

**阶段一RM的工作：**

-   注册分支事务
-   记录undo-log（数据快照）
-   执行业务sql并提交
-   报告事务状态

**阶段二提交时RM的工作：**

-   **删除undo-log即可**

**阶段二回滚时RM的工作：**

-   **根据undo-log恢复数据到更新前**

#### 4.2.2.流程梳理

我们用一个真实的业务来梳理下AT模式的原理。

比如，现在又一个数据库表，记录用户余额：

| **id** | **money** |
| --- | --- |
| 1 | 100 |

其中一个分支业务要执行的SQL为：

```
update tb_account set money = money - 10 where id = 1
```

AT模式下，当前分支事务执行流程如下：

**一阶段：**

1）TM发起并注册全局事务到TC

2）TM调用分支事务

3）分支事务准备执行业务SQL

4）RM拦截业务SQL，根据where条件查询原始数据，形成**快照。**

```bash
{
    "id": 1, "money": 100
}
```

5）RM执行业务SQL，提交本地事务，释放数据库锁。此时 `money = 90`

6）RM报告本地事务状态给TC

**二阶段：**

1）TM通知TC事务结束

2）TC检查分支事务状态

​ a）如果都成功，则立即删除快照

​ b）如果有分支事务失败，需要回滚。读取快照数据（`{"id": 1, "money": 100}`），将快照恢复到数据库。此时数据库再次恢复为100

**流程图：**

![image-20210724180722921](https://i-blog.csdnimg.cn/blog_migrate/29107874cfcbd979db25c068e6feb9da.png)

#### 4.2.3.AT与XA的区别

简述AT模式与XA模式最大的区别是什么？

-   XA模式一阶段不提交事务，锁定资源；**AT模式一阶段直接提交，不锁定资源。**
-   **XA模式依赖数据库机制实现回滚**；**AT模式利用数据快照实现数据回滚。**
-   **XA**模式**强一致**；**AT**模式**最终一致**

#### 4.2.4.脏写问题，全局锁

**快照恢复数据时数据库被更新。**

在多线程并发访问AT模式的分布式事务时，有**可能出现脏写问题，归根结底是业务之间的隔离问题**，导致a业务根据快照恢复数据时，另一个a业务已提交业务成功，导致恢复的数据是未更新时的样子，如图：

![image-20210724181541234](https://i-blog.csdnimg.cn/blog_migrate/0c9401335398abd0b298cc0ac52f7b50.png)

**解决思路就是引入了全局锁**的概念。在释放DB锁之前，先拿到全局锁。避免同一时刻有另外一个事务来操作当前数据。

![image-20210724181843029](https://i-blog.csdnimg.cn/blog_migrate/5e49a0862130bda4afb6950126703a83.png)

#### 4.2.5.优缺点

**AT模式的优点：**

-   **一阶段**完成**直接提交事务**，释放数据库资源，**性能比较好**
-   利用**全局锁**实现**读写隔离**
-   没有代码侵入，框架自动完成回滚和提交

**AT模式的缺点：**

-   两阶段之间属于**软状态**，属于**最终一致**
-   框架的快照功能会影响**性能**，但**比XA模式要好很多**

#### 4.2.6.实现AT模式（完整流程）

AT模式中的快照生成、回滚等动作都是由框架自动完成，没有任何代码侵入，因此实现非常简单。

只不过，AT模式需要一个表来记录全局锁、另一张表来记录数据快照undo\_log。

**0）环境准备**

安装启动事务协调器seata-server，registry.conf设置注册中心（nacos）和配置中心（file）、各服务导入依赖

```XML
<!--seata-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
</dependency>
```

**1）导入数据库表，记录全局锁**

每个需要用的seata的数据库导入undo\_log表，undo\_log表是回滚日志表：

```sql
-- 注意此处0.7.0+ 增加字段 context
CREATE TABLE `undo_log` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `branch_id` bigint(20) NOT NULL,
  `xid` varchar(100) NOT NULL,
  `context` varchar(128) NOT NULL,
  `rollback_info` longblob NOT NULL,
  `log_status` int(11) NOT NULL,
  `log_created` datetime NOT NULL,
  `log_modified` datetime NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `ux_undo_log` (`xid`,`branch_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```

**2）修改application.yml文件，将事务模式修改为AT模式即可：**

```bash
seata:
  data-source-proxy-mode: AT # 默认就是AT
```

**3）给发起全局事务的入口方法添加@GlobalTransactional注解:**

给分布式大事务注解@GlobalTransactional; 每一个远程的小事务用 @Transactional

```java
@GlobalTransactional
@Transactional  // 本地事务，在分布式系统，只能控制住自己的回滚，控制不了其他服务的回滚。
@Override
public SubmitOrderResponseVo submitOrder(OrderSubmitVo vo) {
  //.....
}
```

**4） 配置类注入seata代理数据源**

Seata通过代理数据源实现分支事务，如果没有注入，会导致无法回滚问题。

如果使用的是Hikari数据源配置类： 

```java
@Configuration
public class MySeataConfig {

    @Autowired
    DataSourceProperties dataSourceProperties;


    @Bean
    public DataSource dataSource(DataSourceProperties dataSourceProperties) {

        HikariDataSource dataSource = dataSourceProperties.initializeDataSourceBuilder().type(HikariDataSource.class).build();
        if (StringUtils.hasText(dataSourceProperties.getName())) {
            dataSource.setPoolName(dataSourceProperties.getName());
        }

        return new DataSourceProxy(dataSource);
    }

}
```

> Druid数据源
> 
> ```java
> @Configuration
> public class DataSourceProxyConfig {
> 
>     @Bean
>     @ConfigurationProperties(prefix = "spring.datasource")
>     public DruidDataSource druidDataSource() {
>         return new DruidDataSource();
>     }
> 
>     @Primary
>     @Bean
>     public DataSourceProxy dataSource(DruidDataSource druidDataSource) {
>         return new DataSourceProxy(druidDataSource);
>     }
> 
> }
> ```

**5）将**[file.conf](https://github.com/seata/seata-samples/blob/master/springcloud-jpa-seata/account-service/src/main/resources/file.conf "file.conf")**和**[registry.conf](https://github.com/seata/seata-samples/blob/master/springcloud-jpa-seata/account-service/src/main/resources/registry.conf "registry.conf")**两个配置文件移动到项目resources下：**

> 前面事务协调器seata-server的配置文件registry.conf设置了配置中心方式为file。

地址：

[https://github.com/seata/seata-samples/tree/master/springcloud-jpa-seata/account-service/src/main/resources](https://github.com/seata/seata-samples/tree/master/springcloud-jpa-seata/account-service/src/main/resources "https://github.com/seata/seata-samples/tree/master/springcloud-jpa-seata/account-service/src/main/resources")

file.conf

registry.conf 

> **注意：**file.conf 的 service.vgroup\_mapping 配置必须和`spring.application.name`一致
> 
> 在 `org.springframework.cloud:spring-cloud-starter-alibaba-seata` 的`org.springframework.cloud.alibaba.seata.GlobalTransactionAutoConfiguration` 类中，默认会使用 `${spring.application.name}-fescar-service-group`作为服务名注册到 Seata Server上，如果和`file.conf` 中的配置不一致，会提示 `no available server to connect`错误
> 
> 也可以通过配置 `spring.cloud.alibaba.seata.tx-service-group`修改后缀，但是必须和`file.conf`中的配置保持一致

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b146522e5e160be66d4399d4995662aa.png#pic_center)或者yml配置service.vgroup\_mapping 的服务名：

![](https://i-blog.csdnimg.cn/blog_migrate/d8d8468127ff0f012726065b84e872d8.png)

**7）启动并测试**

#### 4.2.7.@Transactional和@GlobalTransactional对比

**结论：**给分布式大事务注解@GlobalTransactional; 每一个远程的小事务用 @Transactional

        ①、只用@Transactional

                开启本地事务，对本地事务进行支持。如果用了@Transactional则保证a、b、c操作都在同一个本地事务中执行，并且更新时会加行锁，如果本地事务不统一提交，其他SQL不能再更新此条数据。如果不加@Transactional则默认没有事务a、b、c操作分别执行，不会加行锁，其他SQL都可以随便更新。

            ②、只用@GlobalTransactional

                开启全局事务，保证分布式事务。如果只用@GlobalTransactional，那就保证分布式事务，各个分支事务（本地事务）的统一，但是不能保证各个分支事务（本地事务）操作的统一。各个本地操作在无事务的状态下执行操作，不会加锁，别的操作可以随意修改。

            ③、@GlobalTransactional和@Transactional一起用

                @Transactional保证本地事务一致性，@GlobalTransactional保证全局事务的一致性。  
 

### 4.3.TCC模式：基于资源预留

XA和AT模式都要加锁，性能低。 而TCC模式**不需要加锁**，因为每次业务会预留资源，例如冻结应付金额方法。**不加锁性能高。**

**TCC模式**与AT模式非常相似，**每阶段都是独立事务**，不同的是TCC通过**人工编码来实现数据恢复。**

需要**实现三个方法：**

-   **Try：阶段1，资源的检测和预留（例如冻结应付金额）**；
    
-   **Confirm：提交，完成资源操作业务**；要求 Try 成功 Confirm 一定要能成功。
    
-   **Cancel**：**回滚，预留资源释放**，可以理解为try的反向操作。
    

#### 4.3.1.流程分析

**举例，**一个扣减用户余额的业务。假设账户A原来余额是100，需要余额扣减30元。

-   **阶段一（ Try ）**：**检查余额是否充足**，如果充足则**冻结金额从0变30，可用余额从100到70**

初识余额：

![image-20210724182424907](https://i-blog.csdnimg.cn/blog_migrate/16a5be97e13dfe3888c640f57ef5b714.png)

余额充足，可以冻结：

![image-20210724182457951](https://i-blog.csdnimg.cn/blog_migrate/74692d030124f0bf94a778077b8e3852.png)

此时，总金额 = 冻结金额 + 可用金额，数量依然是100不变。事务直接提交无需等待其它事务。

-   **阶段二（Confirm)**：假如要**提交**（Confirm），则**冻结金额扣减30**

确认可以提交，不过之前可用金额已经扣减过了，这里只要清除冻结金额就好了：

![image-20210724182706011](https://i-blog.csdnimg.cn/blog_migrate/d77c034efcadcd2d62b97f257697f13f.png)

此时，总金额 = 冻结金额 + 可用金额 = 0 + 70 = 70元

-   **阶段二(Canncel)**：如果要**回滚**（Cancel），则**冻结金额扣减30，可用余额增加30**

需要回滚，那么就要释放冻结金额，恢复可用金额：

![image-20210724182810734](https://i-blog.csdnimg.cn/blog_migrate/3c3e07b426f46e2586ee814446e7db1f.png)

#### 4.3.2.Seata的TCC模型

Seata中的TCC模型依然延续之前的事务架构，如图：

![image-20210724182937713](https://i-blog.csdnimg.cn/blog_migrate/e02ef53a98eab341abd2b058dcb2e36d.png)

#### 4.3.3.优缺点

**TCC模式的每个阶段是做什么的？**

-   Try：资源检查和预留
-   Confirm：业务执行和提交
-   Cancel：预留资源的释放

**TCC的优点是什么？**

-   **一阶段完成直接提交事务，释放数据库资源**，性能好
-   相比AT模型，无需生成快照，**无需使用全局锁，性能最强**
-   不依赖数据库事务，而是依赖补偿操作，**可以用于非事务型数据库**

**TCC的缺点是什么？**

-   有**代码侵入**，需要**人为编写**try、Confirm和Cancel接口，太麻烦
-   软状态，事务是最终一致
-   **做好幂等处理：**需要考虑Confirm和Cancel的失败情况，做好幂等处理（例如cancel超时，系统以为cancel失败就又调用了一次cancel，而其实第一次cancel是成功的。多次cancel结果是一样的，就是幂等了。）

> **代码侵入：**
> 
> **当你的代码引入了一个组件,导致其它代码或者设计,要做相应的更改以适应新组件**.这样的情况我们就认为这个新组件具有**侵入性**
> 
> 同时,这里又涉及到一个设计方面的概念,就是**耦合性**的问题.
> 
> 我们代码设计的思路是"**高内聚,低耦合**",为了实现这个思路,就必须降低代码的侵入性.

#### 4.3.4.事务悬挂和空回滚

**1）空回滚**

某分支事务因为阻塞导致try阶段没有执行，超时后TC通知全局事务回滚，而该分支因为try压根就没有执行，所以无需回滚。

当执行cancel操作时，应当判断try是否已经执行，如果尚未执行，则应该空回滚。

如图：

![image-20210724183426891](https://i-blog.csdnimg.cn/blog_migrate/7f1fa6a10f58d2ccc67745b7ed317c2b.png)

**2）业务悬挂**

对于已经空回滚的业务，之前被阻塞的try操作恢复，继续执行try冻结资源，然而二阶段早已执行完毕，此分支就永远停留在预留资源而不能提交或回滚的状态。

**解决办法：数据库记录事务状态。**Redis或数据库记录事务状态，每次try前先从Redis或数据库判断是否已经cancel过，每次cancel后修改事务状态为“已cancel”。

**事务表：** 

```sql
CREATE TABLE `account_freeze_tbl` (
  `xid` varchar(128) NOT NULL,
  `user_id` varchar(255) DEFAULT NULL COMMENT '用户id',
  `freeze_money` int(11) unsigned DEFAULT '0' COMMENT '冻结金额',
  `state` int(1) DEFAULT NULL COMMENT '事务状态，0:try，1:confirm，2:cancel',
  PRIMARY KEY (`xid`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 ROW_FORMAT=COMPACT;

```

这个表一方面冻结金额、一方面记录状态。

> **判断空回滚：**cancel时根据事务表的id查到状态state为null，就空回滚；
> 
> **防止业务悬挂：**try时查到状态state为2即回滚，就阻止业务悬挂。

#### 4.3.5.下单代码实现TCC模式，@TwoPhaseBusinessAction，@BusinessActionContextParameter，

解决空回滚和业务悬挂问题，必须要记录当前事务状态，是在try、还是cancel？

**1）思路分析**

这里我们定义一张表：

```sql
CREATE TABLE `account_freeze_tbl` (
  `xid` varchar(128) NOT NULL,
  `user_id` varchar(255) DEFAULT NULL COMMENT '用户id',
  `freeze_money` int(11) unsigned DEFAULT '0' COMMENT '冻结金额',
  `state` int(1) DEFAULT NULL COMMENT '事务状态，0:try，1:confirm，2:cancel',
  PRIMARY KEY (`xid`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 ROW_FORMAT=COMPACT;

```

> **其中：**
> 
> -   **xid：**是全局事务id
> -   **freeze\_money：**用来记录用户冻结金额
> -   **state：**用来记录事务状态

**业务实现方法：**

-   Try业务：
    -   记录冻结金额和事务状态到account\_freeze表
    -   扣减account表可用金额
-   Confirm业务
    -   根据xid删除account\_freeze表的冻结记录
-   Cancel业务
    -   修改account\_freeze表，冻结金额为0，state为2
    -   修改account表，恢复可用金额
-   **如何判断是否空回滚？**
    -   cancel业务中，根据xid查询account\_freeze，如果为null则说明try还没做，需要空回滚
-   **如何避免业务悬挂？**
    -   try业务中，根据xid查询account\_freeze ，如果已经存在则证明Cancel已经执行，拒绝执行try业务

接下来，我们改造account-service，利用TCC实现余额扣减功能。

**2）声明TCC接口**

TCC的Try、Confirm、Cancel方法都需要在接口中**基于注解来声明**，

我们在account-service项目中的`cn.itcast.account.service`包中新建一个接口，声明TCC三个接口：

```java
package cn.itcast.account.service;

import io.seata.rm.tcc.api.BusinessActionContext;
import io.seata.rm.tcc.api.BusinessActionContextParameter;
import io.seata.rm.tcc.api.LocalTCC;
import io.seata.rm.tcc.api.TwoPhaseBusinessAction;

//声明为ttc
@LocalTCC
public interface AccountTCCService {

    //在try方法上@TwoPhaseBusinessAction声明try、confirm、cancel的方法名
    @TwoPhaseBusinessAction(name = "deduct", commitMethod = "confirm", rollbackMethod = "cancel")
    //参数注解@BusinessActionContextParameter将参数放在上下文对象，在本接口所有方法都能拿到这个参数
    void deduct(@BusinessActionContextParameter(paramName = "userId") String userId,
                @BusinessActionContextParameter(paramName = "money")int money);

    //confirm方法名要跟@TwoPhaseBusinessAction声明的一致，BusinessActionContext上下文对象获取try方法注解@BusinessActionContextParameter的参数
    boolean confirm(BusinessActionContext ctx);

    boolean cancel(BusinessActionContext ctx);
}
```

**3）编写实现类**

在account-service服务中的`cn.itcast.account.service.impl`包下新建一个类，实现TCC业务：

```java
package cn.itcast.account.service.impl;

import cn.itcast.account.entity.AccountFreeze;
import cn.itcast.account.mapper.AccountFreezeMapper;
import cn.itcast.account.mapper.AccountMapper;
import cn.itcast.account.service.AccountTCCService;
import io.seata.core.context.RootContext;
import io.seata.rm.tcc.api.BusinessActionContext;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
@Slf4j
public class AccountTCCServiceImpl implements AccountTCCService {

    @Autowired
    private AccountMapper accountMapper;
    @Autowired
    private AccountFreezeMapper freezeMapper;

    @Override
    //业务注解
    @Transactional
    public void deduct(String userId, int money) {
        // 0.获取事务id，RootContext是seata提供的工具类，用来获取id。
        String xid = RootContext.getXID();
        
        //判断事务悬挂，如果有冻结记录则是悬挂，直接return。对于已经空回滚的业务，之前被阻塞的try操作恢复，继续执行try，就永远不可能confirm或cancel ，事务一直处于中间状态，这就是业务悬挂。
        if(accountMapper.selectById(xid)==null) return;
        // 1.扣减可用余额，这里不用余额判断，因为数据库余额字段类型是非负，扣成负数就业务失败
        accountMapper.deduct(userId, money);
        // 2.记录冻结金额，事务状态
        AccountFreeze freeze = new AccountFreeze();
        freeze.setUserId(userId);
        freeze.setFreezeMoney(money);
        //自定义常量AccountFreeze.State.TRY值就是0
        freeze.setState(AccountFreeze.State.TRY);
        freeze.setXid(xid);
        freezeMapper.insert(freeze);
    }

    @Override
    public boolean confirm(BusinessActionContext ctx) {
        // 1.获取事务id，也可以用RootContext获取xid
        String xid = ctx.getXid();
        // 2.根据id删除冻结记录，confirm方法不用幂等处理，因为它是直接删除，删多少次都是删
        int count = freezeMapper.deleteById(xid);
        return count == 1;
    }

    @Override
    public boolean cancel(BusinessActionContext ctx) {
        // 0.查询冻结记录
        String xid = ctx.getXid();
        AccountFreeze freeze = freezeMapper.selectById(xid);
        
        //判断空回滚。当某分支事务的try阶段阻塞时，可能导致全局事务超时而触发二阶段的cancel操作。在未执行try操作时先执行了cancel操作，这时cancel不能做回滚，就是空回滚。
        if(freeze==null){freeze =new freeze;设置userId,state,xid;freezeMapper.insert(freeze);return true}

        //幂等判断，如果已经处理过一次cancel时不需要再cancel了（可能源于超时被认为失败其实没失败，再cancel了一次）。confirm方法不用幂等处理，因为它是直接删除，删多少次都是删
        if(freeze.getState()==AccountFreeze.State.CANCEL){return true;}
        // 1.恢复可用余额
        accountMapper.refund(freeze.getUserId(), freeze.getFreezeMoney());
        // 2.将冻结金额清零，状态改为CANCEL
        freeze.setFreezeMoney(0);
        freeze.setState(AccountFreeze.State.CANCEL);
        int count = freezeMapper.updateById(freeze);
        return count == 1;
    }
}
```

**测试：**

先修改金额为不够和库存数量为充足、再次发请求：

```java
http://localhost:8082/order?userId=user202103032042012&commodityCode=100202003032041&count=1&money=2000000
```

发现报错、回滚。 

### 4.4.SAGA模式：基于一系列本地事务

Saga 模式是 Seata 即将开源的**长事务解决方案**，将由蚂蚁金服主要贡献。

其理论基础是Hector & Kenneth 在1987年发表的论文[Sagas](https://microservices.io/patterns/data/saga.html "Sagas")。

Seata官网对于Saga的指南：https://seata.io/zh-cn/docs/user/saga.html

#### 4.4.1.原理

Saga 模式使用**一系列本地事务**来提供事务管理。 本地事务是由 Saga 参与者执行的原子工作。 每个本地事务都会更新数据库，并发布消息或事件来**触发** Saga 中的下一个本地事务。 如果本地事务失败，则 Saga 将执行一系列补偿事务，以撤消上一个本地事务所做的更改。 

在 Saga 模式下，分布式事务内有多个参与者，每一个参与者都是一个冲正补偿服务，需要用户根据业务场景实现其正向操作和逆向回滚操作。

分布式事务执行过程中，依次执行各参与者的正向操作，如果所有正向操作均执行成功，那么分布式事务提交。如果任何一个正向操作执行失败，那么分布式事务会去退回去执行前面各参与者的逆向回滚操作，回滚已提交的参与者，使分布式事务回到初始状态。

没有全局锁，也没有冻结资源，所以**存在脏写问题。**

> **脏写：快照恢复数据时数据库被更新。**
> 
> 在多线程并发访问AT模式的分布式事务时，有**可能出现脏写问题，归根结底是业务之间的隔离问题**，导致a业务根据快照恢复数据时，另一个a业务已提交业务成功，导致恢复的数据是未更新时的样子

![image-20210724184846396](https://i-blog.csdnimg.cn/blog_migrate/77b75fd55d62dd58ec311a24df510a99.png)

Saga也分为两个阶段：

-   **一阶段：直接提交本地事务**
-   **二阶段：成功则什么都不做；失败则通过编写补偿业务来回滚**

#### 4.4.2.优缺点

**优点：**

-   事务参与者可以**基于事件驱动**实现**异步调用，吞吐高，适合长事务**
-   一阶段直接提交事务，无锁，性能好
-   不用编写TCC中的三个阶段，实现简单

**缺点：**

-   软状态持续时间不确定，时效性差
-   没有锁，没有事务隔离，**会有脏写**

### 4.5.四种模式对比，XA,AT,TCC,SAGA

我们从以下几个方面来对比四种实现：

-   一致性：能否保证事务的一致性？强一致还是最终一致？
-   隔离性：事务之间的隔离性如何？
-   代码侵入：是否需要对业务代码改造？
-   性能：有无性能损耗？
-   场景：常见的业务场景

如图：

![image-20210724185021819](https://i-blog.csdnimg.cn/blog_migrate/da840b6092a99ed2ab834ecf6def1755.png)

> **XA：**一阶段**锁定**数据库资源，业务协调者TC通知各业务执行并获取执行状态，二阶段如果存在业务失败，则通知所有业务回滚。
> 
> **AT：**一阶段资源管理者RM**记录undo-log（数据快照）**，二阶段如果存在业务失败，根据快照回滚。全局锁是在释放DB锁之前，先拿到全局锁。避免同一时刻有另外一个事务来操作当前数据。
> 
> **TCC：**一阶段try方法**资源**的检测和**预留，**二阶段如果存在业务失败，根据**Cancel方法**编写的内容**释放预留资源**
> 
> **SAGA：**一阶段直接提交本地事务，二阶段失败则通过**编写补偿业务**来回滚

## 5.其他分布式事务方案（不使用Seata）

### 5.1.柔性事务方法实现最终一致性

#### 5.1.1.柔性事务-最大努力通知型方案

按规律进行通知，不保证数据一定能通知成功，但会提供可查询操作接口进行**核对**。

这种方案主要用在与第三方系统通讯时，比如：调用微信或支付宝支付后的支付结果通知。这种方案也是结合 MQ 进行实现，例如： 通过 MQ 发送 http 请求，设置最大通知次数。达到通知次数后即不再通知。  
案例：银行通知、商户通知等(各大交易业务平台间的商户通知：多次通知、查询校对、对账文件)，支付宝的支付成功异步回调。

#### 5.1.2.柔性事务-可靠消息+最终一致性方案（异步确保型）

业务处理服务在业务事务提交之前，向实时消息服务**请求发送消息**，实时消息服务只记录消息数据，而不是真正的发送。

业务处理服务在**业务事务提交之后**，向实时消息服务确认发送。只有在得到确认发送指令后，实时消息服务才会**真正发送**。

**案例：**

在商品下单业务的最后要锁定库存，我们设置在锁定库存后发RabbitMQ延迟队列消息，通知锁定库存成功，两分钟后消费消息，根据库存信息查询检查订单是否存在，若不存在代表下订单失败，此时要回滚，也就是解锁库存。

### 5.2.**xxl-job和消息组件实现最终一致性**

在主要业务的数据库里创建消息表和消息记录表； 

在执行主要业务成功后插入一条消息表数据，xxl-job定时扫描任务列表并发处理任务。因为主要业务的表和消息表在一个数据库里，所以是本地事务，不是分布式事务。

![](https://i-blog.csdnimg.cn/blog_migrate/9d26e33986fbc80e7d6e43df577d7048.png)

**举例：** 

例如课程发布业务， 在课程信息入库后，插入一条消息表数据，课程id为业务信息1，阶段1是存redis、阶段2是ES添加索引，阶段3是静态化页面到文件系统：

**强一致：**

如果要满足CP就表示课程发布操作后向数据库、redis、elasticsearch、MinIO写四份数据，只要有一份写失败其它的全部回滚。

**最终一致：**

课程发布操作后，先更新数据库中的课程发布状态，更新后向redis、elasticsearch、MinIO写课程信息，只要在一定时间内最终向redis、elasticsearch、MinIO写数据成功即可。  
 

## 6.高可用

Seata的TC服务作为分布式事务核心，一定要保证集群的高可用性。

### 6.1.高可用架构模型

搭建TC服务集群非常简单，启动多个TC服务，注册到nacos即可。

但集群并不能确保100%安全，万一集群所在机房故障怎么办？所以如果要求较高，一般都会做异地多机房容灾。

比如一个TC集群在上海，另一个TC集群在杭州：

![image-20210724185240957](https://i-blog.csdnimg.cn/blog_migrate/379bfa966d91a99535d0c69b81addd24.png)

微服务基于事务组（tx-service-group)与TC集群的映射关系，来查找当前应该使用哪个TC集群。当SH集群故障时，只需要将vgroup-mapping中的映射关系改成HZ。则所有微服务就会切换到HZ的TC集群了。

### 6.2.实现高可用，异地容灾

#### 6.2.1.模拟异地容灾的TC集群

计划启动两台seata的tc服务节点：

| 节点名称 | ip地址 | 端口号 | 集群名称 |
| --- | --- | --- | --- |
| seata | 127.0.0.1 | 8091 | SH |
| seata2 | 127.0.0.1 | 8092 | HZ |

之前我们已经启动了一台seata服务，端口是8091，集群名为SH。

现在，将seata目录复制一份，起名为seata2

修改seata2/conf/registry.conf内容如下：

```bash
registry {
  ## tc服务的注册中心类，这里选择nacos，也可以是eureka、zookeeper等
  type = "nacos"

  nacos {
    ## seata tc 服务注册到 nacos的服务名称，可以自定义
    application = "seata-tc-server"
    serverAddr = "127.0.0.1:8848"
    group = "DEFAULT_GROUP"
    namespace = ""
    cluster = "HZ"
    username = "nacos"
    pass改成自己的密码word = "nacos"
  }
}

config {
  ## 读取tc服务端的配置文件的方式，这里是从nacos配置中心读取，这样如果tc是集群，可以共享配置
  type = "nacos"
  ## 配置nacos地址等信息
  nacos {
    serverAddr = "127.0.0.1:8848"
    namespace = ""
    group = "SEATA_GROUP"
    username = "nacos"
    pass改成自己的密码word = "nacos"
    dataId = "seataServer.properties"
  }
}
```

进入seata2/bin目录，然后运行命令：

```
seata-server.bat -p 8092
```

打开nacos控制台，查看服务列表：

![image-20210624151150840](https://i-blog.csdnimg.cn/blog_migrate/417d194d4c175ba4a1855be268c0cc52.png)

点进详情查看：

![image-20210624151221747](https://i-blog.csdnimg.cn/blog_migrate/6e844b4c9e843fabe1b56b92347b15da.png)

#### 6.2.2.将事务组映射配置到nacos

接下来，我们需要将tx-service-group与cluster的映射关系都配置到nacos配置中心。

新建一个配置：

![image-20210624151507072](https://i-blog.csdnimg.cn/blog_migrate/ab53a0ba1cd25f66bc656b5ec7415b12.png)

配置的内容如下：

```bash
## 事务组映射关系
service.vgroupMapping.seata-demo=SH

service.enableDegrade=false
service.disableGlobalTransaction=false
## 与TC服务的通信配置
transport.type=TCP
transport.server=NIO
transport.heartbeat=true
transport.enableClientBatchSendRequest=false
transport.threadFactory.bossThreadPrefix=NettyBoss
transport.threadFactory.workerThreadPrefix=NettyServerNIOWorker
transport.threadFactory.serverExecutorThreadPrefix=NettyServerBizHandler
transport.threadFactory.shareBossWorker=false
transport.threadFactory.clientSelectorThreadPrefix=NettyClientSelector
transport.threadFactory.clientSelectorThreadSize=1
transport.threadFactory.clientWorkerThreadPrefix=NettyClientWorkerThread
transport.threadFactory.bossThreadSize=1
transport.threadFactory.workerThreadSize=default
transport.shutdown.wait=3
## RM配置
client.rm.asyncCommitBufferLimit=10000
client.rm.lock.retryInterval=10
client.rm.lock.retryTimes=30
client.rm.lock.retryPolicyBranchRollbackOnConflict=true
client.rm.reportRetryCount=5
client.rm.tableMetaCheckEnable=false
client.rm.tableMetaCheckerInterval=60000
client.rm.sqlParserType=druid
client.rm.reportSuccessEnable=false
client.rm.sagaBranchRegisterEnable=false
## TM配置
client.tm.commitRetryCount=5
client.tm.rollbackRetryCount=5
client.tm.defaultGlobalTransactionTimeout=60000
client.tm.degradeCheck=false
client.tm.degradeCheckAllowTimes=10
client.tm.degradeCheckPeriod=2000

## undo日志配置
client.undo.dataValidation=true
client.undo.logSerialization=jackson
client.undo.onlyCareUpdateColumns=true
client.undo.logTable=undo_log
client.undo.compress.enable=true
client.undo.compress.type=zip
client.undo.compress.threshold=64k
client.log.exceptionRate=100
```

#### 3.微服务读取nacos配置

接下来，需要修改每一个微服务的application.yml文件，让微服务读取nacos中的client.properties文件：

```bash
seata:
  config:
    type: nacos
    nacos:
      server-addr: 127.0.0.1:8848
      username: nacos
      password: nacos
      group: SEATA_GROUP
      data-id: client.properties
```

重启微服务，现在微服务到底是连接tc的SH集群，还是tc的HZ集群，都统一由nacos的client.properties来决定了。