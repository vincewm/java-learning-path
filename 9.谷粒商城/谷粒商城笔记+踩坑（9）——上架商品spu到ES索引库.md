> **导航：**
> 
> [谷粒商城笔记+踩坑汇总篇](https://blog.csdn.net/qq_40991313/article/details/127099139?spm=1001.2014.3001.5501 "谷粒商城笔记+踩坑汇总篇")
> 
>  **Java笔记汇总：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客")

**目录**

[1、ES回顾](#%E4%B8%80%E3%80%81ES%E5%9B%9E%E9%A1%BE)

[2、ES整合商品上架](#2%E3%80%81ES%E6%95%B4%E5%90%88%E5%95%86%E5%93%81%E4%B8%8A%E6%9E%B6%C2%A0) 

[2.1、分析](#%E5%88%86%E6%9E%90)

[2.2、创建sku的es索引库](#sku%E5%9C%A8es%E4%B8%AD%E5%AD%98%E5%82%A8)

[2.2.1、两种索引库设计方案分析](#%E4%B8%A4%E7%A7%8D%E7%B4%A2%E5%BC%95%E5%BA%93%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88%E5%88%86%E6%9E%90)

[2.2.2、最终选用的索引库方案，nested类型](#%E6%9C%80%E7%BB%88%E9%80%89%E7%94%A8%E7%9A%84%E6%95%B0%E6%8D%AE%E6%A8%A1%E5%9E%8B)

[2.3、SkuEsModel模型类](#%E6%9E%84%E9%80%A0%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE)

[2.4、【库存模块】库存量查询](#%E5%BA%93%E5%AD%98%E9%87%8F%E6%9F%A5%E8%AF%A2)

[2.5、【查询模块】保存ES文档](#%E5%95%86%E5%93%81%E4%B8%8A%E6%9E%B6)

[2.5.1、常量类](#%E5%B8%B8%E9%87%8F%E7%B1%BB)

[2.5.2、controller](#controller)

[2.5.3、service](#service)

[2.6、【商品模块】上架单个spu](#%E3%80%90%E5%95%86%E5%93%81%E6%A8%A1%E5%9D%97%E3%80%91%E4%B8%8A%E6%9E%B6%E5%8D%95%E4%B8%AAspu)

[2.6.1、controller](#%E5%AE%8C%E6%95%B4%E4%BB%A3%E7%A0%81)

[2.6.2、远程调用库存模块](#%E8%BF%9C%E7%A8%8B%E8%B0%83%E7%94%A8%E5%BA%93%E5%AD%98%E6%A8%A1%E5%9D%97)

[2.6.3、【公共模块】商品常量类，添加上传成功或失败的状态码](#%E3%80%90%E5%85%AC%E5%85%B1%E6%A8%A1%E5%9D%97%E3%80%91%E5%95%86%E5%93%81%E5%B8%B8%E9%87%8F%E7%B1%BB%EF%BC%8C%E6%B7%BB%E5%8A%A0%E4%B8%8A%E4%BC%A0%E6%88%90%E5%8A%9F%E6%88%96%E5%A4%B1%E8%B4%A5%E7%9A%84%E7%8A%B6%E6%80%81%E7%A0%81)

[2.6.4、service](#2.6.4%E3%80%81service)

[2.6.5、测试](#%E8%AF%A6%E8%A7%A3)

[2.6.6、修改结果类R](#2.6.6%E3%80%81%EF%BC%88%E5%BE%85%E6%9B%B4%E6%96%B0%EF%BC%89%E6%8A%BD%E5%8F%96%E5%93%8D%E5%BA%94%E7%BB%93%E6%9E%9C)

--

## 1、ES回顾

> [elasticsearch基础1——索引、文档\_elasticsearch索引 文档\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126807267?spm=1001.2014.3001.5501 "elasticsearch基础1——索引、文档_elasticsearch索引 文档_vincewm的博客-CSDN博客")
> 
> [elasticsearch基础2——DSL查询文档,黑马旅游项目查询功能\_elasticsearch查询文档\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126819678?spm=1001.2014.3001.5501 "elasticsearch基础2——DSL查询文档,黑马旅游项目查询功能_elasticsearch查询文档_vincewm的博客-CSDN博客")[elasticsearch基础3——聚合、补全、集群\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126861326?spm=1001.2014.3001.5501 "elasticsearch基础3——聚合、补全、集群_vincewm的博客-CSDN博客")[elasticsearch基础2——DSL查询文档,黑马旅游项目查询功能\_elasticsearch查询文档\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126819678?spm=1001.2014.3001.5501 "elasticsearch基础2——DSL查询文档,黑马旅游项目查询功能_elasticsearch查询文档_vincewm的博客-CSDN博客")

## **2、ES整合商品上架** 

### 2.1、分析

**es在整个项目中的应用：**

1.对商品的全文检索功能

2.对日志的全文检索功能

![](https://i-blog.csdnimg.cn/blog_migrate/55a629c06f123f220da01ae8260b6e05.png)

![](https://i-blog.csdnimg.cn/blog_migrate/eabb0e1b9b434a5fce06de05148048a5.png)

> **为什么不用mysql？**
> 
> es比mysql检索功能强大，并且对于庞大的检索数据，es性能更好。
> 
> 因为mysql是存在磁盘中的，磁盘IO效率是很差的，尽管MySQL底层用的是B+树，在精确检索并且命中索引时IO次数可以稳定在4次以内，但如果没命中索引，则需要全表扫描，每次分段加载数据页到内存中进行读写，效率是非常差的。
> 
> ES是基于倒排索引，根据文档id获取文档并根据相关度进行排序，在海量数据查询时效率高。
> 
> **倒排索引流程：**
> 
> 1.  **分词：**将每一个文档的数据利用算法**分词**，得到一个个词条；
>     
> 2.  **映射关系表：**创建分词和文档id的映射关系表；
>     
> 3.  **词条-->id-->文档：**搜索词条时，根据映射关系表找到它对应的所有文档id，然后根据文档id正向索引查到文档。
>     
> 
> 另外，在数据量大的场景下，可以使用ES集群，将索引库从逻辑上拆分为N个分片，并且每个节点可以存储副本分片，提高可用性。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/59dcca18d2100eee01241932d51c7327.png)

**需求：**

-   在后台选择上架的商品才能在网站展示
-   上架的商品也可以被ES检索

![](https://i-blog.csdnimg.cn/blog_migrate/e9f99b0ce0d1248cfb30d213e5c9639d.png)

### 2.2、创建sku的es索引库

#### 2.2.1、两种索引库设计方案分析

-   检索的时候输入名字，这样就是需要用sku的名称去全文检索
-   检索的时候选择商品规格，规格是spu的公共属性，每个spu是一样的

**索引库设计方案1（推荐，空间换时间）：规格参数放在sku里**

缺点：如果每个sku都存储规格参数(如尺寸)，会有冗余存储，因为**每个spu下面的sku规格参数都一样。**例如spu“华为14Pro”下的sku“红色华为14Pro”，以及spu“华为手机”下的sku“蓝色华为14Pro”，这两个sku的规格参数“CPU：A14”相等。

```bash
{
    skuId:1
    spuId:11
    skyTitile:华为xx
    price:999
    saleCount:99
    attr:[
        {尺寸:5},
        {CPU:高通945},
        {分辨率:全高清}
	]
}
```

**索引库设计方案2（不推荐，传输的数据量大）：规格参数和sku分离**

```bash
sku索引
{
    spuId:1
    skuId:11
}
attr索引
{
    skuId:11
    attr:[
        {尺寸:5},
        {CPU:高通945},
        {分辨率:全高清}
	]
}
```

结论：**如果将规格参数单独建立索引，会出现检索时出现大量数据传输的问题，会引起网络故障。**

所以我们选方案一，**用空间换时间**

#### 2.2.2、最终选用的索引库方案，**nested类型**

{ “type”: “keyword” }, 保持数据精度问题，可以检索，但不分词  
“analyzer”: “ik\_smart” 中文分词器  
“index”: false, 不可被检索，不生成index  
“doc\_values”: false 默认为true，不可被聚合，es就不会维护一些聚合的信息

**这个数据模型要先在es中建立**

> **注意：**
> 
> 为了防止对象数组扁平化，商品属性字段类型设为**nested类型。**
> 
> **es数组的扁平化处理：**es存储**对象数组**时，它会将数组扁平化，也就是说**将对象数组的每个属性抽取出来**，作为一个数组。因此会出现查询紊乱的问题。
> 
> **示例：**下面user字段是对象数组类型，因为数组扁平化处理，下面结果跟期望查询结果不符：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/cb9ef612953bdabadf6d3023ba5ec6c9.png)

```bash
PUT product
{
    "mappings":{
        "properties": {
            "skuId":{ "type": "long" },    #商品sku
            "spuId":{ "type": "keyword" },  #当前sku所属的spu。
            "skuTitle": {
                "type": "text",
                "analyzer": "ik_smart"      #只有sku的标题需要被分词
            },
            "skuPrice": { "type": "keyword" },  
            "skuImg"  : { "type": "keyword" },  
            "saleCount":{ "type":"long" },
            "hasStock": { "type": "boolean" },    #是否有库存。在库存模块添加此商品库存后，此字段更为true
            "hotScore": { "type": "long"  },
            "brandId":  { "type": "long" },
            "catalogId": { "type": "long"  },
            "brandName": {"type": "keyword"}, 
            "brandImg":{
                "type": "keyword",
                "index": false,          #不可被检索
                "doc_values": false     #不可被聚合。doc_values默认为true
            },
            "catalogName": {"type": "keyword" }, 
            "attrs": {
                "type": "nested",    #对象数组防止扁平化，不能用object类型
                "properties": {
                    "attrId": {"type": "long"  },
                    "attrName": {
                        "type": "keyword",
                        "index": false,        #在后面“商城业务-检索服务”开发时这里要去掉
                        "doc_values": false    #在后面“商城业务-检索服务”开发时这里要去掉
                    },
                    "attrValue": {"type": "keyword" }
                }
            }
        }
    }
}

```

![image-20220918154851294](https://i-blog.csdnimg.cn/blog_migrate/3130e74ee9aeaafee777015bf0265246.png)

### 2.3、SkuEsModel模型类

商品上架需要在es中保存spu信息并更新spu状态信息，所以我们就建立专门的vo来接收

> SkuEsModel
> 
> 写在common模块

```java
@Data
public class SkuEsModel { //common中
    private Long skuId;
    private Long spuId;
    private String skuTitle;
    private BigDecimal skuPrice;
    private String skuImg;
    private Long saleCount;
    private boolean hasStock;
    private Long hotScore;
    private Long brandId;
    private Long catalogId;
    private String brandName;
    private String brandImg;
    private String catalogName;
    private List<Attr> attrs;

    @Data
    public static class Attr{
        private Long attrId;
        private String attrName;
        private String attrValue;
    }
}

```

### 2.4、【库存模块】库存量查询

**查询sku列表是否有库存：**

上架的话需要确定库存，所以调用ware微服务来检测是否有库存

```java
@RestController
@RequestMapping("ware/waresku")
public class WareSkuController {
    @Autowired
    private WareSkuService wareSkuService;
    
    @PostMapping(value = "/hasStock")
    public R getSkuHasStock(@RequestBody List<Long> skuIds) {
        List<SkuHasStockVo> vos = wareSkuService.getSkuHasStock(skuIds);
        return R.ok().setData(vos);
    }
}
```

实现也比较好理解，就是先用自定义的mapper查有没有库存

有的话，给库存赋值，并收集成集合

```java
@Override
public List<SkuHasStockVo> getSkuHasStock(List<Long> skuIds) {
    List<SkuHasStockVo> skuHasStockVos = skuIds.stream().map(item -> {
//根据sku_id查库存,要写mapper，主要为了真实库存减去锁定库存
        Long count = this.baseMapper.getSkuStock(item);    
        SkuHasStockVo skuHasStockVo = new SkuHasStockVo();
        skuHasStockVo.setSkuId(item);
        skuHasStockVo.setHasStock(count == null ? false : count > 0);
        return skuHasStockVo;
    }).collect(Collectors.toList());

    return skuHasStockVos;

}
```

**自定义mapper**

这里的库存并不是简单查一下库存表，需要自定义一个简单的sql。用库存减去锁定的库存即可得出！

```XML
<select id="getSkuStock" resultType="java.lang.Long">
    SELECT SUM(stock - stock_locked) FROM wms_ware_sku WHERE sku_id = #{skuId}
</select>
```

### 2.5、【查询模块】保存ES文档

#### 2.5.1、常量类

```java
public class EsConstant {

    //在es中的索引
    public static final String PRODUCT_INDEX = "gulimall_product";

    public static final Integer PRODUCT_PAGESIZE = 16;
}
```

#### 2.5.2、controller

ElasticSaveController

```java
package com.xxx.gulimall.search.controller;
@Slf4j
@RequestMapping(value = "/search/save")
@RestController
public class ElasticSaveController {

    @Autowired
    private ProductSaveService productSaveService;


    /**
     * 上架商品
     * @param skuEsModels
     * @return
     */
    @PostMapping(value = "/product")
    public R productStatusUp(@RequestBody List<SkuEsModel> skuEsModels) {

        boolean status=false;
        try {
            status = productSaveService.productStatusUp(skuEsModels);
        } catch (IOException e) {
            //log.error("商品上架错误{}",e);

            return R.error(BizCodeEnum.PRODUCT_UP_EXCEPTION.getCode(),BizCodeEnum.PRODUCT_UP_EXCEPTION.getMessage());
        }

        if(status){
            return R.error(BizCodeEnum.PRODUCT_UP_EXCEPTION.getCode(),BizCodeEnum.PRODUCT_UP_EXCEPTION.getMessage());
        }else {
            return R.ok();
        }

    }


}
```

#### 2.5.3、service

使用BulkRequest ，批量**保存**sku\_es模型类列表到**索引库**

```java
@Slf4j
@Service("productSaveService")
public class ProductSaveServiceImpl implements ProductSaveService {

    @Autowired
    private RestHighLevelClient esRestClient;

    @Override
    public boolean productStatusUp(List<SkuEsModel> skuEsModels) throws IOException {

        //1.在es中建立索引，建立号映射关系（doc/json/product-mapping.json）[kibana中执行product-mapping.txt，需要ES安装IK分词器]

        //2. 在ES中保存这些数据
        BulkRequest bulkRequest = new BulkRequest();
        for (SkuEsModel skuEsModel : skuEsModels) {
            //构造保存请求
            IndexRequest indexRequest = new IndexRequest(EsConstant.PRODUCT_INDEX);
            indexRequest.id(skuEsModel.getSkuId().toString());
            String jsonString = JSON.toJSONString(skuEsModel);
            indexRequest.source(jsonString, XContentType.JSON);
            bulkRequest.add(indexRequest);
        }


        BulkResponse bulk = esRestClient.bulk(bulkRequest, GulimallElasticSearchConfig.COMMON_OPTIONS);

        //TODO 如果批量错误
        boolean hasFailures = bulk.hasFailures();

        List<String> collect = Arrays.asList(bulk.getItems()).stream().map(item -> {
            return item.getId();
        }).collect(Collectors.toList());

        log.info("商品上架完成：{}",collect);

        return hasFailures;
    }
}
```

### 2.6、【商品模块】上架单个spu

![](https://i-blog.csdnimg.cn/blog_migrate/e9f99b0ce0d1248cfb30d213e5c9639d.png)

#### 2.6.1、controller

SpuInfoController上架

```java
/**
 * 商品上架
 */
@PostMapping("/{spuId}/up")
public R spuUp(@PathVariable("spuId") Long spuId){
    spuInfoService.up(spuId);
    return R.ok();
}
```

#### 2.6.2、远程调用库存模块

在商品模块的feign包下：

```java
@FeignClient("gulimall-ware")
public interface WareFeignService {

    @PostMapping(value = "/ware/waresku/hasStock")
    R getSkuHasStock(@RequestBody List<Long> skuIds);

}
```

商品模块启动类：

```java
@EnableFeignClients(basePackages = "com.xunqi.gulimall.product.feign")
```

然后service里就能直接@Autowired注入了。 

#### 2.6.3、【公共模块】商品常量类，添加上传成功或失败的状态码

```java
public class ProductConstant {

    public enum AttrEnum {
        ATTR_TYPE_BASE(1,"基本属性"),
        ATTR_TYPE_SALE(0,"销售属性");

        private int code;

        private String msg;

        public int getCode() {
            return code;
        }

        public String getMsg() {
            return msg;
        }

        AttrEnum(int code, String msg) {
            this.code = code;
            this.msg = msg;
        }

    }


    public enum ProductStatusEnum {
        NEW_SPU(0,"新建"),
        SPU_UP(1,"商品上架"),
        SPU_DOWN(2,"商品下架"),
        ;

        private int code;

        private String msg;

        public int getCode() {
            return code;
        }

        public String getMsg() {
            return msg;
        }

        ProductStatusEnum(int code, String msg) {
            this.code = code;
            this.msg = msg;
        }

    }


}
```

#### 2.6.4、service

**业务流程：**

1.  查询当前spu下的sku列表；
2.  将这个sku列表封装成sku\_es模型类列表；
    1.  给每个sku加上属性规格列表；
    2.  查询每个sku是否有库存，要远程调用库存模块；
    3.  给每个sku加上热度、所属品牌、所属分类名、所有可被检索的规格等属性；
3.  将收集的sku\_es模型类列表发给es保存，要远程调用查询模块。

SpuInfoServiceImpl

```java
@Override
    public void up(Long spuId) {
        //1.获得spu对应的sku集合
        List<SkuInfoEntity> skuInfoEntities = skuInfoService.getSkusBySpuId(spuId);

        //2.获得spu的基础属性实体集合
        List<ProductAttrValueEntity> baseAttrs = productAttrValueService.baseAttrListforSpu(spuId);

        //3.获得基本属性中可搜索的属性id
        //3.1获得spu基础属性实体集合中的属性id集合
        List<Long> attrIds = baseAttrs.stream().map(attr -> {
            return attr.getAttrId();
        }).collect(Collectors.toList());

        //3.2获得可搜索属性实体类对象
        List<Long> searchAttrIds = attrService.selectSearchAttrs(attrIds);

        //3.3将它们转化为set集合
        Set<Long> idSet = searchAttrIds.stream().collect(Collectors.toSet());

        //3.4对所有基础属性实体过滤，第一步是只保留可搜索属性实体类对象，第二步是给这些对象中的Attrs对象赋值，最后收集为attrsList
        List<SkuEsModel.Attrs> attrsList = baseAttrs.stream().filter(item -> {
            return idSet.contains(item.getAttrId());
        }).map(item -> {
            SkuEsModel.Attrs attrs = new SkuEsModel.Attrs();
            BeanUtils.copyProperties(item, attrs);
            return attrs;
        }).collect(Collectors.toList());

        //收集所有skuId的集合
        List<Long> skuIdList = skuInfoEntities.stream()
                .map(SkuInfoEntity::getSkuId)
                .collect(Collectors.toList());

        //TODO 1、发送远程调用，库存系统查询是否有库存
        Map<Long, Boolean> stockMap = null;
        try {
            R skuHasStock = wareFeignService.getSkuHasStock(skuIdList);
            TypeReference<List<SkuHasStockVo>> typeReference = new TypeReference<List<SkuHasStockVo>>() {};
            stockMap = skuHasStock.getData(typeReference).stream()
                    .collect(Collectors.toMap(SkuHasStockVo::getSkuId, item -> item.getHasStock()));
        } catch (Exception e) {
            log.error("库存服务查询异常：原因{}",e);
        }
//2、封装每个sku的信息
        Map<Long, Boolean> finalStockMap = stockMap;
        List<SkuEsModel> collect = skuInfoEntities.stream().map(sku -> {
            //组装需要的数据
            SkuEsModel esModel = new SkuEsModel();
            esModel.setSkuPrice(sku.getPrice());
            esModel.setSkuImg(sku.getSkuDefaultImg());

            //设置库存信息
            if (finalStockMap == null) {
                esModel.setHasStock(true);
            } else {
                esModel.setHasStock(finalStockMap.get(sku.getSkuId()));
            }

            //TODO 2、热度评分。0
            esModel.setHotScore(0L);

            //TODO 3、查询品牌和分类的名字信息
            BrandEntity brandEntity = brandService.getById(sku.getBrandId());
            esModel.setBrandName(brandEntity.getName());
            esModel.setBrandId(brandEntity.getBrandId());
            esModel.setBrandImg(brandEntity.getLogo());

            CategoryEntity categoryEntity = categoryService.getById(sku.getCatalogId());
            esModel.setCatalogId(categoryEntity.getCatId());
            esModel.setCatalogName(categoryEntity.getName());

            //设置检索属性
            esModel.setAttrs(attrsList);

            BeanUtils.copyProperties(sku,esModel);

            return esModel;
        }).collect(Collectors.toList());

        //TODO 5、将数据发给es进行保存：mall-search
        R r = searchFeignService.productStatusUp(collect);

        if (r.getCode() == 0) {
            //远程调用成功
            //TODO 6、修改当前spu的状态，具体代码看代码块后面SpuInfoDao.xml
            this.baseMapper.updaSpuStatus(spuId, ProductConstant.ProductStatusEnum.SPU_UP.getCode());
        } else {
            //远程调用失败
            //TODO 7、重复调用？接口幂等性:重试机制
        }
    }
```

> SpuInfoDao更新spu状态
> 
> ```XML
>     <update id="updaSpuStatus">
>         UPDATE pms_spu_info SET publish_status = #{code} ,update_time = NOW() WHERE id = #{spuId}
>     </update>
> ```

#### 2.6.5、测试

商品上架用到了三个微服务，分别是product、ware、search

那我们分别debug启动它们，然后在这些微服务中使用的方法中打上断点，查看调用流程

获得spu对应的sku集合

![image-20220918160846814](https://i-blog.csdnimg.cn/blog_migrate/f03771a300c3f8df7fd2263ef7014204.png)

获得spu的基础属性实体集合

> 基础属性如下：

![image-20220918161228025](https://i-blog.csdnimg.cn/blog_migrate/333ccb4d2dbc9c47c0547ae12d51b6ad.png)

给SkuEsModel.Attrs对象赋值

![image-20220918190006951](https://i-blog.csdnimg.cn/blog_migrate/8f2fde89c7611cd7dc3df253cd9e4202.png)

测试

![image-20220918192444697](https://i-blog.csdnimg.cn/blog_migrate/f4c0dc25b171b8e61c54dbec4f0e9827.png)

#### 2.6.6、修改结果类R

```java
	public <T> T getData(String key, TypeReference<T> typeReference) {
		Object data = get(key);// 默认是map类型，springmvc做的
		String jsonStr = JSON.toJSONString(data);
		T t = JSON.parseObject(jsonStr, typeReference);
		return t;
	}

	// 利用fastJson进行逆转
	// 这里要声明泛型<T>，这个泛型只跟方法有关，跟类无关。
	// 例如类上有个泛型，这里可以使用类上的泛型，就不用声明
	public <T> T getData(TypeReference<T> typeReference) {
		Object data = get("data");// 默认是map类型，springmvc做的
		String jsonStr = JSON.toJSONString(data);
		T t = JSON.parseObject(jsonStr, typeReference);
		return t;
	}

	public R setData(Object data) {
		put("data", data);
		return this;
	}
```