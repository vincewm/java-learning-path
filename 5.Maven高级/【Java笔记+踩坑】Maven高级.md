>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[0，解除端口调用](#0%EF%BC%8C%E8%A7%A3%E9%99%A4%E7%AB%AF%E5%8F%A3%E8%B0%83%E7%94%A8)

[1，分模块开发](#1%EF%BC%8C%E5%88%86%E6%A8%A1%E5%9D%97%E5%BC%80%E5%8F%91)

[1.1 分模块开发设计](#1.1%20%E5%88%86%E6%A8%A1%E5%9D%97%E5%BC%80%E5%8F%91%E8%AE%BE%E8%AE%A1)

[1.2 分模块开发实现](#1.2%20%E5%88%86%E6%A8%A1%E5%9D%97%E5%BC%80%E5%8F%91%E5%AE%9E%E7%8E%B0)

[1.2.1 环境准备](#1.2.1%20%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)

[1.2.2 抽取domain层](#1.2.2%20%E6%8A%BD%E5%8F%96domain%E5%B1%82)

[1.2.3 抽取Dao层](#1.2.3%20%E6%8A%BD%E5%8F%96Dao%E5%B1%82)

[1.2.4 运行测试并总结](#1.2.4%20%E8%BF%90%E8%A1%8C%E6%B5%8B%E8%AF%95%E5%B9%B6%E6%80%BB%E7%BB%93)

[2，依赖管理](#2%EF%BC%8C%E4%BE%9D%E8%B5%96%E7%AE%A1%E7%90%86)

[2.1 依赖传递与冲突问题](#2.1%20%E4%BE%9D%E8%B5%96%E4%BC%A0%E9%80%92%E4%B8%8E%E5%86%B2%E7%AA%81%E9%97%AE%E9%A2%98)

[2.2 可选依赖和排除依赖](#2.2%20%E5%8F%AF%E9%80%89%E4%BE%9D%E8%B5%96%E5%92%8C%E6%8E%92%E9%99%A4%E4%BE%9D%E8%B5%96)

[方案一:可选依赖optional，对外隐藏](#%E6%96%B9%E6%A1%88%E4%B8%80%3A%E5%8F%AF%E9%80%89%E4%BE%9D%E8%B5%96)

[方案二:排除依赖exclusions，主动排除](#%E6%96%B9%E6%A1%88%E4%BA%8C%3A%E6%8E%92%E9%99%A4%E4%BE%9D%E8%B5%96)

[3，聚合和继承](#3%EF%BC%8C%E8%81%9A%E5%90%88%E5%92%8C%E7%BB%A7%E6%89%BF)

[3.1 聚合](#3.1%20%E8%81%9A%E5%90%88)

[3.1.1 概述](#3.1.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[3.1.2 具体实现](#3.1.2%20%E5%85%B7%E4%BD%93%E5%AE%9E%E7%8E%B0%C2%A0) 

[3.2 继承](#3.2%20%E7%BB%A7%E6%89%BF)

[3.3 聚合与继承的区别](#3.3%20%E8%81%9A%E5%90%88%E4%B8%8E%E7%BB%A7%E6%89%BF%E7%9A%84%E5%8C%BA%E5%88%AB)

[3.4 IDEA构建聚合与继承工程](#3.3.2%20IDEA%E6%9E%84%E5%BB%BA%E8%81%9A%E5%90%88%E4%B8%8E%E7%BB%A7%E6%89%BF%E5%B7%A5%E7%A8%8B)

[4，属性](#4%EF%BC%8C%E5%B1%9E%E6%80%A7)

[4.1 属性](#4.1%20%E5%B1%9E%E6%80%A7)

[4.1.1 问题分析](#4.1.1%20%E9%97%AE%E9%A2%98%E5%88%86%E6%9E%90)

[4.1.2 代码实现](#4.1.2%20%E8%A7%A3%E5%86%B3%E6%AD%A5%E9%AA%A4)

[4.2 配置文件加载属性](#4.2%20%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%8A%A0%E8%BD%BD%E5%B1%9E%E6%80%A7)

[4.3 版本管理](#4.3%20%E7%89%88%E6%9C%AC%E7%AE%A1%E7%90%86)

[5，多环境配置与应用](#5%EF%BC%8C%E5%A4%9A%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE%E4%B8%8E%E5%BA%94%E7%94%A8)

[5.1 多环境开发](#5.1%20%E5%A4%9A%E7%8E%AF%E5%A2%83%E5%BC%80%E5%8F%91)

[5.2 跳过测试](#5.2%20%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[方式一:IDEA工具实现跳过测试按钮](#%E6%96%B9%E5%BC%8F%E4%B8%80%3AIDEA%E5%B7%A5%E5%85%B7%E5%AE%9E%E7%8E%B0%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[方式二:配置插件实现跳过测试](#%E6%96%B9%E5%BC%8F%E4%BA%8C%3A%E9%85%8D%E7%BD%AE%E6%8F%92%E4%BB%B6%E5%AE%9E%E7%8E%B0%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[方式三:命令行跳过测试](#%E6%96%B9%E5%BC%8F%E4%B8%89%3A%E5%91%BD%E4%BB%A4%E8%A1%8C%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[6，私服](#6%EF%BC%8C%E7%A7%81%E6%9C%8D)

[6.1 私服简介](#6.1%20%E7%A7%81%E6%9C%8D%E7%AE%80%E4%BB%8B)

[6.2 私服安装](#6.2%20%E7%A7%81%E6%9C%8D%E5%AE%89%E8%A3%85)

[6.3 私服仓库分类](#6.3%20%E7%A7%81%E6%9C%8D%E4%BB%93%E5%BA%93%E5%88%86%E7%B1%BB)

[6.4 本地仓库访问私服配置](#6.4%20%E6%9C%AC%E5%9C%B0%E4%BB%93%E5%BA%93%E8%AE%BF%E9%97%AE%E7%A7%81%E6%9C%8D%E9%85%8D%E7%BD%AE)

[6.5 私服资源上传与下载](#6.5%20%E7%A7%81%E6%9C%8D%E8%B5%84%E6%BA%90%E4%B8%8A%E4%BC%A0%E4%B8%8E%E4%B8%8B%E8%BD%BD)

[步骤1:配置工程上传私服的具体位置](#%E6%AD%A5%E9%AA%A41%3A%E9%85%8D%E7%BD%AE%E5%B7%A5%E7%A8%8B%E4%B8%8A%E4%BC%A0%E7%A7%81%E6%9C%8D%E7%9A%84%E5%85%B7%E4%BD%93%E4%BD%8D%E7%BD%AE)

[步骤2:发布资源到私服](#%E6%AD%A5%E9%AA%A42%3A%E5%8F%91%E5%B8%83%E8%B5%84%E6%BA%90%E5%88%B0%E7%A7%81%E6%9C%8D)

--

 Maven基础：

[JavaWeb基础3——Maven&MyBatis\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/125818307?spm=1001.2014.3001.5501 "JavaWeb基础3——Maven&MyBatis_vincewm的博客-CSDN博客")

**目录**

[0，解除端口调用](#0%EF%BC%8C%E8%A7%A3%E9%99%A4%E7%AB%AF%E5%8F%A3%E8%B0%83%E7%94%A8)

[1，分模块开发](#1%EF%BC%8C%E5%88%86%E6%A8%A1%E5%9D%97%E5%BC%80%E5%8F%91)

[1.1 分模块开发设计](#1.1%20%E5%88%86%E6%A8%A1%E5%9D%97%E5%BC%80%E5%8F%91%E8%AE%BE%E8%AE%A1)

[1.2 分模块开发实现](#1.2%20%E5%88%86%E6%A8%A1%E5%9D%97%E5%BC%80%E5%8F%91%E5%AE%9E%E7%8E%B0)

[1.2.1 环境准备](#1.2.1%20%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)

[1.2.2 抽取domain层](#1.2.2%20%E6%8A%BD%E5%8F%96domain%E5%B1%82)

[1.2.3 抽取Dao层](#1.2.3%20%E6%8A%BD%E5%8F%96Dao%E5%B1%82)

[1.2.4 运行测试并总结](#1.2.4%20%E8%BF%90%E8%A1%8C%E6%B5%8B%E8%AF%95%E5%B9%B6%E6%80%BB%E7%BB%93)

[2，依赖管理](#2%EF%BC%8C%E4%BE%9D%E8%B5%96%E7%AE%A1%E7%90%86)

[2.1 依赖传递与冲突问题](#2.1%20%E4%BE%9D%E8%B5%96%E4%BC%A0%E9%80%92%E4%B8%8E%E5%86%B2%E7%AA%81%E9%97%AE%E9%A2%98)

[2.2 可选依赖和排除依赖](#2.2%20%E5%8F%AF%E9%80%89%E4%BE%9D%E8%B5%96%E5%92%8C%E6%8E%92%E9%99%A4%E4%BE%9D%E8%B5%96)

[方案一:可选依赖optional，对外隐藏](#%E6%96%B9%E6%A1%88%E4%B8%80%3A%E5%8F%AF%E9%80%89%E4%BE%9D%E8%B5%96)

[方案二:排除依赖exclusions，主动排除](#%E6%96%B9%E6%A1%88%E4%BA%8C%3A%E6%8E%92%E9%99%A4%E4%BE%9D%E8%B5%96)

[3，聚合和继承](#3%EF%BC%8C%E8%81%9A%E5%90%88%E5%92%8C%E7%BB%A7%E6%89%BF)

[3.1 聚合](#3.1%20%E8%81%9A%E5%90%88)

[3.1.1 概述](#3.1.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[3.1.2 具体实现](#3.1.2%20%E5%85%B7%E4%BD%93%E5%AE%9E%E7%8E%B0%C2%A0) 

[3.2 继承](#3.2%20%E7%BB%A7%E6%89%BF)

[3.3 聚合与继承的区别](#3.3%20%E8%81%9A%E5%90%88%E4%B8%8E%E7%BB%A7%E6%89%BF%E7%9A%84%E5%8C%BA%E5%88%AB)

[3.4 IDEA构建聚合与继承工程](#3.3.2%20IDEA%E6%9E%84%E5%BB%BA%E8%81%9A%E5%90%88%E4%B8%8E%E7%BB%A7%E6%89%BF%E5%B7%A5%E7%A8%8B)

[4，属性](#4%EF%BC%8C%E5%B1%9E%E6%80%A7)

[4.1 属性](#4.1%20%E5%B1%9E%E6%80%A7)

[4.1.1 问题分析](#4.1.1%20%E9%97%AE%E9%A2%98%E5%88%86%E6%9E%90)

[4.1.2 代码实现](#4.1.2%20%E8%A7%A3%E5%86%B3%E6%AD%A5%E9%AA%A4)

[4.2 配置文件加载属性](#4.2%20%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%8A%A0%E8%BD%BD%E5%B1%9E%E6%80%A7)

[4.3 版本管理](#4.3%20%E7%89%88%E6%9C%AC%E7%AE%A1%E7%90%86)

[5，多环境配置与应用](#5%EF%BC%8C%E5%A4%9A%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE%E4%B8%8E%E5%BA%94%E7%94%A8)

[5.1 多环境开发](#5.1%20%E5%A4%9A%E7%8E%AF%E5%A2%83%E5%BC%80%E5%8F%91)

[5.2 跳过测试](#5.2%20%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[方式一:IDEA工具实现跳过测试按钮](#%E6%96%B9%E5%BC%8F%E4%B8%80%3AIDEA%E5%B7%A5%E5%85%B7%E5%AE%9E%E7%8E%B0%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[方式二:配置插件实现跳过测试](#%E6%96%B9%E5%BC%8F%E4%BA%8C%3A%E9%85%8D%E7%BD%AE%E6%8F%92%E4%BB%B6%E5%AE%9E%E7%8E%B0%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[方式三:命令行跳过测试](#%E6%96%B9%E5%BC%8F%E4%B8%89%3A%E5%91%BD%E4%BB%A4%E8%A1%8C%E8%B7%B3%E8%BF%87%E6%B5%8B%E8%AF%95)

[6，私服](#6%EF%BC%8C%E7%A7%81%E6%9C%8D)

[6.1 私服简介](#6.1%20%E7%A7%81%E6%9C%8D%E7%AE%80%E4%BB%8B)

[6.2 私服安装](#6.2%20%E7%A7%81%E6%9C%8D%E5%AE%89%E8%A3%85)

[6.3 私服仓库分类](#6.3%20%E7%A7%81%E6%9C%8D%E4%BB%93%E5%BA%93%E5%88%86%E7%B1%BB)

[6.4 本地仓库访问私服配置](#6.4%20%E6%9C%AC%E5%9C%B0%E4%BB%93%E5%BA%93%E8%AE%BF%E9%97%AE%E7%A7%81%E6%9C%8D%E9%85%8D%E7%BD%AE)

[6.5 私服资源上传与下载](#6.5%20%E7%A7%81%E6%9C%8D%E8%B5%84%E6%BA%90%E4%B8%8A%E4%BC%A0%E4%B8%8E%E4%B8%8B%E8%BD%BD)

[步骤1:配置工程上传私服的具体位置](#%E6%AD%A5%E9%AA%A41%3A%E9%85%8D%E7%BD%AE%E5%B7%A5%E7%A8%8B%E4%B8%8A%E4%BC%A0%E7%A7%81%E6%9C%8D%E7%9A%84%E5%85%B7%E4%BD%93%E4%BD%8D%E7%BD%AE)

[步骤2:发布资源到私服](#%E6%AD%A5%E9%AA%A42%3A%E5%8F%91%E5%B8%83%E8%B5%84%E6%BA%90%E5%88%B0%E7%A7%81%E6%9C%8D)

--

## 0，解除端口调用

先查看占用端口的进程号 

```bash
netstat -ano | findstr "8080"
```

然后杀死进程号，例如进程号是12724：

```bash
taskkill -PID 12724 -F
```

示例：

![](https://i-blog.csdnimg.cn/blog_migrate/69ac57e02d5caa487a0c25968cd22a73.png)

> Linux解决端口占用：
> 
> ```
> netstat -tln
> ```
> 
> ```
> netstat -tln | grep 8080
> ```
> 
> ```
> lsof -i:8080
> ```
> 
> ```
> kill -9 进程id
> ```

## 1，分模块开发

### 1.1 分模块开发设计

**(1)按照功能拆分**

**我们现在的项目都是在一个模块**中，比如前面的SSM整合开发。虽然这样做功能也都实现了，但是也**存在了一些问题**，我们拿银行的项目为例来聊聊这个事。

-   网络没有那么发达的时候，我们需要到银行柜台或者取款机进行业务操作
-   随着互联网的发展,我们有了电脑以后，就可以在网页上登录银行网站使用U盾进行业务操作
-   再来就是随着智能手机的普及，我们只需要用手机登录APP就可以进行业务操作

上面三个场景出现的时间是不相同的，如果非要把三个场景的模块代码放入到一个项目，那么当其中某一个模块代码出现问题，就会导致整个项目无法正常启动，从而导致银行的多个业务都无法正常班理。所以我们会**按照功能将项目进行拆分**。

**(2)按照模块拆分**

比如**电商的项目**中，有**订单和商品两个模块**，订单中需要包含商品的详细信息，所以需要商品的模型类，商品模块也会用到商品的模型类，这个时候如果两个模块中都写模型类，就会出现**重复代码**，后期的维护成本就比较高。我们就想能不能将它们**公共的部分抽取成一个独立的模块**，其他模块要想使用可以像添加第三方jar包依赖一样来使用我们自己抽取的模块，这样就解决了代码重复的问题,这种拆分方式就说我们所说的**按照模块**拆分。

![](https://i-blog.csdnimg.cn/blog_migrate/1396ec4caacb5f8de196bfac9e42b453.png)

经过两个案例的分析，我们就知道:

-   **将原始模块按照功能拆分成若干个子模块，方便模块间的相互调用，接口共享。**

刚刚我们说了可以将domain层进行拆分，除了domain层，我们也可以将其他的层也拆成一个个对立的模块，如:

![](https://i-blog.csdnimg.cn/blog_migrate/f22d0e688fc8ea9797f46b7f86fc15bd.png)

这样的话，项目中的每一层都可以单独维护，也可以很方便的被别人使用。关于分模块开发的意义，我们就说完了，说了这么多好处，那么该如何实现呢?

### 1.2 分模块开发实现

前面我们已经完成了SSM整合，接下来，咱们就基于SSM整合的项目来实现对项目的拆分。

#### 1.2.1 环境准备

将`资料\maven_02_ssm`部署到IDEA中，将环境快速准备好，部署成功后，项目的格式如下:

![](https://i-blog.csdnimg.cn/blog_migrate/4a1086cff359836cedd6cca85e3cfe32.png)

#### 1.2.2 抽取domain层

**步骤1:创建新maven非web模块**

创建一个名称为**`maven_03_pojo`**的maven项目,为什么项目名是从02到03这样创建，是因为01留给聚合工程maven\_01\_parent（在3 聚合和继承里详细介绍），这块的名称可以任意。

![](https://i-blog.csdnimg.cn/blog_migrate/03c19201026223201a94a5da106a00f4.png)

**步骤2:项目中创建domain包并拷贝**

在**`maven_03_pojo`**项目中创建`com.itheima.domain`包，并将`maven_02_ssm`中Book类拷贝到该包中

![](https://i-blog.csdnimg.cn/blog_migrate/a038e97f9d1cfe8682f0ae846692660f.png)

**步骤3:删除原项目中的domain包**

删除后，`maven_02_ssm`项目中用到`Book`的类中都会有红色提示，如下:

![](https://i-blog.csdnimg.cn/blog_migrate/dde14a592ab6cad19cf5855b41dd4e15.png)

**说明:**出错的原因是`maven_02_ssm`中已经将Book类删除，所以该项目找不到Book类，所以报错

要想解决上述问题，我们需要在`maven_02_ssm`中添加`maven_03_pojo`的依赖。

**步骤4:建立依赖关系**

在`maven_02_ssm`项目的pom.xml添加`maven_03_pojo`的依赖

```XML
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_03_pojo</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>
```

因为添加了依赖，所以在`maven_02_ssm`中就已经能找到Book类，所以刚才的报红提示就会消失。

**步骤5:编译`maven_02_ssm`项目**

编译`maven_02_ssm`你会在控制台看到如下错误

![](https://i-blog.csdnimg.cn/blog_migrate/da61e10fef942fca18879dbbf7a0e5bb.png)

错误信息为：**不能解决`maven_02_ssm`项目的依赖问题，找不到`maven_03_pojo`这个jar包。**

**为什么找不到呢?**

原因是Maven会从本地仓库找对应的jar包，但是**本地仓库又不存在该jar包**所以会报错。

在IDEA中是有`maven_03_pojo`这个项目，所以我们只需要**将`maven_03_pojo`项目安装到本地仓库**即可。

**步骤6:将项目安装本地仓库**

将需要被依赖的项目`maven_03_pojo`，使用maven的install命令，把其安装到Maven的本地仓库中。

![](https://i-blog.csdnimg.cn/blog_migrate/520c6504fb483ca7fa3792cda2157f56.png)

安装成功后，在对应的路径下就看到安装好的jar包

![](https://i-blog.csdnimg.cn/blog_migrate/9f981e17ef42da9c28f7e620d8f4dde0.png)

**说明:**具体安装在哪里，和你们自己电脑上Maven的本地仓库配置的位置有关。

当再次执行`maven_02_ssm`的compile的命令后，就已经能够成功编译。

#### 1.2.3 抽取Dao层

**步骤1:创建新模块**

创建一个名称为**`maven_04_dao`**的jar项目

![](https://i-blog.csdnimg.cn/blog_migrate/36d7118be596a895331acb252d963603.png)

**步骤2:项目中创建dao包并拷贝**

在`maven_04_dao`项目中创建`com.itheima.dao`包，并将`maven_02_ssm`中BookDao类拷贝到该包中

![](https://i-blog.csdnimg.cn/blog_migrate/80ee6c5011a88c88e98cc62609ffca57.png)

**出现问题:**

![](https://i-blog.csdnimg.cn/blog_migrate/d2242bd0791ee61cae689a1d275ce61d.png)

-   项目`maven_04_dao`的BookDao接口中Book类找不到报错
    
-   项目`maven_04_dao`的BookDao接口中，Mybatis的增删改查注解报错
    

**解决方案：在`maven_04_dao`项目的pom.xml中添加`maven_03_pojo`项目和`mybatis`的相关依赖、spring依赖**

```XML
    <dependencies>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <dependency>
            <groupId>org.example</groupId>
            <artifactId>maven_03_pojo</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

    </dependencies>
```

**步骤3:删除原项目中的dao包**

删除Dao包以后，因为`maven_02_ssm`中的BookServiceImpl类中有使用到Dao的内容，所以需要在`maven_02_ssm`的pom.xml添加`maven_04_dao`的依赖

```XML
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>
```

此时在`maven_02_ssm`项目中就已经添加了`maven_03_pojo`和`maven_04_dao`包

![](https://i-blog.csdnimg.cn/blog_migrate/a2732e8c57afe57f6185823d6ddb61f1.png)

再次对`maven_02_ssm`项目进行编译，又会报错，如下:

![](https://i-blog.csdnimg.cn/blog_migrate/2dd8b0231b6f721cdf003e7dbf01fb81.png)

和刚才的错误原因是一样的，maven在仓库中没有找到`maven_04_dao`,所以此时我们只需要将`maven_04_dao`安装到Maven的本地仓库即可。

**步骤4:将项目安装到本地仓库**

**首先install前面的maven\_03\_pojo，**然后再使用maven的install命令`maven_04_dao`，把其安装到Maven的本地仓库中。

![](https://i-blog.csdnimg.cn/blog_migrate/125a8225ac58f0fb59f8b2109b7d67a2.png)

安装成功后，在对应的路径下就看到了安装好对应的jar包

![](https://i-blog.csdnimg.cn/blog_migrate/004d0a10c47f36b3b1446bbef939aa42.png)

当再次执行`maven_02_ssm`的compile的指令后，就已经能够成功编译。

#### 1.2.4 运行测试并总结

将抽取后的项目进行运行，测试之前的增删改查功能依然能够使用。

所以对于项目的拆分，大致会有如下几个步骤:

(1) 创建Maven模块

(2) 书写模块代码

分模块开发需要先针对模块功能进行设计，再进行编码。不会先将工程开发完毕，然后进行拆分。拆分方式可以按照功能拆也可以按照模块拆。

(3)通过maven指令安装模块到本地仓库(install 指令)

团队内部开发需要发布模块功能到团队内部可共享的仓库中(私服)，私服我们后面会讲解。

## 2，依赖管理

我们现在已经能把项目拆分成一个个独立的模块，当在**其他项目中想要使用**独立出来的这些**模块**，只需要在其pom.xml使用标签来进行**jar包的引入**即可。

其实就是依赖，关于依赖管理里面都涉及哪些内容，我们就一个个来学习下:

-   依赖传递
-   可选依赖
-   排除依赖

**依赖:**

**依赖指当前项目运行所需的jar，一个项目可以设置多个依赖。**

**格式:**

```XML
<!--设置当前项目所依赖的所有jar-->
<dependencies>
    <!--设置具体的依赖-->
    <dependency>
        <!--依赖所属群组id-->
        <groupId>org.springframework</groupId>
        <!--依赖所属项目id-->
        <artifactId>spring-webmvc</artifactId>
        <!--依赖版本号-->
        <version>5.2.10.RELEASE</version>
    </dependency>
</dependencies>
```

### 2.1 依赖传递与冲突问题

回到我们刚才的项目案例中，打开Maven的面板，你会发现:

![](https://i-blog.csdnimg.cn/blog_migrate/92fa72554db10e489db43991fd34dd16.png)

在项目所依赖的这些jar包中，有一个比较大的区别就是**有的依赖前面有箭头`>`,有的依赖前面没有。**

**依赖中箭头>的含义：**

这个依赖还依赖了其他依赖。 

**依赖传递验证：**

打开前面的箭头，你会发现这个jar包下面还包含有其他的jar包

![](https://i-blog.csdnimg.cn/blog_migrate/7346fe52d1cf95963f1873b3c2d62a81.png)

你会发现有两个`maven_03_pojo`的依赖被加载到Dependencies中，那么`maven_04_dao`中的`maven_03_pojo`能不能使用呢?

要想验证非常简单，只需要把`maven_02_ssm`项目中pom.xml关于`maven_03_pojo`的依赖注释或删除掉

![](https://i-blog.csdnimg.cn/blog_migrate/03f709b51b72bfacad3bbc3263dbf526.png)

在Dependencies中移除自己所添加`maven_03_pojo`依赖后，打开BookServiceImpl的类，你会发现Book类依然存在，可以被正常使用

![](https://i-blog.csdnimg.cn/blog_migrate/eeaf76dfd49b28ec14e3fbe7be55f185.png)

这个特性其实就是我们要讲解的**依赖传递**。

**依赖是具有传递性的:**

![](https://i-blog.csdnimg.cn/blog_migrate/902c9f650a6a4480f8f251223da73cf9.png)

**说明:**A代表自己的项目；B,C,D,E,F,G代表的是项目所依赖的jar包；D1和D2 E1和E2代表是相同jar包的不同版本

(1) **A依赖了B和C,B和C有分别依赖了其他jar包，所以在A项目中就可以使用上面所有jar包，这就是所说的依赖传递**

(2) 依赖传递有**直接依赖和间接依赖**

**直接依赖：pom中直接引入的依赖**

**间接依赖：pom中引入依赖中的依赖**

-   相对于A来说，A直接依赖B和C,间接依赖了D1,E1,G，F,D2和E2
-   相对于B来说，B直接依赖了D1和E1,间接依赖了G
-   直接依赖和间接依赖是一个相对的概念

(3)**因为有依赖传递的存在**，就会导致jar包在依赖的过程中**出现冲突问题**。

**依赖冲突：**

这里所说的**依赖冲突**是指项目依赖的**某一个jar包**，**有多个不同的版本**，因而造成类包版本冲突。

> 依赖冲突不用太认真的记忆，**直观看maven的依赖版本比较直白**：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/87f4ec8af27037aa204b753925c25782.png)

**情况一:**

在`maven_02_ssm`的pom.xml中添加两个不同版本的Junit依赖:

```XML
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
</dependencies>
```

![](https://i-blog.csdnimg.cn/blog_migrate/9106ccfe498ad0643fafd53d89105f29.png)

通过对比，会发现一个结论

-   **同级特殊优先：**当同级配置了相同资源的不同版本，**后配置的覆盖先配置的。**

情况二: **不同级路径优先：**当依赖中出现相同的资源时，层级越深，优先级越低，**层级越浅，优先级越高**

-   A通过B间接依赖到E1
-   A通过C间接依赖到E2
-   A就会间接依赖到E1和E2,Maven会按照层级来选择，E1是2度，E2是3度，所以最终会选择E1

情况三: **同级间接依赖声明优先：**当资源在相同层级被依赖时，**配置顺序靠前的覆盖配置顺序靠后的**

-   A通过B间接依赖到D1
-   A通过C间接依赖到D2
-   D1和D2都是两度，这个时候就不能按照层级来选择，需要按照声明来，谁先声明用谁，也就是说B在C之前声明，这个时候使用的是D1，反之则为D2

但是对应上面这些结果，大家不需要刻意去记它。因为不管Maven怎么选，最终的结果都会在Maven的`Dependencies`面板中展示出来，展示的是哪个版本，也就是说它选择的就是哪个版本，如:

![](https://i-blog.csdnimg.cn/blog_migrate/937a2bd909286abe22a4fa33370e65df.png)

如果想更全面的查看Maven中各个坐标的依赖关系，可以点击Maven面板中的`show Dependencies`

![](https://i-blog.csdnimg.cn/blog_migrate/ba0082b2071585b80ebe72f079e140fd.png)

在这个视图中就能很明显的展示出jar包之间的相互依赖关系。

### 2.2 可选依赖和排除依赖

思考：

![](https://i-blog.csdnimg.cn/blog_migrate/d6c26a7a02c16c7647a646986c801be6.png)

-   maven\_02\_ssm 依赖了 maven\_04\_dao
-   maven\_04\_dao 依赖了 maven\_03\_pojo
-   因为现在有依赖传递，所以maven\_02\_ssm能够使用到maven\_03\_pojo的内容
-   如果说现在不想让maven\_02\_ssm依赖到maven\_03\_pojo，有哪些解决方案?

**说明:**在真实使用的过程中，maven\_02\_ssm中是需要用到maven\_03\_pojo的，我们这里只是用这个例子描述我们的需求。因为有时候，maven\_04\_dao出于某些因素的考虑，就是不想让别人使用自己所依赖的maven\_03\_pojo。

#### 方案一:可选依赖optional，对外隐藏

-   **可选依赖指对外隐藏当前所依赖的资源---不透明**

在`maven_04_dao`的pom.xml,在引入`maven_03_pojo`的时候，添加**`optional`**

```XML
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_03_pojo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--可选依赖是隐藏当前工程所依赖的资源，隐藏后对应资源将不具有依赖传递-->
    <optional>true</optional>
</dependency>
```

此时BookServiceImpl就已经报错了,说明由于maven\_04\_dao将maven\_03\_pojo设置成可选依赖，导致maven\_02\_ssm无法引用到maven\_03\_pojo中的内容，导致Book类找不到。

![](https://i-blog.csdnimg.cn/blog_migrate/8da8360043e33a3c57d7d526cdc31321.png)

#### 方案二:排除依赖exclusions，主动排除

-   **排除依赖指主动断开依赖的资源，被排除的资源无需指定版本---不需要**

前面我们已经通过可选依赖实现了阻断maven\_03\_pojo的依赖传递，对于排除依赖，则指的是已经有依赖的事实，也就是说maven\_02\_ssm项目中已经通过依赖传递用到了maven\_03\_pojo，此时我们需要做的是将其进行排除，所以接下来需要修改maven\_02\_ssm的pom.xml

```XML
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--排除依赖是隐藏当前资源对应的依赖关系-->
    <exclusions>
        <exclusion>
            <groupId>com.itheima</groupId>
            <artifactId>maven_03_pojo</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

这样操作后，BookServiceImpl中的Book类一样也会报错。

当然`exclusions`标签带`s`说明我们是可以依次排除多个依赖到的jar包，比如maven\_04\_dao中有依赖junit和mybatis,我们也可以一并将其排除。

```XML
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--排除依赖是隐藏当前资源对应的依赖关系-->
    <exclusions>
        <exclusion>
            <groupId>com.itheima</groupId>
            <artifactId>maven_03_pojo</artifactId>
        </exclusion>
        <exclusion>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

介绍我这两种方式后，简单来梳理下，就是

-   `A依赖B,B依赖C`,`C`通过依赖传递会被`A`使用到，现在要想办法让`A`不去依赖`C`
-   可选依赖是在B上设置`<optional>`,`A`不知道有`C`的存在，
-   排除依赖是在A上设置`<exclusions>`,`A`知道有`C`的存在，主动将其排除掉。

## 3，聚合和继承

我们的项目已经从以前的单模块，变成了现在的多模块开发。项目一旦变成了多模块开发以后，就会引发一些问题。

### 3.1 聚合

#### 3.1.1 概述 

![](https://i-blog.csdnimg.cn/blog_migrate/4f5e43984af851b8da34856ae00375ea.png)

-   分模块开发后，需要将这**四个项目都安装到本地仓库**，目前我们只能通过项目Maven面板的`install`来安装，并且需要安装四个，如果我们的项目足够多，那么一个个安装起来还是比较**麻烦**的
-   如果四个项目都已经安装成功，当**实体类ssm\_pojo发生变化后**，我们就得将ssm\_pojo**重新安装**到maven仓库，但是为了确保我们对ssm\_pojo的修改不会影响到其他项目模块，我们**需要对所有的模块进行重新编译**，那又需要将所有的模块再来一遍

项目少的话还好，但是如果项目多的话，一个个操作项目就容易出现漏掉或重复操作的问题，所以我们就想能不能**抽取一个项目**，**把所有的项目管理起来**，以后我们要想操作这些项目，只需要操作这一个项目，其他所有的项目都走一样的流程，这个不就很省事省力。

**聚合：**

-   **聚合:将多个模块组织成一个整体，同时进行项目构建的过程称为聚合**
    
-   **聚合工程：**通常是一个**不具有业务功能的"空"工程**（**有且仅有一个pom文件**）
    
-   **作用：**使用聚合工程可以将多个工程编组，**通过对聚合工程进行构建**，实现对**所包含的模块进行同步构建**
    
    -   当工程中某个模块发生更新（变更）时，必须保障工程中与已更新模块关联的模块同步更新，此时可以使用聚合工程来解决批量模块同步构建的问题。

#### 3.1.2 具体实现 

关于聚合具体的实现步骤为:

**步骤1:创建一个空的maven项目**

![](https://i-blog.csdnimg.cn/blog_migrate/08b9aec5223feef63d04cd40ccd1ddd6.png)

**步骤2:将项目的打包方式改为pom**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <packaging>pom</packaging>
    
</project>
```

> **项目的打包方式：**
> 
> -   **jar:**默认情况，说明该项目为java项目
> -   **war:**说明该项目为web项目
> -   **pom:**说明该项目为聚合或继承(后面会讲)项目

**步骤3:pom.xml添加所要管理的项目**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <packaging>pom</packaging>
    
    <!--设置管理的模块名称，module顺序不重要，系统会根据依赖关系自动调整顺序。各模块都在当前pom.xml的父目录一级-->
    <modules>
        <module>../maven_02_ssm</module>
        <module>../maven_03_pojo</module>
        <module>../maven_04_dao</module>
    </modules>
</project>
```

**步骤4:使用聚合统一管理项目**

![](https://i-blog.csdnimg.cn/blog_migrate/3a6898a9343c30cb9777c9c59819f591.png)

测试发现，**当`maven_01_parent`的`compile`被点击后**，所有**被其管理的项目**都会被执行**编译**操作。这就是聚合工程的作用。

**说明：**聚合工程管理的项目在进行运行的时候，会**按照项目与项目之间的依赖关系来自动决定执行的顺序，和配置的顺序无关**。

聚合的知识我们就讲解完了，最后总结一句话就是，**聚合工程主要是用来管理项目**。

### 3.2 继承

我们已经完成了使用聚合工程去管理项目，聚合工程进行某一个构建操作，其他被其管理的项目也会执行相同的构建操作。

多模块开发存在的另外一个问题：**`重复配置`的问题**，我们先来看张图:

![](https://i-blog.csdnimg.cn/blog_migrate/18c3dc81ff0010e0425acc04a35adc45.png)

-   `spring-webmvc`、`spring-jdbc`在三个项目模块中都有出现，这样就出现了**重复的内容**
-   `spring-test`只在ssm\_crm和ssm\_goods中出现，而在ssm\_order中没有，这里是部分重复的内容
-   我们使用的spring版本目前是`5.2.10.RELEASE`,假如后期要**想升级spring版本**，**所有**跟Spring相关jar包**都得被修改**，涉及到的项目越多，**维护成本**越高

面对上面的这些问题，我们就得用到接下来要学习的**继承**

-   **继承**:描述的是两个工程间的关系，与java中的继承相似，**子工程可以继承父工程中的配置信息**，常见于依赖关系的继承。
    
-   **作用：**
    
    -   简化配置
    -   减少版本冲突

> **继承的实现步骤总结:**
> 
> -   创建Maven模块，设置打包类型为pom
>     
>     ```
>     <packaging>pom</packaging>
>     ```
>     
> -   在**父工程**的pom文件中**配置共用的依赖**(子工程将沿用父工程中的依赖关系),一般只抽取子项目中公有的jar包
>     
>     ```XML
>     <dependencies>
>         <dependency>
>             <groupId>org.springframework</groupId>
>             <artifactId>spring-webmvc</artifactId>
>             <version>5.2.10.RELEASE</version>
>         </dependency>
>         ...
>     </dependencies>
>     ```
>     
> -   在**父工程**中配置依赖管理，提供可选择的依赖资源，让子工程中可以按需引用
>     
>     ```XML
>     <dependencyManagement>
>         <dependencies>
>             <dependency>
>                 <groupId>com.alibaba</groupId>
>                 <artifactId>druid</artifactId>
>                 <version>1.1.16</version>
>             </dependency>
>         </dependencies>
>         ...
>     </dependencyManagement>
>     ```
>     
> -   在**子工程中**配置当前工程所继承的**父工程**
>     
>     ```XML
>     <!--定义该工程的父工程-->
>     <parent>
>         <groupId>com.itheima</groupId>
>         <artifactId>maven_01_parent</artifactId>
>         <version>1.0-RELEASE</version>
>         <!--快速找到父工程的pom文件的相关路径,可以不写-->
>         <relativePath>../maven_01_parent/pom.xml</relativePath>
>     </parent>
>     ```
>     
> -   在**子工程中**配置使用父工程中可选**依赖的坐标，别配版本**
>     
>     ```XML
>     <dependencies>
>         <dependency>
>             <groupId>com.alibaba</groupId>
>             <artifactId>druid</artifactId>
>         </dependency>
>     </dependencies>
>     ```
>     
>     **注意事项:**
>     
>     1.子工程中使用父工程中的可选依赖时，仅需要提供群组id和项目id，无需提供版本，版本由父工程统一提供，避免版本冲突
>     
>     2.子工程中还可以定义父工程中没有定义的依赖关系,只不过不能被父工程进行版本统一管理。
>     

**实现步骤：**

**步骤1:创建一个空的Maven项目并将其打包方式设置为pom**

因为这一步和前面maven创建聚合工程的方式是一摸一样，所以我们可以单独创建一个新的工程，也可以**直接和聚合公用一个工程**。实际开发中，聚合和继承一般也都放在同一个项目中，但是这两个的功能是不一样的。

**步骤2:在子项目中设置其父工程**

分别在`maven_02_ssm`,`maven_03_pojo`,`maven_04_dao`的**pom.xml中添加其父项目**为`maven_01_parent。别忘了设置relativePath`

```XML
<!--配置当前工程继承自parent工程-->
<parent>
    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <!--设置父项目pom.xml位置路径-->
    <relativePath>../maven_01_parent/pom.xml</relativePath>
</parent>
```

**步骤3:父工程引入共有依赖**

-   将**子项目共同使用的jar包都抽取出来**，维护在**父项目的pom.xml**中。除了Junit和其他模块的依赖都抽取。

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <packaging>pom</packaging>
    
    <!--设置管理的模块名称-->
    <modules>
        <module>../maven_02_ssm</module>
        <module>../maven_03_pojo</module>
        <module>../maven_04_dao</module>
    </modules>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>1.3.0</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.16</version>
        </dependency>

        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>

        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.9.0</version>
        </dependency>
    </dependencies>
</project>
```

-   **删除子项目**中**已经被抽取**到父项目的pom.xml中的**jar包**，如在`maven_02_ssm`的pom.xml中将已经出现在父项目的jar包删除掉，只留下其他模块的依赖和Junit。

```XML
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.itheima</groupId>
  <artifactId>maven_02_ssm</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <!--配置当前工程继承自parent工程-->
  <parent>
    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <relativePath>../maven_01_parent/pom.xml</relativePath>
  </parent>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>com.itheima</groupId>
      <artifactId>maven_04_dao</artifactId>
      <version>1.0-SNAPSHOT</version>
      <!--排除依赖是隐藏当前资源对应的依赖关系-->
      <exclusions>
        <exclusion>
          <groupId>log4j</groupId>
          <artifactId>log4j</artifactId>
        </exclusion>
        <exclusion>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis</artifactId>
        </exclusion>
      </exclusions>
    </dependency>

  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <configuration>
          <port>80</port>
          <path>/</path>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>


```

> **验证子项目继承副项目：**
> 
> **删除完后**，你会发现父项目中有依赖对应的jar包，子项目虽然已经将重复的依赖删除掉了，但是刷新的时候，**子项目中所需要的jar包依然存在**。
> 
> **当项目的`<parent>`标签被移除掉，会发现多出来的jar包依赖也会随之消失。**

-   将**子项目**`maven_04_dao`项目的pom.xml中的**所有依赖删除**，然后**添加上`maven_01_parent`的父项目坐标**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!--配置当前工程继承自parent工程-->
    <parent>
        <groupId>com.itheima</groupId>
        <artifactId>maven_01_parent</artifactId>
        <version>1.0-RELEASE</version>
        <relativePath>../maven_01_parent/pom.xml</relativePath>
    </parent>
</project>
```

刷新并查看Maven的面板，会发现maven\_04\_dao同样引入了父项目中的所有依赖。

![](https://i-blog.csdnimg.cn/blog_migrate/225ef294d73f3781a53448948b3111af.png)

这样我们就可以解决刚才提到的第一个问题，**将子项目中的公共jar包抽取到父工程中进行统一添加依赖**，这样做的可以简化配置，并且当父工程中所依赖的jar包版本发生变化，所有子项目中对应的jar包版本也会跟着更新。

![](https://i-blog.csdnimg.cn/blog_migrate/7caa7541b4c2bc45081a6e31bef2d3d9.png)

**步骤4:优化子项目依赖版本问题，依赖管理`dependencyManagement`**

如果把所有用到的jar包都管理在父项目的pom.xml，看上去更简单些，但是这样就会**导致有很多项目引入了过多自己不需要的jar包**。如上面看到的这张图:

![](https://i-blog.csdnimg.cn/blog_migrate/c5297d38e81dc9bf723722479caa4f93.png)

如果把所有的依赖都放在了父工程中进行统一维护，就会导致ssm\_order项目中多引入了`spring-test`的jar包，如果这样的jar包过多的话，对于ssm\_order来说也是一种"负担"。

那针对于这种部分项目有的jar包**，优化方法：**

-   1.在**父工程**mavne\_01\_parent的pom.xml来**定义依赖管理**

```XML
<!--定义依赖管理-->
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

-   2.将**maven\_02\_ssm**的pom.xml中的**junit依赖删除掉**，**刷新Maven**

![](https://i-blog.csdnimg.cn/blog_migrate/e958dabbf8b393ae5d6a74ddc39665fc.png)

刷新完会发现，在maven\_02\_ssm项目中的junit依赖并没有出现，所以我们得到一个结论:

**`<dependencyManagement>`标签不真正引入jar包，而是配置可供子项目选择的jar包依赖**

子项目要想使用它所提供的这些jar包，需要自己添加依赖，并且不需要指定`<version>`

-   3.在maven\_02\_ssm的pom.xml添加junit的依赖，不指定版本

```XML
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <scope>test</scope>
</dependency>
```

**注意：这里就不需要添加版本了，这样做的好处就是当父工程dependencyManagement标签中的版本发生变化后，子项目中的依赖版本也会跟着发生变化**

-   4.在maven\_04\_dao的pom.xml添加junit的依赖

```XML
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <scope>test</scope>
</dependency>
```

这个时候，maven\_02\_ssm和maven\_04\_dao这两个**子项目中的junit版本**就会跟**随着父项目中的标签dependencyManagement中junit的版本发生变化而变化。**不需要junit的项目就不需要添加对应的依赖即可。

> 总结来说，**继承可以帮助做两件事：**
> 
> -   将所有项目**公共的jar包依赖提取到父工程**的pom.xml中，子项目就可以不用重复编写，简化开发
>     
> -   **将所有项目的jar包配置到父工程的依赖管理**dependencyManagement标签下，实现版本管理，方便维护
>     
>     -   **dependencyManagement标签不真正引入jar包，只是管理jar包的版本**
>     -   子项目在引入的时候，只需要指定groupId和artifactId，不需要加version
>     -   当dependencyManagement标签中jar包版本发生变化，所有子项目中有用到该jar包的地方对应的版本会自动随之更新
> 
> 最后总结一句话就是，**父工程主要是用来快速配置依赖jar包和管理项目中所使用的资源**。

> **小结**
> 
> **继承的实现步骤:**
> 
> -   创建Maven模块，设置打包类型为pom
>     
>     ```XML
>     <packaging>pom</packaging>
>     ```
>     
> -   在**父工程**的pom文件中**配置依赖**关系(子工程将沿用父工程中的依赖关系),一般只抽取子项目中公有的jar包
>     
>     ```XML
>     <dependencies>
>         <dependency>
>             <groupId>org.springframework</groupId>
>             <artifactId>spring-webmvc</artifactId>
>             <version>5.2.10.RELEASE</version>
>         </dependency>
>         ...
>     </dependencies>
>     ```
>     
> -   在**父工程**中配置依赖管理，让子工程中可以不带版本引用父工程可选依赖
>     
>     ```XML
>     <dependencyManagement>
>         <dependencies>
>             <dependency>
>                 <groupId>com.alibaba</groupId>
>                 <artifactId>druid</artifactId>
>                 <version>1.1.16</version>
>             </dependency>
>         </dependencies>
>         ...
>     </dependencyManagement>
>     ```
>     
> -   在**子工程中**配置当前工程所继承的**父工程**
>     
>     ```XML
>     <!--定义该工程的父工程-->
>     <parent>
>         <groupId>com.itheima</groupId>
>         <artifactId>maven_01_parent</artifactId>
>         <version>1.0-RELEASE</version>
>         <!--填写父工程的pom文件,可以不写-->
>         <relativePath>../maven_01_parent/pom.xml</relativePath>
>     </parent>
>     ```
>     
> -   在**子工程中**配置使用父工程中可选**依赖的坐标**
>     
>     ```XML
>     <dependencies>
>         <dependency>
>             <groupId>com.alibaba</groupId>
>             <artifactId>druid</artifactId>
>         </dependency>
>     </dependencies>
>     ```
>     
>     **注意事项:**
>     
>     1.子工程中使用父工程中的可选依赖时，仅需要提供群组id和项目id，无需提供版本，版本由父工程统一提供，避免版本冲突
>     
>     2.子工程中还可以定义父工程中没有定义的依赖关系,只不过不能被父工程进行版本统一管理。
>     

### 3.3 聚合与继承的区别

**两种之间的作用:**

-   **聚合**用于**快速构建项目**，对项目进行管理
-   **继承**用于**快速配置和管理子项目**中所使用**jar包**的版本

聚合和继承的**相同点:**

-   聚合与继承的pom.xml文件**打包方式均为pom**，可以将两种关系制作到同一个pom文件中
-   聚合与继承均属于**设计型模块**，并**无实际的模块内容**

聚合和继承的**不同点:**

-   **聚合**是在**当前模块中配置关系**，聚合可以感知到参与聚合的模块有哪些
-   **继承**是在**子模块中配置关系**，父模块无法感知哪些子模块继承了自己

相信到这里，大家已经能区分开什么是聚合和继承，但是有一个稍微麻烦的地方就是聚合和继承的工程构建，需要在聚合项目中手动添加`modules`标签，需要在所有的子项目中添加`parent`标签，万一写错了咋办?

### 3.4 IDEA构建聚合与继承工程

其实对于聚合和继承工程的创建，IDEA已经能帮助我们快速构建，具体的实现步骤为:

**步骤1:创建一个Maven项目**

创建一个空的Maven项目，可以将项目中的`src`目录删除掉，这个项目作为聚合工程和父工程。

![](https://i-blog.csdnimg.cn/blog_migrate/a5679f62db9909726199bdaeac36ad28.png)

**步骤2:创建子项目**

该项目可以被聚合工程管理，同时会继承父工程。

![](https://i-blog.csdnimg.cn/blog_migrate/0a541566c4cf858fd713ba8aa99bbea3.png)

![](https://i-blog.csdnimg.cn/blog_migrate/4a7f90ca4792f85015edab7c492ed809.png)

创建成功后，maven\_parent即是聚合工程又是父工程，maven\_web中也有parent标签，继承的就是maven\_parent,对于难以配置的内容都自动生成。

按照上面这种方式，大家就可以根据自己的需要来构建分模块项目。

## 4，属性

在这一章节内容中，我们将学习两个内容，分别是

-   属性
-   版本管理

属性中会继续解决分模块开发项目存在的问题，版本管理主要是认识下当前主流的版本定义方式。

### 4.1 属性

#### 4.1.1 问题分析

前面我们已经在父工程中的dependencyManagement标签中对项目中所使用的jar包版本进行了统一的管理，但是**如果在标签中有如下的内容:**

![](https://i-blog.csdnimg.cn/blog_migrate/8a3fa9f4615b8ef6096736d48fd5cb16.png)

你会发现，如果我们现在**想更新Spring的版本**，你会发现我们**依然需要更新多个jar包的版本**，这样的话还是有可能出现漏改导致程序出问题，而且改起来也是比较麻烦。

问题清楚后，我们需要解决的话，就可以参考咱们java基础所学习的变量，**声明一个变量**，**在其他地方使用该变量**，当变量的值发生变化后，所有使用变量的地方，就会跟着修改，即:

![](https://i-blog.csdnimg.cn/blog_migrate/02ea1ddca2173fd94f8ad121d260aa16.png)

#### 4.1.2 代码实现

**步骤1:父工程中定义属性**

```XML
<properties>
    <spring.version>5.2.10.RELEASE</spring.version>
    <junit.version>4.12</junit.version>
    <mybatis-spring.version>1.3.0</mybatis-spring.version>
</properties>
```

**步骤2:修改依赖的version**

```XML
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>${spring.version}</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>${spring.version}</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>${spring.version}</version>
</dependency>
```

此时，我们只需要更新父工程中properties标签中所维护的jar包版本，所有子项目中的版本也就跟着更新。当然除了将spring相关版本进行维护，我们可以将其他的jar包版本也进行抽取，这样就可以对项目中所有jar包的版本进行统一维护，如:

```XML
<!--定义属性-->
<properties>
    <spring.version>5.2.10.RELEASE</spring.version>
    <junit.version>4.12</junit.version>
    <mybatis-spring.version>1.3.0</mybatis-spring.version>
</properties>
```

### 4.2 配置文件加载属性

现在已经能够通过Maven来集中管理Maven中依赖jar包的版本。

现在想让Maven对于属性的管理范围能更大些，比如我们之前项目中的`jdbc.properties`，这个配置文件中的属性，能不能也来让Maven进行管理呢?

父工程配置文件**加载单文件属性：**

**实现步骤:**

**步骤1:父工程定义属性**

```XML
<properties>
   <jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
</properties>
```

**步骤2:jdbc.properties文件中引用属性**

在jdbc.properties，将jdbc.url的值直接获取Maven配置的属性

```XML
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=${jdbc.url}
jdbc.username=root
jdbc.password=root
```

**步骤3:设置maven过滤文件范围**

**Maven**在**默认情况下是从当前项目的`src\main\resources`下读取**文件进行**打包**。现在我们需要打包的资源文件是在maven\_02\_ssm下,需要我们通过配置来指定下具体的资源目录。

```XML
<build>
    <resources>
        <!--设置资源目录-->
        <resource>
            <directory>../maven_02_ssm/src/main/resources</directory>
            <!--设置能够解析${}，默认是false -->
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

**说明:**directory路径前要添加`../`的原因是maven\_02\_ssm相对于父工程的pom.xml路径是在其上一层的目录中，所以需要添加。

修改完后，注意maven\_02\_ssm项目的resources目录就多了些东西，如下:

![](https://i-blog.csdnimg.cn/blog_migrate/a2122e60b7d85f8ec11b193cb64a31c9.png)

**步骤4:测试是否生效**

测试的时候，只需要将**maven\_02\_ssm项目进行打包**，然后观察打包结果中最终**生成的内容是否为Maven中配置的内容**。

![](https://i-blog.csdnimg.cn/blog_migrate/84171c69bc039d259bf642c3ad115c04.png)

**父工程配置文件加载多个项目的属性：**

**方式一:麻烦**

```XML
<build>
    <resources>
        <!--设置资源目录，并设置能够解析${}-->
        <resource>
            <directory>../maven_02_ssm/src/main/resources</directory>
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>../maven_03_pojo/src/main/resources</directory>
            <filtering>true</filtering>
        </resource>
        ...
    </resources>
</build>
```

可以配，但是如果项目够多的话，这个配置也是**比较繁琐**

**方式二:通用**

```XML
<build>
    <resources>
        <!--
			${project.basedir}: 当前项目所在目录,子项目继承了父项目，
			相当于所有的子项目都添加了资源目录的过滤
		-->
        <resource>
            <directory>${project.basedir}/src/main/resources</directory>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

**说明:**打包的过程中如果报如下错误:

![](https://i-blog.csdnimg.cn/blog_migrate/6c80df0d41c33f5db455b50616f5ff8c.png)

原因就是Maven发现你的项目为web项目，就会去找web项目的入口web.xml\[配置文件配置的方式\]，发现没有找到，就会报错。

**方式二的报错解决：**

**解决方案1：**在maven\_02\_ssm项目的`src\main\webapp\WEB-INF\`**添加一个web.xml文件**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
</web-app>
```

**解决方案2:** maven\_02\_ssm配置maven打包war时，**忽略web.xml检查，failOnMissingWebXml**

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.2.3</version>
            <configuration>
                <failOnMissingWebXml>false</failOnMissingWebXml>
            </configuration>
        </plugin>
    </plugins>
</build>
```

上面我们所使用的都是Maven的自定义属性，除了${project.basedir},它属于Maven的内置系统属性。

在Maven中的属性分为:

-   自定义属性（常用）
-   内置属性
-   Setting属性
-   Java系统属性
-   环境变量属性

![](https://i-blog.csdnimg.cn/blog_migrate/9baec7a03420b989a87b43d8b43fe4a0.png)

具体如何查看这些属性:

在cmd命令行中输入`mvn help:system`

![](https://i-blog.csdnimg.cn/blog_migrate/cf66082af90e38b03c6bbde750cf1e88.png)

具体使用，就是使用 `${key}`来获取，key为等号左边的，值为等号右边的，比如获取红线的值，对应的写法为 `${java.runtime.name}`。

### 4.3 版本管理

关于这个版本管理解决的问题是，在Maven创建项目和引用别人项目的时候，我们都看到过如下内容:

![](https://i-blog.csdnimg.cn/blog_migrate/9b88714565305f3d9e1dadd1421cbc17.png)

这里面有两个单词，**SNAPSHOT和RELEASE**，它们所代表的含义是什么呢?

我们打开Maven仓库地址`https://mvnrepository.com/`

![](https://i-blog.csdnimg.cn/blog_migrate/cedff99ceba173c4375e69069a11c1f5.png)

在我们jar包的版本定义中，有两个工程版本用的比较多:

-   **SNAPSHOT（快照版本）**
    
    -   项目开发过程中**临时输出的版本**，称为快照版本
    -   快照版本会随着开发的进展不断更新
-   **RELEASE（发布版本）**
    
    -   项目开发到一定阶段里程碑后，向团队外部发布较为稳定的版本，这种版本所对应的构件文件是稳定的
    -   即便进行功能的后续开发，也不会改变当前发布版本内容，这种版本称为发布版本

除了上面的工程版本，我们还经常能看到一些发布版本:

-   **alpha版:内测版**，bug多不稳定内部版本不断添加新功能
-   **beta版:公测版**，不稳定(比alpha稳定些)，bug相对较多不断添加新功能
-   纯数字版

对于这些版本，大家只需要简单认识下即可。

## 5，多环境配置与应用

### 5.1 多环境开发

开发测试生产三个环境，使用不同的数据库url。 

![](https://i-blog.csdnimg.cn/blog_migrate/bafb74df65e0fde010ae49a27cde46ba.png)

-   我们平常都是在自己的开发环境进行开发，
-   当**开发完成**后，需要把开发的功能**部署到测试环境供测试人员进行测试使用**，
-   等测试人员测试通过后，我们会将项目**部署到生成环境上线使用**。
-   这个时候就有一个问题是，**不同环境的配置是不相同的**，如不可能让三个环境都用一个数据库，所以**就会有三个数据库的url配置。**

> **思考：**
> 
> -   我们在项目中如何配置?
> -   要想实现不同环境之间的配置切换又该如何来实现呢?
> 
> 答案：maven提供配置多种环境的设定，帮助开发者在使用过程中快速切换环境。

**具体实现步骤:**

**步骤1:父工程配置多个环境,并指定默认激活环境，profiles轮廓，配置文件**

首先将上面配置的全局属性**<jdbc.url> 注释掉**，然后在profile定义此开发环境专用属性：

```XML
    <properties>
        <spring.version>5.2.10.RELEASE</spring.version>
        <junit.version>4.12</junit.version>
<!--        <jdbc.url>jdbc:mysql://localhost:3306/ssm_db?useSSL=false</jdbc.url>-->
    </properties>
```

```XML
<profiles>
    <!--开发环境env_dep-->
    <profile>
        <id>env_dep</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
        </properties>
        <!--设定是否为默认启动环境-->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <!--生产环境env_pro-->
    <profile>
        <id>env_pro</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.2.2.2:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
    <!--测试环境env_test-->
    <profile>
        <id>env_test</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.3.3.3:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
</profiles>
```

**步骤2:执行安装查看env\_dep环境是否生效**

![](https://i-blog.csdnimg.cn/blog_migrate/7d8bc33bf1abf7b613d74b963823b7a7.png)

![](https://i-blog.csdnimg.cn/blog_migrate/f8c58a5bda90184bfe31db9ee95b9de4.png)

查看到的结果为:

![](https://i-blog.csdnimg.cn/blog_migrate/ecf49cfd57bda08624c23b5b3e815563.png)

**步骤3:切换默认环境为生产环境**

```XML
<profiles>
    <!--开发环境-->
    <profile>
        <id>env_dep</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
    <!--生产环境-->
    <profile>
        <id>env_pro</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.2.2.2:3306/ssm_db</jdbc.url>
        </properties>
        <!--设定是否为默认启动环境-->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <!--测试环境-->
    <profile>
        <id>env_test</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.3.3.3:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
</profiles>
```

**步骤4:执行安装并查看env\_pro环境是否生效**

查看到的结果为`jdbc:mysql://127.2.2.2:3306/ssm_db`

![](https://i-blog.csdnimg.cn/blog_migrate/d474026ff82893fd0c27d1acc61010ff.png)

虽然已经能够实现不同环境的切换，但是每次切换都是需要手动修改，如何来实现在不改变代码的前提下完成环境的切换呢?

**步骤5:命令行实现环境切换**

![](https://i-blog.csdnimg.cn/blog_migrate/3a02e1361d2c9bad9c512d510d7d0f8d.png)

**步骤6:执行安装并查看env\_test环境是否生效**

查看到的结果为`jdbc:mysql://127.3.3.3:3306/ssm_db`

![](https://i-blog.csdnimg.cn/blog_migrate/f82a151c4ae3999b6d7f90a5f2246c94.png)

> **小结：**
> 
> -   父工程中定义多环境
>     
>     ```XML
>     <profiles>
>     	<profile>
>         	<id>环境名称</id>
>             <properties>
>             	<key>value</key>
>             </properties>
>             <activation>
>             	<activeByDefault>true</activeByDefault>
>             </activation>
>         </profile>
>         ...
>     </profiles>
>     ```
>     
> -   使用多环境(构建过程)
>     
>     ```
>     mvn 指令 -P 环境定义ID[环境定义中获取]
>     ```
>     

### 5.2 跳过测试

**在多环境开发中，执行`install安装`指令的时候**，Maven都会按照顺序从上往下依次执行，**每次都会执行测试**`**tes**t：` 

![](https://i-blog.csdnimg.cn/blog_migrate/0bd87177467cbbe184827f88dfd3f801.png)

**不需要测试的情况：**

-   可以确保**每次打包或者安装**的时候，**程序的正确性**，假如测试已经通过在我们没有修改程序的前提下再次执行打包或安装命令，由于顺序执行，测试会被再次执行，就有点**耗费时间**了。
-   功能开发过程中有**部分模块还没有开发完毕**，**测试无法通过**，但是想要把其中**某一部分进行快速打包**，此时由于**测试环境失败就会导致打包失败**。

遇到上面这些情况的时候，我们就想跳过测试执行下面的构建命令，具体实现方式有三种：

#### 方式一:IDEA工具实现跳过测试按钮

![](https://i-blog.csdnimg.cn/blog_migrate/1d81072ae85db86e37e49c9bdfa4d758.png)

图中的按钮为`Toggle 'Skip Tests' Mode`,选中状态是跳过测试，生命周期中的test变成灰色。

Toggle翻译为切换的意思，也就是说在测试与不测试之间进行切换。

点击一下，出现测试画横线的图片，如下:

![](https://i-blog.csdnimg.cn/blog_migrate/a38ad10dd0118200b9e811a139c32496.png)

说明测试已经被关闭，再次点击就会恢复。

这种方式**最简单，但是有点"暴力"**，会把所有的测试都跳过，如果我们想更精细的控制哪些跳过哪些不跳过，就需要使用配置插件的方式。

#### 方式二:配置插件实现跳过测试

先找到测试插件名称：maven-surefire-plugin，surefire译为一定成功的

![](https://i-blog.csdnimg.cn/blog_migrate/ed19a52c23f998789a371e14685028a9.png)

在父工程中的pom.xml中添加测试插件配置

```XML
<build>
    <plugins>
        <plugin>
            <!--maven测试插件，因为是内部插件，所以不用提高groupId-->
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.12.4</version>
            <configuration>
                <skipTests>false</skipTests>
                <!--排除掉不参与测试的内容-->
                <excludes>
                    <exclude>**/BookServiceTest.java</exclude>
                </excludes>
            </configuration>
        </plugin>
    </plugins>
</build>
```

**skipTests:**如果为**true，则跳过所有测试**，如果为**false，则不跳过测试**

**excludes：**哪些测试类不参与测试，即排除，针对skipTests为false来设置的

**includes:** 哪些测试类要参与测试，即包含,针对skipTests为true来设置的

#### 方式三:命令行跳过测试

![](https://i-blog.csdnimg.cn/blog_migrate/9bee7f70212f81df44e1256520b79f51.png)

使用Maven的命令行，`mvn 指令 -D skipTests`

注意事项:

-   执行的项目构建指令必须包含测试生命周期，否则无效果。例如执行compile生命周期，不经过test生命周期。
-   **该命令可以不借助IDEA，直接使用cmd命令行进行跳过测试**，需要注意的是cmd要在pom.xml所在目录下进行执行。

## 6，私服

### 6.1 私服简介

**团队开发现状分析**

![](https://i-blog.csdnimg.cn/blog_migrate/6eeeb8d77caba047de707d45ec3e81c7.png)

(1)张三负责ssm\_crm的开发，自己写了一个ssm\_pojo模块，要想使用直接将ssm\_pojo安装到本地仓库即可

(2)李四负责ssm\_order的开发，需要用到张三所写的ssm\_pojo模块，这个时候如何将张三写的ssm\_pojo模块交给李四呢?

(3)如果直接拷贝，那么团队之间的jar包管理会非常混乱而且容器出错，这个时候我们就想能不能将写好的项目上传到中央仓库，谁想用就直接联网下载即可

(4)Maven的中央仓库不允许私人上传自己的jar包,那么我们就得换种思路，**自己搭建一个类似于中央仓库的东西，把自己的内容上传上去，其他人就可以从上面下载jar包使用**

(5)这个**类似于中央仓库的东西**就是我们接下来要学习的**私服**

所以到这就有两个概念，一个是私服，一个是中央仓库

**私服:公司内部搭**建的用于**存储Maven资源**的**服务器**

**远程仓库（中央仓库）:**Maven开发团队维护的用于存储Maven资源的服务器

所以说:

-   私服是一台独立的服务器，用于解决团队内部的资源共享与资源同步问题

搭建Maven私服的方式有很多，我们来介绍其中一种使用量比较大的实现方式:

-   **私服产品Nexus**
    
    -   Sonatype公司的一款maven私服产品
    -   下载地址：[Download](https://help.sonatype.com/repomanager3/download "Download")

### **6.2 私服安装**

**步骤1:下载解压**

点击上面地址，用科技下的更快。

![](https://i-blog.csdnimg.cn/blog_migrate/b0e9d45d1c72391350c0979d15d3624a.png)

将`资料\latest-win64.zip`解压到一个**路径没有中文**的空目录下，注意两个文件都要有：

![](https://i-blog.csdnimg.cn/blog_migrate/89e3ee1820fab1ff30bf057c8347e608.png)

**步骤2:启动Nexus**

![](https://i-blog.csdnimg.cn/blog_migrate/aa6c905e5447b916972f7d5c1132bd24.png)

使用cmd进入到解压目录下的`nexus-3.30.1-01\bin`,执行如下命令**启动nexus服务器**:

> tip：进入此文件夹，路径框输入cmd回车，可直接进入本路径的cmd：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/4cb0f4a1424aca624e693e8ebb42f1c2.png)

```
nexus.exe /run nexus
```

看到如下内容，说明启动成功。

![](https://i-blog.csdnimg.cn/blog_migrate/b0008a945a2f9bc8267f91e774f231af.png)

**步骤3:浏览器访问**

访问地址为:

```
http://localhost:8081
```

![](https://i-blog.csdnimg.cn/blog_migrate/922e3c8e180e73b9e80fb1c8768e16d4.png)

**步骤4:首次登录重置密码**

根据登录提示进入文件查看初始密码 ：

![](https://i-blog.csdnimg.cn/blog_migrate/49728bfd50c91ac8f85187e0635febea.png)

输入用户名和密码进行登录，登录成功后，出现如下页面

![](https://i-blog.csdnimg.cn/blog_migrate/230888efa136b19af8d80ce744501615.png)

点击下一步，需要重新输入新密码，为了和后面的保持一致，密码修改为`admin`

![](https://i-blog.csdnimg.cn/blog_migrate/3fa9effa2a7f8bdf3192d0353a4875bf.png)

设置是否运行匿名访问

![](https://i-blog.csdnimg.cn/blog_migrate/2f27b6a21799f882824888ba814883c4.png)

点击完成

![](https://i-blog.csdnimg.cn/blog_migrate/24d1e74db3a14c82b1c731558a27b07e.png)

至此私服就已经安装成功。如果要想修改一些基础配置信息，可以使用:

-   修改基础配置信息
    
    -   安装路径下etc目录中nexus-default.properties文件保存有nexus基础配置信息，例如默认访问端口。![](https://i-blog.csdnimg.cn/blog_migrate/d16cee61e0776ba0a128a3077d1f7c13.png)
    
-   修改服务器运行配置信息
    
    -   安装路径下bin目录中nexus.vmoptions文件保存有nexus服务器启动对应的配置信息，例如默认占用内存空间。![](https://i-blog.csdnimg.cn/blog_migrate/0ba99b9466455c0fa7e13ab12e49fec9.png)
    

### 6.3 私服仓库分类

私服资源操作流程分析:

(1)在**没有私服**的情况下，我们自己**创建的服务都是安装在Maven的本地仓库中**

(2)**私服中也有仓库**，我们要把自己的资源上传到私服，最终也是**放在私服的仓库**中

(3)其他人要想使用你所上传的资源，就需要从私服的仓库中获取

(4)当我们要使用的资源不是自己写的，是**远程中央仓库有的第三方jar包**，这个时候就需要**从远程中央仓库下载**，每个开发者都去远程中央仓库下速度比较慢(中央仓库服务器在国外)

(5)**私服就再准备一个仓库**，用来**专门存储从远程中央仓库下载的第三方jar包**，第一次访问没有就会去远程中央仓库下载，**下次再访问就直接走私服下载**

(6)前面在介绍版本管理的时候提到过有**`SNAPSHOT`和`RELEASE`**，如果把这两类的都放到同一个仓库，比较混乱，所以**私服就把这两个种jar包放入不同的仓库**

(7)上面**我们已经介绍了有三种仓库**，**一种是存放`SNAPSHOT`的，一种是存放`RELEASE`还有一种是存放从远程仓库下载的第三方jar包**，那么我们在获取资源的时候要从哪个仓库种获取呢?

(8)为了方便获取，我们**将所有的仓库编成一个组**，我们只需要**访问仓库组去获取资源**。

![](https://i-blog.csdnimg.cn/blog_migrate/7c9240584121967b90651c65580fe8ba.png)

**所有私服仓库总共分为三大类:**

**宿主仓库hosted**

-   小组内自己用的
    
-   保存**无法从中央仓库获取的资源**
    
    -   自主研发
    -   第三方非开源项目,比如Oracle,因为是付费产品，所以中央仓库没有

**代理仓库proxy**

-   所有项目组公用的
-   代理远程仓库，转调中央仓库，通过nexus访问其他公共仓库，例如中央仓库

**仓库组group**

-   小组内共享资源使用的。
-   将若干个仓库组成一个群组，用来打包下载，简化配置
-   **仓库组不能保存资源，属于设计型仓库**

![](https://i-blog.csdnimg.cn/blog_migrate/5a2a6621eb6c8f8c5a1d3d52f7ac0fb7.png)

### 6.4 本地仓库访问私服配置

-   我们通过**IDEA将开发的模块上传到私服**，中间是要**经过本地Maven**的
-   **本地Maven**需要知道**私服的访问地址以及私服访问的用户名和密码**
-   私服中的仓库很多，Maven最终要把资源上传到哪个仓库?
-   Maven下载的时候，又需要**携带用户名和密码到私服上找对应的仓库组进行下载**，然后再给IDEA

![](https://i-blog.csdnimg.cn/blog_migrate/733db5d005436b72be460640d4446d53.png)

上面所说的这些内容，我们需要在本地Maven的**配置文件`settings.xml`**中进行配置。

**步骤1:私服上配置仓库**

创建名为xxx-snapshot和xxx-release**宿主仓库hosted**

![](https://i-blog.csdnimg.cn/blog_migrate/5f1f5196f8197447f360d712e9686839.png)

**说明:**

第5，6步骤是创建itheima-snapshot仓库

第7，8步骤是创建itheima-release仓库

**步骤2:配置本地Maven对私服的访问权限**

在本地Maven的**配置文件`settings.xml`**中进行配置 

```XML
<servers>
    <server>
        <id>itheima-snapshot</id>
        <username>admin</username>
        <password>admin</password>
    </server>
    <server>
        <id>itheima-release</id>
        <username>admin</username>
        <password>admin</password>
    </server>
</servers>
```

**步骤3:配置私服的访问路径**

在本地Maven的**配置文件`settings.xml`**中进行配置 

![](https://i-blog.csdnimg.cn/blog_migrate/ca73fcae18ca17ea6b504c05431c4536.png)

```XML
<mirrors>
    <mirror>
        <!--配置仓库组的ID-->
        <id>maven-public</id>
        <!--*代表所有内容都从私服获取-->
        <mirrorOf>*</mirrorOf>
        <!--私服仓库组maven-public的访问路径-->
        <url>http://localhost:8081/repository/maven-public/</url>
    </mirror>
</mirrors>
```

为了避免阿里云Maven私服地址的影响，建议先将之前配置的阿里云Maven私服镜像地址注释掉，等练习完后，再将其恢复。

![](https://i-blog.csdnimg.cn/blog_migrate/bb76f7bd871b3228c1920d328d1ac0ff.png)

至此本地仓库就能与私服进行交互了。

### 6.5 私服资源上传与下载

本地仓库与私服已经建立了连接，接下来我们就需要往私服上上传资源和下载资源，具体的实现步骤为:

#### 步骤1:配置工程上传私服的具体位置

```XML
 <!--配置当前工程保存在私服中的具体位置-->
<distributionManagement>
    <repository>
        <!--和maven/settings.xml中server中的id一致，表示使用该id对应的用户名和密码-->
        <id>itheima-release</id>
         <!--release版本上传仓库的具体地址-->
        <url>http://localhost:8081/repository/itheima-release/</url>
    </repository>
    <snapshotRepository>
        <!--和maven/settings.xml中server中的id一致，表示使用该id对应的用户名和密码-->
        <id>itheima-snapshot</id>
        <!--snapshot版本上传仓库的具体地址-->
        <url>http://localhost:8081/repository/itheima-snapshot/</url>
    </snapshotRepository>
</distributionManagement>
```

#### 步骤2:发布资源到私服

![](https://i-blog.csdnimg.cn/blog_migrate/5fc5ba724880a2ce532c6fba194b7a8d.png)

或者执行Maven命令

```
mvn deploy
```

> **注意:**
> 
> **要发布的项目都需要配置分配管理`distributionManagement`标签**，要么在自己的pom.xml中配置，要么**在其父项目中配置**，然后子项目中继承父项目即可。

发布成功，在私服中就能看到:

![](https://i-blog.csdnimg.cn/blog_migrate/0de4c85cf710be83f0ea04efdc2536b8.png)

 **发布release版本：**

**现在发布是在itheima-snapshot仓库**中，如果**想发布到itheima-release仓库**中就需要将父工程和子模块parent标签里继承父工程parent中的version修改成RELEASE即可。

 **删除私服仓库里资源**

如果想删除已经上传的资源，可以在界面上进行删除操作:

![](https://i-blog.csdnimg.cn/blog_migrate/9832f6de0923895aa59d1d5345e8f162.png)

**私服配置阿里云镜像：** 

如果私服中没有对应的jar，会去中央仓库下载，速度很慢。可以配置让私服去阿里云中下载依赖。

![](https://i-blog.csdnimg.cn/blog_migrate/ea1f0100897ab31992ccae695bdb5c11.png)

至此私服的搭建就已经完成，相对来说有点麻烦，但是步骤都比较固定，后期大家如果需要的话，就可以参考上面的步骤一步步完成搭建即可。