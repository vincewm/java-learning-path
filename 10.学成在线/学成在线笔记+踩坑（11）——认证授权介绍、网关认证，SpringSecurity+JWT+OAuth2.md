>  **导航：**
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?spm=1001.2014.3001.5501)

[TOC]



# **1 【认证****模块】需求分析**

## **1.1** **什么是认证授权**

> 截至目前，项目已经完成了课程发布功能，课程发布后用户通过在线学习页面点播视频进行学习。如何去记录学生的学习过程呢？要想掌握学生的学习情况就需要知道用户的身份信息，记录哪个用户**在什么时间学习什么课程**，如果用户要购买课程也需要知道用户的身份信息。所以，去管理学生的学习过程最基本的要实现用户的身份认证。

认证授权模块实现平台所有用户的身份认证与用户授权功能。

**什么是用户身份认证？**

​    用户身份认证即用户去访问系统资源时系统要求**验证用户的身份信息**，身份合法方可继续访问。常见的用户身份认证的表现形式有：用户名密码登录，微信扫码等方式。

项目包括学生、学习机构的老师、平台运营人员三类用户，不管哪一类用户在访问项目受保护资源时都需要进行身份认证。比如：发布课程操作，需要学习机构的老师首先登录系统成功，然后再执行发布课程操作。创建订单，需要学生用户首先登录系统，才可以创建订单。如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/a4d4cffd1d034cf888168d87e00db977.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**什么是用户授权？**

​    用户认证通过后去访问系统的资源，系统会**判断用户是否拥有访问资源的权限**，只允许访问有权限的系统资源，没有权限的资源将无法访问，这个过程叫用户授权。比如：用户去发布课程，系统首先进行用户身份认证，认证通过后继续判断用户是否有发布课程的权限，如果没有权限则拒绝继续访问系统，如果有权限则继续发布课程。如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/f6c085672ce0452ba03d4645bd4d7595.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## **1.2** **业务流程**

### **1.2.1** **统一认证**

项目包括学生、学习机构的老师、平台运营人员三类用户，三类用户将使用**统一的认证入口**，如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/d0518208e9974af389a4aa46c37c2008.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

用户输入账号和密码提交认证，认证通过则继续操作。

项目由统一认证服务受理用户的认证请求，如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/8b07e2a1e6a9485c9b143108699e1268.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**认证通过**由认证服务向给用户**颁发令牌**，相当于访问系统的通行证，用户拿着令牌去访问系统的资源。

### **1.2.2** SSO**单点登录**

本项目基于微服务架构构建，微服务包括：内容管理服务、媒资管理服务、学习中心服务、系统管理服务等，为了提高用户体验性，用户只需要认证一次便可以在多个拥有访问权限的系统中访问，这个功能叫做单点登录。

单点登录（Single Sign On），简称为 SSO，是目前比较流行的企业业务整合的解决方案之一。SSO的定义是在多个应用系统中，用户只需要登录一次就可以访问所有相互信任的应用系统。

如下图，**用户只需要认证一次，便可以在多个拥有访问权限的系统中访问：**

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/4c67d92deb4e40389ec5c33794eff142.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **1.2.3** **第三方认证**

为了提高用户体验，很多网站有扫码登录的功能，如：微信扫码登录、QQ扫码登录等。扫码登录的好处是用户不用输入账号和密码，操作简便，另外一个好处就是有利于用户信息的共享，互联网的优势就是资源共享，用户也是一种资源，对于一个新网站如果让用户去注册是很困难的，如果提供了微信扫码登录将省去用户注册的成本，是一种非常有效的推广手段。

微信扫码登录其中的原理正是使用了第三方认证，如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/0a7c18c3fd7b4fe4955f81f60ec1ff6a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# **2 Spring Security认证授权框架**

## **2.1 Spring Security****介绍**

认证功能几乎是每个项目都要具备的功能，并且它与业务无关，市面上有很多认证框架，如：Apache Shiro、CAS、Spring Security等。由于本项目基于Spring Cloud技术构建，Spring Security是spring家族的一份子且和Spring Cloud集成的很好，所以**本项目选用Spring Security作为认证服务的技术框架。**

Spring Security 是一个功能强大且高度可定制的**身份验证和访问控制框架**，它是一个专注于为 Java 应用程序提供身份验证和授权的框架。

Spring Security项目主页：https://spring.io/projects/spring-security

Spring cloud Security： https://spring.io/projects/spring-cloud-security

## **2.2** **认证授权入门**

### **2.2.1** **初始化认证模块，LoginController**

下边我们使用Spring Security框架快速构建认证授权功能体系。

**1、部署认证服务工程**

创建xuecheng-plus-auth工程

此工程是一个普通的spring boot工程，可以连接数据库。

此工程**不具备认证授权的功能**。

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/e0b60c7b7fa74c9baa2e1b59e52aea52.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2、创建数据库**

创建xc_users数据库

导入课程资料中的xcplus_users.sql脚本。

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/907facc8c6b945bc9fc784a99fb80ca4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**配置** 

在nacos中新增auth-service-dev.yaml：

```bash
server:
  servlet:
    context-path: /auth
  port: 63070
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://192.168.101.65:3306/xc1010_users?serverTimezone=UTC&userUnicode=true&useSSL=false&
    username: root
    password: mysql
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

bootstrap.yml：



```bash
spring:
  application:
    name: auth-service
  cloud:
    nacos:
      server-addr: 192.168.101.65:8848
      discovery:
        namespace: dev402
        group: xuecheng-plus-project
      config:
        namespace: dev402
        group: xuecheng-plus-project
        file-extension: yaml
        refresh-enabled: true
        shared-configs:
          - data-id: swagger-${spring.profiles.active}.yaml
            group: xuecheng-plus-common
            refresh: true
          - data-id: logging-${spring.profiles.active}.yaml
            group: xuecheng-plus-common
            refresh: true
          - data-id: feign-${spring.profiles.active}.yaml
            group: xuecheng-plus-common
            refresh: true

  profiles:
    active: dev
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**登录的controller初始内容**

初始工程自带了一个Controller类，如下：

```java
package com.xuecheng.auth.controller;


/**
 * @author Mr.M
 * @version 1.0
 * @description 测试controller
 * @date 2022/9/27 17:25
 */
@Slf4j
@RestController
public class LoginController {

  @Autowired
  XcUserMapper userMapper;

  @RequestMapping("/login-success")
  public String loginSuccess(){

      return "登录成功";
  }


  @RequestMapping("/user/{id}")
  public XcUser getuser(@PathVariable("id") String id){
    XcUser xcUser = userMapper.selectById(id);
    return xcUser;
  }
//先不添加授权，用于测试
  @RequestMapping("/r/r1")
  public String r1(){
    return "访问r1资源";
  }
//    @RequestMapping("/r/r1")
//    @PreAuthorize("hasAuthority('p1')")//拥有p1权限方可访问
//    public String r1() {
//        return "访问r1资源";
//    }
  @RequestMapping("/r/r2")
  public String r2(){
    return "访问r2资源";
  }



}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动工程，尝试访问http://localhost:63070/auth/r/r1 :

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/278cf8dd6b684ac887c500c59f883e76.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

访问用户信息：http://localhost:63070/auth/user/52

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/35a189aff8b344f48226d001536e9f57.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

以上测试一切正常说明此工程部署成功。

> 因为还没有导入SpringSecurity，所以可以直接访问页面，不会被认证
>
> ```XML
> <dependency>
>     <groupId>org.springframework.cloud</groupId>
>     <artifactId>spring-cloud-starter-security</artifactId>
> </dependency>
> <dependency>
>     <groupId>org.springframework.cloud</groupId>
>     <artifactId>spring-cloud-starter-oauth2</artifactId>
> </dependency>
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **2.2.2** **认证测试，导依赖、安全管理配置类**

**1.导入依赖** 

下边向auth认证工程集成Spring security，向pom.xml加入Spring Security所需要的依赖

```XML
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-oauth2</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

重启工程，访问http://localhost:63070/auth/r/r1

自动进入/login登录页面，**/login是spring security提供的**，不用你再开发,此页面有几个css样式加载会稍微慢点，如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/0e8e437f44674981a1a3e70a8c6ccc8b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 用户表：
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/30d5a37e1f1a419ba0c5e8015c4ea8f2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

账号和密码是多少呢？下一步需要进行安全配置。

**2.创建****安全管理配置类**

WebSecurityConfig.java到config下：

需要三部分内容：

1、用户信息

在内存配置两个用户：zhangsan、lisi

zhangsan用户拥有的权限为p1

lisi用户拥有的权限为p2

2、密码方式

暂时采用明文方式

3、安全拦截机制

/r/**开头的请求需要认证

登录成功到成功页面

代码如下：

>  暂时采用明文方式，仅做测试

```java
/**
 * @author Mr.M
 * @version 1.0
 * @description 安全管理配置
 * @date 2022/9/26 20:53
 */
@EnableWebSecurity
@EnableGlobalMethodSecurity(securedEnabled = true,prePostEnabled = true)
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
//配置用户信息服务
@Bean
public UserDetailsService userDetailsService() {
    //这里配置用户信息,这里暂时使用这种方式将用户存储在内存中
    InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
            manager.createUser(User.withUsername("zhangsan").password("123").authorities("p1").build());
    manager.createUser(User.withUsername("lisi").password("456").authorities("p2").build());
    return manager;
}

    @Bean
    public PasswordEncoder passwordEncoder() {
        //密码为明文方式
        return NoOpPasswordEncoder.getInstance();
    }

    //配置安全拦截机制
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .antMatchers("/r/**").authenticated()//访问/r开始的请求需要认证通过
                .anyRequest().permitAll()//其它请求全部放行
                .and()
                .formLogin().successForwardUrl("/login-success");//登录成功跳转到/login-success
                http.logout().logoutUrl("/logout");//退出地址
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3.重启工程，测试**

0、登录：访问http://localhost:63070/login 登录“zhangsan”和"123"

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/997af8c7a4854d7d8bbb92bf472c2a15.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/649e320666c44240bf11cd74da2d3921.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



1、访问用户：访问http://localhost:63070/auth/user/52 可以正常访问id为52的用户

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/1d8014bfd58240759054cab649cabc4d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



2、认证测试：访问http://localhost:63070/auth/r/r1 显示登录页面

账号zhangsan，密码为123，如果输入的密码不正确会认证失败，输入正确显示登录成功。

> 为什么/auth/user/52 可以正常访问，访问/auth/r/r1 显示登录页面？
>
> 因为里登录controller里配置了退出页面“http.logout().logoutUrl("/logout");”，认证成功后访问/logout可退出登录。
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/c4e423e36c3542c3a4778fd87ba1f626.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **2.2.3** **授权测试，配置权限**

用户认证通过去访问系统资源时spring security进行授权控制，判断用户是否有该资源的访问权限，如果有则继续访问，如果没有则拒绝访问。

下边测试授权功能：

**1、安全管理配置类，配置用户所有权限。**

在WebSecurityConfig类配置zhangsan拥有p1权限，lisi拥有p2权限。

```java
    @Bean
    public UserDetailsService userDetailsService() {
        //这里配置用户信息,这里暂时使用这种方式将用户存储在内存中
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
        manager.createUser(User.withUsername("zhangsan").password("123").authorities("p1").build());
        manager.createUser(User.withUsername("lisi").password("456").authorities("p2").build());
        return manager;
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2、LoginController，指定资源与权限的关系。**

什么是系统的资源？

比如：查询一个用户的信息，用户信息就是系统的资源，要访问资源需要通过URL，所以我们在controller中定义的每个http的接口就是访问资源的接口。

下边在controller中配置/r/r1需要p1权限，/r/r2需要p2权限。

hasAuthority('p1')表示拥有p1权限方可访问。

代码如下：

```java
@RestController
public class LoginController {
    ....
    @RequestMapping("/r/r1")
    @PreAuthorize("hasAuthority('p1')")//拥有p1权限方可访问
    public String r1(){
      return "访问r1资源";
    }
   
    @RequestMapping("/r/r2")
    @PreAuthorize("hasAuthority('p2')")//拥有p2权限方可访问
    public String r2(){
      return "访问r2资源";
    }
    ...
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3、现在重启工程。**

当访问以/r/开头的url时会判断用户是否认证，如果没有认证则跳转到登录页面，如果已经认证则判断用户是否具有该URL的访问权限，如果具有该URL的访问权限则继续，否则拒绝访问。

例如：

访问/r/r1，自动跳转登录页面，使用zhangsan登录可以正常访问，因为在/r/r1的方法上指定了权限p1，zhangsan用户拥有权限p1,所以可以正常访问。

访问/r/r1，使用lisi登录则拒绝访问，由于lisi用户不具有权限p1需要拒绝访问



> 注意：如果访问上不加@PreAuthorize，此方法没有授权控制。
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/d86eeb5dbc6c4eebb94b4af0e5fc2040.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 张三李四对应授权： 
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/a976399273364cf087dabc043594e24c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

整理授权的过程见下图所示：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/22cfce95b5844db4bda6d6c561360492.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **2.2.4** **Spring Security****原理和工作流程**



**Spring Security**所解决的问题就是**安全访问控制**，而安全访问控制功能其实就是对所有进入系统的请求进行**拦截**，**校验每个请求是否能够访问它所期望的资源**。根据前边知识的学习，可以通过Filter或AOP等技术来实现，Spring Security对Web资源的保护是**靠过滤器Filter实现**的，所以从这个Filter来入手，逐步深入Spring Security原理。

​    当初始化Spring Security时，会创建一个名为SpringSecurityFilterChain的Servlet过滤器，类型为 org.springframework.security.web.FilterChainProxy，它实现了javax.servlet.Filter，因此外部的请求会经过此类，下图是Spring Security过虑器链结构图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/7331072bc18942a5b4d40bc8994d5bc5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

FilterChainProxy是一个代理，真正起作用的是FilterChainProxy中SecurityFilterChain所包含的各个Filter，同时这些Filter作为Bean被Spring管理，它们是Spring Security核心，各有各的职责，但他们并不直接处理用户的**认证**，也不直接处理用户的**授权**，而是把它们交给了认证管理器（AuthenticationManager）和决策管理器（AccessDecisionManager）进行处理。

spring Security功能的实现主要是由一系列过滤器链相互配合完成。

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/f15542383c864224a6db8f1151b1008a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

下面介绍过滤器链中主要的几个过滤器及其作用：

**SecurityContextPersistenceFilter** 这个Filter是整个拦截过程的入口和出口（也就是第一个和最后一个拦截器），会在请求开始时从配置好的 SecurityContextRepository 中获取 SecurityContext，然后把它设置给 SecurityContextHolder。在请求完成后将 SecurityContextHolder 持有的 SecurityContext 再保存到配置好的 SecurityContextRepository，同时清除 securityContextHolder 所持有的 SecurityContext；

**UsernamePasswordAuthenticationFilter** 用于处理来自表单提交的认证。该表单必须提供对应的用户名和密码，其内部还有登录成功或失败后进行处理的 AuthenticationSuccessHandler 和 AuthenticationFailureHandler，这些都可以根据需求做相关改变；

**FilterSecurityInterceptor** 是用于保护web资源的，使用AccessDecisionManager对当前用户进行授权访问，前面已经详细介绍过了；

**ExceptionTranslationFilter** 能够捕获来自 FilterChain 所有的异常，并进行处理。但是它只会处理两类异常：AuthenticationException 和 AccessDeniedException，其它的异常它会继续抛出。



Spring Security的执行流程如下：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/eb893588ec8d44c5a1548fa2db58b42c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

1. 用户提交用户名、密码被SecurityFilterChain中的**用户名密码过滤器**UsernamePasswordAuthenticationFilter获取到，封装为**请求Authentication**，通常情况下是UsernamePasswordAuthenticationToken这个实现类。
2. 然后过滤器将Authentication提交至**认证管理器**（AuthenticationManager）进行认证
3. 认证成功后，AuthenticationManager身份管理器通过DaoAuthentication Provider查询返回一个被填充满了信息的（包括上面提到的权限信息，身份信息，细节信息，但密码通常会被移除）Authentication实例。
4. **安全上下文容器**SecurityContextHolder将第3步填充了信息的Authentication，通过SecurityContextHolder.getContext().setAuthentication(…)方法，**将****Authentication保存到安全上下文。**
5. 可以看出AuthenticationManager接口（认证管理器）是认证相关的核心接口，也是发起认证的出发点，它的实现类为ProviderManager。而Spring Security支持多种认证方式，因此ProviderManager维护着一个List<AuthenticationProvider>列表，存放多种认证方式，最终实际的认证工作是由AuthenticationProvider完成的。咱们知道web表单的对应的AuthenticationProvider实现类为DaoAuthenticationProvider，它的内部又维护着一个UserDetailsService负责UserDetails的获取。最终AuthenticationProvider将UserDetails填充至Authentication。





## **2.3** **OAuth2认证协议**

### **2.3.1** **微信扫码****认证登录****流程**

微信扫码认证是一种第三方认证的方式，基于OAuth2协议实现.

OAUTH协议为用户资源的授权提供了一个安全的、开放而又简易的**标准**。同时，**任何第三方都可以使用OAUTH认证服务**，任何服务提供商都可以实现自身的OAUTH认证服务，因而OAUTH是开放的。

业界提供了OAUTH的多种实现如PHP、JavaScript，Java，Ruby等各种语言开发包，大大节约了程序员的时间，因而OAUTH是简易的。互联网很多服务如Open API，很多大公司如Google，Yahoo，Microsoft等都提供了OAUTH认证服务，这些都足以说明OAUTH标准逐渐成为开放资源授权的标准。

> Oauth协议目前发展到2.0版本，1.0版本过于复杂，2.0版本已得到广泛应用。
>
> 参考：[oAuth_百度百科](https://baike.baidu.com/item/oAuth/7153134?fr=aladdin)
>
> Oauth协议：[RFC 6749: The OAuth 2.0 Authorization Framework](https://tools.ietf.org/html/rfc6749)

**微信认证扫码登录的过程：** 

下边分析一个Oauth2认证的例子，黑马程序员网站使用微信认证扫码登录的过程：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/c881a936756144afae457cca0011cdf4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**1、用户点击微信扫码**

用户进入黑马程序的登录页面，点击微信的图标开打微信扫码界面。



![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/9afbabd53aba4ea2a5125faa4685aab2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

弹出二维码。



微信扫码的目的是通过微信认证登录黑马程序员官网，黑马程序员网站需要从微信获取当前用户的身份信息才会让当前用户在黑马网站登录成功。

> 现在搞清楚几个概念：
>
> **资源：**用户信息，在微信中存储。
>
> **资源拥有者：**用户是用户信息资源的拥有者。
>
> **认证服务：**微信负责认证当前用户的身份，负责为客户端颁发令牌。
>
> **客户端：**客户端会携带令牌请求微信获取用户信息，黑马程序员网站即客户端，黑马网站需要在浏览器打开。

**2、用户授权黑马网站访问用户信息**

资源拥有者扫描二维码表示资源拥有者请求微信进行认证，微信认证通过向用户手机返回授权页面，如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/accc7b0505a840c580d8c35e2ae5da4f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

询问用户是否授权黑马程序员访问自己在微信的用户信息，用户点击“确认登录”表示同意授权，微信认证服务器会颁发一个授权码给黑马程序员的网站。

只有资源拥有者同意微信才允许黑马网站访问资源。

**3、黑马程序员的网站获取到授权码**

4、携带授权码请求微信认证服务器申请令牌

此交互过程用户看不到。

5、微信认证服务器向黑马程序员的网站响应令牌

此交互过程用户看不到。

6、黑马程序员网站携带令牌请求微信资源服务器获取资源即用户信息。

7、资源服务器返回受保护资源即用户信息

8、黑马网站接收到用户信息，此时用户在黑马网站登录成功。

理解了微信扫码登录黑马网站的流程，接下来认识Oauth2.0的认证流程，如下：

引自Oauth2.0协议rfc6749 [RFC 6749: The OAuth 2.0 Authorization Framework](https://tools.ietf.org/html/rfc6749)

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/424c0f6541694adfae7b76314e6de6e1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**Oauth2包括以下角色：**

1、客户端

本身不存储资源，需要通过资源拥有者的授权去请求资源服务器的资源，比如：手机客户端、浏览器等。

上边示例中黑马网站即为客户端，它需要通过浏览器打开。

**2、资源拥有者**

> 资源：用户信息

通常为用户，也可以是应用程序，即该资源的拥有者。

A表示 客户端请求资源拥有者授权。

B表示 资源拥有者授权客户端即黑马网站访问自己的用户信息。

**3、授权服务器**（也称认证服务器）

例如微信服务端。认证服务器对资源拥有者进行认证，还会对客户端进行认证并颁发令牌。

C 客户端即黑马网站携带授权码请求认证。

D认证通过颁发令牌。

**4、资源服务器**

如数据库。存储资源的服务器。

E表示客户端即黑马网站携带令牌请求资源服务器获取资源。

F表示资源服务器校验令牌通过后提供受保护资源。



### **2.3.2 OAuth2****在本项目的应用**

Oauth2是一个标准的**开放的授权协议**，应用程序可以根据自己的要求去使用Oauth2，本项目使用Oauth2实现如下目标：

1、学成在线访问第三方系统（如微信）的资源。

本项目要接入微信扫码登录所以本项目要使用OAuth2协议**访问微信中的用户信息**。

2、外部系统访问学成在线的资源 。

同样当第三方系统想要访问学成在线网站的资源也可以基于OAuth2协议。

3、学成在线前端（客户端） 访问学成在线微服务的资源。

本项目是前后端分离架构，**前端访问微服务资源**也可以基于OAuth2协议进行认证。



### **2.3.3 OAuth2****的四种授权模式**

Spring Security支持OAuth2认证，OAuth2提供**授权码模式、密码模式、简化模式、客户端模式**等四种授权模式，前边举的微信扫码登录的例子就是基于授权码模式，这四种模式中授权码模式和密码模式应用较多。

本节使用Spring Security演示授权码模式、密码模式，其余两种请自行查阅相关资料。

### **2.3.3.1** **授权码模式**

> 前边举的微信扫码登录的例子就是基于授权码模式。 

OAuth2的几个授权模式是根据不同的应用场景以不同的方式去**获取令牌**，最终目的是要获取认证服务颁发的令牌，最终**通过令牌去获取资源**。

授权码模式简单理解是**使用授权码去获取令牌**，要想获取令牌先要获取授权码，授权码的获取需要资源拥有者亲自授权同意才可以获取。

下图是授权码模式的交互图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/e92be61cdb154b0d811264eecca71ef4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

还以黑马网站微信扫码登录为例进行说明：

1、用户打开浏览器。

2、通过浏览器访问客户端即黑马网站。

3、用户通过浏览器向认证服务请求授权，请求授权时会携带客户端的URL，此URL为下发授权码的重定向地址。

4、认证服务向资源拥有者返回授权页面。

5、资源拥有者亲自授权同意。

6、通过浏览器向认证服务发送授权同意。

7、认证服务向客户端地址重定向并携带授权码。

8、客户端即黑马网站收到授权码。

9、客户端携带授权码向认证服务申请令牌。

10、认证服务向客户端颁发令牌。



### **2.3.3.2** **授权码模式测试**

要想测试授权模式首先要配置授权服务器即上图中的认证服务器，需要配置授权服务及令牌策略。

1、从课程资料中拷贝 **授权服务配置类AuthorizationServer.java、****令牌策略配置类****TokenConfig.java**到认证服务的config包下。

> **说明**：AuthorizationServer用 @EnableAuthorizationServer 注解标识并继承AuthorizationServerConfigurerAdapter来配置OAuth2.0 授权服务器。

```java
package com.xuecheng.auth.config;
*/
 @Configuration
 @EnableAuthorizationServer
 public class AuthorizationServer extends AuthorizationServerConfigurerAdapter {
 ...
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 父类AuthorizationServerConfigurerAdapter要求配置以下几个类：
>
> ```java
> public class AuthorizationServerConfigurerAdapter implements AuthorizationServerConfigurer {
>     public AuthorizationServerConfigurerAdapter() {}
>     public void configure(AuthorizationServerSecurityConfigurer security) throws Exception {}
>     public void configure(ClientDetailsServiceConfigurer clients) throws Exception {}
>     public void configure(AuthorizationServerEndpointsConfigurer endpoints) throws Exception {}
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> **1****）****ClientDetailsServiceConfigurer**：用来配置客户端详情服务（ClientDetailsService），
>
> 随便一个客户端都可以随便接入到它的认证服务吗？答案是否定的，服务提供商会给批准接入的客户端一个身份，用于接入时的凭据，有客户端标识和客户端秘钥，在这里配置批准接入的客户端的详细信息。
>
> **2****）****AuthorizationServerEndpointsConfigurer**：用来配置令牌（token）的访问端点和令牌服务(token services)。
>
> **3****）****AuthorizationServerSecurityConfigurer**：用来配置令牌端点的安全约束.





**2、TokenConfig为令牌策略配置类**

暂时先使用InMemoryTokenStore在内存存储令牌，令牌的有效期等信息配置如下：

```java
    //令牌管理服务
    @Bean(name="authorizationServerTokenServicesCustom")
    public AuthorizationServerTokenServices tokenService() {
        DefaultTokenServices service=new DefaultTokenServices();
        service.setSupportRefreshToken(true);//支持刷新令牌
        service.setTokenStore(tokenStore);//令牌存储策略
        service.setAccessTokenValiditySeconds(7200); // 令牌默认有效期2小时
        service.setRefreshTokenValiditySeconds(259200); // 刷新令牌默认有效期3天
        return service;
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3、配置认证管理bean

```java
@EnableWebSecurity
@EnableGlobalMethodSecurity(securedEnabled = true,prePostEnabled = true)
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Bean
    public AuthenticationManager authenticationManagerBean() throws Exception {
        return super.authenticationManagerBean();
    }
    ....
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



重启认证服务

**1、get请求获取授权码**

地址: http://localhost:63070/auth/oauth/authorize?client_id=XcWebApp&response_type=code&scope=all&redirect_uri=http://www.51xuecheng.cn

参数列表如下：

- client_id：客户端准入标识。

- response_type：授权码模式固定为code。

- scope：客户端权限。

- redirect_uri：跳转uri，当授权码申请成功后会跳转到此地址，并在后边带上code参数（授权码）。

输入账号zhangsan、密码123登录成功，输入/oauth/authorize?client_id=XcWebApp&response_type=code&scope=all&redirect_uri=http://www.51xuecheng.cn

显示授权页面

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/f8e5acf1182b466c88aa909b9c29a8eb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



授权“XcWebApp”访问自己的受保护资源?

选择同意。

**2、请求成功**，重定向至http://www.51xuecheng.cn/?code=授权码，比如：http://www.51xuecheng.cn/?code=Wqjb5H

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/915fb6b09556423cb50d1036243a56a2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**3、使用httpclient工具，发post请求申请令牌**

```bash
### 授权码模式
### 第一步申请授权码(浏览器请求)/oauth/authorize?client_id=c1&response_type=code&scope=all&redirect_uri=http://www.51xuecheng.cn
### 第二步申请令牌
POST {{auth_host}}/auth/oauth/token?client_id=XcWebApp&client_secret=XcWebApp&grant_type=authorization_code&code=CTvCrB&redirect_uri=http://www.51xuecheng.cn
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **参数列表如下**
>
> - client_id：客户端准入标识。
>
> - client_secret：客户端秘钥。
>
> - grant_type：授权类型，填写authorization_code，表示授权码模式
>
> - code：授权码，就是刚刚获取的授权码，注意：授权码只使用一次就无效了，需要重新申请。
>
> - redirect_uri：申请授权码时的跳转url，一定和申请授权码时用的redirect_uri一致。





申请令牌成功如下所示：

```bash
{
  "access_改成自己的token": "368b1ee7-a9ee-4e9a-aae6-0fcab243aad2",
  "token_type": "bearer",
  "refresh_token": "3d56e139-0ee6-4ace-8cbe-1311dfaa991f",
  "expires_in": 7199,
  "scope": "all"
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **说明：**
>
> 1、**access_token，访问令牌**，用于访问资源使用。
>
> 2、token_type，bearer是在RFC6750中定义的一种token类型，在携带令牌访问资源时需要在head中加入bearer 空格 令牌内容
>
> 3、refresh_token，当令牌快过期时使用刷新令牌可以再次生成令牌。
>
> 4、expires_in：过期时间（秒）
>
> 5、scope，令牌的权限范围，服务端可以根据令牌的权限范围去对令牌授权。



### **2.3.3.3** **密码模式**

密码模式相对授权码模式简单，授权码模式需要借助浏览器供用户亲自授权，密码模式不用借助浏览器，如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/85cb09366e034b03b38d64dabb14b09e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

1、资源拥有者提供账号和密码

2、客户端向认证服务**申请令牌**，**请求中携带账号和密码**

3、认证服务校验账号和密码正确**颁发令牌**。

开始测试：

1、POST请求获取令牌

/oauth/token?client_id=XcWebApp&client_secret=XcWebApp&grant_type=password&username=shangsan&password=123

> **参数列表如下：**
>
> - client_id：客户端准入标识。
>
> - client_secret：客户端秘钥。
>
> - grant_type：授权类型，填写password表示密码模式
>
> - username：资源拥有者用户名。
>
> - password：资源拥有者密码。

2、授权服务器将令牌（access_token）发送给client

使用httpclient进行测试

```bash
### 密码模式
POST {{auth_host}}/auth/oauth/token?client_id=XcWebApp&client_secret=XcWebApp&grant_type=password&username=zhangsan&password=123
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

返回示例：

```bash
{
  "access_t改成自己的oken": "368b1ee7-a9ee-4e9a-aae6-0fcab243aad2",
  "token_type": "bearer",
  "refresh_token": "3d56e139-0ee6-4ace-8cbe-1311dfaa991f",
  "expires_in": 6806,
  "scope": "all"
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

​    这种模式十分简单，但是却意味着**直接将用户敏感信息泄漏给了client**，因此这就说明这种模式只能用于client是我们自己开发的情况下。

### **2.3.3.4** **本项目的应用方式：授权码和密码**

通过演示授权码模式和密码模式，授权码模式适合客户端和认证服务非同一个系统的情况，所以本项目使用授权码模式完成微信扫码认证。本项目采用密码模式作为前端请求微服务的认证方式。



## **2.4 JWT**

### **2.4.1 普通令牌性能低的问题**

**普通令牌需要“资源服务远程调用认证服务”校验，性能较低。** 

客户端申请到令牌，接下来客户端携带令牌去访问资源，到资源服务器将会校验令牌的合法性。

资源服务器如何校验令牌的合法性？

我们以OAuth2的密码模式为例进行说明：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/11436beba6a34f1ba04c06aa6cd5b9c2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

从第4步开始说明：

1、客户端携带令牌访问资源服务获取资源。

2、资源服务远程请求认证服务校验令牌的合法性

3、如果令牌合法资源服务向客户端返回资源。

**这里存在一个问题：**

就是校验令牌需要远程请求认证服务，客户端的每次访问都会**远程校验**，**执行性能低**。

**资源服务****自己校验令牌** 

如果能够让资源服务自己校验令牌的合法性将省去远程请求认证服务的成本，提高了性能。如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/7801f98e791c416f9e7a3ff482a402c6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如何解决上边的问题，实现资源服务**自行校验令牌**。

令牌采用**JWT格式**即可解决上边的问题，用户认证通过后会得到一个JWT令牌，JWT令牌中已经包括了用户相关的信息，客户端只需要携带JWT访问资源服务，资源服务根据事先约定的算法自行完成令牌校验，无需每次都请求认证服务完成授权。



### **2.4.2** **JWT介绍，无状态认证、对称加密和非对称加密**



JSON Web Token（JWT）是一种使用**JSON格式传递数据的网络令牌技术**，它是一个开放的行业标准（RFC 7519），它定义了一种简洁的、自包含的协议格式，用于在通信双方传递json对象，传递的信息经过数字签名可以被验证和信任，它可以使用HMAC算法或使用RSA的公钥/私钥对来签名，防止内容篡改。官网：[JSON Web Tokens - jwt.io](https://jwt.io/)

使用JWT可以实现无状态认证。



> **有状态认证：**
>
> 服务端保存客户端信息。服务端每次请求不需要携带用户信息。
>
> 传统的基于**session的方式**是有状态认证，用户登录成功将用户的身份信息以**session方式存储在服务端**，这样加大了服务端的存储压力，并且这种方式不适合在分布式系统中应用。
>
> 如下图，当用户访问应用服务，每个应用服务都会去服务器查看session信息，如果session中没有该用户则说明用户没有登录，此时就会重新认证，而**解决**这个问题的方法是**Session复制、Session黏贴。**
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/23c6337c19804187917971516db7d942.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**无状态认证** 

*服务端不保存客户端信息。服务端每次请求都需要携带用户信息。* 

如果是基于令牌技术在分布式系统中实现认证则服务端**不用存储session**，可以**将用户身份信息存储在令牌中**，用户认证通过后认证服务颁发令牌给用户，用户**将令牌存储在客户端**，去访问应用服务时携带令牌去访问，服务端**从jwt解析出用户信息**。这个过程就是无状态认证。

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/eb8afc8b41f6450ba7418fd6f10537c9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> session：
>
> session因为保存在服务端，分布式环境下需要实现多机数据共享 session一般需要结合Cookie实现认证，所以需要浏览器支持cookie，因此**移动端无法使用session认证方案**

**JWT令牌的优点：**

1、jwt基于json，非常方便解析。

2、可以在令牌中自定义丰富的内容，易扩展。

3、通过非对称加密算法及数字签名技术，JWT防止篡改，**安全性高**。

4、资源服务使用JWT可**不依赖认证服务**即可完成**授权**。



**缺点：**

JWT令牌较长，占存储空间比较大。

> 下边是一个JWT令牌的示例：
>
> ```bash
> eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsicmVzMSJdLCJ1c2VyX25hbWUiOiJ6aGFuZ3NhbiIsInNjb3BlIjpbImFsbCJdLCJleHAiOjE2NjQyNTQ2NzIsImF1dGhvcml0aWVzIjpbInAxIl0sImp0aSI6Ijg4OTEyYjJkLTVkMDUtNGMxNC1iYmMzLWZkZTk5NzdmZWJjNiIsImNsaWVudF9pZCI6ImMxIn0.wkDBL7roLrvdBG2oGnXeoXq-zZRgE9IVV2nxd-ez_oA
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> JWT令牌由三部分组成，每部分中间使用点（.）分隔，比如：xxxxx.yyyyy.zzzzz
>
> **Header**    
>
>  头部包括令牌的类型（即JWT）及使用的哈希算法（如HMAC SHA256或RSA）
>
>  一个例子如下：
>
>  下边是Header部分的内容
>
> ```bash
>    {
>     "alg": "HS256",
>     "typ": "JWT"
>   }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
>  将上边的内容使用Base64Url编码，得到一个字符串就是JWT令牌的第一部分。
>
>  **Payload**
>
>  第二部分是负载，内容也是一个json对象，它是存放有效信息的地方，它可以存放jwt提供的信息字段，比如：iss（签发者）,exp（过期时间戳）, sub（面向的用户）等，也可自定义字段。
>
>  此部分不建议存放敏感信息，因为此部分可以解码还原原始内容。
>
>  最后将第二部分负载使用Base64Url编码，得到一个字符串就是JWT令牌的第二部分。
>
>  一个例子：
>
> ```java
>   {
>     "sub": "1234567890",
>     "name": "456",
>     "admin": true
>   }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
>  **Signature**
>
>  第三部分是**签名**，**此部分用于防止jwt内容被篡改**。
>
>  这个部分使用base64url将前两部分进行编码，编码后使用点（.）连接组成字符串，最后使用header中声明的签名算法进行签名。
>
>  一个例子：
>
> ```java
>   HMACSHA256(
>     base64UrlEncode(header) + "." +
>     base64UrlEncode(payload),
>     secret)
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> base64UrlEncode(header)：jwt令牌的第一部分。
>
> base64UrlEncode(payload)：jwt令牌的第二部分。
>
> secret：签名所使用的密钥。

**为什么JWT可以防止篡改？**

只要密钥不泄露，jwt就不会被篡改。 

JWT的第三部分使用**签名算法**对第一部分和第二部分的内容进行签名，常用的签名算法是 HS256，常见的还有md5,sha 等，签名算法需要**使用密钥进行签名**，**密钥不对外公开**，并且签名是不可逆的，如果第三方更改了内容那么服务器验证签名就会失败，要想保证验证签名正确必须保证内容、密钥与签名前一致。

**对称加密**

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/b86e762060f443b294ec34380fca5a45.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

从上图可以看出认证服务和资源服务使用**相同的密钥**，这叫**对称加密**，对称加密效率高，缺点是如果一旦密钥泄露可以伪造jwt令牌。

**非对称加密** 

JWT还可以使用非对称加密，**认证服务自己保留私钥**，将公钥下发给受信任的客户端、资源服务，**公钥和私钥是配对的**，成对的公钥和私钥才可以正常加密和解密，非对称加密**效率低**但相比对称加密非对称加密**更安全**一些。



### **2.4.3** jwt对比session



**认证流程**
 **基于session的认证流程**

用户在浏览器中输入用户名和密码，服务器通过密码校验后生成一个session并保存到数据库

服务器为用户生成一个sessionId，并将具有sesssionId的cookie放置在用户浏览器中，在后续的请求中都将带有这个cookie信息进行访问

服务器获取cookie，通过获取cookie中的sessionId查找数据库判断当前请求是否有效

**基于JWT的认证流程**

用户在浏览器中输入用户名和密码，服务器通过密码校验后生成一个token并保存到数据库

前端获取到token，存储到cookie或者local storage中，在后续的请求中都将带有这个token信息进行访问

服务器获取token值，通过查找数据库判断当前token是否有效

**优缺点**
 JWT保存在客户端，在分布式环境下不需要做额外工作。而session因为保存在服务端，分布式环境下需要实现多机数据共享 session一般需要结合Cookie实现认证，所以需要浏览器支持cookie，因此移动端无法使用session认证方案

**安全性**
 JWT的payload使用的是base64编码的，因此在JWT中不能存储敏感数据。而session的信息是存在服务端的，相对来说更安全

**性能**
 经过编码之后JWT将非常长，cookie的限制大小一般是4k，cookie很可能放不下，所以JWT一般放在local storage里面。并且用户在系统中的每一次http请求都会把JWT携带在Header里面，HTTP请求的Header可能比Body还要大。而sessionId只是很短的一个字符串，因此使用JWT的HTTP请求比使用session的开销大得多

**一次性**
 无状态是JWT的特点，但也导致了这个问题，JWT是一次性的。想修改里面的内容，就必须签发一个新的JWT。

**无法废弃**
 一旦签发一个JWT，在到期之前就会始终有效，无法中途废弃。若想废弃，一种常用的处理手段是结合redis

**续签**
 如果使用JWT做会话管理，传统的cookie续签方案一般都是框架自带的，session有效期30分钟，30分钟内如果有访问，有效期被刷新至30分钟。一样的道理，要改变JWT的有效时间，就要签发新的JWT。

最简单的一种方式是每次请求刷新JWT，即每个HTTP请求都返回一个新的JWT。这个方法不仅暴力不优雅，而且每次请求都要做JWT的加密解密，会带来性能问题。另一种方法是在redis中单独为每个JWT设置过期时间，每次访问时刷新JWT的过期时间

**选择JWT或session**
 JWT有很多缺点，但是在分布式环境下不需要像session一样额外实现多机数据共享，虽然seesion的多机数据共享可以通过粘性session、session共享、session复制、持久化session、terracoa实现seesion复制等多种成熟的方案来解决这个问题。但是JWT不需要额外的工作，使用JWT不香吗？并且JWT一次性的缺点可以结合redis进行弥补
 

### **2.4.4 修改令牌配置类，测试生成****JWT****令牌**

在认证服务中的**令牌配置类**，配置jwt令牌服务，即可实现生成jwt格式的令牌。

```java
package com.xuecheng.auth.config;

@Configuration
public class TokenConfig {

//定义密钥
    private String SIGNING_KEY = "mq123";

    @Autowired
    TokenStore tokenStore;

//    @Bean
//    public TokenStore tokenStore() {
//        //使用内存存储令牌（普通令牌）
//        return new InMemoryTokenStore();
//    }

    @Autowired
    private JwtAccessTokenConverter accessTokenConverter;

    @Bean
    public TokenStore tokenStore() {
        return new JwtTokenStore(accessTokenConverter());
    }

    @Bean
    public JwtAccessTokenConverter accessTokenConverter() {
        JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
        converter.setSigningKey(SIGNING_KEY);
        return converter;
    }

    //令牌管理服务
    @Bean(name="authorizationServerTokenServicesCustom")
    public AuthorizationServerTokenServices tokenService() {
        DefaultTokenServices service=new DefaultTokenServices();
        service.setSupportRefreshToken(true);//支持刷新令牌
        service.setTokenStore(tokenStore);//令牌存储策略

        TokenEnhancerChain tokenEnhancerChain = new TokenEnhancerChain();
        tokenEnhancerChain.setTokenEnhancers(Arrays.asList(accessTokenConverter));
        service.setTokenEnhancer(tokenEnhancerChain);

        service.setAccessTokenValiditySeconds(7200); // 令牌默认有效期2小时
        service.setRefreshTokenValiditySeconds(259200); // 刷新令牌默认有效期3天
        return service;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

重启认证服务。

**使用httpclient通过密码模式申请令牌**

```bash
### 密码模式
POST {{auth_host}}/oauth/token?client_id=XcWebApp&client_secret=XcWebApp&grant_type=password&username=zhangsan&password=123
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

生成jwt的示例如下：

```bash
{
  "access改成自己的_token": "eyJhbXxx.-9SKI-qUqKhKcs8Gb80Rascx-JxqsNZxxXoPo82d8SM",
  "token_type": "bearer",
  "refresh_token": "eyJhbXxx.eyJhdXxx.Wsw1JXxxx",
  "expires_in": 7199,
  "scope": "all",
  "jti": "e9d3d0fd-24cb-44c8-8c10-256b34f8dfcc"
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

1、access_token，生成的jwt令牌，用于访问资源使用。

2、token_type，bearer是在RFC6750中定义的一种token类型，在携带jwt访问资源时需要在head中加入bearer jwt令牌内容

3、refresh_token，当jwt令牌快过期时使用刷新令牌可以再次生成jwt令牌。

4、expires_in：过期时间（秒）

5、scope，令牌的权限范围，服务端可以根据令牌的权限范围去对令牌授权。

6、jti：令牌的唯一标识。

**校验jwt令牌**

我们可以通过SpringSecurity自带的check_token接口校验jwt令牌，只需要在路径中加上“/check_token” 

```bash
###校验jwt令牌
POST {{auth_host}}/oauth/check_token?token=eyJhbGciOXxx.qy46CXxx
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

解析的用户信息如下：

```bash
{
  "aud": [
    "res1"
  ],
  "user_name": "zhangsan",
  "scope": [
    "all"
  ],
  "active": true,
  "exp": 1664371780,
  "authorities": [
    "p1"
  ],
  "jti": "f0a3cdeb-399d-48f0-8804-eca638ad8857",
  "client_id": "c1"
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





### **2.4.5 【内容模块】导入认证的依赖和配置类**

拿到了jwt令牌下一步就要携带令牌去访问资源服务中的资源，本项目各个微服务就是资源服务，比如：内容管理服务，客户端申请到jwt令牌，携带jwt去内容管理服务查询课程信息，此时内容管理服务要对jwt进行校验，只有jwt合法才可以继续访问。如下图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/461494e73c7d49aba27ef5c3380b3dc8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

1、在**内容管理服务**的content-api工程中添加依赖

```XML
<!--认证相关-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-oauth2</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2、创建配置类

创建资源服务配置类ResouceServerConfig 和令牌配置类TokenConfig到**内容管理**的api工程的config包下。



```java
/**
 * @description 资源服务配置
 * @author Mr.M
 * @date 2022/10/18 16:33
 * @version 1.0
 */
 @Configuration
 @EnableResourceServer
 @EnableGlobalMethodSecurity(securedEnabled = true,prePostEnabled = true)
 public class ResouceServerConfig extends ResourceServerConfigurerAdapter {


  //资源服务标识
  public static final String RESOURCE_ID = "xuecheng-plus";

  @Autowired
  TokenStore tokenStore;

  @Override
  public void configure(ResourceServerSecurityConfigurer resources) {
   resources.resourceId(RESOURCE_ID)//资源 id
           .tokenStore(tokenStore)
           .stateless(true);
  }

 @Override
 public void configure(HttpSecurity http) throws Exception {
  http.csrf().disable()
          .authorizeRequests()
//需要认证的请求
//                .antMatchers("/r/**","/course/**").authenticated()//所有匹配的请求必须经过认证
          .anyRequest().permitAll()    //全部请求放行
  ;
 }

 }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```java
@Configuration
public class TokenConfig {

//对称加密，和认真模块的令牌配置类的密钥相同
    String SIGNING_KEY = "mq123";


//    @Bean
//    public TokenStore tokenStore() {
//        //使用内存存储令牌（普通令牌）
//        return new InMemoryTokenStore();
//    }

    @Autowired
    private JwtAccessTokenConverter accessTokenConverter;

    @Bean
    public TokenStore tokenStore() {
        return new JwtTokenStore(accessTokenConverter());
    }

    @Bean
    public JwtAccessTokenConverter accessTokenConverter() {
        JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
        converter.setSigningKey(SIGNING_KEY);
        return converter;
    }


}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **2.4.6 httpclient测试，携带令牌访问资源服务** 

**1. 暂时配置课程路径需要被认证**

先修改内容模块的，资源服务配置类ResouceServerConfig ，配置课程路径需要被认证：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/9effe22dfaae443788014be25c1b5740.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2.重启内容管理服务，使用httpclient测试：**

> 1、访问根据课程id查询课程接口
>
> ```bash
> ### 查询课程信息
> GET http://localhost:63040/content/course/2
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 返回：
>
> ```bash
> {
>   "error": "unauthorized",
>   "error_description": "Full authentication is required to access this resource"
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 从返回信息可知当前没有认证。

**3.下边携带JWT令牌访问接口：**

> **1、申请jwt令牌**
>
> 采用密码模式申请令牌。
>
> ```bash
> ### 密码模式
> POST {{auth_host}}/auth/oauth/token?client_id=XcWebApp&client_secret=XcWebApp&grant_type=password&username=zhangsan&password=123
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/e1af73ad2c6c4185ae56cf8d0981af62.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> 
>
> **2、携带jwt令牌访问资源服务地址**
>
> ```bash
> ### 携带token访问资源服务
> GET http://localhost:63040/content/course/2
> Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsicmVzMSJdLCJ1c2VyX25hbWUiOiJ6aGFuZ3NhbiIsInNjb3BlIjpbImFsbCJdLCJleHAiOjE2NjQzMzM0OTgsImF1dGhvcml0aWVzIjpbInAxIl0sImp0aSI6IjhhM2M2OTk1LWU1ZGEtNDQ1Yy05ZDAyLTEwNDFlYzk3NTkwOSIsImNsaWVudF9pZCI6ImMxIn0.73eNDxTX5ifttGCjwc7xrd-Sbp_mCfcIerI3lGetZto
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 在**请求头中添加Authorization**，内容为Bearer 令牌，Bearer用于通过oauth2.0协议访问资源。
>
> 如果携带jwt令牌且jwt正确则正常访问资源服务的内容。
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/2b0122640b784ab1ac6cd56293356a60.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> 
>
> 如果不正确则报令牌无效的错误：
>
> ```bash
> {
>   "error": "invalid_token",
>   "error_description": "Cannot convert access token to JSON"
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **2.4.7 代码测试，SecurityContextHolder类获取用户身份**

>  **暂时配置课程路径需要被认证**
>
> 先修改内容模块的，资源服务配置类ResouceServerConfig ，配置课程路径需要被认证：
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/9effe22dfaae443788014be25c1b5740.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

jwt令牌中记录了用户身份信息，当客户端携带jwt访问资源服务，资源服务验签通过后将前两部分的内容还原即可取出用户的身份信息，并将用户身份信息放在了SecurityContextHolder上下文，SecurityContext与当前线程进行绑定，方便获取用户身份。

还以**查询课程接口**为例，进入查询课程接口的代码中，添加获取用户身份的代码

```java
@ApiOperation("根据课程id查询课程基础信息")
@GetMapping("/course/{courseId}")
public CourseBaseInfoDto getCourseBaseById(@PathVariable("courseId") Long courseId){
    //取出当前用户身份。底层使用的ThreadLocal，把用户身份信息放到线程里
    Object principal = SecurityContextHolder.getContext().getAuthentication().getPrincipal();
    System.out.println(principal);
    return courseBaseInfoService.getCourseBaseInfo(courseId);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> 测试时需要注意：
>
> 1、首先在资源服务配置中指定安全拦截机制 /course/开头的请求需要认证，即请求/course/{courseId}接口需要**携带jwt令牌**且签证通过。
>
> 2、认证服务生成jwt令牌将用户身份信息写入令牌，目前还是将用户信息硬编码并暂放在内存中。
>
> 如下：
>
> ```java
> @Bean
> public UserDetailsService userDetailsService() {
>     //这里配置用户信息,这里暂时使用这种方式将用户存储在内存中
>     InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
>     manager.createUser(User.withUsername("zhangsan").password("123").authorities("p1").build());
>     manager.createUser(User.withUsername("lisi").password("456").authorities("p2").build());
>     return manager;
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 3、我们在使用密码模式生成jwt令牌时用的是zhangsan的信息，所以jwt令牌中存储了zhangsan的信息，那么在资源服务中应该取出zhangsan的信息才对。
>
> 清楚了以上内容，下边重启内容管理服务，跟踪取到的用户身份是否正确。



# **3** **网关认证**

> 回顾网关职责
>
> **认证：**网关作为微服务入口，需要校验用户是是否有请求资格，如果没有则进行拦截。
>
> 路由和负载均衡：一切请求都必须先经过gateway，但网关不处理业务，而是根据某种规则，把请求转发到某个微服务，这个过程叫做路由。当然路由的目标服务有多个时，还需要做负载均衡。
>
> 限流：当请求流量过高时，在网关中按照下流的微服务能够接受的速度来放行请求，避免服务压力过大。

## **3.1 认证流程** 

> 到目前为止，测试通过了认证服务颁发jwt令牌，客户端携带jwt访问资源服务，资源服务对jwt的合法性进行验证。如下图：
>
> ![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/6db0617a9375481299010e4a928bf17a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 仔细观察此图，遗漏了本项目架构中非常重要的组件：网关。

加上网关并完善后的认证流程图：

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/4d405f89112740b79e314630aa76e198.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

所有访问微服务的请求都要经过网关，在网关进行用户身份的认证可以将很多非法的请求拦截到微服务以外，这叫做网关认证。

**网关的职责：**

**1、网站白名单维护**

针对不用认证的URL全部放行。

**2、校验jwt的合法性。**

除了白名单剩下的就是需要认证的请求，网关需要验证jwt的合法性，jwt合法则说明用户身份合法，否则说明身份不合法则拒绝继续访问。



**网关不负责授权，只负责认证：**

网关不负责授权，对请求的授权操作在各个微服务进行，因为微服务最清楚用户有哪些权限访问哪些接口。



## **3.2 【网关模块】网关统一校验jwt和维护白名单**

下边实现网关认证的**网站白名单维护、校验jwt的合法性：**

1、在网关工程添加依赖

```XML
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-oauth2</artifactId>
</dependency>
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2、导入配置类到网关工程的config包下。

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/f52def79f8e749e495ee7a67e798af64.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



这几个配置类都是通用的：

```
GatewayAuthFilter
/**
 * @author Mr.M
 * @version 1.0
 * @description 网关认证过虑器
 * @date 2022/9/27 12:10
 */
@Component
@Slf4j
public class GatewayAuthFilter implements GlobalFilter, Ordered {


    //白名单
    private static List<String> whitelist = null;

    static {
        //加载白名单
        try (
                InputStream resourceAsStream = GatewayAuthFilter.class.getResourceAsStream("/security-whitelist.properties");
        ) {
            Properties properties = new Properties();
            properties.load(resourceAsStream);
            Set<String> strings = properties.stringPropertyNames();
            whitelist= new ArrayList<>(strings);

        } catch (Exception e) {
            log.error("加载/security-whitelist.properties出错:{}",e.getMessage());
            e.printStackTrace();
        }


    }

    @Autowired
    private TokenStore tokenStore;


    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        //请求的url
        String requestUrl = exchange.getRequest().getPath().value();
        AntPathMatcher pathMatcher = new AntPathMatcher();
        //白名单放行
        for (String url : whitelist) {
            if (pathMatcher.match(url, requestUrl)) {
                return chain.filter(exchange);
            }
        }

        //检查token是否存在
        String token = getToken(exchange);
        if (StringUtils.isBlank(token)) {
            return buildReturnMono("没有认证",exchange);
        }
        //判断是否是有效的token
        OAuth2AccessToken oAuth2AccessToken;
        try {
            oAuth2AccessToken = tokenStore.readAccessToken(token);

            boolean expired = oAuth2AccessToken.isExpired();
            if (expired) {
                return buildReturnMono("认证令牌已过期",exchange);
            }
            return chain.filter(exchange);
        } catch (InvalidTokenException e) {
            log.info("认证令牌无效: {}", token);
            return buildReturnMono("认证令牌无效",exchange);
        }

    }

    /**
     * 获取token
     */
    private String getToken(ServerWebExchange exchange) {
        String tokenStr = exchange.getRequest().getHeaders().getFirst("Authorization");
        if (StringUtils.isBlank(tokenStr)) {
            return null;
        }
        String token = tokenStr.split(" ")[1];
        if (StringUtils.isBlank(token)) {
            return null;
        }
        return token;
    }




    private Mono<Void> buildReturnMono(String error, ServerWebExchange exchange) {
        ServerHttpResponse response = exchange.getResponse();
        String jsonString = JSON.toJSONString(new RestErrorResponse(error));
        byte[] bits = jsonString.getBytes(StandardCharsets.UTF_8);
        DataBuffer buffer = response.bufferFactory().wrap(bits);
        response.setStatusCode(HttpStatus.UNAUTHORIZED);
        response.getHeaders().add("Content-Type", "application/json;charset=UTF-8");
        return response.writeWith(Mono.just(buffer));
    }


    @Override
    public int getOrder() {
        return 0;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```
SecurityConfig
 @EnableWebFluxSecurity
 @Configuration
 public class SecurityConfig {


  //安全拦截配置
  @Bean
  public SecurityWebFilterChain webFluxSecurityFilterChain(ServerHttpSecurity http) {

   return http.authorizeExchange()
           .pathMatchers("/**").permitAll()
           .anyExchange().authenticated()
           .and().csrf().disable().build();
  }


 }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```
TokenConfig
@Configuration
public class TokenConfig {

    String SIGNING_KEY = "mq123";


//    @Bean
//    public TokenStore tokenStore() {
//        //使用内存存储令牌（普通令牌）
//        return new InMemoryTokenStore();
//    }

    @Autowired
    private JwtAccessTokenConverter accessTokenConverter;

    @Bean
    public TokenStore tokenStore() {
        return new JwtTokenStore(accessTokenConverter());
    }

    @Bean
    public JwtAccessTokenConverter accessTokenConverter() {
        JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
        converter.setSigningKey(SIGNING_KEY);
        return converter;
    }


}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```
RestErrorResponse
/**
 * 错误响应参数包装
 */
public class RestErrorResponse implements Serializable {

    private String errMessage;

    public RestErrorResponse(String errMessage){
        this.errMessage= errMessage;
    }

    public String getErrMessage() {
        return errMessage;
    }

    public void setErrMessage(String errMessage) {
        this.errMessage = errMessage;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3、配置白名单文件**security-whitelist.properties

内容如下（持续补充）

```java
/auth/**=认证地址
/content/open/**=内容管理公开访问接口
/media/open/**=媒资管理公开访问接口
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**4、测试：**

重启网关工程，进行测试

1）申请令牌

2）通过网关访问资源服务

这里访问内容管理服务

```bash
### 通过网关访问资源服务
GET http://localhost:63010/content/course/2
Authorization: Bearer eyJXxx.eyJhdXxx.lOITXxx
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

当token正确时可以正常访问资源服务，token验证失败返回token无效：

```bash
{
  "errMessage": "认证令牌无效"
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**5、认证功能开发之前，暂时放行全部路径**

注意：网关鉴权功能调试通过后，由于目前还没有开发认证功能，前端请求网关的URL不在白名单中间时会“没有认证”的错误，**暂时在白名单中添加 全部放行配置**，待认证功能开发完成再屏蔽全部放行配置，

![img](学成在线笔记+踩坑（11）——认证授权介绍、网关认证，SpringSecurity+JWT+OAuth2.assets/2aa687fc0a4647408acceb47760141dc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**6、内容模块注释掉配置类里认证的路径**

由于是在网关处进行令牌校验，所以在微服务处不再校验令牌的合法性，修改内容管理服务的ResouceServerConfig类，屏蔽authenticated()。

```java
 @Override
 public void configure(HttpSecurity http) throws Exception {
  http.csrf().disable()
          .authorizeRequests()
//          .antMatchers("/r/**","/course/**").authenticated()//所有/r/**的请求必须认证通过
          .anyRequest().permitAll()
  ;
 }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)