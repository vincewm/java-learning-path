> **导航：**
> 
> [谷粒商城笔记+踩坑汇总篇](https://blog.csdn.net/qq_40991313/article/details/127099139?spm=1001.2014.3001.5501 "谷粒商城笔记+踩坑汇总篇")
> 
>  **Java笔记汇总：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析-CSDN博客")

 **目录**

[1\. 环境搭建](#1.%20%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA)

[1.1 新建模块gulimall-auth-server](#1.1%20%E6%96%B0%E5%BB%BA%E6%A8%A1%E5%9D%97gulimall-auth-server)

[1.2 pom引入依赖](#1.2%20pom%E6%96%87%E4%BB%B6)

[1.3 引导类开启远程调用](#1.3%20%E4%BF%AE%E6%94%B9%E4%B8%BB%E7%B1%BB)

[1.4 yml配置和关闭thymeleaf缓存](#1.4%20%E9%85%8D%E7%BD%AE%E6%9C%8D%E5%8A%A1%E5%90%8D%2C%E7%AB%AF%E5%8F%A3%E5%8F%8A%E6%B3%A8%E5%86%8C%E4%B8%AD%E5%BF%83%E5%9C%B0%E5%9D%80)

[1.5 hosts文件新增域名映射](#1.5%20host%E6%96%B0%E5%A2%9E%E5%9F%9F%E5%90%8D%E6%98%A0%E5%B0%84)

[1.6 登录、注册页面动静分离](#1.6%20%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90%E4%B8%8A%E4%BC%A0)

[1.7 登录注册页面的路径加"/static/login"或"/static/reg"](#1.7%20%E4%BF%AE%E6%94%B9reg.html%20login.html%E7%9A%84%20%E5%9C%B0%E5%9D%80)

[1.8 网关配置认证路由](#1.8%20%E9%85%8D%E7%BD%AE%E7%BD%91%E5%85%B3)

[1.9 新建配置类，映射请求和页面，实现WebMvcConfigurer接口](#1.9%20%E6%96%B0%E5%A2%9E%E8%A7%86%E5%9B%BE%E6%98%A0%E5%B0%84)

[1.10 修改前端](#1.10%20%E4%BF%AE%E6%94%B9%E5%89%8D%E7%AB%AF)

[1.11 测试](#1.11%C2%A0%E6%B5%8B%E8%AF%95)

[2\. 整合短信验证码](#2.%20%E6%95%B4%E5%90%88%E7%9F%AD%E4%BF%A1%E9%AA%8C%E8%AF%81%E7%A0%81)

[2.1 购买阿里云短信服务](#2.1%20%E8%B4%AD%E4%B9%B0%E9%98%BF%E9%87%8C%E4%BA%91%E7%9F%AD%E4%BF%A1%E6%9C%8D%E5%8A%A1)

[2.2 api接口](#2.2%20postMan%E6%B5%8B%E8%AF%95)

[2.2.1 请求响应](#%E8%AF%B7%E6%B1%82%E5%93%8D%E5%BA%94)

[2.2.2 postMan测试](#postMan%E6%B5%8B%E8%AF%95)

[2.2.3 代码测试，填入自己的appcode](#%E4%BB%A3%E7%A0%81%E6%B5%8B%E8%AF%95%EF%BC%8C%E5%A1%AB%E5%85%A5%E8%87%AA%E5%B7%B1%E7%9A%84appcode)

[2.3 第三方模块整合短信服务](#%E7%AC%AC%E4%B8%89%E6%96%B9%E6%A8%A1%E5%9D%97%E6%95%B4%E5%90%88%E7%9F%AD%E4%BF%A1%E6%9C%8D%E5%8A%A1)

[2.3.0 导入HttpUtils](#2.3.4.1%20%E6%96%B0%E5%A2%9E%E7%9F%AD%E4%BF%A1%E6%9C%8D%E5%8A%A1%E7%BB%84%E4%BB%B6SmsComponent%C2%A0)

[2.3.1 新增短信服务组件SmsComponent](#2.3.1%20%E6%96%B0%E5%A2%9E%E7%9F%AD%E4%BF%A1%E6%9C%8D%E5%8A%A1%E7%BB%84%E4%BB%B6SmsComponent%C2%A0) 

[2.3.2 yml添加自定义的短信属性配置](#3.3.4.2%20yml%E6%B7%BB%E5%8A%A0%E8%87%AA%E5%AE%9A%E4%B9%89%E7%9A%84%E7%9F%AD%E4%BF%A1%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE)

[2.3.3 新增发验证码Controller](#3.3.4.3%20%E6%96%B0%E5%A2%9E%E5%8F%91%E9%AA%8C%E8%AF%81%E7%A0%81Controller)

[2.3.4 测试](#3.3.4.4%20%E6%B5%8B%E8%AF%95)

[3\. 认证服务调用短信服务](#3.%20%E8%AE%A4%E8%AF%81%E6%9C%8D%E5%8A%A1%E8%B0%83%E7%94%A8%E7%9F%AD%E4%BF%A1%E6%9C%8D%E5%8A%A1)

[3.1 feign远程调用，“认证服务”调用“第三方服务”发送短信](#3.1%20%E8%AE%A4%E8%AF%81%E6%9C%8D%E5%8A%A1%E8%BF%9C%E7%A8%8B%E8%B0%83%E7%94%A8%E4%B8%89%E6%96%B9%E6%9C%8D%E5%8A%A1%E5%8F%91%E9%80%81%E7%9F%AD%E4%BF%A1)

[3.2 登录controller发送验证码（简单实现，不考虑接口防刷）](#3.2%20%E8%AE%A4%E8%AF%81%E6%9C%8D%E5%8A%A1%E5%8F%91%E9%80%81%E7%9F%AD%E4%BF%A1%E6%8E%A5%E5%8F%A3)

[3.3 前端调用接口发送验证码](#3.3%20%E5%89%8D%E7%AB%AF%E8%B0%83%E7%94%A8%E6%8E%A5%E5%8F%A3)

[3.5 使用redis实现接口防刷](#3.5%20%E6%8E%A5%E5%8F%A3%E9%98%B2%E5%88%B7%E5%8A%9F%E8%83%BD)

[3.5.1 业务流程](#3.4%20%E6%AD%A4%E6%97%B6%E7%9A%84%E7%BC%BA%E9%99%B7)

[3.5.1 引入redis依赖](#3.5.1%20%E5%BC%95%E5%85%A5redis%E7%9B%B8%E5%85%B3%E4%BE%9D%E8%B5%96)

[3.5.2 yml配置redis地址信息](#3.5.2%20yml%E9%85%8D%E7%BD%AEredis%E5%9C%B0%E5%9D%80%E4%BF%A1%E6%81%AF)

[3.5.3 LoginController发送验证码（考虑接口防刷）](#3.5.3%20LoginController%E5%8F%91%E9%80%81%E9%AA%8C%E8%AF%81%E7%A0%81%EF%BC%88%E8%80%83%E8%99%91%E6%8E%A5%E5%8F%A3%E9%98%B2%E5%88%B7%EF%BC%89)

[4\. 注册页面相关功能实现](#4.%20%E6%B3%A8%E5%86%8C%E9%A1%B5%E9%9D%A2%E7%9B%B8%E5%85%B3%E5%8A%9F%E8%83%BD%E5%AE%9E%E7%8E%B0)

[4.1 准备](#4.1%20%E5%90%8E%E5%8F%B0JSR%20303%E6%A0%A1%E9%AA%8C)

[4.1.1 抽取注册模型类](#4.1.1%20%E6%8A%BD%E5%8F%96%E6%B3%A8%E5%86%8C%E6%A8%A1%E5%9E%8B%E7%B1%BB%C2%A0) 

[4.1.2 业务流程](#4.1.2%20%E4%B8%9A%E5%8A%A1%E6%B5%81%E7%A8%8B)

[4.1.3 controller参数注解@Valid](#4.1.3%C2%A0controller%E5%8F%82%E6%95%B0%E6%B3%A8%E8%A7%A3%40Valid%C2%A0) 

[4.2 【会员模块】存储会员信息](#4.2%20member%E6%9C%8D%E5%8A%A1%EF%BC%8C%E5%AD%98%E5%82%A8%E4%BC%9A%E5%91%98%E4%BF%A1%E6%81%AF)

[4.2.1 抽取模型类，接收用户信息](#4.2.1%20%E6%8A%BD%E5%8F%96%E6%A8%A1%E5%9E%8B%E7%B1%BB%EF%BC%8C%E6%8E%A5%E6%94%B6%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)

[4.2.2 自定义“用户名与手机号重复”的异常类](#4.2.2%20%E8%87%AA%E5%AE%9A%E4%B9%89%E2%80%9C%E7%94%A8%E6%88%B7%E5%90%8D%E4%B8%8E%E6%89%8B%E6%9C%BA%E5%8F%B7%E9%87%8D%E5%A4%8D%E2%80%9D%E7%9A%84%E5%BC%82%E5%B8%B8%E7%B1%BB)

[4.2.3 注册controller实现](#%E3%80%90%E4%BC%9A%E5%91%98%E6%A8%A1%E5%9D%97%E3%80%91%E6%B3%A8%E5%86%8C%E4%B8%9A%E5%8A%A1controller)

[4.2.4 使用BCrypt实现密码加密解密](#4.2.3%20%E4%BD%BF%E7%94%A8BCrypt%E5%AE%9E%E7%8E%B0%E5%AF%86%E7%A0%81%E5%8A%A0%E5%AF%86%E8%A7%A3%E5%AF%86)

[4.2.5 注册业务实现](#4.2.4%20%E6%B3%A8%E5%86%8C%E4%B8%9A%E5%8A%A1%E5%AE%9E%E7%8E%B0)

[4.3 【认证模块】注册业务实现](#4.3%20%E8%AE%A4%E8%AF%81%E6%9C%8D%E5%8A%A1%E6%B3%A8%E5%86%8C%E6%8E%A5%E5%8F%A3)

--

## 1\. 环境搭建

### 1.1 新建模块gulimall-auth-server

![](https://i-blog.csdnimg.cn/blog_migrate/a64f10afb9fbc255d6c27e121ef4dffc.png)

![image-20211129155519295](https://i-blog.csdnimg.cn/blog_migrate/8d8f2eaf19611d2d8dec416de187761c.png)

### 1.2 pom引入依赖

> **引入common模块，排除gulimall-common包的mybatis-plus**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.3.2.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.atguigu.gulimall</groupId>
	<artifactId>gulimall-auth-server</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>gulimall-auth-server</name>
	<description>认证中心（社交登录、OAuth2.0、单点登录）</description>

	<properties>
		<java.version>1.8</java.version>
		<spring-cloud.version>Hoxton.SR6</spring-cloud.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>com.zhourui.gulimall</groupId>
			<artifactId>gulimall-common</artifactId>
			<version>0.0.1-SNAPSHOT</version>
			<exclusions>
                <!--不需要数据库操作移除mybatis-plus,防止报错-->
				<exclusion>
					<groupId>com.baomidou</groupId>
					<artifactId>mybatis-plus-boot-starter</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-thymeleaf</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-openfeign</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
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
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```

### 1.3 引导类开启远程调用

```java
//可以远程调用,使服务能够被nacos发现
@EnableFeignClients
@EnableDiscoveryClient
```

### 1.4 yml配置和关闭thymeleaf缓存

```bash
spring:
  cloud:
    nacos:
      discovery:
        server-addr: 127.0.0.1:8848
  application:
    name: gulimall-auth-server
server:
  port: 20000
feign:

  thymeleaf:
    cache: false
```

### 1.5 hosts文件新增域名映射

```
192.168.157.128 auth.gulimall.com
```

![image-20211129161528002](https://i-blog.csdnimg.cn/blog_migrate/3dbf8dcc8e7930bde4c8ec6df0445180.png)

### 1.6 登录、注册页面动静分离

静态文件移到Nginx：

![image-20211129162344777](https://i-blog.csdnimg.cn/blog_migrate/25585564cd5d85074f8b1b96743aaada.png)

动态文件reg.html和login.html放到项目templates文件夹下： 

![](https://i-blog.csdnimg.cn/blog_migrate/6bfbc2041fd6d714ace46db6b8e5ada3.png)

### 1.7 登录注册页面的路径加"/static/login"或"/static/reg"

对应nginx上的静态地址就行

![](https://i-blog.csdnimg.cn/blog_migrate/0120d07056ca38bdb9af382091120935.png)

![](https://i-blog.csdnimg.cn/blog_migrate/6f681d475e641422011241c55e06524c.png)

![](https://i-blog.csdnimg.cn/blog_migrate/4863560ab0554886b26cac25b76bffeb.png)

### 1.8 网关配置认证路由

> gulimall-gateway/src/main/resources/application.yml

```bash
        #认证服务
        - id: gulimall_auth_host
          uri: lb://gulimall-auth-server
          predicates:
            - Host=auth.gulimall.com
```

### 1.9 新建配置类，映射请求和页面，实现WebMvcConfigurer接口

> gulimall-auth-server/src/main/java/site/xx/gulimall/auth/config/GulimallWebConfig.java

```java
package site.xxx.gulimall.auth.config;
@Configuration
public class GulimallWebConfig implements WebMvcConfigurer {

    /**
     * 视图映射:发送一个请求，直接跳转到一个页面
     */
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
//将请求"/login.html"映射到"login"页面
         registry.addViewController("/login.html").setViewName("login");
        registry.addViewController("/reg.html").setViewName("reg");
    }
}

```

> 这样就不需要写controller处理请求页面映射了：
> 
> ```java
> @Controller
> public class LoginController {
>     @GetMapping(value = "/login.html")
>     public String loginPage(HttpSession session) {
> 		return "login";
>    }
>     @GetMapping(value = "/reg.html")
>     public String regPage(HttpSession session) {
> 		return "reg";
>    }
> }
> ```

### 1.10 修改前端

修改，使登录、注册、其他页面之间可以正常跳转： 

![](https://i-blog.csdnimg.cn/blog_migrate/2a0f6a637e62f297ab5e881720e46836.png)

编写验证码的单击事件：

![](https://i-blog.csdnimg.cn/blog_migrate/a71df568e50b61bc931225aa87d420a0.png)

### 1.11 测试

http://auth.gulimall.com/login.html

![image-20211129165256538](https://i-blog.csdnimg.cn/blog_migrate/446a8d657226816e0e519b56d5581624.png)http://auth.gulimall.com/reg.html

![image-20211129165313632](https://i-blog.csdnimg.cn/blog_migrate/e8ba06014c82a3bcb08bc5e66643b46a.png)

## 2\. 整合短信验证码

### 2.1 购买阿里云短信服务

购买地址:

[【三网合一短信接口-支持协号转网】短信接口 短信验证码发送接口（免费试用）【最新版】\_数据API\_数据应用\_电商-云市场-阿里云](https://market.aliyun.com/products/57126001/cmapi024822.html?spm=5176.21213303.J_6704733920.11.49fb3edaM8bteY&scm=20140722.S_market%40%40API%E5%B8%82%E5%9C%BA%40%40cmapi024822..ID_market%40%40API%E5%B8%82%E5%9C%BA%40%40cmapi024822-RL%E4%B8%89%E5%90%88%E4%B8%80%E7%9F%AD%E4%BF%A1-OR_main-V_2-P0_2#sku=yuncode18822000012 "【三网合一短信接口-支持协号转网】短信接口 短信验证码发送接口（免费试用）【最新版】_数据API_数据应用_电商-云市场-阿里云")

![](https://i-blog.csdnimg.cn/blog_migrate/652bb6b8f236f30e349fa846e2e1ac3c.png)

### 2.2 api接口

#### 2.2.1 请求响应

_调用地址：_http(s)://fesms.market.alicloudapi.com/sms/

_请求方式：_GET

_返回类型：_JSON

请求参数：

| 
名称

 | 

类型

 | 

是否必须

 | 

描述

 |
| --- | --- | --- | --- |
| 

code

 | 

STRING

 | 

必选

 | 

要发送的验证码

 |
| 

phone

 | 

STRING

 | 

必选

 | 

接收人的手机号

 |
| 

sign

 | 

STRING

 | 

可选

 | 

签名编号【联系客服人员申请，测试请用1】

 |
| 

skin

 | 

STRING

 | 

必选

 | 

模板编号【联系旺旺客服申请，测试请用1~21】

 |

响应：

```java
{ "Message": "发送成功", "RequestId": "B26BB173-E569-46BD-B0A7-7EAF581C06D7", "BizId": "267610413312539060^0", "Code": "OK" } 
```

![](https://i-blog.csdnimg.cn/blog_migrate/6ce2af5ce02f6eecd01050c6ac4b8d03.png)

#### 2.2.2 postMan测试

 发送错误手机号：![](https://i-blog.csdnimg.cn/blog_migrate/58952edbb929100d74464433427c232b.png)

正常发送： 

![](https://i-blog.csdnimg.cn/blog_migrate/c43f50bcc46d43c1688c0e539b41dc10.png)

#### 2.2.3 代码测试，填入自己的appcode

> gulimall-third-party/src/test/java/site/zhourui/gulimall/thirdparty/SMSTest.java

![](https://i-blog.csdnimg.cn/blog_migrate/eb4440118f73640ee01da63bf2c77a6e.png)

```java
package site.xx.gulimall.thirdparty;

public class SMSTest {
    public static void main(String[] args) {
        String host = "https://fesms.market.alicloudapi.com";// 【1】请求地址 支持http 和 https 及 WEBSOCKET
        String path = "/sms/";// 【2】后缀
        String appcode = "自己的appcode "; // 【3】开通服务后 买家中心-查看AppCode
        String code = "123456"; // 【4】请求参数，详见文档描述
        String phone = "17748781xxx"; // 【4】请求参数，详见文档描述
        String sign = "1"; // 【4】请求参数，详见文档描述
        String skin = "1"; // 【4】请求参数，详见文档描述
        String urlSend = host + path + "?code=" + code + "&phone=" + phone + "&sign=" + sign + "&skin=" + skin ; // 【5】拼接请求链接
        try {
            URL url = new URL(urlSend);
            HttpURLConnection httpURLCon = (HttpURLConnection) url.openConnection();
            httpURLCon.setRequestProperty("Authorization", "APPCODE " + appcode);// 格式Authorization:APPCODE
            // (中间是英文空格)
            int httpCode = httpURLCon.getResponseCode();
            if (httpCode == 200) {
                String json = read(httpURLCon.getInputStream());
                System.out.println("正常请求计费(其他均不计费)");
                System.out.println("获取返回的json:");
                System.out.print(json);
            } else {
                Map<String, List<String>> map = httpURLCon.getHeaderFields();
                String error = map.get("X-Ca-Error-Message").get(0);
                if (httpCode == 400 && error.equals("Invalid AppCode `not exists`")) {
                    System.out.println("AppCode错误 ");
                } else if (httpCode == 400 && error.equals("Invalid Url")) {
                    System.out.println("请求的 Method、Path 或者环境错误");
                } else if (httpCode == 400 && error.equals("Invalid Param Location")) {
                    System.out.println("参数错误");
                } else if (httpCode == 403 && error.equals("Unauthorized")) {
                    System.out.println("服务未被授权（或URL和Path不正确）");
                } else if (httpCode == 403 && error.equals("Quota Exhausted")) {
                    System.out.println("套餐包次数用完 ");
                } else {
                    System.out.println("参数名错误 或 其他错误");
                    System.out.println(error);
                }
            }

        } catch (MalformedURLException e) {
            System.out.println("URL格式错误");
        } catch (UnknownHostException e) {
            System.out.println("URL地址错误");
        } catch (Exception e) {
            // 打开注释查看详细报错异常信息
            // e.printStackTrace();
        }

    }

    /*
     * 读取返回结果
     */
    private static String read(InputStream is) throws IOException {
        StringBuffer sb = new StringBuffer();
        BufferedReader br = new BufferedReader(new InputStreamReader(is));
        String line = null;
        while ((line = br.readLine()) != null) {
            line = new String(line.getBytes(), "utf-8");
            sb.append(line);
        }
        br.close();
        return sb.toString();
    }
}

```

![](https://i-blog.csdnimg.cn/blog_migrate/0a0025cfa7df2c21ef380950b9993c87.png)

### 2.3 第三方模块整合短信服务

#### 2.3.0 导入HttpUtils

从下面地址下载并导入到公共模块：

package com.xunqi.common.utils;

```
https://github.com/aliyun/api-gateway-demo-sign-java/blob/master/src/main/java/com/aliyun/api/gateway/demo/util/HttpUtils.java
```

![](https://i-blog.csdnimg.cn/blog_migrate/36ce44edf00725eb6fa27020570f835d.png)

#### 2.3.1 新增短信服务组件SmsComponent 

```java
package site.xx.gulimall.thirdparty.component;
//这个注解设置yml配置文件前缀，这样配置后yml数据就会自动注入到 Bean 中，不用再@Value
@ConfigurationProperties(prefix = "spring.cloud.alicloud.sms")
@Data
@Component
public class SmsComponent {

    private String host;
    private String path;
    private String skin;
    private String sign;
    private String appcode;

    public void sendCode(String phone,String code) {
        String method = "GET";
        Map<String, String> headers = new HashMap<String, String>();
        //最后在header中的格式(中间是英文空格)为Authorization:APPCODE 83359fd73fe94948385f570e3c139105
        headers.put("Authorization", "APPCODE " + appcode);
        Map<String, String> querys = new HashMap<String, String>();
        querys.put("code", code);
        querys.put("phone", phone);
        querys.put("skin", skin);
        querys.put("sign", sign);
        //JDK 1.8示例代码请在这里下载：  http://code.fegine.com/Tools.zip
        try {
            /**
             * 重要提示如下:
             * HttpUtils请从
             * https://github.com/aliyun/api-gateway-demo-sign-java/blob/master/src/main/java/com/aliyun/api/gateway/demo/util/HttpUtils.java
             * 或者直接下载：
             * http://code.fegine.com/HttpUtils.zip
             * 下载
             *
             * 相应的依赖请参照
             * https://github.com/aliyun/api-gateway-demo-sign-java/blob/master/pom.xml
             * 相关jar包（非pom）直接下载：
             * http://code.fegine.com/aliyun-jar.zip
             */
            HttpResponse response = HttpUtils.doGet(host, path, method, headers, querys);
            //System.out.println(response.toString());如不输出json, 请打开这行代码，打印调试头部状态码。
            //状态码: 200 正常；400 URL无效；401 appCode错误； 403 次数用完； 500 API网管错误
            //获取response的body
            System.out.println(EntityUtils.toString(response.getEntity()));
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

#### 2.3.2 yml添加自定义的短信属性配置

> 配置提示依赖，不加不影响运行。
> 
> gulimall-third-party/pom.xml
> 
> ```XML
>         <!--自定义配置的提示        -->
>         <dependency>
>             <groupId>org.springframework.boot</groupId>
>             <artifactId>spring-boot-configuration-processor</artifactId>
>             <optional>true</optional>
>         </dependency>
> ```

gulimall-third-party/src/main/resources/application.yml

> 建议配置到nacos 

```bash
      sms:
        host: http://fesms.market.alicloudapi.com
        path: /sms/
        skin: 1
        sign: 1
        appcode: 004c4072d4ed40b489d77b987ad3404d
```

![](https://i-blog.csdnimg.cn/blog_migrate/65d8619d289eb887ab708eb1dd3f8c16.png)

#### 2.3.3 新增发验证码Controller

SmsSendController，提供给别的服务进行调用 

```java
package site.xx.gulimall.thirdparty.controller;
@RestController
@RequestMapping(value = "/sms")
public class SmsSendController {
    @Autowired
    private SmsComponent smsComponent;

    /**
     * 提供给别的服务进行调用
     * @param phone
     * @param code
     * @return
     */
    @GetMapping(value = "/sendCode")
    public R sendCode(@RequestParam("phone") String phone, @RequestParam("code") String code) {
        //发送验证码
        smsComponent.sendCode(phone,code);
        return R.ok();
    }
}

```

#### 2.3.4 测试

测试:[localhost:30000/sms/sendCode?phone=17748781568&code=8888](http://localhost:30000/sms/sendCode?phone=17748781568&code=8888 "localhost:30000/sms/sendCode?phone=17748781568&code=8888")

成功同时收到短信

![image-20211129220633171](https://i-blog.csdnimg.cn/blog_migrate/46426502ef9673be52c7d6b7f5f50d7d.png)

## 3\. 认证服务调用短信服务

### 3.1 feign远程调用，“认证服务”调用“第三方服务”发送短信

认证模块：

```java
package site.xx.gulimall.auth.feign;

@FeignClient("gulimall-third-party")
public interface ThirdPartFeignService {

    @GetMapping(value = "/sms/sendCode")
    public R sendCode(@RequestParam("phone") String phone, @RequestParam("code") String code);
}

```

>  确保启动类注解了@EnableFeignClients和@EnableDiscoveryClient

### 3.2 登录controller发送验证码（简单实现，不考虑接口防刷）

> 验证码用随机UUID子串。

```java
package site.xxx.gulimall.auth.controller;

@Controller
public class LoginController {
    @Autowired
    ThirdPartFeignService thirdPartFeignService;

    @GetMapping(value = "/sms/sendCode")
    public R sendCode(@RequestParam("phone") String phone)
    {
        String code = UUID.randomUUID().toString().substring(0, 5);
        thirdPartFeignService.sendCode(phone,code);
        return R.ok();
    }
}

```

### 3.3 前端调用接口发送验证码

![image-20211129223313093](https://i-blog.csdnimg.cn/blog_migrate/c7b7bb6dfbadcd4b20d2bda3c7dbc73b.png)

> 发送验证码短信成功

![image-20211129223201931](https://i-blog.csdnimg.cn/blog_migrate/742e7e825f40d272b27c9604591ea0f0.png)

### 3.5 使用redis实现接口防刷

#### 3.5.1 业务流程

> **接口写在前端js代码里,仍然可以被其他人拿来盗刷**
> 
> 由于发送验证码的接口暴露，为了防止恶意攻击，我们不能随意让接口被调用。
> 
> -   在redis中以`phone-code`将电话号码和验证码进行存储并将当前时间与code一起存储
>     -   如果调用时以当前`phone`取出的v不为空且当前时间在存储时间的60s以内，说明60s内该号码已经调用过，返回错误信息
>     -   60s以后再次调用，需要删除之前存储的`phone-code`
>     -   code存在一个过期时间，我们设置为10min，10min内验证该验证码有效

 **接口防刷过程：**  
1）先查询**redis**，是否超过60s，否则不允许发送短信  
2）存入redis，key为“sms:code:手机号”，value为“六位数字+当前系统时间”，通过比较redis存的时间和现在时间是否超过一分钟，防止一分钟内不断刷验证码，构造参数存入过期时间10min，并且存入当前系统时间

#### 3.5.1 引入redis依赖

认证模块 

```XML
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
```

#### 3.5.2 yml配置redis地址信息

认证模块 

```
  redis:
    host: 192.168.157.128
    port: 6379
```

#### 3.5.3 LoginController发送验证码（考虑接口防刷）

> 该常量用于redis短信验证码前缀

认证模块相关的常量类：

```java
package site.xx.common.constant;

public class AuthServerConstant {

//短信验证码的缓存前缀
    public static final String SMS_CODE_CACHE_PREFIX = "sms:code:";
}

```

common模块的错误码枚举类： 

![](https://i-blog.csdnimg.cn/blog_migrate/aeac368205660892bbe9e6845a31a264.png)

controller 

```java
package site.xx.gulimall.auth.controller;
@Controller
public class LoginController {
    @Autowired
    private ThirdPartFeignService thirdPartFeignService;
    @Autowired
    private StringRedisTemplate stringRedisTemplate;

    @ResponseBody
    @GetMapping(value = "/sms/sendCode")
    public R sendCode(@RequestParam("phone") String phone) {

        //1、接口防刷
        String redisCode = stringRedisTemplate.opsForValue().get(AuthServerConstant.SMS_CODE_CACHE_PREFIX + phone);
        if (!StringUtils.isEmpty(redisCode)) {
            //活动存入redis的时间，用当前时间减去存入redis的时间，通过比较redis存的时间和现在时间是否超过一分钟，防止一分钟内不断刷验证码
            long currentTime = Long.parseLong(redisCode.split("_")[1]);
            if (System.currentTimeMillis() - currentTime < 60000) {
                //60s内不能再发
                return R.error(BizCodeEnume.SMS_CODE_EXCEPTION.getCode(),BizCodeEnume.SMS_CODE_EXCEPTION.getMsg());
            }
        }

        //2、验证码的再次效验 redis.存key-phone,value-code
//        String code = UUID.randomUUID().toString().substring(0, 5);
//        String redisValue = code+"_"+System.currentTimeMillis();
        int code = (int) ((Math.random() * 9 + 1) * 100000);// 验证码只可以是数字
        String codeNum = String.valueOf(code);
//redis存的值为六位数字+当前系统时间，防止一分钟内不断刷验证码
        String redisStorage = codeNum + "_" + System.currentTimeMillis();

        //存入redis并指定过期时间10min，十分钟内验证码有效
        stringRedisTemplate.opsForValue().set(AuthServerConstant.SMS_CODE_CACHE_PREFIX + phone,
                redisStorage,10, TimeUnit.MINUTES);

        thirdPartFeignService.sendCode(phone, codeNum);

        return R.ok();
    }
}

```

![image-20211129225450927](https://i-blog.csdnimg.cn/blog_migrate/0f6848a78806f4f9ed902612ed42cc09.png)

> 在60秒之内再次发送该号码的验证码

![image-20211129225750892](https://i-blog.csdnimg.cn/blog_migrate/16576c0e88c67c0e0b747fb6256178c0.png)

## 4\. 注册页面相关功能实现

### 4.1 准备

#### 4.1.1 抽取注册模型类 

```java
package site.xx.gulimall.auth.vo;
@Data
public class UserRegisterVo {

    @NotEmpty(message = "用户名必须提交")
    @Length(min = 6, max = 19, message="用户名长度必须是6-18字符")
    private String userName;

    @NotEmpty(message = "密码必须填写")
    @Length(min = 6,max = 18,message = "密码长度必须是6—18位字符")
    private String password;

    @NotEmpty(message = "手机号必须填写")
    @Pattern(regexp = "^[1]([3-9])[0-9]{9}$", message = "手机号格式不正确")
    private String phone;

    @NotEmpty(message = "验证码必须填写")
    private String code;

}

```

#### 4.1.2 业务流程

注册的主体逻辑：

1.  若JSR303校验未通过，则通过`BindingResult`封装错误信息，并重定向至注册页面
2.  若通过JSR303校验，则需要从**`redis`**中取值**判断验证码是否正确**，正确的话通过会员模块的feign注册(检查验证码、用户名、手机号 唯一),校验通过后,**调用会员服务添加会员信息**
3.  会员服务调用成功则重定向至登录页，否则封装远程服务返回的错误信息返回至注册页面

#### 4.1.3 controller参数注解@Valid 

> **注：** `RedirectAttributes`可以通过session保存信息并在重定向的时候携带过去。这里用于**存错误消息**

 LoginController注册方法校验：

```java

//BindingResult参数获取校验结果
//RedirectAttributes可以通过session保存信息并在重定向的时候携带过去。这里用于存错误消息
    @PostMapping(value = "/register")
    public String register(@Valid UserRegisterVo vos, BindingResult result,
                           RedirectAttributes attributes) {

        //如果有错误回到注册页面
        if (result.hasErrors()) {
            Map<String, String> errors = result.getFieldErrors().stream().collect(
                    Collectors.toMap(FieldError::getField, FieldError::getDefaultMessage));
//            flash是一闪而过，此数据只取一次
            attributes.addFlashAttribute("errors",errors);

            //效验出错，重定向到注册页面。不用转发是为了防止刷新时重复提交表单
            // 不用return reg是因为本来就在注册页面点击发送了这个注册请求，要重定向清空表单
            return "redirect:http://auth.gulimall.com/reg.html";
        }

        //1、效验验证码
        return null
    }
```

### 4.2 【会员模块】存储会员信息

#### 4.2.1 抽取模型类，接收用户信息

```java
package site.xx.gulimall.member.vo;
/**
 * 会员注册Vo
 */
@Data
public class MemberUserRegisterVo {
    private String userName;
    private String password;
    private String phone;
}

```

#### 4.2.2 自定义“用户名与手机号重复”的异常类

```java
package site.xx.gulimall.member.exception;

public class PhoneException extends RuntimeException {
    public PhoneException() {
        super("存在相同的手机号");
    }
}

```

```java
package site.xx.gulimall.member.exception;

public class UsernameException extends RuntimeException {
    public UsernameException() {
        super("存在相同的用户名");
    }
}

```

#### 4.2.3 注册controller实现

**业务流程：** 

1.  通过异常机制判断当前注册会员名和电话号码**是否已经注册**
2.  如果已经注册，则抛出对应的**自定义异常**，并在返回时封装对应的错误信息
3.  如果没有注册，则封装传递过来的会员信息，并**设置默认的会员等级、创建时间**

member/controller/**MemberController**.java 

```java
    @PostMapping(value = "/register")
    public R register(@RequestBody MemberUserRegisterVo vo) {
        try {
            memberService.register(vo);
            //异常机制：通过捕获对应的自定义异常判断出现何种错误并封装错误信息
        } catch (PhoneException e) {
            return R.error(BizCodeEnume.PHONE_EXIST_EXCEPTION.getCode(),BizCodeEnume.PHONE_EXIST_EXCEPTION.getMsg());
        } catch (UsernameException e) {
            return R.error(BizCodeEnume.USER_EXIST_EXCEPTION.getCode(),BizCodeEnume.USER_EXIST_EXCEPTION.getMsg());
        }
        return R.ok();
    }
```

#### 4.2.4 使用BCrypt实现密码加密解密

> **MD5**
> 
> -   Message Digest algorithm 5，**信息摘要算法**
> -   压缩性：任意长度的数据，算出的**MD5值长度都是固定**的。
> -   容易计算：从原数据计算出MD5值很容易。
> -   抗修改性：对原数据进行任何改动，哪怕只修改1个字节，所得到的MD5值都有很大区别。
> -   **强抗碰撞：**想找到两个不同的数据，使它们具有相同的MD5值，是非常困难的。可以用md5值对比两个文件是否相同。
> -   不可逆，但因为抗修改性和抗碰撞，所以可以**暴力破解**，不能直接用md5加密密码。
> 
> **加盐**
> 
> -   通过生成**随机数**与MD5生成字符串进行组合
> -   数据库同时存储MD5值与salt值。验证正确性时使用salt进行MD5即可

**BCrypt加密：** 一种加盐的单向Hash，不可逆的加密算法，同一种明文（plaintext），每次加密后的密文都不一样，而且不可反向破解生成明文，破解难度很大。 

和其他加密方式相比，BCryptPasswordEncoder有着它自己的优势所在，首先**加密的hash值每次都不同**，就像md5的盐值加密一样，只不过**盐值加密用到了随机数**，前者用到的是其内置的算法规则，毕竟随机数没有设合适的话还是有一定几率被攻破的。其次BCryptPasswordEncoder的生成加密存储串也有60位之多。最重要的一点是，md5的加密不是spring security所推崇的加密方式了，所以我们还是要多了解点新的加密方式。

BCryptPasswordEncoder**每次加密相同的值,都会得到不同的密文**

BCryptPasswordEncoder加密(encode)解密(matches)

**加密encode**

```java
        BCryptPasswordEncoder bCryptPasswordEncoder = new BCryptPasswordEncoder();
//加密
        String encode = bCryptPasswordEncoder.encode("123456");
//测试匹配，第一个参数是原始密码，第二个参数是编码后的密码。尽管每次加密后的值都不同,但matches能够匹配
        boolean matches = bCryptPasswordEncoder.matches("123456",encode);    //true

```

#### 4.2.5 注册业务实现

> member/service/MemberService.java

```java
    /**
     * 用户注册
     * @param vo
     */
    void register(MemberUserRegisterVo vo);

    /**
     * 判断邮箱是否重复
     * @param phone
     * @return
     */
    void checkPhoneUnique(String phone) throws PhoneException;

    /**
     * 判断用户名是否重复
     * @param userName
     * @return
     */
    void checkUserNameUnique(String userName) throws UsernameException;
```

> member/service/impl/MemberServiceImpl.java

```java
    @Override
    public void register(MemberUserRegisterVo vo) {
        MemberEntity memberEntity = new MemberEntity();

        //设置默认等级【普通会员】
        MemberLevelEntity levelEntity = memberLevelDao.getDefaultLevel();
        memberEntity.setLevelId(levelEntity.getId());

        //设置其它的默认信息
        //检查用户名和手机号是否唯一。感知异常，异常机制
        checkPhoneUnique(vo.getPhone());
        checkUserNameUnique(vo.getUserName());

        memberEntity.setNickname(vo.getUserName());
        memberEntity.setUsername(vo.getUserName());
        //密码进行MD5加密
        BCryptPasswordEncoder bCryptPasswordEncoder = new BCryptPasswordEncoder();
        String encode = bCryptPasswordEncoder.encode(vo.getPassword());
        memberEntity.setPassword(encode);
        memberEntity.setMobile(vo.getPhone());
        memberEntity.setGender(0);
        memberEntity.setCreateTime(new Date());

        //保存数据
        baseMapper.insert(memberEntity);
    }
//检查手机号是否已存在
    @Override
    public void checkPhoneUnique(String phone) throws PhoneException {
        Integer phoneCount = baseMapper.selectCount(new QueryWrapper<MemberEntity>().eq("mobile", phone));
        if (phoneCount > 0) {
            throw new PhoneException();
        }
    }
//检查用户名是否已存在
    @Override
    public void checkUserNameUnique(String userName) throws UsernameException {
        Integer usernameCount = baseMapper.selectCount(new QueryWrapper<MemberEntity>().eq("username", userName));
        if (usernameCount > 0) {
            throw new UsernameException();
        }
    }
```

### 4.3 【认证模块】注册业务实现

**业务流程**

1.  若JSR303校验未通过，则通过`BindingResult`封装错误信息，并重定向至注册页面
2.  若通过JSR303校验，则需要从**`redis`**中取值**判断验证码是否正确**，正确的话通过会员模块的feign注册(检查验证码、用户名、手机号 唯一),校验通过后,**调用会员服务添加会员信息**
3.  会员服务调用成功则重定向至登录页，否则封装远程服务返回的错误信息返回至注册页面

**代码实现**

> feign接口
> 
> ```java
> package site.zhourui.gulimall.auth.feign;
> @FeignClient("gulimall-member")
> public interface MemberFeignService {
>     @PostMapping(value = "/member/member/register")
>     R register(@RequestBody UserRegisterVo vo);
> }
> 
> ```
> 
> 确保启动类注解了“发现客户端”和“开启feign ”

auth/controller/LoginController.java

```java
    /**
     *
     * TODO: 重定向携带数据：利用session原理，将数据放在session中。
     * TODO:只要跳转到下一个页面取出这个数据以后，session里面的数据就会删掉
     * TODO：分布下session问题
     * RedirectAttributes：重定向也可以保留数据，不会丢失。这里用于存错误消息
     * 用户注册
     * @return
     */
    @PostMapping(value = "/register")
    public String register(@Valid UserRegisterVo vos, BindingResult result, RedirectAttributes attributes) {

        //如果有错误回到注册页面
        if (result.hasErrors()) {
            Map<String, String> errors = result.getFieldErrors().stream().collect(Collectors.toMap(FieldError::getField, FieldError::getDefaultMessage));
            attributes.addFlashAttribute("errors", errors);

            //效验出错回到注册页面
            return "redirect:http://auth.gulimall.com/reg.html";
            // 1、return "reg"; 请求转发【使用Model共享数据】【异常：，405 POST not support】
            // 2、"redirect:http:/reg.html"重定向【使用RedirectAttributes共享数据】【bug：会以ip+port来重定向】
            // 3、redirect:http://auth.gulimall.com/reg.html重定向【使用RedirectAttributes共享数据】
        }

        //1、效验验证码
        String code = vos.getCode();

        //获取存入Redis里的验证码
        String redisCode = stringRedisTemplate.opsForValue().get(AuthServerConstant.SMS_CODE_CACHE_PREFIX + vos.getPhone());
        if (!StringUtils.isEmpty(redisCode)) {
            // 判断验证码是否正确【有BUG，如果字符串存储有问题，没有解析出code，数据为空，导致验证码永远错误】
            if (code.equals(redisCode.split("_")[0])) {
                //删除验证码（不可重复使用）;令牌机制
                stringRedisTemplate.delete(AuthServerConstant.SMS_CODE_CACHE_PREFIX+vos.getPhone());
                //验证码通过，真正注册，调用远程服务进行注册【会员服务】
                R register = memberFeignService.register(vos);
                if (register.getCode() == 0) {
                    //成功，重定向到登录页面
                    return "redirect:http://auth.gulimall.com/login.html";
                } else {
                    //失败
                    Map<String, String> errors = new HashMap<>();
                    errors.put("msg", register.getData("msg",new TypeReference<String>(){}));
                    attributes.addFlashAttribute("errors",errors);
                    return "redirect:http://auth.gulimall.com/reg.html";
                }
            } else {
                //验证码错误
                Map<String, String> errors = new HashMap<>();
                errors.put("code","验证码错误");
                attributes.addFlashAttribute("errors",errors);
                return "redirect:http://auth.gulimall.com/reg.html";
            }
        } else {
            // redis中验证码过期
            Map<String, String> errors = new HashMap<>();
            errors.put("code","验证码过期");
            attributes.addFlashAttribute("errors",errors);
            return "redirect:http://auth.gulimall.com/reg.html";
        }
    }
```