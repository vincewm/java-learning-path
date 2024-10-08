> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?spm=1001.2014.3001.5501 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1.【内容模块】需求分析](#%E3%80%90%E5%86%85%E5%AE%B9%E6%A8%A1%E5%9D%97%E3%80%91%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90)

[2.【内容模块】模块工程的结构](#%E3%80%90%E5%86%85%E5%AE%B9%E6%A8%A1%E5%9D%97%E3%80%91%E6%A8%A1%E5%9D%97%E5%B7%A5%E7%A8%8B%E7%9A%84%E7%BB%93%E6%9E%84)

[3.【课程查询功能1】通用](#%E3%80%90%E8%AF%BE%E7%A8%8B%E6%9F%A5%E8%AF%A2%E5%8A%9F%E8%83%BD1%E3%80%91%E9%80%9A%E7%94%A8)

[3.1 分析数据模型](#%E5%88%86%E6%9E%90%E6%95%B0%E6%8D%AE%E6%A8%A1%E5%9E%8B)

[3.2 mybatis-plus代码生成器](#mybatis-plus%E4%BB%A3%E7%A0%81%E7%94%9F%E6%88%90%E5%99%A8)

[3.3 内容模块聚合api,model,service模块](#%E5%86%85%E5%AE%B9%E6%A8%A1%E5%9D%97%E8%81%9A%E5%90%88api%2Cmodel%2Cservice%E6%A8%A1%E5%9D%97)

[3.4 接口设计分析](#%E6%8E%A5%E5%8F%A3%E8%AE%BE%E8%AE%A1%E5%88%86%E6%9E%90)

[3.5 【基础模块】分页查询模型类](#%E3%80%90%E5%9F%BA%E7%A1%80%E6%A8%A1%E5%9D%97%E3%80%91%E5%88%86%E9%A1%B5%E6%9F%A5%E8%AF%A2%E6%A8%A1%E5%9E%8B%E7%B1%BB)

[3.6【基础模块】日期配置类](#%E3%80%90%E5%9F%BA%E7%A1%80%E6%A8%A1%E5%9D%97%E3%80%91%E6%97%A5%E6%9C%9F%E9%85%8D%E7%BD%AE%E7%B1%BB)

[3.7【内容模块】分页插件拦截器](#%E3%80%90%E5%86%85%E5%AE%B9%E6%A8%A1%E5%9D%97%E3%80%91%E5%88%86%E9%A1%B5%E6%8F%92%E4%BB%B6%E6%8B%A6%E6%88%AA%E5%99%A8)

[3.8【内容模块】查询条件模型类](#%E3%80%90%E5%86%85%E5%AE%B9%E6%A8%A1%E5%9D%97%E3%80%91%E6%9F%A5%E8%AF%A2%E6%9D%A1%E4%BB%B6%E6%A8%A1%E5%9E%8B%E7%B1%BB%C2%A0) 

[3.9【内容模块】响应模型类](#%E3%80%90%E5%86%85%E5%AE%B9%E6%A8%A1%E5%9D%97%E3%80%91%E5%93%8D%E5%BA%94%E6%A8%A1%E5%9E%8B%E7%B1%BB)

[4.swagger](#swagger)

[4.1 swagger生成接口文档步骤](#swagger%E7%94%9F%E6%88%90%E6%8E%A5%E5%8F%A3%E6%96%87%E6%A1%A3%E6%AD%A5%E9%AA%A4%C2%A0) 

[4.2 swagger常用注解](#swagger%E5%B8%B8%E7%94%A8%E6%B3%A8%E8%A7%A3)

[4.3 设置swagger信息，@Api和@ApiOperation](#%E8%AE%BE%E7%BD%AEswagger%E4%BF%A1%E6%81%AF%EF%BC%8C%40Api%E5%92%8C%40ApiOperation)

[4.4 优化分页模型类，用@ApiModelProperty描述字段](#%E4%BC%98%E5%8C%96%E5%88%86%E9%A1%B5%E6%A8%A1%E5%9E%8B%E7%B1%BB%EF%BC%8C%E7%94%A8%40ApiModelProperty%E6%8F%8F%E8%BF%B0%E5%AD%97%E6%AE%B5)

[4.5 使用Swagger进行接口测试](#%E4%BD%BF%E7%94%A8Swagger%E8%BF%9B%E8%A1%8C%E6%8E%A5%E5%8F%A3%E6%B5%8B%E8%AF%95)

[5.【课程查询功能2】具体](#%E3%80%90%E8%AF%BE%E7%A8%8B%E6%9F%A5%E8%AF%A2%E5%8A%9F%E8%83%BD2%E3%80%91%E5%85%B7%E4%BD%93)

[5.1【习惯】先写持久层，再写Service](#%E3%80%90%E4%B9%A0%E6%83%AF%E3%80%91%E5%85%88%E5%86%99%E6%8C%81%E4%B9%85%E5%B1%82%EF%BC%8C%E5%86%8D%E5%86%99Service)

[5.2【内容-接口模块】yml配置](#%E3%80%90%E5%86%85%E5%AE%B9-%E6%8E%A5%E5%8F%A3%E6%A8%A1%E5%9D%97%E3%80%91yml%E9%85%8D%E7%BD%AE)

[5.3 创建审核状态数据库字典](#%E5%88%9B%E5%BB%BA%E5%AE%A1%E6%A0%B8%E7%8A%B6%E6%80%81%E6%95%B0%E6%8D%AE%E5%BA%93%E5%AD%97%E5%85%B8)

[5.4【业务】条件查询课程列表](#%E3%80%90%E4%B8%9A%E5%8A%A1%E3%80%91%E6%9D%A1%E4%BB%B6%E6%9F%A5%E8%AF%A2%E8%AF%BE%E7%A8%8B%E5%88%97%E8%A1%A8)

[5.5【接口】查询课程列表](#%E3%80%90%E6%8E%A5%E5%8F%A3%E3%80%91%E6%9F%A5%E8%AF%A2%E8%AF%BE%E7%A8%8B%E5%88%97%E8%A1%A8)

[5.6 swagger测试](#swagger%E6%B5%8B%E8%AF%95)

[5.7【idea插件】Httpclient测试](#%E3%80%90idea%E6%8F%92%E4%BB%B6%E3%80%91Httpclient%E6%B5%8B%E8%AF%95)

[5.8 封装用来Httpclient测试的文件夹](#%E5%B0%81%E8%A3%85%E7%94%A8%E6%9D%A5Httpclient%E6%B5%8B%E8%AF%95%E7%9A%84%E6%96%87%E4%BB%B6%E5%A4%B9)

[5.9 使用idea启动前端项目](#%E4%BD%BF%E7%94%A8idea%E5%90%AF%E5%8A%A8%E5%89%8D%E7%AB%AF%E9%A1%B9%E7%9B%AE)

[5.10 创建系统模块](#%E5%88%9B%E5%BB%BA%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97)

[5.11 解决CORS跨域问题](#%E8%A7%A3%E5%86%B3CORS%E8%B7%A8%E5%9F%9F%E9%97%AE%E9%A2%98)

[5.11.1 方法一（使用）：系统模块-通过cors过滤器，添加跨域响应头](#%E6%96%B9%E6%B3%95%E4%B8%80%EF%BC%88%E4%BD%BF%E7%94%A8%EF%BC%89%EF%BC%9A%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97-%E9%80%9A%E8%BF%87cors%E8%BF%87%E6%BB%A4%E5%99%A8%EF%BC%8C%E6%B7%BB%E5%8A%A0%E8%B7%A8%E5%9F%9F%E5%93%8D%E5%BA%94%E5%A4%B4%C2%A0) 

[5.11.2 方法二：实现接口WebMvcConfigurer](#%E6%96%B9%E6%B3%95%E4%BA%8C%EF%BC%9A%E5%AE%9E%E7%8E%B0%E6%8E%A5%E5%8F%A3WebMvcConfigurer)

[5.11.3 方法三：JSONP](#%E6%96%B9%E6%B3%95%E4%B8%89%EF%BC%9AJSONP)

[5.11.4 方法四：使用nginx反向代理为同一域](#%E6%96%B9%E6%B3%95%E5%9B%9B%EF%BC%9A%E4%BD%BF%E7%94%A8nginx%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86%E4%B8%BA%E5%90%8C%E4%B8%80%E5%9F%9F)

[5.12前后端联调](#%E5%89%8D%E5%90%8E%E7%AB%AF%E8%81%94%E8%B0%83)

--

## 1.【内容模块】需求分析

**过程：**确认用户需求、 确认关键问题、梳理业务流程、数据建模、编写需求规格说明书。

**确认用户需求：**开发人员将用户抽象的需求转换为项目具体的功能、性能方面的要求。

**确认关键问题：**发布课程要发布哪些信息，发布了不良信息怎么办，用户怎么查看课程

**梳理业务流程：**首先分析核心业务流程，包括内容模块的课程发布、全项目的选课学习流程。

**数据建模：**根据关键信息建表。

**编写需求规格说明书：**针对每一个问题编写需求用例，例如添加课程功能的参与者、前置条件（机构仅允许向自己机构添加课程）、基本流程（展示课程页面、添加课程、录入哪些信息、提交）、数据描述、后置条件（插入记录）。

## 2.【内容模块】模块工程的结构

三个工程聚合在内容模块：接口工程（controller，为前端提供接口）、业务工程Service和dao，数据模型工程（实体类、数据传输对象dto）

## 3.【课程查询功能1】通用

### **3.1 分析**数据模型

分析数据模型，查哪个数据库、查哪些信息，查询条件。

![](https://i-blog.csdnimg.cn/blog_migrate/c98e56b09167296d211475e78cdc00d9.png)

![](https://i-blog.csdnimg.cn/blog_migrate/6ae4986804e597d330cea7ecdfc32803.png)

### 3.2 mybatis-plus代码生成器

使用mybatis-plus的generator工程，根据内容模块相关的数据库表生成PO类、Mapper接口、Mapper的xml文件。

地址在：[GitHub - baomidou/generator: Any Code generator](https://github.com/baomidou/generator "GitHub - baomidou/generator: Any Code generator")

修改数据库信息、生成路径，运行main方法：

```java
        //数据库账号
        private static final String DATA_SOURCE_USER_NAME  = "root";
        //数据库密码
        private static final String DATA_SOURCE_PASSWORD  = "mysql";
        //生成的表
        private static final String[] TABLE_NAMES = new String[]{
                "course_base",
                "course_market",
                "course_teacher",
                "course_category",
                "teachplan",
                "teachplan_media",
                "course_publish",
                "course_publish_pre"
        };
        // TODO 默认生成entity，需要生成DTO修改此变量
        // 一般情况下要先生成 DTO类 然后修改此参数再生成 PO 类。
        private static final Boolean IS_DTO = false;

        public static void main(String[] args) {
                ....
                //生成路径
                gc.setOutputDir(System.getProperty("user.dir") + "/xuecheng-plus-generator/src/main/java");
                
        ....
        // 数据库配置
                DataSourceConfig dsc = new DataSourceConfig();
                dsc.setDbType(DbType.MYSQL);
                dsc.setUrl("jdbc:mysql://192.168.101.65:3306/xcplus_" + SERVICE_NAME+"166"
                                + "?serverTimezone=UTC&useUnicode=true&useSSL=false&characterEncoding=utf8");
                ...
```

运行后会自动在内容模块下生成生成PO类、Mapper接口、Mapper的xml文件。

### 3.3 内容模块聚合api,model,service模块

api就是controller，model就是模型。

![](https://i-blog.csdnimg.cn/blog_migrate/928b3a2b78d9ab6ddae9bacf2fb75d35.png)

### 3.4 接口设计分析

分析请求方式、请求参数、请求类型（json）、响应类型、状态码

```bash
#请求类型
POST /content/course/list?pageNo=2&pageSize=1
Content-Type: application/json
#请求参数
{
  "auditStatus": "202002",
  "courseName": "",
  "publishStatus":""
}
#成功响应结果
{
  "items": [
    {
      "id": 26,
      "companyId": 1232141425,
      "companyName": null,
      "name": "spring cloud实战",
      "users": "所有人",
      "tags": null,
      "mt": "1-3",
      "mtName": null,
      "st": "1-3-2",
      "stName": null,
      "grade": "200003",
      "teachmode": "201001",
      "description": "本课程主要从四个章节进行讲解： 1.微服务架构入门 2.spring cloud 基础入门 3.实战Spring Boot 4.注册中心eureka。",
      "pic": "https://cdn.educba.com/academy/wp-content/uploads/2018/08/Spring-BOOT-Interview-questions.jpg",
      "createDate": "2019-09-04 09:56:19",
      "changeDate": "2021-12-26 22:10:38",
      "createPeople": null,
      "changePeople": null,
      "auditStatus": "202002",
      "auditMind": null,
      "auditNums": 0,
      "auditDate": null,
      "auditPeople": null,
      "status": 1,
      "coursePubId": null,
      "coursePubDate": null
    }
  ],
  "counts": 23,
  "page": 2,
  "pageSize": 1
}
```

### 3.5 【**基础**模块】分页查询**模型类**

![](https://i-blog.csdnimg.cn/blog_migrate/0bec2146fa7d96164c2f1a3d3fff2705.png)

在基础模块 

```java
package com.xuecheng.base.model;

import lombok.Data;
import lombok.ToString;
import lombok.extern.java.Log;

/**
 * @description 分页查询通用参数
 * @author Mr.M
 * @date 2022/9/6 14:02
 * @version 1.0
 */
@Data
@ToString
public class PageParams {

  //当前页码
  private Long pageNo = 1L;

  //每页记录数默认值
  private Long pageSize =10L;

  public PageParams(){

  }

  public PageParams(long pageNo,long pageSize){
      this.pageNo = pageNo;
      this.pageSize = pageSize;
  }



}
```

### 3.6【**基础**模块】日期配置类

在base工程com.xuecheng.base.config包下加配置LocalDateTimeConfig 类实现转json时字符串与LocalDateTime类型的转换。

```java
@Configuration
public class LocalDateTimeConfig {

    /*
     * 序列化内容
     *   LocalDateTime -> String
     * 服务端返回给客户端内容
     * */
    @Bean
    public LocalDateTimeSerializer localDateTimeSerializer() {
        return new LocalDateTimeSerializer(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));
    }

    /*
     * 反序列化内容
     *   String -> LocalDateTime
     * 客户端传入服务端数据
     * */
    @Bean
    public LocalDateTimeDeserializer localDateTimeDeserializer() {
        return new LocalDateTimeDeserializer(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));
    }
    //long转string避免精度损失
    @Bean
    public ObjectMapper jacksonObjectMapper(Jackson2ObjectMapperBuilder builder) {
        ObjectMapper objectMapper = builder.createXmlMapper(false).build();
        //忽略value为null 时 key的输出
        objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL);
        SimpleModule module = new SimpleModule();
        module.addSerializer(Long.class, ToStringSerializer.instance);
        module.addSerializer(Long.TYPE, ToStringSerializer.instance);
        objectMapper.registerModule(module);
        return objectMapper;
    }

    // 配置
    @Bean
    public Jackson2ObjectMapperBuilderCustomizer jackson2ObjectMapperBuilderCustomizer() {
        return builder -> {
            builder.serializerByType(LocalDateTime.class, localDateTimeSerializer());
            builder.deserializerByType(LocalDateTime.class, localDateTimeDeserializer());
        };
    }

}
```

### 3.7【内容模块】分页插件拦截器

```java
@Configuration
public class MybatisPlusConfig {
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        PaginationInnerInterceptor paginationInnerInterceptor = new PaginationInnerInterceptor();
//        溢出总页数后是否进行处理(默认不处理)
        paginationInnerInterceptor.setOverflow(true);
//        单页分页条数限制(默认无限制)
        paginationInnerInterceptor.setMaxLimit(1000L);

        interceptor.addInnerInterceptor(paginationInnerInterceptor);
        return interceptor;
    }
}
```

### 3.8【内容模块】查询条件模型类 

![](https://i-blog.csdnimg.cn/blog_migrate/a430ff12aaca3ef57e2161a23c35521c.png)

```java
package com.xuecheng.content.model.dto;

import lombok.Data;
import lombok.ToString;

/**
 * @description 课程查询参数Dto
 * @author Mr.M
 * @date 2022/9/6 14:36
 * @version 1.0
 */
 @Data
 @ToString
public class QueryCourseParamsDto {

  //审核状态
 private String auditStatus;
 //课程名称
 private String courseName;
  //发布状态
 private String publishStatus;

}
```

### 3.9【内容模块】响应模型类

```java
package com.xuecheng.base.model;

import lombok.Data;
import lombok.ToString;

import java.io.Serializable;
import java.util.List;

/**
 * @description 分页查询结果模型类
 * @author Mr.M
 * @date 2022/9/6 14:15
 * @version 1.0
 */
@Data
@ToString
public class PageResult<T> implements Serializable {

    // 数据列表
    private List<T> items;

    //总记录数
    private long counts;

    //当前页码
    private long page;

    //每页记录数
    private long pageSize;

    public PageResult(List<T> items, long counts, long page, long pageSize) {
        this.items = items;
        this.counts = counts;
        this.page = page;
        this.pageSize = pageSize;
    }



}
```

## 4.swagger

swagger：通过定义一种用来**描述API格式或API定义的语言**，来规范RESTful服务开发过程。

### 4.1 swagger生成接口文档**步骤** 

**1.导入依赖**

content.api包下 

```XML
<!-- Spring Boot 集成 swagger -->
<dependency>
    <groupId>com.spring4all</groupId>
    <artifactId>swagger-spring-boot-starter</artifactId>
</dependency>
```

**2.bootstrap.yml**配置swagger的扫描包路径及其它信息

```bash
server:
  servlet:
    context-path: /content    #应用的上下文路径，即项目路径，是构成请求url地址的一部分。
  port: 63041
swagger:
  title: "学成在线内容管理系统"
  description: "内容系统管理系统对课程相关信息进行管理"
  base-package: com.xuecheng.content
  enabled: true
  version: 1.0.0
```

**3.启动类**中添加@EnableSwagger2Doc注解

访问[http://localhost:63040/content/swagger-ui.html](http://localhost:63040/content/swagger-ui.html "http://localhost:63040/content/swagger-ui.html")查看接口信息

![](https://i-blog.csdnimg.cn/blog_migrate/45bcd8892a1916108515bd202ed2f4d1.png)

> 这个文档存在两个问题：
> 
> 1、接口名称显示course-base-info-controller名称不直观
> 
> 2、课程查询是post方式只显示post /course/list即可。

### 4.2 swagger常用注解

```java
 @Api：修饰整个类，描述Controller的作用
 @ApiOperation：描述一个类的一个方法，或者说一个接口
 @ApiParam：单个参数描述
 @ApiModel：用对象来接收参数
 @ApiModelProperty：用对象接收参数时，描述对象的一个字段
 @ApiResponse：HTTP响应其中1个描述
 @ApiResponses：HTTP响应整体描述
 @ApiIgnore：使用该注解忽略这个API
 @ApiError ：发生错误返回的信息
 @ApiImplicitParam：一个请求参数
 @ApiImplicitParams：多个请求参数
```

@ApiImplicitParam属性如下：

<table border="1" cellspacing="0"><tbody><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">属性</span></p></td><td style="border-color:#dee0e3;width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">取值</span></p></td><td style="border-color:#dee0e3;width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">作用</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">paramType</span></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">查询参数类型</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">path</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">以地址的形式提交数据</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">query</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">直接跟参数完成自动映射赋值</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">body</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">以流的形式提交</span> <span style="color:#000000;">仅支持</span><span style="color:#000000;">POST</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">header</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">参数在</span><span style="color:#000000;">request headers </span><span style="color:#000000;">里边提交</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">form</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">以</span><span style="color:#000000;">form</span><span style="color:#000000;">表单的形式提交</span> <span style="color:#000000;">仅支持</span><span style="color:#000000;">POST</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">dataType</span></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">参数的数据类型</span> <span style="color:#000000;">只作为标志说明，并没有实际验证</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">Long</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">String</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">name</span></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">接收参数名</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">value</span></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">接收参数的意义描述</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">required</span></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">参数是否必填</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">true</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">必填</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">false</span></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">非必填</span></p></td></tr><tr><td style="border-color:#dee0e3;width:87.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">defaultValue</span></p></td><td style="width:102.5pt;"><p style="margin-left:0;text-align:left;"></p></td><td style="width:234.85pt;"><p style="margin-left:0;text-align:left;"><span style="color:#000000;">默认值</span></p></td></tr></tbody></table>

### **4.3 设置swagger信息，@Api和@ApiOperation**

content.ap包下 

```java
 @Api(value = "课程信息编辑接口",tags = "课程信息编辑接口")
 @RestController
public class CourseBaseInfoController {

 @ApiOperation("课程查询接口")
 @PostMapping("/course/list")    //设置请求方式后，swagger页面就只显示post请求
  public PageResult<CourseBase> list(PageParams pageParams, @RequestBody(required=false) QueryCourseParamsDto queryCourseParams){

     //....

  }

}
```

再次启动服务，工程启动起来，访问[http://localhost:63040/content/swagger-ui.html](http://localhost:63040/content/swagger-ui.html "http://localhost:63040/content/swagger-ui.html")查看接口信息 

![](https://i-blog.csdnimg.cn/blog_migrate/c0e684b7e28117fae1ada058ae8bd69a.png)

点开请求：

![](https://i-blog.csdnimg.cn/blog_migrate/1ba055dc59314625ae4e2de7ef3c9d04.png)

### 4.4 优化分页模型类，用@ApiModelProperty描述字段

 @ApiModelProperty

```java
@ApiModelProperty：用对象接收参数时，描述对象的一个字段
```

```java
@Data
@ToString
public class PageParams {

    //当前页码
    @ApiModelProperty("页码")
    private Long pageNo = 1L;
    //每页显示记录数
    @ApiModelProperty("每页记录数")
    private Long pageSize = 30L;

    public PageParams() {
    }

    public PageParams(Long pageNo, Long pageSize) {
        this.pageNo = pageNo;
        this.pageSize = pageSize;
    }
}
```

再次访问swagger页面，可以看到描述信息已经出来了：

![](https://i-blog.csdnimg.cn/blog_migrate/36ac4cd429e6161a9cae51750fede33a.png)

### 4.5 使用Swagger进行接口测试

content.ap包下 CourseBaseInfoController 

```java
@ApiOperation("课程查询接口")
@PostMapping("/course/list")
public PageResult<CourseBase> list(PageParams pageParams, @RequestBody(required=false) QueryCourseParamsDto queryCourseParams){

    CourseBase courseBase = new CourseBase();
    courseBase.setName("测试名称");
    courseBase.setCreateDate(LocalDateTime.now());
    List<CourseBase> courseBases = new ArrayList();
    courseBases.add(courseBase);
    PageResult pageResult = new PageResult<CourseBase>(courseBases,10,1,10);
    return pageResult;

}
```

启动项目，打开swagger。

使用Swagger进行接口测试 ：

![](https://i-blog.csdnimg.cn/blog_migrate/509ce92857fff4c127d0d75568bf81c8.png)

设置请求参数

![](https://i-blog.csdnimg.cn/blog_migrate/067c26aa9d1bc68c6b8b79476d71e95a.png)

 swagger能看到响应的数据： 

![](https://i-blog.csdnimg.cn/blog_migrate/c923a09072d8e7c66821be19e719713a.png)

> 如果添加过日期格式配置类，序列化和反序列化时，时间格式就可以自定义。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3dace0cf6098718d470ec407aaf194f8.png)

## 5.【课程查询功能2】具体

### 5.1【习惯】先写持久层，再写Service

一个专业的程序员，要先写持久层，再写Service，提高代码复用性。

### 5.2【内容-接口模块】yml配置

> 仅接口模块需要写启动类和bootstrap.yml。 

```bash
server:
  servlet:
    context-path: /content
  port: 63040
#微服务配置
spring:
  application:
    name: content-api
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://192.168.101.65:3306/xc402_content?serverTimezone=UTC&userUnicode=true&useSSL=false&
    username: root
    password: mysql
# 日志文件配置路径
logging:
  config: classpath:log4j2-dev.xml

swagger:
  title: "学成在线内容管理系统"
  description: "内容系统管理系统对课程相关信息进行管理"
  base-package: com.xuecheng.content
  enabled: true
  version: 1.0.0
```

### 5.3 创建审核状态数据库字典

> **为什么要创建数据库字典？**
> 
> 降低耦合性，例如将课程的审核状态写成202001等数字，然后用数据库字典查询此数字代表的含义，这样以后想改审核状态的描述时候，就只需要从数据库字典改，不用sql语句逐条改课程表。

> 课程表的教学模式、审核状态、课程发布状态都将使用数据库字典：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/5d80054370eb7541e79b712b6d0bb95a.png)

课程审核状态的定义： 

```java
[
    {"code":"202001","desc":"审核未通过"},
    {"code":"202002","desc":"未审核"},
    {"code":"202003","desc":"审核通过"}
]
```

创建存放“数据库字典”的数据库：

![](https://i-blog.csdnimg.cn/blog_migrate/a1eb36dcab718eafe705d227722a1c45.png)

创建dictionary表：

 ![](https://i-blog.csdnimg.cn/blog_migrate/9e5b4a8b504b5ea28a100f5d09145351.png)

### 5.4【业务】条件查询课程列表

```java
package com.xuecheng.content.service.impl;

import ...

/**
 * @description 课程信息管理业务接口实现类
 * @author Mr.M
 * @date 2022/9/6 21:45
 * @version 1.0
 */
@Service
public class CourseBaseInfoServiceImpl  implements CourseBaseInfoService {


 @Autowired
 CourseBaseMapper courseBaseMapper;

 @Override
 public PageResult<CourseBase> queryCourseBaseList(PageParams pageParams, QueryCourseParamsDto queryCourseParamsDto) {


  //构建查询条件对象
  LambdaQueryWrapper<CourseBase> queryWrapper = new LambdaQueryWrapper<>();
  //构建查询条件，根据课程名称查询
     queryWrapper.like(StringUtils.isNotEmpty(queryCourseParamsDto.getCourseName()),CourseBase::getName,queryCourseParamsDto.getCourseName());
  //构建查询条件，根据课程审核状态查询
     queryWrapper.eq(StringUtils.isNotEmpty(queryCourseParamsDto.getAuditStatus()),CourseBase::getAuditStatus,queryCourseParamsDto.getAuditStatus());
//构建查询条件，根据课程发布状态查询
//todo:根据课程发布状态查询 

  //分页对象
  Page<CourseBase> page = new Page<>(pageParams.getPageNo(), pageParams.getPageSize());
  // 查询数据内容获得结果
  Page<CourseBase> pageResult = courseBaseMapper.selectPage(page, queryWrapper);
  // 获取数据列表
  List<CourseBase> list = pageResult.getRecords();
  // 获取数据总数
  long total = pageResult.getTotal();
  // 构建结果集
  PageResult<CourseBase> courseBasePageResult = new PageResult<>(list, total, pageParams.getPageNo(), pageParams.getPageSize());
  return courseBasePageResult;


 }


}
```

### 5.5【接口】查询课程列表

com.xuecheng.content.api.CourseBaseInfoController

```java
 @ApiOperation("课程查询接口")
@PostMapping("/course/list")
 public PageResult<CourseBase> list(PageParams pageParams, @RequestBody QueryCourseParamsDto queryCourseParams){
     PageResult<CourseBase> pageResult = courseBaseInfoService.queryCourseBaseList(pageParams, queryCourseParams);
    return pageResult;
 }
```

### 5.6 swagger测试

[http://localhost:63040/content/swagger-ui.html](http://localhost:63040/content/swagger-ui.html "http://localhost:63040/content/swagger-ui.html")

![](https://i-blog.csdnimg.cn/blog_migrate/bcd630a34fef67161236a61a05e16f47.png)

### **5.7【idea插件】Httpclient测试**

> swagger测试的缺点：刷新页面后请求数据就没了，**Httpclient就没有这个缺点。**
> 
> 2022版之后都是自带的。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bae30ec512619ae44b34bdca2b23f2e7.png)

**测试步骤：**

进入controller类，找到http接口对应的方法

![](https://i-blog.csdnimg.cn/blog_migrate/8f77f8231db451bf8386ec48a5358773.png)

点击Generate request in HTTP Client即可生成的一个测试用例。

![](https://i-blog.csdnimg.cn/blog_migrate/1a5a208f0ad6cc19a20bd74123fc93fd.png)

可以看到自己生成了一个.http结尾的文件

**添加请求参数进行测试、运行**

![](https://i-blog.csdnimg.cn/blog_migrate/fb240ad7acdbd5b77173a06415e8a76a.png)

观察控制台，测试通过。

![](https://i-blog.csdnimg.cn/blog_migrate/2630c2d968b161d925d48b1c0ed711bf.png)

### 5.8 封装用来**Httpclient**测试的文件夹

![](https://i-blog.csdnimg.cn/blog_migrate/750fa694cb6bfeeeab5deafc6d02b162.png)

xc-content-api.http

```bash
### 查询课程信息
POST {{content_host}}/content/course/list?pageNo=1&pageSize=2
Content-Type: application/json

{
  "auditStatus": "202004",
  "courseName": "java",
  "publishStatus":""
}

### 查询课程分类
GET {{content_host}}/content/course-category/tree-nodes

### 新增课程
POST {{content_host}}/content/course
Content-Type: application/json

{
  "charge": "201001",
  "price": 10,
  "originalPrice":100,
  "qq": "22333",
  "wechat": "223344",
  "phone": "13333333",
  "validDays": 365,
  "mt": "1-1",
  "st": "1-1-1",
  "name": "",
  "pic": "fdsf",
  "teachmode": "200002",
  "users": "初级人员",
  "tags": "tagstagstags",
  "grade": "204001",
  "description": "java网络编程高级java网络编程高级java网络编程高级"
}
```

http-client.env.json

```bash
{
  "dev": {
    "access额_token": "",
    "gateway_host": "localhost:63010",
    "content_host": "localhost:63040",
    "system_host": "localhost:63110",
    "media_host": "localhost:63050",
    "search_host": "localhost:63080",
    "auth_host": "localhost:63070",
    "checkcode_host": "localhost:63075",
    "learning_host": "localhost:63020"
  }
}
```

### **5.9 使用idea**启动前端项目

> **前后端联调：**
> 
> 通常由后端工程师将接口设计好并编写接口文档，将接口文档交给前端工程师，前后端的工程师就开始并行开发，前端开发人员会使用mock数据（假数据）进行开发，当前后端代码完成后开始进行接口联调，前端工程师将mock数据改为请求后端接口获取，前端代码请求后端服务测试接口是否正常，这个过程是前后端联调。 

**使用idea前后端联调：**

> **也可以用vscode运行前端项目**，这里介绍使用idea前后端联调。

1、安装nodejs

2、前端项目放到项目总目录下

![](https://i-blog.csdnimg.cn/blog_migrate/a5052e77170483acbf603ffccfd27990.png)

3、idea配置nodejs

![](https://i-blog.csdnimg.cn/blog_migrate/b83b05cd6e15b6b75b55a8b38aa4b022.png)

> vue-cli项目的package.json就相当于maven的pom，node-modules相当于maven的本地仓库。 

4、右键点击project-xczx2-portal-vue-ts目录下的package.json文件，

![](https://i-blog.csdnimg.cn/blog_migrate/563dd94d7e9a81401ff566c6a0548ae9.png)

5、点击Show npm Scripts打开npm窗口

![](https://i-blog.csdnimg.cn/blog_migrate/c54bbf02e17239ee2d240b6b99a5f71a.png)

6、点击“Edit 'serve'” setting，下边对启动项目的一些参数进行配置，选择nodejs、npm。

![](https://i-blog.csdnimg.cn/blog_migrate/27778babfee8b863f5c794e926579f14.png)

7、右键点击Serve，点击“Run serve”启动工程。

![](https://i-blog.csdnimg.cn/blog_migrate/b2104f23564eaf93b45a11381ab27b63.png)

出现如下访问链接说明启动成功

![](https://i-blog.csdnimg.cn/blog_migrate/e2346f78c70ed67c27f1dc093fd78c08.png)

8、访问http://localhost:8601即可访问前端工程。

![](https://i-blog.csdnimg.cn/blog_migrate/63e9410ce95249b1c47893c7f1e745c5.png)

> 如果存在问题尝试配置serve：
> 
> 1、cmd进入工程根目录
> 
> 2、运行以下命令
> 
> ```bash
> npm install -g cnpm --registry=https://registry.npm.taobao.org
> 
> cnpm i
> 
> npm run serve
> ```

### **5.10 创建系统模块**

> 前端工程报错如下：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/4d12b56816a6d8586d82ee23fd817074.png)
> 
> [http://localhost:8601/system/dictionary/all](http://localhost:8601/api/system/dictionary/all "http://localhost:8601/system/dictionary/all") 指向的是系统管理服务。此链接正是在前端请求后端获取数据字典数据的接口地址。**数据字典表**中配置了项目用的字典信息，**把它放到内存中以便使用**，此接口是查询字典中的全部数据

![](https://i-blog.csdnimg.cn/blog_migrate/6cf01125c3837b67695e1577065a11ff.png)

Service模块application.yml：

```bash
spring:
  application:
    name: system-service
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://192.168.101.65:3306/xc402_system?serverTimezone=UTC&userUnicode=true&useSSL=false&
    username: root
    password: mysql
# 日志文件配置路径
logging:
  config: classpath:log4j2-dev.xml


```

api模块bootstrap.yml

```bash
server:
  servlet:
    context-path: /system
  port: 63110
#微服务配置
spring:
  application:
    name: system-service

# 日志文件配置路径
logging:
  config: classpath:log4j2-dev.xml

# swagger 文档配置
swagger:
  title: "学成在线内容管理系统"
  description: "内容系统管理系统对课程相关信息进行业务管理数据"
  base-package: com.xuecheng.content
  enabled: true
  version: 1.0.0
```

启动系统管理服务，启动成功，在浏览器请求：[http://localhost:63110/system/dictionary/all](http://localhost:63110/system/dictionary/all "http://localhost:63110/system/dictionary/all")

此时请求状态码不再是500，而是跨域问题：

![](https://i-blog.csdnimg.cn/blog_migrate/a7955b0f88990cae76e66dff7b7ef91d.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/5e37af61219ac01c8777469d589b4e14.png)

### 5.11 解决CORS跨域问题

CORS全称是 cross origin resource share 表示跨域资源共享。

出这个提示的原因是基于浏览器的同源策略，去判断是否跨域请求，同源策略是浏览器的一种安全机制，从一个地址请求另一个地址，如果协议、主机、端口三者全部一致则不属于跨域，否则有一个不一致就是跨域请求。

![](https://i-blog.csdnimg.cn/blog_migrate/5e37af61219ac01c8777469d589b4e14.png)

#### 5.11.1 方法一（使用）：**系统模块-通过cors过滤器，**添加跨域响应头 

服务端在响应头添加 Access-Control-Allow-Origin：\*

**实现：** 

在**系统模块**的api工程config包下编写GlobalCorsConfig.java，

```java
//这个包别导错了，有一个很像的。
import org.springframework.web.cors.reactive.UrlBasedCorsConfigurationSource;
@Configuration
public class CorsConfiguration{
 
    @Bean
    public CorsWebFilter corsWebFilter(){
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
 
        CorsConfiguration corsConfiguration= new CorsConfiguration();
        //1、配置跨域
        // 允许跨域的请求头
        corsConfiguration.addAllowedHeader("*");
        // 允许跨域的请求方式
        corsConfiguration.addAllowedMethod("*");
        // 允许跨域的请求来源
        corsConfiguration.addAllowedOriginPattern("*");
//注释的这句会报错。因为当allowCredentials为真时，allowedorigin不能包含特殊值"*"，因为不能在"访问-控制-起源“响应头中设置该值。
        //corsConfiguration.addAllowedOrigin("*");//这句会报错，具体看下文
        // 是否允许携带cookie跨域
        corsConfiguration.setAllowCredentials(true);
 
        // 任意url都要进行跨域配置，两个*号就是可以匹配包含0到多个/的路径
        source.registerCorsConfiguration("/**",corsConfiguration);
        return new CorsWebFilter(source);
 
    }
}
```

>  **坑点：**
> 
> 报错：When allowCredentials is true, allowedOrigins cannot contain the special value "\*" since that cannot be set on the "Access-Control-Allow-Origin" response header. To allow credentials to a set of origins, list them explicitly or consider using "allowedOriginPatterns" instead.
> 
> 分析：当allowCredentials为真时，allowedorigin不能包含特殊值"\*"，因为不能在"访问-控制-起源“响应头中设置该值。
> 
> **解决：**
> 
> 移除这条语句：
> 
> ```java
> corsConfiguration.addAllowedOrigin("*");
> ```
> 
> 设置允许跨域的请求来源为具体的域名端口：
> 
> ```java
> corsConfiguration.addAllowedOrigin("http://localhost:8001");
> ```
> 
> 或者：
> 
> ```java
> corsConfiguration.addAllowedOriginPattern("*");
> ```
> 
> 备用：
> 
> ```java
> package com.xuecheng.system.config;
>  @Configuration
>  public class GlobalCorsConfig {
> 
>   /**
>    * 允许跨域调用的过滤器
>    */
>   @Bean
>   public CorsFilter corsFilter() {
>    CorsConfiguration config = new CorsConfiguration();
>    //允许白名单域名进行跨域调用
>    config.addAllowedOrigin("*");
>    //允许跨越发送cookie
>    config.setAllowCredentials(true);
>    //放行全部原始头信息
>    config.addAllowedHeader("*");
>    //允许所有请求方法跨域调用
>    config.addAllowedMethod("*");
>    UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
>    source.registerCorsConfiguration("/**", config);
>    return new CorsFilter(source);
>   }
>  }
> ```

#### 5.11.2 方法二：实现接口WebMvcConfigurer

```java
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOriginPatterns("*")
                .allowedMethods("GET", "HEAD", "POST", "PUT", "DELETE", "OPTIONS")
                .allowCredentials(true)
                .maxAge(3600)
                .allowedHeaders("*");
    }
}
```

#### 5.11.3 方法三：JSONP

通过script标签的src属性进行跨域请求，如果服务端要响应内容则首先读取请求参数callback的值，callback是一个回调函数的名称，服务端读取callback的值后将响应内容通过调用callback函数的方式告诉请求方。如下图：

![](https://i-blog.csdnimg.cn/blog_migrate/836de32e61be72f42d73e5ddb6a50b56.png)

#### 5.11.4 方法四：使用nginx反向代理为同一域

使用Nginx反向代理，不同地址、端口都被同一个域名反向代理了，这就是统一域了。**这种方法在开发时没法用，所以不采用。** 

由于服务端之间没有跨域，浏览器通过nginx去访问跨域地址。

![](https://i-blog.csdnimg.cn/blog_migrate/0f0e36f765b3b1e6bee9702017901629.png)

1）浏览器先访问[http://192.168.101.10:8601](http://192.168.101.10:8601 "http://192.168.101.10:8601") nginx提供的地址，进入页面

2）此页面要跨域访问[http://192.168.101.11:8601](http://192.168.101.11:8601 "http://192.168.101.11:8601") ，不能直接跨域访问[http://www.baidu.com:8601](http://www.baidu.com:8601 "http://www.baidu.com:8601")  ，而是访问nginx的一个同源地址，比如：[http://192.168.101.11:8601/api](http://192.168.101.11:8601/api "http://192.168.101.11:8601/api") ，通过[http://192.168.101.11:8601/api](http://192.168.101.11:8601/api "http://192.168.101.11:8601/api") 的代理去访问[http://www.baidu.com:8601](http://www.baidu.com:8601 "http://www.baidu.com:8601")。

这样就实现了跨域访问。

浏览器到[http://192.168.101.11:8601/api](http://192.168.101.11:8601/api "http://192.168.101.11:8601/api") 没有跨域

nginx到[http://www.baidu.com:8601](http://www.baidu.com:8601 "http://www.baidu.com:8601")通过服务端通信，没有跨域。

### **5.12前后端联调**

体会前后端联调的流程，测试的功能为课程查询功能。

**1、修改前端配置文件**

前端默认连接的是项目的网关地址，由于现在网关工程还没有创建，这里需要更改前端工程的参数配置文件 ，修改网关地址为内容管理服务的地址。

![](https://i-blog.csdnimg.cn/blog_migrate/578601a212866e6026804e5c713d9a81.png)

> 网关端口63010，配置网关后就改成显示第一行，注释第三行。

**2、启动前端工程，再启内容管理服务端。**

进入课程管理：[http://localhost:8601/#/organization/course-list](http://localhost:8601/#/organization/course-list "http://localhost:8601/#/organization/course-list")

**3、正常显示**

![](https://i-blog.csdnimg.cn/blog_migrate/198562429025df2651f8f5c8aa68b3fa.png)

> 如果页面没正常显示，复制并格式化响应数据，进行分析。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/5c7e4d349e719e8edceae31aa32baf28.png)