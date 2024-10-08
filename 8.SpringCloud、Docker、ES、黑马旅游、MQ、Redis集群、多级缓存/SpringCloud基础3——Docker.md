>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1.初识Docker](#1.%E5%88%9D%E8%AF%86Docker)

[1.1.什么是Docker](#1.1.%E4%BB%80%E4%B9%88%E6%98%AFDocker)

[1.1.1.应用部署的环境问题](#1.1.1.%E5%BA%94%E7%94%A8%E9%83%A8%E7%BD%B2%E7%9A%84%E7%8E%AF%E5%A2%83%E9%97%AE%E9%A2%98)

[1.1.2.Docker解决依赖兼容问题](#1.1.2.Docker%E8%A7%A3%E5%86%B3%E4%BE%9D%E8%B5%96%E5%85%BC%E5%AE%B9%E9%97%AE%E9%A2%98)

[1.1.3.Docker解决操作系统环境差异](#1.1.3.Docker%E8%A7%A3%E5%86%B3%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E7%8E%AF%E5%A2%83%E5%B7%AE%E5%BC%82)

[1.1.4.小结](#1.1.4.%E5%B0%8F%E7%BB%93)

[1.2.Docker和虚拟机的区别](#1.2.Docker%E5%92%8C%E8%99%9A%E6%8B%9F%E6%9C%BA%E7%9A%84%E5%8C%BA%E5%88%AB)

[1.3.Docker架构](#1.3.Docker%E6%9E%B6%E6%9E%84)

[1.3.1.镜像和容器](#1.3.1.%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%B9%E5%99%A8)

[1.3.2.DockerHub](#1.3.2.DockerHub)

[1.3.3.Docker架构](#1.3.3.Docker%E6%9E%B6%E6%9E%84)

[1.3.4.小结镜像、容器、结构、dockerhub](#1.3.4.%E5%B0%8F%E7%BB%93)

[1.4.CentOS安装Docker](#1.4.CentOS%E5%AE%89%E8%A3%85Docker)

[1.4.1.卸载（可选）](#1.4.1.%E5%8D%B8%E8%BD%BD%EF%BC%88%E5%8F%AF%E9%80%89%EF%BC%89)

[1.4.2.安装docker](#1.4.2.%E5%AE%89%E8%A3%85docker)

[1.4.3.启动docker](#1.4.3.%E5%90%AF%E5%8A%A8docker)

[1.4.4.配置镜像加速](#1.4.4.%E9%85%8D%E7%BD%AE%E9%95%9C%E5%83%8F%E5%8A%A0%E9%80%9F)

[1.4.5 设置开机启动docker](#1.4.5%20%E8%AE%BE%E7%BD%AE%E5%BC%80%E6%9C%BA%E5%90%AF%E5%8A%A8docker)

[2.Docker的基本操作](#2.Docker%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%93%8D%E4%BD%9C)

[2.1.镜像操作](#2.1.%E9%95%9C%E5%83%8F%E6%93%8D%E4%BD%9C)

[2.1.1.镜像名称](#2.1.1.%E9%95%9C%E5%83%8F%E5%90%8D%E7%A7%B0)

[2.1.2.镜像命令](#2.1.2.%E9%95%9C%E5%83%8F%E5%91%BD%E4%BB%A4)

[2.1.3.案例1-拉取、查看镜像](#2.1.3.%E6%A1%88%E4%BE%8B1-%E6%8B%89%E5%8F%96%E3%80%81%E6%9F%A5%E7%9C%8B%E9%95%9C%E5%83%8F)

[2.1.4.案例2-保存、导入镜像](#2.1.4.%E6%A1%88%E4%BE%8B2-%E4%BF%9D%E5%AD%98%E3%80%81%E5%AF%BC%E5%85%A5%E9%95%9C%E5%83%8F)

[2.2.容器操作](#2.2.%E5%AE%B9%E5%99%A8%E6%93%8D%E4%BD%9C)

[2.2.1.容器相关命令](#2.2.1.%E5%AE%B9%E5%99%A8%E7%9B%B8%E5%85%B3%E5%91%BD%E4%BB%A4)

[2.2.2.案例-创建并运行容器，run](#2.2.2.%E6%A1%88%E4%BE%8B-%E5%88%9B%E5%BB%BA%E5%B9%B6%E8%BF%90%E8%A1%8C%E4%B8%80%E4%B8%AA%E5%AE%B9%E5%99%A8)

[2.2.2.5. 查看容器状态、日志](#2.2.2.5.%20%E6%9F%A5%E7%9C%8B%E5%AE%B9%E5%99%A8%E7%8A%B6%E6%80%81%E3%80%81%E6%97%A5%E5%BF%97)

[2.2.3.案例-进入容器，修改文件（不建议）](#2.2.3.%E6%A1%88%E4%BE%8B-%E8%BF%9B%E5%85%A5%E5%AE%B9%E5%99%A8%EF%BC%8C%E4%BF%AE%E6%94%B9%E6%96%87%E4%BB%B6)

[2.2.4.停止、删除容器](#2.2.4.%E5%B0%8F%E7%BB%93)

[2.2.5.创建redis容器](#2.2.5.%E5%88%9B%E5%BB%BAredis%E5%AE%B9%E5%99%A8)

[2.2.5.小结](#2.2.5.%E5%B0%8F%E7%BB%93)

[2.3.数据卷（容器数据管理）](#2.3.%E6%95%B0%E6%8D%AE%E5%8D%B7%EF%BC%88%E5%AE%B9%E5%99%A8%E6%95%B0%E6%8D%AE%E7%AE%A1%E7%90%86%EF%BC%89)

[2.3.1.什么是数据卷](#2.3.1.%E4%BB%80%E4%B9%88%E6%98%AF%E6%95%B0%E6%8D%AE%E5%8D%B7)

[2.3.2.数据卷操作命令](#2.3.2.%E6%95%B0%E6%8D%AE%E9%9B%86%E6%93%8D%E4%BD%9C%E5%91%BD%E4%BB%A4)

[2.3.3.创建和查看数据卷](#2.3.3.%E5%88%9B%E5%BB%BA%E5%92%8C%E6%9F%A5%E7%9C%8B%E6%95%B0%E6%8D%AE%E5%8D%B7)

[2.3.4.挂载数据卷、宿主机目录，-v](#2.3.4.%E6%8C%82%E8%BD%BD%E6%95%B0%E6%8D%AE%E5%8D%B7)

[2.3.5.案例-给nginx挂载数据卷](#2.3.5.%E6%A1%88%E4%BE%8B-%E7%BB%99nginx%E6%8C%82%E8%BD%BD%E6%95%B0%E6%8D%AE%E5%8D%B7)

[2.3.6.docker安装MySQL，挂载本地目录](#2.3.6.%E6%A1%88%E4%BE%8B-%E7%BB%99MySQL%E6%8C%82%E8%BD%BD%E6%9C%AC%E5%9C%B0%E7%9B%AE%E5%BD%95)

[2.3.7.小结](#2.3.7.%E5%B0%8F%E7%BB%93)

[3.Dockerfile自定义镜像](#3.Dockerfile%E8%87%AA%E5%AE%9A%E4%B9%89%E9%95%9C%E5%83%8F)

[3.1.镜像结构](#3.1.%E9%95%9C%E5%83%8F%E7%BB%93%E6%9E%84)

[3.2.Dockerfile语法](#3.2.Dockerfile%E8%AF%AD%E6%B3%95)

[3.3.使用Dockerfile构建Java项目的镜像](#3.3.%E6%9E%84%E5%BB%BAJava%E9%A1%B9%E7%9B%AE)

[3.3.1.基于Ubuntu构建Java项目（不推荐）](#3.3.1.%E5%9F%BA%E4%BA%8EUbuntu%E6%9E%84%E5%BB%BAJava%E9%A1%B9%E7%9B%AE)

[3.3.2.基于java8构建Java项目（推荐）](#3.3.2.%E5%9F%BA%E4%BA%8Ejava8%E6%9E%84%E5%BB%BAJava%E9%A1%B9%E7%9B%AE)

[3.4.小结](#3.4.%E5%B0%8F%E7%BB%93)

[4.Docker-Compose，部署分布式项目](#4.Docker-Compose)

[4.1.初识DockerCompose](#4.1.%E5%88%9D%E8%AF%86DockerCompose)

[4.2.安装DockerCompose](#4.2.%E5%AE%89%E8%A3%85DockerCompose)

[4.2.1.下载](#4.2.1.%E4%B8%8B%E8%BD%BD)

[4.2.2.修改文件权限](#4.2.2.%E4%BF%AE%E6%94%B9%E6%96%87%E4%BB%B6%E6%9D%83%E9%99%90)

[4.2.3.Base自动补全命令：](#4.2.3.Base%E8%87%AA%E5%8A%A8%E8%A1%A5%E5%85%A8%E5%91%BD%E4%BB%A4%EF%BC%9A)

[4.3.部署微服务集群](#4.3.%E9%83%A8%E7%BD%B2%E5%BE%AE%E6%9C%8D%E5%8A%A1%E9%9B%86%E7%BE%A4)

[4.3.1.初始compose、Dockerfile介绍](#4.3.1.compose%E6%96%87%E4%BB%B6)

[4.3.2.修改微服务配置，localhost改服务名](#4.3.2.%E4%BF%AE%E6%94%B9%E5%BE%AE%E6%9C%8D%E5%8A%A1%E9%85%8D%E7%BD%AE)

[4.3.3.所有服务打包成app.jar](#4.3.3.%E6%89%93%E5%8C%85)

[4.3.4.拷贝jar包到部署目录](#4.3.4.%E6%8B%B7%E8%B4%9Djar%E5%8C%85%E5%88%B0%E9%83%A8%E7%BD%B2%E7%9B%AE%E5%BD%95)

[4.3.5.部署](#4.3.5.%E9%83%A8%E7%BD%B2)

[5.Docker镜像仓库](#5.Docker%E9%95%9C%E5%83%8F%E4%BB%93%E5%BA%93)

[5.1.搭建私有镜像仓库](#5.1.%E6%90%AD%E5%BB%BA%E7%A7%81%E6%9C%89%E9%95%9C%E5%83%8F%E4%BB%93%E5%BA%93)

[5.1.1.简化版镜像仓库](#5.1.1.%E7%AE%80%E5%8C%96%E7%89%88%E9%95%9C%E5%83%8F%E4%BB%93%E5%BA%93)

[5.1.2.带有图形化界面版本](#5.1.2.%E5%B8%A6%E6%9C%89%E5%9B%BE%E5%BD%A2%E5%8C%96%E7%95%8C%E9%9D%A2%E7%89%88%E6%9C%AC)

[5.2.推送、拉取镜像](#5.2.%E6%8E%A8%E9%80%81%E3%80%81%E6%8B%89%E5%8F%96%E9%95%9C%E5%83%8F)

--

## 1.初识Docker

### 1.1.什么是Docker

docker译为容器。

**Docker 是一个**开源的**应用容器引擎**，让**开发者可以打包**他们的**应用以及依赖包到**一个可移植的**镜像**中，然后发布到任何流行的 [Linux](https://baike.baidu.com/item/Linux?fromModule=lemma_inlink "Linux")或[Windows](https://baike.baidu.com/item/Windows/165458?fromModule=lemma_inlink "Windows")操作系统的机器上，也可以实现[虚拟化](https://baike.baidu.com/item/%E8%99%9A%E6%8B%9F%E5%8C%96/547949?fromModule=lemma_inlink "虚拟化")。容器是完全使用[沙箱](https://baike.baidu.com/item/%E6%B2%99%E7%AE%B1/393318?fromModule=lemma_inlink "沙箱")机制，相互之间不会有任何接口。 

微服务虽然具备各种各样的优势，但服务的拆分通用给部署带来了很大的麻烦。

-   **分布式系统中，依赖的组件非常多**，不同组件之间部署时往往会产生一些**冲突**。
-   在数百上千台服务中**重复部署，环境**不一定一致，会遇到各种问题

#### 1.1.1.应用部署的环境问题

大型项目组件较多，运行环境也较为复杂，部署时会碰到一些问题：

-   依赖关系复杂，容易出现兼容性问题
    
-   开发、测试、生产环境有差异
    

![image-20210731141907366](https://i-blog.csdnimg.cn/blog_migrate/f3b0915799f69eb3ead191c726dffa80.png)

例如一个项目中，部署时需要依赖于node.js、Redis、RabbitMQ、MySQL等，这些服务部署时所需要的函数库、依赖项各不相同，甚至会有冲突。给部署带来了极大的困难。

#### 1.1.2.Docker解决依赖兼容问题

而**Docker巧妙的解决了这些问题**，Docker是如何实现的呢？

Docker为了**解决依赖的兼容问题**的，采用了两个手段：

-   **将应用的Libs（函数库）、Deps（依赖）、配置与应用一起打包**
    
-   **将每个应用放到一个隔离容器去运行，避免互相干扰**
    

![image-20210731142219735](https://i-blog.csdnimg.cn/blog_migrate/419adebbcfae010bb6220e16db37a7bb.png)

这样打包好的应用包中，既包含应用本身，也保护应用所需要的Libs、Deps，无需再操作系统上安装这些，自然就不存在不同应用之间的兼容问题了。

> 虽然解决了不同应用的兼容问题，但是开发、测试等环境会存在差异，操作系统版本也会有差异，怎么解决这些问题呢？

#### 1.1.3.Docker解决操作系统环境差异

要解决不同操作系统环境差异问题，必须先了解操作系统结构。以一个Ubuntu操作系统为例，结构如下：

![image-20210731143401460](https://i-blog.csdnimg.cn/blog_migrate/e5b8beaf2b6f3b29fb537cf2e40c22c5.png)

结构包括：

-   **计算机硬件：**例如CPU、内存、磁盘等
-   **系统内核：**所有Linux发行版的内核都是Linux，例如CentOS、Ubuntu、Fedora等。内核可以与计算机硬件交互，对外提供**内核指令**，用于**操作计算机硬件**。
-   **系统应用：**操作系统本身提供的应用、函数库。这些函数库是对内核指令的封装，使用更加方便。

应用于计算机交互的流程如下：

1）应用调用**操作系统应用**（函数库），实现各种功能

**2）系统函数库**是对内核指令集的封装，会调用内核指令

3）**内核指令**操作计算机硬件

**Ubuntu和CentOSpringBoot**都是基于Linux内核，无非是**系统应用不同，提供的函数库有差异：**

![image-20210731144304990](https://i-blog.csdnimg.cn/blog_migrate/6a09e05c525bccec8fbfe6c866bfcd13.png)

此时，**如果**将一个**Ubuntu版本的MySQL**应用**安装到CentOS系统**，MySQL在调用Ubuntu函数库时，会发现找不到或者不匹配，就会**报错**了：

![image-20210731144458680](https://i-blog.csdnimg.cn/blog_migrate/8578476fa440db60c642082d1a8453a4.png)

**Docker如何解决不同系统环境的问题？**

Docker将**用户程序与**所需要调用的**系统**(比如Ubuntu)**函数库一起打包**，这样**每个程序调用自己打包好的函数库**就不会出现环境问题。Docker运行到不同操作系统时，直接基于打包的函数库，借助于操作系统的Linux内核来运行。

因此，**docker打包好的程序包，可以运行在任何Linux内核的操作系统上。**

如图：

![image-20210731144820638](https://i-blog.csdnimg.cn/blog_migrate/934dfe18f73afa0fbe03a8c7fb72e836.png)

#### 1.1.4.小结

Docker如何解决大型项目依赖关系复杂，不同组件依赖的兼容性问题？

-   Docker允许开发中将应用、依赖、函数库、配置一起**打包**，形成可移植镜像
-   Docker应用运行在容器中，使用沙箱机制，相互**隔离**

Docker如何解决开发、测试、生产环境有差异的问题？

-   **Docker镜像中包含完整运行环境，包括系统函数库**，仅依赖系统的Linux内核，因此可以在任意Linux操作系统上运行

Docker是一个快速交付应用、运行应用的技术，具备下列**优势：**

-   可以将程序及其依赖、运行环境一起**打包为一个镜像**，可以**迁移**到**任意Linux**操作系统
-   运行时利用**沙箱机制形成隔离容器**，各个应用互不干扰
-   启动、移除都可以通过一行命令完成，方便快捷

### 1.2.Docker和虚拟机的区别

Docker可以让一个应用在任何操作系统中非常方便的运行。而以前我们接触的**虚拟机**，**也能在一个操作系统中，运行另外一个操作系统**，保护系统中的任何应用。

两者有什么**差异**呢？

-   **虚拟机**（virtual machine）是在操作系统中**模拟硬件设备**，然后**运行另一个操作系统**，比如在 Windows 系统里面运行 Ubuntu 系统，这样就可以运行任意的Ubuntu应用了。
-   **Docker仅仅是封装函数库**，并没有模拟完整的操作系统，如图：

![image-20210731145914960](https://i-blog.csdnimg.cn/blog_migrate/c91b0b6b2149caf5b00f6795893a83fa.png)

对比来看：

![image-20210731152243765](https://i-blog.csdnimg.cn/blog_migrate/fb0b1040015c83d3547a32595a334672.png)

小结：

**Docker和虚拟机的差异：**

-   **docker是一个系统进程**；**虚拟机是**在操作系统中的**操作系统**
    
-   **docker体积小、启动速度快、性能好**；虚拟机体积大、启动速度慢、性能一般
    

### 1.3.Docker架构

#### 1.3.1.镜像和容器

Docker中有几个重要的概念：

**镜像（Image）**：Docker将**应用程序**及其所需的**依赖、函数库、环境、配置**等文件**打包**在一起，称为镜像。

**容器（Container）**：**镜像中的应用程序运行后形成的进程**就是**容器**，只是Docker会给容器进程做隔离，**对外不可见**。

一切应用最终都是代码组成，都是硬盘中的一个个的字节形成的**文件**。只有运行时，才会加载到内存，形成进程。

而**镜像**，就是把一个应用在硬盘上的文件、及其运行环境、部分系统函数库文件一起打包形成的文件包。

**每个文件包（镜像）是只读的，每个容器是可读写的，所以镜像不会被干扰。**可以基于镜像去创建容器，然后在每个容器里记录日志等数据。

**容器**，就是**将这些文件中**编写的**程序、函数加载到内存中**允许，形成进程，只不过要**隔离**起来。因此**一个镜像可以启动多次**，形成多个容器进程。

![image-20210731153059464](https://i-blog.csdnimg.cn/blog_migrate/9fa62e74a6a0ead46d37aed36c5b5411.png)

例如你下载了一个QQ，如果我们将QQ在磁盘上的运行**文件**及其运行的操作系统依赖打包，形成QQ镜像。然后你可以启动多次，双开、甚至三开QQ，跟多个妹子聊天。

#### 1.3.2.DockerHub

开源应用程序非常多，打包这些应用往往是重复的劳动。为了避免这些重复劳动，人们就会将自己打包的应用镜像，例如Redis、MySQL镜像放到网络上，共享使用，就像GitHub的代码共享一样。

-   **DockerHub：**DockerHub是一个官方的**Docker镜像的托管平台**。**这样的平台称为Docker注册Docker Registry。**
    
-   国内也有类似于DockerHub 的公开服务，比如 [网易云镜像服务](https://c.163yun.com/hub "网易云镜像服务")、[阿里云镜像库](https://cr.console.aliyun.com/ "阿里云镜像库")等。
    

我们一方面可以将自己的镜像共享到DockerHub，另一方面也可以从DockerHub拉取镜像：

![image-20210731153743354](https://i-blog.csdnimg.cn/blog_migrate/cbee0d84ebbe3a03535f5708da03a22c.png)

#### 1.3.3.Docker架构

我们要使用Docker来操作镜像、容器，就必须要安装Docker。

Docker是一个CS架构的程序，由两部分组成：

-   **服务端(server)：**Docker**守护进程**，负责**处理Docker指令**，管理镜像、容器等
    
-   **客户端(client)：**通过命令或RestAPI**向Docker服务端发送指令**。可以在本地或远程向服务端发送指令。
    

如图：

![image-20210731154257653](https://i-blog.csdnimg.cn/blog_migrate/f1207605397586f97032a69960e33568.png)

docker build是构建镜像，被docker daemon接收处理构建成镜像images。

docker pull拉取镜像，docker daemon从接收指令后，从registry拉取镜像。

docker run创建容器。

#### 1.3.4.小结镜像、容器、结构、dockerhub

**镜像：**

-   将应用程序及其依赖、环境、配置打包在一起

**容器：**

-   镜像运行起来就是容器，一个镜像可以运行多个容器

**Docker结构：**

-   服务端：接收命令或远程请求，操作镜像或容器
    
-   客户端：发送命令或者请求到Docker服务端
    

**DockerHub：**

-   一个镜像托管的服务器，类似的还有阿里云镜像服务，统称为DockerRegistry

### 1.4.CentOS安装Docker

Docker 分为 CE 和 EE 两大版本。CE 即社区版（免费，支持周期 7 个月），EE 即企业版，强调安全，付费使用，支持周期 24 个月。

Docker CE 分为 `stable` `test` 和 `nightly` 三个更新频道。

官方网站上有各种环境下的 [安装指南](https://docs.docker.com/install/ "安装指南")，这里主要介绍 Docker CE 在 CentOS上的安装。

Docker CE 支持 64 位版本 CentOS 7，并且要求内核版本不低于 3.10， CentOS 7 满足最低内核的要求，所以我们在CentOS 7安装Docker。

#### 1.4.1.卸载（可选）

如果之前安装过旧版本的Docker，可以使用下面命令卸载：

```bash
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine \
                  docker-ce
```

#### 1.4.2.安装docker

首先需要大家虚拟机联网，安装yum工具

```
yum install -y yum-utils \
           device-mapper-persistent-data \
           lvm2 --skip-broken
```

然后更新本地镜像源：

```bash
## 1.4.设置docker镜像源
yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    
sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo

yum makecache fast
```

然后输入命令：

```
yum install -y docker-ce
```

docker-ce为社区免费版本。稍等片刻，docker即可安装成功。

#### 1.4.3.启动docker

Docker应用需要用到各种端口，逐一去修改防火墙设置。非常麻烦，因此建议大家直接关闭防火墙！

启动docker前，**一定要关闭防火墙**后！！

启动docker前，一定要关闭防火墙后！！

启动docker前，一定要关闭防火墙后！！

```bash
## 1.4.关闭
systemctl stop firewalld
## 1.4.禁止开机启动防火墙
systemctl disable firewalld
```

通过命令启动docker：

```bash
systemctl start docker  ## 1.4.启动docker服务

systemctl stop docker  ## 1.4.停止docker服务

systemctl restart docker  ## 1.4.重启docker服务
```

然后输入命令，可以查看docker版本：

```
docker -v
```

#### 1.4.4.配置镜像加速

docker官方镜像仓库网速较差，我们需要设置国内镜像服务：

参考阿里云的镜像加速文档：[阿里云登录 - 欢迎登录阿里云，安全稳定的云计算服务平台](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors "阿里云登录 - 欢迎登录阿里云，安全稳定的云计算服务平台")

通过修改daemon配置文件/etc/docker/daemon.json来使用加速器。

**在ssh输入下面命令：**

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://tfa5975m.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

可以看见，多了个/etc/docker/daemon.json文件：

![](https://i-blog.csdnimg.cn/blog_migrate/ce25033b6d6b1777e2a5a77fda739fef.png)

#### 1.4.5 设置开机启动docker

1、查看已经启动的服务

```bash
systemctl list-units --type=service
```

2、查看是否设置开机启动

```bash
systemctl list-unit-files | grep docker
```

3、设置开机启动

```bash
systemctl enable docker.service
```

**设置容器自启**

```
docker update --restart=always 容器名称
```

例如：

```
docker update --restart=always mysql nginx
```

## 2.Docker的基本操作

### 2.1.镜像操作

#### 2.1.1.镜像名称

首先来看下镜像的名称组成：

-   镜名称一般分两部分组成：**\[repository\]:\[tag\]**。
-   在没有指定**tag**时，**默认是latest**，代表**最新版本**的镜像

如图：

![image-20210731155141362](https://i-blog.csdnimg.cn/blog_migrate/c124330d35eea73bfa60cbac39d5cf7e.png)

这里的mysql就是repository，5.7就是tag，合一起就是镜像名称，代表5.7版本的MySQL镜像。

#### 2.1.2.镜像命令

常见的镜像操作命令如图：

![image-20210731155649535](https://i-blog.csdnimg.cn/blog_migrate/c4e5d336b66e8a43f84a2053d972a85a.png)

```bash
 docker pull nginx
```

```bash
docker images
```

```
docker save -o nginx.tar nginx:latest
```

```
docker rmi nginx:latest
```

```
docker load -i nginx.tar
```

#### 2.1.3.案例1-拉取、查看镜像

**需求：从DockerHub中拉取一个nginx镜像并查看**

**1）搜索镜像名称。**首先去镜像仓库搜索nginx镜像，比如[DockerHub](https://hub.docker.com/ "DockerHub"):

![image-20210731155844368](https://i-blog.csdnimg.cn/blog_migrate/ba6088d042269252c71ada7288de5aa7.png)

**2）拉取镜像。**根据查看到的镜像名称，这里拉取官方镜像，通过命令：docker pull nginx

![](https://i-blog.csdnimg.cn/blog_migrate/25b389ea93ea4e330e631d2e55307fac.png)

```bash
 docker pull nginx
```

![image-20210731155856199](https://i-blog.csdnimg.cn/blog_migrate/5e93205fffec921027925f86312d0098.png)

**3）查看镜像。**通过命令：docker images 查看拉取到的镜像

```bash
docker images
```

![image-20210731155903037](https://i-blog.csdnimg.cn/blog_migrate/937ef44c9296d36f3d3e992346f13c8b.png)

#### 2.1.4.案例2-保存、导入镜像

**需求：**利用docker save将**nginx镜像导出磁盘，然后再通过load加载回来**

**1）查看命令用法。**利用**docker xx --help**命令查看docker save和docker load的语法

例如，查看save命令用法，可以输入命令：

```
docker save --help
```

结果：

![image-20210731161104732](https://i-blog.csdnimg.cn/blog_migrate/cd313cded50865b8a3370c22ebba7763.png)

命令格式：

```
docker save -o [保存的目标文件名称] [镜像名称]
```

**2）保存镜像。**使用docker save导出镜像到磁盘

运行命令：

```
docker save -o nginx.tar nginx:latest
```

结果如图：

![image-20210731161354344](https://i-blog.csdnimg.cn/blog_migrate/ee7e93734a3e7797ccf7335403b42368.png)

**3）导入镜像。**使用docker load加载镜像

先删除本地的nginx镜像：

```
docker rmi nginx:latest
```

> rmi是remove image的缩写。

然后运行命令，加载本地文件：

```
docker load -i nginx.tar
```

结果：

![image-20210731161746245](https://i-blog.csdnimg.cn/blog_migrate/4e3a8076f1092b2d7f4f6f79e6fb0652.png)

### 2.2.容器操作

#### 2.2.1.容器相关命令

容器操作的命令如图：

![image-20210731161950495](https://i-blog.csdnimg.cn/blog_migrate/27a0bdd1f4fcde965c7694c72bde4c00.png)

exec是execute的缩写。 

容器保护三个状态：

-   运行：进程正常运行
-   **暂停：**进程暂停，CPU不再运行，**并不释放内存**
-   停止：进程终止，回收进程占用的内存、CPU等资源

其中：

-   **docker run：创建并运行一个容器，处于运行状态**
    
-   **docker pause：让一个运行的容器暂停**
    
-   **docker unpause：让一个容器从暂停状态恢复运行**
    
-   **docker stop：停止一个运行的容器**
    
-   **docker start：让一个停止的容器再次运行**
    
-   **docker rm：删除一个容器**
    

#### 2.2.2.案例-创建并运行容器，run

可以看官方方法启动容器 

[Docker Hub](https://hub.docker.com/_/nginx "Docker Hub")

![](https://i-blog.csdnimg.cn/blog_migrate/67b76dcba7b5041d10f0484515b50b38.png)

**创建并运行nginx容器的命令：**

```bash
#docker run --name 容器名称 -p 主机端口:需要映射的容器端口 -d 镜像名称
docker run --name mn -p 80:80 -d nginx
```

命令解读：

-   docker run ：创建并运行一个容器
-   –name : 给容器起一个名字，比如叫做mn（my\_nginx缩写）
-   **\-p ：将宿主机端口给容器端口映射**，冒号左侧是宿主机端口，右侧是容器端口
-   **\-d：后台运行容器**
-   nginx：镜像名称，例如nginx

> **端口映射详解：**
> 
> 这里的**`-p`**参数，是**将容器端口映射到宿主机端口**。
> 
> 默认情况下，**容器是隔离环境**，我们**不能直接访问到容器的80端口**。
> 
> 现在，将容器的80与宿主机的80关联起来，当我们**访问宿主机的80端口时**，就会被**映射到容器的80**，**这样访问主机的80端口，就相当于访问容器的80端口**。
> 
> ![image-20210731163255863](https://i-blog.csdnimg.cn/blog_migrate/cef8986d434c1c5a8d08edd8bfa97532.png)

**启动容器后生成唯一ID  ：**

![](https://i-blog.csdnimg.cn/blog_migrate/8d504d751697016254336998fd0416f0.png)

**访问主机80端口可以看到Nginx已经运行：**

![](https://i-blog.csdnimg.cn/blog_migrate/da8360b1feff4e0976a01fa5268dcd90.png)

#### 2.2.2.5. 查看容器状态、日志

**查看所有容器运行状态：**

```bash
docker ps
```

![](https://i-blog.csdnimg.cn/blog_migrate/b3ec901b2b868941cc0f6ac31c3e2249.png)**查看日志：**

```bash
docker logs mn
```

**跟踪日志：**

```bash
docker logs -f mn
```

![](https://i-blog.csdnimg.cn/blog_migrate/b569cb2c2a5101712cfce3e5df2db9ad.png)

#### 2.2.3.案例-进入容器，修改文件（不建议）

> **不建议进入容器修改文件，建议用下面2.3的数据卷。** 

**需求**：进入Nginx容器，修改HTML文件内容，添加“传智教育欢迎您”

**提示**：进入容器要用到docker exec命令。

**步骤**：

**1）进入容器。**进入我们刚刚创建的nginx容器的命令为：

```
docker exec -it mn bash
```

> exec是execute执行的缩写。 

 **命令解读：**

-   docker exec ：进入容器内部，执行一个命令
    
-   **\-it :** 给当前进入的**容器创建一个标准输入、输出终端**，允许我们与容器交互
    
-   mn ：要进入的容器的名称
    
-   **bash：进入容器后执行的命令**，bash是一个linux终端交互命令
    

![image-20210731164159811](https://i-blog.csdnimg.cn/blog_migrate/73ae274713783ec4e16a76852d8fe72d.png)

>  **退出容器**
> 
> ```bash
> exit
> ```
> 
> docker容器里命令是阉割版Linux命令，没有ll和vim，有ls。

**2）进入nginx的HTML所在目录** /usr/share/nginx/html

![](https://i-blog.csdnimg.cn/blog_migrate/85d5fcb433118eae6f0bf1a1f807f304.png)

容器内部会模拟一个独立的Linux文件系统，看起来如同一个linux服务器一样：

![image-20210731164159811](https://i-blog.csdnimg.cn/blog_migrate/73ae274713783ec4e16a76852d8fe72d.png)

nginx的环境、配置、运行文件全部都在这个文件系统中，包括我们要修改的html文件。

查看DockerHub网站中的nginx页面，可以知道nginx的html目录位置在`/usr/share/nginx/html`

**进入html目录：**

```
cd /usr/share/nginx/html
```

查看目录下文件：

![image-20210731164455818](https://i-blog.csdnimg.cn/blog_migrate/e3f529cfa1982ecc9064403a64862c9d.png)

**3）修改index.html的内容**

容器内**没有vi命令**，无法直接修改，我们用下面的命令来修改：

```
sed -i -e 's#Welcome to nginx#传智教育欢迎您#g' -e 's#<head>#<head><meta charset="utf-8">#g' index.html
```

在浏览器访问自己的虚拟机地址，例如我的是：http://192.168.150.101，即可看到结果：

![image-20210731164717604](https://i-blog.csdnimg.cn/blog_migrate/c039c27c41c884d75b6e325710671e1d.png)

**4）退出容器**

```bash
exit
```

![](https://i-blog.csdnimg.cn/blog_migrate/7996e40052b92e09bf96231ebcd006e3.png)

#### 2.2.4.停止、删除容器

**停止容器：** 

```bash
#docker stop 容器名
docker stop mn
```

**查看所有容器（包括停止的） ：**

```bash
docker ps -a
```

![](https://i-blog.csdnimg.cn/blog_migrate/afdede48dc9d043b6dbb2ef112ff81fe.png)

**强制删除容器**

```bash
docker rm -f mn
```

![](https://i-blog.csdnimg.cn/blog_migrate/109fafa358515621619919a4e78d6913.png)

#### 2.2.5.创建redis容器

[Docker Hub](https://hub.docker.com/_/redis "Docker Hub")

![](https://i-blog.csdnimg.cn/blog_migrate/16651d3b159d52e46c459ffb69b96791.png)

```bash
docker run --name mr -p 6379:6379 -d redis redis-server --appendonly yes
docker exec -it mr bash
redis-cli
```

#### 2.2.5.小结

docker run命令的常见参数有哪些？

-   –name：指定容器名称
-   \-p：指定端口映射
-   \-d：让容器后台运行

查看容器日志的命令：

-   docker logs
-   添加 -f 参数可以持续查看日志

查看容器状态：

-   docker ps
-   docker ps -a 查看所有容器，包括已经停止的

### 2.3.数据卷（容器数据管理）

在之前的nginx案例中，修改nginx的html页面时，需要进入nginx内部。并且因为没有编辑器，修改文件也很麻烦。

这就是因为**容器与数据（容器内文件）耦合**带来的后果。

![image-20210731172440275](https://i-blog.csdnimg.cn/blog_migrate/31d92db0e3e4ebb5868c3c6756ef00a1.png)

要解决这个问题，**必须将数据与容器解耦**，这就要用到**数据卷**了。

#### 2.3.1.什么是数据卷

**数据卷（volume译为卷，容积，音量）**是一个**虚拟目录，指向宿主机文件系统中的某个目录。**

![image-20210731173541846](https://i-blog.csdnimg.cn/blog_migrate/60318031b9afbe1e9c97ee6c237d5259.png)

一旦完成数据卷挂载，**对容器的一切操作都会作用在数据卷对应的宿主机目录了。**

这样，我们操作宿主机的/var/lib/docker/volumes/html目录，就等于操作容器内的/usr/share/nginx/html目录了。只要数据卷对应的宿主机目录在，删除再创建容器，数据依然不变。

#### 2.3.2.数据卷操作命令

数据卷操作的基本语法如下：

```
docker volume [COMMAND]
```

docker volume命令是数据卷操作，根据命令后跟随的command来确定下一步的操作：

-   create 创建一个volume
-   inspect 显示一个或多个volume的信息
-   ls 列出所有的volume
-   prune 删除未使用的volume
-   rm 删除一个或多个指定的volume

![](https://i-blog.csdnimg.cn/blog_migrate/5204e4505df63ddfe42198257383b436.png)

#### 2.3.3.创建和查看数据卷

**需求**：创建一个数据卷，并查看数据卷在宿主机的目录位置

**① 创建数据卷**

```
docker volume create html
```

**② 查看所有数据**

```
docker volume ls
```

结果：

![image-20210731173746910](https://i-blog.csdnimg.cn/blog_migrate/ecb7e35065d13950d30ad12401f329f8.png)

**③ 查看数据卷详细信息卷**

```
docker volume inspect html
```

结果：

![image-20210731173809877](https://i-blog.csdnimg.cn/blog_migrate/3c79a8452e7f9163adeb8258e233eb38.png)

可以看到，我们创建的html这个数据卷关联的宿主机目录为`/var/lib/docker/volumes/html/_data`目录。

> **小结**：
> 
> **数据卷的作用：**
> 
> -   将容器与数据分离，解耦合，方便操作容器内数据，保证数据安全
> 
> **数据卷操作：**
> 
> -   docker volume create：创建数据卷
> -   docker volume ls：查看所有数据卷
> -   docker volume inspect：查看数据卷详细信息，包括关联的宿主机目录位置
> -   docker volume rm：删除指定数据卷
> -   docker volume prune：删除所有未使用的数据卷

#### 2.3.4.挂载数据卷、宿主机目录，-v

**挂载宿主机目录：**

```bash
docker run --name mn -v /root/nginx/html:/usr/share/nginx/html -p 80:80 -d nginx
```

**挂载数据卷** 

我们在创建容器时，可以通过 -v 参数来**挂载一个数据卷到某个容器内目录**，命令格式如下：

```bash
docker run \
  --name mn \
  -v html:/usr/share/nginx/html \
  -p 8080:80 \
  -d nginx 
#docker run --name mn -v html:/usr/share/nginx/html -p 80:80 -d nginx
```

这里的-v就是挂载数据卷的命令：

-   **`-v html:`/usr/share/nginx/html：左边是数据卷名，右边是容器内目录。**把html**数据卷挂载到容器内**的/usr/share/nginx/html这个目录中

可以看到容器内数据通过挂载数据卷指向的目录里，已经出现初始文件。

![](https://i-blog.csdnimg.cn/blog_migrate/4893868f4362f981dfbbedf53402bdda.png)

数据卷挂载与目录直接挂载的

-   **数据卷挂载耦合度低**，由docker来管理目录，但是目录较深，**不好找**
-   **目录挂载耦合度高**，需要我们自己管理目录，不过目录容易**寻找查看**

> **查看数据卷html的信息 ：**
> 
> ```bash
> docker volume inspect html
> ```
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/00350e60372a82c7cce40e0a1d1e6909.png)

#### 2.3.5.案例-给nginx挂载数据卷

**需求**：创建一个nginx容器，修改容器内的html目录内的index.html内容

**分析**：上个案例中，我们进入nginx容器内部，已经知道nginx的html目录所在位置/usr/share/nginx/html ，我们需要把这个目录挂载到html这个数据卷上，方便操作其中的内容。

**提示**：运行容器时使用 -v 参数挂载数据卷

步骤：

**① 创建容器并挂载数据卷到容器内的HTML目录**

```bash
docker run --name mn -v html:/usr/share/nginx/html -p 80:80 -d nginx
```

**② 进入html数据卷指向的宿主机位置，并修改HTML内容**

```bash
# 查看html数据卷的位置
docker volume inspect html
# 进入该目录
cd /var/lib/docker/volumes/html/_data
# 修改文件
vi index.html
```

![](https://i-blog.csdnimg.cn/blog_migrate/d9095950ee321b97d8304e720f72a641.png)

#### 2.3.6.docker安装MySQL，挂载本地目录

**docker安装mysql和直接安装的区别：**

1、docker安装快速，效率高;

2、docker隔离性好，**可以安装无数个mysql实例**，互相不干扰，只要映射主机端口不同即可;

3、占用资源少，MB级别，而服务器安装GB级别;

4、启动速度秒级，而服务器安装启动分钟级别;

5、性能接近原生，而服务器安装较低;

6、数据备份、迁移，docker更方便强大;

7、卸载管理更方便和干净，直接删除容器和镜像即可;

8、稳定性，只要保证docker环境没问题，mysql就没问题。

容器不仅仅可以挂载数据卷，也可以直接挂载到宿主机目录上。关联关系如下：

-   **带数据卷模式：宿主机目录 --> 数据卷 —> 容器内目录**
-   **直接挂载模式：宿主机目录 —> 容器内目录**

如图：

![image-20210731175155453](https://i-blog.csdnimg.cn/blog_migrate/561a229e60ba38009f8b7a63c7e75454.png)

**语法**：

目录挂载与数据卷挂载的语法是类似的：

-   **\-v \[宿主机目录\]:\[容器内目录\]**
-   **\-v \[宿主机文件\]:\[容器内文件\]**

**需求**：创建并运行一个MySQL容器，将宿主机目录直接挂载到容器

实现思路如下：

1）在将课前资料中的mysql.tar文件上传到虚拟机，通过load命令加载为镜像

```bash
docker load -i mysql.tar
```

 也可以拉取

```bash
sudo docker pull mysql:5.7.25
```

2）创建目录/tmp/mysql/data 、/tmp/mysql/conf，将课前资料提供的hmy.cnf上传到/tmp/mysql/conf

```bash
cd /tmp/
mkdir mysql
cd mysql
mkdir data
mkdir conf
cd conf
touch my.cnf
vi my.cnf
```

```bash
[mysqld]
skip-name-resolve
character_set_server=utf8
datadir=/var/lib/mysql
server-id=1000
```

4）去DockerHub查阅资料，创建并运行MySQL容器，要求：

[Docker Hub](https://hub.docker.com/_/mysql "Docker Hub")

**注意端口3306占用问题。** 

```bash
 docker run --name mysql -e MYSQL_ROOT_PASSWORD=1234 -p 3306:3306 -v /tmp/mysql/conf/hmy.cnf:/etc/mysql/conf.d/hmy.cnf -v /tmp/mysql/data:/var/lib/mysql -d mysql:5.7.25
```

![](https://i-blog.csdnimg.cn/blog_migrate/efc457041e148c326673dcfbf7c2838e.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/13ce4fbe529a0e0719f7fbc5eda20eca.png)

使用Navicat可以连接：

![](https://i-blog.csdnimg.cn/blog_migrate/7d5399115a183e8c74fef9c99dd5b0d6.png)

① 挂载/tmp/mysql/data到mysql容器内数据存储目录

② 挂载/tmp/mysql/conf/hmy.cnf到mysql容器的配置文件

③ 设置MySQL密码

#### 2.3.7.小结

docker run的命令中通过 -v 参数挂载文件或目录到容器中：

-   \-v volume名称:容器内目录
-   \-v 宿主机文件:容器内文
-   \-v 宿主机目录:容器内目录

数据卷挂载与目录直接挂载的

-   **数据卷挂载耦合度低**，由docker来管理目录，但是目录较深，**不好找**
-   **目录挂载耦合度高**，需要我们自己管理目录，不过目录容易寻找查看

## 3.Dockerfile自定义镜像

常见的镜像在DockerHub就能找到，但是我们自己写的项目就必须自己构建镜像了。

而要自定义镜像，就必须先了解镜像的结构才行。

### 3.1.镜像结构

**镜像是将应用程序及其需要的系统函数库、环境、配置、依赖打包而成。**

我们以MySQL为例，来看看镜像的组成结构：

![image-20210731175806273](https://i-blog.csdnimg.cn/blog_migrate/7037f58a6cf8b437be191d63725ee382.png)

**分层操作可以提高更新版本时的复用性。** 

简单来说，镜像就是在系统函数库、运行环境基础上，添加应用程序文件、配置文件、依赖文件等组合，然后编写好启动脚本打包在一起形成的文件。

我们要构建镜像，其实就是实现上述打包的过程。

### 3.2.Dockerfile语法

构建自定义的镜像时，并不需要一个个文件去拷贝，打包。

我们只需要告诉Docker，我们的镜像的组成，需要哪些BaseImage、需要拷贝什么文件、需要安装什么依赖、启动脚本是什么，将来Docker会帮助我们构建镜像。

而描述上述信息的文件就是Dockerfile文件。

**Dockerfile就是一个文本文件**，其中**包含**一个个的**指令(Instruction)**，用指令来说明要执行什么操作来构建镜像。**每一个指令都会形成一层Layer**。

![image-20210731180321133](https://i-blog.csdnimg.cn/blog_migrate/afb0b25bed650af7b80fcc062ba43392.png)

更新详细语法说明，请参考官网文档： https://docs.docker.com/engine/reference/builder

### 3.3.使用**Dockerfile**构建Java项目的镜像

#### 3.3.1.基于Ubuntu构建Java项目（不推荐）

需求：基于Ubuntu镜像构建一个新镜像，运行一个java项目

-   **步骤1：新建一个空文件夹docker-demo**
    
    ```bash
    cd /tmp/
    mkdir docker-demo
    cd docker-demo
    ```
    
-   **步骤2：**拷贝课前资料中的docker-demo.jar文件到docker-demo这个目录
    
    ![image-20210801101314816](https://i-blog.csdnimg.cn/blog_migrate/59da96af0134f31461ad677af2836025.png)
    
-   **步骤3：**拷贝课前资料中的jdk8.tar.gz文件到docker-demo这个目录
    
    ![image-20210801101410200](https://i-blog.csdnimg.cn/blog_migrate/28d2c9487ada8adea2c48fe79c1f5851.png)
    
-   步骤4：拷贝课前资料提供的Dockerfile到docker-demo这个目录
    
    ![image-20210801101455590](https://i-blog.csdnimg.cn/blog_migrate/7d745623077f7d83037dd5bc88b943df.png)
    
    其中的内容如下：
    
    ```bash
    # 指定基础镜像
    FROM ubuntu:16.04
    # 配置环境变量，JDK的安装目录
    ENV JAVA_DIR=/usr/local
    
    # 拷贝jdk和java项目的包
    COPY ./jdk8.tar.gz $JAVA_DIR/
    COPY ./docker-demo.jar /tmp/app.jar
    
    # 安装JDK
    RUN cd $JAVA_DIR \
     && tar -xf ./jdk8.tar.gz \
     && mv ./jdk1.8.0_144 ./java8
    
    # 配置环境变量
    ENV JAVA_HOME=$JAVA_DIR/java8
    ENV PATH=$PATH:$JAVA_HOME/bin
    
    # 暴露端口
    EXPOSE 8090
    # 入口，java项目的启动命令
    ENTRYPOINT java -jar /tmp/app.jar
    ```
    
-   步骤5：进入docker-demo
    
    将准备好的docker-demo上传到虚拟机任意目录，然后进入docker-demo目录下
    
-   步骤6：运行命令：
    
    ```bash
    #最后面的空格点别忘了
    docker build -t javaweb:1.0 .
    ```
    

创建容器 

```bash
docker run --name web -p 8090:8090 -d javaweb:1.0
```

最后访问 http://虚拟机ip地址:8090/hello/count，其中的ip改成你的虚拟机ip

#### 3.3.2.基于java8构建Java项目（推荐）

虽然我们可以基于Ubuntu基础镜像，添加任意自己需要的安装包，构建镜像，但是却比较麻烦。所以大多数情况下，我们都可以在一些安装了部分软件的基础镜像上做改造。

例如，构建java项目的镜像，可以在已经准备了JDK的基础镜像基础上构建。

**需求：基于java:8-alpine镜像，将一个Java项目构建为镜像**

实现思路如下：

-   ① 新建一个空的目录，然后在目录中新建一个文件，命名为Dockerfile
    
-   ② 拷贝课前资料提供的docker-demo.jar到这个目录中
    
-   ③ 编写Dockerfile文件：
    
    -   a ）基于java:8-alpine作为基础镜像
        
    -   b ）将app.jar拷贝到镜像中
        
    -   c ）暴露端口
        
    -   d ）编写入口ENTRYPOINT
        
        内容如下：
        
        ```bash
        FROM java:8-alpine
        COPY ./docker-demo.jar /tmp/app.jar
        EXPOSE 8090
        ENTRYPOINT java -jar /tmp/app.jar
        ```
        
-   ④ 使用docker build命令构建镜像
    
    ```bash
    #最后面的空格点别忘了，表示在当前目录下构建镜像
    docker build -t javaweb:2.0 .
    ```
    
-   ⑤ 使用docker run创建容器并运行
    
    ```bash
    docker run --name web -p 8090:8090 -d javaweb:2.0
    ```
    

### 3.4.小结

小结：

1.  Dockerfile的本质是一个文件，通过指令描述镜像的构建过程
    
2.  Dockerfile的第一行必须是FROM，从一个基础镜像来构建
    
3.  基础镜像可以是基本操作系统，如Ubuntu。也可以是其他人制作好的镜像，例如：java:8-alpine
    

## 4.Docker-Compose，部署分布式项目

Docker Compose可以基于Compose文件帮我们快速的部署分布式应用，而无需手动一个个创建和运行容器！

![image-20210731180921742](https://i-blog.csdnimg.cn/blog_migrate/7990f25ed1b1981704722d16a4c6dc9f.png)

### 4.1.初识DockerCompose

compose译为生成，组成，写作。 

Compose文件是一个文本文件，通过指令定义集群中的每个容器如何运行。格式如下：

```bash
version: "3.8"
 services:
  mysql:
    image: mysql:5.7.25
    environment:
     MYSQL_ROOT_PASSWORD: 123 
    volumes:
     - "/tmp/mysql/data:/var/lib/mysql"
     - "/tmp/mysql/conf/hmy.cnf:/etc/mysql/conf.d/hmy.cnf"
#临时构建镜像并运行
  web:
    build: .
    ports:
     - "8090:8090"

```

上面的Compose文件就描述一个项目，其中包含两个容器：

-   mysql：一个基于`mysql:5.7.25`镜像构建的容器，并且挂载了两个目录。这里不需要暴露端口，因为微服务集群部署，集群内部能访问即可，不用暴露。
-   web：一个基于`docker build`临时构建的镜像容器，映射端口时8090

DockerCompose的详细语法参考官网：https://docs.docker.com/compose/compose-file/

其实DockerCompose文件可以看做是将多个docker run命令写到一个文件，只是语法稍有差异。

### 4.2.安装DockerCompose

#### 4.2.1.下载

Linux下需要通过命令下载：

```bash
## 1.4.安装
curl -L https://github.com/docker/compose/releases/download/1.23.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```

如果下载速度较慢，或者下载失败，可以使用课前资料提供的docker-compose文件：

上传到`/usr/local/bin/`目录也可以。

#### 4.2.2.修改文件权限

修改文件权限，给执行权：

```bash
## 1.4.修改权限
chmod +x /usr/local/bin/docker-compose
```

#### 4.2.3.Base自动补全命令：

```bash
## 1.4.补全命令
curl -L http://raw.githubusercontent.com/docker/compose/1.29.1/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose
```

如果这里出现错误，需要修改自己的hosts文件然后重启systemctl restart docke、新建shell窗口：

```
echo "199.232.68.133 raw.githubusercontent.com" >> /etc/hosts
```

### 4.3.部署微服务集群

**需求**：将之前学习的cloud-demo微服务集群利用DockerCompose部署

**实现思路**：

① 查看课前资料提供的cloud-demo文件夹，里面已经编写好了docker-compose文件

② 修改自己的cloud-demo项目，将数据库、nacos地址都命名为docker-compose中的服务名

③ 使用maven打包工具，将项目中的每个微服务都打包为app.jar

④ 将打包好的app.jar拷贝到cloud-demo中的每一个对应的子目录中

⑤ 将cloud-demo上传至虚拟机，利用 docker-compose up -d 来部署

#### 4.3.1.初始compose、Dockerfile介绍

查看课前资料提供的cloud-demo文件夹，里面已经编写好了docker-compose文件，而且每个微服务都准备了一个独立的目录：

![image-20210731181341330](https://i-blog.csdnimg.cn/blog_migrate/d59bab1c4a37a962fc40956bdaae46ae.png)

**docker-compose.yml**内容如下：

```bash
version: "3.2"

services:
  nacos:
    image: nacos/nacos-server
    environment:
#nacos启动命令startup.cmd -m standalone
      MODE: standalone
    ports:
      - "8848:8848"
  mysql:
    image: mysql:5.7.25
    environment:
      MYSQL_ROOT_PASSWORD: 123
    volumes:
      - "$PWD/mysql/data:/var/lib/mysql"
      - "$PWD/mysql/conf:/etc/mysql/conf.d/"
  userservice:
    build: ./user-service
  orderservice:
    build: ./order-service
  gateway:
    build: ./gateway
    ports:
      - "10010:10010"
```

可以看到，其中包含5个service服务：

-   `nacos`：作为注册中心和配置中心
    -   `image: nacos/nacos-server`： 基于nacos/nacos-server镜像构建
    -   `environment`：环境变量
        -   `MODE: standalone`：单点模式启动
    -   `ports`：端口映射，这里暴露了8848端口
-   `mysql`：数据库
    -   `image: mysql:5.7.25`：镜像版本是mysql:5.7.25
    -   `environment`：环境变量
        -   `MYSQL_ROOT_PASSWORD: 123`：设置数据库root账户的密码为123
    -   `volumes`：数据卷挂载，这里挂载了mysql的data、conf目录，其中有我提前准备好的数据
-   `userservice`、`orderservice`、`gateway`：都是基于Dockerfile临时构建的

查看mysql目录，可以看到其中已经准备好了cloud\_order、cloud\_user表：

![image-20210801095205034](https://i-blog.csdnimg.cn/blog_migrate/12eec0d1e734cb39f15a94da93c80d32.png)

查看微服务目录，可以看到都包含Dockerfile文件：

![image-20210801095320586](https://i-blog.csdnimg.cn/blog_migrate/4ceb87c7ca0af4638cf051b5bffff570.png)

内容如下：

```
FROM java:8-alpine
COPY ./app.jar /tmp/app.jar
ENTRYPOINT java -jar /tmp/app.jar
```

#### 4.3.2.修改微服务配置，localhost改服务名

用**docker-compose**部署微服务时，**所有服务之间用服务名互相访问。**

因为微服务将来要部署为docker容器，而容器之间互联不是通过IP地址，而是通过容器名。这里我们将order-service、user-service、gateway服务的mysql、nacos地址都修改为基于容器名的访问。

如下所示：

```bash
spring:
  datasource:
#这里mysql还是有端口的，仅用于服务内调用，docker-compose就不配置端口
    url: jdbc:mysql://mysql:3306/cloud_order?useSSL=false
    username: root
    password: 123
    driver-class-name: com.mysql.jdbc.Driver
  application:
    name: orderservice
  cloud:
    nacos:
      server-addr: nacos:8848 # nacos服务地址
```

#### 4.3.3.所有服务打包成app.jar

接下来需要将我们的每个微服务都打包。因为之前查看到Dockerfile中的jar包名称都是app.jar，因此我们的每个微服务都需要用这个名称。

可以通过修改pom.xml中的打包名称来实现，**除了父工程和feign-api每个微服务的pom都需要修改：** 

```XML
<build>
  <!-- 服务打包的最终名称 -->
  <finalName>app</finalName>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
  </plugins>
</build>
```

打包后：

![image-20210801095951030](https://i-blog.csdnimg.cn/blog_migrate/7f433d172a7bb78b2737d9ad72f35b52.png)

#### 4.3.4.拷贝jar包到部署目录

编译打包好的app.jar文件，需要放到Dockerfile的同级目录中。注意：每个微服务的app.jar放到与服务名称对应的目录，别搞错了。

user-service：

![image-20210801100201253](https://i-blog.csdnimg.cn/blog_migrate/4fdae6b48cd55e441cba89a08686b618.png)

order-service：

![image-20210801100231495](https://i-blog.csdnimg.cn/blog_migrate/9f546371201708a76ed566cf0422f798.png)

gateway：

![image-20210801100308102](https://i-blog.csdnimg.cn/blog_migrate/80e2d2c1e2794539a85b5842dd78c779.png)

#### 4.3.5.部署

最后，我们需要将文件整个cloud-demo文件夹上传到虚拟机中，由DockerCompose部署。

上传到任意目录：

![image-20210801100955653](https://i-blog.csdnimg.cn/blog_migrate/c8ebee475655e5621e838377c162c5e8.png)

**部署：**

进入cloud-demo目录后，运行下面的命令：

```bash
docker-compose up -d
```

如果nacos没有第一个启动，会报错，此时要重启nacos外的服务 

![](https://i-blog.csdnimg.cn/blog_migrate/2258c4f73fb1888ca710cc5f6ae961c2.png)

```bash
docker-compose restart gateway userservice orderservice
```

查看日志：

```bash
docker-compose logs -f
```

查看命令

```bash
docker-compose --help
```

重启：

```bash
docker-compose restart -d
```

终止：

```bash
docker-compose stop
```

## 5.Docker镜像仓库

### 5.1.搭建私有镜像仓库

搭建镜像仓库可以基于Docker官方提供的DockerRegistry来实现。

官网地址：[Docker Hub](https://hub.docker.com/_/registry "Docker Hub")

#### 5.1.1.简化版镜像仓库

Docker官方的Docker Registry是一个基础版本的Docker镜像仓库，具备仓库管理的完整功能，但是没有图形化界面。

搭建方式比较简单，命令如下：

```
docker run -d \
    --restart=always \
    --name registry	\
    -p 5000:5000 \
    -v registry-data:/var/lib/registry \
    registry
```

命令中挂载了一个数据卷registry-data到容器内的/var/lib/registry 目录，这是私有镜像库存放数据的目录。

访问[http://YourIp:5000/v2/\_catalog](http://YourIp:5000/v2/_catalog "http://YourIp:5000/v2/_catalog") 可以查看当前私有镜像服务中包含的镜像

#### 5.1.2.带有图形化界面版本

**1.配置Docker信任地址**

我们的私服采用的是http协议，默认不被Docker信任，所以需要做一个配置：

```bash
## 1.4.打开要修改的文件
vi /etc/docker/daemon.json
## 1.4.添加内容：
"insecure-registries":["http://192.168.150.101:8080"]
## 1.4.重加载
systemctl daemon-reload
## 1.4.重启docker
systemctl restart docker
```

**2.启动**

 使用DockerCompose部署带有图象界面的DockerRegistry，命令如下：

```bash
cd /root
mkdir registry-ui
cd registry-ui
touch docker-compose.yml
vi docker-compose.yml
```

将下面内容复制粘贴进去： 

```bash
version: '3.0'
services:
  registry:
    image: registry
    volumes:
      - ./registry-data:/var/lib/registry
  ui:
    image: joxit/docker-registry-ui:static
    ports:
      - 8080:80
    environment:
      - REGISTRY_TITLE=传智教育私有仓库
      - REGISTRY_URL=http://registry:5000
    depends_on:
      - registry
```

然后启动

```bash
docker-compose up -d
```

**3.浏览器访问**

http://centos的ip地址:8080

![](https://i-blog.csdnimg.cn/blog_migrate/8f0450a508a1b65ebdf38889e0357591.png)

### 5.2.推送、拉取镜像

推送镜像到私有镜像服务**必须先tag重命名，给镜像前加"ip地址:8080/"**，步骤如下：

**① 重新tag本地镜像**，名称前缀为私有仓库的地址：192.168.150.101:8080/

```
docker tag nginx:latest 192.168.150.101:8080/nginx:1.0 
```

**② 推送镜像（确保tag过）**

```
docker push 192.168.150.101:8080/nginx:1.0 
```

**③ 拉取镜像**

```
docker pull 192.168.150.101:8080/nginx:1.0 
```

![](https://i-blog.csdnimg.cn/blog_migrate/4d44f9b327c1e6472a06da0f2d1fdb98.png)