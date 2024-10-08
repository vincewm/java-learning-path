> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/黑马旅游/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/黑马旅游/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码-CSDN博客")

**目录**

[一、说说倒排索引](#%E8%AF%B4%E8%AF%B4%E5%80%92%E6%8E%92%E7%B4%A2%E5%BC%95)

[二、ElasticSearch为什么是近实时不是实时？如何保证实时？](#ElasticSearch%E4%B8%BA%E4%BB%80%E4%B9%88%E6%98%AF%E8%BF%91%E5%AE%9E%E6%97%B6%E4%B8%8D%E6%98%AF%E5%AE%9E%E6%97%B6%EF%BC%9F%E5%A6%82%E4%BD%95%E4%BF%9D%E8%AF%81%E5%AE%9E%E6%97%B6%EF%BC%9F)

[三、怎么保证MySQL和ES一致性](#%E6%80%8E%E4%B9%88%E4%BF%9D%E8%AF%81MySQL%E5%92%8CES%E4%B8%80%E8%87%B4%E6%80%A7)

[四、说说ES集群的节点和分片](#1.6.4%20%E8%AF%B4%E8%AF%B4ES%E9%9B%86%E7%BE%A4%E7%9A%84%E8%8A%82%E7%82%B9%E5%92%8C%E5%88%86%E7%89%87)

[五、ES集群是怎么搭建的](#%E9%9B%86%E7%BE%A4%E6%98%AF%E6%80%8E%E4%B9%88%E6%90%AD%E5%BB%BA%E7%9A%84)

[六、说说集群脑裂问题](#%E8%AF%B4%E8%AF%B4%E9%9B%86%E7%BE%A4%E8%84%91%E8%A3%82%E9%97%AE%E9%A2%98)

[七、ES怎么进行调优？](#1.6.7%20ES%E6%80%8E%E4%B9%88%E8%BF%9B%E8%A1%8C%E8%B0%83%E4%BC%98%EF%BC%9F)

--

## 一、说说倒排索引

**倒排索引流程：**

1.  **分词：**将每一个文档的数据利用算法**分词**，得到一个个词条；
2.  **映射关系表：**创建分词和文档id的映射关系表；
3.  **词条-->id-->文档：**搜索词条时，根据映射关系表找到它对应的所有文档id，然后根据文档id正向索引查到文档。

## 二、ElasticSearch为什么是近实时不是实时？如何保证实时？

当数据添加到索引后并不能马上被查询到，等到**索引刷新**后才会被查询到。 refresh\_interval 配置的刷新间隔。默认是1s。

**解决办法：**

-   **修改刷新间隔：**修改索引库的\_settings下的refresh\_interval为40ms或更小。
-   **设置刷新策略为立即刷新**：刷新策略可以是false（异步刷新）、true（立即刷新；对集群压力大）、wait\_for（默认，到刷新间隔再刷新）。java high level client的request可以也设置策略，对应NONE、IMMEDIATE、WAIT\_UNTIL。

```
indexRequest.setRefreshPolicy(WriteRequest.RefreshPolicy.IMMEDIATE);
```

**批量导入ES文档时提高效率：**

elasticsearch设置refresh\_interval为 -1 时，意味着不刷新索引，也就是只写在内存中，不刷新。当我们大批量的往Elasticsearch索引录入数据时，通常会把refresh\_interval 设置为 -1，这样会加快数据导入的速度，在数据导入完成后，再将该参数设置为正数。比如：1s。

简单介绍下es的写入原理：

大概分为三个步骤：write -> refresh -> flush

1、write：文档数据到内存缓存，并存到 translog

2、refresh：内存缓存中的文档数据，到文件缓存中的 segment 。此时可以被搜到。

3、flush 是缓存中的 segment 文档数据写入到磁盘

## 三、怎么保证MySQL和ES一致性

-   **思路一：**MySQL落库后发MQ进行ES落库，应该保证消息可靠消费。
-   **思路二：**Canal异步监听binlog，监听到更新操作后，同步ES。

**强一致性：**

说实话，我们一般不保证MySQL和ES的强一致性，因为ES是近实时的，默认有1秒的刷新间隔，但如果刷新间隔设置成小于1秒，可能会对性能产生影响，而且ES设计之初就是为了应对多读少写的情景，如果要保证强一致性，就应该用关系型数据库。ES更多是做倒排索引、 海量数据查询，如果真的要想保持强一致的话，只能采用下面方案，不过一般没有公司这样做。我们一般对数据库和搜索引擎一致性要求不会那么强：

1.  **事务：**事务内，落库后，立刻保存ES
2.  **读写串行：**数据库传播级别

## 四、说说ES集群的节点和分片

一个集群里有多个节点，每个节点都是一个es实例， 每个节点保存了自己的分片和一个其他节点备份的分片。

-   **集群（cluster）**：一组拥有共同的 集群名 的 节点。
    
-   **节点（node) ：**集群中的一个 Elasticearch 实例
    
-   **分片（shard）：**索引可以被拆分为不同的部分进行存储，称为分片。在每次读写数据时，会根据文档ID%分片数量，得出具体访问分片的序号。在集群环境下，一个索引的不同分片可以拆分到不同的节点中。
    
    **解决问题：**数据量太大，单点存储量有限、高可用的问题。
    
    -   **主分片（Primary shard）：**相对于副本分片的定义。主分片和副本分片会自动分配在各节点，
    -   **副本分片（Replica shard）：**每个主分片可以有一个或者多个副本，数据和主分片一样。主分片副本数 <=  节点数 - 1 。例如3个节点，则主分片有3个，每个主分片最多有2个副本，副本数可以动态扩展。

**集群职责划分：**实际场景，每个节点要细化角色，当然只搭建备选主节点也是可以的，默认情况下，集群中的任何一个节点都同时具备上述四种角色。

-   **候选主节点（master eligible）：**管理集群状态，处理索引库增删请求。
-   **数据节点（data）：**对记录的增删改查。
-   **接待节点（ingest）：**数据存储前的预处理。
-   **协作节点（coordinating）：**将请求路由其他节点，合并处理结果并返回。这样用户访问任何一个节点都能请求路由到数据实际存储分片所在节点。

## 五、ES集群是怎么搭建的

Docker Compose用来将一个或多个容器组合成一个完整的应用程序。这里搭建三个节点，因为es集群至少需要三个节点，这是跟它的内部机制有关，为了防止脑裂现象。

1.  docker-compose.yml的services里配置三个es节点，设置镜像名、容器名、集群名（三个节点集群名必须一致，es自动会把集群名相同的节点组装成集群）、可以参与选举的主节点（三个都加上，都能选举主节点）、地址、内存。
2.  执行 docker-compose up 命令（后面加-d是在后台运行）来启动并运行整个应用程序。
3.  搭建cerebro监控平台，输入任意节点地址进行连接，就可以监控管理整个集群，查看各节点cpu、内存、磁盘、负载、分片信息。当然也可以使用kibana，但kibana监控集群有些困难。

## 六、说说集群脑裂问题

**选举master条件：**当一个节点发现包括自己在内的多数派的master-eligible节点认为集群没有master时，就可以发起master选举。

**选举master过程：**

1.  备选主节点首先根据节点id（第一次启动时生成的随机字符串）排序，第一个节点暂定master；
2.  如果有n/2+1个节点（quorum值）投票它是mater，并且它自己也给自己投票，则它当选master；
3.  否则就暂定第二个节点为master，以此类推。
4.  旧主的分片移动到健康节点。

**脑裂：**master故障，集群选举出新master后旧master又恢复了，导致集群出现了两个master。

**脑裂原因：**

-   **网络延迟导致误判：**集群间的网络延迟导致一些节点访问不到master, 认为master 挂掉了从而选举出新的master,并对master上的分片和副本标红，分配新的主分片
-   **主节点负载过高导致误判：**主节点的角色既为master又为data,访问量较大时可能会导致ES停止响应造成大面积延迟，此时其他节点得不到主节点的响应认为主节点挂掉了，会重新选取主节点
-   **内存回收导致误判：**data 节点上的ES进程占用的内存较大，引发JVM的大规模内存回收，造成ES进程失去响应，从而长时间没ping通主节点，导致误判主节点下线
-   **主节点故障**。

**解决方案：**

-   **调大超时时间减少误判：**discovery.zen.ping\_timeout节点状态的响应时间，默认为3s，可以适当调大，如果master在该响应时间的范围内没有做出响应应答，判断该节点已经挂掉了。调大超时时间（如6s，discovery.zen.ping\_timeout:6），可适当减少误判
-   **修改最小候选主节点数量：**配置最小候选主节点数量minimum\_master\_nodes:备选主节点数量/ 2 +1。该参数是用于控制选举条件，master故障后，只有备选主节点数量到达(n / 2) +1个才开始选举。在es7.0以后，已经成为默认配置，因此一般不会发生脑裂问题
-   **master和data分离：**即master节点与data节点分离，这样master就不会因为访问量大而延迟。

## 七、ES怎么进行调优？

**1、增大Refresh时长**

Lucene 在新增数据时，采用了延迟写入的策略，默认情况下索引的refresh\_interval 为1 秒。

Lucene 将待写入的数据先写到内存中，超过 1 秒（默认）时就会触发一次 Refresh，然后 Refresh 会把内存中的的数据刷新到操作系统的文件缓存系统中。

如果我们对搜索的**时效性要求不高**，可以将 Refresh 周期延长，例如 30 秒。

这样还可以有效地减少段刷新次数，但这同时意味着需要消耗更多的 Heap 内存。

**2、加大 Flush 设置**

Flush 的主要目的是把文件缓存系统中的段持久化到硬盘，当 Translog 的数据量达到 512MB 或者 30 分钟时，会触发一次 Flush。

index.translog.flush\_threshold\_size 参数的默认值是 512MB，我们进行修改。

增加参数值意味着文件缓存系统中可能需要存储更多的数据，所以我们需要为操作系统的文件缓存系统留下足够的空间。

**3、减少副本的数量**

ES 为了保证集群的可用性，提供了 Replicas（副本）支持，然而每个副本也会执行分析、索引及可能的合并过程，所以 Replicas 的数量会严重影响写索引的效率。

当写索引时，需要把写入的数据都同步到副本节点，副本节点越多，写索引的效率就越慢。

如果我们需要大批量进行写入操作，可以先禁止Replica复制，设置index.number\_of\_replicas: 0 关闭副本。在写入完成后， Replica 修改回正常的状态。