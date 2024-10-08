> **导航：**
> 
> [谷粒商城笔记+踩坑汇总篇](https://blog.csdn.net/qq_40991313/article/details/127099139?spm=1001.2014.3001.5501 "谷粒商城笔记+踩坑汇总篇")
> 
>  **Java笔记汇总：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客")

**目录**

[12、商品服务-新增商品](#12%E3%80%81%E6%96%B0%E5%A2%9E%E5%95%86%E5%93%81)

[12.0、效果展示](#12.1%E3%80%81%E8%B0%83%E8%AF%95%E4%BC%9A%E5%91%98%E7%AD%89%E7%BA%A7%E7%9B%B8%E5%85%B3%E6%8E%A5%E5%8F%A3)

[12.1、配置、启动会员模块](#12.1%E3%80%81%E9%85%8D%E7%BD%AE%E3%80%81%E5%90%AF%E5%8A%A8%E4%BC%9A%E5%91%98%E6%A8%A1%E5%9D%97)

[12.1.1、用户模块添加到nacos注册中心](#12.1.1%E3%80%81%E7%94%A8%E6%88%B7%E6%A8%A1%E5%9D%97%E6%B7%BB%E5%8A%A0%E5%88%B0nacos%E6%B3%A8%E5%86%8C%E4%B8%AD%E5%BF%83)

[12.1.2、配置网关路由](#12.1.2%E3%80%81%E9%85%8D%E7%BD%AE%E7%BD%91%E5%85%B3%E8%B7%AF%E7%94%B1)

[12.1.3、添加“会员等级”数据](#12.1.3%E3%80%81%E6%B7%BB%E5%8A%A0%E2%80%9C%E4%BC%9A%E5%91%98%E7%AD%89%E7%BA%A7%E2%80%9D%E6%95%B0%E6%8D%AE)

[12.2、获取当前分类关联的品牌（不用分页）](#12.2%E3%80%81%E8%8E%B7%E5%8F%96%E5%88%86%E7%B1%BB%E5%85%B3%E8%81%94%E7%9A%84%E5%93%81%E7%89%8C)

[12.2.1、分析](#12.2.1%E3%80%81%E5%88%86%E6%9E%90)

[12.2.2、新建BrandVo](#12.2.2%E3%80%81%E6%96%B0%E5%BB%BABrandVo)

[12.2.3、代码实现](#12.2.3%E3%80%81%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0%C2%A0) 

[12.2.4、测试](#12.2.4%E3%80%81%E6%B5%8B%E8%AF%95)

[12.3、获取当前分类下的分组及其关联的属性](#12.3%E3%80%81%E8%8E%B7%E5%8F%96%E5%88%86%E7%B1%BB%E4%B8%8B%E6%89%80%E6%9C%89%E5%88%86%E7%BB%84%E4%BB%A5%E5%8F%8A%E5%B1%9E%E6%80%A7)

[12.3.1、分析](#12.3.1%E3%80%81%E5%88%86%E6%9E%90%C2%A0) 

[12.3.2、代码实现](#12.3.2%E3%80%81%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0)

[12.3.3、测试](#12.3.3%E3%80%81%E6%B5%8B%E8%AF%95)

[12.4、新增商品](#12.4%E3%80%81%E6%96%B0%E5%A2%9E%E5%95%86%E5%93%81)

[12.4.1、分析](#12.4.1%E3%80%81%E5%88%86%E6%9E%90)

[12.4.2、填写表单](#12.4.2%E3%80%81%E5%A1%AB%E5%86%99%E8%A1%A8%E5%8D%95)

[12.4.3、vo类封装表单json数据](#12.4.3%E3%80%81vo%E7%B1%BB%E5%B0%81%E8%A3%85%E8%A1%A8%E5%8D%95json%E6%95%B0%E6%8D%AE)

[12.4.4、新增业务流程分析](#12.4.4%E3%80%81%E6%96%B0%E5%A2%9E%E4%B8%9A%E5%8A%A1%E6%B5%81%E7%A8%8B%E5%88%86%E6%9E%90)

[12.4.5、保存商品模块的商品信息](#12.4.5%E3%80%81%E4%BF%9D%E5%AD%98%E5%95%86%E5%93%81%E6%A8%A1%E5%9D%97%E7%9A%84%E5%95%86%E5%93%81%E4%BF%A1%E6%81%AF)

[12.4.6、保存优惠券模块的商品信息，feign远程调用](#12.4.6%E3%80%81%E4%BF%9D%E5%AD%98%E4%BC%98%E6%83%A0%E5%88%B8%E6%A8%A1%E5%9D%97%E7%9A%84%E5%95%86%E5%93%81%E4%BF%A1%E6%81%AF%EF%BC%8Cfeign%E8%BF%9C%E7%A8%8B%E8%B0%83%E7%94%A8)

[12.5、添加复合配置、限制内存](#12.5%E3%80%81%E5%86%85%E5%AD%98%E8%B0%83%E4%BC%98)

[12.6、报错loadbalancer解决](#12.6%E3%80%81%E5%95%86%E5%93%81%E4%BF%9D%E5%AD%98debug)

[12.7、商品保存debug、解决其他报错](#12.7%E3%80%81%E5%95%86%E5%93%81%E4%BF%9D%E5%AD%98debug%E3%80%81%E8%A7%A3%E5%86%B3%E5%85%B6%E4%BB%96%E6%8A%A5%E9%94%99)

--

## 12、商品服务-新增商品

### 12.0、效果展示

todo。这节写后补上 

### 12.1、配置、启动会员模块

进入“发布商品”页面会发获取会员等级的请求，所以第一步要先配置、启动会员模块。

![](https://i-blog.csdnimg.cn/blog_migrate/cb564542cd53d5940f8c868599226c7b.png)

#### 12.1.**1、用户模块添加到nacos注册中心**

修改gulimall-member配置文件，将用户模块添加到服务注册中心，然后启动gulimall-member服务 

![](https://i-blog.csdnimg.cn/blog_migrate/f1f18937ae0c30c1b069ff58cca470d9.png)

启动成功： 

![](https://i-blog.csdnimg.cn/blog_migrate/dde2ec7731bc1a44dab4f70d23291173.png)

![](https://i-blog.csdnimg.cn/blog_migrate/c66d7f86912cc8bb1c8e62fca37876aa.png)

> “获取所有会员等级”功能，在逆向工程时已经自动生成了。url:`/member/memberlevel/list`

#### 12.1.2、配置网关路由

网关模块修改yml，用户路由（/api/member/\*\*）要放到人人管理后台路由（/api/\*\*）前面，因为路由路径更具体。

```bash
#用户模块路由
        - id: member_route
          uri: lb://gulimall-member
          predicates:
            - Path=/api/member/**
          filters:
#/api/member/**重写成/menber/**
            - RewritePath=/api/(?<segment>.*),/$\{segment}
```

> 当前网关模块的yml： 
> 
> ```bash
> server:
>   port: 88
> spring:
>   cloud:
>     nacos:
>       discovery:
>         server-addr: 127.0.0.1:8848
>     gateway:
>       routes:
> #商品模块路由
>         - id: product_route
>           uri: lb://gulimall-product
>           predicates:
>             - Path=/api/product/**  #http://localhost:88/api/product/category/list/tree转发http://localhost:10000/product/category/list/tree
>           filters:
>             - RewritePath=/api/(?<segment>.*),/$\{segment}
> 
> # oss等第三方模块路由
>         - id: third_party_route
>           uri: lb://gulimall-third-party
>           predicates:
>             - Path=/api/thirdparty/**
>           filters:
> #            http://localhost:88/api/thirdparty/oss/policy--->http://localhost:30000/oss/policy
>             - RewritePath=/api/thirdparty/(?<segment>.*),/$\{segment}
> #用户模块路由
>         - id: member_route
>           uri: lb://gulimall-member
>           predicates:
>             - Path=/api/member/**
>           filters:
>             - RewritePath=/api/(?<segment>.*),/$\{segment}
> #人人管理后台，路径路由。路由id，自定义，只要唯一即可
>         - id: admin_route
>           # uri路由的目标地址。lb就是负载均衡，后面跟服务名称。
>           uri: lb://renren-fast
>           #断言工厂的Path，请求路径必须符合指定规则，才能进行转发
>           predicates:
>             - Path=/api/**    # 把所有api开头的请求都转发给renren-fast
>           #局部过滤器。回顾默认过滤器default-filters是与routes同级
>           filters:
>             - RewritePath=/api/(?<segment>.*),/renren-fast/$\{segment}
>             # 默认规则， 请求过来：http://localhost:88/api/captcha.jpg   转发-->  http://renren-fast:8080/api/captcha.jpg
>             # 但是真正的路径是http://renren-fast:8080/renren-fast/captcha.jpg
>             # 所以使用路径重写把/api/* 改变成 /renren-fast/*
>   application:
>     name: gulimall-gateway
> logging:
>   level:
>     com.vince.gulimall: debug
> ```

重启网关模块，发现“会员列表”和“会员等级”请求已经不报错404： 

![](https://i-blog.csdnimg.cn/blog_migrate/170be3db2262eddcda117ac7b5016550.png)

#### 12.1.3、添加“会员等级”数据

点击 用户系统-会员等级 

添加一些数据

![](https://i-blog.csdnimg.cn/blog_migrate/3d535a60a49560dea46b5da8efc5cb9c.png)

然后进入“发布商品”页面，就不用请求会员等级报错：

![](https://i-blog.csdnimg.cn/blog_migrate/6a1e7a95b9960ed4d04f1f4a6d2b78b2.png)

### 12.2、获取当前分类关联的品牌（不用分页）

#### 12.2.1、分析

**需求：**发布商品时，选择分类后，会发请求获取当前分类关联的品牌，所以需要编写这个业务，下面是完成后的效果：

![](https://i-blog.csdnimg.cn/blog_migrate/d109eb5107876720125a687d774d0cc6.png)

**请求14：**`/product/categorybrandrelation/brands/list`

-   新增商品时，点击商品的分类，要获取与该分类关联的所有品牌id和name

![](https://i-blog.csdnimg.cn/blog_migrate/717f844b41ba01f0ed5d9d9515c3d4cb.png)

#### 12.2.**2、新建BrandVo**

> **因为只需要品牌id和name，也可以不新建vo**，使用CategoryBrandRelationEntity响应数据：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/debdb8bc6db324708a0b7daae57bec9e.png)
> 
> CategoryBrandRelationController中一步到位：
> 
> ```java
>     /**
>      * 获取当前分类关联的所有品牌id和name
>      * @param catId
>      * @return
>      */
>     @GetMapping("/brands/list")
>     public R relationBrandsList(@RequestParam(value = "catId",required = true) Long catId){
>         List<CategoryBrandRelationEntity> categoryBrandRelationEntities = categoryBrandRelationService.list(
>                 new LambdaQueryWrapper<CategoryBrandRelationEntity>().eq(CategoryBrandRelationEntity::getCatelogId, catId)
>         );
>         return R.ok().put("data",categoryBrandRelationEntities);
>     }
> ```

```java
@Data
public class BrandVo {
    private Long brandId;
    private String brandName;
}
```

#### 12.2.3、代码实现 

CategoryBrandRelationController

```java
/**
    * 获取当前分类关联的所有品牌
     * 1、 Controller: 处理请求，接受和校验数据
     * 2、Service接受controller传来的数据，进行业务处理
     * 3、Controller接受Service处理完的数据，封装成页面指定的vo
    */
    @GetMapping("/brands/list")
    public R relationBrandsList(@RequestParam(value = "catId", required = true) Long catId){
        List<BrandEntity> vos = categoryBrandRelationService.getBrandsByCatId(catId);
//遍历拷贝vos到brandVo
        List<BrandVo> collect = vos.stream().map(item -> {
            BrandVo brandVo = new BrandVo();
            brandVo.setBrandId(item.getBrandId());
            brandVo.setBrandName(item.getName());

            return brandVo;
        }).collect(Collectors.toList());

        return R.ok().put("data", collect);
    }
```

CategoryBrandRelationServiceImpl

```java
@Autowired
BrandService brandService;

@Override
public List<BrandEntity> getBrandsByCatId(Long catId) {
    List<CategoryBrandRelationEntity> catelogId = this.baseMapper.selectList(new QueryWrapper<CategoryBrandRelationEntity>().eq("catelog_id", catId));
    List<BrandEntity> collect = catelogId.stream().map(item -> {
        Long brandId = item.getBrandId();
        BrandEntity byId = brandService.getById(brandId);
        return byId;
    }).collect(Collectors.toList());
    return collect;
}
```

> 如果报错：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/13bfc30be35e3080a0dfd215bc4cd845.png)
> 
> 就把brandService.getById改成brandDao.selectById 

>  **也可以不新建vo**，使用CategoryBrandRelationEntity响应数据：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/debdb8bc6db324708a0b7daae57bec9e.png)
> 
> CategoryBrandRelationController中一步到位：
> 
> ```java
>     /**
>      * 获取当前分类关联的所有品牌id和name
>      * @param catId
>      * @return
>      */
>     @GetMapping("/brands/list")
>     public R relationBrandsList(@RequestParam(value = "catId",required = true) Long catId){
>         List<CategoryBrandRelationEntity> categoryBrandRelationEntities = categoryBrandRelationService.list(
>                 new LambdaQueryWrapper<CategoryBrandRelationEntity>().eq(CategoryBrandRelationEntity::getCatelogId, catId)
>         );
>         return R.ok().put("data",categoryBrandRelationEntities);
>     }
> ```

#### 12.2.4、测试

再次发布商品，选择分类后就能查到该分类下的品牌了：

![](https://i-blog.csdnimg.cn/blog_migrate/d109eb5107876720125a687d774d0cc6.png)

### 12.3、获取当前分类下的分组及其关联的属性

#### 12.3.1、分析 

**需求：**录入规格参数时要获取当前分类下所有分组和关联属性，进行选择分组、规格参数

 ![](https://i-blog.csdnimg.cn/blog_migrate/ebbe59b2e3e64c80ce1b545440f0e4be.png)

> **无法上传图片问题**
> 
> 如果在填写基本信息时候无法上传图片，开启第三方模块。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/fb62c5527abf75875dc5af5a582c6caa.png)
> 
> 检测bucket域名，参考下文7.3.10修改前端，替换成自己的**Bucket域名**：
> 
> [谷粒商城笔记+踩坑（4）——商品服务-品牌管理、云存储](https://blog.csdn.net/qq_40991313/article/details/127058164?spm=1001.2014.3001.5501 "谷粒商城笔记+踩坑（4）——商品服务-品牌管理、云存储")
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/23dc41a5750fd232cadefa6cdfc80859.png)

**请求17：**`/product/attrgroup/{catelogId}/withattr`

**响应数据：**

![](https://i-blog.csdnimg.cn/blog_migrate/9ea3a207c6beb9d2a169e518b3581a18.png)

#### 12.3.2、代码实现

新建AttrGroupWithAttrsVo

```java
@Data
public class AttrGroupWithAttrsVo extends AttrGroupEntity {

    private List<AttrEntity> attrs;
}
```

AttrGroupController

```java
@GetMapping("/{catelogId}/withattr")
public R getAttrGroupWithAttrs(@PathVariable("catelogId") Long catelogId){
    //1、查出当前分类下的所有属性分组
    //2、查出每个属性分组的所有属性
    List<AttrGroupWithAttrsVo> vos = attrGroupService.getAttrGroupWithAttrsByCatelogId(catelogId);
    return R.ok().put("data", vos);

}
```

AttrGroupServiceImpl

```java
    /**
     * 获取当前分类下所有分组以及属性
     * @param catelogId
     * @return
     */
    @Override
    public List<AttrGroupWithAttrsVo> getAttrGroupWithAttrsByCatelogId(Long catelogId) {
        //查询此分类下所有分组
        List<AttrGroupEntity> attrGroupEntities = this.list(new LambdaQueryWrapper<AttrGroupEntity>().eq(AttrGroupEntity::getCatelogId, catelogId));

        //每个分组查询规格属性
        List<AttrGroupWithAttrsVo> vos=attrGroupEntities.stream().map(item->{
            AttrGroupWithAttrsVo vo = new AttrGroupWithAttrsVo();
            BeanUtils.copyProperties(item,vo);
            //在关联表里查询此分组的规格属性
            Long groupId = item.getAttrGroupId();
            //有编写这个业务，获取分组关联的属性list
            vo.setAttrs(attrService.getRelationAttr(groupId));
            return vo;
        }).collect(Collectors.toList());
        return vos;
    }
```

#### 12.3.3、测试

重启商品模块，可以看到当前分类下的分组和规格参数已显示： 

![](https://i-blog.csdnimg.cn/blog_migrate/46f0367de3500a62890f790788766f89.png)

> **无法上传图片问题**
> 
> 如果在填写基本信息时候无法上传图片，开启第三方模块。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/fb62c5527abf75875dc5af5a582c6caa.png)
> 
> 检测bucket域名，参考下文7.3.10修改前端，替换成自己的**Bucket域名**：
> 
> [谷粒商城笔记+踩坑（4）——商品服务-品牌管理、云存储](https://blog.csdn.net/qq_40991313/article/details/127058164?spm=1001.2014.3001.5501 "谷粒商城笔记+踩坑（4）——商品服务-品牌管理、云存储")
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/23dc41a5750fd232cadefa6cdfc80859.png)

### 12.4、新增商品

#### 12.4.1、分析

url：`/product/spuinfo/save`

#### 12.4.2、填写表单

参考商品：[【AppleiPhone 14 Pro】Apple iPhone 14 Pro (A2892) 256GB 暗紫色 支持移动联通电信5G 双卡双待手机【行情 报价 价格 评测】-京东](https://item.jd.com/100038004389.html "【AppleiPhone 14 Pro】Apple iPhone 14 Pro  (A2892) 256GB 暗紫色 支持移动联通电信5G 双卡双待手机【行情 报价 价格 评测】-京东")

图片地址：D:\\download\\尚硅谷谷粒商城电商项目等1个文件\\尚硅谷谷粒商城电商项目\\资料源码\\docs\\pics

 基本信息

![](https://i-blog.csdnimg.cn/blog_migrate/99727af67776bcb661852df3504c83c0.png)

规格参数 

![](https://i-blog.csdnimg.cn/blog_migrate/b344645a0ff5621a2a4db7b0a7398e13.png) 销售属性

![](https://i-blog.csdnimg.cn/blog_migrate/a7b876286190989e1bd893d5753edba4.png)

> 销售属性展示的是“可选值”。这里自定义“+” 号，可以新加销售属性的可选值，仅针对于这个商品，不会改动销售属性的数据库。

sku信息 

> 根据笛卡尔积计算销售属性，得出相应数量的sku信息。一个sku决定了一个价格。

![](https://i-blog.csdnimg.cn/blog_migrate/5a0bb067912491785993e0f5bb5dc0ce.png)

![](https://i-blog.csdnimg.cn/blog_migrate/0cb928e2f046b5d21070cccd8eb26a9d.png)

#### 12.4.3、vo类封装表单json数据

点击下一步“保存商品信息” ，然后点击取消，复制控制台的json数据。

![](https://i-blog.csdnimg.cn/blog_migrate/66da9556227291b25bcbdf8a5b4aae02.png)

**json格式化工具：**

```java
https://www.bejson.com/
```

**json生成java类：**

```java
https://www.bejson.com/json2javapojo/new/
```

**1.生成vo类并下载，复制到自己项目的vo包下**

![](https://i-blog.csdnimg.cn/blog_migrate/ebb21facf320d788bbdad34e498ec960.png)

**2.把所有id字段改成Long类型，把所有金额相关字段的类型由String或Double改成BigDecimal类型，把get和set方法改成@Data**

1.  SpuSaveVo的brandId和catelogId改成Long，weight改成BigDecimal。
2.  Bounds都改成BigDecimal
3.  BaseAttrs的attrId改成Long；price,discount,fullPrice,reducePrice改成BigDecimal ;
4.  Attr的attrId改成Long
5.  MemberPrice的id改成Long，price改成BigDecimal； 

> **BigDecimal**
> 
> Java在java.math包中提供的API类BigDecimal，用来对超过16位有效位的数进行精确的运算。双精度浮点型变量double可以处理16位有效数。在实际应用中，需要对更大或者更小的数进行运算和处理。float和double只能用来做科学计算或者是工程计算，在商业计算中要用java.math.BigDecimal。BigDecimal所创建的是对象，我们不能使用传统的+、-、\*、/等算术运算符直接对其对象进行数学运算，而必须调用其相对应的方法。方法中的参数也必须是BigDecimal的对象。构造器是类的特殊方法，专门用来创建对象，特别是带有参数的对象。
> 
>   
>  

#### 12.4.4、新增业务流程分析

1.  保存spu基本信息`pms_spu_info`
2.  保存spu的描述图片`pms_spu_info_desc`
3.  保存spu的图片集`pms_spu_images`
4.  保存spu的规格参数`pms_product_attr_value`
5.  保存spu的积分信息`gulimall_sms`\->`sms_spu_bounds`
6.  保存spu对应的所有sku信息
    1.  sku的基本信息`pms_sku_info`
    2.  sku的图片信息`pms_sku_images`
    3.  sku的销售属性信息`pms_sku_sale_attr_value`
    4.  sku的优惠、满减等信息`gulimall_sms`\->`sms_sku_ladder`/`sms_sku_full_reduction`/`sms_member_price`

#### 12.4.5、**保存商品模块的商品信息**

SpuInfoController

```java
    /**
     * 保存
     */
    @RequestMapping("/save")
    public R save(@RequestBody SpuSaveVo spuSaveVo){
		spuInfoService.saveSpuInfo(spuSaveVo);

        return R.ok();
    }
```

SpuInfoServiceImpl

> **注意：**
> 
> -   保存sku的优惠、满减信息时，需要用到gulimall-coupon模块的服务，所以这里要用**open-feign远程调用**。

```java
@Autowired
SkuInfoService skuInfoService;

@Autowired
SkuImagesService skuImagesService;

@Autowired
SkuSaleAttrValueService skuSaleAttrValueService;

@Autowired
CouponFeignService couponFeignService;

    @Transactional
    @Override
    public void saveSpuInfo(SpuSaveVo vo) {
        //1、保存spu基本信息`pms_spu_info`
        SpuInfoEntity infoEntity = new SpuInfoEntity();
        BeanUtils.copyProperties(vo, infoEntity);
        infoEntity.setCreateTime(new Date());
        infoEntity.setUpdateTime(new Date());
        this.save(infoEntity);

        //2、保存spu的描述图片`pms_spu_info_desc`
        List<String> decript = vo.getDecript();
        SpuInfoDescEntity descEntity = new SpuInfoDescEntity();
        descEntity.setSpuId(infoEntity.getId());
        //String.join方法可以快速拼接list里的字符串
        descEntity.setDecript(String.join(",", decript));
        spuInfoDescService.save(descEntity);

        //3、保存spu的图片集`pms_spu_images`
        List<String> images = vo.getImages();
        if (images != null && images.size() != 0) {
            List<SpuImagesEntity> collect = images.stream().map(image -> {
                SpuImagesEntity imagesEntity = new SpuImagesEntity();
                imagesEntity.setSpuId(infoEntity.getId());
                imagesEntity.setImgUrl(image);
                return imagesEntity;
            }).collect(Collectors.toList());
            imagesService.saveBatch(collect);
        }

        //4、保存spu的规格参数`pms_product_attr_value`
        List<BaseAttrs> baseAttrs = vo.getBaseAttrs();
        List<ProductAttrValueEntity> productAttrValueEntityList = baseAttrs.stream().map(attr -> {
            ProductAttrValueEntity valueEntity = new ProductAttrValueEntity();
            valueEntity.setAttrId(attr.getAttrId());
            AttrEntity byId = attrService.getById(attr.getAttrId());
            valueEntity.setAttrName(byId.getAttrName());
            valueEntity.setAttrValue(attr.getAttrValues());
            valueEntity.setQuickShow(attr.getShowDesc());
            valueEntity.setSpuId(infoEntity.getId());
            return valueEntity;
        }).collect(Collectors.toList());
        productAttrValueService.saveBatch(productAttrValueEntityList);


        //5、保存spu的积分信息`gulimall_sms`->`sms_spu_bounds`
        Bounds bounds = vo.getBounds();
        SpuBoundTo spuBoundTo = new SpuBoundTo();
        BeanUtils.copyProperties(bounds, spuBoundTo);
        spuBoundTo.setSpuId(infoEntity.getId());
        R r = couponFeignService.saveSpuBounds(spuBoundTo);
        if (r.getCode() != 0){
            log.error("远程保存spu积分信息失败");
        }

        //6、保存spu对应的所有sku信息
        List<Skus> skus = vo.getSkus();
        if (skus != null && skus.size() > 0) {
            skus.forEach(item -> {
                String defaultImg = "";
                //查找出默认图片
                for (Images image : item.getImages()) {
                    if (image.getDefaultImg() == 1) {
                        defaultImg = image.getImgUrl();
                    }
                }
                //6.1、sku的基本信息`pms_sku_info`
                //skus列表里的每个item赋值给sku_info实体类
                SkuInfoEntity skuInfoEntity = new SkuInfoEntity();
                BeanUtils.copyProperties(item, skuInfoEntity);
                skuInfoEntity.setSpuId(infoEntity.getId());
                skuInfoEntity.setBrandId(infoEntity.getBrandId());
                skuInfoEntity.setCatalogId(infoEntity.getCatalogId());
                skuInfoEntity.setSaleCount(0L); //销量
                skuInfoEntity.setSkuDefaultImg(defaultImg);

                skuInfoService.save(skuInfoEntity);

                //6.2、sku的图片信息`pms_sku_images`
                Long skuId = skuInfoEntity.getSkuId();

                List<SkuImagesEntity> skuImagesEntities = item.getImages().stream().map(img -> {
                    SkuImagesEntity skuImagesEntity = new SkuImagesEntity();
                    skuImagesEntity.setSkuId(skuId);
                    skuImagesEntity.setImgUrl(img.getImgUrl());
                    skuImagesEntity.setDefaultImg(img.getDefaultImg());
                    return skuImagesEntity;
                }).collect(Collectors.toList());
                skuImagesService.saveBatch(skuImagesEntities);

                //6.3、sku的销售属性信息`pms_sku_sale_attr_value`
                List<Attr> attr = item.getAttr();
                List<SkuSaleAttrValueEntity> skuSaleAttrValueEntities = attr.stream().map(a -> {
                    SkuSaleAttrValueEntity skuSaleAttrValueEntity = new SkuSaleAttrValueEntity();
                    skuSaleAttrValueEntity.setSkuId(skuId);
                    BeanUtils.copyProperties(a, skuSaleAttrValueEntity);
                    return skuSaleAttrValueEntity;
                }).collect(Collectors.toList());
                skuSaleAttrValueService.saveBatch(skuSaleAttrValueEntities);


                //6.4、sku的优惠、满减等信息`gulimall_sms`->`sms_sku_ladder`/`sms_sku_full_reduction`/`sms_member_price`
                SkuReductionTo skuReductionTo = new SkuReductionTo();
                BeanUtils.copyProperties(item, skuReductionTo);
                skuReductionTo.setSkuId(infoEntity.getId());
                R r1 = couponFeignService.saveSkuReduction(skuReductionTo);
                if (r1.getCode() != 0){
                    log.error("远程保存优惠信息失败");
                }
            });
        }
    }
```

#### 12.4.6、**保存优惠券模块的商品信息，feign远程调用**

**1.common模块创建to，用于不同服务间传数据**

> **TO:Transfer Object 数据传输对象**  
> 在应用程序不同关系之间传输的对象。

在`common模块`中新建common.to.SpuBoundTo用来做远程调用积分数据传输

```java
@Data
public class SpuBoundTo {

    private Long spuId;
    private BigDecimal buyBounds;
    private BigDecimal growBounds;
}
```

在`common模块`中新建common.to.`SkuReductionTo`用来做远程调用满减数据传输

```java
@Data
public class SkuReductionTo {
    private Long skuId;
    private int fullCount;
    private BigDecimal discount;
    private int countStatus;
    private BigDecimal fullPrice;
    private BigDecimal reducePrice;
    private int priceStatus;
    private List<MemberPrice> memberPrice;
}
```

在`common`中新建`MemberPrice`

```java
@Data
public class MemberPrice {

    private Long id;
    private String name;
    private BigDecimal price;
    
}
```

**2.引导类注解扫描远程调用的包**

在GulimallProductApplication中注解feign包扫描

> 也可以不注解，默认也能扫描到。因为目前引导类和feign同级，都在product包下，可以扫描到。

```java
@SpringBootApplication
@EnableDiscoveryClient
@EnableFeignClients(basePackages = "com.vince.gulimall.product.feign")
@EnableTransactionManagement
public class GulimallProductApplication {

    public static void main(String[] args) {
        SpringApplication.run(GulimallProductApplication.class, args);
        System.err.println("商品模块已启动");
    }
}
```

**3.product远程调用coupon服务保存积分和满减信息** 

> SpuInfoServiceImpl中保存coupon模块的信息：
> 
> ```java
>         //5、保存spu的积分信息；gulimall_sms->sms_spu_bounds
>         Bounds bounds = vo.getBounds();
>         SpuBoundTo spuBoundTo = new SpuBoundTo();
>         BeanUtils.copyProperties(bounds,spuBoundTo);
>         spuBoundTo.setSpuId(infoEntity.getId());
>         R r = couponFeignService.saveSpuBounds(spuBoundTo);
>         if(r.getCode() != 0){
>             log.error("远程保存spu积分信息失败");
>         }
> ```
> 
> ```java
>                 // //6.4）、sku的优惠、满减等信息；gulimall_sms->sms_sku_ladder\sms_sku_full_reduction\sms_member_price
>                 SkuReductionTo skuReductionTo = new SkuReductionTo();
>                 BeanUtils.copyProperties(item,skuReductionTo);
>                 skuReductionTo.setSkuId(skuId);
>                 if(skuReductionTo.getFullCount() >0 || skuReductionTo.getFullPrice().compareTo(new BigDecimal("0")) == 1){
>                     R r1 = couponFeignService.saveSkuReduction(skuReductionTo);
>                     if(r1.getCode() != 0){
>                         log.error("远程保存sku优惠信息失败");
>                     }
>                 }
> ```

在`product`模块的product.feign包新建CouponFeignService接口，用来远程调用Coupon服务。 

一共调用了两个服务`"coupon/spubounds/save"`和`"coupon/skufullreduction/saveInfo"，`即保存积分和满减：

```java
@FeignClient("gulimall-coupon")
public interface CouponFeignService {

    /**
    *1、CouponFeginService.saveSpuBounds(spuBoudnTo);
     *  1)、@RequestBody 将这个对象转化为json
     *  2)、找到gulimall-coupon服务，给coupon/spubounds/save发送请求
     *      将上一步转的json放在请求体位置，发送数据
     *  3)、对方服务接受请求，请求体里面有json数据
     *      public R save(@RequestBody SpuBoundsEntity spuBounds);
     *      将请求体的json转化为SpuBoundsEntity;
     * 只要json数据模型是兼容的。双方无需使用同一个to
    *@param:[spuBoundTo]
    *@return:com.xmh.common.utils.R
    *@date: 2021/8/18 1:28
    */
    @PostMapping("coupon/spubounds/save")
    R saveSpuBounds(@RequestBody SpuBoundTo spuBoundTo);

    @PostMapping("coupon/skufullreduction/saveInfo")
    R saveSkuReduction(@RequestBody SkuReductionTo skuReductionTo);
}
```

在coupon模块的`SkuFullReductionController`中新建方法

```java
    @PostMapping("/saveInfo")
    public R saveInfo(@RequestBody SkuReductionTo skuReductionTo){
        skuFullReductionService.saveSkuReduction(skuReductionTo);
        return R.ok();
    }
```

在`SkuFullReductionServiceImpl`中实现

```java
    public void saveSkuReduction(SkuReductionTo reductionTo) {
        //1、// //5.4）、sku的优惠、满减等信息；gulimall_sms->sms_sku_ladder\sms_sku_full_reduction\sms_member_price
        //sms_sku_ladder
        SkuLadderEntity skuLadderEntity = new SkuLadderEntity();
        skuLadderEntity.setSkuId(reductionTo.getSkuId());
        skuLadderEntity.setFullCount(reductionTo.getFullCount());
        skuLadderEntity.setDiscount(reductionTo.getDiscount());
        skuLadderEntity.setAddOther(reductionTo.getCountStatus());
        if(reductionTo.getFullCount() > 0){
            skuLadderService.save(skuLadderEntity);
        }




        //2、sms_sku_full_reduction
        SkuFullReductionEntity reductionEntity = new SkuFullReductionEntity();
        BeanUtils.copyProperties(reductionTo,reductionEntity);
        if(reductionEntity.getFullPrice().compareTo(new BigDecimal("0"))==1){
            this.save(reductionEntity);
        }


        //3、sms_member_price
        List<MemberPrice> memberPrice = reductionTo.getMemberPrice();
        List<MemberPriceEntity> collect=null;
        //坑点，空指针异常
        if(memberPrice!=null){
            collect = memberPrice.stream().map(item -> {
                MemberPriceEntity priceEntity = new MemberPriceEntity();
                priceEntity.setSkuId(reductionTo.getSkuId());
                priceEntity.setMemberLevelId(item.getId());
                priceEntity.setMemberLevelName(item.getName());
                priceEntity.setMemberPrice(item.getPrice());
                priceEntity.setAddOther(1);
                return priceEntity;
            }).filter(item->{
                return item.getMemberPrice().compareTo(new BigDecimal("0")) == 1;
            }).collect(Collectors.toList());
        }


        memberPriceService.saveBatch(collect);
    }
```

common模块的R结果类加上获取状态码方法，方便判断远程调用是否成功

```java
public Integer getCode(){
   return Integer.parseInt((String) this.get("code"));
}
```

### 12.5、添加复合配置、限制内存

1、新建复合Compound

![](https://i-blog.csdnimg.cn/blog_migrate/335006628c3446947c492518ee86b4b6.png)

![](https://i-blog.csdnimg.cn/blog_migrate/f94865439e8cc5d709459cf3517f347e.png)

2、把服务添加到新建的compound里

![](https://i-blog.csdnimg.cn/blog_migrate/43ccd97075f9ec7740404dff135313fd.png)

3、设置每个项目最大占用内存为100M

```java
-Xmx100m
```

 ![](https://i-blog.csdnimg.cn/blog_migrate/a98f664e2c76ee2fe5e3b0ce664af894.png)

![image-20210927214421128](https://i-blog.csdnimg.cn/blog_migrate/ce9f81b63661dc465394087ea0fd8b1d.png)

4.设置compound命名后，点确定：

![](https://i-blog.csdnimg.cn/blog_migrate/52b2cc54832ca603c4d53c02d8905e8c.png)

5、启动或重启复合配置

![](https://i-blog.csdnimg.cn/blog_migrate/9272aae44344b4f4127fc95b550bb536.png)

启动后此复合包含的六个模块就都会启动成功，如果有报错请看下一节报错解决。 

![](https://i-blog.csdnimg.cn/blog_migrate/19a1f78a8659b12f2597be06a86271a1.png)

### 12.6、报错loadbalancer解决

**如果product模块启动报错**

```java
No Feign Client for loadBalancing defined. Did you forget to include spring-cloud-starter-loadbalancer?
```

**原因：**SpringCloud Feign在Hoxton.M2 RELEASED版本之后抛弃了Ribbon，使用了spring-cloud-loadbalancer，所以我们这里还需要引入spring-cloud-loadbalancer的依赖，否则就会报错。

**解决：**

common模块的pom引入依赖：

```XML
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-loadbalancer</artifactId>
            <version>3.1.4</version>
        </dependency>
```

nacos里排除ribbon：

```XML
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
            <exclusions>
                <exclusion>
                    <groupId>org.springframework.cloud</groupId>
                    <artifactId>spring-cloud-netflix-ribbon</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
```

### 12.7、商品保存debug、解决其他报错

> 如果自己网页没出意外，就重新点击保存商品，否则就重新发请求。
> 
> POST
> 
> ```java
> http://localhost:88/api/product/spuinfo/save
> ```
> 
> 请求参数样式：
> 
> ```java
> {
> 	"spuName": "Apple XR",
> 	"spuDescription": "Apple XR",
> 	"catalogId": 225,
> 	"brandId": 12,
> 	"weight": 0.048,
> 	"publishStatus": 0,
> 	"decript": ["https://gulimall-hello.oss-cn-beijing.aliyuncs.com/2019-11-22//66d30b3f-e02f-48b1-8574-e18fdf454a32_f205d9c99a2b4b01.jpg"],
> 	"images": ["https://gulimall-hello.oss-cn-beijing.aliyuncs.com/2019-11-22//dcfcaec3-06d8-459b-8759-dbefc247845e_5b5e74d0978360a1.jpg", "https://gulimall-hello.oss-cn-beijing.aliyuncs.com/2019-11-22//5b15e90a-a161-44ff-8e1c-9e2e09929803_749d8efdff062fb0.jpg"],
> 	"bounds": {
> 		"buyBounds": 500,
> 		"growBounds": 6000
> 	},
> 	"baseAttrs": [{
> 		"attrId": 7,
> 		"attrValues": "aaa;bb",
> 		"showDesc": 1
> 	}, {
> 		"attrId": 8,
> 		"attrValues": "2019",
> 		"showDesc": 0
> 	}],
> 	"skus": [{
> 		"attr": [{
> 			"attrId": 9,
> 			"attrName": "颜色",
> 			"attrValue": "黑色"
> 		}, {
> 			"attrId": 10,
> 			"attrName": "内存",
> 			"attrValue": "6GB"
> 		}],
> 		"skuName": "Apple XR 黑色 6GB",
> 		"price": "1999",
> 		"skuTitle": "Apple XR 黑色 6GB",
> 		"skuSubtitle": "Apple XR 黑色 6GB",
> 		"images": [{
> 			"imgUrl": "https://gulimall-hello.oss-cn-beijing.aliyuncs.com/2019-11-22//dcfcaec3-06d8-459b-8759-dbefc247845e_5b5e74d0978360a1.jpg",
> 			"defaultImg": 1
> 			}, {
> 			"imgUrl": "https://gulimall-hello.oss-cn-beijing.aliyuncs.com/2019-11-22//5b15e90a-a161-44ff-8e1c-9e2e09929803_749d8efdff062fb0.jpg",
> 			"defaultImg": 0
> 		}],
> 		"descar": ["黑色", "6GB"],
> 		"fullCount": 5,
> 		"discount": 0.98,
> 		"countStatus": 1,
> 		"fullPrice": 1000,
> 		"reducePrice": 10,
> 		"priceStatus": 0,
> 		"memberPrice": [{
> 			"id": 1,
> 			"name": "aaa",
> 			"price": 1998.99
> 		}]
> 		}, {
> 		"attr": [{
> 			"attrId": 9,
> 			"attrName": "颜色",
> 			"attrValue": "黑色"
> 		}, {
> 			"attrId": 10,
> 			"attrName": "内存",
> 			"attrValue": "12GB"
> 		}],
> 		"skuName": "Apple XR 黑色 12GB",
> 		"price": "2999",
> 		"skuTitle": "Apple XR 黑色 12GB",
> 		"skuSubtitle": "Apple XR 黑色 6GB",
> 		"images": [{
> 			"imgUrl": "",
> 			"defaultImg": 0
> 		}, {
> 			"imgUrl": "",
> 			"defaultImg": 0
> 		}],
> 		"descar": ["黑色", "12GB"],
> 		"fullCount": 0,
> 		"discount": 0,
> 		"countStatus": 0,
> 		"fullPrice": 0,
> 		"reducePrice": 0,
> 		"priceStatus": 0,
> 		"memberPrice": [{
> 			"id": 1,
> 			"name": "aaa",
> 			"price": 1998.99
> 		}]
> 	}, {
> 		"attr": [{
> 			"attrId": 9,
> 			"attrName": "颜色",
> 			"attrValue": "白色"
> 		}, {
> 			"attrId": 10,
> 			"attrName": "内存",
> 			"attrValue": "6GB"
> 		}],
> 		"skuName": "Apple XR 白色 6GB",
> 		"price": "1998",
> 		"skuTitle": "Apple XR 白色 6GB",
> 		"skuSubtitle": "Apple XR 黑色 6GB",
> 		"images": [{
> 			"imgUrl": "",
> 			"defaultImg": 0
> 		}, {
> 			"imgUrl": "",
> 			"defaultImg": 0
> 		}],
> 		"descar": ["白色", "6GB"],
> 		"fullCount": 0,
> 		"discount": 0,
> 		"countStatus": 0,
> 		"fullPrice": 0,
> 		"reducePrice": 0,
> 		"priceStatus": 0,
> 		"memberPrice": [{
> 			"id": 1,
> 			"name": "aaa",
> 			"price": 1998.99
> 		}]
> 	}, {
> 		"attr": [{
> 			"attrId": 9,
> 			"attrName": "颜色",
> 			"attrValue": "白色"
> 		}, {
> 			"attrId": 10,
> 			"attrName": "内存",
> 			"attrValue": "12GB"
> 		}],
> 		"skuName": "Apple XR 白色 12GB",
> 		"price": "2998",
> 		"skuTitle": "Apple XR 白色 12GB",
> 		"skuSubtitle": "Apple XR 黑色 6GB",
> 		"images": [{
> 			"imgUrl": "",
> 			"defaultImg": 0
> 		}, {
> 			"imgUrl": "",
> 			"defaultImg": 0
> 		}],
> 		"descar": ["白色", "12GB"],
> 		"fullCount": 0,
> 		"discount": 0,
> 		"countStatus": 0,
> 		"fullPrice": 0,
> 		"reducePrice": 0,
> 		"priceStatus": 0,
> 		"memberPrice": [{
> 			"id": 1,
> 			"name": "aaa",
> 			"price": 1998.99
> 		}]
> 	}]
> }
> ```

**1、保存基本信息断点调试通过**

由于函数是个事务，而数据库默认读出已经提交了的数据，所以用如下命令设置隔离级别，以方便查看数据库变化

```
SET SESSION TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
```

![](https://i-blog.csdnimg.cn/blog_migrate/7064d7dad1726c26d078cceae07f0469.png)

第一步保存基本信息成功。 

**2、`SpuInfoDesc`报错**

![](https://i-blog.csdnimg.cn/blog_migrate/a674c1fb61289303cf35b0a6f64b3969.png)

报错原因：表的id设计不是自增的，保存**`SpuInfoDesc`**时mybatisplus默认主键策略自增，这里要改变主键策略为input：

![](https://i-blog.csdnimg.cn/blog_migrate/9e9123bb008cef867fc5345cc1f9e8af.png)

![](https://i-blog.csdnimg.cn/blog_migrate/074e8dc36fd6942ea726b1c0997b63b4.png)

报错解决：mybatis默认主键为自增的，而`SpuInfoDescEntity`中的主键为自己输入的，所以修改主键注释

```java
	@TableId(type = IdType.INPUT)
	private Long spuId;
```

![image-20210927215631335](https://i-blog.csdnimg.cn/blog_migrate/01421185026d94198aaf2c9aa9ed7578.png)

**3、结果类R响应码类型报错**

抛出异常，修改`R`中的getCode方法

> 按我博客上面一节里设置R的getCode方法不会此步报错。 

![](https://i-blog.csdnimg.cn/blog_migrate/e0d7367015ef6883e6436e640ee4e99b.png)

```java
	public Integer getCode(){
		return (Integer) this.get("code");
	}
```

**4、保存空图片问题**

![](https://i-blog.csdnimg.cn/blog_migrate/fb803d5c2053165128863c4e4cb495f9.png)

![](https://i-blog.csdnimg.cn/blog_migrate/09d3e9f4e8fdebe069f13a3731a9d8fb.png)

出现问题，保存sku图片时，有些图片是没有路径的，没有路径的图片，无需保存。

在6.2图片map处理后、收集前进行filter过滤

```java
                List<SkuImagesEntity> skuImagesEntities = item.getImages().stream().map(img -> {
                    SkuImagesEntity skuImagesEntity = new SkuImagesEntity();
                    skuImagesEntity.setSkuId(skuId);
                    skuImagesEntity.setImgUrl(img.getImgUrl());
                    skuImagesEntity.setDefaultImg(img.getDefaultImg());
                    return skuImagesEntity;
                }).filter(entity -> {
                    //返回true是需要，返回false是过滤掉
                    return !StringUtils.isNullOrEmpty(entity.getImgUrl());
                }).collect(Collectors.toList());
                skuImagesService.saveBatch(skuImagesEntities);
```

```java
                //6.2、sku的图片信息`pms_sku_images`。skus列表里的每个item的图片列表赋值给pms_sku_images实体类列表
                Long skuId = skuInfoEntity.getSkuId();

                List<SkuImagesEntity> skuImagesEntities = item.getImages().stream().map(img -> {
                    SkuImagesEntity skuImagesEntity = new SkuImagesEntity();
                    skuImagesEntity.setSkuId(skuId);
                    skuImagesEntity.setImgUrl(img.getImgUrl());
                    skuImagesEntity.setDefaultImg(img.getDefaultImg());
                    return skuImagesEntity;
                }).filter(entity -> {
                    //返回true是需要，返回false是过滤掉
                    return !StringUtils.isNullOrEmpty(entity.getImgUrl());
                }).collect(Collectors.toList());
                skuImagesService.saveBatch(skuImagesEntities);
```

5、保存折扣信息的时候，满0元打0折这种都是无意义的，要过滤掉

![image-20210927222814462](https://i-blog.csdnimg.cn/blog_migrate/4529580e0c1b7c9c1311afb222704f65.png)

解决方法：在保存之前做判断，过滤掉小于等于0的无意义信息（不贴代码了），要注意的是判断BigDecimal进行判断时，要用compareTo函数。

例：

```java
                if (skuReductionTo.getFullCount() > 0 || skuReductionTo.getFullPrice().compareTo(new BigDecimal("0")) == 1){
                    R r1 = couponFeignService.saveSkuReduction(skuReductionTo);
                    if (r1.getCode() != 0){
                        log.error("远程保存优惠信息失败");
                    }
                }
```

6、保存满减时product模块远程调用报错500，coupon模块报错空指针异常 

![](https://i-blog.csdnimg.cn/blog_migrate/7a53f2217ad5d0f321ca8b99c8571f25.png)