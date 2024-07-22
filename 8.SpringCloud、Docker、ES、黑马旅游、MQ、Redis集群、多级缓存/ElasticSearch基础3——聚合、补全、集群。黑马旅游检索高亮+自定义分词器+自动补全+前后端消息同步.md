> **导航：**
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})
>
>  **黑马旅游源码：** 
>
> https://wwmg.lanzouk.com/b04q61nof
>  密码:foqf

[TOC]



# 1.数据聚合

[聚合（](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html)[aggregations](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html)[）](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html)可以让我们极其方便的实现对数据的统计、分析、运算。例如：

- 什么品牌的手机最受欢迎？
- 这些手机的平均价格、最高价格、最低价格？
- 这些手机每月的销售情况如何？

实现这些统计功能的比数据库的sql要方便的多，而且查询速度非常快，可以实现近实时搜索效果。

## 1.1.聚合的种类

聚合常见的有三类：

- **桶（Bucket）聚合：**用来对文档做分组
  - TermAggregation：按照文档字段值分组，例如按照品牌值分组、按照国家分组
  - Date Histogram：按照日期阶梯分组，例如一周为一组，或者一月为一组
- **度量（Metric）聚合**：用以计算一些值，比如：最大值、最小值、平均值等
  - Avg：求平均值
  - Max：求最大值
  - Min：求最小值
  - Stats：同时求max、min、avg、sum等
- **管道（pipeline）聚合：**其它聚合的结果为基础做聚合

> **注意：参加聚合的字段必须是不能分词**，例如是keyword、日期、数值、布尔类型

## 1.2.DSL实现聚合

现在，我们要统计所有数据中的酒店品牌有几种，其实就是按照品牌对数据分组。此时可以根据酒店品牌的名称做聚合，也就是Bucket聚合。

### 1.2.1.Bucket聚合语法

语法如下：

```java
GET /hotel/_search
{
  "size": 0,  // 设置size为0，结果中不包含文档，只包含聚合结果。如果设为20，就是既展示20个brand查询的"hits"，又展示聚合"aggregations"
  "aggs": { // 定义聚合
    "聚合名": { //给聚合起个名字，例如brandAgg。查询结果里聚合名会嵌套在"aggregations"里
      "terms": { // 聚合的类型，按照品牌值聚合，所以选择term
        "field": "字段名", // 参与聚合的字段,例如brand
        "size": 20 // 希望获取的聚合结果数量
        "order": {
          "_count": "asc"        //按升序排序，默认是降序
        }
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 1.2.2.聚合结果排序

**默认情况下**，Bucket聚合会**统计Bucket内的文档数量**，记为_count，并且**按照_count降序**排序。

我们可以指定order属性，自定义聚合的排序方式：

```java
GET /hotel/_search
{
  "size": 0, 
  "aggs": {
    "brandAgg": {
      "terms": {
        "field": "brand",
        "order": {
          "_count": "asc" // 按照_count升序排列
        },
        "size": 20        
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 结果如图：

![image-20210723171948228](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/3064de64dcb8013575d33c953db1f236.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





### 1.2.3.通过query标签限定聚合范围

“query” 标签和“aggs”标签是并列的，“query” 标签不为空就是限定了聚合范围。

默认情况下，Bucket聚合是对索引库的所有文档做聚合，但真实场景下，用户会输入搜索条件，因此聚合必须是对搜索结果聚合。那么聚合必须添加限定条件。

我们可以限定要聚合的文档范围，只要添加query条件即可。

 **需求：**只对200元以下的文档聚合

```java
GET /hotel/_search
{
  "query": {
    "range": {
      "price": {
        "lte": 200 // 只对200元以下的文档聚合
      }
    }
  }, 
  "size": 0, 
  "aggs": {
    "brandAgg": {
      "terms": {
        "field": "brand",
        "size": 20
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这次，聚合得到的品牌明显变少了：

![image-20210723172404836](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/9b37bbbdf5986ccb6ad9cd7359ed43e9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.2.4.度量聚合语法，stats



上节课，我们对酒店按照品牌分组，形成了一个个桶。

**需求：**现在我们需要**对桶内的酒店做运算**，获取每个品牌的用户评分的min、max、avg等值。

这就要用到Metric聚合了，例如stat聚合：就可以获取min、max、avg等结果。

语法如下：

```java
GET /hotel/_search
{
  "size": 0, 
  "aggs": {
    "brandAgg": { 
      "terms": { 
        "field": "字段名", 
        "size": 20
      },
      "aggs": { // 是brands聚合的子聚合，也就是分组后对每组分别计算
        "聚合名如score_stats": { // 聚合名称
          "stats": { // 聚合类型，这里stats可以计算min、max、avg等。stats是statistics统计缩写
            "field": "score" // 聚合字段，这里是score
          }
        }
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这次的score_stats聚合是在brandAgg的聚合内部嵌套的子聚合。因为我们需要在每个桶分别计算。

我们还可以给聚合结果做个排序，例如按照每个桶的酒店平均分做排序：

![image-20210723172917636](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/56bbacea122f5c3a54447e67bed50e50.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.2.5.小结，聚合三要素

**aggs代表聚合**，与query同级，**此时query的作用是？**

- **限定聚合的的文档范围**

**聚合必须的三要素：**

- 聚合**名称**
- 聚合**类型**
- 聚合**字段**

**聚合可配置属性有：**

- size：指定聚合结果数量
- order：指定聚合结果排序方式
- field：指定聚合字段

## 1.3.RestAPI实现聚合

### 1.3.1.API语法

**聚合条件与query条件同级别**，因此需要使用**request.source()**来指定聚合条件。

**聚合条件的语法：**

![image-20210723173057733](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/89fb94d13016dbea75e341f561119596.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 注意：request.source().aggregation()，**聚合不是负数**，因为虽然DSL是"aggs"，但它不是数组，所以不是request.source().aggregations()

**聚合结果：**

聚合的结果也与查询结果不同，API也比较特殊。不过同样是JSON逐层解析：

![image-20210723173215728](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/8c5e8fa18587b410ca0f9347757c95c4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**response.getAggregations().get("brandAgg")的返回结果要是Terms，注意包别导错了，提示的第一个不是es的包。
>
> ```java
>     @Test
>     public void aggregation()throws IOException{
>         SearchRequest request = new SearchRequest("hotel");
>         request.source().size(0).aggregation(AggregationBuilders.terms("brandAgg").field("brand").size(20));
>         SearchResponse response = client.search(request, RequestOptions.DEFAULT);
>         Terms brandTerms =response.getAggregations().get("brandAgg");
>         List<? extends Terms.Bucket> buckets = brandTerms.getBuckets();
>         for(Terms.Bucket bucket:buckets){
>             System.out.println(bucket.getKeyAsString()+":"+bucket.getDocCount());
>         }
>     }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.3.2.黑马旅游业务需求，标签随着搜索结果变化

需求：搜索页面的品牌、城市等信息不应该是在页面写死，而是通过聚合索引库中的酒店数据得来的：

![image-20210723192605566](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/1399400e47935f98ddf68d28522c3b5b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**分析：**

目前，页面的城市列表、星级列表、品牌列表都是写死的，并不会**随着搜索结果的变化而变化**。但是用户搜索条件改变时，搜索结果会跟着变化。

例如：用户搜索“东方明珠”，那搜索的酒店肯定是在上海东方明珠附近，因此，城市只能是上海，此时城市列表中就不应该显示北京、深圳、杭州这些信息了。

也就是说，搜索结果中包含哪些城市，页面就应该列出哪些城市；搜索结果中包含哪些品牌，页面就应该列出哪些品牌。

如何得知搜索结果中包含哪些品牌？如何得知搜索结果中包含哪些城市？

使用聚合功能，利用Bucket聚合，对搜索结果中的文档基于品牌分组、基于城市分组，就能得知包含哪些品牌、哪些城市了。

因为是对搜索结果聚合，因此聚合是**限定范围的聚合**，也就是说聚合的限定条件跟搜索文档的条件一致。

查看浏览器可以发现，前端其实已经发出了这样的一个请求：

![image-20210723193730799](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/58eeafbb94a8207eac21d8672190e66c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

请求**参数与搜索文档的参数完全一致**。

返回值类型就是页面要展示的最终结果：

![image-20210723203915982](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/513853565e77087c98c1ab03c8214851.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

结果是一个Map结构：

- key是字符串，城市、星级、品牌、价格
- value是集合，例如多个城市的名称

### 1.3.3.业务实现

在`cn.itcast.hotel.web`包的`HotelController`中添加一个方法，遵循下面的要求：

- 请求方式：`POST`
- 请求路径：`/hotel/filters`
- 请求参数：`RequestParams`，与搜索文档的参数一致
- 返回值类型：`Map<String, List<String>>`

代码：

```java
    @PostMapping("filters")
    public Map<String, List<String>> getFilters(@RequestBody RequestParams params){
        return hotelService.getFilters(params);
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这里调用了IHotelService中的getFilters方法，尚未实现。

在`cn.itcast.hotel.service.IHotelService`中定义新方法：

```java
Map<String, List<String>> filters(RequestParams params);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在`cn.itcast.hotel.service.impl.HotelServiceImpl`中实现该方法：

```java
@Override
public Map<String, List<String>> filters(RequestParams params) {
    try {
        // 1.准备Request
        SearchRequest request = new SearchRequest("hotel");
        // 2.准备DSL
        // 2.1.query查询城市、品牌等基本信息
        buildBasicQuery(params, request);
        // 2.2.设置size
        request.source().size(0);
        // 2.3.聚合，根据
        buildAggregation(request);
        // 3.发出请求
        SearchResponse response = client.search(request, RequestOptions.DEFAULT);
        // 4.解析结果
        Map<String, List<String>> result = new HashMap<>();
        Aggregations aggregations = response.getAggregations();
        // 4.1.根据品牌名称，获取品牌结果
        List<String> brandList = getAggByName(aggregations, "brandAgg");
        result.put("brand", brandList);
        // 4.2.根据品牌名称，获取品牌结果
        List<String> cityList = getAggByName(aggregations, "cityAgg");
        result.put("city", cityList);
        // 4.3.根据品牌名称，获取品牌结果
        List<String> starList = getAggByName(aggregations, "starAgg");
        result.put("starName", starList);

        return result;
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}

//三个聚合，分别聚合品牌、城市、星级
private void buildAggregation(SearchRequest request) {
    request.source().aggregation(AggregationBuilders
                                 .terms("brandAgg")
                                 .field("brand")
                                 .size(100)
                                );
    request.source().aggregation(AggregationBuilders
                                 .terms("cityAgg")
                                 .field("city")
                                 .size(100)
                                );
    request.source().aggregation(AggregationBuilders
                                 .terms("starAgg")
                                 .field("starName")
                                 .size(100)
                                );
}

private List<String> getAggByName(Aggregations aggregations, String aggName) {
    // 4.1.根据聚合名称获取聚合结果
    Terms brandTerms = aggregations.get(aggName);
    // 4.2.获取buckets
    List<? extends Terms.Bucket> buckets = brandTerms.getBuckets();
    // 4.3.遍历
    List<String> brandList = new ArrayList<>();
    for (Terms.Bucket bucket : buckets) {
        // 4.4.获取key
        String key = bucket.getKeyAsString();
        brandList.add(key);
    }
    return brandList;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

测试： 

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/9f3c4532922943d8bda8666cee4dd948.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 2.自动补全

当用户在搜索框输入字符时，我们应该提示出与该字符有关的搜索项，如图：

![image-20210723204936367](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/7554c84831dfd2053fafbba36c246031.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这种根据用户输入的字母，提示完整词条的功能，就是自动补全了。

因为需要根据拼音字母来推断，因此要用到拼音分词功能。

## 2.1.pinyin拼音分词器的介绍和安装

要实现根据字母做补全，就必须对文档按照拼音分词。在GitHub上恰好有elasticsearch的拼音分词插件。地址：

```java
https://github.com/medcl/elasticsearch-analysis-pinyin
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![image-20210723205932746](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/350d2b4b387111da44cf331c2c44514f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

课前资料中也提供了拼音分词器的安装包：

![image-20210723205722303](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/c939879fe10276919932894b281324df.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

安装方式与IK分词器一样，分三步：

 ①解压

 ②上传到虚拟机中，elasticsearch的plugin目录

```bash
/var/lib/docker/volumes/es-plugins/_data
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/d535e8ac8191475198762b11e2032e03.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 ③重启elasticsearch

```java
docker restart es
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 ④测试

详细安装步骤可以参考IK分词器的安装过程。

测试用法如下：

```java
POST /_analyze
{
  "text": "如家酒店还不错",
  "analyzer": "pinyin"
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

结果：

![image-20210723210126506](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/56bc081eee13dc7c3f9c08d670e4dc6a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.2.自定义分词器，ik+拼音过滤

自定义分词器适合在创建索引库时使用，不能在搜索时候用 

### 2.2.1 实现方法 

默认的拼音分词器会将每个汉字单独分为拼音，而我们希望的是每个词条形成一组拼音，需要对拼音分词器做个性化定制，形成自定义分词器。

elasticsearch中分词器（analyzer）的组成包含三部分：

- **character filters：**在tokenizer之前对特**殊字符进行处理**。例如删除字符、替换字符
- **tokenizer：**将文本按照一定的**规则切割成词条（term）**。例如keyword，就是不分词；还有ik_smart
- **tokenizer filter：**将tokenizer输出的词条做**进一步处理，tokenizer的词条结果依然在，只是处理后新加了一些**。例如大小写转换、同义词处理、拼音处理等

**拼音分词器处理文档流程：**

![image-20210723210427878](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/2f48af22e7abeaff966b3e432d33efe9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**自定义分词器，把ik分词结果过滤成拼音：**

> **settings-analysis下定义分词器analyzer和filter**

```java
PUT /test
{
   //设置分词器和过滤器
  "settings": {
    "analysis": {
      "analyzer": { // 自定义分词器
        "my_analyzer": {  // 分词器名称，这里不需要指定character filters过滤器，因为没有特殊字符需要处理
          "tokenizer": "ik_max_word",
          "filter": "my_py_filter"    //对ik分词结果做进一步处理
        }
      },
      "filter": { // 自定义tokenizer filter
        "my_py_filter": { // 过滤器名称
          "type": "pinyin", // 过滤器类型，填写分词器名，这里是pinyin
		  "keep_full_pinyin": false,//eg: 刘德华> [liu,de,hua], default: true
          "keep_joined_full_pinyin": true,//eg: 刘德华> [liudehua], default: false
          "keep_original": true,//保留原始输入，默认false
          "limit_first_letter_length": 16,//
          "remove_duplicated_term": true,//
          "none_chinese_pinyin_tokenize": false// 默认true。eg: liudehuaalibaba13zhuanghan -> liu,de,hua,a,li,ba,ba,13,zhuang,han
        }
      }
    }
  },

  //创建索引
  "mappings": {
    "properties": {
      "name": {
        "type": "text",
        "analyzer": "my_analyzer",        //拼音分词器适合在创建索引时使用，不能在搜索时候用
        "search_analyzer": "ik_smart"     //如果搜索时用拼音分词器，搜索"狮子爱跳舞"，会搜出"虱子"等同音字
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **注意：**
>
> **拼音分词器适合在创建索引时使用，不能在搜索时候用**，如果搜索时用拼音分词器，搜索"狮子爱跳舞"，会搜出"虱子"等同音字。

**测试：自定义分词器搜索结果既有ik_smart，还有拼音分词的结果**

```java
GET /test/_analyze
{
  "analyzer": "my_analyzer"
  , "text": "今天天气好"
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![image-20210723211829150](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/d915218ef3a3c2735a717473e4606cad.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.2.2 索引分词器和搜索分词器问题

在使用**ik+拼音过滤**的分词器时，建议创建的字段的**索引分词器设为自定义分词器，搜索分词器设为ik分词器。防止搜索时搜出拼音谐音的情况。**

**指定索引、搜索分词器，并创建索引：**

```java
PUT /test
{
   //设置分词器和过滤器
  "settings": {
    "analysis": {
      "analyzer": { // 自定义分词器
        "my_analyzer": {  // 分词器名称，这里不需要指定character filters过滤器，因为没有特殊字符需要处理
          "tokenizer": "ik_max_word",
          "filter": "my_py_filter"    //对ik分词结果做进一步处理
        }
      },
      "filter": { // 自定义tokenizer filter
        "my_py_filter": { // 过滤器名称
          "type": "pinyin", // 过滤器类型，填写分词器名，这里是pinyin
		  "keep_full_pinyin": false,//eg: 刘德华> [liu,de,hua], default: true
          "keep_joined_full_pinyin": true,//eg: 刘德华> [liudehua], default: false
          "keep_original": true,//保留原始输入，默认false
          "limit_first_letter_length": 16,//
          "remove_duplicated_term": true,//
          "none_chinese_pinyin_tokenize": false// 默认true。eg: liudehuaalibaba13zhuanghan -> liu,de,hua,a,li,ba,ba,13,zhuang,han
        }
      }
    }
  },

  //创建索引
  "mappings": {
    "properties": {
      "name": {
        "type": "text",
        "analyzer": "my_analyzer",        //拼音分词器适合在创建索引时使用，不能在搜索时候用
        "search_analyzer": "ik_smart"     //如果搜索时用拼音分词器，搜索"狮子爱跳舞"，会搜出"虱子"等同音字
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

建议索引分词器设为自定义分词器，搜索分词器设为ik分词器。防止搜索时搜出拼音谐音问题。

> **问题模拟，索引、搜索都用自定义分词器：**
>
> ```java
> DELETE /test
> 
> PUT /test
> {
>   "settings": {
>     "analysis": {
>       "analyzer": {
>         "my_analyzer":{
>           "tokenizer":"ik_smart",
>           "filter":"py_filter"
>         }
>       },
>       "filter": {
>         "py_filter":{
>           "type":"pinyin",
>           "keep_full_pinyin": false,
>           "keep_joined_full_pinyin": true,
>           "keep_original": true,
>           "limit_first_letter_length": 16,
>           "remove_duplicated_term": true,
>           "none_chinese_pinyin_tokenize": false
>         }
>       }
>     }
>   },
>   "mappings": {
>     "properties": {
>       "name":{
>         "type": "text",
>         "analyzer": "my_analyzer"    //统一ik+拼音过滤
>       }
>     }
>   }
> }
> POST /test/_doc/1
> {
>   "name":"狮子"
> }
> 
> POST /test/_doc/2
> {
>   "name":"师资"
> }
> 
> GET /test/_search
> {
>   "query": {
>     "match": {
>       "name": "狮子爱跳舞"
>     }
>   }
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> ![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/5efcb816b07846cab7192a753bc3db0b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 可以看见，明明搜索的是狮子，却搜出了谐音师资。因为搜索“狮子爱跳舞”时，ik+拼音过滤后的结果里有“shizi”，而师资的分词结果也有“shizi”，所以就搜出了师资。
>
> 如果搜索“shizi”，出现结果正常，是狮子和师资。

**解决办法：索引分词器设为自定义分词器，搜索分词器设为ik分词器。防止搜索时搜出拼音谐音问题。**

明显不是我们想要的，所以要让它搜索时候只用ik分词，不要拼音过滤就搜不出谐音了，而添加新文档时还要它进行分词拼音，以便于我们可以搜拼音时也能搜出对应字段。

```java
PUT /test
{
   //设置分词器和过滤器
  "settings": {
     ...自定义分词器
  },

  //创建索引
  "mappings": {
    "properties": {
      "name": {
        "type": "text",
        "analyzer": "my_analyzer",        //创建文档时自定义分词器，ik+拼音过滤
        "search_analyzer": "ik_smart"     //搜索时只用ik分词器
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **总结：**
>
> **如何使用拼音分词器？**
>
> - ①下载pinyin分词器
> - ②解压并放到elasticsearch的plugin目录
> - ③重启即可
>
> **如何自定义分词器？**
>
> - ①创建索引库时，在settings中配置，可以包含三部分
> - ②character filter
> - ③tokenizer
> - ④filter
>
> **拼音分词器注意事项？**
>
> - **为了避免搜索到同音字，搜索时不要使用拼音分词器**

## 2.3.自动补全查询，conmpetion suggester

**补全效果预览：**录入 ["天苍苍", "野茫茫"]、["天府", "天下"]、["世界", "黄天"]。suggest搜索“天”，可以搜索出前两个文档。suggest搜索“天苍”，只能搜索出第一个文档。

elasticsearch提供了[Completion Suggester](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/search-suggesters.html)查询来实现自动补全功能。这个查询会匹配以用户输入内容开头的词条并返回。为了提高补全查询的效率，对于文档中字段的类型有一些约束：

- **参与补全查询的字段必须是completion类型，数据是字符串数组。completion译为完成**
- **字段的内容**一般是用来补全的**多个词条形成的数组**。

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/13487be8fef9491eac8765c5d4465c81.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**创建索引库：**

```java
// 创建索引库
PUT test
{
  "mappings": {
    "properties": {
      "title":{
        "type": "completion"    
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**插入数据：**

```java
// 示例数据
POST test/_doc
{
  "title": ["天苍苍", "野茫茫"]
}
POST test/_doc
{
  "title": ["天府", "天下"]
}
POST test/_doc
{
  "title": ["世界", "黄天"]
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**自动补全查询：**

```java
// 自动补全查询
GET /test/_search
{
  "suggest": {
    "titleSuggest": {    //例如自定义查询名称
      "text": "天", // 关键字
      "completion": {
        "field": "title", // 补全查询的字段，例如title
        "skip_duplicates": true, // 跳过重复的
        "size": 10 // 获取前10条结果
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**搜索结果：**

```java
{
  "took" : 275,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 0,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "suggest" : {
    "my_suggest" : [
      {
        "text" : "天",
        "offset" : 0,
        "length" : 1,
        "options" : [
          {
            "text" : "天下",
            "_index" : "test2",
            "_type" : "_doc",
            "_id" : "AEutP4MBg4Wtm5vtyLdE",
            "_score" : 1.0,
            "_source" : {
              "name" : [
                "天府",
                "天下"
              ]
            }
          },
          {
            "text" : "天苍苍",
            "_index" : "test2",
            "_type" : "_doc",
            "_id" : "AUutP4MBg4Wtm5vtyLdI",
            "_score" : 1.0,
            "_source" : {
              "name" : [
                "天苍苍",
                "野茫茫"
              ]
            }
          }
        ]
      }
    ]
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 2.4.实现酒店搜索框自动补全

现在，我们的hotel索引库还没有设置拼音分词器，需要修改索引库中的配置。但是我们知道索引库是无法修改的，只能删除然后重新创建。

另外，我们需要添加一个字段，用来做自动补全，将brand、suggestion、city等都放进去，作为自动补全的提示。

因此，总结一下，我们需要做的事情包括：

1. 修改hotel索引库结构，设置自定义拼音分词器
2. 修改索引库的name、all字段，使用自定义分词器
3. 索引库添加一个新字段suggestion，类型为completion类型，使用自定义的分词器
4. 给HotelDoc类添加suggestion字段，内容包含brand、business
5. 重新导入数据到hotel库

### 2.4.1.创建新索引库，使用自定义分词器

①ik+拼音过滤分词器，给ik分词设置自定义过滤器，给分词进一步处理成拼音。索引使用自定义分词器，搜索使用ik分词器。②关键字+拼音过滤分词器，代码补全使用的分词器。  

代码如下：

```java
//酒店数据索引库。先删除旧的，再新的
DELETE /hotel
PUT /hotel
{
  "settings": {
    "analysis": {
      "analyzer": {
        "text_anlyzer": {    //ik+拼音过滤
          "tokenizer": "ik_max_word",
          "filter": "py"
        },
        "completion_analyzer": {    //keyword+拼音过滤，相当于又保持关键词，又新加定制版拼音分词
          "tokenizer": "keyword",
          "filter": "py"
        }
      },
      "filter": {
        "py": {
          "type": "pinyin",
          "keep_full_pinyin": false,
          "keep_joined_full_pinyin": true,
          "keep_original": true,
          "limit_first_letter_length": 16,
          "remove_duplicated_term": true,
          "none_chinese_pinyin_tokenize": false
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "id":{
        "type": "keyword"
      },
      "name":{
        "type": "text",
        "analyzer": "text_anlyzer",        //新建文档时分词器用ik+拼音过滤
        "search_analyzer": "ik_smart",    //搜索分词器用ik
        "copy_to": "all"
      },
      "address":{
        "type": "keyword",
        "index": false
      },
      "price":{
        "type": "integer"
      },
      "score":{
        "type": "integer"
      },
      "brand":{
        "type": "keyword",
        "copy_to": "all"
      },
      "city":{
        "type": "keyword"
      },
      "starName":{
        "type": "keyword"
      },
      "business":{
        "type": "keyword",
        "copy_to": "all"
      },
      "location":{
        "type": "geo_point"
      },
      "pic":{
        "type": "keyword",
        "index": false
      },
      "all":{
        "type": "text",
        "analyzer": "text_anlyzer",
        "search_analyzer": "ik_smart"
      },
      "suggestion":{    //补全字段suggestion
          "type": "completion",    //补全字段类型必须completion
          "analyzer": "completion_analyzer"    //补全分词器，keyword+拼音过滤
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.4.2.HotelDoc实体类添加suggestion字段

HotelDoc中要添加一个字段，用来做自动补全，内容可以是酒店品牌、城市、商圈等信息。按照自动补全字段的要求，最好是这些字段的数组。

因此我们在HotelDoc中添加一个suggestion字段，类型为`List<String>`，然后将brand、city、business等信息放到里面。

代码如下：

```java
package cn.itcast.hotel.pojo;

import lombok.Data;
import lombok.NoArgsConstructor;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

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
    private String business;	//商圈，例如虹桥机场/国家会展中心
    private String location;
    private String pic;
    private Object distance;
    private Boolean isAD;
    private List<String> suggestion;	//放自动补全的list列表，这里只补全搜索商圈和品牌

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
        // 组装suggestion，把品牌和商圈放进去
        if(this.business.contains("/")){
            // business有多个值，例如“例如虹桥机场/国家会展中心”，需要切割
            String[] arr = this.business.split("/");
            // 添加元素
            this.suggestion = new ArrayList<>();
            this.suggestion.add(this.brand);
            Collections.addAll(this.suggestion, arr);
        }else {
            this.suggestion = Arrays.asList(this.brand, this.business);
        }
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.4.3.重新导入MySQL数据到es索引库

重新执行之前编写的导入数据功能

```java
    @Test
    public void bulk() throws IOException {
        List<Hotel> hotels = hotelService.list();
        for(Hotel hotel:hotels){
            HotelDoc hotelDoc = new HotelDoc(hotel);
            client.index(new IndexRequest("hotel").id(hotel.getId().toString()).source(JSON.toJSONString(hotelDoc),XContentType.JSON),RequestOptions.DEFAULT);
        }

    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

查询所有 ，可以看到新的酒店数据中包含了suggestion：

```java
GET /hotel/_search
{
  "query": {
    "match_all": {}
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![image-20210723213546183](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/92c320e716e197d3c8114aadc5c92c49.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **2.4.4 测试补全，suggest搜索"rj"结果“如家”的文档**

因为**suggestion字段**自定义分词器是**keyword+拼音过滤**，所以搜索“如”搜不出“如家”。搜索“如家”可以搜索出brand为“如家”的一条文档（搜索条件有跳过重复）。搜索“rj”，可以搜索出brand为“如家”的文档

**测试：** 

```java
GET /hotel/_search
{
  "suggest": {
    "my_suggest": {
      "text": "rj",
      "completion":{
        "field": "suggestion", 
        "skip_duplicates": true, 
        "size": 10
      }
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**因为指定跳过重复，所以搜索结果仅一条：**

```java
{
  "took" : 6,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 0,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "suggest" : {
    "my_suggest" : [
      {
        "text" : "如家",
        "offset" : 0,
        "length" : 2,
        "options" : [
          {
            "text" : "如家",
            "_index" : "hotel",
            "_type" : "_doc",
            "_id" : "415600",
            "_score" : 1.0,
            "_source" : {
              "address" : "三间房乡褡裢坡村青年沟西侧558号",
              "brand" : "如家",
              "business" : "传媒大学/管庄地区",
              "city" : "北京",
              "id" : 415600,
              "location" : "39.923212, 116.560023",
              "name" : "如家酒店(北京朝阳北路传媒大学褡裢坡地铁站店)",
              "pic" : "https://m.tuniucdn.com/fb3/s1/2n9c/3NezpxNZWQMdNXibwbMkQuAZjDyJ_w200_h200_c1_t0.jpg",
              "price" : 259,
              "score" : 47,
              "starName" : "二钻",
              "suggestion" : [
                "如家",
                "传媒大学",
                "管庄地区"
              ]
            }
          }
        ]
      }
    ]
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.4.5.自动补全查询的JavaAPI，SuggestBuilder()

之前我们学习了自动补全查询的DSL，而没有学习对应的JavaAPI，这里给出一个示例：

suggest和query是平级的。 

![image-20210723213759922](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/f4faad9f765f308be2b4f7ed92eb4003.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

而自动补全的结果也比较特殊，解析的代码如下：

![image-20210723213917524](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/618ca7b92e0fe0e04616c2d792751cdd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.4.6.实现旅游项目搜索框自动补全

查看前端页面，可以发现当我们在输入框键入时，前端会发起ajax请求：

![image-20210723214021062](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/d912d0734e1c37159955d98362688dcf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

返回值是补全词条的集合，类型为`List<String>`

1）在`cn.itcast.hotel.web`包下的`HotelController`中添加新接口，接收新的请求：

```java
@GetMapping("suggestion")
public List<String> getSuggestions(@RequestParam("key") String prefix) {
    return hotelService.getSuggestions(prefix);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2）在`cn.itcast.hotel.service`包下的`IhotelService`中添加方法：

```java
List<String> getSuggestions(String prefix);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3）在`cn.itcast.hotel.service.impl.HotelService`中实现该方法：

> 建议截图补全的es代码，贴到屏幕上，层层解析 

```java
@Override
public List<String> getSuggestions(String prefix) {
    try {
        // 1.准备Request
        SearchRequest request = new SearchRequest("hotel");
        // 2.准备DSL
        request.source().suggest(new SuggestBuilder().addSuggestion(    //new SuggestBuilder()不是SuggestBuilders
            "suggestions",    //自定义补全的名字，后面根据它解析response
            SuggestBuilders.completionSuggestion("suggestion")    //字段名
            .prefix(prefix)    //需要补全的文本
            .skipDuplicates(true)
            .size(10)
        ));
        // 3.发起请求
        SearchResponse response = client.search(request, RequestOptions.DEFAULT);
        // 4.解析结果
        Suggest suggest = response.getSuggest();
        // 4.1.根据补全查询名称，获取补全结果，注意返回值和ctrl+alt+v生成的内容不一样
        CompletionSuggestion suggestions = suggest.getSuggestion("suggestions");
        // 4.2.获取options
        List<CompletionSuggestion.Entry.Option> options = suggestions.getOptions();
        // 4.3.遍历
        List<String> list = new ArrayList<>(options.size());
        for (CompletionSuggestion.Entry.Option option : options) {
            String text = option.getText().toString();
            list.add(text);
        }
        return list;
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**测试成功：**

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/235a3c2b75c24d4b9e91746e05b69bea.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 3.mysql与es数据同步

elasticsearch中的酒店数据来自于mysql数据库，因此mysql数据发生改变时，elasticsearch也必须跟着改变，这个就是elasticsearch与mysql之间的**数据同步**。

![image-20210723214758392](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/61c5a08f58d3da4b138ab5eddd9203f8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 3.1.思路分析

常见的数据同步方案有三种：

- 同步调用
- 异步通知
- 监听binlog

### 3.1.1.**方案一：**同步调用

**方案一：同步调用**

管理端只能访问mysql，用户端只能访问es，两者间隔离，符合微服务规范。 

![image-20210723214931869](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/1fac0dfb4b195e538d6b8b064b30a587.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

基本步骤如下：

- hotel-demo对外提供接口，用来修改elasticsearch中的数据
- 酒店管理服务在完成数据库操作后，直接调用hotel-demo提供的接口，

**缺点：耦合度高** 

### 3.1.2.方案二：异步通知

方案二：异步通知

![image-20210723215140735](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/652e7750c8232923eb4efdd97c8ca7c4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

流程如下：

- hotel-admin对mysql数据库数据完成增、删、改后，发送MQ消息
- hotel-demo监听MQ，接收到消息后完成elasticsearch数据修改

优点：性能高，耦合度低

缺点：依赖于mq消息队列可靠性 

### 3.1.3.方案三：canal监听mysql的binlog

canal译为管道，运河。



> **回顾主从复制，**主库开启binlog，从库根据主库binlog的增删改信息，进行相同操作。

![image-20210723215518541](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/c8e28d9408d94916cba589767fb32778.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

流程如下：

- 给mysql开启binlog功能
- mysql完成增、删、改操作都会记录在binlog中
- hotel-demo基于canal监听binlog变化，实时更新elasticsearch中的内容

**优点：**耦合度最低

**缺点：**mysql压力增加 

### 3.1.4.三种方案优缺点总结

**方式一：同步调用**

- 优点：实现简单，粗暴
- 缺点：业务**耦合度高**

**方式二：异步通知**

- 优点：低耦合，实现难度一般
- 缺点：**依赖mq的可靠性**

**方式三：监听binlog**

- 优点：**完全解除服务间耦合**
- 缺点：开启binlog增加**数据库负担**、实现复杂度高

## 3.2.MQ实现数据同步

### 3.2.1.思路

利用课前资料提供的hotel-admin项目作为酒店管理的微服务。当酒店数据发生增、删、改时，要求对elasticsearch中数据也要完成相同操作。

**使用RabbitMQ的发布/订阅模型topic话题模式，支持不同的消息根据routingKey被不同的队列消费。先声明交换机、队列，增删两个routingKey。只需要增删两个队列，restapi里增改是一致的，id存在则修改，id不存在则新增。**  

> 忘了就回顾：[SpringCloud基础4——RabbitMQ和SpringAMQP](https://blog.csdn.net/qq_40991313/article/details/126801025?spm=1001.2014.3001.5501) 

步骤：

- 导入课前资料提供的hotel-admin项目，启动并测试酒店数据的CRUD
- 声明exchange、queue、RoutingKey
- 在hotel-admin中的增、删、改业务中完成消息发送
- 在hotel-demo中完成消息监听，并更新elasticsearch中数据
- 启动并测试数据同步功能

### 3.2.2.导入hotel-admin后台管理端、修改pom和yml

导入课前资料提供的hotel-admin项目：

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/df7d3217ad5f4e6dbe849b4d36621db5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/ecab78b0d4d343d888bfdb4fe99497f8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**修改pom**

```XML
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.4.2</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.2.11</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**修改yml：**

```bash
server:
  port: 8099
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/heima?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf-8&zeroDateTimeBehavior=convertToNull&useSSL=false&allowPublicKeyRetrieval=true
      username: root
      password: 1234
  main:
    banner-mode: off
  rabbitmq:
    host: 192.168.200.131
    port: 5672
    username: itcast
    password: 123321
    virtual-host: / #虚拟主机
#logging:
#  level:
#    cn.itcast: debug
#  pattern:
#    dateformat: MM-dd HH:mm:ss:SSS

#  type-aliases-package:com.vince.hotel.pojo
mybatis-plus:
  configuration:
    map-underscore-to-camel-case: true
  global-config:
    banner: false
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 运行后，访问 http://localhost:8099

![image-20210723220354464](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/55ac3aa5ebc5a06cc855b6ddecc78c36.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**其中包含了酒店的CRUD功能：**

![image-20210723220511090](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/47f1c5c34fe2e27e754e123c8d1910f0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.2.3.声明交换机、队列

MQ结构如图：

![image-20210723215850307](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/0123d9075752c22418c4e99aab885bbd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**0)开启RabbitMQ**

```
docker ps -a
docker start 容器名
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

管理端：

```bash
http://ip地址:15672/
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> [SpringCloud基础4——RabbitMQ_springcloud rabbitmq_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126801025?spm=1001.2014.3001.5501)

**1）引入依赖、yml**

在hotel-admin、hotel-demo中引入rabbitmq的依赖：

```XML
<!--amqp-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

yml：

```bash
server:
  port: 8099
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/heima?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf-8&zeroDateTimeBehavior=convertToNull&useSSL=false&allowPublicKeyRetrieval=true
      username: root
      password: 1234
  main:
    banner-mode: off
  rabbitmq:
    host: 192.168.200.131
    port: 5672
    username: itcast
    password: 123321
    virtual-host: / #虚拟主机
#logging:
#  level:
#    cn.itcast: debug
#  pattern:
#    dateformat: MM-dd HH:mm:ss:SSS

#  type-aliases-package:com.vince.hotel.pojo
mybatis-plus:
  configuration:
    map-underscore-to-camel-case: true
  global-config:
    banner: false
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2）常量类，声明队列交换机名称**

在hotel-admin和hotel-demo中的`cn.itcast.hotel.constatnts`包下新建一个类`MqConstants`：



```java
package cn.itcast.hotel.constants;

    public class MqConstants {
    /**
     * 交换机
     */
    public final static String HOTEL_EXCHANGE = "hotel.topic";
    /**
     * 监听新增和修改的队列
     */
    public final static String HOTEL_INSERT_QUEUE = "hotel.insert.queue";
    /**
     * 监听删除的队列
     */
    public final static String HOTEL_DELETE_QUEUE = "hotel.delete.queue";
    /**
     * 新增或修改的RoutingKey
     */
    public final static String HOTEL_INSERT_KEY = "hotel.insert";
    /**
     * 删除的RoutingKey
     */
    public final static String HOTEL_DELETE_KEY = "hotel.delete";
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3）声明队列交换机**

> **topic模式回顾：话题模式，通配符。**`Topic`类型的`Exchange`与`Direct`相比，都是可以根据`RoutingKey`把消息路由到不同的队列。只不过**`Topic`类型`Exchange`可以让队列在绑定`Routing key` 的时候使用通配符！**
>
> 也可以在接收消息时，使用注解方式@RabbitListener的bindings，适用于消息队列少的情况:
>
> ```java
> @RabbitListener(bindings = @QueueBinding(
>     value = @Queue(name = "topic.queue1"),
>     exchange = @Exchange(name = "itcast.topic", type = ExchangeTypes.TOPIC),
>     key = "china.#"
> ))
> public void listenTopicQueue1(String msg){
>     System.out.println("消费者接收到topic.queue1的消息：【" + msg + "】");
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 在config包下创建MqConfig，声明队列、交换机：

```java
package cn.itcast.hotel.config;

import cn.itcast.hotel.constants.MqConstants;
import org.springframework.amqp.core.Binding;
import org.springframework.amqp.core.BindingBuilder;
import org.springframework.amqp.core.Queue;
import org.springframework.amqp.core.TopicExchange;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MqConfig {
    @Bean
    public TopicExchange topicExchange(){
        //第二个参数为是否持久化，第三个参数为是否自动删除。两个参数默认值就是持久化、不自动删除
        return new TopicExchange(MqConstants.HOTEL_EXCHANGE, true, false);
    }

    @Bean
    public Queue insertQueue(){
        return new Queue(MqConstants.HOTEL_INSERT_QUEUE, true);
    }

    @Bean
    public Queue deleteQueue(){
        return new Queue(MqConstants.HOTEL_DELETE_QUEUE, true);
    }

    @Bean
    public Binding insertQueueBinding(){
        return BindingBuilder.bind(insertQueue()).to(topicExchange()).with(MqConstants.HOTEL_INSERT_KEY);
    }

    @Bean
    public Binding deleteQueueBinding(){
        return BindingBuilder.bind(deleteQueue()).to(topicExchange()).with(MqConstants.HOTEL_DELETE_KEY);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **为什么只需要增删两个队列，不用“改” 队列？**
>
> 在RestClient的API中，**全量修改与新增的API完全一致**，判断依据是ID：
>
> - 如果新增时，ID已经存在，则修改
> - 如果新增时，ID不存在，则新增

### 3.2.4.后台端发送MQ消息

在hotel-admin中的增、删、改业务中分别发送MQ消息，**消息内容为id，到时候用户端根据id增删改**：

![image-20210723221843816](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/2a2817424dcc9c8743434236d3ca3c7a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.2.5.**用户端**接收MQ消息

管理端hotel-admin不能直接调用es，想对es实现增删改要通过给用户端hotel-demo发送新增（修改）、删除消息。

**hotel-demo**接收到MQ消息要做的事情包括：

- **新增消息：**根据传递的hotel的**id**查询hotel信息，然后新增一条数据到**索引库**
- **删除消息：**根据传递的hotel的**id删除索引库**中的一条数据

**0） 环境准备**

pom

```XML
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-amqp</artifactId>
        </dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

yml

```bash
spring:
  rabbitmq:
    host: 192.168.200.131
    port: 5672
    username: itcast
    password: 123321
    virtual-host: / #虚拟主机
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

复制管理端的MqConstants.java和MqConfig到用户端

**1）service接口新增新增、删除业务**

首先在hotel-demo的`cn.itcast.hotel.service`包下的`IHotelService`中**新增新增、删除业务**

```java
//mp的增删方法是saveById和removeById，所以这里并不冲突
void deleteById(Long id);

void insertById(Long id);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）service实现类实现业务**

给hotel-demo中的`cn.itcast.hotel.service.impl`包下的HotelService中**实现业务：**

```java
//mp的增删方法是saveById和removeById，所以这里并不冲突
@Override
public void deleteById(Long id) {
    try {
        // 1.准备Request
        DeleteRequest request = new DeleteRequest("hotel", id.toString());
        // 2.发送请求
        client.delete(request, RequestOptions.DEFAULT);
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}

@Override
public void insertById(Long id) {
    try {
        // 0.根据id查询酒店数据
        Hotel hotel = getById(id);
        // 转换为文档类型
        HotelDoc hotelDoc = new HotelDoc(hotel);

        // 1.准备Request对象
        IndexRequest request = new IndexRequest("hotel").id(hotel.getId().toString());
        // 2.准备Json文档
        request.source(JSON.toJSONString(hotelDoc), XContentType.JSON);
        // 3.发送请求
        client.index(request, RequestOptions.DEFAULT);
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 坑点：删除文档的request别忘了设置id，不然会删除所有数据。

**3）编写监听器**

**在`mq`包下**新增一个类：

```java
package cn.itcast.hotel.mq;

import cn.itcast.hotel.constants.MqConstants;
import cn.itcast.hotel.service.IHotelService;
import org.springframework.amqp.rabbit.annotation.RabbitListener;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
//别忘了@Component，被ioc容器管理，一直监听
@Component
public class HotelListener {

    @Autowired
    private IHotelService hotelService;

    /**
     * 监听酒店新增或修改的业务
     * @param id 酒店id
     */
    @RabbitListener(queues = MqConstants.HOTEL_INSERT_QUEUE)
    public void listenHotelInsertOrUpdate(Long id){
        hotelService.insertById(id);
    }

    /**
     * 监听酒店删除的业务
     * @param id 酒店id
     */
    @RabbitListener(queues = MqConstants.HOTEL_DELETE_QUEUE)
    public void listenHotelDelete(Long id){
        hotelService.deleteById(id);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.2.6 测试

运行管理端和用户端服务后，打开rabbitmq服务端： http://ip地址:15672

可以看到队列、交换机创建成功：

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/770c054f53014517bc06dd6333917e31.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/9acfba90a5e84f4da68edc5b4fc9e64e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**交换机绑定关系：**

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/99f01c94ad9441e69a3c90ba414e80c3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**先用户端搜索一个酒店，然后在管理端修改酒店信息 ：**

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/eb55fd08f4cf436682ef53ac6fd4b20b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**可以看到队列的消息记录：**

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/ef3d1a356ee3420e894f8e0104178f8f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**用户端搜索后的数据也改变了：**

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/a79bb3c3fca5403281c24cf79f71245c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

再删除酒店，发现成功。

### 3.2.7.vue插件实现快速拷贝数据到表单

**安装地址**

https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh

**拷贝数据并保存的办法：**

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/e7078dcab74c4c678aaf4f84a126f9e9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

粘贴即可快速填充表单：

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/0acf00ca33554fc1808cc189cfe63514.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 4.集群

## 4.0.概述 

单机的elasticsearch做数据存储，必然面临两个问题：海量数据存储问题、单点故障问题。

- **海量数据存储问题：**将**索引库**从逻辑**上拆分为N个分片**（shard），存储到多个节点
- **单点故障问题：将分片数据在不同节点备份**（replica ） 

**ES集群相关概念**:

**一个集群里有多个节点，每个节点都是一个es实例， 每个节点保存了自己的分片和一个其他节点备份的分片。**

- **集群（cluster）**：一组拥有共同的 集群名 的 节点。

- **节点（node) ：**集群中的一个 Elasticearch 实例

- **分片（shard）：**索引可以被拆分为不同的部分进行存储，称为分片。在集群环境下，**一个索引的不同分片可以拆分到不同的节点中**

  **解决问题：**数据量太大，单点存储量有限的问题。

  ![image-20200104124440086](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/0df5d050d70b550759e020064d56dce2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > 此处，我们把数据分成3片：shard0、shard1、shard2

- **主分片（Primary shard）：**相对于副本分片的定义。

- **副本分片（Replica shard）：**每个主分片可以有一个或者多个副本，**数据和主分片一样**。

  

数据备份可以保证高可用，但是每个分片备份一份，所需要的节点数量就会翻一倍，成本实在是太高了！

为了在高可用和成本间寻求平衡，我们可以这样做：

- 首先对数据分片，存储到不同节点
- 然后对**每个分片进行备份，放到对方节点，完成互相备份**

这样可以大大减少所需要的服务节点数量，如图，我们以3分片，每个分片备份一份为例：

![image-20200104124551912](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/31461289848e82c6019658a5797b7810.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

现在，每个分片都有1个备份，存储在3个节点：

- **节点node0：保存了分片0和1**
- node1：保存了分片0和2
- node2：保存了分片1和2

## 4.1.搭建ES集群

### 4.1.0.Docker Compose介绍

Docker Compose是一个用来定义和运行复杂应用的Docker工具，将一个或多个容器组合成一个完整的应用程序。一个使用Docker容器的应用，通常由多个容器组成。使用Docker Compose不再需要使用shell脚本来启动容器。

Compose 通过一个**配置文件**来管理多个Docker容器，在配置文件中，所有的容器通过**services**来定义，然后使用**docker-compose脚本**来启动，停止和重启应用，和应用中的服务以及所有依赖服务的容器，非常适合组合使用多个容器进行开发的场景。

**Docker Compose 使用的三个步骤：**

1. 使用 Dockerfile 定义应用程序的环境
2. 使用 docker-compose.yml 定义构成应用程序的服务，这样它们可以在隔离环境中一起运行
3. 执行 docker-compose up 命令（后面加-d是在后台运行）来启动并运行整个应用程序

### 4.1.1.创建es集群

创建同一个集群的三个节点，每个节点都是一个es实例：

**①首先编写一个docker-compose.yml文件**，上传到/root，内容如下：

> **注意端口占用问题**：ports:-9200:9200，左边是centos的端口，右边是容器内部端口，只有左边会发生端口占用问题，前面安装过单点es的默认接口是9200，注意一下。

```bash
#创建三个es容器，容器名和节点名都是es01、es02、es03。

version: '2.2'
services:
  es01:
    image: elasticsearch:7.12.1    #镜像名称
    container_name: es01    #容器名称
    environment:
      - node.name=es01
#集群名称。三个容器集群名称一样，es会自动把他们组装成一个集群。
      - cluster.name=es-docker-cluster    
#集群中其他节点的ip地址；docker容器之间通过名字直接相互访问
      - discovery.seed_hosts=es02,es03	
#集群中可以参与选举的主节点
      - cluster.initial_master_nodes=es01,es02,es03
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"    #内存大小，最小和最大内存
    volumes:
      - data01:/usr/share/elasticsearch/data
    ports:
      - 9200:9200    #对外端口9200：对内端口9200
    networks:
      - elastic
  es02:
    image: elasticsearch:7.12.1
    container_name: es02
    environment:
      - node.name=es02
#集群名称。三个容器集群名称一样，es会自动把他们组装成一个集群。
      - cluster.name=es-docker-cluster
      - discovery.seed_hosts=es01,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    volumes:
      - data02:/usr/share/elasticsearch/data
    ports:
      - 9201:9200
    networks:
      - elastic
  es03:
    image: elasticsearch:7.12.1
    container_name: es03
    environment:
      - node.name=es03
      - cluster.name=es-docker-cluster
#集群名称。三个容器集群名称一样，es会自动把他们组装成一个集群。
      - discovery.seed_hosts=es01,es02
      - cluster.initial_master_nodes=es01,es02,es03
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    volumes:
      - data03:/usr/share/elasticsearch/data
    networks:
      - elastic
    ports:
      - 9202:9200
volumes:
  data01:
    driver: local
  data02:
    driver: local
  data03:
    driver: local

networks:
  elastic:
    driver: bridge
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**②修改权限：** 

es运行需要修改一些linux系统权限，修改`/etc/sysctl.conf`文件

```
vi /etc/sysctl.conf
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

添加下面的内容，或将注释打开：

```
vm.max_map_count=262144
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

然后执行命令，**让配置生效**：

```
sysctl -p
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**③通过docker-compose up启动集群：**

```
docker-compose up -d
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 4.1.2.集群状态监控，安装cerebro

kibana可以监控es集群，不过新版本需要依赖es的x-pack 功能，配置比较复杂。

这里推荐使用cerebro来监控es集群状态，官方网址：https://github.com/lmenezes/cerebro

课前资料已经提供了安装包：

![image-20210602220751081](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/2b109113ed8dbc16a19466ee90b0a9ae.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**windows解压即可**使用，非常方便。

解压好的目录如下：

![image-20210602220824668](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/22186d68f77e128740841d38268fcf91.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

进入对应的bin目录：

![image-20210602220846137](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/bdcc8240d74fadeaf7718b4077cc95f6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

双击其中的cerebro.bat文件即可启动服务。

![image-20210602220941101](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/ffe57f79c5b7b6bb8942f307e1d0adbc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问http://localhost:9000 即可进入管理界面：

![image-20210602221115763](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/0b274d50dd8e8a302eedd7f0b7a384a5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

输入你的elasticsearch的任意节点的地址和端口，点击connect即可：

![image-20210109181106866](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/c5902d22d324e59bbdfa0d80b9b3d1cc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

绿色的条，代表集群处于绿色（健康状态）。

### 4.1.3.创建索引库

**1）方法一：利用kibana的DevTools创建索引库**

在DevTools中输入指令：

```java
PUT /itcast
{
  "settings": {
    "number_of_shards": 3, // 分片数量，shard译为碎片
    "number_of_replicas": 1 // 副本数量，replica译为副本，复制品。
  },
  "mappings": {
    "properties": {
      // mapping映射定义 ...
    }
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2）方法二：利用cerebro创建索引库**

利用cerebro还可以创建索引库：

![image-20210602221409524](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/4f72cd49b5ea70bcb92b51523af4411a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

填写索引库信息：

![image-20210602221520629](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/6c075df27b044d4d3d33c27446cb510e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

点击右下角的create按钮：

![image-20210602221542745](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/4806b2cac4ef56ed7cf74b2624ab79a7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.1.4.查看分片效果

回到首页，即可查看索引库分片效果：

![image-20210602221914483](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/448cee816ff561b30b9bbd2211e165c8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 4.2.集群脑裂问题

### 4.2.1.集群职责划分，四种节点类型

**集群职责划分：**

- **候选主节点（master eligible）：**管理集群状态，处理索引库增删请求。
- **数据节点（data）：**对记录的增删改查。
- **接待节点（ingest）：**数据存储前的预处理。

**协作节点（coordinating）：**将请求路由其他节点，合并处理结果并返回。



![image-20210723223008967](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/91b705a17caf8a639dbcdfec55fe1ee8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> 主节点的类型也是master eligible，它是备选主节点选出来的。
>
> **eligible 译为合格的，合适的。**
>
> **ingest译为接待、吸收。**
>
> **coordinating译为协调，合作。**

**默认情况下**，集群中的任何一个节点都**同时具备上述四种角色**。

但是**真实的集群**一定要将**集群职责分离**：

职责分离可以让我们根据不同节点的需求分配不同的硬件去部署。而且避免业务之间的互相干扰。

**典型的es集群职责划分：LB是负载均衡**

![image-20210723223629142](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/a549595adf40b2d38aa66a10a875c5c5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 4.2.2.脑裂问题

**选举master条件：**当一个节点发现包括自己在内的多数派的master-eligible节点认为集群没有master时，就可以发起master选举。

**选举master过程：**

1. 备选主节点首先根据节点id（第一次启动时生成的随机字符串）排序，第一个节点暂定master；
2. 如果有(n+1)/2个节点投票它是mater，并且它自己也给自己投票，则它当选master；
3. 否则就暂定第二个节点为master，以此类推。

**脑裂：**master故障，集群选举出新master后旧master又恢复了，导致集群出现了两个master。  

**"脑裂"成因：**

- **网络延迟导致误判：**集群间的网络延迟导致一些节点访问不到master, 认为master 挂掉了从而选举出新的master,并对master上的分片和副本标红，分配新的主分片
- **主节点负载过高导致误判：**主节点的角色既为master又为data,访问量较大时可能会导致ES停止响应造成大面积延迟，此时其他节点得不到主节点的响应认为主节点挂掉了，会重新选取主节点
- **内存回收导致误判：**data 节点上的ES进程占用的内存较大，引发JVM的大规模内存回收，造成ES进程失去响应，从而长时间没ping通主节点，导致误判主节点下线
- **主节点故障**。

**解决方案：**

- **调大超时时间减少误判：**discovery.zen.ping_timeout节点状态的响应时间，默认为3s，可以适当调大，如果master在该响应时间的范围内没有做出响应应答，判断该节点已经挂掉了。调大参数（如6s，discovery.zen.ping_timeout:6），可适当减少误判
- **选举触发条件：**discovery.zen.minimum_master_nodes:(备选主节点数量/ 2) +1。该参数是用于控制选举条件，只有(n / 2) +1个备选主节点认为主节点故障才开始选举。在es7.0以后，已经成为默认配置，因此一般不会发生脑裂问题
- **master和data分离：**即master节点与data节点分离，限制角色
  - 主节点配置为：node.master: true，node.data: false
  - 从节点配置为：node.master: false，node.data: true  

> 脑裂**是由集群中的节点失联导致的。**
>
> **脑裂情况演示：** 
>
> 例如一个集群中，主节点与其它节点失联：
>
> ![image-20210723223804995](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/75edb6e8c23b8420a2364b4de8229bde.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 此时，node2和node3认为node1宕机（但其实只是阻塞了），就会重新选主：
>
> 宕机，即down机、死机。
>
> 指[操作系统](https://baike.baidu.com/item/操作系统/192?fromModule=lemma_inlink)无法从一个严重系统错误中恢复过来，或系统[硬件](https://baike.baidu.com/item/硬件/479446?fromModule=lemma_inlink)层面出问题，以致系统长时间无响应，而不得不重新启动计算机的现象。
>
> ![image-20210723223845754](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/70ccc7a978b77fd430f6a4a0505a2816.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 当node3当选后，集群继续对外提供服务，node2和node3自成集群，node1自成集群，两个集群数据不同步，出现数据差异。
>
> 当网络恢复后，因为集群中有两个master节点，集群状态的不一致，出现脑裂的情况：
>
> ![image-20210723224000555](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/18cf1437f7e254aee46c2ff670b71d1f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> **解决脑裂** 
>
> **解决脑裂的方案**是，要求选票超过 ( eligible节点数量 + 1 ）/ 2 才能当选为主，因此**eligible节点数量最好是奇数**。对应配置项是**discovery.zen.minimum_master_nodes**，在es7.0以后，已经成为**默认配置**，因此**一般不会发生脑裂问题**
>
> 例如：3个节点形成的集群，选票必须超过 （3 + 1） / 2 ，也就是2票。node3得到node2和node3的选票，当选为主。node1只有自己1票，没有当选。集群中依然只有1个主节点，没有出现脑裂。

### 4.2.3.小结，四种节点类型

master eligible节点的作用是什么？

data节点的作用是什么？

coordinator节点的作用是什么？

## 4.3.集群分布式存储

当新增文档时，应该保存到不同分片，保证数据均衡，那么**coordinating node如何确定数据该存储到哪个分片**呢？

### 4.3.1.文档存储到分片测试

> **一个集群里有多个节点，每个节点都是一个es实例， 每个节点保存了自己的分片和一个其他节点备份的分片。** 

**在9200端口的es插入三条数据：**

![image-20210723225006058](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/414525ebdadc824c226831d6d801a58c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![image-20210723225034637](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/5cc1dbac7dda04d828fdebfb6d00a2a5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![image-20210723225112029](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/9512a302fa99c83b4bdb48bec20c515d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

测试可以看到，**三条数据分别在不同分片：**

![image-20210723225227928](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/6d3fecac4ba653dc4f18ab5e810f9dda.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![image-20210723225342120](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/addbb3cd23d46c1d27cfe17201e9ef66.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.3.2.分片存储原理

**分布式新增如何确定分片？** 

elasticsearch会通过**hash算法来计算文档应该存储到哪个分片，跟文档id和分片数量有关：**

![image-20210723224354904](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/23bc0003154ceab5fbc66afd9557f6c8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 说明：
>
> - _routing默认是文档的id
> - 算法与分片数量有关，因此索引库一旦创建，**分片数量不能修改！**

**新增文档的流程如下：**

![image-20210723225436084](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/07fad8142c2f43068290ef073354d228.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

解读：

## 4.4.集群分布式查询，协调节点的分散和聚集

elasticsearch的查询分成两个阶段：

![image-20210723225809848](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/2069d14621a9ae2bfe5a96e11a2ea974.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 4.5.集群故障转移

集群的**master节点会监控集群中的节点状态**，如果发现有节点宕机，会立即**将宕机节点的分片数据迁移到其它节点**，确保数据安全，这个叫做**故障转移**。

**故障转移流程演示：**

**1）例如一个集群结构如图：**

![image-20210723225945963](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/809e4741abd1ae5f370aba2425370af2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

现在，node1是主节点，其它两个节点是从节点。

**2）突然，node1发生了故障：**

![image-20210723230020574](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/e977827e996a92d9d35a596756dd1d6a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**宕机后的第一件事，需要重新选主，例如选中了node2：**

![image-20210723230055974](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/196bbe497002471708686bbf0f9e32c3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**node2成为主节点后，会检测集群监控状态，发现：shard-1、shard-0没有副本节点。因此需要将node1上的数据迁移到node2、node3：**

![image-20210723230216642](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/7f67d70f2d8975c1232d6ecc98764379.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**实际演示：**

现在有三个节点，其中es01是主节点。

![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/56127c4d1d134b93b7ceef4882230595.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**令es01宕机**

```java
docker-compose stop es01
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

此时es01节点上的1主分片和0副本分片没了，主节点转到es03，控制es01节点的数据迁移到es02和03。

故障转移后，所有分片都有主分片和副本分片：

 ![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/340550391f1c4a1db66abb25e192e291.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **再恢复es01，发现主节点es03迁移出两个分片到es01：**

```java
docker-compose start es01
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](ElasticSearch基础3——聚合、补全、集群。黑马旅游检索高亮+自定义分词器+自动补全+前后端消息同步.assets/e2dbf0b90b704022a56f90fd85708f43.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





- **master节点：**对CPU要求高，但是内存要求低
- **data节点：**对CPU和内存要求都高
- **coordinating节点：**对网络带宽、CPU要求高
- 参与集群选主
- **主节点可以管理集群状态、管理分片信息、处理创建和删除索引库的请求**
- 数据的CRUD
- **路由请求**到其它节点
- **合并**查询到的**结果**，返回给用户
- 1）新增一个id=1的文档
- 2）对id做hash运算，假如得到的是2，则应该存储到shard-2
- 3）shard-2的主分片在node3节点，将数据路由到node3
- 4）保存文档
- 5）同步给shard-2的副本replica-2，在node2节点
- 6）返回结果给coordinating-node节点
- **scatter phase：分散阶段**，coordinating node会把**请求分发到每一个分片**（只有data节点保存分片数据）
- **gather phase：聚集阶段**，coordinating node汇总data node的搜索结果，并处理为最终结果集返回给用户