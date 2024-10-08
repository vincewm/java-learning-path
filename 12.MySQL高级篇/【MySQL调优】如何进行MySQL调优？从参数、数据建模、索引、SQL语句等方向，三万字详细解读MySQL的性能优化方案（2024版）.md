> **导航：**
> 
> 本文一些内容需要聚簇索引、非聚簇索引、B+树、覆盖索引、索引下推等前置概念，虽然本文有简单回顾，但详细可以参考下文的【MySQL高级篇】
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[一、监控报警](#%E4%B8%80%E3%80%81%E7%9B%91%E6%8E%A7%E6%8A%A5%E8%AD%A6) 

[二、排查慢SQL](#%E4%BA%8C%E3%80%81%E6%8E%92%E6%9F%A5%E6%85%A2SQL)

[2.1 开启慢查询日志](#2.1%20%E5%BC%80%E5%90%AF%E6%85%A2%E6%9F%A5%E8%AF%A2%E6%97%A5%E5%BF%97%C2%A0) 

[2.2 找出最慢的几条SQL](#2.2%20%E6%89%BE%E5%87%BA%E6%9C%80%E6%85%A2%E7%9A%84%E5%87%A0%E6%9D%A1SQL)

[2.3 分析查询计划](#2.3%20%E5%88%86%E6%9E%90%E6%9F%A5%E8%AF%A2%E8%AE%A1%E5%88%92%C2%A0) 

[2.3.1 EXPLAIN命令](#2.3.1%20EXPLAIN%E5%91%BD%E4%BB%A4)

[2.3.2 EXPLAIN ANALYZE命令](#2.3.2%20EXPLAIN%20ANALYZE%E5%91%BD%E4%BB%A4)

[三、MySQL调优](#%E4%B8%89%E3%80%81MySQL%E8%B0%83%E4%BC%98)

[3.1 基础优化](#3.1%20%E5%9F%BA%E7%A1%80%E4%BC%98%E5%8C%96)

[3.1.1 缓存优化](#3.1.1%20%E7%BC%93%E5%AD%98%E4%BC%98%E5%8C%96%C2%A0) 

[3.1.1.0 简介](#3.1.1.0%20%E7%AE%80%E4%BB%8B)

[3.1.1.1 缓冲池优化](#3.1.1.1%20%E7%BC%93%E5%86%B2%E6%B1%A0%E4%BC%98%E5%8C%96)

[3.1.1.2 Redis优化](#3.1.1.2%C2%A0Redis%E4%BC%98%E5%8C%96)

[3.1.2 硬件优化](#3.1.2%20%E7%A1%AC%E4%BB%B6%E4%BC%98%E5%8C%96)

[3.1.3 参数优化](#3.1.3%20%E5%8F%82%E6%95%B0%E4%BC%98%E5%8C%96%C2%A0)

[3.1.4 定期清理垃圾](#3.1.4%C2%A0%E5%AE%9A%E6%9C%9F%E6%B8%85%E7%90%86%E5%9E%83%E5%9C%BE)

[3.1.4.1.清理不再使用的表](#3.1.4.1.%E6%B8%85%E7%90%86%E4%B8%8D%E5%86%8D%E4%BD%BF%E7%94%A8%E7%9A%84%E8%A1%A8)

[3.1.4.2.清理过期数据](#3.1.4.2.%E6%B8%85%E7%90%86%E8%BF%87%E6%9C%9F%E6%95%B0%E6%8D%AE)

[3.1.4.3.清理日志](#3.1.4.3.%E6%B8%85%E7%90%86%E6%97%A5%E5%BF%97)

[3.1.4.4.清理缓存池](#3.1.4.4.%E6%B8%85%E7%90%86%E7%BC%93%E5%AD%98%E6%B1%A0)

[3.1.4.5.优化表：OPTIMIZE TABLE](#3.1.4.5.%E4%BC%98%E5%8C%96%E8%A1%A8%EF%BC%9AOPTIMIZE%20TABLE)

[3.1.4.6.分析表：ANALYZE TABLE](#3.1.4.6.%E5%88%86%E6%9E%90%E8%A1%A8%EF%BC%9AANALYZE%C2%A0TABLE)

[3.1.4.7.计划任务清理数据、日志、优化表](#3.1.4.7.%E8%AE%A1%E5%88%92%E4%BB%BB%E5%8A%A1%E6%B8%85%E7%90%86%E6%95%B0%E6%8D%AE%E3%80%81%E6%97%A5%E5%BF%97%E3%80%81%E4%BC%98%E5%8C%96%E8%A1%A8)

[3.1.5 使用合适的存储引擎](#3.1.5%C2%A0%E4%BD%BF%E7%94%A8%E5%90%88%E9%80%82%E7%9A%84%E5%AD%98%E5%82%A8%E5%BC%95%E6%93%8E)

[3.1.5.1 各存储引擎使用场景](#3.1.5.1%C2%A0%E5%90%84%E5%AD%98%E5%82%A8%E5%BC%95%E6%93%8E%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)

[3.1.5.2 回顾各存储引擎和B+树](#3.1.5.2%20%E5%9B%9E%E9%A1%BE%E5%90%84%E5%AD%98%E5%82%A8%E5%BC%95%E6%93%8E%E5%92%8CB%2B%E6%A0%91)

[3.1.6 读写分离](#3.1.6%C2%A0%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB)

[3.1.7 分库分表](#3.1.7%C2%A0%E5%88%86%E5%BA%93%E5%88%86%E8%A1%A8)

[3.2 表设计优化](#3.2%20%E8%A1%A8%E8%AE%BE%E8%AE%A1%E4%BC%98%E5%8C%96)

[3.2.1 混合业务分表、冷热数据分表](#3.2.1%20%E6%B7%B7%E5%90%88%E4%B8%9A%E5%8A%A1%E5%88%86%E8%A1%A8%E3%80%81%E5%86%B7%E7%83%AD%E6%95%B0%E6%8D%AE%E5%88%86%E8%A1%A8)

[3.2.2 联合查询改为中间关系表](#3.2.2%20%E8%81%94%E5%90%88%E6%9F%A5%E8%AF%A2%E6%94%B9%E4%B8%BA%E4%B8%AD%E9%97%B4%E5%85%B3%E7%B3%BB%E8%A1%A8)

[3.2.3 遵循三个范式](#3.2.3%20%E9%81%B5%E5%BE%AA%E4%B8%89%E4%B8%AA%E8%8C%83%E5%BC%8F)

[3.2.4 字段建议非空约束](#3.2.4%20%E5%AD%97%E6%AE%B5%E5%BB%BA%E8%AE%AE%E9%9D%9E%E7%A9%BA%E7%BA%A6%E6%9D%9F)

[3.2.5 反范式：使用冗余字段](#3.2.5%20%E4%BD%BF%E7%94%A8%E5%86%97%E4%BD%99%E5%AD%97%E6%AE%B5)

[3.2.6 数据类型优化](#3.2.6%20%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E4%BC%98%E5%8C%96)

[3.3 索引优化](#3.3%20%E7%B4%A2%E5%BC%95%E4%BC%98%E5%8C%96)

[3.3.0 数据准备](#3.3.0%20%E6%95%B0%E6%8D%AE%E5%87%86%E5%A4%87)

[3.3.0.1 创建学生表并生成50w条数据](#3.3.0.1%20%E5%88%9B%E5%BB%BA%E5%AD%A6%E7%94%9F%E8%A1%A8%E5%B9%B6%E7%94%9F%E6%88%9050w%E6%9D%A1%E6%95%B0%E6%8D%AE)

[3.3.0.2 创建删除所有索引的存储过程](#3.3.0.2%20%E5%88%9B%E5%BB%BA%E5%88%A0%E9%99%A4%E6%89%80%E6%9C%89%E7%B4%A2%E5%BC%95%E7%9A%84%E5%AD%98%E5%82%A8%E8%BF%87%E7%A8%8B)

[3.3.1 考虑索引失效的11个场景](#3.3.1%20%E8%80%83%E8%99%91%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88%E7%9A%8411%E4%B8%AA%E5%9C%BA%E6%99%AF)

[3.3.1.1.尽量全值匹配](#3.3.1.1.%E5%B0%BD%E9%87%8F%E5%85%A8%E5%80%BC%E5%8C%B9%E9%85%8D)

[3.3.1.2.考虑最左前缀](#3.3.1.2.%E8%80%83%E8%99%91%E6%9C%80%E5%B7%A6%E5%89%8D%E7%BC%80)

[3.3.1.3.主键尽量有序](#3.3.1.3.%E4%B8%BB%E9%94%AE%E5%B0%BD%E9%87%8F%E6%9C%89%E5%BA%8F)

[3.3.1.4.计算、函数导致索引失效](#3.3.1.4.%E8%AE%A1%E7%AE%97%E3%80%81%E5%87%BD%E6%95%B0%E5%AF%BC%E8%87%B4%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)

[3.3.1.5.类型转换导致索引失效](#3.3.1.5.%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2%E5%AF%BC%E8%87%B4%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)

[3.3.1.6.没索引下推时，范围条件右边的列索引失效](#3.3.1.6.%E8%8C%83%E5%9B%B4%E6%9D%A1%E4%BB%B6%E5%8F%B3%E8%BE%B9%E7%9A%84%E5%88%97%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)

[3.3.1.7.没覆盖索引时，“不等于”导致索引失效](#3.3.1.7.%E6%B2%A1%E8%A6%86%E7%9B%96%E7%B4%A2%E5%BC%95%E6%97%B6%EF%BC%8C%E2%80%9C%E4%B8%8D%E7%AD%89%E4%BA%8E%E2%80%9D%E5%AF%BC%E8%87%B4%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)

[3.3.1.8.没覆盖索引时，左模糊查询导致索引失效](#3.3.1.8.%E6%B2%A1%E8%A6%86%E7%9B%96%E7%B4%A2%E5%BC%95%E6%97%B6%EF%BC%8C%E5%B7%A6%E6%A8%A1%E7%B3%8A%E6%9F%A5%E8%AF%A2%E5%AF%BC%E8%87%B4%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)

[3.3.1.9.没覆盖索引时，is not null、not like无法使用索引](#3.3.1.9.%E6%B2%A1%E8%A6%86%E7%9B%96%E7%B4%A2%E5%BC%95%E6%97%B6%EF%BC%8Cis%20not%20null%E3%80%81not%20like%E6%97%A0%E6%B3%95%E4%BD%BF%E7%94%A8%E7%B4%A2%E5%BC%95)

[3.3.1.10.“OR”前后存在非索引列或不同索引列，导致索引失效](#3.3.1.10.%E2%80%9COR%E2%80%9D%E5%89%8D%E5%90%8E%E5%AD%98%E5%9C%A8%E9%9D%9E%E7%B4%A2%E5%BC%95%E5%88%97%E6%88%96%E4%B8%8D%E5%90%8C%E7%B4%A2%E5%BC%95%E5%88%97%EF%BC%8C%E5%AF%BC%E8%87%B4%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)

[3.3.1.11.不同字符集导致索引失败](#3.3.1.11.%E4%B8%8D%E5%90%8C%E5%AD%97%E7%AC%A6%E9%9B%86%E5%AF%BC%E8%87%B4%E7%B4%A2%E5%BC%95%E5%A4%B1%E8%B4%A5)

[3.3.2 遵循索引设计原则](#3.3.2%20%E9%81%B5%E5%BE%AA%E7%B4%A2%E5%BC%95%E8%AE%BE%E8%AE%A1%E5%8E%9F%E5%88%99)

[3.3.3 连接查询优化](#3.3.3%20%E8%BF%9E%E6%8E%A5%E6%9F%A5%E8%AF%A2%E4%BC%98%E5%8C%96)

[3.3.3.1 被驱动表连接字段加索引](#3.3.3.1%20%E8%A2%AB%E9%A9%B1%E5%8A%A8%E8%A1%A8%E8%BF%9E%E6%8E%A5%E5%AD%97%E6%AE%B5%E5%8A%A0%E7%B4%A2%E5%BC%95)

[3.3.3.2 小表驱动大表](#3.3.3.2%20%E5%B0%8F%E8%A1%A8%E9%A9%B1%E5%8A%A8%E5%A4%A7%E8%A1%A8)

[3.3.3.3 两表连接字段类型必须一致](#3.3.3.3%20%E4%B8%A4%E8%A1%A8%E8%BF%9E%E6%8E%A5%E5%AD%97%E6%AE%B5%E7%B1%BB%E5%9E%8B%E5%BF%85%E9%A1%BB%E4%B8%80%E8%87%B4)

[3.3.4 子查询优化](#3.3.4%C2%A0%E5%AD%90%E6%9F%A5%E8%AF%A2%E4%BC%98%E5%8C%96)

[3.3.4.1.子查询优化成关联查询](#3.3.4.1.%E5%AD%90%E6%9F%A5%E8%AF%A2%E4%BC%98%E5%8C%96%E6%88%90%E5%85%B3%E8%81%94%E6%9F%A5%E8%AF%A2)

[3.3.4.2.多次查询代替子查询](#3.3.4.2.%E5%A4%9A%E6%AC%A1%E6%9F%A5%E8%AF%A2%E4%BB%A3%E6%9B%BF%E5%AD%90%E6%9F%A5%E8%AF%A2)

[3.3.4.3.临时表代替子查询](#3.3.4.3.%E4%B8%B4%E6%97%B6%E8%A1%A8%E4%BB%A3%E6%9B%BF%E5%AD%90%E6%9F%A5%E8%AF%A2)

[3.3.5 排序优化](#3.3.5%C2%A0%E6%8E%92%E5%BA%8F%E4%BC%98%E5%8C%96)

[3.3.5.1 合理选择索引排序和FileSort排序](#3.3.5.1%20%E5%90%88%E7%90%86%E9%80%89%E6%8B%A9%E7%B4%A2%E5%BC%95%E6%8E%92%E5%BA%8F%E5%92%8CFileSort%E6%8E%92%E5%BA%8F)

[3.3.5.2 排序字段符合最左前缀](#3.3.5.2%20%E6%8E%92%E5%BA%8F%E5%AD%97%E6%AE%B5%E7%AC%A6%E5%90%88%E6%9C%80%E5%B7%A6%E5%89%8D%E7%BC%80)

[3.3.5.3 全升序或者全降序](#3.3.5.3%20%E5%85%A8%E5%8D%87%E5%BA%8F%E6%88%96%E8%80%85%E5%85%A8%E9%99%8D%E5%BA%8F)

[3.3.5.4 待排序数量大时，尽管索引没失效，索引效率不如filesort](#3.3.5.4%20%E5%BE%85%E6%8E%92%E5%BA%8F%E6%95%B0%E9%87%8F%E5%A4%A7%E6%97%B6%EF%BC%8C%E5%B0%BD%E7%AE%A1%E7%B4%A2%E5%BC%95%E6%B2%A1%E5%A4%B1%E6%95%88%EF%BC%8C%E7%B4%A2%E5%BC%95%E6%95%88%E7%8E%87%E4%B8%8D%E5%A6%82filesort)

[3.3.5.5 范围查询使排序索引失效](#3.3.5.5%20%E8%8C%83%E5%9B%B4%E6%9F%A5%E8%AF%A2%E4%BD%BF%E6%8E%92%E5%BA%8F%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)

[3.3.5.6 优先范围字段加索引（即使排序索引失效）](#3.3.5.6%20%E4%BC%98%E5%85%88%E8%8C%83%E5%9B%B4%E5%AD%97%E6%AE%B5%E5%8A%A0%E7%B4%A2%E5%BC%95%EF%BC%88%E5%8D%B3%E4%BD%BF%E6%8E%92%E5%BA%8F%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88%EF%BC%89)

[3.3.5.7 调优FileSort](#3.3.5.7%20%E8%B0%83%E4%BC%98FileSort)

[3.3.6 分组优化](#3.3.6%C2%A0%E5%88%86%E7%BB%84%E4%BC%98%E5%8C%96)

[3.3.7 深分页查询优化](#3.3.7%C2%A0%E6%B7%B1%E5%88%86%E9%A1%B5%E6%9F%A5%E8%AF%A2%E4%BC%98%E5%8C%96)

[3.3.8 尽量覆盖索引](#3.3.8%C2%A0%E5%B0%BD%E9%87%8F%E8%A6%86%E7%9B%96%E7%B4%A2%E5%BC%95)

[3.3.9 字符串前缀索引](#3.3.9%C2%A0%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%89%8D%E7%BC%80%E7%B4%A2%E5%BC%95)

[3.3.10 尽量使用MySQL5.6支持的索引下推](#3.3.10%C2%A0%E5%B0%BD%E9%87%8F%E4%BD%BF%E7%94%A8MySQL5.6%E6%94%AF%E6%8C%81%E7%9A%84%E7%B4%A2%E5%BC%95%E4%B8%8B%E6%8E%A8)

[3.3.11 读少写多的场景，尽量用普通索引](#3.3.11%C2%A0%E5%86%99%E5%A4%9A%E8%AF%BB%E5%B0%91%E7%9A%84%E5%9C%BA%E6%99%AF%EF%BC%8C%E5%B0%BD%E9%87%8F%E7%94%A8%E6%99%AE%E9%80%9A%E7%B4%A2%E5%BC%95)

[3.4 SQL优化](#3.4%20SQL%E4%BC%98%E5%8C%96)

[3.4.1 合理选用 EXISTS 和 IN](#3.4.1%C2%A0%E5%90%88%E7%90%86%E9%80%89%E7%94%A8%20EXISTS%20%E5%92%8C%20IN)

[3.4.2 统计数量COUNT(1) 或 COUNT(\*)](#3.4.2%C2%A0%E7%BB%9F%E8%AE%A1%E6%95%B0%E9%87%8FCOUNT%281%29%20%E6%88%96%20COUNT%28*%29)

[3.4.3 避免SELECT \*](#3.4.3%C2%A0%E9%81%BF%E5%85%8DSELECT%20*)

[3.4.4 全表扫描时尽量用 LIMIT](#3.4.4%C2%A0%E5%85%A8%E8%A1%A8%E6%89%AB%E6%8F%8F%E6%97%B6%E5%B0%BD%E9%87%8F%E7%94%A8%20LIMIT)

[3.4.5 使用 LIMIT N，少用 LIMIT M, N](#3.4.5%C2%A0%E4%BD%BF%E7%94%A8%20LIMIT%20N%EF%BC%8C%E5%B0%91%E7%94%A8%20LIMIT%20M%2C%20N)

[3.4.6 代码将长事务拆为多个小事务](#3.4.6%C2%A0%E4%BB%A3%E7%A0%81%E5%B0%86%E9%95%BF%E4%BA%8B%E5%8A%A1%E6%8B%86%E4%B8%BA%E5%A4%9A%E4%B8%AA%E5%B0%8F%E4%BA%8B%E5%8A%A1)

[3.4.7 删改前先查询](#3.4.7%C2%A0%E5%88%A0%E6%94%B9%E5%89%8D%E5%85%88%E6%9F%A5%E8%AF%A2)

[3.4.8 尽量UNION ALL而不是UNION](#3.4.8%C2%A0%E5%B0%BD%E9%87%8FUNION%20ALL%E8%80%8C%E4%B8%8D%E6%98%AFUNION)

--

MySQL调优主要分为三个步骤：监控报警、 排查慢SQL、MySQL调优。

## 一、监控报警 

在MySQL调优过程中，首先第一步是发现问题，而发现慢SQL的场景可以是用户访问时查询慢，也可以是通过监控工具监控到慢SQL。

监控工具（例如Prometheus+Grafana）监控MySQL，发现查询性能变慢时，可以报警提醒运维人员：

![](https://i-blog.csdnimg.cn/blog_migrate/9d1123b56f83677b4763b70a54b09475.png)

**其他监控工具：**

1.  **MySQL Enterprise Monitor：**由Oracle提供的商业工具，提供实时和历史的MySQL性能监控，包括查询性能、服务器状态、数据库复制等。
2.  **Percona Monitoring and Management：**Percona提供的开源工具，提供性能监控、查询分析、数据库配置等功能。
3.  **MyTOP：**一个基于命令行的工具，用于实时监控MySQL数据库的性能。
4.  **MySQL Performance Schema：**MySQL自带的性能监控工具，可以通过查询Performance Schema表来获取有关数据库性能和资源利用情况的详细信息。
5.  **Nagios：**一个通用的网络监控工具，可以使用插件来监控MySQL数据库的各种指标。
6.  **Zabbix：**一个通用的网络监控工具，可以使用插件来监控MySQL数据库的各种指标。
7.  **Datadog：**一个云端监控服务，提供对MySQL数据库的性能和状态的实时监控。
8.  **Prometheus + Grafana：**一组流行的开源工具，可以通过Prometheus监控MySQL数据库，然后使用Grafana创建漂亮的仪表板进行可视化。

## 二、排查慢SQL

### 2.1 开启慢查询日志 

**查看慢查询次数：**

```sql
# 临时关闭慢查询日志，如果想永久关闭，需要修改my.ini或my.cnf配置文件
show status like 'slow_queries';
```

![](https://i-blog.csdnimg.cn/blog_migrate/a0315cca9f7788cbd0db02cf355a7aa6.png)

**查询慢查询日志是否打开：**

```bash
SHOW VARIABLES LIKE 'slow_query_log';
```

![](https://i-blog.csdnimg.cn/blog_migrate/b4675a6c53927b8e066ce78b5dc2a356.png)

**开启慢查询日志，修改慢查询阈值：**

```bash
set slow_query_log='ON';    #开启慢查询日志
set long_query_time = 1;     #设置慢查询阈值
```

### 2.2 找出最慢的几条SQL

可以通过**mysqldumpslow命令，分析慢查询日志，找到最慢的几条语句：**

mysqldumpslow 命令的具体参数如下：

-   \-a: 不将数字抽象成N，字符串抽象成S
-   \-s: 是表示按照何种方式排序：
-   c: 访问次数
-   l: 锁定时间
-   r: 返回记录
-   t: 查询时间
-   al:平均锁定时间
-   ar:平均返回记录数
-   at:平均查询时间 （默认方式）
-   ac:平均查询次数
-   \-t: 即为返回前面多少条的数据；
-   \-g: 后边搭配一个正则匹配模式，大小写不敏感的；

> 示例： 按照查询时间排序，查看前五条慢查询SQL 语句
> 
> ```bash
> #命令行，按照查询时间排序，查看前五条 慢查询SQL 语句
> mysqldumpslow -s t -t 5 /var/lib/mysql/xxx-slow.log    
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/68082432a630787639e7981a68448c41.png)

### 2.3 分析查询计划 

#### 2.3.1 EXPLAIN命令

explan分析sql执行计划（访问类型、记录条数、索引长度等）；主要关注字段：

1.  **possible\_keys：**查询可能用到的索引
2.  **key：**实际使用的索引
3.  **key\_len：**实际使用的索引的字节数长度。
4.  **type：**访问类型，看有没有走索引。按性能从高到低：
    1.  **system：**一行记录时,快速查询。例如SELECT \* FROM dual;
    2.  **const：**命中主键索引或唯一索引
    3.  **eq\_ref：**对于前一张表的结果（连接查询或子查询），第二个表查找时命中主键索引或唯一索引
    4.  **ref：**命中非唯一索引
    5.  **range：**范围索引。_**阿里规约：**SQL 性能优化的目标：至少要达到 range 级别，要求是 ref 级别，如果可以是const最好。_
    6.  **index：**索引树上全表扫描
    7.  **index\_merge：**查询条件多时，使用多个索引合并结果。使用了多个索引来满足查询条件，然后将结果合并。这通常发生在查询中有多个条件，每个条件可以使用不同的索引来访问数据。
    8.  **all：**全表扫描。性能最差
5.  **Extra：**额外信息。看有没有走索引。
    1.  **using index：**覆盖索引，不回表。
    2.  **using filesort：**需要额外的排序。排序分为索引排序和filesort排序，索引排序一般更快，深分页等查询数据量大时filesort更快。
    3.  **using index condition：**索引下推。MySQL5.6开始支持。联合索引某字段是模糊查询（非左模糊）或者范围查询、不等于时，该字段进行条件判断后，后面几个字段可以直接条件判断，判断过滤后再回表对不包含在联合索引内的字段条件进行判断。
    4.  **using where：**没完全走索引，需要回表。在MySQL中，回表（table lookup 或 table access）是指在使用非聚簇索引（secondary index）查询时，数据库先通过索引查找到满足条件的记录的主键（或行ID），然后再根据主键到聚簇索引（或数据表）中查找完整的记录。

> **执行计划各个列的作用**
> 
> <table border="1" cellpadding="1" cellspacing="1"><tbody><tr><td>id</td><td>每个SELECT子句或者join操作都会被分配一个唯一的编号，编号越小优先级越高，id相同的语句可以被认为是一组。id为NULL表示独立的子查询，子查询优先级都比主查询高。</td></tr><tr><td>select_type</td><td>查询的类型。主查询(primary)、普通查询(simple)、联合查询、子查询(subquery)、derived(from表临时子查询)、union(union后查询)、union result()</td></tr><tr><td>table</td><td>表名。显示当前这行的数据是哪个表的。</td></tr><tr><td>partitions</td><td>匹配的分区信息。如果表未分区则为NULL。</td></tr><tr><td><strong>type</strong></td><td><strong>访问类型，根据索引、全表扫描等方法来执行查询的优化策略。</strong>all（全表扫描），ref（命中非唯一索引），const（命中主键/唯一索引）、range(范围索引查询)、index_merge(使用多个索引)、&nbsp;system(一行记录时,快速查询)。</td></tr><tr><td>possible_keys</td><td><p>可能用到的索引。列出MySQL能够使用哪些索引来查询。</p><p>如果该列只有一个possible_keys，通常意味着这个查询是高效的。</p><p>如果这个列有多个possible_keys，并且MySQL只使用了其中一个，则需要考虑是否需要在该列上增加一个联合索引。</p></td></tr><tr><td><strong>key</strong></td><td><strong>实际上使用的索引。</strong>如果没有明确的指定KEY，MySQL会根据查询条件自动选择最优的索引。</td></tr><tr><td><strong>key_len</strong></td><td>实际使用到索引的字节数长度。越短表示越快，一般表示索引字段越小越好。</td></tr><tr><td>ref</td><td>当使用索引列等值查询时，与索引列进行等值匹配的对象信息。常量等值查询const, 表达式/函数使用到时func,关联查询显示关联字段名</td></tr><tr><td><strong>rows</strong></td><td>预估的需要读取的记录条数。数值越小越好，表示结果集越小，查询越高效。</td></tr><tr><td>filtered</td><td>某个表经过搜索条件过滤后剩余记录条数的百分比。这个值越小越好，说明可通过索引直接返回数据。</td></tr><tr><td><strong>Extra</strong></td><td>额外信息。看有没有走索引，还是全表扫描了。一般搭配type字段看。Using index(使用到覆盖索引)、Using where(使用了回表，在服务器层面（即SQL层）应用WHERE条件过滤记录，而不是在存储引擎层面利用索引进行过滤。)、Using temporary(临时表存储结果集.排序/分组会使用)、Using filesort(排序操作未用索引)、Using join buffer(连接条件未用索引)、Impossible where(where约束语句可能有问题导致没有结果集)</td></tr></tbody></table>

#### 2.3.2 EXPLAIN ANALYZE命令

MySQL 8.0引入了explain analyze命令，相比explain，它提供的是实际的查询计划，而explain提供的是预估查询计划。

**explain和explain analyze的区别：**

-   **explain：**只生成执行计划，不实际执行
-   **explain analyze：**生成执行计划，并实际执行sql

> **示例：**
> 
> 人员表联查部门表：
> 
> ```sql
> EXPLAIN ANALYZE
> SELECT *
> FROM personnel p LEFT JOIN department d on p.department=d.id
> ```
> 
> 查询计划结果：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/50a7d7f776c0c600377a65823c0c674b.png)
> 
> ```sql
> -> Nested loop left join  (cost=915.25 rows=1980) (actual time=0.333..14.500 rows=2453 loops=1)
>     -> Table scan on p  (cost=222.25 rows=1980) (actual time=0.283..8.625 rows=2453 loops=1)
>     -> Filter: (p.DEPARTMENT = d.ID)  (cost=0.25 rows=1) (actual time=0.002..0.002 rows=1 loops=2453)
>         -> Single-row index lookup on d using PRIMARY (ID=p.DEPARTMENT)  (cost=0.25 rows=1) (actual time=0.002..0.002 rows=1 loops=2453)
> ```
> 
> 结果分析：
> 
> **第一行：**
> 
> Nested loop left join  (cost=915.25 rows=1980) (actual time=0.333..14.500 rows=2453 loops=1)
> 
> -   **Nested loop left join:** 执行的最外层操作，表示使用嵌套循环的左连接。
>     
> -   **成本估计**: (cost=915.25 rows=1980)：预计消耗915.25ms并返回1980行。
>     
> -   **实际时间**: (actual time=0.333..14.500 rows=2453 loops=1)：实际读取第一行平均花费0.333ms，返回所有行平均花费14.500ms，共循环调用该迭代器1次，返回2453行。
>     
> 
> **第二行：**
> 
> Table scan on p  (cost=222.25 rows=1980) (actual time=0.283..8.625 rows=2453 loops=1)
> 
> -   **Table scan on p:** 对人员表的全表扫描。
>     
> -   **成本估计**: (cost=222.25 rows=1980)：预计消耗222.25ms并返回1980行。
>     
> -   **实际时间**: (actual time=0.283..8.625 rows=2453 loops=1)：实际读取第一行平均花费0.283ms，返回所有行平均花费8.625ms，共循环调用该迭代器1次，返回2453行。
>     
> 
> **第三行：**
> 
> Filter: (p.DEPARTMENT = d.ID)  (cost=0.25 rows=1) (actual time=0.002..0.002 rows=1 loops=2453)
> 
> -   **Filter: (p.DEPARTMENT = d.ID):** 执行对 md\_gams\_jc\_department 表中 p.DEPARTMENT = d.ID 条件的过滤操作。
>     
> -   **成本估计**: (cost=0.25 rows=1)：预计消耗0.25ms并返回1行。
>     
> -   **实际时间**: (actual time=0.002..0.002 rows=1 loops=2453)：实际过滤操作平均花费0.002ms，共循环调用该迭代器2453次，返回1行。
>     
> 
> **第四行：**
> 
> Single-row index lookup on d using PRIMARY (ID=p.DEPARTMENT)  (cost=0.25 rows=1) (actual time=0.002..0.002 rows=1 loops=2453)
> 
> -   **Single-row index lookup on d using PRIMARY (ID=p.DEPARTMENT):** 对部门表使用主键索引进行单行查找，其中 ID=p.DEPARTMENT。
>     
> -   **成本估计**: (cost=0.25 rows=1)：预计消耗0.25ms并返回1行。
>     
> -   **实际时间**: (actual time=0.002..0.002 rows=1 loops=2453)：实际查找操作平均花费0.002ms，共循环调用该迭代器2453次，返回1行。
>     

## **三、MySQL调优**

### 3.1 基础优化

#### 3.1.1 缓存优化 

##### **3.1.1.0 简介**

-   **缓冲池优化：**调整缓冲池大小innodb\_buffer\_pool\_size。
-   **引入内存结构数据库：**例如Redis。

##### 3.1.1.1 缓冲池优化

**缓冲池：**MySQL的缓冲池被分为多个不同的缓存池，其中包括：

-   **查询缓存：**用来缓存查询结果。
-   **InnoDB缓存池：**用来缓存热点表和索引数据页。
-   **MyISAM缓存池：**用来缓存表数据块。

缓冲池是主内存中的一部分空间，用来缓存已使用的表和索引数据。缓冲池使得经常被使用的数据能够直接在内存中获得，从而提高速度。

**缓冲池的淘汰策略：**

LRU算法。MySQL的缓冲池默认使用的是LRU（最近最少使用）淘汰策略，它会优先缓存最近使用的数据。当缓冲池的空间不足时，MySQL会将最不常用的数据从缓冲池中替换出去，以腾出空间缓存新的数据。

> **lru算法底层原理：**
> 
> 底层是双向链表（因为经常要移动元素），链表首部是最常使用元素，尾部是最少使用元素。
> 
> 每次刚访问的数据会移动到链表首部，刚添加的数据也会添加到链表首部。超出maxmemory会淘汰链表尾部元素，它也最长时间没有被使用的数据。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/be86667b5fa68de28d2ec7ff3e5d6697.png)

**缓冲池相关参数：**

MySQL的缓存设置包括多个参数，其中比较常见的缓存参数包括以下几个：

-   **MyISAM缓冲池大小：**key\_buffer\_size：该参数用来设置MyISAM索引的缓存大小。如果应用程序中涉及到大量的索引查询，可以适当提高该值。一般来说，key\_buffer\_size占用总内存的1/4到1/3比较合适。
    
-   **InnoDB缓冲池大小：**innodb\_buffer\_pool\_size：该参数用来设置InnoDB缓冲池的大小。**InnoDB**存储引擎使用**缓冲池来缓存数据和索引文件**。如果InnoDB表的读写频次较高，建议将该值设置为物理内存的70%到80%。
    
-   **排序缓冲区大小：**sort\_buffer\_size：该参数用来设置排序缓冲区大小。如果查询中涉及到ORDER BY或GROUP BY操作，可以适当提高该值。一般来说，sort\_buffer\_size占用总内存的1/4到1/3比较合适。
    
-   **读取缓冲区大小：**read\_buffer\_size和read\_rnd\_buffer\_size：这两个参数是用来设置读取缓冲区大小的，默认值为128 KB。如果应用程序中经常进行大文件的读取操作，可以适当提高这两个参数。
    
-   **binlog大小：**binlog\_cache\_size：该参数是用来设置二进制日志的缓存大小。如果应用程序中需要持久化一些数据，可以开启二进制日志，并适当调整该参数。
    

**参数配置方法：**

**1.查看当前缓冲池参数：**

```java
show VARIABLES  like 'key_buffer_size';
```

 ![](https://i-blog.csdnimg.cn/blog_migrate/5c662eef1b21877dad4d0ba30050a64b.png)

**2.修改缓冲池参数：**

-   方法一：在运行中的MySQL实例中临时设置这个值（这不会持久保存，重启后会失效）：
    
    ```java
    SET GLOBAL key_buffer_size = 67108864;  -- 64MB
    ```
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/c4c3cde5fc65f82298711660435b9ed6.png)
    
-   方法二： 在MySQL配置文件（通常是 my.cnf 或 my.ini）中进行更改，然后重启MySQL服务使更改生效。例如：
    
    ```
    [mysqld]
    key_buffer_size = 64M
    ```
    

##### 3.1.1.2 Redis优化

Redis是一个基于内存的NoSQL数据库，MySQL是一个基于磁盘的关系型数据库。

我们知道，内存的读写速度是远高于磁盘的，所以对于一些多读少写的热点数据，搭配Redis存储数据，可以极大地提高数据的访问速度。

> **Redis特点：**
> 
> -   **数据库：**Redis是一款基于键值对的、线程安全的NoSQL数据库；
> -   **内存读写性能：**它在内存中读写性能非常高，每秒可以处理超过百万次的读写操作。
> -   **服务端线程安全，客户端线程不安全：**Redis服务端是线程安全的，永远只有主线程一个线程进行读写，不需要任何的同步机制。虽然Redis6.0增加了多线程的模型，但多线程目的只是为了处理网络的IO事件，读写指令的执行依然由主线程自己处理。Redis客户端层面线程不安全，要引入原子指令（例如INCR是给数值原子性加1）、分布式锁、lua脚本保证Redis的原子操作。
> 
> **Redis读写为什么不采用多线程？** 
> 
> -   **CPU不是瓶颈：**Redis在内存中读写性能非常高，CPU不是Redis的瓶颈，无需使用多线程。
> -   **担心加锁影响性能：**多线程情况下，想实现线程安全必须加锁，加锁将极大地影响性能。
> 
> **为什么单线程还读写性能这么高？**
> 
> -   **基于内存：**Redis是基于内存的，内存的读写速度非常快；
> -   **上下文切换：**单线程避免了不必要的上下文切换和竞争条件；
> -   **IO多路复用：**底层采用NIO（非阻塞IO），NIO采用IO多路复用技术，一个线程通过多路复用器处理多个连接。IO多路复用技术选用epoll调用模型，红黑树存所有事件，链表存就绪事件。epoll\_wait函数链表，通知应用程序读写操作。
> 
> **Redis的瓶颈：**
> 
> -   **内存：**因为读写在内存中进行，内存大小会影响Redis性能。可以通过加内存、读写分离优化性能。
> -   **网络带宽：**网络 IO是Redis最大瓶颈，也就是客户端和服务端之间的网络传输延迟。Redis6.0引入了网络IO多线程模型，提高了性能瓶颈。
> 
> **功能：**键过期、事务、lua脚本（基于C语言，性能快）、持久化机制。
> 
> **事务：**
> 
> -   **实现方式：**MULTI（开启事务，将命令都放进队列里），EXEC（执行事务），DISCARD（取消事务，清空队列）。
> -   **不支持回滚：**在语法正确的情况下，Redis事务一定会执行成功。只有语法错误时才会导致事务失败，而语法问题应该在开发时就避免，所以为了提高性能，Redis事务不支持回滚。事务是一个原子操作，要么全部执行，要么全不执行。
> -   **不完全满足ACID特性：**Redis只满足隔离性和持久性，不满足原子性和一致性。
>     -   **原子性：**事务的所有操作，要么全部成功，要么全部失败。Redis不满足原子性，单个 Redis 命令的执行是原子性的，但事务失败后无法回滚。
>     -   **一致性：**事务前后，数据库的约束没有被破坏，保持前后一致。Redis连约束这个概念都没有。
>     -   **隔离性：**操作同一资源的并发事务之间相互隔离，不会互相干扰。Redis满足隔离性，因为redis server是单线程的，串行化执行事务，肯定是满足隔离性的。
>     -   **持久性：**事务的结果最终一定会持久化到数据库，宕机等故障也无法影响。Redis在开启aof并指定立刻持久化命令时，满足持久性。rdb模式会丢失部分数据，不满足持久性。
> 
> **数据类型：** string、hash、 list、set（集合）、zset（有序集合）
> 
> **应用场景：**缓存热点且不经常修改的数据、计数器、限时业务、分布式锁（set nx）、队列等。
> 
> **持久化机制：**
> 
> -   **数据备份机制RDB（默认）：数据**每隔一段时间写进磁盘rdb文件，故障后从文件读。可以在redis.conf配置多少秒内多少key修改时自动bgsave。占CPU和内存但恢复快，不能恢复完整数据。save命令是主进程立即执行一次RDB，其他所有命令进程阻塞。bgsave是子进程fork主进程，阻塞并拷贝一份主进程的页表（虚拟内存到物理内存的映射关系），然后子进程写数据到rdb文件，主进程继续处理用户请求，
> -   **追加文件机制AOF：**命令**日志**按指定频率（默认立刻，在redis.conf配置为缓存一秒）写进磁盘aof文件，可以按条件（redis.conf配置，比上次重写aof文件超过多少百分比时自动重写、aof文件超过多大自动重写）自动重写aof文件中的命令（多次更新同一数据只有最近一次更新有效），故障后从文件读命令恢复数据。不占CPU和内存占IO，能恢复完整或故障1s前的数据但恢复慢。

#### 3.1.2 硬件优化

在很多情景下，我们已经对数据库的索引、参数等数据进行了优化，但当数据库并发量高、数据量大时，就需要考虑优化服务器配置、分库分表等方案，直观地提高数据库的性能。 

**优化方案：** 

-   服务器加内存条
-   升级SSD固态硬盘
-   把磁盘I/O分散在多个设备
-   配置多处理器。

#### 3.1.3 参数优化

除了以上说的缓冲池参数外，我们还可以通过其他参数，对MySQL进行优化。

**优化方案：**  

-   **关闭不必要的服务和日志：**调优结束后关闭慢查询日志；
    
    ```bash
    # 临时关闭慢查询日志，如果想永久关闭，需要修改my.ini或my.cnf配置文件
    SET GLOBAL slow_query_log = 'OFF';
    ```
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/2f270460b87da4ba7aa7b6a558086e17.png)
    
-   **调整最大连接数：**max\_connections。MySQL5.5及之后版本默认最大连接数是151，可以根据实际场景，压测得出合适的最大连接数。
    -   MySQL5.5 ～ 5.7：默认的最大连接数都是 151，上限为：100000
    -   MySQL5.0 版本：默认的最大连接数为 100，上限为 16384
    -   MySQL8.0 版本: 默认的最大连接数是 151
-   **调整线程池缓存线程数：**thread\_cache\_size，缓存空闲线程，有连接时直接分配该线程处理连接；
-   **调整缓冲池大小：**innodb\_buffer\_pool\_size 。上面3.1.1已经详细说过了，此处不再赘述。

>  **修改最大连接数：**
> 
> **1.查看当前最大连接数：**
> 
> ```
> SHOW VARIABLES LIKE 'max_connections';
> ```
> 
> ![](https://i-blog.csdnimg.cn/direct/165683a5005c4876b37c555abb27ecb4.png)
> 
> **2.临时修改最大连接数（重启后失效）：**
> 
> ```bash
> SET GLOBAL max_connections =1000
> ```
> 
> ![](https://i-blog.csdnimg.cn/direct/6e56f99149b64f14a7c15fa4ae76dd59.png)
> 
> **3.永久修改连接数（重启后有效）：**
> 
> 在Linux系统中，配置文件通常是/etc/my.cnf或/etc/mysql/my.cnf。在Windows系统中，通常是C:\\ProgramData\\MySQL\\MySQL Server 5.7\\my.ini。
> 
> ```bash
> [mysqld]
> max_connections = 1000
> ```
> 
> 然后重启
> 
> ```bash
> sudo systemctl restart mysql
> ```
> 
> 如果是windows，则服务重启：
> 
> ![](https://i-blog.csdnimg.cn/direct/816e62e2e4ef46b29c13c8eb0eb5bdcc.png)

#### 3.1.4 **定期清理垃圾**

对于不再使用的表、数据、日志、缓存等，应该及时清理，避免占用过多的MySQL资源，从而提高MySQL的性能。

##### 3.1.4.1.清理不再使用的表

```bash
# 删除这些表：
DROP TABLE table_name;
# 保留表结构但删除所有数据
delete from table_name;
```

##### 3.1.4.2.清理过期数据

一些场景下，某个时期之前的数据都不再需要，可以清理这些数据：

```bash
DELETE FROM table_name WHERE createTime < NOW() - INTERVAL 30 DAY;
```

创建一个MySQL事件来定期清理过期数据：

```
CREATE EVENT clean_up_event
ON SCHEDULE EVERY 1 DAY
DO
  DELETE FROM table_name WHERE created_at < NOW() - INTERVAL 30 DAY;
```

##### 3.1.4.3.清理日志

```bash
# 清理2023年之前的日志
PURGE BINARY LOGS BEFORE '2023-01-01 00:00:00';
```

##### 3.1.4.4.清理缓存池

```bash
RESET QUERY CACHE;
```

![](https://i-blog.csdnimg.cn/blog_migrate/44960deaef76356ad265255159d8c022.png)

或者修改配置文件，禁用查询缓存以避免潜在的性能问题：

```bash
[mysqld]
query_cache_type = 0
query_cache_size = 0
```

##### 3.1.4.5.优化表：OPTIMIZE TABLE

在 MySQL 数据库中，OPTIMIZE TABLE 是一个重要的命令，用于优化表的性能和空间利用。通过重新组织表的存储结构，去除碎片、重建索引，OPTIMIZE TABLE 可以帮助提高查询性能、减少存储空间占用以及减少数据碎片。

**OPTIMIZE TABLE命令：**

```bash
OPTIMIZE TABLE table_name;
```

**优化原理：**

删除delete语句留下来的垃圾碎片。使用delete语句删除数据时，delete语句只会将记录的位置或者数据页标记为"可复用"，但是数据库磁盘文件的大小不会改变，即表空间不会被回收，此时使用该命令可以释放空间，压缩数据文件。

**底层原理：**

执行OPTIMIZE TABLE命令后，MySQL会进行以下几个步骤：

1.  **创建临时表**：MySQL 首先会创建一个与原表结构相同的临时表。
2.  **原表数据复制到临时表**：将原表中的数据复制到临时表中。
3.  **临时表去碎片**：在数据复制的过程中，MySQL 会对数据进行整理和重组，去除碎片，提高数据的连续性。
4.  **删旧表留新表**：当数据复制完成并且表被优化后，MySQL 会删除原表，然后将临时表重命名为原表的名称。

##### 3.1.4.6.分析表：ANALYZE **TABLE**

MySQL 的Optimizer（优化元件）在优化SQL语句时，首先需要收集一些相关信息，其中就包括表的cardinality（散列程度），它表示某个索引对应的列包含多少个不同的值——如果cardinality大大少于数据的实际散列程度，那么索引就基本失效了。

**ANALYZE TABLE命令：** 

```bash
ANALYZE TABLE table_name;
```

**对不同存储引擎的效果：**

-   **InnoDB：**对 InnoDB 表执行 ANALYZE TABLE 会重新计算表和索引的统计信息，并更新优化器统计信息。
-   **MyISAM：**对 MyISAM 表执行 ANALYZE TABLE 会分析表的关键字分布，并更新索引统计信息。
-   **其他存储引擎：**对其他存储引擎（如 MEMORY 或 ARCHIVE），效果类似，即更新表和索引的统计信息。

##### 3.1.4.7.计划任务清理数据、日志、优化表

对于以上的清理垃圾方案，可以写一个定时任务，定期统一清理垃圾数据、优化表的存储空间和索引。

**方案一：创建cron作业**

**1.编辑crontab**

使用crontab命令编辑当前用户的cron作业列表。对于系统级别的作业，可以使用sudo运行crontab。

```
crontab -e
```

> 或者，为特定用户编辑cron作业：
> 
> ```bash
> sudo crontab -u username -e
> ```

**2.编写cron作业**

在打开的编辑器中，添加新的cron作业，每行代表一个作业，执行指定路径下的脚本：

```
0 2 * * * /path/to/cleanup_script.sh
```

> cron表达式格式如下：
> 
> ```bash
> * * * * * command-to-be-executed
> - - - - -
> | | | | |
> | | | | +----- Day of the week (0 - 7) (Sunday=0 or 7)
> | | | +------- Month (1 - 12)
> | | +--------- Day of the month (1 - 31)
> | +----------- Hour (0 - 23)
> +------------- Minute (0 - 59)
> ```

**3.示例清理脚本**

/path/to/cleanup\_script.sh

```
#!/bin/bash

# MySQL credentials
USER="your_username"
PASSWORD="your_password"
DATABASE="your_database"

# 清理过期数据
mysql -u $USER -p$PASSWORD -e "DELETE FROM table_name WHERE created_at < NOW() - INTERVAL 30 DAY;" $DATABASE

# 清理二进制日志
mysql -u $USER -p$PASSWORD -e "PURGE BINARY LOGS BEFORE NOW() - INTERVAL 7 DAY;"

# 优化表
mysql -u $USER -p$PASSWORD -e "OPTIMIZE TABLE table_name;" $DATABASE
```

**方案二：使用Spring定时任务**

 spring根据定时任务的特征，将定时任务的开发简化到了极致。怎么说呢？要做定时任务总要告诉容器有这功能吧，然后定时执行什么任务直接告诉对应的bean什么时间执行就行了，就这么简单，一起来看怎么做

**步骤①**：**开启定时任务功能**，在引导类上开启定时任务功能的开关，使用**注解@EnableScheduling**

```java
@SpringBootApplication
//开启定时任务功能
@EnableScheduling
public class Springboot22TaskApplication {
    public static void main(String[] args) {
        SpringApplication.run(Springboot22TaskApplication.class, args);
    }
}
```

**步骤②**：在task包下**定义Bean**，在对应要定时执行的操作上方，使用注解@Scheduled定义执行的时间，执行时间的描述方式还是cron表达式

```java
@Component
public class MyBean {
    @Scheduled(cron = "0/1 * * * * ?")
    public void print(){
        // 具体清理垃圾的逻辑
    }
}
```

**如何想对定时任务进行详细配置，可以通过配置文件进行**

```bash
spring:
  task:
   	scheduling:
      pool:
       	size: 1							 #任务调度线程池大小 默认 1
      thread-name-prefix: ssm_      	 #调度线程名称前缀 默认 scheduling-      
        shutdown:
          await-termination: false		 #线程池关闭时等待所有任务完成
          await-termination-period: 10s	 #调度线程关闭前最大等待时间，确保最后一定关闭
```

> **总结**
> 
> 1.  spring task需要使用注解@EnableScheduling开启定时任务功能
>     
> 2.  为定时执行的的任务设置执行周期，描述方式cron表达式
>     

#### 3.1.5 **使用合适的存储引擎**

##### 3.1.5.1 **各存储引擎使用场景**

-   InnoDB：适合并发写入的场景（因为行级锁、B+树叶存记录）。
-   MyISAM：适合读取频繁，写入较少的场景（因为表级锁、B+树叶存地址）

##### 3.1.5.2 回顾各存储引擎和B+树

> **详细参考：**
> 
> [MySQL高级篇——存储引擎和索引\_mysql存储索引的表-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130308116 "MySQL高级篇——存储引擎和索引_mysql存储索引的表-CSDN博客")

**InnoDB：**支持外键和事务，行锁适合高并发，缓存索引和数据，内存要求高（因为要缓存索引和记录），适合存大数据量，增删改性能更优（行级锁高并发），耗费磁盘（因为有多个非聚簇索引，索引可能比记录空间还大）。

**B+每个元素的结构：**

![](https://i-blog.csdnimg.cn/blog_migrate/da238235bb5d5dd22cdec5fe7cc87d9e.png)

**InnoDB叶节点存数据各列的值：**

![](https://i-blog.csdnimg.cn/blog_migrate/f3ecbc0068cda24414b34b243e48c4b5.png)

因为聚簇索引树数据页存的元素第一个值是主键，而且聚簇索引树是默认创建的，所以如果我没有另外创建索引时，或者创建了其他索引但没发生覆盖索引时，用主键查询是最快的，例如select \* from student where id=xx快过select \* from student where age=xx。

当然聚簇索引并不一定是最快的，例如给age字段创建了索引，那么虽然select \* from

student where id=xx快过select \* from student where age=xx（因为要回表聚簇索引树查所有字段），但是select age from student where age=xx快过select age from student where id=xx，因为发生了覆盖索引，直接在非聚簇索引树就查到了age，没必要再回表聚簇索引树查其他字段信息。

**MyISAM：**不支持外键和事务，表锁不适合高并发，缓存索引和数据地址，内存要求低（因为不用缓存记录），查询性能更优（因为查询时InnoDB要维护MVCC一致，而且多缓存了记录），节省磁盘（因为磁盘不存完整记录）。

![](https://i-blog.csdnimg.cn/blog_migrate/170eb9068b402416a605df36378148ad.png)

<table border="1" cellspacing="0"><tbody><tr><td><p><strong>对比</strong></p></td><td><p><strong>InnoDB</strong></p></td><td><p><strong>MyISAM</strong></p></td></tr><tr><td><p>特点</p></td><td><p>支持外键和事务</p></td><td><p>不支持外键和事务</p></td></tr><tr><td><p>行表锁</p></td><td><p>行锁，操作时只锁某一行，不对其它行有影响， 适合高并发的操作</p></td><td><p>表锁，即使操作一条记录也会锁住整个表，不适合高并发的操作</p></td></tr><tr><td><p>缓存</p></td><td><p>缓存索引和数据，对内存要求较高，而且内存大小对性能有决定性的影响</p></td><td><p>只缓存索引，不缓存真实数据</p></td></tr><tr><td><p>关注点</p></td><td><p>事务：并发写、事务、更大资源</p></td><td><p>性能：节省资源、消耗少、简单业务、查询快</p></td></tr><tr><td><p>默认使用</p></td><td>5.5及其之后</td><td><p>5.5之前</p></td></tr></tbody></table>

#### 3.1.6 **读写分离**

**读写分离****：**读写分离能有效提高查询性能。读写分离基于MySQL的主从同步，一台主库负责写，多台从库负责读，每次主库发生写操作后，通过binlog和relay log，将修改操作同步到从库，从而保持主库和从库的数据一致性。

**主从同步：**一台或多台MySQL数据库(slave，即从库)从另一台NySQL数据库（master，即主库）进行日志的复制，然后再解析日志并应用到自身，最终实现从库的数据和主库的数据保持一致。MySQL主从复制是NySQL数据库自带功能，无需借助第三方工具。

**主从同步实现步骤：** 

1.  **主服务器**把数据更改记录到**二进制日志**（binlog，记录改不记录读，用于数据复制和数据恢复）中；
2.  **从服务器**异步近似实时地把主服务器的二进制日志**复制到**自己的**中继日志**（relay log）中；
3.  **从服务器重做**中继日志中的操作，把更改应用到自己的数据库上，以达到数据的最终一致性。

**主从同步的延时问题；**

-   **延时问题：**是主服务器压力大导致的复制延时问题。
-   **解决方案：**
    -   **网络带宽优化：**如果是网络延时问题，可以通过增大服务器的带宽解决。
    -   **硬件调优：**如果是因为硬件配置差导致同步延时，可以通过提升服务器配置解决。
-   **参数调优：**
    
    ```bash
    [mysqld]
    # 多线程复制（MySQL 5.7及以上版本）：设置并行线程数
    slave_parallel_workers = 4  
    # 开启半同步复制（MySQL 5.5及以上版本）
    rpl_semi_sync_master_enabled = 1
    rpl_semi_sync_slave_enabled = 1
    # 同步延时时间：1秒超时。如果频繁写，则适当缩小；如果频繁读少写，则适当增大，以降低服务器压力
    rpl_semi_sync_master_timeout = 1000  
    ```
    
-   **缩小事务粒度：**一些代码中直接在整个Controller或者整个Service方法上加个@Transcational，而整个业务中其实只有一小段需要保持事务，这样是很影响性能的，因为事务不是那个，MySQL的连接会一直被占用，对数据库的压力很大。**解决方案：**减小代码中事务的粒度，例如将大事务拆解成小事务，将其中的一些查询操作脱离出去，只在写操作的方法中加事务；

**复制原理：** 

-   **主库二进制日志转储线程：**负责将二进制日志发给从库。强制从主库读取数据时（/\*master\*/ SELECT \* FROM user），会给二进制日志**加锁** ，读完解锁。
-   **从库I/O 线程：**负责连接主库，并向主库发送请求和复制二进制日志到中继日志。
-   **从库SQL 线程：**负责读取并执行中继日志中的更新语句，实现主从同步。 

**主从库数量：** 

-   每个 Master 可以有多个 Slave
-   每个 Slave 只能有一个唯一的服务器ID，只有一个 Master。

#### 3.1.7 **分库分表**

**概念：**

-   **只分表：**单表数据量大，读写出现瓶颈，这个表所在的库还可以支撑未来几年的增长。
-   **只分库：**整个数据库读写出现性能瓶颈，将整个库拆开。
-   **分库分表：**单表数据量大，所在库也出现性能瓶颈，就要既分库又分表。
-   **垂直拆分：**把字段分开。例如spu表的pic字段特别长，建议把这个pic字段拆到另一个表（同库或不同库）。
-   **水平拆分：**把记录分开。例如表数据量到达百万，我们拆成四张20万的表。

![](https://i-blog.csdnimg.cn/blog_migrate/1576dcf70952dbddcd5f9c63a6ec1130.png)

 **拆分原则：**

| 数据量增长情况 | 数据表类型 | 优化核心思想 |
| --- | --- | --- |
| 数据量为千万级，是一个相对**稳定**的数据量 | 状态表 | 能不拆就不拆读需求水平扩展 |
| 数据量为千万级，可能达到**亿级**或者更高 | 流水表 | 业务拆分，面向分布式存储设计 |
| 数据量为千万级，可能达到**亿级**或者更高 | 流水表 | 设计数据统计需求存储的分布式扩展 |
| 数据量为千万级，不应该有这么多的数据 | 配置表 | 小而简，避免大一统 |

**分库分表步骤：**

1.  **MySQL调优：**数据量能稳定在千万级，近几年不会到达亿级，其实是不用着急拆的，先尝试MySQL调优，优化读写性能。
    
2.  **目标评估：**评估拆几个库、表，举例: 当前20亿，5年后评估为100亿。分几个表? 分几个库?解答:一个合理的答案，1024个表，16个库按1024个表算，拆分完单表200万，5年后为1000万.1024个表\*200w≈100亿
    
3.  **表拆分：**
    
    -   **业务层拆分：**混合业务拆分为独立业务、冷热分离
        
    -   **数据层拆分：**
        
        -   **按日期拆分：**这种使用方式比较普遍，尤其是按照日期维度的拆分，其实在程序层面的改动很小，但是扩展性方面的收益很大。例如
            
            -   日维度拆分，如log\_20191021。
            -   月维度拆分，如log\_201910。当需要查询某天的日志时，就可以直接根据所在月份，直接得出在哪个日志表查。
            -   年维度拆分，如log\_2019
        -   **按主键范围拆分：**例如【1,200w】主键在一个表，【200w，400w】主键在一个表。优点是单表数据量可控。缺点是流量无法分摊，写操作集中在最后面的表。
            
        -   **中间表映射：**表随意拆分，引入中间表记录查询的字段值，以及它对应的数据在哪个表里。优点是灵活。确定是引入中间表让流程变复杂。
            
        -   **hash切分：**sharding\_key%N。优点是数据分片均匀，流量分摊。缺点是扩容需要迁移数据，跨节点查询问题。例如日志表拆分成logs\_0、logs\_1、logs\_2，每次读写日志时，将用户的id转成md5哈希值，然后%3，就可以得出具体要在哪个日志表查询。
            
        -   **按分区拆分：**hash,range等方式。不建议，因为数据其实难以实现水平扩展。
            
4.  **sharding\_key（分表字段）选择：**尽量选择查询频率最高的字段，然后根据表拆分方式选择字段。
    
5.  **代码改造：**修改代码里的查询、更新语句，以便让其适应分库分表后的情况。
    
6.  **数据迁移：**最简单的就是停机迁移，复杂点的就是不停机迁移，要考虑增量同步和全量同步的问题。
    
    1.  **全量同步：**老库到新库的数据迁移，要控制好迁移效率，解决增量数据的一致性。
        
        1.  **定时任务：**定时任务查老库写新库
        2.  **中间件：**使用中间件迁移数据
    2.  **增量同步：**老库迁移到新库期间，新增删改命令的落库不能出错
        
        1.  **同步双写：**同步写新库和老库；
        2.  **异步双写（推荐）：** 写老库，监听binlog异步同步到新库
        3.  **中间件同步工具：**通过一定的规则将数据同步到目标库表
7.  **数据一致性校验和补偿：**假设采用异步双写方案，在迁移完成后，逐条对比新老库数据，**一致则跳过，不一致则补偿：**
    
    1.  新库存在，老库不存在：新库删除数据
    2.  新库不存在，老库存在：新库插入数据
    3.  新库存在、老库存在：比较所有字段，不一致则将新库更新为老库数据
8.  **灰度切读：**灰度发布指黑（旧版本）与白（新版本）之间，让一些用户继续用旧版本，一些用户开始用新版本，如果用户对新版本没什么意见，就逐步把所有用户迁移到新版本，实现平滑过渡发布。**原则：**
    
    1.  有问题及时切回老库
    2.  灰度放量先慢后快，每次放量观察一段时间
    3.  支持灵活的规则：门店维度灰度、百 (万)分比灰度
9.  **停老用新：**下线老库，用新库读写。
    

### **3.2 表设计优化**

#### **3.2.1 混合业务分表、冷热数据分表**

**混合业务分表：**

根据业务逻辑，将不同的业务数据分开存储在不同的表中。每个业务模块的数据单独存储，减少了单表的大小和查询的复杂度。

-   **示例：**将一个大的日志表，拆分成交易日志表、操作日志表、登录日志表等等。这些需要在项目设计期间就根据预估的数据量进行拆分。

**冷热数据分表：**

将频繁访问的“热数据”和不常访问的“冷数据”分开存储。这种策略有助于提高热数据的查询性能，并且在存储和备份方面更加灵活。

-   **示例1：**把一个大的任务表，分离成任务表和历史任务表，任务表里任务完成后移动到历史任务表。任务表是热数据，历史任务表是冷数据，提高查询性能。
-   **示例2：**或者将日志表分成日志表和历史日志表，使用定时任务将三个月前的日志都迁移到历史日志表，用户查看操作记录时，默认只显示近三个月的数据，从而提高性能。

#### **3.2.2 联合查询改为中间关系表**

对于复杂的数据库设计，使用关系表是一种常见的方法，特别是在多对多的关系中，例如学生表和课程表、商品表和商品属性表、用户和角色表、作者和书籍表、部门和人员表。

**示例：** 

**部门表 (departments)**：

-   department\_id：部门ID（主键）
-   department\_name：部门名称

**人员表 (employees)**：

-   employee\_id：员工ID（主键）
-   employee\_name：员工名称

**部门员工关联表 (department\_employees)**：

-   id：主键ID
-   department\_id：部门ID（外键，指向 departments 表）
-   employee\_id：员工ID（外键，指向 employees 表）

**关系表的优点：**

-   **多对多关系：**通过中间表可以管理多对多的映射关系。
-   **支持扩展：**关系表可以添加额外的字段来描述关系的属性。
-   **提高查询性能：**减少表连接的次数，提高查询性能。

#### **3.2.3 遵循三个范式**

**数据库三范式：**

-   每个属性不可再分
-   表必须有且只有一个主键
-   非主键列必须直接依赖于主键

#### **3.2.4 字段建议非空约束**

①可能查询出现空指针问题；

②导致聚合函数不准确，因为它会忽略null

③不能用“=”判断，只能用is null判断；

④null和其他值运算只能是null，可能让你不小心把它当成0；

⑤null值比空字符更占用空间，空值长度是0，null长度是1bit；

⑥不覆盖索引情况下，is not null无法用索引

#### **3.2.5 反范式：使用冗余字段**

**反范式：**为提高查询效率，可添加不常更新的字段为冗余字段。

反范式化是数据库设计的一种策略，通过在设计中引入冗余数据来提高查询性能，简化查询操作，或满足其他业务需求。

**使用场景：**

将多读少写的字段，增加为冗余字段，从而不再需要每次都连表查询这个字段。需要注意每次数据更新时必须同步这个冗余字段。

**示例：**

**部门表 (departments)：**

-   department\_id：部门ID（主键）
-   department\_name：部门名称

**人员表 (employees)**：

-   employee\_id：员工ID（主键）
-   employee\_name：员工名称

**部门员工关联表 (department\_employees)**：

-   id：主键ID
-   department\_id：部门ID（指向 departments 表）
-   employee\_id：员工ID（指向 employees 表）

> **注意：**
> 
> 增加冗余字段后，当这个冗余字段对应的数据改动后，必须同步更改这个冗余字段。
> 
> 例如成绩表除了有student\_id字段外，增加冗余字段student\_name，因为学生名基本不会变化，但在修改姓名的接口里，修改学生名后要同步修改成绩表的student\_name字段。

#### **3.2.6 数据类型优化**

**整数类型：**

考虑好数值范围，前期可以使用int保证稳定性。非负数类型要用UNSIGNED；同样字节数，存储的数值范围更大。主键一般使用bigint,布尔类型tinint

**能整数就不要用文本类型：**

跟文本类型数据相比，大整数往往占用更少的存储空间。

**避免使用TEXT、BLOB数据类：**

这两个大数据类型，排序时不能使用临时内存表，只能使用磁盘临时表，效率很差，建议别用，或分表到单独扩展表里。LongBlob类型能存储4G文件；

**避免使用枚举类型：**

因为枚举类型排序很慢。

**使用TIMESTAMP存储时间：**

TIMESTAMP使用4字节，DATETIME使用8个字节，同时TIMESTAMP具有自动赋值以及自动更新的特性。 缺点是只能存到2038年，MySQL5.6.4版本可以参数配置，自动修改它为BIGINT类型。

**DECIMAL存浮点数：**

Decimal类型为精准浮点数，在计算时不会丢失精度，尤其是财务相关的金融类数据。占用空间由定义的宽度决定，每4个字节可以存储9位数字，并且小数点要占用一个字节。可用于存储比bigint更大的整型数据。 

### **3.3 索引优化**

#### 3.3.0 数据准备

##### 3.3.0.1 创建学生表并生成50w条数据

> **本文使用MySQL版本：**
> 
> 5.7.41

学员表插 50万 条，班级表 插 1万 条。

**步骤0：建库** 

```sql
CREATE DATABASE test;
USE test;
```

**步骤1：建表**

```sql
CREATE TABLE `class` (
    `id` INT(11) NOT NULL AUTO_INCREMENT,
    `className` VARCHAR(30) DEFAULT NULL,
    `address` VARCHAR(40) DEFAULT NULL,
    `monitor` INT NULL ,
    PRIMARY KEY (`id`)
) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;

CREATE TABLE `student` (
    `id` INT(11) NOT NULL AUTO_INCREMENT,
    `stuno` INT NOT NULL ,
    `name` VARCHAR(20) DEFAULT NULL,
    `age` INT(3) DEFAULT NULL,
    `classId` INT(11) DEFAULT NULL,
    PRIMARY KEY (`id`)
    #CONSTRAINT `fk_class_id` FOREIGN KEY (`classId`) REFERENCES `t_class` (`id`)
) ENGINE=INNODB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```

**步骤2：设置参数**

-   命令开启：允许创建函数设置：

```sql
set global log_bin_trust_function_creators=1; # 不加global只是当前窗口有效。
```

**步骤3：创建函数**

保证每条数据都不同。

```sql
DELIMITER //

CREATE FUNCTION rand_string(n INT) RETURNS VARCHAR(255)
DETERMINISTIC
NO SQL
BEGIN
    DECLARE chars_str VARCHAR(100) DEFAULT 'abcdefghijklmnopqrstuvwxyzABCDEFJHIJKLMNOPQRSTUVWXYZ';
    DECLARE return_str VARCHAR(255) DEFAULT '';
    DECLARE i INT DEFAULT 0;
    WHILE i < n DO
        SET return_str = CONCAT(return_str,SUBSTRING(chars_str,FLOOR(1+RAND()*52),1));
        SET i = i + 1;
    END WHILE;
    RETURN return_str;
END //

DELIMITER ;
```

随机产生班级编号

```sql
DELIMITER //

CREATE FUNCTION rand_num (from_num INT ,to_num INT) RETURNS INT(11)
DETERMINISTIC
NO SQL
BEGIN
    DECLARE i INT DEFAULT 0;
    SET i = FLOOR(from_num +RAND()*(to_num - from_num+1)) ;
    RETURN i;
END //

DELIMITER ;
```

**步骤4：创建存储过程**

```sql
#创建往stu表中插入数据的存储过程
DELIMITER //
CREATE PROCEDURE insert_stu( START INT , max_num INT )
BEGIN
DECLARE i INT DEFAULT 0;
SET autocommit = 0; #设置手动提交事务
REPEAT #循环
SET i = i + 1; #赋值
INSERT INTO student (stuno, name ,age ,classId ) VALUES
((START+i),rand_string(6),rand_num(1,50),rand_num(1,1000));
UNTIL i = max_num
END REPEAT;
COMMIT; #提交事务
END //
DELIMITER ;
#假如要删除
#drop PROCEDURE insert_stu;
```

创建往class表中插入数据的存储过程

```sql
#执行存储过程，往class表添加随机数据
DELIMITER //
CREATE PROCEDURE `insert_class`( max_num INT )
BEGIN
DECLARE i INT DEFAULT 0;
SET autocommit = 0;
REPEAT
SET i = i + 1;
INSERT INTO class ( classname,address,monitor ) VALUES
(rand_string(8),rand_string(10),rand_num(1,100000));
UNTIL i = max_num
END REPEAT;
COMMIT;
END //
DELIMITER ;
#假如要删除
#drop PROCEDURE insert_class;
```

**步骤5：调用存储过程**

class

```sql
#执行存储过程，往class表添加1万条数据
CALL insert_class(10000);
```

stu

```sql
#执行存储过程，往stu表添加50万条数据
CALL insert_stu(100000,500000);
```

##### 3.3.0.2 创建删除所有索引的存储过程

创建删除索引的存储过程

```sql
DELIMITER //
CREATE PROCEDURE `proc_drop_index`(dbname VARCHAR(200),tablename VARCHAR(200))
BEGIN
        DECLARE done INT DEFAULT 0;
        DECLARE ct INT DEFAULT 0;
        DECLARE _index VARCHAR(200) DEFAULT '';
        DECLARE _cur CURSOR FOR SELECT index_name FROM
information_schema.STATISTICS WHERE table_schema=dbname AND table_name=tablename AND
seq_in_index=1 AND index_name <>'PRIMARY' ;
#每个游标必须使用不同的declare continue handler for not found set done=1来控制游标的结束
        DECLARE CONTINUE HANDLER FOR NOT FOUND set done=2 ;
#若没有数据返回,程序继续,并将变量done设为2
        OPEN _cur;
        FETCH _cur INTO _index;
        WHILE _index<>'' DO
            SET @str = CONCAT("drop index " , _index , " on " , tablename );
            PREPARE sql_str FROM @str ;
            EXECUTE sql_str;
            DEALLOCATE PREPARE sql_str;
            SET _index='';
            FETCH _cur INTO _index;
        END WHILE;
    CLOSE _cur;
END //
DELIMITER ;
```

执行存储过程

```sql
CALL proc_drop_index("数据库名","表名");
```

> **练习：**删除student表的所有索引：
> 
> ```
> CALL proc_drop_index("test","student");
> ```
> 
> **验证：**
> 
> 创建索引：
> 
> ```
> CREATE INDEX idx_stuno_age on student(stuno,age);
> 
> ```
> 
> 查看索引：
> 
> ```
> SHOW INDEX FROM student;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/adda26cb5961a4d1190f7a88c8a7338b.png)
> 
> 删除所有索引：
> 
> ```
> CALL proc_drop_index("test","student");
> ```
> 
> 再次查看索引：
> 
> ```
> SHOW INDEX FROM student;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/b671c880361962a3de220c88c42de684.png)

#### **3.3.1 考虑索引失效的11个场景**

> **详细请参考：**
> 
> [MySQL高级篇——索引失效的11种情况\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130779528 "MySQL高级篇——索引失效的11种情况_vincewm的博客-CSDN博客")

##### **3.3.1.1.尽量全值匹配**

全值匹配指的是查询条件完全匹配索引中的所有列。例如，如果一个索引包含列 `A` 和 `B`，那么查询条件应该包括这两个列才能完全匹配这个索引。

查询age and classId and name时，(age,classId,name)索引比(age,classId)快。

> **验证：**
> 
> 创建联合索引
> 
> ```sql
> CREATE INDEX idx_stuno_age on student(stuno,age);
> ```
> 
> 全值匹配：
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno=1 and age=2;
> ```
> 
> 可以看到type是ref，即命中非唯一索引。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/e04cdc5225804e2c37f70565894ef96f.png)

##### **3.3.1.2.考虑最左前缀**

联合索引把频繁查询的列放左。例如索引（a,b,c），只能查(a,b,c),(a,b),(a)。

> **验证：**
> 
> 保持创建上面idx\_stuno\_age联合索引
> 
> 没符合最佳左前缀原则：
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE age=2;
> ```
> 
> 可以看到type是all，即全表扫描。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/fab47e3b164f6005ab53e61b27a64e99.png)

##### **3.3.1.3.主键尽量有序**

如果主键不有序，需要查找目标位置再插入，并且如果目标位置所在数据页满了就必须得分裂页，造成性能损耗。可以选择自增策略或MySQL8.0有序UUID策略。

##### **3.3.1.4.计算、函数导致索引失效**

**计算：**

当对索引列进行计算时，MySQL 不能使用索引。因为索引存储的是列的原始值，而计算改变了这些值。

> **验证：**
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno+1=2
> ```
> 
> 可以看到type是all，全表扫描，没有走索引。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8d6e5bb6e96bb4c9b174469580afe2d7.png)

> 如果是等号右边的计算，则索引不受影响，依然生效，因为这个计算预先就能计算得出：
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno=2+1
> ```
> 
>  可以看出type是ref，命中非唯一索引：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3f7369e85724f2ed9419c87415aa0dab.png)

**函数：**

在索引列上使用函数会导致索引失效，因为 MySQL 不能预先计算索引列的函数值并存储在索引中。

>  **验证：**
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE abs(stuno)=3
> ```
> 
> 可以看到type是all，全表扫描，没有走索引。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8d6e5bb6e96bb4c9b174469580afe2d7.png)

> 如果是等号右边的函数，则索引不受影响，依然生效，因为这个计算预先就能计算得出：
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno=abs(2.3)
> ```
> 
>  可以看出type是ref，命中非唯一索引：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3f7369e85724f2ed9419c87415aa0dab.png)

##### **3.3.1.5.类型转换导致索引失效**

**隐式转换导致索引失效：**

当查询条件中的数据类型与索引列的数据类型不匹配时，MySQL 会进行隐式类型转换。这种类型转换会导致 MySQL 无法利用索引，从而导致全表扫描，影响查询性能。

使用不同字符集时，也会触发类型隐式转换，导致索引失效。

**注意：**MySQL官方文档有提到：

> In all other cases, the arguments are compared as floating-point (double-precision) numbers. For example, a comparison of string and numeric operands takes place as a comparison of floating-point numbers.

也就是说，对比的时候，MySQL 自身会有一套基本的规则来对应不同类型数据的比较，而字符串与数字的对比中，字符串会被转换成双精度浮点型数字之后再进行对比。

例如name=123，而不是name='123'，则会导致索引失效。

而stuno='12abc3'，而不是stuno=123，则并不会导致索引失效。

> 验证：
> 
> 保持创建索引idx\_stuno\_age、idx\_name
> 
> ```
> EXPLAIN SELECT * FROM student WHERE name = '123';
> ```
> 
> 可以看到type是ref，这是走索引的。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/ccb02700083fc675fe13d5eb0e5bdd7c.png)
> 
> 而下面触发类型隐式转换，type是all，全表扫描，没有走索引（虽然字符串可以转数字，但数字不能转字符串，会导致索引失效）：
> 
> ```
> EXPLAIN SELECT * FROM student WHERE name = 123;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/78b3e560efd520c8c0dd569fa26877c4.png)

**显式转换导致索引失效：**

显式类型转换是指在查询条件中使用 CAST 或 CONVERT 函数将数据类型转换为匹配索引列的数据类型。这种方式同样会导致索引失效。

> **验证：**
> 
> 给name字段创建索引：
> 
> ```
> CREATE INDEX idx_name on student(name);
> ```
> 
> 正常查询name会走索引，type是ref，命中非唯一索引：
> 
> ```
> EXPLAIN SELECT * FROM student WHERE name = '123';
> ```
> 
> 将name类型转换成char，type是all，全表扫描：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/4abde307b0aee04fde3f6b7316c9a560.png)

##### **3.3.1.6.没索引下推时，范围条件右边的列索引失效**

当查询条件使用了范围条件（例如 >、<、>=、<=、BETWEEN）时，会导致索引右边的列失效，因为范围查询会阻止 MySQL 使用复合索引的后续列。 

**例如：**（a,b,c）联合索引，查询条件a,b,c，如果b使用了范围查询，那么b右边的c索引失效。所以建议把需要范围查询的字段放在最后。

**索引下推：**

索引下推(ICP，Index Condition Pushdown)是MySQL 5.6中新特性，是一种在存储引擎层使用索引过滤数据的一种优化方式。它可以**使范围查询右侧索引失效的列，依然可以在索引树上过滤，而不需要回表。**

如果开启了索引下推，范围条件右边的列实际上是索引失效的，但是可以直接在这颗联合索引树上直接过滤右边的这些字段。

**例如：**索引(name,age)，查询name like 'z%' and age and address，'z%'是模糊查询，实际上也是范围查询。使用索引下推时，在联合索引树查询时不止查name，还会判断后面的age。而如果关闭了索引下推，联合索引里范围查询后面的字段age不能在联合索引树里直接条件判断，必须回表到主键索引树后，以之前过滤结果id查找到对应数据，再过滤age列。

> **注意：**这里举例没有使用'%z'，因为左模糊查询会使整个索引失效，也就不会用到索引下推了。

> **验证：**
> 
> 继续使用idx\_stuno\_age索引
> 
> **关闭索引下推，范围查询右侧的列索引失效：**
> 
> ```sql
> SET optimizer_switch='index_condition_pushdown=off';
> EXPLAIN SELECT * FROM student WHERE stuno > 123 and stuno<129 and age=2;
> ```
> 
> 可以看到，type是range，即范围查询，extra是using where，即用到了回表，age字段是根据name过滤结果的id，回表到主键索引数过滤的：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/0e0ec6f66d1f0ad0e4ac51c1b39ac9a6.png)
> 
> **打开索引下推，范围查询右侧的列依然在索引树过滤：**
> 
> ```sql
> SET optimizer_switch='index_condition_pushdown=on';
> EXPLAIN SELECT * FROM student WHERE stuno > 123 and stuno<129 and age=2;
> ```
> 
> 对age字段使用范围查询，发现type是range，即命中范围查询，extra是using index condition，即使用了索引下推。因为age在联合索引里，所以直接在联合索引所在的非聚簇索引树中即可完成过滤 age=2，而不需要回表：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/79216d0c96ab74496ff94c626728f98f.png)
> 
> **tip：范围查询过滤量过小时，查询优化器连范围索引也不用：**
> 
> 对stuno使用范围查询stuno>123，发现type是all，即全表扫描。因为stuno>123的记录有50w条，索引直接全表扫描。：
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno > 123 and stuno<129 and age=2;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/07aae7ca4ffe0e24d8658e2e3c2a1c86.png)

##### **3.3.1.7.没覆盖索引时，“不等于”导致索引失效**

因为“不等于”不能精准匹配，全表扫描二级索引树再回表效率不如直接全表扫描聚簇索引树。但使用覆盖索引时，联合索引数据量小，加载到内存所需空间比聚簇索引树小，且不需要回表（因为直接在非聚簇索引树全表扫描，比在聚簇索引树全表扫描要快），索引效率优于全表扫描聚簇索引树。

**覆盖索引：**一个索引包含了满足查询结果的数据就叫做覆盖索引，不需要回表等操作。

> **聚簇索引和非聚簇索引：**
> 
> [MySQL高级篇——存储引擎和索引\_mysql存储索引的表-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130308116 "MySQL高级篇——存储引擎和索引_mysql存储索引的表-CSDN博客")

> **验证：**
> 
> 没覆盖索引，不等于导致索引失效：
> 
> ```
> EXPLAIN SELECT * FROM student WHERE stuno <>3;
> ```
> 
> type是all，全表扫描
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/22bd7f39a9be8e01f30ca39f1aa333e8.png)
> 
> 有覆盖索引，即使不等于，索引依然生效，因为只查这两个字段，直接在联合索引树上全表扫描，肯定比在主键索引树上全表扫描快。
> 
> ```
> EXPLAIN SELECT stuno FROM student WHERE stuno <>3;
> ```
> 
> type是range，即范围查询，extra是using index，即用到了覆盖索引，extra又是using where，即因为不等于导致索引失效，所以在联合索引树上进行了全表扫描：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8246a6f9e9935bc636a5512d73ff0d09.png)
> 
> 覆盖索引+走索引：
> 
> ```
> EXPLAIN SELECT stuno FROM student WHERE stuno =3;
> ```
> 
> type是ref，命中非唯一索引，extra是using index，即使用了覆盖索引
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/24f2745fbdd871cfee4ea3388a05c6a5.png)

##### **3.3.1.8.没覆盖索引时，左模糊查询导致索引失效**

因为“左模糊查询”不能精准匹配，全表扫描二级索引树再回表效率不如直接全表扫描聚簇索引树。但使用覆盖索引时，联合索引数据量小，加载到内存所需空间比聚簇索引树小，且不需要回表（因为直接在非聚簇索引树全表扫描，比在聚簇索引树全表扫描要快），索引效率优于全表扫描聚簇索引树。

**覆盖索引：**一个索引包含了满足查询结果的数据就叫做覆盖索引，不需要回表等操作。

例如LIKE '%abc'。因为字符串开头都不能精准匹配。

> **验证：**
> 
> 跟上面范围查询导致索引失效同理，此处不再赘述。

##### **3.3.1.9.没覆盖索引时，is not null、not like无法使用索引**

因为“is not null、not like”不能精准匹配，全表扫描二级索引树再回表效率不如直接全表扫描聚簇索引树。但使用覆盖索引时，联合索引数据量小，加载到内存所需空间比聚簇索引树小，且不需要回表（因为直接在非聚簇索引树全表扫描，比在聚簇索引树全表扫描要快），索引效率优于全表扫描聚簇索引树。

**覆盖索引：**一个索引包含了满足查询结果的数据就叫做覆盖索引，不需要回表等操作。

> **验证：**
> 
> 跟上面范围查询导致索引失效同理，此处不再赘述。

##### **3.3.1.10.“OR”前后存在非索引列或不同索引列，导致索引失效**

or前后是不同索引列时，整个语句的索引失效。例如a=x or b=x

or前后是同一索引列时，命中范围索引。例如a=x or a=xx

or前后是不同或相同的非索引列时，索引失效。例如联合索引（a,b）,查询a=x and (c=x or c=xx)

> **验证：**
> 
> 清除并重新创建索引：
> 
> ```
> CALL proc_drop_index("test","student");
> CREATE INDEX idx_stuno_age_classid on student(stuno,age,classid);
> ```
> 
> **or前后是不同列时，索引就一定会失效：**
> 
> ```
> EXPLAIN SELECT * FROM student WHERE stuno =3 and age=2 or classid=3
> ```
> 
> 可以看到type是all，全表扫描，即使stuno和age都在联合索引树的前两级：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/cc3bc82d2f676ec3c1ef69267304c64a.png)
> 
> **or前后是同一列时，命中范围索引：**
> 
> ```
> EXPLAIN SELECT * FROM student WHERE stuno =3 or stuno=2 and age=3;
> ```
> 
> type是range，extra是索引下推。索引下推就是把stuno=3和stuno=2，两个条件其中一个条件在联合索引树上走索引判断，另一个条件在此树的过滤结果基础上再过滤，而不需要在MySQL服务器上再回表过滤。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/7beafe45355e317793ae666d938e73b4.png)
> 
> **or前后是同一列时，命中范围索引，它后面的列依然在联合索引树上判断：**
> 
> ```
> EXPLAIN SELECT * FROM student WHERE stuno =3 or stuno=2 and age=3;
> ```
> 
> key\_len是9，说明age也继续在联合索引树上走索引：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bcdc3f30f768194b296c7ecf10625dc6.png)
> 
> **or前后是非索引列，索引失效：**
> 
> ```
> EXPLAIN SELECT * FROM student WHERE name ='3' or name='3';
> ```
> 
> 可以看到全表扫描：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/d53bc71e41b73bb6ff798991ccc1cc62.png)

##### **3.3.1.11.不同字符集导致索引失败**

建议utf8mb4，不同的字符集进行比较前需要进行 转换 会造成索引失效。 

> 例如创建表时给不同字段设置不同字符集，再判断这些字段时会导致索引失效：  
> 例如下面表，给name\_utf8和name\_latin1创建联合索引，再where name\_utf8=name\_latin1时会导致索引失效：
> 
> ```sql
> CREATE TABLE student2 (
>   id INT(11) NOT NULL AUTO_INCREMENT,
>   name_utf8 VARCHAR(20) CHARACTER SET utf8 DEFAULT NULL,
>   name_latin1 VARCHAR(20) CHARACTER SET latin1 DEFAULT NULL,
> ) ENGINE=InnoDB;
> ```

#### **3.3.2 遵循索引设计原则**

>  **详细请参考：**
> 
> [MySQL高级篇——索引的创建与设计原则\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130352271 "MySQL高级篇——索引的创建与设计原则_vincewm的博客-CSDN博客")

1.   **命名：**索引的字段个数尽量别超过5个，命名格式“idx\_col1\_col2”
2.  在频繁查询（特别是分组、范围、排序查询）的列建立索引；
3.  频繁更新的表，不要创建过多索引
4.  唯一特性的字段，适合创建索引；
5.  很长的varchar字段，适合根据区分度和长度创建前缀索引；
6.  多个字段都要创建索引时，联合索引优于单值索引；
7.  避免创建过多索引，避免索引失效；
8.  **尽量用有序的字段作为主键索引：**防止乱序时新主键前移到已满的数据页，导致插入后分裂数据页，造成性能损耗； 

#### **3.3.3 连接查询优化**

> **详细请参考：**
> 
> [MySQL高级篇——索引失效的11种情况\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130779528 "MySQL高级篇——索引失效的11种情况_vincewm的博客-CSDN博客")

##### **3.3.3.1 被驱动表连接字段加索引**

外连接查询时，右表就是被驱动表，建议加索引。

**原因：**因为MySQL连接查询底层是先查过滤条件下的左表，按左表查询的结果，再以**连接字段**作为条件查询结果，所以右表的连接字段加索引，将极大地提高查询性能。

> **驱动表与被驱动表：**
> 
> -   **驱动表：**在连接操作中，驱动表是首先被读取的表。MySQL会从驱动表中读取数据行，然后在被驱动表中寻找匹配的行。
> -   **被驱动表：**被驱动表是连接操作中第二个被读取的表。对于驱动表中的每一行，MySQL会在被驱动表中寻找匹配的行。

> **验证：**
> 
> **被驱动表连接字段没索引：**
> 
> 下面SQL驱动表是班级表，被驱动表是学生表，学生表的连接字段classId没有创建索引，所以查询性能不如上面的SQL：
> 
> ```sql
> EXPLAIN SELECT * FROM class c LEFT JOIN student s on c.id=s.classId;
> ```
> 
> 这个连接查询相当于先查驱动表班级表，再查被驱动表学生表。两个type都是all，被驱动表学生表的条件是连接字段classId，这个字段没有加索引，所以type是all。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bf2ae9a1939ad6a59046cdcba0b04e01.png)
> 
> 查询时长：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/a109c5e10858754cd54e7e5623e85bcc.png)
> 
> **被驱动表连接字段有索引：**
> 
> 创建索引并分析：
> 
> ```sql
> -- 因为被驱动表连接字段是classid，所以给他创建索引
> CREATE INDEX idx_classid on student(classid);
> EXPLAIN SELECT * FROM class c LEFT JOIN student s on c.id=s.classId;
> ```
> 
> 我们可以看到，被驱动表学生表走了索引，type是ref，即命中非唯一索引。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/cc12622c8a1d3611a2acb89010195010.png)
> 
> 查询时长：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/864a6db2460be61e7ed82b8d0e8ec1d8.png)
> 
> **结论：**可以看到，查询时长**从180秒优化到了0.6秒**。被驱动表的连接字段，加索引和不加索引，性能区别还是很大的。
> 
> **注意：**我这里被驱动表用的是学生表，而不是班级表，因为如果用班级表作为被驱动表，连接字段将成为被驱动表的id，id主键默认加唯一索引，不方便验证。

##### **3.3.3.2 小表驱动大表**

在MySQL连接查询时，建议用小表驱动大表，即“小表 left join 大表”，或者“小表 right join 大表”。

**小表驱动大表是为了减少连接次数：**

因为同样两张表相互连接，小表驱动大表，可以有效减少连接的次数。上一节有说过，连接查询的原理是先查左表，再根据连接字段查右表，然后过滤右表的条件。因为相比普通的查询，连接查询要左表右表都查一次，肯定没有只查一次快，所以连接次数越少越好，所以要用小表驱动大表。

**连接次数验证：**

现有两个表A与B ，表A有200条数据，表B有20万条数据 ;  
按照循环的概念举个例子

-   小表驱动大表 > A驱动表，B被驱动表：连接次数200次。

```java
 for(200条){
   for(20万条){
     ...
   }
 }
```

-   大表驱动小表 > B驱动表，A被驱动表：连接次数20万次。

```java
 for(20万){
   for(200条){
    ...
   }
 }
```

**所以：**

-   如果小的循环在外层，对于表连接来说就只连接200次 ;
-   如果大的循环在外层，则需要进行20万次表连接，从而浪费资源，增加消耗 ;

> **验证-不加索引（学生表50w数据，班级表1w数据）：**
> 
> **先清除所有索引：**
> 
> 为了防止索引带来的影响，先去掉所有索引：
> 
> ```sql
> CALL proc_drop_index("test","student");
> ```
> 
> **大表驱动小表：**
> 
> 为了避免主键唯一索引对结果的影响，我们连接字段不使用id，而使用classId和monitor。
> 
> 下面SQL驱动表是学生表，被驱动表是班级表，连接字段是班级表的monitor。
> 
> 学生比班级多，符合大表驱动小表：
> 
> ```sql
> SELECT * FROM student s LEFT JOIN class c on s.classId=c.monitor;
> ```
> 
> 可以看到查询时长是206s。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/a908d01975a675a1b93e05d40cf595be.png)
> 
> **小表驱动大表：**即班级表驱动学生表
> 
> ```sql
> SELECT * FROM class c LEFT JOIN student s on s.classId=c.monitor;
> ```
> 
> 可以看到查询时长只有189s：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/ea3cb2985b80b4ee9189ae27ae6790c2.png)
> 
> **结论：**可以看出使用小表驱动大表后，查询时长缩短了16s。

> **验证-加索引：** 
> 
> ```sql
> CREATE INDEX idx_classid on student(classid);
> CREATE INDEX idx_monitor on class(monitor);
> ```
> 
> **大表驱动小表：**学生比班级多，符合大表驱动小表
> 
> ```sql
> SELECT * FROM student s LEFT JOIN class c on s.classId=c.monitor;
> ```
> 
> 查询时长：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/226e766c1d0eae45833fd9859915b9e3.png)
> 
> **小表驱动大表：**即班级表驱动学生表
> 
> ```sql
> SELECT * FROM class c LEFT JOIN student s on s.classId=c.monitor;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/600ea76c0c8bbec51126de04769afca4.png)
> 
> **结论：**可以看出使用小表驱动大表后，查询时长由0.6s优化到了0.2s

##### **3.3.3.3 两表连接字段类型必须一致**

两个表JOIN字段数据类型保持绝对一致。防止MySQL查询优化器隐式的自动类型转换导致索引失效。

索引失效上面3.3.1.5有详细说，此处不再赘述。

> **验证：**
> 
> ```sql
> -- 修改classId 字段类型
> ALTER TABLE student MODIFY COLUMN classId VARCHAR(255);
> -- 删除所有索引
> CALL proc_drop_index("test","student");
> -- 创建classId 字段索引
> CREATE INDEX idx_classid on student(classid);
> ```
> 
> 学生表的classid字段设置成varchar类型，而班级表的id是int类型，再使用下面SQL将这两个字段连接起来，就会导致索引失效。
> 
> ```sql
> EXPLAIN SELECT * FROM class c LEFT JOIN student s on s.classId=c.monitor;
> ```
> 
>  可以看到被驱动表学生表的查询计划中，type是all，即全表扫描，索引失效了：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3a91b7b8a1d451e8ee685958fd1f0f78.png)
> 
> **结论：**连接查询时，两个表的连接字段必须保持类型一致。
> 
> 然后我们把classid字段类型改回来：
> 
> ```sql
> ALTER TABLE student MODIFY COLUMN classId INT;
> ```

#### **3.3.4 子查询优化**

> **详细请参考：**
> 
> [MySQL高级篇——索引失效的11种情况\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130779528 "MySQL高级篇——索引失效的11种情况_vincewm的博客-CSDN博客")

**优化方案：**

##### **3.3.4.1.子查询优化成关联查询**

-   **性能：**
    -   在数据量小、过滤条件简单时，子查询效率高一点；在数据量大、过滤条件复杂时，关联查询效率高很多。综合考虑，建议使用关联查询。
    -   **子查询的缺点：**
        -   **嵌套查询：**子查询可能导致嵌套查询，一个子查询套另一个子查询，又套另一个子查询，这会增加查询的复杂性并降低性能。
        -   **数据重复检索：**子查询可能需要对数据进行多次检索，尤其是在相关子查询中。而连接则允许数据库一次性检索所有需要的数据，从而减少I/O操作和计算开销。
-   **语义清晰度**：还是建议使用关联查询，阅读起来更直白、明确，层次结构清晰，后期维护成本也越低，查询次数也一般更低一些。

> **子查询原理：**
> 
> 子查询是指在一个SQL语句中嵌套另一个完整的SQL查询。它可以作为主查询的一部分，也可以作为WHERE、FROM或HAVING子句的一部分。子查询的执行顺序是先执行子查询，然后将其结果作为外部查询的条件或数据源。

> **注意**：
> 
> 如果见到**子查询+范围查询**的SQL，要直接进行优化，我曾经优化过一个慢SQL，将其由子查询优化成关联查询，时间从4.5s缩减成了0.2s：
> 
> **优化前**：例如查询每个学生的出生地：
> 
> ```sql
> SELECT
> 	id,
> 	fullname,
> 	birth_city 
> FROM
> 	person 
> WHERE
> 	id IN (
> 		SELECT  person_id  
> FROM
> 	student)
> ```
> 
>  **优化后**：
> 
> ```sql
> SELECT
> 	id,
> 	fullname,
> 	birth_city 
> FROM
> 	person p
> 	LEFT JOIN student s ON p.id = s.person_id
> ```
> 
> 因为范围查询会使索引失效，再加上使用子查询，优化前的SQL性能是很慢的。
> 
> **实际场景**：
> 
> ![](https://i-blog.csdnimg.cn/direct/eaaf1b18b0fa4a27aa750e9625c2d62a.png)
> 
> ![](https://i-blog.csdnimg.cn/direct/0064cac969c14457a55ee004c16a78b6.png)

> **验证：子查询比关联查询快的场景**
> 
> 查询所有班长的学号、姓名
> 
> 关联查询：
> 
> ```sql
> SELECT DISTINCT s.* from class c LEFT JOIN student s on c.monitor=s.id;
> ```
> 
>  查询时长：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8eb335033a9ce43ccb6b759d115f6e2f.png)
> 
> 子查询：
> 
> ```sql
>  SELECT * FROM student WHERE id in (SELECT DISTINCT monitor FROM class)
> ```
> 
> 查询时长：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/e516e421e3c73de244d7b0c883cadf67.png)
> 
> **验证：子查询比关联查询慢的场景**
> 
> 查询所有学生及其对应的班级名称
> 
> 关联查询：
> 
> ```sql
> SELECT s.name, c.address
> FROM student s
> JOIN class c ON s.classId = c.id;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/e95fe02715c6297a8532604612211f3f.png)
> 
> 子查询：
> 
> ```sql
> SELECT name, 
>                (SELECT address FROM class WHERE id = s.classId) AS address
> FROM student s;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/fd12b64dfb2b74f125c1e9199e158b49.png)

##### **3.3.4.2.多次查询代替子查询**

在复杂SQL中，同一个子查询语句可能在整个SQL中多次出现，这就导致了性能浪费。这种情况下，结合Java代码多次查询而不用子查询，可以使这个重复子查询语句只查一次，从而提高性能。

> 通常情况下，我们可能想，多次查询肯定没有一次查询，因为MySQL查询两次肯定就有两次I/O调用过程，而查询一次也就只有一次调用过程。
> 
> 但其实还是需要具体情况具体分析，如果是简单SQL，只调用了一次子查询，那肯定是子查询快，当同一个子查询语句可能在整个SQL中多次出现时，用Java代码，肯定是更快的，虽然IO次数多，但这么多次子查询缩减成了一次，性能是快了的。
> 
> 这也是日常开发中的一个原则，任何性能优化都需要看具体的业务场景。

##### **3.3.4.3.临时表代替子查询**

如果一个复杂SQL中，多次用到了同一个子查询，可以尝试将其抽离出来，优化成临时表。这样可以避免重复计算、减少查询次数，从而提高查询性能。

并且可维护性也有效提高，每次修改时只需要修改这一个临时表，而不需要手动一个个修改子查询语句。

#### **3.3.5 排序优化**

> 详细请参考：
> 
> [MySQL高级篇——排序、分组、分页优化\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130790354 "MySQL高级篇——排序、分组、分页优化_vincewm的博客-CSDN博客")

##### **3.3.5.1 合理选择索引排序和FileSort排序**

**结论：**

-   查询优化器会自动选择索引排序和FileSort排序；
-   索引排序一般更快；
-   在一些索引失效的情况下，FileSort可能效率更高；

> MySQL支持索引排序和FileSort排序，索引保证记录有序性，性能高，推荐使用。
> 
> FileSort排序是内存中排序，当数据量大时，查询优化器会产生临时文件，在磁盘里对数据排序。我们知道，磁盘的IO速度是远低于内存的，所以它的性能一般不如索引排序，而且排序过程中会**占用大量CPU**。
> 
> 当然，任何事不是绝对的，一些情况FileSort可能效率高。例如没覆盖索引的左模糊、“不等于”、not null等索引失效情况下，全表扫描效率比非聚簇索引树遍历再回表更高。
> 
> **创建索引：**
> 
> ```sql
> CREATE INDEX idx_name on student(name);
> ```
> 
> **验证：索引失效时FileSort更快**
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE name like '%34' order by name;
> ```
> 
> 可以看到type是all，全表扫描，extra是using filesort，即使用了FileSort排序，全表扫描排序：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/ae403dac8e280a058ac09e958f6540ec.png)
> 
> **覆盖索引时索引排序更快**
> 
> 而如果我们使用了覆盖索引，在非聚簇索引树查询时，将不需要回表，所以使用了索引排序：
> 
> ```sql
> EXPLAIN SELECT name FROM student WHERE name like '%34' order by name;
> ```
> 
> 可以看到type是index，即索引树上全表扫描，extra是using index，覆盖索引：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/f474c59042fc6b1d8e8da45d8bc4429b.png)

##### **3.3.5.2 排序字段符合最左前缀**

当where后的条件符合最左前缀原则时，要让排序也走索引，需要排序字段也符合最佳左前缀原则。例如索引(a,b,c)，查询where a=1 order by a,b,c走索引，而where a=1 order by b,c不走索引。

> 验证：
> 
> **创建索引：**
> 
> ```sql
> CREATE INDEX idx_stuno_age_classid on student(stuno,age,classid);
> ```
> 
> **标准的排序字段符合最左前缀：**
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno =3 and age=2 order by stuno;
> ```
> 
> 可以看到type是ref，即命中非唯一索引，extra是空：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3d29d7de7522197999c78990d53326f9.png)
> 
> **排序字段不符合最左前缀-使用索引下推：**
> 
> 将排序字段由学号改为班号
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno =3 and age=2 order by classid;
> ```
> 
> 可以看到type是ref，即命中非唯一索引，extra是using index condition，即使用索引下推。索引下推是MySQL5.6支持的，当过滤的字段在索引树上并且索引失效时，将直接在索引树上走过滤，而不需要在MySQL服务器回表过滤。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/d7798df9bb19b6b96815f6fda8191c98.png)
> 
> **排序字段不符合最左前缀-不使用索引下推：**
> 
> 将排序字段由学号改为名字
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno =3 and age=2 order by name;
> ```
> 
> 可以看到type是ref，即命中非唯一索引，extra是using filesort，即使用了FileSort排序。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/49f485766a3eb3754f4fe8845588e8d0.png)

##### **3.3.5.3 全升序或者全降序**

排序顺序必须要么全部DESC，要么全部ASC，尽量不要使用混合排序。因为索引树的数据以一个顺序排列的，如果一些字段升序，一些字段降序，会导致整体性能较差。

> **验证：**
> 
> 全升序，运行时间0.025s
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno =3 and age=2 order by stuno ,age,classid;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/0f46d01545fd9b8f0fdda5fced391649.png)
> 
> 乱序，运行时间0.071s
> 
> ```
> SELECT * FROM student WHERE stuno =3 and age=2  order by stuno desc ,age,classid desc;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/c56c556bcd5df84acf590e22e24297cb.png)

##### **3.3.5.4 待排序数量大时，尽管索引没失效，索引效率不如filesort**

待排序数据量大约超过一万个，就不走索引走filesort了。建议用l**imit和where过滤**，减少数据量。数据量很大时，索引排序完需要回表根据这些过滤后数据的id查所有数据，性能很差，还不如FileSort在内存中排序效率高。

**注意：**并不是说使用limit一定会走索引排序，关键看的是数据量，数据量过大时优化器会使用FileSort排序。

##### **3.3.5.5 范围查询使排序索引失效**

前面3.3.1.6 有提到，范围查询会使后续的列索引失效，当然也会令排序无法走索引。

> **验证：**
> 
> 索引排序：
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno =3 order by stuno;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/25668b0719c4457b928baa9063c37dc1.png)
> 
> 范围查询导致排序索引失效：
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE stuno >3 order by stuno;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/4d4403e16e4644e10eef03bd6694f425.png)

##### **3.3.5.6 优先范围字段加索引（即使排序索引失效）**

当【范围条件】和【group by 或者 order by】的字段出现二选一时，如果过滤的数据足够多，而需要排序的数据并不多时，优先把索引放在范围字段上。

因为MySQL底层是，先where过滤，按过滤结果再分组、排序，所以优先给where后的字段加过滤，过滤掉主要的数据，然后再分组或排序，性能可以快很多。

这样即使范围查询导致排序索引失效，效率依然比只索引排序字段时候高。如果只能过滤一点点，那就优先索引放到排序字段上。

##### **3.3.5.7 调优FileSort**

无法使用 Index 排序时，需要对 FileSort 方式进行调优。

**1.排序缓冲区大小：**

sort\_buffer\_size。增加 sort\_buffer\_size 可以让更多的数据在内存中排序，从而减少对磁盘的依赖，提高性能。

```sql
SET GLOBAL sort_buffer_size = 1048576; -- 设置为1MB，根据需求调整
```

> 查看当前排序缓冲区大小：
> 
> ```sql
> SHOW VARIABLES LIKE 'sort_buffer_size';
> ```
> 
>  ![](https://i-blog.csdnimg.cn/blog_migrate/5eb6d53d7a443c381bb377bc596d4f43.png)

**2.排序数据最大长度：**

max\_length\_for\_sort\_data。增大这个值可以让 MySQL 采用更有效的排序方式，但需要权衡内存使用量。

```sql
SET GLOBAL max_length_for_sort_data = 1024; -- 设置为1KB，根据需求调整
```

#### **3.3.6 分组优化**

跟排序基本一个思路。

排序分组都比较耗费cpu，能不用就不用。

当需要过滤数据时，核心思路是能在where前过滤就别在having后过滤。因为where效率高于having。where是分组前过滤，having是分组后过滤。

#### **3.3.7 深分页查询优化**

深分页（Deep Pagination）：指在数据库查询中，通过 LIMIT 和 OFFSET 子句来分页获取数据时，偏移量（OFFSET）较大的情况。例如“limit 200000,10” ，即查询学生表中第200000~200010 的数据。

一般情况下，偏移量到达一万就可以称为深分页。但实际情况下还是需要根据具体的字段数量和类型去进行判断，例如一个表里只有两个int型字段，那么可能要十万以上才能算作深分页。

**优化方法：**

-   **如果主键有序：**
    -   如果排序字段是主键，则先过滤再排序；过滤条件是上一页最后一条记录，适用于app这种手滑翻页情景，翻页时一定是顺序翻页；
    -   如果排序字段不是主键，则根据上一页最后一条记录按规律排序
-   **如果主键不有序：**
    -   如果排序字段是主键，则先给主键分页，然后内连接原表查其他字段

> **验证：**
> 
> 需求：返回第200000~200010 的记录
> 
> **常规查询：**
> 
> ```sql
> EXPLAIN SELECT * FROM student ORDER BY id limit 200000,10
> ```
> 
> 可以看到运行时长0.09s，因为排序字段是id，所以走了主键索引树，type是index。 
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/e3cef8fbcf1093a2e4c8001d032232e3.png)
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/2adca39622ec4aa50bac031ec44f1b73.png)
> 
> **主键有序的表根据主键排序，先过滤再排序：**
> 
> 直接查范围之后的几个数据。
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE id > 200000 LIMIT 10;
> ```
> 
> 运行时长0.048s，可以看到性能变快。因为走范围索引后只对10个元素进行了排序，而常规查询方案相当于对200010条数据排序了。
> 
> 分析查询计划，可以看到，type是range，即范围索引，extra是using where ，即回表了（因为select \*）。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bbbbd61ee86a949f6202d14d6d5d3927.png)
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/86609fb9aa75c525f1784e083c4e4a36.png)
> 
> **主键不有序的表根据主键排序，先给主键分页，然后内连接原表：**
> 
> 当前表内连接排序截取后的主键表，连接字段是主键。因为查主键是在聚簇索引树查，不用回表，排序和分页很快
> 
> ```sql
> EXPLAIN SELECT * FROM student t,(SELECT id FROM student ORDER BY id LIMIT 200000,10) a WHERE t.id = a.id;
> ```
> 
> 可以看到运行时长明显缩短。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bbbbd61ee86a949f6202d14d6d5d3927.png) ![](https://i-blog.csdnimg.cn/blog_migrate/8154441fa523fea43f63324b22fc3e83.png)
> 
> **主键有序的表根据非主键排序：**
> 
> 得到上一页最后一条记录x，那么目标页码的所有记录id都比x.id小（因为逆序，且排序依据其实是age,id，主键自增），目标页码的所有记录age都比x.age小或等于。
> 
> ```sql
> EXPLAIN SELECT * FROM student WHERE id<#{x.id} AND age>=#{x.age} ORDER BY age DESC LIMIT 10;
> ```
> 
> **验证：**
> 
> 常规方案：0.378s
> 
> ```sql
> SELECT * FROM student ORDER BY age,id limit 200000,10
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/01b62e21db7bc23df8e63d275f1536fd.png)
> 
>  优化方案：0.031s
> 
> ```sql
> SELECT * FROM student WHERE id>481690 AND age>=20 ORDER BY age,id LIMIT 10;
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/2f142fc5cf28c2be6439c0cc6b8a1e86.png)

#### **3.3.8 尽量覆盖索引**

> **详细请参考：**
> 
> [MySQL高级篇——覆盖索引、前缀索引、索引下推、SQL优化、主键设计\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130804019 "MySQL高级篇——覆盖索引、前缀索引、索引下推、SQL优化、主键设计_vincewm的博客-CSDN博客")

一个索引包含了满足查询结果的数据。因为不需要回表，所以查询效率高。覆盖索引时“左模糊”和“不等于”不能让索引失效。

**示例：**

```bash
#没覆盖索引的情况下，左模糊查询导致索引失效
CREATE INDEX idx_age_name ON student(age, NAME);
EXPLAIN SELECT * FROM student WHERE NAME LIKE '%abc';
```

![](https://i-blog.csdnimg.cn/blog_migrate/5c3dcd422d7440f79048e24e5faeab68.png)

**覆盖索引：**一个索引包含了满足查询结果的数据就叫做覆盖索引，不需要回表等操作。

索引是高效找到行的一个方法，但是一般数据库也能使用索引找到一个列的数据，因此它不必读取整个行。毕竟索引叶子节点存储了它们索引的数据；当能通过读取索引就可以得到想要的数据，那就不需要读取行了。

覆盖索引是非聚簇索引的一种形式，它包括在查询里的SELECT、JOIN和WHERE子句用到的所有列 （即建索引的字段正好是覆盖查询条件中所涉及的字段）。简单说就是， 索引列+主键 包含 SELECT 到 FROM之间查询的列 。

#### **3.3.9 字符串前缀索引**

例如(email(6))，给字符串前缀而不是整个字符串添加索引，前缀长度要根据区分度和长度进行取舍。

**示例：**

MySQL是支持前缀索引的。默认地，如果你**创建索引的语句不指定前缀长度，那么索引就会包含整个字符串。**

```sql
mysql> alter table teacher add index index1(email);
#或
mysql> alter table teacher add index index2(email(6));
```

这两种不同的定义在数据结构和存储上有什么区别呢？下图就是这两个索引的示意图。

![](https://i-blog.csdnimg.cn/blog_migrate/90133d4bc129b1554fa46e3091a9684e.png)

![](https://i-blog.csdnimg.cn/blog_migrate/273a90dca71d7e5c2e2e8cbd784a8658.png)

**如果使用的是index1**（索引包含整个字符串），执行顺序是这样的：

1.  从index1索引树找到满足索引值是’ zhangssxyz@xxx.com’的这条记录，取得ID2的值；
2.  **回表**到主键上查到主键值是ID2的行，判断email的值是正确的，将这行记录加入结果集；
3.  取index1索引树上刚刚查到的位置的下一条记录，发现已经不满足email=' zhangssxyz@xxx.com ’的 条件了，循环结束。

这个过程中，只需要回主键索引取一次数据，所以系统认为只扫描了一行。

**如果使用的是index2**（索引包含字符串前缀email(6)），执行顺序是这样的：

1.  从index2索引树找到满足索引值是’zhangs’的记录，找到的第一个是ID1；
2.  **回表**到主键上查到主键值是ID1的行，判断出email的值不是’ zhangssxyz@xxx.com ’，这行记录丢弃；
3.  取index2上刚刚查到的位置的下一条记录，发现仍然是’zhangs’，取出ID2，再到**回表到**ID索引上取整行然后判断，这次值对了，将这行记录加入结果集；
4.  重复上一步，**直到在index2上取到的值不是’zhangs’时**，循环结束。

也就是说使用前缀索引，定义好长度，**就可以做到既节省空间，又不用额外增加太多的查询成本。**前面 已经讲过区分度，**区分度越高越好**。因为区分度越高，意味着重复的键值越少。

#### **3.3.10 尽量使用MySQL5.6支持的索引下推**

**ICP（索引下推）：**在使用范围查询时，允许 MySQL 在存储引擎层面（如 InnoDB）利用索引树来过滤数据，而不是将数据传递给 MySQL 服务器层再进行过滤，从而减少了需要从存储引擎传递到服务器层的数据量。

简而言之，**索引下推可以使范围查询右侧索引失效的列，依然可以在索引树上过滤。**

例如索引(name,age)，查询name like 'z%' and age and address，'z%'是模糊查询，实际上也是范围查询。使用索引下推时，在联合索引树查询时不止查name，还会判断后面的age。而如果关闭了索引下推，联合索引里范围查询后面的字段age不能在联合索引树里直接条件判断，必须回表到主键索引树后，以之前过滤结果id查找到对应数据，再过滤age列。

> **注意：**这里举例没有使用'%z'，因为左模糊查询会使整个索引失效，也就不会用到索引下推了。

**索引下推**(ICP，Index Condition Pushdown)是MySQL 5.6中新特性，是一种在存储引擎层使用索引过滤数据的一种优化方式。

-   **如果没有ICP**：联合索引某字段是模糊查询（非左模糊）或范围查询时，该字段进行条件判断后，后面几个字段不能用来直接条件判断，必须在MySQL服务器回表后再判断。
-   **启用ICP 后**：联合索引某字段是模糊查询（非左模糊）或范围查询时，该字段进行条件判断后，后面几个字段可以直接条件判断，判断过滤后再回表对不包含在联合索引内的字段条件进行判断。主要优化点是在回表之前过滤，减少回表次数。主要应用：模糊查询（非左模糊）导致索引里该字段后面的字段无序，必须要回表判断，而使用了索引下推，就不需要回表，直接在联合索引树里判断。

**举例：**

-   **不支持索引下推的联合索引：**例如索引(name,age)，查询name like 'z%' and age=？，模糊查询（实际是范围查询）导致右边的列age无法走索引。在联合索引树查询时只会查name，后面的age乱序不能直接进行条件判断，必须回表后再判断age。
-   **而支持索引下推的联合索引：**例如索引(name,age)，查询name like 'z%' and age and address，在联合索引树查询时不止查name，还会判断后面的age，过滤后再回表判断address。

> **验证：**
> 
> 删除所有索引：
> 
> ```sql
> CALL proc_drop_index("test","student");
> ```
> 
> 创建索引 
> 
> ```sql
> CREATE INDEX idx_name_age ON student(name,age);
> ```
> 
> 开启索引下推：
> 
> ```sql
> SET optimizer_switch='index_condition_pushdown=on';
> ```
> 
> 索引下推查询计划分析： 
> 
> ```bash
> #索引成功；MySQL5.6引入索引下推，where后面的name和age都在联合索引里，可以又过滤又索引，不用回表，索引生效
> EXPLAIN SELECT * FROM student WHERE `name` like 'bc%' AND age=30;
> ```
> 
> 可以看出，type是range，即范围索引，extra是using index condition，即使用了索引下推。因为 age在联合索引（name,age）树里，所以即使name是范围查询导致右侧的age索引失效了，依然可以在这个索引树中过滤age条件：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/d09dd0bdcf9cf38aaac60e9f79c4beb8.png)
> 
> 关闭索引下推：
> 
> ```sql
> SET optimizer_switch='index_condition_pushdown=off';
> ```
> 
> 关闭索引下推后查询计划分析： 
> 
> ```bash
> #范围查询导致右侧列age索引失效，因为关闭了索引下推
> EXPLAIN SELECT * FROM student WHERE `name` like 'bc%' AND age=30;
> ```
> 
> 可以看到，type是range，即使用了范围索引，extra是using where，即使用了回表。在走name列范围查询后，age列索引失效，转为回表，将name过滤后的数据id作为条件，在主键索引数中过滤age条件：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/d41255f1d276412e3ca121e024bbeee8.png)

#### **3.3.11 读少写多的场景，尽量用普通索引**

**结论：**读多写少用唯一索引，读少写多用普通索引+代码逻辑中去维护唯一性。

**普通索引和唯一索引的区别：** 

-   **概念：**普通索引可重复，唯一索引不能重复。
-   **查询性能：**
    -   唯一索引查询性能略高，特别是重复记录很多的时候。
    -   因为同样查k=4，普通索引查到第一个k=4记录时还要继续查下去，直到查到不满足k=4的记录；而唯一索引查到第一个k=4记录将不再需要查下去。
    -   整体来说，二者性能差距很小，因为 InnoDB 是以页为单位读写的，所以可能对于普通索引的扫描过程来说就是在内存中进行，除非是需要跨页查询了，那还要继续读取下一页数据。
-   **更新性能：**
    -   普通索引更新性能更高，特别是目标页不在内存中场景。
    -   因为普通索引有change buffer（写缓存）将更新后的数据页缓存到内存，下次访问时或后台定期会执行merge操作，将该数据页写入磁盘。（change buffer在事务提交时会写入redo log，保证数据持久化）而唯一索引不支持写缓存，而且插入前要判断唯一性，这部分会影响性能。
-   **应用场景：**
    -   **数据唯一、多读少写：**使用唯一索引，因为它查询性能高，写性能差。
    -   **数据唯一、少读多写：**使用普通索引+代码逻辑保持唯一。
        -   **更新之后需要立刻查询**：关闭 change buffer。不然要经历“更新操作存入change buffer->加载数据页到内存（缓冲池）->更新->“change buffer删除对应更新操作”->查询”的过程，影响性能。关闭后流程是“加载数据页到内存（缓冲池）->更新->查询”。
        -   **更新之后不需要立刻查询：**保持change buffer打开。
    -   **数据不唯一：**使用普通索引，不能使用唯一索引。
-   **语句：** 
    -   **普通索引：**不加任何限制条件，如create index idx\_name on student(name)。
    -   **唯一索引：**UNIQUE参数限制索引唯一，如create UNIQUE index idx\_name on student(name)。

> **写缓存（change buffer）：**
> 
> 当需要更新一个数据页时，如果数据页在内存中就直接更新，而如果这个数据页还没有在内存中的话， 在不影响数据一致性的前提下， **InooDB会将这些更新操作缓存在change buffer中** ，这样就不需要从磁盘中读入这个数据页了。在下次查询需要访问这个数据页的时候，将数据页读入内存，然后执行change buffer中与这个页有关的操作。通过这种方式就能保证这个数据逻辑的正确性。
> 
> **merge ：**将change buffer中的操作应用到原数据页，得到最新结果的过程称为 merge 。除了访问这个数据页会触发merge外，系统有后台线程会定期merge。在数据库正常关闭（shutdown）的过程中，也会执行merge 操作。
> 
> 如果能够将更新操作先记录在change buffer， **减少读磁盘** ，语句的执行速度会得到明显的提升。而且， 数据读入内存是需要占用 buffer pool 的，所以这种方式还能够 **避免占用内存**，提高内存利用率。
> 
> **唯一索引的更新就不能使用change buffer** ，实际上也只有普通索引可以使用。

> **做好区分：**
> 
> -   读数据用的是**缓冲池buffer pool**；
> -   重做日志有个**redo log buffer**，是将缓冲池里更新的数据写入redo log buffer，事务提交时根据刷盘策略，将redo log buffer刷盘到redo log file或page cache。

### **3.4 SQL优化**

> **详细请参考：**
> 
> [MySQL高级篇——覆盖索引、前缀索引、索引下推、SQL优化、主键设计\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/130804019 "MySQL高级篇——覆盖索引、前缀索引、索引下推、SQL优化、主键设计_vincewm的博客-CSDN博客")

#### **3.4.1** 合理选用 EXISTS 和 IN

遵循小表驱动大表原则，左边表小就是EXISTS，左边表大就用IN。

-   **EXISTS**：适用于左边表较小的情况，因为EXISTS子查询在找到满足条件的记录后会立即返回，适合处理小表驱动大表的场景。
    
    ```sql
    SELECT * FROM large_table WHERE EXISTS (SELECT 1 FROM small_table WHERE small_table.id = large_table.id);
    ```
    
-   **IN**：适用于左边表较大的情况，因为IN子查询会先执行并将结果集缓存下来，再与外部查询匹配，适合处理大表驱动小表的场景。
    
    ```sql
    SELECT * FROM small_table WHERE id IN (SELECT id FROM large_table);
    ```
    

#### **3.4.2** 统计数量COUNT(1) 或 COUNT(\*)

-   **count（1）:**统计整个表的记录行数。括号里表示一个固定值，可以是任何固定的数字字符，是个常量。在InnoDB存储引擎中，查询优化器会优先选择占用空间最小的二级索引树进行统计。COUNT(1)和COUNT(\*)在性能上没有显著差别，因为优化器会处理为相同的查询计划。MyISAM存储引擎中，COUNT操作的时间复杂度为O(1)。
-   **count（\*）:**统计整个表的记录行数，与count（1）执行结果相同，但是执行会根据目标表的不同进行优化。
-   **count（列名）:**统计某一列的非空记录数。它会统计指定列中不为NULL的行数，忽略NULL值。
-   **count(distinct(列名)) ：**统计某一列的非空去重记录数。其实是 count(列名) + distinct 的结果集，指定列不为NULL，并且在字段值重复的情况下只统计一次

在使用InnoDB存储引擎时，COUNT(1),COUNT(\*)时，查询优化器会优先选用有索引的、占用空间最小的二级索引树进行统计，只有找不到非聚簇索引树时才会采用使用聚簇索引树统计。

当然也能COUNT(最小空间二级索引字段)，但很麻烦，需要你自己找到最小空间并且建了索引的字段，而且也要考虑null值，不如交给优化器自动选择。

在使用MyISAM存储引擎时，就无所谓了，用哪个时间复杂度都是O(1)。 

```sql
SELECT COUNT(*) FROM table_name;
```

#### **3.4.3** 避免SELECT \*

-   **明确字段查询**：避免使用SELECT \*，明确列名不仅可以提高查询解析速度，还可以利用覆盖索引，减少回表操作。select \*可能会多查一些字段，提高了一些网络传输负担，而且杜绝了覆盖索引的可能性，性能较差。
    
    ```sql
    SELECT id, name, age FROM student WHERE id = 123;
    ```
    

> **数据库引擎的通用查询流程：**
> 
> 1.  **解析 SQL 语句：**数据库引擎先将 SQL 语句解析成内部的执行计划，包括了查询哪些数据表、使用哪些索引、如何连接多个数据表等信息。
> 2.  **优化查询计划：**数据库引擎对内部的执行计划进行优化，根据查询的复杂度、数据量和系统资源等因素，选择最优的执行计划。
> 3.  **执行查询计划：**数据库引擎根据执行计划，通过 I/O 操作读取数据表的数据，进行数据过滤、排序、分组等操作，最终返回结果集。
> 4.  **缓存查询结果：**如果查询结果集比较大或者查询频率较高，数据库引擎会将查询结果缓存在内存中，以加速后续的查询操作。
> 
> **MySQL执行一条select语句时会经过的流程：**
> 
> 1.  **连接器：**主要作用是建立连接、管理连接及校验用户信息。
> 2.  **查询缓冲：**查询缓冲是以key-value的方式存储，key就是查询语句，value就是查询语句的查询结果集；如果命中直接返回。
>     1.  **8.0版本废弃：**注意，MySQL 8.0已经删除了查询缓冲。从MySQL 5.6版本开始，官方将Query Cache设置为了默认关闭。
>     2.  **原因：**官方给出的原因是这个功能比较鸡肋，而且减少性能的可变性确实通常比提高峰值吞吐量更重要，尤其是在生产环境中。稳定的性能可以确保用户体验的一致性，并减少系统出现瓶颈或宕机的风险。
>     3.  **方案：**官方给出了所替代的解决方案建议——使用第三方工具客户端缓存ProxySQL 来代替Query Cache。
> 3.  **分析器：**词法句法分析生成语法树。
> 4.  **优化器：**指定执行计划，选择查询成本最小的计划。
> 5.  **执行器：**根据执行计划，从存储引擎获取数据，并返回客户端
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/7c7c2dab6c2b37e1f1d79758c21ad91b.png)
> 
> **ProxySQL：**
> 
> -   **基本介绍：**一个MySQL中间件，一个高性能的 MySQL 代理，一个用 C++ 开发的轻量级产品。旨在提高 MySQL 服务器的性能、可伸缩性和可用性。MySQL官方推荐的Query Cache替换方案。
> -   **同类产品：**DBproxy、MyCAT、OneProxy
> -   **安装配置：**
>     -   **安装：**
>         
>         ```sql
>         sudo yum install proxysql
>         ```
>         
>         **配置：** 修改/etc/proxysql.cnf 直接配置，或者访问管理接口配置：
>         
>         ```sql
>         -- 连接到管理接口
>         mysql -u admin -padmin -h 127.0.0.1 -P 6032
>         
>         -- 添加MySQL服务器
>         INSERT INTO mysql_servers (hostgroup_id, hostname, port) VALUES (0, '192.168.1.100', 3306);
>         
>         -- 加载配置到运行时
>         LOAD MYSQL SERVERS TO RUNTIME;
>         
>         -- 保存配置到磁盘
>         SAVE MYSQL SERVERS TO DISK;
>         ```
>         
> -   **功能：**
>     -   **查询缓存**
>     -   **负载均衡**：支持自动摘除宕机的DB
>     -   读写分离
>         
>         ```sql
>         -- 主库
>         INSERT INTO mysql_servers (hostgroup_id, hostname, port) VALUES (10, '192.168.1.101', 3306);
>         
>         -- 从库
>         INSERT INTO mysql_servers (hostgroup_id, hostname, port) VALUES (20, '192.168.1.102', 3306);
>         INSERT INTO mysql_servers (hostgroup_id, hostname, port) VALUES (20, '192.168.1.103', 3306);
>         -- 将所有写操作（INSERT、UPDATE、DELETE）定向到主库
>         INSERT INTO mysql_query_rules (rule_id, active, match_pattern, destination_hostgroup) VALUES (1, 1, '^INSERT', 10);
>         INSERT INTO mysql_query_rules (rule_id, active, match_pattern, destination_hostgroup) VALUES (2, 1, '^UPDATE', 10);
>         INSERT INTO mysql_query_rules (rule_id, active, match_pattern, destination_hostgroup) VALUES (3, 1, '^DELETE', 10);
>         
>         -- 将所有读操作（SELECT）定向到从库
>         INSERT INTO mysql_query_rules (rule_id, active, match_pattern, destination_hostgroup) VALUES (4, 1, '^SELECT', 20);
>         -- 加载并保存配置
>         LOAD MYSQL SERVERS TO RUNTIME;
>         SAVE MYSQL SERVERS TO DISK;
>         ```
>         
>     -   实时监控
>     -   连接池
>     -   动态加载配置
>     -   访问控制
>     -   ProxySQL集群

#### **3.4.4** 全表扫描时尽量用 LIMIT

当进行全表扫描并且明确时，使用LIMIT可以在达到指定数量后停止扫描，减少不必要的开销。

例如根据学号查询学生，根据身份证号查询人，根据订单号查询订单，当我们明确知道需要精准查询时，用Limit 1 总错不了。

当然如果走了唯一索引，就无需用limit了，查到对应记录会直接返回；如果走了普通索引，并且对应记录重复数据很多的话，用limit也会提高一些性能。

```sql
-- 根据学号（假设学号是按班级隔离的）和班级号精准查询学生
SELECT * FROM student where stuno =23 and classid=1 LIMIT 1;
```

#### **3.4.5** 使用 LIMIT N，少用 LIMIT M, N

-   **避免大偏移量的LIMIT**：在大表或M值较大时，LIMIT M, N的性能较差，因为需要扫描并丢弃前M条记录。可以通过记录上次查询的最大ID来优化分页。
    
    ```sql
    SELECT * FROM large_table WHERE id > last_id ORDER BY id ASC LIMIT 10;
    ```
    

#### **3.4.6** 代码将长事务拆为多个小事务

-   **多使用COMMIT**：长事务会持有锁和占用资源较长时间，拆分为小事务并频繁COMMIT可以释放锁、减少资源占用。
    

**示例：** 

```java
@Transactional
public void fun(){
    // 1.查询a
    // 2.查询b
    // 3.数据处理
    // 4.保存c表
    // 5.保存b表
}
```

优化成：

```java
​
@Transactional
public void fun(){
    // 1.查询a
    // 2.查询b
    // 3.数据处理
    // 4.落库
    savaFun();
}

​public void savaFun(){
    // 1.保存c表
    // 2.保存d表
}
```

#### **3.4.7** 删改前先查询

-   **确保WHERE条件明确**：在执行UPDATE或DELETE操作前，先SELECT一下并不会让性能变差，它可以确保有明确的WHERE条件，避免误操作和全表扫描。
    
    ```sql
    UPDATE student SET age = age + 1 WHERE id = 123;
    DELETE FROM student WHERE id = 123;
    ```
    

> **阿里规约：**
> 
> 【强制】 数据订正（特别是删除、修改记录操作）时，要先 select ，避免出现误删除，确认无误才能执行更新语句。

#### **3.4.8** 尽量UNION ALL而不是UNION

-   **UNION ALL**：UNION ALL 和 UNION 都用于组合两个或多个查询结果集。UNION ALL在组合时，不进行去重操作，比UNION更快，适用于不需要去重的场景。
    
    ```sql
    SELECT id, name FROM table1
    UNION ALL
    SELECT id, name FROM table2;
    ```