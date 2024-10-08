> **导航：**
> 
> [谷粒商城笔记+踩坑汇总篇](https://blog.csdn.net/qq_40991313/article/details/127099139?spm=1001.2014.3001.5501 "谷粒商城笔记+踩坑汇总篇")
> 
>  **Java笔记汇总：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客")

**目录**

[4、分布式组件](#%E5%9B%9B%E3%80%81%E5%88%86%E5%B8%83%E5%BC%8F%E7%BB%84%E4%BB%B6)

[4.0. 简介](#4.0.%20%E7%AE%80%E4%BB%8B)

[4.0.1、SpringCloud 对比SpringCloud Alibaba](#4.0.1%E3%80%81SpringCloud%20%E5%AF%B9%E6%AF%94SpringCloud%20Alibaba)

[4.0.2、项目技术搭配方案选择](#4.0.2%E3%80%81%E9%A1%B9%E7%9B%AE%E6%8A%80%E6%9C%AF%E6%90%AD%E9%85%8D%E6%96%B9%E6%A1%88)

[4.0.3、common模块引入SpringCloud Alibaba依赖管理](#4.0.3%E3%80%81common%E6%A8%A1%E5%9D%97%E5%BC%95%E5%85%A5SpringCloud%20Alibaba%E4%BE%9D%E8%B5%96%E7%AE%A1%E7%90%86)

[4.1 nacos下载、启动、配置](#1.%20nacos%E7%94%A8%E4%BD%9C%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E4%B8%AD%E5%BF%83)

[4.1.1、nacos下载安装](#4.1.1%E3%80%81nacos%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85)

[4.1.2、配置nacos注册中心](#4.1%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B.2%E3%80%81%E9%85%8D%E7%BD%AEnacos)

[4.1.3、启动gulimall-xxx, 查看服务注册中心](#4.1%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B%E2%80%8B.3%E3%80%81%E5%90%AF%E5%8A%A8gulimall-xxx%2C%20%E6%9F%A5%E7%9C%8B%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E4%B8%AD%E5%BF%83)

[4.2. openfegin远程调用，案例演示](#2.%20openfegin%E8%BF%9C%E7%A8%8B%E8%B0%83%E7%94%A8)

[4.2.0、需求，member调用coupon](#4.2.0%E3%80%81%E9%9C%80%E6%B1%82%EF%BC%8Cmember%E8%B0%83%E7%94%A8coupon)

[4.2.1、common模块引入openfegin依赖](#4.2.1%E3%80%81common%E6%A8%A1%E5%9D%97%E5%BC%95%E5%85%A5openfegin%E4%BE%9D%E8%B5%96)

[4.2.2、 coupon的controller编写测试方法](#4.2.2%E3%80%81%20coupon%E7%9A%84controller%E7%BC%96%E5%86%99%E6%B5%8B%E8%AF%95%E6%96%B9%E6%B3%95)

[4.2.3、member的引导类注解@EnableFeignClients](#4.2.3%E3%80%81member%E7%9A%84%E5%BC%95%E5%AF%BC%E7%B1%BB%E6%B3%A8%E8%A7%A3%40EnableDiscoveryClient)

[4.2.4、member模块编写coupon的客户端](#4.2.4%E3%80%81member%E6%A8%A1%E5%9D%97%E7%BC%96%E5%86%99coupon%E7%9A%84%E5%AE%A2%E6%88%B7%E7%AB%AF)

[4.2.5、member模块注入coupon的客户端](#4.2.5%E3%80%81member%E6%A8%A1%E5%9D%97%E6%B3%A8%E5%85%A5coupon%E7%9A%84%E5%AE%A2%E6%88%B7%E7%AB%AF%C2%A0) 

[4.3. nacos用作配置中心](#3.%20nacos%E7%94%A8%E4%BD%9C%E9%85%8D%E7%BD%AE%E4%B8%AD%E5%BF%83)

[4.3.1、依赖 nacos-config,bootstrap](#4.3.1%E3%80%81common%E4%B8%AD%E6%B7%BB%E5%8A%A0%E4%BE%9D%E8%B5%96%20nacos-config)

[4.3.2、coupons模块创建bootstrap.yml](#4.3.2%E3%80%81coupons%E6%A8%A1%E5%9D%97%E5%88%9B%E5%BB%BAbootstrap.yml)

[4.3.3、nacos服务端添加配置文件](#4.3.3%E3%80%81nacos%E6%9C%8D%E5%8A%A1%E7%AB%AF%E6%B7%BB%E5%8A%A0%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)

[4.3.4、coupon的controller中编写测试代码](#4.3.4%E3%80%81coupon%E7%9A%84controller%E4%B8%AD%E7%BC%96%E5%86%99%E6%B5%8B%E8%AF%95%E4%BB%A3%E7%A0%81)

[4.3.5、启动测试](#4.3.5%E3%80%81%E5%90%AF%E5%8A%A8%E6%B5%8B%E8%AF%95)

[4.3.6、配置热更新，controller注解@RefreshScope动态刷新](#4.3.6%E3%80%81%E9%85%8D%E7%BD%AE%E7%83%AD%E6%9B%B4%E6%96%B0%EF%BC%8Ccontroller%E6%B3%A8%E8%A7%A3%40RefreshScope%E5%8A%A8%E6%80%81%E5%88%B7%E6%96%B0)

[4.3.7、命名空间](#4.3.7%E3%80%81%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)

[4.3.8、根据服务创建命名空间，各命名空间根据环境分组](#4.3.8%E3%80%81%E7%BB%88%E6%9E%81%E7%89%88%EF%BC%8C%E6%A0%B9%E6%8D%AE%E6%9C%8D%E5%8A%A1%E5%88%9B%E5%BB%BA%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4%EF%BC%8C%E5%90%84%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4%E6%A0%B9%E6%8D%AE%E7%8E%AF%E5%A2%83%E5%88%86%E7%BB%84)

[4.3.9、按类型抽取配置，加载多配置集](#4.3.9%E3%80%81%E6%8C%89%E7%B1%BB%E5%9E%8B%E6%8A%BD%E5%8F%96%E9%85%8D%E7%BD%AE%EF%BC%8C%E5%8A%A0%E8%BD%BD%E5%A4%9A%E9%85%8D%E7%BD%AE%E9%9B%86%C2%A0) 

[4.4. 网关gateway](#4.%20%E7%BD%91%E5%85%B3gateway-88)

[4.4.0、简介](#4.4.0%E3%80%81%E7%AE%80%E4%BB%8B%C2%A0) 

[4.4.1、gulimall父工程下新建gulimall-gateway模块作为网关](#4.4.1%E3%80%81gulimall%E7%88%B6%E5%B7%A5%E7%A8%8B%E4%B8%8B%E6%96%B0%E5%BB%BAgulimall-gateway%E4%BD%9C%E4%B8%BA%E7%BD%91%E5%85%B3)

[4.4.2、演示，网关路由到百度](#4.4.2%E3%80%81%E6%BC%94%E7%A4%BA%EF%BC%8C%E7%BD%91%E5%85%B3%E8%B7%AF%E7%94%B1%E5%88%B0%E7%99%BE%E5%BA%A6)

[5、前端基础（回顾，与项目无关）](#%E4%BA%94%E3%80%81%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80)

[5.1. ES6基础](#1.%20ES6%E5%9F%BA%E7%A1%80)

[5.1.1、let & const](#1%E3%80%81let%20%26%20const)

[5.1.2、解构表达式](#2%E3%80%81%E8%A7%A3%E6%9E%84%E8%A1%A8%E8%BE%BE%E5%BC%8F)

[5.1.3、函数优化](#3%E3%80%81%E5%87%BD%E6%95%B0%E4%BC%98%E5%8C%96)

[5.1.4、对象优化](#4%E3%80%81%E5%AF%B9%E8%B1%A1%E4%BC%98%E5%8C%96)

[5.1.5、map和reduce](#5%E3%80%81map%E5%92%8Creduce)

[5.1.6、promise](#6%E3%80%81promise)

[5.1.7、模块化](#7%E3%80%81%E6%A8%A1%E5%9D%97%E5%8C%96)

[5.2. VUE基础](#2.%20VUE%E5%9F%BA%E7%A1%80)

[5.2.1、VUE安装](#1%E3%80%81VUE%E5%AE%89%E8%A3%85)

[5.2.2、v-model, v-on](#2%E3%80%81v-model%2C%20v-on)

[5.2.3、v-text、v-html、v-ref](#3%E3%80%81v-text%E3%80%81v-html%E3%80%81v-ref)

[5.2.4、单向绑定v-bind:](#4%E3%80%81%E5%8D%95%E5%90%91%E7%BB%91%E5%AE%9Av-bind%3A)

[5.2.5、双向绑定v-model](#5%E3%80%81%E5%8F%8C%E5%90%91%E7%BB%91%E5%AE%9Av-model)

[5.2.6、v-on事件](#6%E3%80%81v-on%E4%BA%8B%E4%BB%B6)

[5.2.7、v-for遍历](#7%E3%80%81v-for%E9%81%8D%E5%8E%86)

[5.2.8、v-if和v-show](#8%E3%80%81v-if%E5%92%8Cv-show)

[5.2.9、v-else和v-else-if](#9%E3%80%81v-else%E5%92%8Cv-else-if)

[5.2.10、计算属性和监听器](#10%E3%80%81%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7%E5%92%8C%E7%9B%91%E5%90%AC%E5%99%A8)

[5.2.11、过滤器filter](#11%E3%80%81%E8%BF%87%E6%BB%A4%E5%99%A8filter)

[5.2.12、组件化](#12%E3%80%81%E7%BB%84%E4%BB%B6%E5%8C%96)

[5.2.13、生命周期和钩子函数](#13%E3%80%81%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%92%8C%E9%92%A9%E5%AD%90%E5%87%BD%E6%95%B0)

[5.3. vue脚手架进行模块化开发](#3.%20vue-dome)

[5.3.1、全局安装webpack](#1%E3%80%81%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85webpack)

[5.3.2、全局安装vue脚手架](#2%E3%80%81%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85vue%E8%84%9A%E6%89%8B%E6%9E%B6)

[5.3.3、初始化vue项目](#3%E3%80%81%E5%88%9D%E5%A7%8B%E5%8C%96vue%E9%A1%B9%E7%9B%AE)

[5.3.4、vue项目目录结构](#4%E3%80%81vue%E9%A1%B9%E7%9B%AE%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)

[5.3.5、分析主页展示逻辑](#5.3.5%E3%80%81%E4%BF%AE%E6%94%B9vue%E9%A1%B9%E7%9B%AE)

[5.3.6、新建Hello组件，负责/hello路径](#5.3.6%E3%80%81%E6%96%B0%E5%BB%BAHello%E7%BB%84%E4%BB%B6%EF%BC%8C%E8%B4%9F%E8%B4%A3%2Fhello%E8%B7%AF%E5%BE%84)

[5.3.7、快速生成组件模板](#5.3.6%E3%80%81%E5%BF%AB%E9%80%9F%E7%94%9F%E6%88%90%E7%BB%84%E4%BB%B6%E6%A8%A1%E6%9D%BF)

[5.4. ElementUI](#5.4.%20ElementUI)

--

## 4、分布式组件

> 本节主要用于回顾，主要就**4.4.1网关模块时真实操作一下**就行，其他都是测试。

### 4.0. 简介

#### 4.0.1、**SpringCloud 对比SpringCloud Alibaba**

**springcloud对比SpringCloud Alibaba：** 

![](https://i-blog.csdnimg.cn/blog_migrate/3049aa7135cd57fbae86b65f6c7fdfbb.png)

**企业需求：**

![](https://i-blog.csdnimg.cn/blog_migrate/02d52dd2bcdb4cf9515523efbd319a51.png)

#### 4.0.2、项目技术搭配方案选择

![](https://i-blog.csdnimg.cn/blog_migrate/5e464ee74a0bb25ab3798e1a9900bea8.png)

![](https://i-blog.csdnimg.cn/blog_migrate/6a1fe7994d464988eb55eb55038c2e25.png)

#### 4.0.3、common模块引入**SpringCloud Alibaba**依赖管理

[spring-cloud-alibaba/README-zh.md at 2021.x · alibaba/spring-cloud-alibaba · GitHub](https://github.com/alibaba/spring-cloud-alibaba/blob/2021.x/README-zh.md "spring-cloud-alibaba/README-zh.md at 2021.x · alibaba/spring-cloud-alibaba · GitHub")

guimall-common模块的pom： 

```XML
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>2.1.0.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

### 4.1 nacos下载、启动、配置

#### 4.1.**1、nacos下载安装**

-   下载地址：https://github.com/alibaba/nacos/releases

![image-20210925231418023](https://i-blog.csdnimg.cn/blog_migrate/b1c719d06b49174904adc310bbf52520.png)​

**启动：** 

-   解压后启动nacos：

 在bin目录下cmd：

```XML
startup.cmd -m standalone
```

-   命令运行成功后直接访问http://localhost:8848/nacos，默认账号密码都是nacos

[http://localhost:8848/nacos/index.html](http://localhost:8848/nacos/index.html "http://localhost:8848/nacos/index.html")

![image-20210925231458882](https://i-blog.csdnimg.cn/blog_migrate/96fe2b8589b64385b81fc980979f571f.png)​

#### 4.1.**2、配置nacos注册中心**

-    **common引入依赖**
    
    ```XML
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
            </dependency>
    ```
    

-   在**所有子模块gulimall-xxx里yml**里写**`spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848`**（指定nacos的地址）。再指定**spring.applicatin.name**告诉注册到nacos中以什么命名
    
    ```bash
    spring:
      application:
    #注意修改服务名
        name: gulimall-coupon
      cloud:
        nacos:
          discovery:
            server-addr: 127.0.0.1:8848
    ```
    
-   在**所有子模块gulimall-xxx引导类**上使用 **`@EnableDiscoveryClient` 注解开启Feign**服务注册与发现功能
    
-   ```java
    @EnableDiscoveryClient
    @SpringBootApplication
    public class GulimallCouponApplication {
        public static void main(String[] args) {
            SpringApplication.run(GulimallCouponApplication.class, args);
        }
    }
    ```
    

#### 4.1.**3、启动gulimall-xxx, 查看服务注册中心**

![](https://i-blog.csdnimg.cn/blog_migrate/3b089ab8fbac9c74fa1ac467cf5ae1ce.png)​

### 4.2. openfegin远程调用，案例演示

声明式远程调用

feign是一个声明式的HTTP客户端，他的目的就是让远程调用更加简单。给远程服务发的是HTTP请求。

会员服务想要远程调用优惠券服务，只需要给会员服务里引入openfeign依赖，他就有了远程调用其他服务的能力。

#### 4.2.0**、需求，member调用coupon**

会员模块通过feign远程调用优惠券模块controller的方法。

#### 4.2.**1、common模块引入**openfegin**依赖**

```XML
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

#### 4.2.**2、 coupon的controller编写测试方法**

 在gulimall-coupon中的**CouponController**中添加**测试方法**

```java
    @RequestMapping("/member/list")
    public R membercoupons(){    //全系统的所有返回都返回R
        // 假数据，模拟去数据库查用户对于的优惠券
        CouponEntity couponEntity = new CouponEntity();
        couponEntity.setCouponName("满100-10");//优惠券的名字
        return R.ok().put("coupons",Arrays.asList(couponEntity));
    }
```

> R 结果类：
> 
> ```java
> public class R extends HashMap<String, Object> {
> 	private static final long serialVersionUID = 1L;
> 	
> 	public R() {
> 		put("code", 0);
> 		put("msg", "success");
> 	}
> 	
> 	public static R error() {
> 		return error(HttpStatus.SC_INTERNAL_SERVER_ERROR, "未知异常，请联系管理员");
> 	}
> 	
> 	public static R error(String msg) {
> 		return error(HttpStatus.SC_INTERNAL_SERVER_ERROR, msg);
> 	}
> 	
> 	public static R error(int code, String msg) {
> 		R r = new R();
> 		r.put("code", code);
> 		r.put("msg", msg);
> 		return r;
> 	}
> 
> 	public static R ok(String msg) {
> 		R r = new R();
> 		r.put("msg", msg);
> 		return r;
> 	}
> 	
> 	public static R ok(Map<String, Object> map) {
> 		R r = new R();
> 		r.putAll(map);
> 		return r;
> 	}
> 	
> 	public static R ok() {
> 		return new R();
> 	}
> 
> 	public R put(String key, Object value) {
> 		super.put(key, value);
> 		return this;
> 	}
> }
> ```

#### 4.2.3、member的引导类注解`**@EnableFeignClients**`

在**member的主启动类**上加注解@EnableFeignClients**启用`feign`客户端**

```java
@EnableDiscoveryClient
@SpringBootApplication
@EnableFeignClients(basePackages="com.vince.gulimall.member.feign")//扫描接口方法注解
public class GulimallMemberApplication {
    public static void main(String[] args) {
        SpringApplication.run(GulimallMemberApplication.class, args);
    }
}
```

>  @EnableDiscoveryClient是服务的注册发现。

#### 4.2.4、member模块编写coupon的客户端

在`com.xmh.gulimall.member.**feign**`中**新建接口`CouponFeignService（或CouponClient）`**

```java
@FeignClient("gulimall-coupon")//告诉spring cloud这个接口是一个远程客户端，要调用coupon服务(nacos中找到)
public interface CouponFeignService{

    // 远程服务的url
    @RequestMapping("/coupon/coupon/member/list")//注意写全优惠券类上还有映射
    public R membercoupons();//得到一个R对象


}
```

#### 4.2.5、member模块注入coupon的客户端 

在member的**MemberController**写一个**测试**

```java
    @Autowired
    private CouponFeignService couponFeignService; //注入刚才的CouponFeignService接口

    @RequestMapping("/coupons")
    public R coupons(){
        MemberEntity memberEntity = new MemberEntity();
        memberEntity.setNickname("会员昵称张三");
        R membercoupons = couponFeignService.membercoupons();

        return R.ok().put("member", memberEntity).put("coupons", membercoupons.get("coupons"));
    }
```

启动gulimall-me mber，gulimall-coupon项目。**访问http://localhost:8000/member/member/coupons**测试

![image-20210925232220401](https://i-blog.csdnimg.cn/blog_migrate/f4aa445281c9c8dbf1ab7788d50728b0.png)​

测试成功！

### 4.3. nacos用作配置中心

**Nacos**一方面可以**将配置集中管理**，另一方面可以在**配置变更时**，及时**通知微服务**，实现**配置的热更新。** 

#### 4.3.**1、依赖 nacos-config,bootstrap**

**common中添加依赖**

```XML
<dependency>
     <groupId>com.alibaba.cloud</groupId>
     <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
 </dependency>
<!--        在SpringBoot 2.4.x的版本之后，对于bootstrap.properties/bootstrap.yaml配置文件(我们合起来成为Bootstrap配置文件)的支持，需要导入如下的依赖-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-bootstrap</artifactId>
            <version>3.1.4</version>
        </dependency>
```

#### 4.3.**2、coupons模块创建bootstrap.yml**

**在coupons模块中创建/src/main/resources/bootstrap.yml，优先级别application.properties高**

> **问题：nacos配置要先于yml，但如果尚未读取yml，又如何得知nacos地址并获取nacos配置呢？**
> 
> **答案：**因此spring引入了一种新的配置文件：**bootstrap.yaml**文件，优先级高于application.yml，会在application.yml之前被读取。

```bash
# 改名字，对应nacos里的配置文件名
spring:
  application:
    name: gulimall-coupon
  cloud:
    nacos:
      config:
        server-addr: 127.0.0.1:8848
        file-extension: yaml # 指定配置文件为yaml格式
```

#### 4.3.**3、nacos服务端**添加配置文件

**浏览器去nacos里的配置列表，点击＋号，data ID：`gulimall-coupon.yaml`，配置**

![](https://i-blog.csdnimg.cn/blog_migrate/dd1fa046c3d855e0118c90debb44913a.png)​ 

![image-20210925232732790](https://i-blog.csdnimg.cn/blog_migrate/ed8d9469386c49fbcbce199e5cb87905.png)​

> ![](https://i-blog.csdnimg.cn/blog_migrate/d95f8837beaf10f5ab1f4e21313f6a12.png)​ 
> 
> 这里分组名称默认DEFAULT\_GROUP，我们看服务列表也可以看到所有服务默认都在这个分组：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/292425d7a7552f0336441593528a10af.png)​

#### 4.3.**4、coupon的controller中编写测试代码**

```java
    @Value("${coupon.user.name}")
    private String name;
    
    @Value("${coupon.user.age}")
    private int age;

    @RequestMapping("/nacos")
    public R nacos(){
        return R.ok().put("name", name).put("age", age);
    }
```

#### 4.3.**5、启动测试**

**访问http://localhost:7000/coupon/coupon/nacos测试**

![image-20210925233031028](https://i-blog.csdnimg.cn/blog_migrate/db158cf03f2d516982bf2dc80da7d8df.png)​

#### 4.3.**6、配置热更新，controller注解`@RefreshScope`动态刷新**

![image-20210925233121327](https://i-blog.csdnimg.cn/blog_migrate/93352fb3e912782335bc2c6dd5f6e405.png)​

#### 4.3.7、命名空间

![](https://i-blog.csdnimg.cn/blog_migrate/946f545ed617748bb48ae0d5bd60842f.png)​ 

命名空间用于将开发测试生产三种**环境**、**或者**各**微服务**之间**配置隔离**。默认命名空间是public：

![](https://i-blog.csdnimg.cn/blog_migrate/26505760f6595218480a3c617417a5aa.png)​

**不同命名空间设置不同配置：** 

![](https://i-blog.csdnimg.cn/blog_migrate/9a3273384757105e1f1af22fb6d36de0.png)​ 

**指定命名空间：** 

 ![](https://i-blog.csdnimg.cn/blog_migrate/415ec3db090e74248917f8c01bfcf6e9.png)​

#### 4.3.8、根据服务创建命名空间，各命名空间根据环境分组

![](https://i-blog.csdnimg.cn/blog_migrate/46d8e2b512608616a6e0e228cda849f6.png)​

![](https://i-blog.csdnimg.cn/blog_migrate/0ebf82d6252871872717c0380334db9e.png)​

![](https://i-blog.csdnimg.cn/blog_migrate/976b80da68f292cb83accd4315684392.png)​ 

#### 4.3.9、按类型抽取配置，加载多配置集 

![](https://i-blog.csdnimg.cn/blog_migrate/d2db5b401eea56fce29cf1323ea93394.png)​ 

> 开发时为了方便可以将配置文件写在项目中，等发布后再抽取到nacos中。 

**将datasource相关配置抽取成一个配置**，在coupon命名空间下，分组名为dev（根据环境分组） ：

![](https://i-blog.csdnimg.cn/blog_migrate/e25274fb7839250faaaa9a59adf3e06e.png)​

**使用：**

![](https://i-blog.csdnimg.cn/blog_migrate/5237085b70e77e5a53cf05a918f52ece.png)​ 

**或者bootstrap.yml** 

```bash
spring:
  application:
    name: gulimall-coupon
  cloud:
    nacos:
      config:
        server-addr: 127.0.0.1:8848
        file-extension: yaml
        namespace: xxxx
        extension-configs:
          - data-id: datasource.yml
            group: dev
            refresh: true
```

### 4.4. 网关gateway

#### 4.4.0、简介 

网关的**核心功能特性**：

-   **请求路由**
-   **权限控制**
-   **限流**

动态上下线：发送请求需要知道商品服务的地址，如果商品服务器有123服务器，1号掉线后，还得改，所以需要网关动态地管理，他能从注册中心中实时地感知某个服务上线还是下线。【先通过网关，网关路由到服务提供者】

拦截：请求也要加上询问权限，看用户有没有权限访问这个请求，也需要网关。

所以我们使用spring cloud的gateway组件做网关功能。

网关是请求流量的入口，常用功能包括**路由转发，权限校验，限流控制**等。

https://spring.io/projects/spring-cloud-gateway

参考手册：https://cloud.spring.io/spring-cloud-gateway/2.2.x/reference/html/

**三大核心概念：**

-   **Route路由:** The basic building block of the gateway. It is defined by an ID, a destination URI, a collection of predicates断言, and a collection of filters. A route is matched if the aggregate predicate is true.**发一个请求给网关，网关要将请求路由到指定的服务。路由有id，目的地uri，断言的集合，匹配了断言就能到达指定位置，**
-   **Predicate断言:** This is a Java 8 Function Predicate. The input type is a Spring Framework ServerWebExchange. This lets you match on anything from the HTTP request, such as headers or parameters.**就是java里的断言函数，匹配请求里的任何信息，包括请求头等。根据请求头路由哪个服务**
-   **Filter过滤:** These are instances of Spring Framework GatewayFilter that have been constructed with a specific factory. Here, you can modify requests and responses before or after sending the downstream request.**过滤器请求和响应都可以被修改。  
    客户端发请求给服务端。中间有网关。先交给映射器，如果能处理就交给handler处理，然后交给一系列filer，然后给指定的服务，再返回回来给客户端。**

客户端发请求给服务端。中间有网关。先交给映射器，如果能处理就交给handler处理，然后交给一系列filer，然后给指定的服务，再返回回来给客户端。

![image-20210925233712996](https://i-blog.csdnimg.cn/blog_migrate/6a90dc066d40e89f765dcefca5703f2f.png)​

#### 4.4.**1、gulimall父工程下新建gulimall-gateway模块作为网关**

新建springboot项目，勾选gateway：

![](https://i-blog.csdnimg.cn/blog_migrate/d31ea91abe32751a1cefd9f4d74a5f6c.png)​

![](https://i-blog.csdnimg.cn/blog_migrate/0beaea83653b77505ab0f1f7fdbff60e.png)​ 

pom导入common模块 

```XML
    <dependencies>
        <dependency>
            <groupId>com.xmh.gulimall</groupId>
            <artifactId>gulimall-common</artifactId>
            <version>1.0.0-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
    </dependencies>
```

在nacos上新建gateway命名空间

![](https://i-blog.csdnimg.cn/blog_migrate/ea6149f118328747df1af9bfc538ef86.png)​ 

在gateway命名空间下新建配置`gulimall-gateway.yml`： 

![image-20210925234232602](https://i-blog.csdnimg.cn/blog_migrate/753006b806685704f9bbb96b85259ffd.png)​

配置application.yml

```bash
server:
  port: 88
spring:
  cloud:
    nacos:
      discovery:
        server-addr: 127.0.0.1:8848
  application:
    name: gulimall-gateway
```

配置bootstrap.yml

```java
spring:
  application:
    name: gulimall-gateway
  cloud:
    nacos:
      config:
        server-addr: 127.0.0.1:8848
        file-extension: yaml
        namespace: 改成你自己命名空间id
        #namespace: d717d0ee-7a07-4125-9881-3ef57d696ad3
```

**引导类注解@EnableDiscoveryClient，并排除数据源配置：**

> **引入mybatisplus依赖​​​​​​​后不配置数据源报错：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/238ddd8081ec6500a9a7c6382297fd24.png)
> 
>  因为引入了common模块的依赖，common里有mybatisplus依赖。**引入了mybatisplus依赖就必须配置数据源项目才能运行，而网关模块没必要配置数据源，所以这里要排除。**

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class}) //不用数据源，过滤掉数据源配置
@EnableDiscoveryClient
public class GulimallGatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(GulimallGatewayApplication.class, args);
    }
}
```

#### 4.4.**2、演示，网关路由到百度**

> **需求：访问http://localhost:88?url=baidu 切换到百度， http://localhost:88?url=qq 切换到qq**

在网关的application.yml中配置路由

```bash
server:
  port: 88
spring:
  cloud:
    nacos:
      discovery:
        server-addr: 127.0.0.1:8848
    gateway:
      routes:
        - id: baidu_route              # 每一个路由的名字，唯一即可
          uri: https://www.baidu.com   # 匹配后提供服务的路由地址
          predicates:                 # 断言规则
            - Query=url,baidu         #如果url参数等于baidu 符合断言，转到uri

        - id: qq_route                  # 每一个路由的名字，唯一即可
          uri: https://www.qq.com   # 匹配后提供服务的路由地址
          predicates: # 断言规则
            - Query=url,qq         #如果url参数等于baidu 符合断言，转到uri

  application:
    name: gulimall-gateway
```

> **断言工厂包括：** 
> 
> | **名称** | **说明** | **示例** |
> | --- | --- | --- |
> | After | 是某个时间点后的请求 | \- After=2037-01-20T17:42:47.789-07:00\[America/Denver\] |
> | Before | 是某个时间点之前的请求 | \- Before=2031-04-13T15:14:47.433+08:00\[Asia/Shanghai\] |
> | Between | 是某两个时间点之前的请求 | \- Between=2037-01-20T17:42:47.789-07:00\[America/Denver\], 2037-01-21T17:42:47.789-07:00\[America/Denver\] |
> | Cookie | 请求必须包含某些cookie | \- Cookie=chocolate, ch.p |
> | Header | 请求必须包含某些header | \- Header=X-Request-Id, \\d+ |
> | Host | 请求必须是访问某个host（域名） | \- Host=**.somehost.org,**.anotherhost.org |
> | Method | 请求方式必须是指定方式 | \- Method=GET,POST |
> | **Path** | **请求路径**必须符合指定规则 | **\- Path=**/red/{segment},/blue/\*\* |
> | Query | 请求参数必须包含指定参数 | \- Query=name, Jack或者- Query=name |
> | RemoteAddr | 请求者的ip必须是指定范围 | \- RemoteAddr=192.168.1.1/24 |
> | Weight | 权重处理 |  |
> 
> ​​​​​​​具体网关内容参考： [SpringCloud基础2——nacos配置、Feign、Gateway\_nacos feign配置\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126772669?spm=1001.2014.3001.5501 "SpringCloud基础2——nacos配置、Feign、Gateway_nacos feign配置_vincewm的博客-CSDN博客")

启动网关，访问http://localhost:88?url=baidu测试，成功！

![image-20210925234834078](https://i-blog.csdnimg.cn/blog_migrate/8f7de6104f88a0f1002d77adf94ee4cd.png)​

## 5、前端基础（回顾，与项目无关）

> 前端基础**了解即可，初级工程师应该提升深度而非广度**，技术停留在**能基本看懂代码**的基础上即可，**建议选择性过一遍即可**，哪个知识点没学过就过哪里。
> 
> [【黑马Java笔记】JavaWeb基础4——HTML,JavaScript&CSS\_vincewm的博客-CSDN博客\_java添加输入框](https://blog.csdn.net/qq_40991313/article/details/125909662 "【黑马Java笔记】JavaWeb基础4——HTML,JavaScript&CSS_vincewm的博客-CSDN博客_java添加输入框")
> 
> [【黑马Java笔记】JavaWeb基础10——VUE&Element&整合Javaweb的商品管理系统\_vincewm的博客-CSDN博客\_javaweb商品管理系统](https://blog.csdn.net/qq_40991313/article/details/126186764?spm=1001.2014.3001.5502 "【黑马Java笔记】JavaWeb基础10——VUE&Element&整合Javaweb的商品管理系统_vincewm的博客-CSDN博客_javaweb商品管理系统")

### 5.1. ES6基础

![](https://i-blog.csdnimg.cn/blog_migrate/68ced9e8a259e39441696a55216ace7c.png)​ 

![](https://i-blog.csdnimg.cn/blog_migrate/f3d3bf42ec0e7c1ae1e6292d845eefa7.png)​ 

#### 5.1.1、let & const

vscode快捷键：`！+ 回车`生成html模板

![](https://i-blog.csdnimg.cn/blog_migrate/88d0de8819aeabfff2b3bdc996b1f230.png)​ 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

-   **let声明后不能作用于{}外**，var可以
-   **let只能声明一次**（let a=1;let a=2;报错），var可以声明多次
-   **var会变量提升**（使用在定义之前，console.log(x);var x = 10;  // undefined），let必须先定义再使用
-   const一旦初始化后，不能改变

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        // var 声明的变量往往会越域
        // let 声明的变量有严格局部作用域
        {
            var a = 1;
            let b = 2;
        }
        console.log(a);  // 1
        console.log(b);  // ReferenceError: b is not defined

        // var 可以声明多次
        // let 只能声明一次
        var m = 1
        var m = 2
        let n = 3
        //         let n = 4
        console.log(m)  // 2
        console.log(n)  // Identifier 'n' has already been declared

        // var 会变量提升
        // let 不存在变量提升
        console.log(x);  // undefined
        var x = 10;
        console.log(y);   //报错ReferenceError: y is not defined
        let y = 20;

        // let
        // 1. const声明之后不允许改变
        // 2. 一但声明必须初始化，否则会报错
        const a = 1;
        a = 3; //Uncaught TypeError: Assignment to constant variable.

    </script>
</body>

</html>
```

打开Chrome控制台可以查看报错信息。 

#### 5.1.2、解构表达式

-   **数组解构（批量赋值）**`let arr = [1,2,3];` `let [a,b,c] = arr`
-   **对象解构**`const{name:abc, age, language} = person;console.log(abc);` 其中`name:abc`代表把name改名为abc
-   **字符串扩展**`str.startsWith();str.endsWith();str.includes();str.includes()`
-   **字符串模板**，\`\`符号，支持一个字符串定义为多行

![](https://i-blog.csdnimg.cn/blog_migrate/bad0faa8eeedaaede16a4ecf92f30d96.png)​

![](https://i-blog.csdnimg.cn/blog_migrate/df062f36bb20a02b1df44a406efd125f.png)​ 

-   **占位符功能** ${}，字符串插入变量

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        //数组解构
        let arr = [1,2,3];
        // // let a = arr[0];
        // // let b = arr[1];
        // // let c = arr[2];

        let [a,b,c] = arr;
        console.log(a,b,c)

        const person = {
            name: "jack",
            age: 21,
            language: ['java', 'js', 'css']
        }
        //         const name = person.name;
        //         const age = person.age;
        //         const language = person.language;

        //对象解构 // 把name属性变为abc，声明了abc、age、language三个变量
        const { name: abc, age, language } = person;
        console.log(abc, age, language)

        //4、字符串扩展
        let str = "hello.vue";
        console.log(str.startsWith("hello"));//true
        console.log(str.endsWith(".vue"));//true
        console.log(str.includes("e"));//true
        console.log(str.includes("hello"));//true

        //字符串模板 ``可以定义多行字符串
        let ss = `<div>
                    <span>hello world<span>
                </div>`;
        console.log(ss);
        
        function fun() {
            return "这是一个函数"
        }

        // 2、字符串插入变量和表达式。变量名写在 ${} 中，${} 中可以放入 JavaScript 表达式。
        let info = `我是${abc}，今年${age + 10}了, 我想说： ${fun()}`;
        console.log(info);

    </script>
</body>
</html>
```

#### 5.1.3、函数优化

-   支持函数**形参默认值**`function add(a, **b = 1**){}`
-   支持**不定参数数量**`function fun(...values){}，此时能传多个参数，values.length获取数量。`
-   支持**箭头函数**`var print = obj => console.log(obj);有点**像Lambda表达式**`
-   支持**箭头函数+解构对象**`var hello2 = ({name}) => console.log("hello," +name); hello2(person);这里参数{name}是解构出person对象的name属性`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

    <script>
        //在ES6以前，我们无法给一个函数参数设置默认值，只能采用变通写法：
        function add(a, b) {
            // 判断b是否为空，为空就给默认值1
            b = b || 1;
            return a + b;
        }
        // 传一个参数
        console.log(add(10));


        //现在可以这么写：直接给参数写上默认值，没传就会自动使用默认值
        function add2(a, b = 1) {
            return a + b;
        }
        console.log(add2(20));


        //2）、不定参数
        function fun(...values) {
            console.log(values.length)
        }
        fun(1, 2)      //2
        fun(1, 2, 3, 4)  //4

        //3）、箭头函数。lambda
        //以前声明一个方法
        // var print = function (obj) {
        //     console.log(obj);
        // }
        var print = obj => console.log(obj);
        print("hello");

        var sum = function (a, b) {
            c = a + b;
            return a + c;
        }

        var sum2 = (a, b) => a + b;
        console.log(sum2(11, 12));

        var sum3 = (a, b) => {
            c = a + b;
            return a + c;
        }
        console.log(sum3(10, 20))


        const person = {
            name: "jack",
            age: 21,
            language: ['java', 'js', 'css']
        }

        function hello(person) {
            console.log("hello," + person.name)
        }

        //箭头函数+解构
        var hello2 = ({name}) => console.log("hello," +name);
        hello2(person);

    </script>
</body>
</html>
```

#### 5.1.4、对象优化

-   可以**获取map的键值对**`Object.keys(personMap)`、`Object.values(personMap)`、`Object.entries(personMap)`
-   `Object.assgn(target,source1,source2)` **合并对象**source1，source2到target
-   支持**对象名声明简写**：如果属性名和属性值的变量名相同可以省略
-   `let someone = {...person}`取出person对象所有的属性拷贝到当前对象

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <script>
        const person = {
            name: "jack",
            age: 21,
            language: ['java', 'js', 'css']
        }

        console.log(Object.keys(person));//["name", "age", "language"]
        console.log(Object.values(person));//["jack", 21, Array(3)]
        console.log(Object.entries(person));//[Array(2), Array(2), Array(2)]，这里每个Array能点开查看键值对

        const target = { a: 1 };
        const source1 = { b: 2 };
        const source2 = { c: 3 };

        // 合并
        //{a:1,b:2,c:3}
        Object.assign(target, source1, source2);

        console.log(target);//["name", "age", "language"]

        //2）、声明对象简写
        const age = 23
        const name = "张三"
        const person1 = { age: age, name: name }
        // 等价于
        const person2 = { age, name }//声明对象简写
        console.log(person2);

        //3）、对象的函数属性简写
        let person3 = {
            name: "jack",
            // 以前：
            eat: function (food) {
                console.log(this.name + "在吃" + food);
            },
            //箭头函数this不能使用，要使用的话需要使用：对象.属性
            eat2: food => console.log(person3.name + "在吃" + food),
            eat3(food) {
                console.log(this.name + "在吃" + food);
            }
        }

        person3.eat("香蕉");
        person3.eat2("苹果")
        person3.eat3("橘子");

        //4）、对象拓展运算符

        // 1、拷贝对象（深拷贝）
        let p1 = { name: "Amy", age: 15 }
        let someone = { ...p1 }
        console.log(someone)  //{name: "Amy", age: 15}

        // 2、合并对象
        let age1 = { age: 15 }
        let name1 = { name: "Amy" }
        let p2 = { name: "zhangsan" }
        p2 = { ...age1, ...name1 }
        console.log(p2)
    </script>
</body>

</html>
```

#### 5.1.5、map和reduce

-   `arr.map()`接收一个函数，将arr中的所有元素用接收到的函数处理后放入新的数组
-   `arr.reduce()`为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>

    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>

    <body>


        <script>
            //数组中新增了map和reduce方法。
            //map()：接收一个函数，将原数组中的所有元素用这个函数处理后放入新数组返回。
            let arr = ['1', '20', '-5', '3'];

            //  arr = arr.map((item)=>{
            //     return item*2
            //  });
            arr = arr.map(item => item * 2);



            console.log(arr);
            //reduce() 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，
            //[2, 40, -10, 6]
            //arr.reduce(callback,[initialValue])
            /**
             1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
        2、currentValue （数组中当前被处理的元素）
        3、index （当前元素在数组中的索引）
        4、array （调用 reduce 的数组）*/
            let result = arr.reduce((a, b) => {
                console.log("上一次处理后：" + a);
                console.log("当前正在处理：" + b);
                return a + b;
            }, 100);
            console.log(result)


        </script>
    </body>

    </html>
    <script>
        //数组中新增了map和reduce方法。
        //map()：接收一个函数，将原数组中的所有元素用这个函数处理后放入新数组返回。
        let arr = ['1', '20', '-5', '3'];

        //  arr = arr.map((item)=>{
        //     return item*2
        //  });
        arr = arr.map(item => item * 2);



        console.log(arr);
        //reduce() 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，
        //[2, 40, -10, 6]
        //arr.reduce(callback,[initialValue])
        /**
        1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
        2、currentValue （数组中当前被处理的元素）
        3、index （当前元素在数组中的索引）
        4、array （调用 reduce 的数组）*/
        let result = arr.reduce((a, b) => {
            console.log("上一次处理后：" + a);
            console.log("当前正在处理：" + b);
            return a + b;
        }, 100);
        console.log(result)


    </script>
</body>

</html>
```

#### 5.1.6、promise

-   优化异步操作。封装ajax
-   把Ajax封装到Promise中，赋值给let p
-   在Ajax中成功使用resolve(data)，失败使用reject(err)
-   p.then().catch()

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>
</head>

<body>

    <script>
        //1、查出当前用户信息
        //2、按照当前用户的id查出他的课程
        //3、按照当前课程id查出分数
        // $.ajax({
        //     url: "mock/user.json",
        //     success(data) {
        //         console.log("查询用户：", data);
        //         $.ajax({
        //             url: `mock/user_corse_${data.id}.json`,
        //             success(data) {
        //                 console.log("查询到课程：", data);
        //                 $.ajax({
        //                     url: `mock/corse_score_${data.id}.json`,
        //                     success(data) {
        //                         console.log("查询到分数：", data);
        //                     },
        //                     error(error) {
        //                         console.log("出现异常了：" + error);
        //                     }
        //                 });
        //             },
        //             error(error) {
        //                 console.log("出现异常了：" + error);
        //             }
        //         });
        //     },
        //     error(error) {
        //         console.log("出现异常了：" + error);
        //     }
        // });


        //1、Promise可以封装异步操作
        // let p = new Promise((resolve, reject) => {
        //     //1、异步操作
        //     $.ajax({
        //         url: "mock/user.json",
        //         success: function (data) {
        //             console.log("查询用户成功:", data)
        //             resolve(data);
        //         },
        //         error: function (err) {
        //             reject(err);
        //         }
        //     });
        // });

        // p.then((obj) => {
        //     return new Promise((resolve, reject) => {
        //         $.ajax({
        //             url: `mock/user_corse_${obj.id}.json`,
        //             success: function (data) {
        //                 console.log("查询用户课程成功:", data)
        //                 resolve(data);
        //             },
        //             error: function (err) {
        //                 reject(err)
        //             }
        //         });
        //     })
        // }).then((data) => {
        //     console.log("上一步的结果", data)
        //     $.ajax({
        //         url: `mock/corse_score_${data.id}.json`,
        //         success: function (data) {
        //             console.log("查询课程得分成功:", data)
        //         },
        //         error: function (err) {
        //         }
        //     });
        // })

        function get(url, data) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    url: url,
                    data: data,
                    success: function (data) {
                        resolve(data);
                    },
                    error: function (err) {
                        reject(err)
                    }
                })
            });
        }

        get("mock/user.json")
            .then((data) => {
                console.log("用户查询成功~~~:", data)
                return get(`mock/user_corse_${data.id}.json`);
            })
            .then((data) => {
                console.log("课程查询成功~~~:", data)
                return get(`mock/corse_score_${data.id}.json`);
            })
            .then((data)=>{
                console.log("课程成绩查询成功~~~:", data)
            })
            .catch((err)=>{
                console.log("出现异常",err)
            });

    </script>
</body>

</html>
```

#### 5.1.7、模块化

-   `export`用于规定模块的对外接口,`export`不仅可以导出对象，一切JS变量都可以导出。比如：基本类型变量、函数、数组、对象
-   `import`用于导入其他模块提供的功能

```javascript
// user.js

var name = "jack"
var age = 21
function add(a,b){
    return a + b;
}
// 导出变量和函数
export {name,age,add}

---------------------------------------------------------------
// hello.js
    
// 导出后可以重命名
export default {
    sum(a, b) {
        return a + b;
    }
}


--------------------------------------------------------------
// main.js

import abc from "./hello.js"
import {name,add} from "./user.js"

abc.sum(1,2);
console.log(name);
add(1,3);
```

### 5.2. VUE基础

MVVM思想

M：model 包括数据和一些基本操作  
V：view 视图，页面渲染结果  
VM：View-model，模型与视图间的双向操作（无需开发人员干涉）  
视图和数据通过VM绑定起来，model里有变化会自动地通过Directives填写到视view中，视图表单中添加了内容也会自动地通过DOM Listeners保存到模型中。

官方文档：https://cn.vuejs.org/v2/guide/

#### 5.2.1、VUE安装

给当前项目安装vue

```bash
#npm初始化项目，生成package.json
npm init -y
#安装vue
npm install vue@2.6.10
```

> **npm init -y：**在文件夹下生成默认的**package.json**文件，代表此文件夹是npm管理的项目。

![](https://i-blog.csdnimg.cn/blog_migrate/d472635aab0d9995afd300c3cb132e84.png)​

**引入vue：**

```
<script src="./node_modules/vue/dist/vue.js"></script>
```

**示例：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <p>原始字符串: {{ message }}</p>
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                message: 'Runoob!'
            }
        })
    </script>
</body>
</html>
```

![](https://i-blog.csdnimg.cn/blog_migrate/4811928b32bef91c2a044744bb9112d2.png)

#### 5.2.2、v-model, v-on

-   new VUE
-   v-model 双向绑定
-   v-on 绑定事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <input type="text" v-model="num">
        <!-- v-model实现双向绑定。此处代表输入框和vue里的data绑定 -->
        
        <button v-on:click="num++">点赞</button>
        <!-- v-on:click绑定事件，实现自增。 -->
        
        <button v-on:click="cancel">取消</button>
        <!-- 回调自定义的方法。 此时字符串里代表的函数 -->
        
        <h1> {{name}} ,非常帅，有{{num}}个人为他点赞{{hello()}}</h1>
        <!-- 先从vue中拿到值填充到dom，input再改变num值，vue实例更新，然后此处也更新 -->
    </div>

    <!-- 导入依赖 -->
    <script src="./node_modules/vue/dist/vue.js"></script>

    <script>
        //1、vue声明式渲染
        let vm = new Vue({ //生成vue对象
            el: "#app",//绑定元素 div id="app" // 可以指定恰标签，但是不可以指定body标签
            data: {  //封装数据
                name: "张三",  // 也可以使用{} //表单中可以取出
                num: 1
            },
            methods:{  //封装方法
                cancel(){
                    this.num -- ;
                },
                hello(){
                    return "1"
                }
            }
        });
        // 还可以在html控制台vm.name

        //2、双向绑定,模型变化，视图变化。反之亦然。
        //3、事件处理

        //v-xx：指令

        //1、创建vue实例，关联页面的模板，将自己的数据（data）渲染到关联的模板，响应式的
        //2、指令来简化对dom的一些操作。
        //3、声明方法来做更复杂的操作。methods里面可以封装方法。

    </script>
</body>
</html>
```

#### 5.2.3、v-text、v-html、v-ref

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
   
    <div id="app">
        {{msg}}  {{1+1}}  {{hello()}} 前面的内容如果网速慢的话会先显示括号，然后才替换成数据。
        v-html 和v-text能解决这个问题
        <br/>
        
        用v-html取内容
        <span v-html="msg"></span>
        
        <br/>
        原样显示
        <span v-text="msg"></span>  
    </div>
   
    <script src="../node_modules/vue/dist/vue.js"></script>

    <script>
        new Vue({
            el:"#app",
            data:{
                msg:"<h1>Hello</h1>",
                link:"http://www.baidu.com"
            },
            methods:{
                hello(){
                    return "World"
                }
            }
        })
    </>
    
</body>
</html>
```

#### 5.2.4、单向绑定v-bind:

-   花括号只能写在标签体内（`<div 标签内> 标签体 </div>`），不能用在标签内。
    
    插值表达式只能用在标签体里，如果我们这么用`<a href="{{}}">`是不起作用的，所以要用v-bind
    
-   跳转页面`<a v-bind:href="link">跳转</a>`
    
-   用`v-bind:`，简写为`:`。表示把model绑定到view。可以设置src、title、class等
    

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
</head>
<body>

    <!-- 给html标签的属性绑定 -->
    <div id="app"> 

        <a v-bind:href="link">跳转</a>

        <!-- class,style  {class名：vue值}-->
        <span v-bind:class="{active:isActive,'text-danger':hasError}"
          :style="{color: color1,fontSize: size}">你好</span>

    </div>

    <script src="../node_modules/vue/dist/vue.js"></script>

    <script>
        let vm = new Vue({
            el:"#app",
            data:{
                link: "http://www.baidu.com",
                isActive:true,
                hasError:true,
                color1:'red',
                size:'36px'
            }
        })
    </script>

</body>
</html>
```

#### 5.2.5、双向绑定v-model

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

    <!-- 表单项，自定义组件 -->
    <div id="app">

        精通的语言：如果是多选框，那么会把每个value值赋值给vue数据
            <input type="checkbox" v-model="language" value="Java"> java<br/>
            <input type="checkbox" v-model="language" value="PHP"> PHP<br/>
            <input type="checkbox" v-model="language" value="Python"> Python<br/>
        选中了 {{language.join(",")}}
    </div>
    
    <script src="../node_modules/vue/dist/vue.js"></script>

    <script>
        let vm = new Vue({
            el:"#app",
            data:{
                language: []
            }
        })
    </script>

</body>
</html>
```

#### 5.2.6、v-on事件

-   事件监听可以使用 v-on 指令
-   `v-on:事件类型="方法"` ，可以简写成`@事件类型="方法"`
-   Vue.js 为 v-on 提供了事件修饰符来处理 DOM 事件细节，如：event.preventDefault() 或 event.stopPropagation()。
-   Vue.js 通过由点 . 表示的指令后缀来调用修饰符。
    -   .stop - 阻止冒泡
    -   .prevent - 阻止默认事件
    -   .capture - 阻止捕获
    -   .self - 只监听触发该元素的事件
    -   .once - 只触发一次
    -   .left - 左键事件
    -   .right - 右键事件
    -   .middle - 中间滚轮事

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <div id="app">
                
        <!--事件中直接写js片段-->
        <button v-on:click="num++">点赞</button>
        <!--事件指定一个回调函数，必须是Vue实例中定义的函数-->
        <button @click="cancel">取消</button>
        <!--  -->
        <h1>有{{num}}个赞</h1>


        <!-- 事件修饰符 -->
        <div style="border: 1px solid red;padding: 20px;" v-on:click.once="hello">
            大div
            <div style="border: 1px solid blue;padding: 20px;" @click.stop="hello">
                小div <br />
                <a href="http://www.baidu.com" @click.prevent.stop="hello">去百度</a>
            </div>
        </div>



        <!-- 按键修饰符： -->
        <input type="text" v-model="num" v-on:keyup.up="num+=2" @keyup.down="num-=2" @click.ctrl="num=10"><br />

        提示：

    </div>
    <script src="../node_modules/vue/dist/vue.js"></script>

    <script>
        new Vue({
            el:"#app",
            data:{
                num: 1
            },
            methods:{
                cancel(){
                    this.num--;
                },
                hello(){
                    alert("点击了")
                }
            }
        })
    </script>
</body>

</html>
```

#### 5.2.7、v-for遍历

-   可以遍历 数组\[\] 字典{} 。对于字典`<li v-for="(value, key, index) in object">`
-   遍历的时候都加上:key来区分不同数据，提高vue渲染效率

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>

    <div id="app">
        <ul>
            <!-- 4、遍历的时候都加上:key来区分不同数据，提高vue渲染效率 -->
            <li v-for="(user,index) in users" :key="user.name" v-if="user.gender == '女'">
                <!-- 1、显示user信息：v-for="item in items" -->
               当前索引：{{index}} ==> {{user.name}}  ==>   
                  {{user.gender}} ==>{{user.age}} <br>
                <!-- 2、获取数组下标：v-for="(item,index) in items" -->
                <!-- 3、遍历对象：
                        v-for="value in object"
                        v-for="(value,key) in object"
                        v-for="(value,key,index) in object" 
                -->
                对象信息：
                <span v-for="(v,k,i) in user">{{k}}=={{v}}=={{i}}；</span>
                <!-- 4、遍历的时候都加上:key来区分不同数据，提高vue渲染效率 -->
            </li>

            
        </ul>

        <ul>
            <li v-for="(num,index) in nums" :key="index"></li>
        </ul>
    </div>
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script>         
        let app = new Vue({
            el: "#app",
            data: {
                users: [
                { name: '柳岩', gender: '女', age: 21 },
                { name: '张三', gender: '男', age: 18 },
                { name: '范冰冰', gender: '女', age: 24 },
                { name: '刘亦菲', gender: '女', age: 18 },
                { name: '古力娜扎', gender: '女', age: 25 }
                ],
                nums: [1,2,3,4,4]
            },
        })
    </script>
</body>

</html>
```

#### 5.2.8、v-if和v-show

-   在vue实例的data指定一个bool变量，然后v-show赋值即可。show里的字符串也可以比较
-   if是根据表达式的真假，切换元素的显示和隐藏（操作dom元素）
-   区别：show的标签F12一直都在，if的标签会移除，
-   if操作dom树对性能消耗大

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <!-- 
        v-if，顾名思义，条件判断。当得到结果为true时，所在的元素才会被渲染。
        v-show，当得到结果为true时，所在的元素才会被显示。 
    -->
    <div id="app">
        <button v-on:click="show = !show">点我呀</button>
        <!-- 1、使用v-if显示 -->
        <h1 v-if="show">if=看到我....</h1>
        <!-- 2、使用v-show显示 -->
        <h1 v-show="show">show=看到我</h1>
    </div>

    <script src="../node_modules/vue/dist/vue.js"></script>
        
    <script>
        let app = new Vue({
            el: "#app",
            data: {
                show: true
            }
        })
    </script>

</body>

</html>
```

#### 5.2.9、v-else和v-else-if

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <button v-on:click="random=Math.random()">点我呀</button>
        <span>{{random}}</span>

        <h1 v-if="random>=0.75">
            看到我啦? >= 0.75
        </h1>
        <h1 v-else-if="random>=0.5">
            看到我啦? >= 0.5
        </h1>
        <h1 v-else-if="random>=0.2">
            看到我啦? >= 0.2
        </h1>
        <h1 v-else>
            看到我啦? < 0.2
        </h1>

    </div>


    <script src="../node_modules/vue/dist/vue.js"></script>
        
    <script>         
        let app = new Vue({
            el: "#app",
            data: { random: 1 }
        })     
    </script>
</body>

</html>
```

#### 5.2.10、计算属性和监听器

**计算属性computed：属性**不是具体值，而**是通过一个函数计算出来的**，**随时变化**

```html
<body>
    <div id="app">
        <p>原始字符串: {{ message }}</p>
        <p>计算后反转字符串: {{ reversedMessage }}</p>
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                message: 'Run,oob!'
            },
            computed: {
                // 计算属性的 getter
                reversedMessage: function () {
                    // `this` 指向 vm 实例
                    return this.message.split(',').reverse().join('')
                }
            }
        })
    </script>
</body>
```

![](https://i-blog.csdnimg.cn/blog_migrate/81266c872c27ff62a214ac891492c599.png)

**监听watch:**可以让我们**监控一个值的变化，从而做出相应的反应**。

以下实例通过使用 watch 实现计数器：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <!-- 某些结果是基于之前数据实时计算出来的，我们可以利用计算属性。来完成 -->
        <ul>
            <li>西游记； 价格：{{xyjPrice}}，数量：<input type="number" v-model="xyjNum"> </li>
            <li>水浒传； 价格：{{shzPrice}}，数量：<input type="number" v-model="shzNum"> </li>
            <li>总价：{{totalPrice}}</li>
            {{msg}}
        </ul>
    </div>
    <script src="../node_modules/vue/dist/vue.js"></script>

    <script>
        
        new Vue({
            el: "#app",
            data: {
                xyjPrice: 99.98,
                shzPrice: 98.00,
                xyjNum: 1,
                shzNum: 1,
                msg: ""
            },
//计算属性
            computed: {
                totalPrice(){
                    return this.xyjPrice*this.xyjNum + this.shzPrice*this.shzNum
                }
            },
//监听器，watch可以让我们监控一个值的变化。从而做出相应的反应。
            watch: {
                xyjNum: function(newVal,oldVal){
                    if(newVal>=3){
                        this.msg = "库存超出限制";
                        this.xyjNum = 3
                    }else{
                        this.msg = "";
                    }
                }
            },
        })
    </script>

</body>

</html>
```

#### 5.2.11、过滤器filter

过滤器filter：定义filter组件后，管道符“|”后面跟具体过滤器**`{{user.gender | gFilter}}`**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <!-- 过滤器常用来处理文本格式化的操作。过滤器可以用在两个地方：双花括号插值和 v-bind 表达式 -->
    <div id="app">
        <ul>
            <li v-for="user in userList">
                {{user.id}} ==> {{user.name}} ==> {{user.gender == 1?"男":"女"}} ==>
                {{user.gender | genderFilter}} ==> {{user.gender | gFilter}}
            </li>
        </ul>
    </div>
    <script src="../node_modules/vue/dist/vue.js"></script>

    <script>

        // 全局过滤器，方法实参是管道符前面的值
        Vue.filter("gFilter", function (val) {
            if (val == 1) {
                return "男~~~";
            } else {
                return "女~~~";
            }
        })

        let vm = new Vue({
            el: "#app",
            data: {
                userList: [
                    { id: 1, name: 'jacky', gender: 1 },
                    { id: 2, name: 'peter', gender: 0 }
                ]
            },
            filters: { // 局部过滤器，只可以在当前vue实例中使用
                genderFilter(val) {
                    if (val == 1) {
                        return "男";
                    } else {
                        return "女";
                    }
                }
            }
        })
    </script>
</body>

</html>
```

![](https://i-blog.csdnimg.cn/blog_migrate/ad6258e86399ab9db0381b520e77789b.png)

#### 5.2.12、组件化

-   在大型应用开发的时候，页面可以划分成很多部分。往往不同的页面，也会有相同的部分。例如可能会有相同的头部导航。
-   但是如果每个页面都自开发，这无疑增加了我们开发的成本。所以我们会把页面的不同分拆分成立的组件，然后在不同页面就可以共享这些组件，避免重复开发。
-   在vue里，所有的vue实例都是组件
-   组件其实也是一个vue实例，因此它在定义时也会接收：data、methods、生命周期函数等
-   不同的是组件不会与页面的元素绑定（所以不写el），否则就无法复用了，因此没有el属性。
-   但是组件渲染需要html模板，所以增加了template属性，值就是HTML模板
-   data必须是一个函数，不再是一个对象。
-   全局组件定义完毕，任何vue实例都可以直接在HTML中通过组件名称来使用组件了

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
</head>

<body>

    <div id="app">
        <button v-on:click="count++">我被点击了 {{count}} 次</button>

        每个对象都是独立统计的
        <counter></counter>
        <counter></counter>
        <counter></counter>
        <counter></counter>
        <counter></counter>

        <button-counter></button-counter>
    </div>
    <script src="../node_modules/vue/dist/vue.js"></script>


    <script>
        //1、全局声明注册一个组件 // counter标签，代表button
        // 把页面中<counter>标签替换为指定的template，而template中的数据用data填充
        Vue.component("counter", {
            template: `<button v-on:click="count++">我被点击了 {{count}} 次</button>`,
            data() {// 如果 Vue 没有这条规则，点击一个按钮就可能会像如下代码一样影响到其它所有实例：
                return {
                    count: 1 // 数据
                }
            }
        });

        //2、局部声明一个组件
        const buttonCounter = {
            template: `<button v-on:click="count++">我被点击了 {{count}} 次~~~</button>`,
            data() {
                return {
                    count: 1
                }
            }
        };

        new Vue({
            el: "#app",
            data: {
                count: 1
            },
            components: { // 局部声明的组件
                'button-counter': buttonCounter
            }
        })
    </script>
</body>

</html>
```

#### 5.2.13、生命周期和钩子函数

每个vue实例在被创建时都要经过一系列的初始化过程：创建实例，装载模板、渲染模板等等。vue为生命周期中的每个状态都设置了钩子函数（监听函）。每当vue实列处于不同的生命周期时，对应的函数就会被触发调用。

![](https://i-blog.csdnimg.cn/blog_migrate/eb3c6dd900b85b47607f0d757af54326.png)​

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <span id="num">{{num}}</span>
        <button @click="num++">赞！</button>
        <h2>{{name}}，有{{num}}个人点赞</h2>
    </div>

    <script src="../node_modules/vue/dist/vue.js"></script>
    
    <script>
        let app = new Vue({
            el: "#app",
            data: {
                name: "张三",
                num: 100
            },
            methods: {
                show() {
                    return this.name;
                },
                add() {
                    this.num++;
                }
            },
            beforeCreate() {
                console.log("=========beforeCreate=============");
                console.log("数据模型未加载：" + this.name, this.num);
                console.log("方法未加载：" + this.show());
                console.log("html模板未加载：" + document.getElementById("num"));
            },
            created: function () {
                console.log("=========created=============");
                console.log("数据模型已加载：" + this.name, this.num);
                console.log("方法已加载：" + this.show());
                console.log("html模板已加载：" + document.getElementById("num"));
                console.log("html模板未渲染：" + document.getElementById("num").innerText);
            },
            beforeMount() {
                console.log("=========beforeMount=============");
                console.log("html模板未渲染：" + document.getElementById("num").innerText);
            },
            mounted() {
                console.log("=========mounted=============");
                console.log("html模板已渲染：" + document.getElementById("num").innerText);
            },
            beforeUpdate() {
                console.log("=========beforeUpdate=============");
                console.log("数据模型已更新：" + this.num);
                console.log("html模板未更新：" + document.getElementById("num").innerText);
            },
            updated() {
                console.log("=========updated=============");
                console.log("数据模型已更新：" + this.num);
                console.log("html模板已更新：" + document.getElementById("num").innerText);
            }
        });
    </script>
</body>

</html>
```

### 5.3. vue脚手架进行模块化开发

#### 5.3.1、全局安装webpack

在任意目录下cmd，注意命令尾部“-g” 是全局安装的意思。

```
npm install webpack -g
```

默认安装到目录：

![](https://i-blog.csdnimg.cn/blog_migrate/51ffabbe0b5637b0a21e37bfd1d05dd0.png)

#### 5.3.2、全局安装vue脚手架

```bash
npm install -g @vue/cli@4.0.3
```

> **注意：**脚手架版本和node版本要匹配，我node版本10.16.3，匹配脚手架4.0.3 

#### 5.3.3、初始化vue项目

在工程文件夹下cmd，输入以下命令初始化vue项目。建议工程名与文件夹名一致

```bash
vue init webpack 想要起的工程名
#vue init webpack vue-demo
```

![image-20210927110259380](https://i-blog.csdnimg.cn/blog_migrate/712ffa1d36a054c851fea3a0dae4d726.png)​

> standalone单例是选择运行+编译：![](https://i-blog.csdnimg.cn/blog_migrate/230738f37a3bfa9f049bdd643614be4f.png)
> 
> ESLint是检查代码规范的，这里不选否。 
> 
> test是否使用单元测试，这里也是否

> 如果一直卡在downloading template，配置淘宝镜像
> 
> ```
> npm config set chromedriver_cdnurl https://npm.taobao.org/mirrors/chromedriver
> ```

**初始化成功，运行项目**

```bash
cd vue-demo

```

```bash
npm run dev
```

>  **为什么运行命令是npm run dev?**
> 
> 在项目目录下，我们可以看到一个名为package.json的文件，该文件是对项目、模块包的描述，在package.json文件中，有一个scripts的字段:
> 
> ```javascript
>   "scripts": {
>     "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
>     "start": "npm run dev",
>     "build": "node build/build.js"
>   },
> ```
> 
> 修改后运行命令就是npm run serve：
> 
> ```javascript
> // 运行npm run serve的scripts字段
>   "scripts": {
>     "serve": "vue-cli-service serve",
>     "build": "vue-cli-service build",
>     "lint": "vue-cli-service lint"
>   },
> ```

**启动成功**

![](https://i-blog.csdnimg.cn/blog_migrate/d0775746ef4540e85b878c436ad0af2e.png)

**访问默认端口**[http://localhost:8080/#/](http://localhost:8080/#/ "http://localhost:8080/#/")**。**

![image-20210927110328858](https://i-blog.csdnimg.cn/blog_migrate/79ea857002cfa71819c17322db577e75.png)​

关闭cmd窗口，在vscode打开项目，重新启动： 

```bash
npm run dev
```

#### 5.3.4、vue项目目录结构

![](https://i-blog.csdnimg.cn/blog_migrate/022c4d96bf23a2dc647c6ebc198f1f7b.png)

| 
目录/文件

 | 

说明

 |
| --- | --- |
| 

build

 | 

项目构建(webpack)相关代码

 |
| 

config

 | 

配置目录，包括端口号等。我们初学可以使用默认的。

 |
| 

node\_modules

 | 

npm 加载的项目依赖模块

 |
| 

**src**

 | 

这里是我们**要开发的目录**，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：`assets`: 放置一些图片，如logo等。`components`: 目录里面放了一个组件文件，可以不用。`App.vue`: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。`main.js`: 项目的核心文件。

 |
| 

**static**

 | 

**静态资源目录，如图片、字体等。**

 |
| 

test

 | 

初始测试目录，可删除

 |
| 

.xxxx文件

 | 

这些是一些配置文件，包括语法配置，git配置等

 |
| 

index.html

 | 

首页入口文件。

 |
| 

package.json

 | 

项目配置文件。

 |
| 

README.md

 | 

项目的说明文档，markdown 格式

 |

#### 5.3.5、**分析主页展示逻辑**

> /config/**index.js配置端口：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/d2c68bb4afc111829f0b390776ee00d8.png)

**/index.html主页**

其中只有一个`div，内容由src/main.js主程序决定。`

```html
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
```

src/**main.js****主程序，里面有vue实例挂载id为“app”元素：**

```java
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
//创建vue实例挂载“app”元素
new Vue({
  el: '#app',
  router, //采用router路由，导入位置./router。这里是简写，完整是router:router
  components: { App },//绑定App组件。完整是App:App
  template: '<App/>'    //元素渲染模板
})
```

**主组件/src/App.vue，显示页面并引入路由规则**

-   首先显示一张图片，图片路径为`"./assets/logo.png`
    
-   其中的`<router-view/>`是根据url要决定访问的vue,在main.js中提及了使用的是`./router`规则
    

```html
<!--模板标签，编写页面展示内容-->
<template>
  <div id="app">
<!--这里引进了一个图片-->
    <img src="./assets/logo.png">
<!--路由视图，/src/router/index.js路由规则配置访问的模块-->
    <router-view/>
  </div>
</template>

<!--vue实例代码-->
<script>
export default {
  name: 'App'
}
</script>

<!--当前模板样式-->
<style>
...
</style>
```

**配置路由规则**/src/router/**index.js**

routes表示路由规则

当访问`/`时， 显示组件`Helloword`

```javascript
import Vue from 'vue'
import Router from 'vue-router'
import HelloWorld from '@/components/HelloWorld'

Vue.use(Router)

export default new Router({
  routes: [
//访问跟路径时，路由到helloworld模块
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    }
  ]
})
```

/src/components/**HelloWorld.vue组件**

```html
<!--模板，设置内容-->
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li>
        <a
          href="https://vuejs.org"
          target="_blank"
        >
          Core Docs
        </a>
      </li>
      <li>
        <a
          href="https://forum.vuejs.org"
          target="_blank"
        >
          Forum
        </a>
      </li>
      <li>
        <a
          href="https://chat.vuejs.org"
          target="_blank"
        >
          Community Chat
        </a>
      </li>
      <li>
        <a
          href="https://twitter.com/vuejs"
          target="_blank"
        >
          Twitter
        </a>
      </li>
      <br>
      <li>
        <a
          href="http://vuejs-templates.github.io/webpack/"
          target="_blank"
        >
          Docs for This Template
        </a>
      </li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li>
        <a
          href="http://router.vuejs.org/"
          target="_blank"
        >
          vue-router
        </a>
      </li>
      <li>
        <a
          href="http://vuex.vuejs.org/"
          target="_blank"
        >
          vuex
        </a>
      </li>
      <li>
        <a
          href="http://vue-loader.vuejs.org/"
          target="_blank"
        >
          vue-loader
        </a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/awesome-vue"
          target="_blank"
        >
          awesome-vue
        </a>
      </li>
    </ul>
  </div>
</template>

<!--script，vue实例代码。-->
<script>
<!--这里导出组件，名为“HelloWorld”，在路由文件/src/router/index.js会进行导入-->
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!--style ，设置样式-->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
```

#### **5.3.6、新建Hello组件，负责/hello路径**

/src/components**创建hello.vue组件，编写组件三标签：**

```html
<template>
    <div>
        <h1>你好，hello，{{name}}</h1>
    </div>
</template>

<script>
<!--导出组件，在路由文件/src/router/index.js会导入-->
export default {
    data(){
        return {
            name: "张三"
        }
    }
}
</script>

<style>

</style>
```

**编写路由文件**，修改/src/router/index.js

```java
import Vue from 'vue'
import Router from 'vue-router'
import HelloWorld from '@/components/HelloWorld'
import Hello from '@/components/hello' //导入自定义的组件

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    },
    //新增路由
    {
      path: '/hello',
      name: "Hello",
      component: Hello
    }
  ]
})
```

**此时访问**[http://localhost:8080/#/hello](http://localhost:8080/#/hello "http://localhost:8080/#/hello")

![](https://i-blog.csdnimg.cn/blog_migrate/0164084f137693be04ae293bb8c060ac.png)

**添加App.vue点击跳转**，修改/src/App.vue的template标签：

```html
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-link to="/hello">去hello</router-link> <!--新增去hello-->
    <router-link to="/">去首页</router-link><!--新增去首页-->
    <router-view/>
  </div>
</template>
```

运行测试效果

![](https://i-blog.csdnimg.cn/blog_migrate/7ad9285646aa70d63ab59951f33b971d.png)

#### 5.3.7、快速生成组件模板

1、文件->首选项->用户代码 新建全局代码片段

2、把下面代码粘贴进去

```java
{
    "Print to console": {
        "prefix": "vue",
        "body": [
            "<!-- $1 -->",
            "<template>",
            "<div class='$2'>$5</div>",
            "</template>",
            "",
            "<script>",
            "//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）",
            "//例如：import 《组件名称》 from '《组件路径》';",
            "",
            "export default {",
            "//import引入的组件需要注入到对象中才能使用",
            "components: {},",
            "data() {",
            "//这里存放数据",
            "return {",
            "",
            "};",
            "},",
            "//监听属性 类似于data概念",
            "computed: {},",
            "//监控data中的数据变化",
            "watch: {},",
            "//方法集合",
            "methods: {",
            "",
            "},",
            "//生命周期 - 创建完成（可以访问当前this实例）",
            "created() {",
            "",
            "},",
            "//生命周期 - 挂载完成（可以访问DOM元素）",
            "mounted() {",
            "",
            "},",
            "beforeCreate() {}, //生命周期 - 创建之前",
            "beforeMount() {}, //生命周期 - 挂载之前",
            "beforeUpdate() {}, //生命周期 - 更新之前",
            "updated() {}, //生命周期 - 更新之后",
            "beforeDestroy() {}, //生命周期 - 销毁之前",
            "destroyed() {}, //生命周期 - 销毁完成",
            "activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发",
            "}",
            "</script>",
            "<style scoped>",
            "$4",
            "</style>"
        ],
        "description": "生成vue模板"
    }
    
}
```

3、在创建组件时直接输入`vue`点击回车就可生成模板

### 5.4. ElementUI

官方文档：https://element.eleme.cn/#/zh-CN/component/installation

1、安装

```
npm install element-ui
```

2、在main.js下引入

```bash
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI);
```

然后就可以使用elementui之中的组件。

3、快速搭建后台管理系统的页面

elementui手册中找到`Container 布局容器`，找到代码直接复制到`App.vue`组件

启动测试：

![image-20210927111110073](https://i-blog.csdnimg.cn/blog_migrate/25c70bc1305215dbc1a8baf24a942546.png)​

4、实现当点击用户列表，显示用户。点击hello组件，显示hello。

![image-20210927111213237](https://i-blog.csdnimg.cn/blog_migrate/541732ff4127d4c84aa75744d4a9c278.png)​

把`<el-main>`中的数据列表换成路由视图`<router-view></router-view>`

![image-20210927111502253](https://i-blog.csdnimg.cn/blog_migrate/747b154610a28028d799dd8c9f87bea8.png)​

新建MyTable组件，用来显示用户数据

```html
<!--  -->
<template>
  <div class="">
    <el-table :data="tableData">
      <el-table-column prop="date" label="日期" width="140"> </el-table-column>
      <el-table-column prop="name" label="姓名" width="120"> </el-table-column>
      <el-table-column prop="address" label="地址"> </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    const item = {
      date: "2016-05-02",
      name: "王小虎",
      address: "上海市普陀区金沙江路 1518 弄",
    };
    return {
      tableData: Array(20).fill(item),
    };
  },
};
</script>
<style scoped>
</style>
```

添加路由规则

```javascript
import MyTable from '@/components/MyTable'


	{
      path: '/mytable',
      name: "mytable",
      components: MyTable
    }
```

修改App.vue

![image-20210927111630855](https://i-blog.csdnimg.cn/blog_migrate/ad45a8bbf30a4bae6b22084272aa630c.png)​

启动测试