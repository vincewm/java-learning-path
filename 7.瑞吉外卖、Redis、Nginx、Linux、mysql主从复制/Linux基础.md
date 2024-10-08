>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1 Linux简介](#1%20Linux%E7%AE%80%E4%BB%8B)

[1.0 linux用途](#1.0%20linux%E7%94%A8%E9%80%94)

[1.1 三种主流操作系统](#1.1%20%E4%B8%89%E7%A7%8D%E4%B8%BB%E6%B5%81%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F)

[1.2 Linux系统版本](#1.2%20Linux%E7%B3%BB%E7%BB%9F%E7%89%88%E6%9C%AC)

[2 Linux安装-CentOS](#2%20Linux%E5%AE%89%E8%A3%85-CentOS)

[2.1 虚拟机安装Linux](#2.1%20%E5%AE%89%E8%A3%85%E6%96%B9%E5%BC%8F%E4%BB%8B%E7%BB%8D)

[2.2 安装Linux（VMWare和centos）](#2.2%20%E5%AE%89%E8%A3%85Linux)

[2.3 网卡设置](#2.3%20%E7%BD%91%E5%8D%A1%E8%AE%BE%E7%BD%AE)

[2.4 安装SSH链接工具finalshell](#2.4%20%E5%AE%89%E8%A3%85SSH%E9%93%BE%E6%8E%A5%E5%B7%A5%E5%85%B7)

[2.5 Linux与window目录结构对比](#2.5%20Linux%E4%B8%8Ewindow%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84%E5%AF%B9%E6%AF%94)

[2.6 禁止centos自动修改ip](#2.6%20%E7%A6%81%E6%AD%A2centos%E8%87%AA%E5%8A%A8%E4%BF%AE%E6%94%B9ip)

[3 命令](#3%2020%E4%B8%AA%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)

[3.1 常用命令](#3.1%20%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)

[4 软件安装](#4%20%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85)

[4.1.软件安装方式](#4.1.%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85%E6%96%B9%E5%BC%8F)

[4.2 安装JDK11](#4.2%20%E5%AE%89%E8%A3%85JDK)

[4.3 安装Tomcat](#4.3%20%E5%AE%89%E8%A3%85Tomcat)

[4.3.1 安装步骤](#4.3.1%20%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4)

[4.3.2 验证Tomcat启动](#4.3.2%20%E9%AA%8C%E8%AF%81Tomcat%E5%90%AF%E5%8A%A8%E6%98%AF%E5%90%A6%E6%88%90%E5%8A%9F)

[4.3.3 防火墙操作](#4.3.3%20%E9%98%B2%E7%81%AB%E5%A2%99%E6%93%8D%E4%BD%9C)

[4.3.4 停止Tomcat服务](#4.3.4%20%E5%81%9C%E6%AD%A2Tomcat%E6%9C%8D%E5%8A%A1)

[4.4 安装MySQL](#4.4%20%E5%AE%89%E8%A3%85MySQL)

[4.4.1 安装步骤](#4.4.1%20%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4)

[4.4.2 运行mysql](#4.4.2%20%E8%BF%90%E8%A1%8Cmysql)

[4.4.3 登录mysql](#4.4.3%20%E7%99%BB%E5%BD%95mysql)

[4.5 安装文件上传工具lrzsz](#4.5%20%E5%AE%89%E8%A3%85lrzsz)

[4.6 Linux和Windows解决端口占用](#4.6%20Linux%E5%92%8CWindows%E8%A7%A3%E5%86%B3%E7%AB%AF%E5%8F%A3%E5%8D%A0%E7%94%A8)

[4.6.1 Linux解决端口占用](#4.6.1%20Linux%E8%A7%A3%E5%86%B3%E7%AB%AF%E5%8F%A3%E5%8D%A0%E7%94%A8)

[4.6.2 Windows解决端口占用](#4.6.2%20Windows%E8%A7%A3%E5%86%B3%E7%AB%AF%E5%8F%A3%E5%8D%A0%E7%94%A8%EF%BC%9A%C2%A0)

[5 项目部署](#5%20%E9%A1%B9%E7%9B%AE%E9%83%A8%E7%BD%B2)

[5.1 手工部署](#5.1%20%E6%89%8B%E5%B7%A5%E9%83%A8%E7%BD%B2)

[5.1.1 前台部署](#5.1.1%20%E5%89%8D%E5%8F%B0%E9%83%A8%E7%BD%B2%C2%A0) 

[5.1.2 后台部署，nohup](#5.1.2%20%E5%90%8E%E5%8F%B0%E9%83%A8%E7%BD%B2%EF%BC%8Cnohup)

[5.2 通过shell脚本自动部署](#5.2%20%E9%80%9A%E8%BF%87shell%E8%84%9A%E6%9C%AC%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2)

--

## 1 Linux简介

### 1.0 linux用途

![](https://i-blog.csdnimg.cn/blog_migrate/579c6f0dd81a71a93fafa01c2d139297.png)

### 1.1 三种主流操作系统

**桌面操作系统**

-   **Windows (用户数量最多)**
-   MacOS (操作体验好，办公人士首选)
-   Linux (用户数量少，多用于服务器系统，少用于桌面系统)

**服务器操作系统**

-   UNIX (安全、稳定、付费)
-   **Linux (安全、稳定、免费、占有率高)**
-   Windows Server (付费、占有率低)

**移动设备操作系统**

-   Android (**基于Linux**、开源，主要用于智能手机、平板电脑和智能电视)
-   ios (苹果公司开发、不开源，用于苹果公司的产品，例如: iPhone、iPad)

**嵌入式操作系统**

-   Linux (机顶盒、路由器、交换机)

### 1.2 Linux系统版本

Linux系统分为内核版和发行版

**1.2.1 内核版**

-   由Linus Torvalds及其团队开发、维护
-   免费、开源
-   负责控制硬件

**1.2.2 发行版（最常用centos）**

-   基于Linux内核版进行扩展
-   由各个Linux厂商开发、维护
-   有收费版本和免费 版本 ![](https://i-blog.csdnimg.cn/blog_migrate/d4269bcda72257634824c0e78a360db8.png)

## 2 Linux安装-CentOS

### 2.1 虚拟机安装Linux

**3.1.1 物理机安装**

直接将操作系统安装到服务器硬件上

**3.1.2 虚拟机安装**

通过虚拟机**软件安装虚拟机**：指通过软件模拟具有完整硬件系统功能，运行在完全隔离环境中的完整计算机系统。 常用虚拟机软件

-   **VMWare**
-   VirtualBox
-   VMLite WorkStation
-   Qemu
-   HopeddotVOS

### 2.2 安装Linux（**VMWare和centos**）

**2.2.1 先安装VMWare**

![](https://i-blog.csdnimg.cn/blog_migrate/5dba88e17633eb4bf792527e56768636.png)

根据提示安装即可。

**2.2.2 安装CentOS镜像**

![](https://i-blog.csdnimg.cn/blog_migrate/c0a0b04a039f23ecd8ed6023dd146ef4.png)

1.  打开虚拟机软件
2.  点击【创建新的虚拟机按钮】 ![](https://i-blog.csdnimg.cn/blog_migrate/5adcf0c1795fc2604d2ed99c3ce12809.png)
3.  选择典型，下一步![](https://i-blog.csdnimg.cn/blog_migrate/d04d37af1f9293127f8a2e87deea37f6.png)
4.  选择稍后安装操作系统 ![](https://i-blog.csdnimg.cn/blog_migrate/b2fdf9332792adbb776c8b5a6e0056c0.png)
5.  勾选版本

![](https://i-blog.csdnimg.cn/blog_migrate/c6b7ad062596566d4760e6c532419efc.png)

6.创建名称，选择物理文件的存储路径

![](https://i-blog.csdnimg.cn/blog_migrate/b37b5224013982c54b173fac35c48766.png)

7.分配磁盘空间大小，20G即可

 ![](https://i-blog.csdnimg.cn/blog_migrate/d238bc252a0085c3380edbf3b8be866c.png)

8.自定义硬件，内存2G，处理器2个，选择镜像的位置，点击完成

![](https://i-blog.csdnimg.cn/blog_migrate/a3983f678af955102f22667a34a7e195.png)

![](https://i-blog.csdnimg.cn/blog_migrate/5b64f8d9f7cfac4a6174c082def4032c.png)

9.点击开启此虚拟机，点击进入虚拟机，ctr+alt 快捷键可以退出虚拟机 点击Install … 安装虚拟机

![](https://i-blog.csdnimg.cn/blog_migrate/a6cad4a0f7855f888341ad452407add7.png)

![](https://i-blog.csdnimg.cn/blog_migrate/b79bace2c1d14b4110c2e2c8b3dd2a1b.png)

10.**一路回车即可，耐心等待**，然后选择语言为中文，安装位置：

![](https://i-blog.csdnimg.cn/blog_migrate/1ce34f699b8ef7958fbdc1fee11c1da6.png)![](https://i-blog.csdnimg.cn/blog_migrate/5517d541456a278a2bf8def9862503e3.png)

键盘选择最小安装 

![](https://i-blog.csdnimg.cn/blog_migrate/895c357ad25d393864947025a2ca1413.png)

 开始安装

![](https://i-blog.csdnimg.cn/blog_migrate/be460c83962cc0963590354ac8633173.png)

11\. 设置root密码，别创建用户，用户很多操作没权限

 ![](https://i-blog.csdnimg.cn/blog_migrate/8898dcff171008c3117d1a474d332b44.png)

12 重启和登录：

![](https://i-blog.csdnimg.cn/blog_migrate/c0d67cc493abb211b5d8bc6f79da3afd.png) 注意密码输入时候是看不到的

![](https://i-blog.csdnimg.cn/blog_migrate/bfb28529d14e013dff9f1d85911c1b67.png)

### 2.3 网卡设置

启动服务器时，没有加载网卡 查看IP地址

```
 ip addr
```

> 没有安装网卡的状态：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/79c9c3b1c1b0ca807e309079af370b4d.png) 安装有网卡的状态：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/bd19c33aff66b39271e9c2e3c464252d.png)

**修改网络初始化配置，设定网卡**

```bash
cd /etc/sysconfig/network-scripts    #进入network - scripts

vi ifcfg-ens33                         #编辑ifcfg-ens33文件
```

此时是在vim浏览状态，i进入编辑状态  
修改ONBOOT=yes  
然后<ESC>→输入:Wq→<ENTER>保存退出 

**重新启动：**

![](https://i-blog.csdnimg.cn/blog_migrate/fb4315195a1d7743dcb6e137380a763a.png)

![](https://i-blog.csdnimg.cn/blog_migrate/b006c577d10fd4f9d66ce6fb85607061.png)

### 2.4 安装SSH链接工具finalshell

SSH（Secure Shell），建立在应用层基础上的安全协议 常用的SSH链接工具

-   putty
-   secureCRT
-   **xshell（推荐）**
-   **finalshell（推荐）**

通过SSH连接工具就可以实现从本地连接到远程的Linux服务器

![](https://i-blog.csdnimg.cn/blog_migrate/f359b91fc71ae101ed0c632ea606f0ab.png)

**SSH使用**

下载地址：[FinalShell SSH工具,服务器管理,远程桌面加速软件,支持Windows,macOS,Linux,版本4.3.10,更新日期2023.12.31 - FinalShell官网](https://www.hostbuf.com/t/988.html "FinalShell SSH工具,服务器管理,远程桌面加速软件,支持Windows,macOS,Linux,版本4.3.10,更新日期2023.12.31 - FinalShell官网") 

打开finalshell

点击如下图所示图标

![](https://i-blog.csdnimg.cn/blog_migrate/09ffb9f958933a941f0f59e98337387e.png)

点击最左侧按钮，选择SSH链接 ![](https://i-blog.csdnimg.cn/blog_migrate/d2bf723a23bd456cf20691162adfa459.png)![](https://i-blog.csdnimg.cn/blog_migrate/888500215ae4efaaca49f8eccd5b6e19.png)

配置相关信息

![](https://i-blog.csdnimg.cn/blog_migrate/1dcb7053f175565d348954702f112d5b.png)

点击就可以连接

 ![](https://i-blog.csdnimg.cn/blog_migrate/40789494e644f716533f5b9d9b895797.png)

>  **注意：**
> 
> 一般centos会**隔两天左右自动改一下ip值**，如果连接成功过几天后，发现VMware端可以登录成功，而ssh链接不到服务器，那大概率就是ip地址自动改了，在VMware查一下新的id地址即可：
> 
> ```
> ip addr
> ```

### 2.5 Linux与window目录结构对比

Linux系统中的目录

-   **/是所有目录的顶点**
-   **目录结构像一颗倒挂的树**

![](https://i-blog.csdnimg.cn/blog_migrate/0f9223e447a09afcfb1b83a35bfc51ab.png)

**Linux自带目录：** 

 ![](https://i-blog.csdnimg.cn/blog_migrate/c715dd3618db77b3b233134b3cc74dba.png)

-   bin存放二进制可执行文件
-   boot存放系统引导时使用的各种文件
-   dev存放设备文件
-   **etc存放系统配置文件**
-   home存放系统用户的文件
-   lib存放程序运行所需的共享库和内核模块
-   opt额外安装的可选应用程序包所放置的位置
-   **root超级用户目录**
-   sbin存放二进制可执行文件，只有root用户才能访问
-   tmp存放临时文件
-   **usr存放系统应用程序**
-   var存放运行时需要改变数据的文件，例如日志文件

### 2.6 禁止centos自动修改ip

默认情况，linux会自动修改ip。

查看ip地址：

```
ip addr
```

 禁止ip自动修改

```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

**找到**BOOTPROTO**修改：**

```
BOOTPROTO=none 
```

**BOOTPROTO值：**dhcp（默认值）表示动态获取IP地址，satic表示静态IP，none表示不指定，就是静态。

然后在文件最下面输入：

```bash
IPADDR=填写你想要的ip地址例如192.168.1.101
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=1.0.0.1
DNS2=1.1.1.1
DNS3=8.8.4.4
```

## 3 命令

### 3.1 常用命令

[Linux的20个常用命令\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126258465?spm=1001.2014.3001.5501 "Linux的20个常用命令_vincewm的博客-CSDN博客")

## 4 软件安装

### 4.1.软件安装方式

**方式1：二进制发布包安装**

软件已经针对具体平台编译打包发布，直接从目标官网下载.tar.gz文件，上传解压,修改配置即可

**方式2：rpm安装**

软件已经按照redhat的包管理规范进行打包，使用rpm命令进行安装,不能自行解决库依赖问题

**方式3：yum安装（建议）**

一种在线软件安装方式， 本质上还是rpm安装，自动下载安装包并安装,**安装过程中自动解决库依赖问题**

搜索指定安装包：

```bash
yum list xxx
```

 安装指定安装包：

```bash
yum install xxx
```

> Yum (全称为**Yellow dog Updater, Modified)**是-个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。

**方式4：源码编译安装**

软件以源码工程的形式发布,需要自己编译打包，**例如前面springboot项目打包成jar后**，然后直接运行jar包。

### 4.2 安装JDK11

> 建议安装在/usr/local

1.  使用FinalShell自带的上传工具将jdk的二进制发布包上传到Linux**【jdk-11.0.16.1\_linux-x64\_bin.tar.gz】**![](https://i-blog.csdnimg.cn/blog_migrate/4873dbfc918c27c32b5ed32bcbd0816e.png)
    
2.  解压安装包,命令为，程序一般安装在 /usr/local 目录下
    
    ```bash
    tar -zxvf jdk-11.0.16.1_linux-x64_bin.tar.gz -C /usr/local
    ```
    
3.  配置环境变量，使用vim命令修改/etc/profile文件，在文件末尾加入如下配置![](https://i-blog.csdnimg.cn/blog_migrate/808bd9b6465680faeb33832638ad60f0.png)
    
    ```bash
    vi /etc/profile
    ```
    
    ```bash
    JAVA_HOME=/usr/local/jdk-11.0.16.1
    PATH=$JAVA_HOME/bin:$PATH
    ```
    
4.  重新加载profile文件， 使更改的配置立即生效，命令为
    
    ```
    source /etc/profile
    ```
    
5.  检查安装是否成功，命令为
    
    ```
    java -version
    ```
    

![](https://i-blog.csdnimg.cn/blog_migrate/3a116f5f49bcb82cdd17a1195d509d9d.png)

### 4.3 安装Tomcat

#### 4.3.1 安装步骤

[Apache Tomcat® - Welcome!](https://tomcat.apache.org/ "Apache Tomcat® - Welcome!")

1.  使用FinalShell自 带的上传工具将Tomcat的二进制发布包上传到Linux【apache- tomcat-7.0.57.tar.gz】
    
2.  解压安装包，命令为
    
    ```bash
    tar -zxvf apache-tomcat-7.0.57.tar.gz -C /usr/local
    ```
    
3.  进入Tomcat的bin目录启动服务，命令为
    
    ```bash
    cd /usr/local/apache-tomcat-7.0.57.tar.gz/bin
    
    ./startup.sh
    #或者sh startup. sh
    ```
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/7c18c80e4ac58a0aa53cc03d6cdc389c.png)
    

#### 4.3.2 验证Tomcat启动

**方式0：访问页面：**

http://centos的ip地址:8080

![](https://i-blog.csdnimg.cn/blog_migrate/6812b6daf4fbff7d05e236f8c0d6ed80.png)

> 要确保防火墙关闭状态才能查看：
> 
> **永久关闭防火墙：**
> 
> ```bash
> systemctl disable firewalld
> ```

**方式1：查看启动日志**

```
more /usr/local/ apache-tomcat- 7.0.57/logs/catalina.out
tail -50 /usr/local/ apache-tomcat-7.0.57/logs/catalina.out
```

启动成功显示

```
五月 21, 2022 7:14:08 下午 org.apache.coyote.AbstractProtocol start
信息: Starting ProtocolHandler ["http-bio-8080"]
五月 21, 2022 7:14:08 下午 org.apache.coyote.AbstractProtocol start
信息: Starting ProtocolHandler ["ajp-bio-8009"]
五月 21, 2022 7:14:08 下午 org.apache.catalina.startup.Catalina start
信息: Server startup in 599 ms
```

**方式2：查看进程**

```
ps -ef|grep tomcat
```

启动成功的话能看到进程

![](https://i-blog.csdnimg.cn/blog_migrate/6abdac9d339d84426e0708a34e66a669.png)

> **注意:**
> 
> -   `ps`命令是linux下非常强大的进程查看命令,通过`ps -ef`可以查看当前运行的所有进程的详细信息
> -   `"|”`在Linux中 称为管道符，可以将前一个命令的结果输出给后一个命令作为输入
> -   使用`ps`命令查看进程时，经常配合管道符和查找命令`grep` 一起使用，来查看特定进程

#### 4.3.3 防火墙操作

-   **查看防火墙状态**
    
    ```bash
    firewall-cmd --state    #简洁
    #systemctl status firewalld    #详细
    
    ```
    

开启状态：

![](https://i-blog.csdnimg.cn/blog_migrate/4eaa3e9a3ec83b3c42e1bc02246f8fad.png)

![](https://i-blog.csdnimg.cn/blog_migrate/23e6648e3de1a34a95c8de287bf904fd.png)

关闭状态：

![](https://i-blog.csdnimg.cn/blog_migrate/66d45069ffda4c42084e24e084fcd1ef.png)

-   暂时关闭防火墙
    
    ```
    systemctl stop firewalld
    ```
    
-   **永久关闭防火墙（不安全，怕被攻击，建议开放指定端口）**
    
    ```
    systemctl disable firewalld
    ```
    
-   开启防火墙
    
    ```
    systemctl start firewalld
    ```
    
-   **开放指定端口**
    
    ```
    firewall-cmd --zone=public --add-port=8080/tcp --permanent
    ```
    
-   关闭指定端口
    
    ```
    firewall-cmd --zone=public --remove-port=8080/tcp --permanent
    ```
    
-   **立即生效**
    
    ```
    firewall-cmd --reload
    ```
    
-   **查看开放的端口**
    
    ```
    firewall-cmd --zone=public --list-ports
    ```
    

> **注意:**
> 
> 1.  `systemctl`是管理Linux中服务的命令，可以对服务进行启动、停止、重启、查看状态等操作
> 2.  `firewall-cmd`是 Linux中专门用于控制防火墙的命令
> 3.  为了保证系统安全,服务器的**防火墙不建议关闭**

#### 4.3.4 停止Tomcat服务

**方式1：运行Tomcat的bin目录中提供的停止服务的脚本文件shutdown.sh**

```bash

cd /usr/local/apache-tomcat-7.0.57.tar.gz/bin
./shutdown.sh
#或者sh shutdown.sh
```

**方式2：结束Tomcat进程（不建议）**

查看Tomcat进程，获得进程id

```
ps -ef | grep tomcat
```

执行命令结束进程

![](https://i-blog.csdnimg.cn/blog_migrate/3cf28b8597be2da80d3b81b646b58bf2.png)

```
kill-9 26000(进程id)
```

注意: kill命令是Linux提供的用于结束进程的命令, `-9`表示强制结束

### 4.4 安装MySQL

> 安装失败的话可以参考：[linux安装mysql\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126514654?spm=1001.2014.3001.5501 "linux安装mysql_vincewm的博客-CSDN博客") 

#### 4.4.1 安装步骤

1.  检测当前系统中是否安装MySQL数据库
    
    查询当前系统中安装的所有软件
    
    ```
    rpm -qa
    ```
    
    查询当前系统中安装的名称带mysql的软件
    
    ```
    rpm -qa | grep mysql
    ```
    
    查询当前系统中安装的名称带mariadb的软件
    
    ```bash
    rpm -qa | grep mariadb 
    ```
    
    RPM ( Red-Hat Package Manager) RPM软件包管理器，是红帽Linux用于管理和安装软件的工具
    
    注意事项：如果当前系统中已经安装有MySQL数据库，安装将失败。CentOS7 自带mariadb,与MySQL数据库冲突,
    
2.  卸载与MySQL数据库冲突的软件 mariadb
    
    ```
    rpm -e --nodeps 软件名称  #卸载软件
    rpm -e --nodeps mariadb-libs-5.5.60-1.el7_5.x86_64
    
    ```
    
3.  将MySQL安装包上传到Linux并解压
    
    ```bash
    mkdir /usr/local/mysql
    tar -zxvf mysql-5.7.25-1.el7.x86_64.rpm-bundle.tar.gz -C /usr/local/mysql
    ```
    
    说明:解压后得到6个rpm的安装包文件 ![](https://i-blog.csdnimg.cn/blog_migrate/3eff88217daf40ff4465021ac0d92706.png)
    
4.  按照顺序安装rpm软件包
    
    ```
    rpm -ivh mysql-community-common-5.7.25-1.el7.x86_64.rpm
    rpm -ivh mysql-community-libs-5.7.25- 1.el7.x86. 64.rpm
    rpm -ivh mysql-community-devel- 5.7.25-1.el7.x86 64.rpm
    rpm -ivh mysql-community-libs-compat-5.7.25-1.el7 .x86_ 64.rpm
    rpm -ivh mysql-communit-client-5.7.25-1.el7.x86.64.rpm
    yum install net-tools
    rpm -ivh mysql-community-server-5.7.25-1.eI7.x86 64.rpm 
    ```
    
    说明1:安装过程中提示缺少`net-tools`依赖，使用yum安装 说明2:可以通过指令升级现有软件及系统内核
    
    ```
    yum update
    ```
    

#### 4.4.2 运行mysql

查看mysql服务状态

```
systemctl status mysqld
```

启动mysql服务

```
systemctl start mysqld
```

![](https://i-blog.csdnimg.cn/blog_migrate/5594ae17872f6f8892abb9d843fdb565.png)

说明:可以设置开机时启动mysq|服务，避免每次开机启动mysql

**开机启动mysql服务**

```
systemctl enable mysqld
```

查看已经启动的服务

```
netstat -tunlp
netstat -tunlp | grep mysql
```

查看mysql进程

```
ps -ef | grep mysql
```

#### 4.4.3 登录mysql

1.  查阅临时密码
    
    查看文件内容
    
    ```
    cat /var/log/mysqld.log
    ```
    
    查看文件内容中包含password的行信息
    
    ```
    cat /var/log/mysqld.log | grep password
    ```
    
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/2c87446244ee3659cfc96f7e6b421ee8.png)
    
2.  登录mysql，修改密码，开放访问权限
    
    登录mysql (使用临时密码登录)
    
    ```
    mysql -uroot -p
    ```
    
    设置密码长度最低位数
    
    ```bash
    #修改密码
    set global validate_password_length=4;
    ```
    
    设置密码安全等级低，便于密码可以修改成root
    
    ```
    set global validate_password_policy=LOW;
    ```
    
    设置密码为root
    
    ```bash
    set password = password('root');
    ```
    
    ```bash
    #开启访问权限
    grant all on . to 'root'@'%' identified by '123456';
    flush privileges;
    ```
    

### 4.5 安装文件上传工具lrzsz

安装成功之后命令行下输入rz回车，都可以上传文件。当然如果**使用finalshell则没必要安装了**：

![](https://i-blog.csdnimg.cn/blog_migrate/acc3d1ed9e995f45e77267ad3e79fe65.png)

搜索lrzsz安装包,命令为

```bash
yum list lrzsz
```

![](https://i-blog.csdnimg.cn/blog_migrate/7a2071fc95a10161409a9f1a64af85a1.png)

使用yum命令在线安装，命令为

```bash
yum install lrzsz.x86_64
```

### 4.6 Linux和Windows解决端口占用

#### **4.6.1 Linux解决端口占用**

**方式一：lsof命令**

1、查看占用端口进程的PID：

```
lsof -i:{端口号}

```

  
2、根据PID kill掉相关进程：

```
kill -9 {PID}

```

**方式二：netstat命令**

1、查看占用端口进程的PID：

```
netstat -tunlp|grep {port}

```

  
2、kill方法如上。

```
kill -9 {PID}

```

**补充1：根据程序名查看对应的PID**

1、用[ps命令](https://so.csdn.net/so/search?q=ps%E5%91%BD%E4%BB%A4&spm=1001.2101.3001.7020 "ps命令")（zb专用）：

```
ps -ef | grep {programName}
kill -9 {PID}

# 查看详细内存占用
ps aux -u root | grep {programName}

```

2、用pgrep命令：

pgrep命令的p表明了这个命令是专门用于进程查询的grep。

```
pgrep {programName}
kill -9 {PID}

```

**补充2：根据PID查看对应的进程**

```
ps -aux |grep -v grep|grep {$PID}

```

#### **4.6.2 Windows解决端口占用**

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

## 5 项目部署

### 5.1 手工部署

#### 5.1.1 前台部署 

**自己打包、手动上传Linux系统、java -jar运行jar包。** 

准备一个springboot项目：

![](https://i-blog.csdnimg.cn/blog_migrate/a7ca834c54fad8bf20cb6cc1942bed0f.png) 打包：

![](https://i-blog.csdnimg.cn/blog_migrate/161906ef8bff7884fc186cb32902a67c.png)

上传jar包到linux 

![](https://i-blog.csdnimg.cn/blog_migrate/a535d28a2c024ee06822909fed583d83.png)

 运行jar包：

![](https://i-blog.csdnimg.cn/blog_migrate/71978a484a72bcdb91f0008decf1c356.png)

**此时关闭窗口，项目就终止了。** 

#### 5.1.2 后台部署，nohup

![](https://i-blog.csdnimg.cn/blog_migrate/1a0689c4da1d9ca19e15254f9daee9e8.png)

```bash
cd /usr/local/app
nohup java -jar 项目名.jar &> hello.log &
```

![](https://i-blog.csdnimg.cn/blog_migrate/859c675b514c4efc559818151a9ec52b.png)

此时关闭窗口依然可以访问http://localhost:8080

**杀死进程**，直接搜索java：

![](https://i-blog.csdnimg.cn/blog_migrate/46017a8263e7edec5953d23846099d92.png)  

### 5.2 通过shell脚本自动部署

这一节只写到一半，感觉比手动不熟麻烦很多，后面有时间再补

 ![](https://i-blog.csdnimg.cn/blog_migrate/814c8647be019f4b131793e597886a44.png)

![](https://i-blog.csdnimg.cn/blog_migrate/a3e401009a861a18d75849157e5ab4d0.png)

1.Linux安装git：

```bash
yum install git
```

2.使用git克隆仓库

```bash
cd /usr/local/
git clone https://gitee.com/vincewm/reggie_takeout.git
```

 需要输入账号密码的话输入即可。

3.Linux安装Maven

[Maven – Download Apache Maven](https://maven.apache.org/download.cgi "Maven – Download Apache Maven")

国内网下载慢，建议开科技

![](https://i-blog.csdnimg.cn/blog_migrate/b93b3a8fcdc3010a9f63698666db57aa.png)

```bash
tar -zxvf apache-maven-3.8.6-bin.tar.gz -C /usr/local
vim /etc/profile
```

vim修改： 

```bash

export MAVEN_HOME=/usr/local/apache-maven-3.8.6
export PATH最后面加上		:$MAVEN_HOME/bin
```

![](https://i-blog.csdnimg.cn/blog_migrate/342dacbf07974202080954162496316c.png)

 重新加载、查看版本：

```bash
source /etc/profile
mvn -version
```

![](https://i-blog.csdnimg.cn/blog_migrate/433c7ec6c6532f6753d6a0d0dfb24c4d.png)

修改settings.xml

```bash
cd /usr/local
mkdir repo
vim /usr/local/apache-maven-3.8.6/conf/settings.xml
```

 ![](https://i-blog.csdnimg.cn/blog_migrate/46fdf25747b532b78ea22d45ef15425c.png)