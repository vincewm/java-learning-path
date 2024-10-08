> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")
> 
> **黑马旅游源码：** 
> 
> https://wwmg.lanzouk.com/b04q61nof  
> 密码:foqf

**目录**

[1.DSL查询文档](#1.DSL%E6%9F%A5%E8%AF%A2%E6%96%87%E6%A1%A3)

[1.1.DSL查询分类](#1.1.DSL%E6%9F%A5%E8%AF%A2%E5%88%86%E7%B1%BB) 

[1.2.全文检索查询（单条件）](#1.2.%E5%85%A8%E6%96%87%E6%A3%80%E7%B4%A2%E6%9F%A5%E8%AF%A2)

[1.2.1.使用场景](#1.2.1.%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF)

[1.2.2.基本语法，match,multi\_match](#1.2.2.%E5%9F%BA%E6%9C%AC%E8%AF%AD%E6%B3%95)

[1.2.3.示例](#1.2.3.%E7%A4%BA%E4%BE%8B)

[1.2.4.总结](#1.2.4.%E6%80%BB%E7%BB%93)

[1.3.精准查询](#1.3.%E7%B2%BE%E5%87%86%E6%9F%A5%E8%AF%A2)

[1.3.1.精确值查询，term和terms](#1.3.1.term%E6%9F%A5%E8%AF%A2)

[1.3.2.范围查询，range](#1.3.2.range%E6%9F%A5%E8%AF%A2)

[1.3.3.总结](#1.3.3.%E6%80%BB%E7%BB%93)

[1.4.地理坐标查询](#1.4.%E5%9C%B0%E7%90%86%E5%9D%90%E6%A0%87%E6%9F%A5%E8%AF%A2)

[1.4.1.矩形范围查询，geo\_bounding\_box](#1.4.1.%E7%9F%A9%E5%BD%A2%E8%8C%83%E5%9B%B4%E6%9F%A5%E8%AF%A2)

[1.4.2.距离查询，geo\_distance](#1.4.2.%E9%99%84%E8%BF%91%E6%9F%A5%E8%AF%A2)

[1.5.复合查询](#1.5.%E5%A4%8D%E5%90%88%E6%9F%A5%E8%AF%A2)

[1.5.1.相关性算分，默认match查询](#1.5.1.%E7%9B%B8%E5%85%B3%E6%80%A7%E7%AE%97%E5%88%86)

[1.5.2.算分函数查询，function\_score](#1.5.2.%E7%AE%97%E5%88%86%E5%87%BD%E6%95%B0%E6%9F%A5%E8%AF%A2)

[1.5.3.布尔查询（多条件），bool](#1.5.3.%E5%B8%83%E5%B0%94%E6%9F%A5%E8%AF%A2)

[1.6 nested嵌入式查询](#1.6%20nested%E5%B5%8C%E5%85%A5%E5%BC%8F%E6%9F%A5%E8%AF%A2)

[2.搜索结果处理](#2.%E6%90%9C%E7%B4%A2%E7%BB%93%E6%9E%9C%E5%A4%84%E7%90%86)

[2.0.搜索结果处理的整体样式](#2.4.%E6%80%BB%E7%BB%93)

[2.1.排序](#2.1.%E6%8E%92%E5%BA%8F)

[2.1.1.普通字段排序,sort](#2.1.1.%E6%99%AE%E9%80%9A%E5%AD%97%E6%AE%B5%E6%8E%92%E5%BA%8F)

[2.1.2.地理坐标排序，\_geo\_distance](#2.1.2.%E5%9C%B0%E7%90%86%E5%9D%90%E6%A0%87%E6%8E%92%E5%BA%8F)

[2.2.分页](#2.2.%E5%88%86%E9%A1%B5)

[2.2.1.基本的分页，from+size](#2.2.1.%E5%9F%BA%E6%9C%AC%E7%9A%84%E5%88%86%E9%A1%B5)

[2.2.2.深度分页问题，after search](#2.2.2.%E6%B7%B1%E5%BA%A6%E5%88%86%E9%A1%B5%E9%97%AE%E9%A2%98)

[2.2.3.小结，三种分页](#2.2.3.%E5%B0%8F%E7%BB%93)

[2.3.高亮](#2.3.%E9%AB%98%E4%BA%AE)

[2.3.1.高亮原理](#2.3.1.%E9%AB%98%E4%BA%AE%E5%8E%9F%E7%90%86)

[2.3.2.实现高亮](#2.3.2.%E5%AE%9E%E7%8E%B0%E9%AB%98%E4%BA%AE)

[3.RestClient查询文档](#3.RestClient%E6%9F%A5%E8%AF%A2%E6%96%87%E6%A1%A3)

[3.1.快速入门，查询所有，match\_all](#3.1.%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)

[3.1.1.发起查询请求](#3.1.1.%E5%8F%91%E8%B5%B7%E6%9F%A5%E8%AF%A2%E8%AF%B7%E6%B1%82)

[3.1.2.解析响应](#3.1.2.%E8%A7%A3%E6%9E%90%E5%93%8D%E5%BA%94)

[3.1.3.完整代码](#3.1.3.%E5%AE%8C%E6%95%B4%E4%BB%A3%E7%A0%81)

[3.1.4.小结](#3.1.4.%E5%B0%8F%E7%BB%93)

[3.2.match查询](#3.2.match%E6%9F%A5%E8%AF%A2)

[3.3.精确查询](#3.3.%E7%B2%BE%E7%A1%AE%E6%9F%A5%E8%AF%A2)

[3.4.布尔查询](#3.4.%E5%B8%83%E5%B0%94%E6%9F%A5%E8%AF%A2)

[3.5.排序、分页](#3.5.%E6%8E%92%E5%BA%8F%E3%80%81%E5%88%86%E9%A1%B5)

[3.6.高亮](#3.6.%E9%AB%98%E4%BA%AE)

[3.6.1.高亮请求构建](#3.6.1.%E9%AB%98%E4%BA%AE%E8%AF%B7%E6%B1%82%E6%9E%84%E5%BB%BA)

[3.6.2.高亮结果解析](#3.6.2.%E9%AB%98%E4%BA%AE%E7%BB%93%E6%9E%9C%E8%A7%A3%E6%9E%90)

[4.黑马旅游案例](#4.%E9%BB%91%E9%A9%AC%E6%97%85%E6%B8%B8%E6%A1%88%E4%BE%8B)

[4.0.项目准备和预览](#4.0.%E9%A1%B9%E7%9B%AE%E5%87%86%E5%A4%87%E5%92%8C%E9%A2%84%E8%A7%88%C2%A0) 

[4.1.酒店搜索和分页](#4.1.%E9%85%92%E5%BA%97%E6%90%9C%E7%B4%A2%E5%92%8C%E5%88%86%E9%A1%B5)

[4.1.1.需求分析](#4.1.1.%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90)

[4.1.2.定义分页请求参数和响应结果实体类](#4.1.2.%E5%AE%9A%E4%B9%89%E5%AE%9E%E4%BD%93%E7%B1%BB)

[4.1.3.定义controller](#4.1.3.%E5%AE%9A%E4%B9%89controller)

[4.1.4.实现搜索业务](#4.1.4.%E5%AE%9E%E7%8E%B0%E6%90%9C%E7%B4%A2%E4%B8%9A%E5%8A%A1)

[4.2.酒店结果过滤](#4.2.%E9%85%92%E5%BA%97%E7%BB%93%E6%9E%9C%E8%BF%87%E6%BB%A4)

[4.2.1.需求分析](#4.2.1.%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90)

[4.2.2.查询条件实体类增加成员变量](#4.2.2.%E4%BF%AE%E6%94%B9%E5%AE%9E%E4%BD%93%E7%B1%BB)

[4.2.3.修改搜索业务，布尔查询](#4.2.3.%E4%BF%AE%E6%94%B9%E6%90%9C%E7%B4%A2%E4%B8%9A%E5%8A%A1)

[4.3.我周边的酒店](#4.3.%E6%88%91%E5%91%A8%E8%BE%B9%E7%9A%84%E9%85%92%E5%BA%97)

[4.3.1.需求分析](#4.3.1.%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90)

[4.3.2.查询条件实体类增加成员变量](#4.3.2.%E4%BF%AE%E6%94%B9%E5%AE%9E%E4%BD%93%E7%B1%BB)

[4.3.3.距离排序API](#4.3.3.%E8%B7%9D%E7%A6%BB%E6%8E%92%E5%BA%8FAPI)

[4.3.4.添加距离排序](#4.3.4.%E6%B7%BB%E5%8A%A0%E8%B7%9D%E7%A6%BB%E6%8E%92%E5%BA%8F)

[4.3.5.排序距离显示](#4.3.5.%E6%8E%92%E5%BA%8F%E8%B7%9D%E7%A6%BB%E6%98%BE%E7%A4%BA)

[4.4.酒店竞价排名](#4.4.%E9%85%92%E5%BA%97%E7%AB%9E%E4%BB%B7%E6%8E%92%E5%90%8D)

[4.4.1.需求分析](#4.4.1.%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90)

[4.4.2.HotelDoc实体类添加成员变量isAD](#4.4.2.%E4%BF%AE%E6%94%B9HotelDoc%E5%AE%9E%E4%BD%93)

[4.4.3.给文档添加广告标记](#4.4.3.%E6%B7%BB%E5%8A%A0%E5%B9%BF%E5%91%8A%E6%A0%87%E8%AE%B0)

[4.4.4.基础查询业务添加算分函数查询](#4.4.4.%E6%B7%BB%E5%8A%A0%E7%AE%97%E5%88%86%E5%87%BD%E6%95%B0%E6%9F%A5%E8%AF%A2)

--

## 1.DSL查询文档

elasticsearch的查询依然是基于JSON风格的DSL来实现的。

> **领域特定语言**（英语：_domain_\-_specific_ _language_、**DSL**）指的是专注于某个应用程序领域的计算机语言。

### 1.1.DSL查询分类 

Elasticsearch提供了基于JSON的DSL（[Domain Specific Language](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html "Domain Specific Language")）来定义查询。常见的查询类型包括：

-   **查询所有**：查询出所有数据，一般测试用。例如：
    
    -   match\_all
        
-   **全文检索（full text）查询**：利用**分词器**对用户输入内容分词，然后去倒排索引库中匹配。例如：
    
    -   match
    -   multi\_match
-   **精确查询**：根据精确词条值查找数据，一般**查找不分词的字段**，例如keyword、数值、日期、boolean等类型字段。例如：
    
    -   ids
    -   range
    -   term
-   **地理（geo）查询**：根据经纬度查询，经纬度不分词。例如：
    
    -   geo\_distance
    -   geo\_bounding\_box
-   **复合（compound）查询**：复合查询可以将上述各种查询条件组合起来，合并查询条件。例如：
    
    -   bool
    -   function\_score

查询的语法基本一致：

```bash
GET /indexName/_search
{
  "query": {
    "查询类型": {
      "查询条件": "条件值"
    }
  }
}
```

我们以查询所有为例，其中：

-   查询类型为match\_all
-   没有查询条件

```java
// 查询所有
GET /indexName/_search
{
  "query": {
    "match_all": {
    }
  }
}
```

其它查询无非就是**查询类型**、**查询条件**的变化。

### 1.2.全文检索查询（单条件）

#### 1.2.1.使用场景

全文检索查询的**基本流程**如下：

-   对用户搜索的内容做**分词**，得到词条
-   根据词条去倒排索引库中**匹配**，得到**文档id**
-   根据文档id**找到文档**，返回给用户

比较常用的场景包括：

-   商城的输入框搜索
-   百度输入框搜索

例如京东：

![image-20210721165326938](https://i-blog.csdnimg.cn/blog_migrate/8ed6516665ec8b5662769eadac48b332.png)

因为是拿着词条去匹配，因此参与搜索的字段也必须是可分词的text类型的字段。

#### 1.2.2.基本语法，match,multi\_match

常见的全文检索查询包括：

-   **match查询：**单字段查询
-   **multi\_match查询：**多字段查询，**任意一个字段符合条件就算符合查询条件**

**match查询语法如下：**

```bash
GET /indexName/_search
{
  "query": {
    "match": {
      "字段名": "检索内容"
    }
  }
}
```

例如 

```bash
GET /indexName/_search
{
  "query": {
    "match": {
      "all": "上海"
    }
  }
}
```

**multi\_match语法如下：同时多字段查询**

```bash
GET /indexName/_search
{
  "query": {
    "multi_match": {        #任意一个字段符合条件就算符合查询条件
      "query": "查询内容",
      "fields": ["字段名1", " 字段名2"]
    }
  }
}
```

>  建议match查询，**multi\_match字段越多效率越低，多字段建议用match查copy\_to**。

#### 1.2.3.示例

match查询示例：

![image-20210721170455419](https://i-blog.csdnimg.cn/blog_migrate/8833aa456625aad2ad8c3059d0bb9373.png)

multi\_match查询示例：

![image-20210721170720691](https://i-blog.csdnimg.cn/blog_migrate/9681821eebf9868074d355ed89d2cf60.png)

可以看到，两种查询结果是一样的，为什么？

因为我们将brand、name、business值都利用**copy\_to复制**到了all字段中。因此你根据三个字段搜索，和根据all字段搜索效果当然一样了。

但是，搜索字段越多，对查询性能影响越大，因此建议**采用copy\_to**，然后单字段查询的方式。

#### 1.2.4.总结

match和multi\_match的区别是什么？

-   match：根据一个字段查询
-   multi\_match：根据多个字段查询，参与查询字段越多，查询性能越差

### 1.3.精准查询

精确查询一般是**查找不分词的字段**，例如keyword、数值、日期、boolean等类型字段。所以**不会**对搜索条件分词。常见的有：

-   **term：**根据词条精确值查询
-   **range：**根据值的范围查询

#### 1.3.1.精确值查询，term和terms

因为精确查询的字段**搜不分词的字段**，因此查询的条件也**必须是不分词**的词条。查询时，用户输入的内容跟自动值**一模一样**时才认为符合条件。如果用户输入的内容过多，反而搜索不到数据。

**语法说明：**

```java
// term查询某个字段里含有某个关键词的文档
GET /indexName/_search
{
  "query": {
    "term": {
      "不参与分词的字段名": {    
        "value": "查询内容"
      }
    }
  }
}
```

```java
// terms查询某个字段里含有多个关键词的文档
GET /indexName/_search
{
  "query": {
    "term": {
      "不参与分词的字段名": {    
        "value": [ "精准内容1","精准内容2"]
      }
    }
  }
}
```

> **注意：** 
> 
> -   **只能查不参与分词的字段**
> -   **查询内容字符串和数字都行，例如"price":"23"和"price":23一样**

**示例：**

当我搜索的是精确词条时，能正确查询出结果：

![image-20210721171655308](https://i-blog.csdnimg.cn/blog_migrate/febf446a2b6d89a29042c11662e07fb0.png)

但是，当我搜索的内容不是词条，而是多个词语形成的短语时，反而搜索不到：

![image-20210721171838378](https://i-blog.csdnimg.cn/blog_migrate/32b9e449c7e47da468164b1ede054f4f.png)

#### 1.3.2.范围查询，range

范围查询，一般应用在对数值类型做**范围过滤**的时候。比如做价格范围过滤。

**基本语法：**

```java
// range查询
GET /indexName/_search
{
  "query": {
    "range": {
      "字段名": {
        "gte": 10, // 这里的gte代表大于等于，gt则代表大于
        "lte": 20 // lte代表小于等于，lt则代表小于
      }
    }
  }
}
```

> **gt:great than** 
> 
> **gte:great than or equal** 
> 
> **lt:less than**
> 
> **lte:less than or equal**

示例：

![image-20210721172307172](https://i-blog.csdnimg.cn/blog_migrate/ef837a71c378e63b0342eee81f531bd2.png)

#### 1.3.3.总结

精确查询常见的有哪些？

-   term查询：根据词条精确匹配，一般搜索keyword类型、数值类型、布尔类型、日期类型字段
-   range查询：根据数值范围查询，可以是数值、日期的范围

### 1.4.地理坐标查询

所谓的地理坐标查询，其实就是根据经纬度查询，官方文档：https://www.elastic.co/guide/en/elasticsearch/reference/current/geo-queries.html

常见的使用场景包括：

-   携程：搜索我附近的酒店
-   滴滴：搜索我附近的出租车
-   微信：搜索我附近的人

附近的酒店：

![image-20210721172645103](https://i-blog.csdnimg.cn/blog_migrate/b6a5e95091999b1b9b5a70c30fca68c2.png)

附近的车：

![image-20210721172654880](https://i-blog.csdnimg.cn/blog_migrate/643c285108884eeec5e67bbab54dd1cd.png)

#### 1.4.1.矩形范围查询，geo\_bounding\_box

矩形范围查询，也就是geo\_bounding\_box查询，查询**坐标落在某个矩形范围**的所有文档：

 geo\_bounding\_box译为地理边框盒子。

![DKV9HZbVS6](https://i-blog.csdnimg.cn/blog_migrate/2e513563d56d760aec1a9ced520efe46.gif)

查询时，需要指定矩形的**左上**、**右下两个点的坐标**，然后画出一个矩形，落在该矩形内的都是符合条件的点。

语法如下：

```java
// geo_bounding_box查询
GET /indexName/_search
{
  "query": {
    "geo_bounding_box": {
      "FIELD": {
        "top_left": { // 左上点
          "lat": 31.1,
          "lon": 121.5
        },
        "bottom_right": { // 右下点
          "lat": 30.9,
          "lon": 121.7
        }
      }
    }
  }
}
```

这种并不符合“附近的人”这样的需求，所以我们就不做了。

#### 1.4.2.距离查询，geo\_distance

附近查询，也叫做距离查询（geo\_distance）：查询到**指定中心点小于某个距离值**的所有文档。

换句话来说，在地图上找一个点作为圆心，以指定距离为半径，画一个圆，落在圆内的坐标都算符合条件：

![](https://i-blog.csdnimg.cn/blog_migrate/cc2497aaf3088e493e513243961f8349.png)

语法说明：

```java
// geo_distance 查询
GET /indexName/_search
{
  "query": {
    "geo_distance": {
      "distance": "15km", // 半径
      "FIELD": "31.21,121.5" // 圆心
    }
  }
}
```

**示例：**

我们先搜索陆家嘴附近15km的酒店：

![image-20210721175443234](https://i-blog.csdnimg.cn/blog_migrate/c3b68fdd994146685b729fda49349498.png)

发现共有47家酒店。

然后把半径缩短到3公里：

![image-20210721182031475](https://i-blog.csdnimg.cn/blog_migrate/a5be49b0f9fa6b20da54c2b72f84972a.png)

可以发现，搜索到的酒店数量减少到了5家。

### 1.5.复合查询

复合（compound）查询：复合查询可以将其它简单查询组合起来，实现更复杂的搜索逻辑。常见的有两种：

-   **fuction score：**算分函数查询，可以**控制文档相关性算分**，控制文档排名
-   **bool query：**布尔查询，利用**逻辑关系组合多个其它的查询**，实现复杂搜索

#### 1.5.1.相关性算分，默认match查询

当我们利用match查询时，文档结果会根据与搜索词条的关联度打分（\_score），返回结果时按照分值降序排列。

**match单条件查询默认就是根据相关性排序的。**

> **match查询**
> 
> ```javascript
> GET /indexName/_search
> {
>   "query": {
>     "match": {
>       "字段名": "检索内容"
>     }
>   }
> }
> ```

例如，我们搜索 “虹桥如家”，结果如下：

```javascript
GET /indexName/_search
{
  "query": {
    "match": {
      "name": "虹桥如家"
    }
  }
}
```

```java
[
  {
    "_score" : 17.850193,
    "_source" : {
      "name" : "虹桥如家酒店真不错",
    }
  },
  {
    "_score" : 12.259849,
    "_source" : {
      "name" : "外滩如家酒店真不错",
    }
  },
  {
    "_score" : 11.91091,
    "_source" : {
      "name" : "迪士尼如家酒店真不错",
    }
  }
]
```

在elasticsearch中，早期使用的打分算法是TF-IDF算法，公式如下：

![image-20210721190152134](https://i-blog.csdnimg.cn/blog_migrate/c38e04133ae988d26588cd799ad4d373.png)

> **tf词条频率算法**弊端：有些词条频率太高，几乎每个文档中都包含该词条，例如“了”、“的”之类的，给每个文档都加词条频率就没有意义。
> 
> **idf逆文档频率算法**改进了tf算法，降低高频分词的权重，提高低频分词的权重。
> 
> 例如搜索“睡觉了”，分词“睡觉”、“了”。“了”每个文档都包含，log(n/n)=1；“睡觉”只有1个文档包含，log(n/1)值就很大了。1和log(n)对比，可以得知“了”的权重低，“睡觉”的权重高。而低频词权重也不会太高，score=idf\*tf

在后来的5.1版本升级中，elasticsearch将算法改进为BM25算法，公式如下：

![image-20210721190416214](https://i-blog.csdnimg.cn/blog_migrate/c79c49df08d12d9d430fdc2cf4e0b5d3.png)

TF-IDF算法有一各缺陷，就是词条频率越高，文档得分也会越高，单个词条对文档影响较大。而BM25则会让单个词条的算分有一个上限，曲线更加平滑：

![image-20210721190907320](https://i-blog.csdnimg.cn/blog_migrate/5dd992a07c9d5ca0c2c374e62144b417.png)

小结：elasticsearch会根据词条和文档的相关度做打分，算法由两种：

-   **TF-IDF算法**
-   **BM25算法，**elasticsearch5.1版本后采用的算法

#### 1.5.2.算分函数查询，function\_score

根据相关度打分是比较合理的需求，但**合理的不一定是产品经理需要**的。

以百度为例，你搜索的结果中，并不是相关度越高排名越靠前，而是谁掏的钱多排名就越靠前。如图：

![image-20210721191144560](https://i-blog.csdnimg.cn/blog_migrate/c9a4ab708d603935f044606d494e04b9.png)

要想认为控制相关性算分，就需要利用elasticsearch中的function score 查询了。

**1）语法说明**

![image-20210721191544750](https://i-blog.csdnimg.cn/blog_migrate/28dec9d2b8a2fbe8a0ac8746b483c05c.png)

**function score 查询中包含四部分内容：**

-   **原始查询**条件：query部分，基于这个条件搜索文档，并且基于BM25算法给文档打分，**原始算分**（query score)
-   **过滤条件**：filter部分，符合该条件的文档才会重新算分
-   **算分函数**：符合filter条件的文档要根据这个函数做运算，得到的**函数算分**（function score），有四种函数
    -   weight：函数结果是常量
    -   field\_value\_factor：以文档中的某个字段值作为函数结果
    -   random\_score：以随机数作为函数结果
    -   script\_score：自定义算分函数算法
-   **运算模式**：算分函数的结果、原始查询的相关性算分，两者之间的运算方式，包括：
    -   multiply：相乘
    -   replace：用function score替换query score
    -   其它，例如：sum、avg、max、min

function score的运行流程如下：

-   1）根据**原始条件**查询搜索文档，并且计算相关性算分，称为**原始算分**（query score）
-   2）根据**过滤条件**，过滤文档
-   3）符合**过滤条件**的文档，基于**算分函数**运算，得到**函数算分**（function score）
-   4）将**原始算分**（query score）和**函数算分**（function score）基于**运算模式**做运算，得到最终结果，作为相关性算分。

因此，其中的关键点是：

-   过滤条件：决定哪些文档的算分被修改
-   算分函数：决定函数算分的算法
-   运算模式：决定最终算分结果

**2）示例**

需求：给“如家”这个品牌的酒店排名靠前一些

翻译一下这个需求，转换为之前说的四个要点：

-   原始条件：不确定，可以任意变化
-   过滤条件：brand = “如家”
-   算分函数：可以简单粗暴，直接给固定的算分结果，weight
-   运算模式：比如求和

因此最终的DSL语句如下：

```java
GET /hotel/_search
{
  "query": {
    "function_score": {
      "query": {  .... }, // 原始查询，可以是任意条件
      "functions": [ // 算分函数
        {
          "filter": { // 满足的条件，品牌必须是如家
            "term": {
              "brand": "如家"
            }
          },
          "weight": 2 // 算分权重为2，一般最大_score就是一点多，加上2就很多了
        }
      ],
      "boost_mode": "sum" // 加权模式，求和，默认是乘multiply
    }
  }
}
```

测试，在未添加算分函数时，如家得分如下：

![image-20210721193152520](https://i-blog.csdnimg.cn/blog_migrate/c1d355ed928543001fe921a6b719f4ea.png)

添加了算分函数后，如家得分就提升了：

![image-20210721193458182](https://i-blog.csdnimg.cn/blog_migrate/bda82c968bcbc356fe08eb791fae0e44.png)

3）小结

function score query定义的三要素是什么？

-   过滤条件：哪些文档要加分
-   算分函数：如何计算function score
-   加权方式：function score 与 query score如何运算

#### 1.5.3.布尔查询（多条件），bool

布尔查询是一个或多个查询子句的组合，每一个子句就是一个**子查询**。子查询的组合方式有：

-   **must：必须匹配**每个子查询，类似“与”。一般**搭配match匹配，查text类型。**
-   **should：**选择性匹配子查询，类似“或”
-   **must\_not：**必须不匹配，**不参与算分**，类似“非”
-   **filter：必须匹配**，**不参与算分**。一般**搭配term、range匹配，查数值、关键字、地理等**。

> -   **无子查询时布尔查询等同于match\_all，参与算法。**
> -   **不参与算分时（例如子查询只有filter和must\_not），所有\_score==0，此时再用乘法加权模式的算分函数查询就没意义了，因为所有\_score==0，乘权重还是0.**

比如在搜索酒店时，除了关键字搜索外，我们还可能根据品牌、价格、城市等字段做过滤：

![image-20210721193822848](https://i-blog.csdnimg.cn/blog_migrate/64e732182ecb0bfe87f283ebbdecf1b0.png)

每一个不同的字段，其查询的条件、方式都不一样，必须是多个不同的查询，而要组合这些查询，就必须用bool查询了。

需要注意的是，搜索时，参与**打分的字段越多，查询的性能也越差，建议多用must\_not和filter**。

因此**多条件查询时，建议这样做：**

-   **搜索框的关键字搜索，是全文检索查询，使用must查询，参与算分**
-   **其它过滤条件，采用filter查询。不参与算分**

1）语法示例：

> **注意：**
> 
> **布尔查询不算分数\_score时（例如只有filter没有must），此时算分函数加权模式是乘的话就使所有文档\_score为0，因为n\*0=0。布尔查询没有子查询时默认是match\_all查询所有，算分的。** 

```java
GET /hotel/_search
{
  "query": {
    "bool": {
      "must": [
        {"term": {"city": "上海" }}
      ],
      "should": [
        {"term": {"brand": "皇冠假日" }},
        {"term": {"brand": "华美达" }}
      ],
      "must_not": [
        { "range": { "price": { "lte": 500 } }}
      ],
      "filter": [
        { "range": {"score": { "gte": 45 } }}        #用户打分大于45
      ]
    }
  }
}
```

**2）示例**

需求：搜索名字包含“如家”，价格不高于400，在坐标31.21,121.5周围10km范围内的酒店。

分析：

-   名称搜索，属于全文检索查询，应该参与算分。放到must中
-   价格不高于400，用range查询，属于过滤条件，不参与算分。放到must\_not中
-   周围10km范围内，用geo\_distance查询，属于过滤条件，不参与算分。放到filter中

![image-20210721194744183](https://i-blog.csdnimg.cn/blog_migrate/347c6f3750df4628ab1388cde6841da5.png)

> **3）小结**
> 
> **bool查询有几种逻辑关系？**
> 
> -   must：必须匹配的条件，可以理解为“与”
> -   should：选择性匹配的条件，可以理解为“或”
> -   must\_not：必须不匹配的条件，不参与打分
> -   filter：必须匹配的条件，不参与打分

### 1.6 nested嵌入式查询

**es数组的扁平化处理：**

es存储**对象数组**时，它会将数组扁平化，也就是说**将对象数组的每个属性抽取出来**，作为一个数组。因此会出现查询紊乱的问题。 

**嵌入式查询示例：**

创建索引库

```bash
PUT /my-index-000001
{
  "mappings": {
    "properties": {
      "obj1": {
        "type": "nested"
      }
    }
  }
}
```

查询：

```bash
GET /my-index-000001/_search
{
  "query": {
    "nested": {
      "path": "obj1",
      "query": {
        "bool": {
          "must": [
            { "match": { "obj1.name": "blue" } },
            { "range": { "obj1.count": { "gt": 5 } } }
          ]
        }
      },
      "score_mode": "avg"
    }
  }
}
```

## 2.搜索结果处理

搜索的结果可以按照用户指定的方式去处理或展示。

### 2.0.搜索结果处理的整体样式

查询的DSL是一个大的JSON对象，包含下列属性：

-   query：查询条件
-   from和size：分页条件
-   sort：排序条件
-   highlight：高亮条件

**示例：**

![image-20210721203657850](https://i-blog.csdnimg.cn/blog_migrate/d5efc235ab2b8c0f5a834a8e4cf43f4a.png)

### 2.1.排序

elasticsearch默认是根据相关度算分（\_score）来排序，但是也支持自定义方式对搜索[结果排序](https://www.elastic.co/guide/en/elasticsearch/reference/current/sort-search-results.html "结果排序")。可以排序字段类型有：keyword类型（字母序排序）、数值类型、地理坐标类型（距离排序）、日期类型等。

#### 2.1.1.普通字段排序,sort

keyword、数值、日期类型排序的语法基本一致。

**语法**：

```java
GET /indexName/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "FIELD": "desc"  // 排序字段、排序方式ASC、DESC
    }
  ]
}
```

排序条件是一个数组，也就是可以写多个排序条件。按照声明的顺序，当第一个条件相等时，再按照第二个条件排序，以此类推

**示例**：

需求描述：酒店数据按照用户评价（score)降序排序，评价相同的按照价格(price)升序排序

![image-20210721195728306](https://i-blog.csdnimg.cn/blog_migrate/a96542af14de55f8b0adba46c838418d.png)

#### 2.1.2.地理坐标排序，\_geo\_distance

地理坐标排序略有不同。

**语法说明**：

```java
GET /indexName/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "_geo_distance" : {
          "FIELD" : "纬度，经度", // 文档中geo_point类型的字段名、目标坐标点
          "order" : "asc", // 排序方式
          "unit" : "km" // 排序的距离单位
      }
    }
  ]
}
```

这个查询的含义是：

-   指定一个坐标，作为目标点
-   计算每一个文档中，指定字段（必须是geo\_point类型）的坐标 到目标点的距离是多少
-   根据距离排序

**示例：**

需求描述：实现对酒店数据按照到你的位置坐标的距离升序排序

提示：获取你的位置的经纬度的方式：https://lbs.amap.com/demo/jsapi-v2/example/map/click-to-get-lnglat/

假设我的位置是：31.034661，121.612282，寻找我周围距离最近的酒店。

![image-20210721200214690](https://i-blog.csdnimg.cn/blog_migrate/84985c4fe17f4c5c9122bb0c0d7dd6d8.png)

### 2.2.分页

elasticsearch 默认情况下只返回top10的数据。而如果要查询更多数据就需要修改分页参数了。elasticsearch中通过修改from、size参数来控制要返回的分页结果：

-   from：从第几个文档开始
-   size：总共查询几个文档

类似于mysql中的`limit ?, ?`

#### 2.2.1.基本的分页，from+size

索引是从0开始的。 

分页的基本语法如下：

```java
GET /hotel/_search
{
  "query": {
    "match_all": {}
  },
  "from": 0, // 分页开始的位置，默认为0
  "size": 10, // 期望获取的文档总数
  "sort": [
    {"price": "asc"}
  ]
}
```

#### 2.2.2.深度分页问题，after search

> **集群查询，深度分页问题分析：**
> 
> 现在，我要查询990~1000的数据，查询逻辑要这么写：
> 
> ```java
> GET /hotel/_search
> {
>   "query": {
>     "match_all": {}
>   },
>   "from": 990, // 分页开始的位置，默认为0
>   "size": 10, // 期望获取的文档总数
>   "sort": [
>     {"price": "asc"}
>   ]
> }
> ```
> 
> 这里是查询990开始的数据，也就是 第990~第1000条 数据。
> 
> 不过，elasticsearch内部分页时，必须先查询 0~1000条，然后截取其中的990 ~ 1000的这10条：
> 
> ![image-20210721200643029](https://i-blog.csdnimg.cn/blog_migrate/7f99809bcea2167a769761d54e02cd7a.png)
> 
> 查询TOP1000，如果es是单点模式，这并无太大影响。
> 
> 但是elasticsearch将来一定是集群，例如我集群有5个节点，我要查询TOP1000的数据，并不是每个节点查询200条就可以了。
> 
> 因为节点A的TOP200，在另一个节点可能排到10000名以外了。

因此**要想获取整个集群的TOP1000，必须先查询出每个节点的TOP1000，汇总结果后，重新排名，重新截取TOP1000。**

![image-20210721201003229](https://i-blog.csdnimg.cn/blog_migrate/2813dce918d0eef65a2c7bc4b7e0e097.png)

那如果我要查询9900~10000的数据呢？是不是要先查询TOP10000呢？那每个节点都要查询10000条？汇总到内存中？

当查询分页深度较大时，汇总数据过多，对内存和CPU会产生非常大的压力，因此**elasticsearch会禁止from+ size 超过10000的请求。**例如"form":9991,"size":10会报错。

针对深度分页，ES提供了**两种解决方案**，[官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/current/paginate-search-results.html "官方文档")：

-   **search after：**分页时需要排序，原理是从上一次的排序值开始，查询下一页数据。官方**推荐**使用的方式。没有查询上限（单次查询的size不超过10000，,只能向后逐页查询，不支持随机翻页
-   scroll：原理将排序后的文档id形成快照，保存在内存。官方已经**不推荐**使用。

#### 2.2.3.小结，三种分页

分页查询的常见实现方案以及优缺点：

-   `from + size`：
    
    -   优点：支持随机翻页
    -   缺点：深度分页问题，默认查询上限（from + size）是10000
    -   场景：百度、京东、谷歌、淘宝这样的随机翻页搜索
-   `after search`：
    
    -   优点：没有查询上限（单次查询的size不超过10000）
    -   缺点：只能向后逐页查询，不支持随机翻页
    -   场景：没有随机翻页需求的搜索，例如手机向下滚动翻页
-   `scroll`：
    
    -   优点：没有查询上限（单次查询的size不超过10000）
    -   缺点：会有额外内存消耗，并且搜索结果是非实时的
    -   场景：海量数据的获取和迁移。从ES7.1开始不推荐，建议用 after search方案。

### 2.3.高亮

#### 2.3.1.高亮原理

什么是高亮显示呢？

我们在百度，京东搜索时，关键字会变成红色，比较醒目，这叫高亮显示：

![image-20210721202705030](https://i-blog.csdnimg.cn/blog_migrate/8e5a4d8c723d4902137c7863a5248a00.png)

高亮显示的实现分为两步：

-   **1）给文档中的所有关键字都添加一个标签，例如`<em>`标签**
-   **2）页面给`<em>`标签编写CSS样式**

> <em> 默认样式：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bec9a08e37b8362dfebd0f4b5e698043.png)

#### 2.3.2.实现高亮

**高亮的语法**：

```java
GET /hotel/_search
{
  "query": {
    "match": {
      "FIELD": "TEXT" // 查询条件，高亮一定要使用全文检索查询
    }
  },
  "highlight": {
    "fields": { // 指定要高亮的字段
      "FIELD": {
        "pre_tags": "<em>",  // 用来标记高亮字段的前置标签
        "post_tags": "</em>" // 用来标记高亮字段的后置标签
      }
    }
  }
}
```

> **注意：**
> 
> -   高亮是对关键字高亮，因此**搜索条件必须带有关键字**，而不能是范围这样的查询。
> -   **默认**情况下，**高亮的字段，必须与搜索指定的字段一致**，否则无法高亮
> -   如果要对**非搜索字段高亮**，则需要添加一个属性：**required\_field\_match=false**

**示例**：

![image-20210721203349633](https://i-blog.csdnimg.cn/blog_migrate/c342fdaf4bf50ced52e189ea40b2e59d.png)

## 3.RestClient查询文档

文档的查询同样适用昨天学习的 RestHighLevelClient对象，基本步骤包括：

-   1）准备Request对象
-   2）准备请求参数
-   3）发起请求
-   4）解析响应

### 3.1.快速入门，查询所有，match\_all

我们以match\_all查询为例

#### 3.1.1.发起查询请求

![image-20210721203950559](https://i-blog.csdnimg.cn/blog_migrate/8f463854070335f0010a547f123d7275.png)

> **回顾根据id查询**是GetRequest:
> 
> ```java
> @Test
> void testGetDocumentById() throws IOException {
>     // 1.准备Request
>     GetRequest request = new GetRequest("hotel", "61082");
>     // 2.发送请求，得到响应
>     GetResponse response = client.get(request, RequestOptions.DEFAULT);
>     // 3.解析响应结果。如果是getSource()方法则获得的是Map<String,Object>
>     String json = response.getSourceAsString();
>  
>     HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
>     System.out.println(hotelDoc);
> }
> ```

代码解读：

-   第一步，创建`SearchRequest`对象，指定索引库名
    
-   第二步，利用`request.source()`构建DSL，DSL中可以包含查询、分页、排序、高亮等
    
    -   `query()`：代表查询条件，利用`QueryBuilders.matchAllQuery()`构建一个match\_all查询的DSL
-   第三步，利用client.search()发送请求，得到响应
    

这里关键的API有两个，一个是`request.source()`，其中包含了查询、排序、分页、高亮等所有功能：

![image-20210721215640790](https://i-blog.csdnimg.cn/blog_migrate/2dda96ceea18a1474970d0ef562543a2.png)

另一个是`QueryBuilders`，其中包含match、term、function\_score、bool等各种查询：

![image-20210721215729236](https://i-blog.csdnimg.cn/blog_migrate/b41e3ac002ab2ee97edbc2620aa2411d.png)

#### 3.1.2.解析响应

响应结果的解析：

![image-20210721214221057](https://i-blog.csdnimg.cn/blog_migrate/e1e4942e59ef4e606c71b97b0437f7d7.png)

elasticsearch返回的结果是一个JSON字符串，结构包含：

-   `hits`：命中的结果
    -   `total`：总条数，其中的value是具体的总条数值
    -   `max_score`：所有结果中得分最高的文档的相关性算分
    -   `hits`：搜索结果的文档数组，其中的每个文档都是一个json对象
        -   `_source`：文档中的原始数据，也是json对象

因此，我们解析响应结果，就是逐层解析JSON字符串，流程如下：

-   `SearchHits`：通过response.getHits()获取，就是JSON中的最外层的hits，代表命中的结果
    -   `SearchHits#getTotalHits().value`：获取总条数信息
    -   `SearchHits#getHits()`：获取SearchHit数组，也就是文档数组
        -   `SearchHit#getSourceAsString()`：获取文档结果中的\_source，也就是原始的json文档数据

#### 3.1.3.完整代码

> 之前已经导入了依赖和创建了客户端，忘了的话参考上篇文章：
> 
> [elasticsearch基础1——索引、文档\_elasticsearch 索引文档\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126807267?spm=1001.2014.3001.5501 "elasticsearch基础1——索引、文档_elasticsearch 索引文档_vincewm的博客-CSDN博客")
> 
> ```XML
> 
>         <dependency>
>             <groupId>org.elasticsearch.client</groupId>
>             <artifactId>elasticsearch-rest-high-level-client</artifactId>
>         </dependency>
> ```
> 
> ```java
> 
> @SpringBootTest
> public class HotelDocumentTest {
>     @Autowired
>     private IHotelService hotelService;
>  
>     private RestHighLevelClient client;
>  
>     @BeforeEach
>     void setUp() {
>         this.client = new RestHighLevelClient(RestClient.builder(
>                 HttpHost.create("http://192.168.150.101:9200")
>         ));
>     }
>  
>     @AfterEach
>     void tearDown() throws IOException {
>         this.client.close();
>     }
> }
>  
> ```

```java
@Test
void testMatchAll() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL。QueryBuilders构造各种查询条件
    request.source()
        .query(QueryBuilders.matchAllQuery());
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);

    // 4.解析响应
    handleResponse(response);
}

private void handleResponse(SearchResponse response) {
    // 4.解析响应。参看json从外到内解析
    SearchHits searchHits = response.getHits();
    // 4.1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("数量：" + total );
    // 4.2.文档数组
    SearchHit[] hits = searchHits.getHits();
    // 4.3.遍历
    for (SearchHit hit : hits) {
        // 获取文档source
        String json = hit.getSourceAsString();
        // 反序列化
        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
        System.out.println("hotelDoc = " + hotelDoc);
    }
}
```

**测试结果：**没有指定size，只显示前十条数据。

![](https://i-blog.csdnimg.cn/blog_migrate/32c9a7e0e49510d6ed271d15d08f2ade.png)

> **回顾客户端代码：**
> 
> ```java
>     private RestHighLevelClient client;
>     @BeforeEach
>     void setup(){
>         this.client=new RestHighLevelClient(RestClient.builder(
>                 HttpHost.create("http://192.168.200.130:9200")
>         ));
>     }
>     @AfterEach
>     void tearDown() throws IOException {
>         this.client.close();
>     }
> ```
> 
> **回顾根据id查询**是GetRequest:
> 
> ```java
> @Test
> void testGetDocumentById() throws IOException {
>     // 1.准备Request
>     GetRequest request = new GetRequest("hotel", "61082");
>     // 2.发送请求，得到响应
>     GetResponse response = client.get(request, RequestOptions.DEFAULT);
>     // 3.解析响应结果。如果是getSource()方法则获得的是Map<String,Object>
>     String json = response.getSourceAsString();
>  
>     HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
>     System.out.println(hotelDoc);
> }
> ```

#### 3.1.4.小结

查询的基本步骤是：

1.  创建SearchRequest对象
    
2.  准备Request.source()，也就是DSL。
    
    ① QueryBuilders来构建查询条件
    
    ② 传入Request.source() 的 query() 方法
    
3.  发送请求，得到结果
    
4.  解析结果（参考JSON结果，从外到内，逐层解析）
    

### 3.2.match查询

全文检索的match和multi\_match查询与match\_all的API基本一致。差别是查询条件，也就是query的部分。

![image-20210721215923060](https://i-blog.csdnimg.cn/blog_migrate/09d6f6794eaae19f7b64c22ab8b225bd.png)

因此，Java代码上的差异主要是request.source().query()中的参数了。同样是利用QueryBuilders提供的方法：

![image-20210721215843099](https://i-blog.csdnimg.cn/blog_migrate/7d8c5848c1a3179d8773de7633217789.png)

而结果解析代码则完全一致，可以抽取并共享。

完整代码如下：

```java
@Test
void testMatch() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    request.source()
        .query(QueryBuilders.matchQuery("all", "如家"));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```

### 3.3.精确查询

精确查询主要是两者：

-   term：词条精确匹配
-   range：范围查询

与之前的查询相比，差异同样在查询条件，其它都一样。

查询条件构造的API如下：

![image-20210721220305140](https://i-blog.csdnimg.cn/blog_migrate/8b58812bd42d479c3c30eaee395b8caa.png)

### 3.4.布尔查询

布尔查询是用must、must\_not、filter等方式组合其它查询，代码示例如下：

![image-20210721220927286](https://i-blog.csdnimg.cn/blog_migrate/5083d66554c21f3c0688eb9e78a2d13b.png)

可以看到，API与其它查询的差别同样是在查询条件的构建，QueryBuilders，结果解析等其他代码完全不变。

完整代码如下：

```java
@Test
void testBool() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.准备BooleanQuery
    BoolQueryBuilder boolQuery = QueryBuilders.boolQuery();
    // 2.2.添加term
    boolQuery.must(QueryBuilders.termQuery("city", "杭州"));
    // 2.3.添加range
    boolQuery.filter(QueryBuilders.rangeQuery("price").lte(250));

    request.source().query(boolQuery);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```

> **注意：**
> 
> **布尔查询不算分数\_score时（例如只有filter没有must），此时算分函数加权模式是乘的话就使所有文档\_score为0，因为n\*0=0。布尔查询没有子查询时默认是match\_all查询所有，算分的。** 

### 3.5.排序、分页

**排序、分页是搜索结果的操作，所以是对request.source().xx()不是 request.source().query().xx()**

搜索结果的排序和分页是与query同级的参数，因此同样是使用request.source()来设置。

对应的API如下：

![image-20210721221121266](https://i-blog.csdnimg.cn/blog_migrate/928d5bf9b8eeabe8695a3df316609c7e.png)

完整代码示例：

```java
@Test
void testPageAndSort() throws IOException {
    // 页码，每页大小
    int page = 1, size = 5;

    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    //request.source().query(QueryBuilders.matchQuery("all", "上海")).sort("price", SortOrder.ASC).from((currentPage-1)*size).size(size);    //也可以链式编程一步到位
    // 2.1.query
    request.source().query(QueryBuilders.matchAllQuery());
    // 2.2.排序 sort
    request.source().sort("price", SortOrder.ASC);
    // 2.3.分页 from、size
    request.source().from((page - 1) * size).size(5);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```

### 3.6.高亮

高亮的代码与之前代码差异较大，有两点：

-   查询的DSL：其中除了查询条件，还需要添加高亮条件，同样是与query同级。
-   结果解析：结果除了要解析\_source文档数据，还要解析高亮结果

#### 3.6.1.高亮请求构建

高亮请求的构建API如下：

![image-20210721221744883](https://i-blog.csdnimg.cn/blog_migrate/d7f02d49ee19966644f090125370c416.png)

上述代码省略了查询条件部分，但是大家不要忘了：高亮查询必须使用全文检索查询，并且要有搜索关键字，将来才可以对关键字高亮。

完整代码如下：

```java
@Test
void testHighlight() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.query
    request.source().query(QueryBuilders.matchQuery("all", "如家"));
    // 2.2.高亮
    request.source().highlighter(new HighlightBuilder().field("name").requireFieldMatch(false));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```

#### 3.6.2.高亮结果解析

**高亮的结果与查询的文档结果默认是分离的**，并不在一起。

因此解析高亮的代码需要额外处理：

![image-20210721222057212](https://i-blog.csdnimg.cn/blog_migrate/c6856f395dda5a7777ea7894824b7980.png)

代码解读：

-   第一步：从结果中获取source。hit.getSourceAsString()，这部分是非高亮结果，json字符串。还需要反序列为HotelDoc对象
-   第二步：获取高亮结果。hit.getHighlightFields()，返回值是一个Map，key是高亮字段名称，值是HighlightField对象，代表高亮值
-   第三步：从map中根据高亮字段名称，获取高亮字段值对象HighlightField
-   第四步：从HighlightField中获取Fragments，并且转为字符串。这部分就是真正的高亮字符串了
-   第五步：用高亮的结果替换HotelDoc中的非高亮结果

完整代码如下：

hit.getHighlightFields().get("name") .getFragments()\[0\].toString()

```java
private void handleResponse(SearchResponse response) {
    // 4.解析响应
    SearchHits searchHits = response.getHits();
    // 4.1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("共搜索到" + total + "条数据");
    // 4.2.文档数组
    SearchHit[] hits = searchHits.getHits();
    // 4.3.遍历
    for (SearchHit hit : hits) {
        // 获取文档source
        String json = hit.getSourceAsString();
        // 反序列化
        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
        // 获取高亮结果
        Map<String, HighlightField> highlightFields = hit.getHighlightFields();
        if (!CollectionUtils.isEmpty(highlightFields)) {    //不是null且size>0
            // 根据字段名获取高亮结果
            HighlightField highlightField = highlightFields.get("name");
            if (highlightField != null) {
                // 获取高亮值。highlightField还有个getName()方法，获取当前字段名
                String name = highlightField.getFragments()[0].string();
                // 覆盖非高亮结果
                hotelDoc.setName(name);
            }
        }
        System.out.println("hotelDoc = " + hotelDoc);
    }
}
```

## 4.黑马旅游案例

### 4.0.项目准备和预览 

我们实现四部分功能：

-   酒店搜索和分页
-   酒店结果过滤
-   我周边的酒店
-   酒店竞价排名

> 创建索引库、 springboot项目、MySQL数据库表、yml配置、导入依赖等操作在上一篇文章已经完成了，具体参考下面文章的第四节和第五节：
> 
> [elasticsearch基础1——索引、文档\_elasticsearch 索引文档\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126807267?spm=1001.2014.3001.5501 "elasticsearch基础1——索引、文档_elasticsearch 索引文档_vincewm的博客-CSDN博客")

**用户端hotel-demo项目：**

![image-20210721223159598](https://i-blog.csdnimg.cn/blog_migrate/a08c432c46c6b2dd99bb0271b750bd63.png)

搜索框候选栏可以补全拼音或文字为“商圈”、“品牌”等数据：

![](https://i-blog.csdnimg.cn/blog_migrate/3732772091693d0e3536f83218836cd8.png)

标签随着搜索结果变化

![](https://i-blog.csdnimg.cn/blog_migrate/a3e599970a04a10359af0dc03bd91d1e.png)

**后台管理端hotel-admin项目：**

![](https://i-blog.csdnimg.cn/blog_migrate/c230ccec74c9965c1a5ec278ac55369c.png)

### 4.1.酒店搜索和分页

案例需求：实现黑马旅游的酒店搜索功能，完成关键字搜索和分页

#### 4.1.1.需求分析

在项目的首页，有一个大大的搜索框，还有分页按钮：

![image-20210721223859419](https://i-blog.csdnimg.cn/blog_migrate/de2489ec2b64f985917fa0ee60ec2b5c.png)

点击搜索按钮，可以看到浏览器控制台发出了请求：

![image-20210721224033789](https://i-blog.csdnimg.cn/blog_migrate/4ec778364f96ce544b194d3d988a362a.png)

请求参数如下：

![image-20210721224112708](https://i-blog.csdnimg.cn/blog_migrate/56fc12b92ed2b86ece0b620b728b7427.png)

由此可以知道，我们这个请求的信息如下：

-   请求方式：POST
-   请求路径：/hotel/list
-   请求参数：JSON对象，包含4个字段：
    -   key：搜索关键字
    -   page：页码
    -   size：每页大小
    -   sortBy：排序，目前暂不实现
-   返回值：分页查询，需要返回分页结果PageResult，包含两个属性：
    -   `total`：总条数
    -   `List<HotelDoc>`：当前页的数据

因此，我们实现业务的流程如下：

-   步骤一：定义实体类，接收请求参数的JSON对象
-   步骤二：编写controller，接收页面的请求
-   步骤三：编写业务实现，利用RestHighLevelClient实现搜索、分页

#### 4.1.2.定义分页请求参数和响应结果实体类

实体类有两个，一个是前端的请求参数实体，一个是服务端应该返回的响应结果实体。

**1）请求参数**

前端请求的json结构如下：

```java
{
    "key": "搜索关键字",
    "page": 1,
    "size": 3,
    "sortBy": "default"
}
```

因此，我们在`cn.itcast.hotel.pojo`包下定义一个实体类：

```java
package cn.itcast.hotel.pojo;

import lombok.Data;

@Data
public class RequestParams {
    private String key;
    private Integer page;
    private Integer size;
    private String sortBy;
}
```

**2）返回值**

 ![](https://i-blog.csdnimg.cn/blog_migrate/b2e02d029be4e2ce50da490078553147.png)

分页查询，需要返回分页结果PageResult，包含两个属性：

-   `total`：总条数
-   `List<HotelDoc>`：当前页的数据

因此，我们在`cn.itcast.hotel.pojo`中定义返回结果：

```java
package cn.itcast.hotel.pojo;

import lombok.Data;

import java.util.List;

@Data
public class PageResult {
    private Long total;
    private List<HotelDoc> hotels;

    public PageResult() {
    }

    public PageResult(Long total, List<HotelDoc> hotels) {
        this.total = total;
        this.hotels = hotels;
    }
}
```

#### 4.1.3.定义controller

定义一个HotelController，声明查询接口，满足下列要求：

-   请求方式：Post
-   请求路径：/hotel/list
-   请求参数：对象，类型为RequestParam
-   返回值：PageResult，包含两个属性
    -   `Long total`：总条数
    -   `List<HotelDoc> hotels`：酒店数据

因此，我们在`cn.itcast.hotel.web`中定义HotelController：

```java
@RestController
@RequestMapping("/hotel")
public class HotelController {

    @Autowired
    private IHotelService hotelService;
	// 搜索酒店数据
    @PostMapping("/list")
    public PageResult search(@RequestBody RequestParams params){
        return hotelService.search(params);
    }
}
```

#### 4.1.4.实现搜索业务

我们在controller调用了IHotelService，并没有实现该方法，因此下面我们就在IHotelService中定义方法，并且去实现业务逻辑。

1）在`cn.itcast.hotel.service`中的`IHotelService`接口中定义一个方法：

```java
/**
 * 根据关键字搜索酒店信息
 * @param params 请求参数对象，包含用户输入的关键字 
 * @return 酒店文档列表
 */
PageResult search(RequestParams params);
```

2）实现搜索业务，肯定离不开RestHighLevelClient，我们需要把它注册到Spring中作为一个Bean。在`cn.itcast.hotel`中的`HotelDemoApplication`中声明这个Bean：

```java
@Bean
public RestHighLevelClient client(){
    return  new RestHighLevelClient(RestClient.builder(
        HttpHost.create("http://192.168.150.101:9200")
    ));
}
```

3）在`cn.itcast.hotel.service.impl`中的`HotelService`中实现search方法：

```java
@Override
public PageResult search(RequestParams params) {
    try {
        // 1.准备Request
        SearchRequest request = new SearchRequest("hotel");
        // 2.准备DSL
        // 2.1.query
        String key = params.getKey();
        if(!StringUtils.isEmpty(key)) request.source().query(QueryBuilders.matchQuery("all",key));
        else request.source().query(QueryBuilders.matchAllQuery());

        // 2.2.分页
        int page = params.getPage();
        int size = params.getSize();
        request.source().from((page - 1) * size).size(size);

        // 3.发送请求
        SearchResponse response = client.search(request, RequestOptions.DEFAULT);
        // 4.解析响应
        return handleResponse(response);
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}

// 结果解析
private PageResult handleResponse(SearchResponse response) {
    // 4.解析响应
    SearchHits searchHits = response.getHits();
    // 4.1.获取总条数
    long total = searchHits.getTotalHits().value;
    // 4.2.文档数组
    SearchHit[] hits = searchHits.getHits();
    // 4.3.遍历
    List<HotelDoc> hotels = new ArrayList<>();
    for (SearchHit hit : hits) {
        // 获取文档source
        String json = hit.getSourceAsString();
        // 反序列化
        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
		// 放入集合
        hotels.add(hotelDoc);
    }
    // 4.4.封装返回
    return new PageResult(total, hotels);
}
```

### 4.2.酒店结果过滤

需求：添加品牌、城市、星级、价格等过滤功能

#### 4.2.1.需求分析

在页面搜索框下面，会有一些过滤项：

![image-20210722091940726](https://i-blog.csdnimg.cn/blog_migrate/44e9e4d8c1adcc29845e548d575ce27c.png)

传递的参数如图：

![image-20210722092051994](https://i-blog.csdnimg.cn/blog_migrate/bc94f900255b38275440973266384c0b.png)

包含的过滤条件有：

-   brand：品牌值
-   city：城市
-   minPrice~maxPrice：价格范围
-   starName：星级

我们需要做两件事情：

-   修改请求参数的对象RequestParams，接收上述参数
-   修改业务逻辑，在搜索条件之外，添加一些过滤条件

#### 4.2.2.查询条件实体类增加成员变量

修改在`cn.itcast.hotel.pojo`包下的实体类RequestParams：

```java
@Data
public class RequestParams {
    private String key;
    private Integer page;
    private Integer size;
    private String sortBy;
    // 下面是新增的过滤条件参数
    private String city;
    private String brand;
    private String starName;
    private Integer minPrice;
    private Integer maxPrice;
}
```

#### 4.2.3.修改搜索业务，布尔查询

在HotelService的search方法中，只有一个地方需要修改：requet.source().query( … )其中的查询条件。

在之前的业务中，只有match查询，根据关键字搜索，现在要添加条件过滤，包括：

-   品牌过滤：是keyword类型，用term查询
-   星级过滤：是keyword类型，用term查询
-   价格过滤：是数值类型，用range查询
-   城市过滤：是keyword类型，用term查询

**多个查询条件组合**，肯定是**bool查询**来组合：

-   关键字搜索放到must中，参与算分
-   其它过滤条件放到filter中，不参与算分

> **match只能单条件查询，multi\_match只能单条件查询多字段，所以这里只能用复合查询中的布尔查询。**

因为条件构建的逻辑比较复杂，**将基础查询代码封装为一个函数：**

![image-20210722092935453](https://i-blog.csdnimg.cn/blog_migrate/b7c08dc8d5c3edbc416c51f5452b0141.png)

buildBasicQuery的代码如下：

> **注意：**
> 
> -   **多条件查询用bool查询，必须要保证至少有一个条件存在**
> -   **bool查询能用filter就别用must，因为filter不参与算分，性能快。**
> -   **bool查询的must常用于match查text类型，filter****常用于查其他类型。**

```java
private void buildBasicQuery(RequestParams params, SearchRequest request) {
    // 1.构建BooleanQuery
    BoolQueryBuilder boolQuery = QueryBuilders.boolQuery();
    // 2.关键字搜索
    String key = params.getKey();
    if (key == null || "".equals(key)) {    //必须要保证至少有一个条件
        boolQuery.must(QueryBuilders.matchAllQuery());
    } else {    
        boolQuery.must(QueryBuilders.matchQuery("all", key));
    }
    // 3.城市条件
    if (params.getCity() != null && !params.getCity().equals("")) {
        boolQuery.filter(QueryBuilders.termQuery("city", params.getCity()));
    }
    // 4.品牌条件。品牌的es是keyword类型，不分词，用must(match)也可以，但filter不参与算分，性能快
    if (params.getBrand() != null && !params.getBrand().equals("")) {
        boolQuery.filter(QueryBuilders.termQuery("brand", params.getBrand()));
    }
    // 5.星级条件
    if (params.getStarName() != null && !params.getStarName().equals("")) {
        boolQuery.filter(QueryBuilders.termQuery("starName", params.getStarName()));
    }
	// 6.价格
    if (params.getMinPrice() != null && params.getMaxPrice() != null) {
        boolQuery.filter(QueryBuilders
                         .rangeQuery("price")
                         .gte(params.getMinPrice())
                         .lte(params.getMaxPrice())
                        );
    }
	// 7.放入source
    request.source().query(boolQuery);
}
```

### 4.3.我周边的酒店

需求：我附近的酒店

#### 4.3.1.需求分析

在酒店列表页的右侧，有一个小地图，点击地图的定位按钮（谷歌浏览器不知道什么原因无法定位，测试edge浏览器可以），地图会找到你所在的位置：

![image-20210722093414542](https://i-blog.csdnimg.cn/blog_migrate/909e97c02a3b958853990e8eb96ff8ac.png)

并且，在前端会发起查询请求，将你的坐标发送到服务端：

![image-20210722093642382](https://i-blog.csdnimg.cn/blog_migrate/a75f223bac3c18e9e5b8dd72dee41a69.png)

我们要做的事情就是基于这个location坐标，然后按照距离对周围酒店排序。实现思路如下：

-   修改RequestParams参数，接收location字段
-   修改search方法业务逻辑，如果location有值，添加根据geo\_distance排序的功能

#### 4.3.2.查询条件实体类增加成员变量

修改在`cn.itcast.hotel.pojo`包下的实体类RequestParams：

```java
package cn.itcast.hotel.pojo;

import lombok.Data;

@Data
public class RequestParams {
    private String key;
    private Integer page;
    private Integer size;
    private String sortBy;
    private String city;
    private String brand;
    private String starName;
    private Integer minPrice;
    private Integer maxPrice;
    // 我当前的地理坐标
    private String location;
}

```

#### 4.3.3.距离排序API

我们以前学习过排序功能，包括两种：

-   普通字段排序
-   地理坐标排序

我们只讲了普通字段排序对应的java写法。地理坐标排序只学过DSL语法，如下：

```java
GET /indexName/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "price": "asc"  
    },
    {
      "_geo_distance" : {
          "FIELD" : "纬度，经度",
          "order" : "asc",
          "unit" : "km"
      }
    }
  ]
}
```

对应的java代码示例：

![image-20210722095227059](https://i-blog.csdnimg.cn/blog_migrate/726375d3de6d1518c00bbcf00ad4fd27.png)

#### 4.3.4.添加距离排序

在`cn.itcast.hotel.service.impl`的`HotelService`的`search`方法中，添加一个排序功能：

![image-20210722095902314](https://i-blog.csdnimg.cn/blog_migrate/82fbf026e891ca1cda5bd9940b7c2818.png)

完整代码：

> **默认排序是按照距离排序** 

```java
@Override
public PageResult search(RequestParams params) {
    try {
        // 1.准备Request
        SearchRequest request = new SearchRequest("hotel");
        // 2.准备DSL
        // 2.1.query
        buildBasicQuery(params, request);

        // 2.2.分页
        int page = params.getPage();
        int size = params.getSize();
        request.source().from((page - 1) * size).size(size);

        // 2.3.排序
        String location = params.getLocation();
        if (location != null && !location.equals("")) {
            request.source().sort(SortBuilders
                                  .geoDistanceSort("location", new GeoPoint(location))    //注意第二个参数是GeoPoint对象，不是String类型
                                  .order(SortOrder.ASC)
                                  .unit(DistanceUnit.KILOMETERS)
                                 );
        }

        // 3.发送请求
        SearchResponse response = client.search(request, RequestOptions.DEFAULT);
        // 4.解析响应
        return handleResponse(response);
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}
```

#### 4.3.5.排序距离显示

重启服务后，测试我的酒店功能：

![image-20210722100040674](https://i-blog.csdnimg.cn/blog_migrate/ca20f324985ca40d25248aa9377a1b4f.png)

发现确实可以实现对我附近酒店的排序，不过并没有看到酒店到底距离我多远，这该怎么办？

**按距离排序完成后**，页面还要获取我附近每个酒店的**具体距离值**，这个值在响应结果中是独立的：

![image-20210722095648542](https://i-blog.csdnimg.cn/blog_migrate/9adbab7b498e6f80a5305fd9a51d33b9.png)

因此，我们在结果解析阶段，除了解析source部分以外，还要得到sort部分，也就是排序的距离，然后放到响应结果中。

我们要做两件事：

-   修改HotelDoc，添加排序距离字段，用于页面显示
-   修改HotelService类中的handleResponse方法，添加对sort值的获取

1）修改HotelDoc类，添加距离字段

```java
package cn.itcast.hotel.pojo;

import lombok.Data;
import lombok.NoArgsConstructor;


@Data
@NoArgsConstructor
public class HotelDoc {
    private Long id;
    private String name;
    private String address;
    private Integer price;
    private Integer score;
    private String brand;
    private String city;
    private String starName;
    private String business;
    private String location;
    private String pic;
    // 排序时的 距离值
    private Object distance;

    public HotelDoc(Hotel hotel) {
        this.id = hotel.getId();
        this.name = hotel.getName();
        this.address = hotel.getAddress();
        this.price = hotel.getPrice();
        this.score = hotel.getScore();
        this.brand = hotel.getBrand();
        this.city = hotel.getCity();
        this.starName = hotel.getStarName();
        this.business = hotel.getBusiness();
        this.location = hotel.getLatitude() + ", " + hotel.getLongitude();
        this.pic = hotel.getPic();
    }
}

```

2）修改HotelService中的handleResponse方法

![image-20210722100613966](https://i-blog.csdnimg.cn/blog_migrate/8280ac702f511b4b70d05aed3c6f09f7.png)

> 为什么跟source并列的**sort值是数组？**
> 
> 因为可能根据多个字段排序。

重启后测试，发现页面能成功显示距离了：

![image-20210722100838604](https://i-blog.csdnimg.cn/blog_migrate/2e0fb0072f7165d191781c7ef772dd7c.png)

### 4.4.酒店竞价排名

需求：让指定的酒店在搜索结果中排名置顶

#### 4.4.1.需求分析

要让指定酒店在搜索结果中排名置顶，效果如图：

![image-20210722100947292](https://i-blog.csdnimg.cn/blog_migrate/951e4810b240d8d97d05645d67e3667f.png)

页面会给指定的酒店添加**广告**标记。

那怎样才能让指定的酒店排名置顶呢？

我们之前学习过的function\_score查询可以影响算分，算分高了，自然排名也就高了。而function\_score包含3个要素：

-   过滤条件：哪些文档要加分
-   算分函数：如何计算function score
-   加权方式：function score 与 query score如何运算

这里的需求是：让**指定酒店**排名靠前。因此我们需要给这些酒店添加一个标记，这样在过滤条件中就可以**根据这个标记来判断，是否要提高算分**。

比如，我们给酒店添加一个字段：isAD，Boolean类型：

-   true：是广告
-   false：不是广告

这样function\_score包含3个要素就很好确定了：

-   过滤条件：判断isAD 是否为true
-   算分函数：我们可以用最简单暴力的weight，固定加权值
-   加权方式：可以用默认的相乘，大大提高算分

因此，业务的实现步骤包括：

1.  给HotelDoc类添加isAD字段，Boolean类型
    
2.  挑选几个你喜欢的酒店，给它的文档数据添加isAD字段，值为true
    
3.  修改search方法，添加function score功能，给isAD值为true的酒店增加权重
    

#### 4.4.2.HotelDoc实体类添加成员变量isAD

给`cn.itcast.hotel.pojo`包下的HotelDoc类添加isAD字段：

![image-20210722101908062](https://i-blog.csdnimg.cn/blog_migrate/48f0b14c7441296baadf959a0cefeb60.png)

#### 4.4.3.给文档添加广告标记

接下来，我们挑几个酒店，添加isAD字段，设置为true：

```java
POST /hotel/_update/1902197537
{
    "doc": {
        "isAD": true
    }
}
POST /hotel/_update/2056126831
{
    "doc": {
        "isAD": true
    }
}
POST /hotel/_update/1989806195
{
    "doc": {
        "isAD": true
    }
}
POST /hotel/_update/2056105938
{
    "doc": {
        "isAD": true
    }
}
```

#### 4.4.4.基础查询业务添加算分函数查询

接下来我们就要修改查询条件了。之前是用的boolean 查询，现在要改成function\_socre查询。

function\_score查询结构如下：

![image-20210721191544750](https://i-blog.csdnimg.cn/blog_migrate/28dec9d2b8a2fbe8a0ac8746b483c05c.png)

对应的JavaAPI如下：

![image-20210722102850818](https://i-blog.csdnimg.cn/blog_migrate/fc672b866b35ba900f41860837071c6a.png)

我们可以将之前写的boolean查询作为**原始查询**条件放到query中，接下来就是添加**过滤条件**、**算分函数**、**加权模式**了。所以原来的代码依然可以沿用。

修改`cn.itcast.hotel.service.impl`包下的`HotelService`类中的`buildBasicQuery`方法，添加算分函数查询：

```java
private void buildBasicQuery(RequestParams params, SearchRequest request) {
    // 1.构建BooleanQuery
    BoolQueryBuilder boolQuery = QueryBuilders.boolQuery();
    // 关键字搜索
    String key = params.getKey();
    if (key == null || "".equals(key)) {
        boolQuery.must(QueryBuilders.matchAllQuery());
    } else {
        boolQuery.must(QueryBuilders.matchQuery("all", key));
    }
    // 城市条件
    if (params.getCity() != null && !params.getCity().equals("")) {
        boolQuery.filter(QueryBuilders.termQuery("city", params.getCity()));
    }
    // 品牌条件
    if (params.getBrand() != null && !params.getBrand().equals("")) {
        boolQuery.filter(QueryBuilders.termQuery("brand", params.getBrand()));
    }
    // 星级条件
    if (params.getStarName() != null && !params.getStarName().equals("")) {
        boolQuery.filter(QueryBuilders.termQuery("starName", params.getStarName()));
    }
    // 价格
    if (params.getMinPrice() != null && params.getMaxPrice() != null) {
        boolQuery.filter(QueryBuilders
                         .rangeQuery("price")
                         .gte(params.getMinPrice())
                         .lte(params.getMaxPrice())
                        );
    }

    // 2.算分控制
    FunctionScoreQueryBuilder functionScoreQuery =
        QueryBuilders.functionScoreQuery(
        // 第一个参数是原始查询，相关性算分的查询
        boolQuery,
        // 第二个参数是function数组，数组每个元素是一个过滤方法
        new FunctionScoreQueryBuilder.FilterFunctionBuilder[]{
            // 第一个一个function score 元素
            new FunctionScoreQueryBuilder.FilterFunctionBuilder(
                // 过滤条件精准查询
                QueryBuilders.termQuery("isAD", true),
                // 算分函数
                ScoreFunctionBuilders.weightFactorFunction(10)
            )
        });
    request.source().query(functionScoreQuery);
}
```

> **坑点：**
> 
> **布尔查询不算分数\_score时（例如只有filter没有must），此时算分函数加权模式是乘的话就使所有文档\_score为0，因为n\*0=0。布尔查询没有子查询时默认是match\_all查询所有，算分的。**
> 
> 如果忘了写下面else，酒店结果过滤后就广告位的酒店就不在前面了，原因是原始查询即bool查询只有filter没有must，就不算分了，所有score都是0.：
> 
> ```java
>         if(!StringUtils.isEmpty(key)) builder.must(QueryBuilders.matchQuery("all",key));
>         else builder.must(QueryBuilders.matchAllQuery());
> ```