>  **导航：**
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})



[TOC]



# 1 Linux简介

## 1.0 linux用途

![img](Linux基础.assets/8b09c53857a846edb56d956d1a6b3e67.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 1.1 三种主流操作系统

**桌面操作系统**

- **Windows (用户数量最多)**
- MacOS (操作体验好，办公人士首选)
- Linux (用户数量少，多用于服务器系统，少用于桌面系统)

**服务器操作系统**

- UNIX (安全、稳定、付费)
- **Linux (安全、稳定、免费、占有率高)**
- Windows Server (付费、占有率低)

**移动设备操作系统**

- Android (**基于Linux**、开源，主要用于智能手机、平板电脑和智能电视)
- ios (苹果公司开发、不开源，用于苹果公司的产品，例如: iPhone、iPad)

**嵌入式操作系统**

- Linux (机顶盒、路由器、交换机)

## 1.2 Linux系统版本

Linux系统分为内核版和发行版

**1.2.1 内核版**

- 由Linus Torvalds及其团队开发、维护
- 免费、开源
- 负责控制硬件

**1.2.2 发行版（最常用centos）**

- 基于Linux内核版进行扩展
- 由各个Linux厂商开发、维护
- 有收费版本和免费 版本 ![img](Linux基础.assets/18b8179906954894a3f4bd328b6a5d41.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 2 Linux安装-CentOS

## 2.1 虚拟机安装Linux

**3.1.1 物理机安装**

直接将操作系统安装到服务器硬件上

**3.1.2 虚拟机安装**

通过虚拟机**软件安装虚拟机**：指通过软件模拟具有完整硬件系统功能，运行在完全隔离环境中的完整计算机系统。 常用虚拟机软件

- **VMWare**
- VirtualBox
- VMLite WorkStation
- Qemu
- HopeddotVOS

## 2.2 安装Linux（**VMWare和centos**）

**2.2.1 先安装VMWare**

![img](Linux基础.assets/ae6ab78bb6514b659096e190ac4ea8c6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

根据提示安装即可。



**2.2.2 安装CentOS镜像**

![img](Linux基础.assets/08c2403ae7ef4815a5b43b53d74682d8.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



1. 打开虚拟机软件
2. 点击【创建新的虚拟机按钮】 ![img](Linux基础.assets/476ca4e8876e44b4aaccf5816c21248d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
3. 选择典型，下一步![img](Linux基础.assets/130f5112b1e44f54a5e7e1dbbfea8090.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
4. 选择稍后安装操作系统 ![img](Linux基础.assets/0ac0fd4fb588422e80ba32cc4c2ad6d5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
5. 勾选版本

![img](Linux基础.assets/fc17ea750ab844d0b507cb8214dc16eb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

6.创建名称，选择物理文件的存储路径

![img](Linux基础.assets/61a528071f20490c83b352da3d6bec8c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



7.分配磁盘空间大小，20G即可

 ![img](Linux基础.assets/3495c112f2fe4e99b7a85e996e5bb9d9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



8.自定义硬件，内存2G，处理器2个，选择镜像的位置，点击完成

![img](Linux基础.assets/10f4203a63494aaa92d52f3e830bcf57.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/6a5a12c5b5584cb18e44a7af0d40b4d0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



9.点击开启此虚拟机，点击进入虚拟机，ctr+alt 快捷键可以退出虚拟机 点击Install … 安装虚拟机

![img](Linux基础.assets/9078ce5e45064f91a8912fcfdc1b20a0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/4caa5282c5114278a6465e2cb2626a55.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



10.**一路回车即可，耐心等待**，然后选择语言为中文，安装位置：

![img](Linux基础.assets/63265a175f9247d0a1c70fd55be566ec.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](Linux基础.assets/2d3dca6b9c2541c6bff185250bdca7d0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

键盘选择最小安装 

![img](Linux基础.assets/48390c2ee7e545c69bc5953fb59a9a90.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 开始安装

![img](Linux基础.assets/a63792b9684d415f96cdae60fc1cc351.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



11. 设置root密码，别创建用户，用户很多操作没权限

 ![img](Linux基础.assets/14f05f30ac964b1b800bf4370cf43045.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

12 重启和登录：

![img](Linux基础.assets/9453efb78e6e475280372685cf0386a7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 注意密码输入时候是看不到的

![img](Linux基础.assets/eb5adb5dff38433f95d9793e45a49eea.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





## 2.3 网卡设置

启动服务器时，没有加载网卡 查看IP地址

```
 ip addr
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 没有安装网卡的状态：
>
> ![img](Linux基础.assets/43653b6ffff4493bbb6fc8dcfe80cb8e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 安装有网卡的状态：
>
> ![img](Linux基础.assets/00c89682133b4171921ebfbe02fe63a2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**修改网络初始化配置，设定网卡**

```bash
cd /etc/sysconfig/network-scripts    #进入network - scripts

vi ifcfg-ens33                         #编辑ifcfg-ens33文件
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

此时是在vim浏览状态，i进入编辑状态
 修改ONBOOT=yes
 然后<ESC>→输入:Wq→<ENTER>保存退出 

**重新启动：**

![img](Linux基础.assets/79728715c8d34eb3ba5de2df87b2e7a0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/71ef22af76cb4758b76b8b973ca35716.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 2.4 安装SSH链接工具finalshell



SSH（Secure Shell），建立在应用层基础上的安全协议 常用的SSH链接工具

- putty
- secureCRT
- **xshell（推荐）**
- **finalshell（推荐）**

通过SSH连接工具就可以实现从本地连接到远程的Linux服务器

![img](Linux基础.assets/7c3fd80183ee49f183681a2cf6b3b387.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**SSH使用**

下载地址：[FinalShell SSH工具,服务器管理,远程桌面加速软件,支持Windows,macOS,Linux,版本4.3.10,更新日期2023.12.31 - FinalShell官网](https://www.hostbuf.com/t/988.html) 

打开finalshell

点击如下图所示图标

![img](Linux基础.assets/897c4269cf3e445d85b1729345288b88.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

点击最左侧按钮，选择SSH链接 ![img](Linux基础.assets/9cc9b4a244b3419686351bb34ee6c429.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](Linux基础.assets/3ede753db09f4f30897343e3af9b0128.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





配置相关信息

![img](Linux基础.assets/f1a728158a7643af8d14955590567beb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



点击就可以连接

 ![img](Linux基础.assets/2bb15d3e966344329006ea00665d9c32.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

>  **注意：**
>
> 一般centos会**隔两天左右自动改一下ip值**，如果连接成功过几天后，发现VMware端可以登录成功，而ssh链接不到服务器，那大概率就是ip地址自动改了，在VMware查一下新的id地址即可：
>
> ```
> ip addr
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.5 Linux与window目录结构对比

Linux系统中的目录

- **/是所有目录的顶点**
- **目录结构像一颗倒挂的树**

![img](Linux基础.assets/56f2fff01b134c1d85f317eb2df0f08b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**Linux自带目录：** 

 ![img](Linux基础.assets/1aaf07d6ec10432e9ddf0b9299bbc91d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- bin存放二进制可执行文件
- boot存放系统引导时使用的各种文件
- dev存放设备文件
- **etc存放系统配置文件**
- home存放系统用户的文件
- lib存放程序运行所需的共享库和内核模块
- opt额外安装的可选应用程序包所放置的位置
- **root超级用户目录**
- sbin存放二进制可执行文件，只有root用户才能访问
- tmp存放临时文件
- **usr存放系统应用程序**
- var存放运行时需要改变数据的文件，例如日志文件

## 2.6 禁止centos自动修改ip

默认情况，linux会自动修改ip。

查看ip地址：

```
ip addr
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 禁止ip自动修改

```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**找到**BOOTPROTO**修改：**

```
BOOTPROTO=none 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 3 命令

## 3.1 常用命令

[Linux的20个常用命令_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126258465?spm=1001.2014.3001.5501)



# 4 软件安装

## 4.1.软件安装方式

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

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 安装指定安装包：

```bash
yum install xxx
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> Yum (全称为**Yellow dog Updater, Modified)**是-个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。

**方式4：源码编译安装**

软件以源码工程的形式发布,需要自己编译打包，**例如前面springboot项目打包成jar后**，然后直接运行jar包。

## 4.2 安装JDK11

> 建议安装在/usr/local

1. 使用FinalShell自带的上传工具将jdk的二进制发布包上传到Linux**【jdk-11.0.16.1_linux-x64_bin.tar.gz】**![img](Linux基础.assets/b8860bd7a5a44e3a8e9ad65da45b4c32.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

2. 解压安装包,命令为，程序一般安装在 /usr/local 目录下

   ```bash
   tar -zxvf jdk-11.0.16.1_linux-x64_bin.tar.gz -C /usr/local
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3. 配置环境变量，使用vim命令修改/etc/profile文件，在文件末尾加入如下配置![img](Linux基础.assets/e774a810be144a15a467fffe4cd951ad.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

   ```bash
   vi /etc/profile
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   ```bash
   JAVA_HOME=/usr/local/jdk-11.0.16.1
   PATH=$JAVA_HOME/bin:$PATH
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

4. 重新加载profile文件， 使更改的配置立即生效，命令为

   ```
   source /etc/profile
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

5. 检查安装是否成功，命令为

   ```
   java -version
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

![img](Linux基础.assets/4bbebacea11841e08c2089e7bc63ee89.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 4.3 安装Tomcat

### 4.3.1 安装步骤

[Apache Tomcat® - Welcome!](https://tomcat.apache.org/)

1. 使用FinalShell自 带的上传工具将Tomcat的二进制发布包上传到Linux【apache- tomcat-7.0.57.tar.gz】

2. 解压安装包，命令为

   ```bash
   tar -zxvf apache-tomcat-7.0.57.tar.gz -C /usr/local
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3. 进入Tomcat的bin目录启动服务，命令为

   ```bash
   cd /usr/local/apache-tomcat-7.0.57.tar.gz/bin
   
   ./startup.sh
   #或者sh startup. sh
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   ![img](Linux基础.assets/7fc6b7aeaaf54e089d0498b5a3a72d12.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

### 4.3.2 验证Tomcat启动

**方式0：访问页面：**

http://centos的ip地址:8080

![img](Linux基础.assets/d89978d1ea694e10b1d42714353063cb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 要确保防火墙关闭状态才能查看：
>
> **永久关闭防火墙：**
>
> ```bash
> systemctl disable firewalld
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**方式1：查看启动日志**

```
more /usr/local/ apache-tomcat- 7.0.57/logs/catalina.out
tail -50 /usr/local/ apache-tomcat-7.0.57/logs/catalina.out
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动成功显示

```
五月 21, 2022 7:14:08 下午 org.apache.coyote.AbstractProtocol start
信息: Starting ProtocolHandler ["http-bio-8080"]
五月 21, 2022 7:14:08 下午 org.apache.coyote.AbstractProtocol start
信息: Starting ProtocolHandler ["ajp-bio-8009"]
五月 21, 2022 7:14:08 下午 org.apache.catalina.startup.Catalina start
信息: Server startup in 599 ms
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**方式2：查看进程**

```
ps -ef|grep tomcat
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动成功的话能看到进程

![img](Linux基础.assets/d453b912706e45feac39ed7658cf0577.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **注意:**
>
> - `ps`命令是linux下非常强大的进程查看命令,通过`ps -ef`可以查看当前运行的所有进程的详细信息
> - `"|”`在Linux中 称为管道符，可以将前一个命令的结果输出给后一个命令作为输入
> - 使用`ps`命令查看进程时，经常配合管道符和查找命令`grep` 一起使用，来查看特定进程

### 4.3.3 防火墙操作

- **查看防火墙状态**

  ```bash
  firewall-cmd --state    #简洁
  #systemctl status firewalld    #详细
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

开启状态：

![img](Linux基础.assets/a106163c3e8e48b99d1c7a538e4fcb26.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/68c46628d4bc461eb0c6e1621efffda1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

关闭状态：

![img](Linux基础.assets/dab96bba0e444eb2907bf58176dbe89d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- 暂时关闭防火墙

  ```
  systemctl stop firewalld
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **永久关闭防火墙（不安全，怕被攻击，建议开放指定端口）**

  ```
  systemctl disable firewalld
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 开启防火墙

  ```
  systemctl start firewalld
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **开放指定端口**

  ```
  firewall-cmd --zone=public --add-port=8080/tcp --permanent
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 关闭指定端口

  ```
  firewall-cmd --zone=public --remove-port=8080/tcp --permanent
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **立即生效**

  ```
  firewall-cmd --reload
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **查看开放的端口**

  ```
  firewall-cmd --zone=public --list-ports
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意:**
>
> 1. `systemctl`是管理Linux中服务的命令，可以对服务进行启动、停止、重启、查看状态等操作
> 2. `firewall-cmd`是 Linux中专门用于控制防火墙的命令
> 3. 为了保证系统安全,服务器的**防火墙不建议关闭**

### 4.3.4 停止Tomcat服务

**方式1：运行Tomcat的bin目录中提供的停止服务的脚本文件shutdown.sh**

```bash
cd /usr/local/apache-tomcat-7.0.57.tar.gz/bin
./shutdown.sh
#或者sh shutdown.sh
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**方式2：结束Tomcat进程（不建议）**

查看Tomcat进程，获得进程id

```
ps -ef | grep tomcat
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

执行命令结束进程

![img](Linux基础.assets/50d348b0bd5448a28f6686b5ce135457.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```
kill-9 26000(进程id)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

注意: kill命令是Linux提供的用于结束进程的命令, `-9`表示强制结束

## 4.4 安装MySQL

> 安装失败的话可以参考：[linux安装mysql_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126514654?spm=1001.2014.3001.5501) 

### 4.4.1 安装步骤

1. 检测当前系统中是否安装MySQL数据库

   查询当前系统中安装的所有软件

   ```
   rpm -qa
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   查询当前系统中安装的名称带mysql的软件

   ```
   rpm -qa | grep mysql
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   查询当前系统中安装的名称带mariadb的软件

   ```bash
   rpm -qa | grep mariadb 
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

   RPM ( Red-Hat Package Manager) RPM软件包管理器，是红帽Linux用于管理和安装软件的工具

   注意事项：如果当前系统中已经安装有MySQL数据库，安装将失败。CentOS7 自带mariadb,与MySQL数据库冲突,

2. 卸载与MySQL数据库冲突的软件 mariadb

   ```
   rpm -e --nodeps 软件名称  #卸载软件
   rpm -e --nodeps mariadb-libs-5.5.60-1.el7_5.x86_64
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3. 将MySQL安装包上传到Linux并解压

   ```bash
   mkdir /usr/local/mysql
   tar -zxvf mysql-5.7.25-1.el7.x86_64.rpm-bundle.tar.gz -C /usr/local/mysql
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   说明:解压后得到6个rpm的安装包文件 ![img](Linux基础.assets/e9550b3e7c8246df9ac65552afb78671.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   

4. 按照顺序安装rpm软件包

   ```
   rpm -ivh mysql-community-common-5.7.25-1.el7.x86_64.rpm
   rpm -ivh mysql-community-libs-5.7.25- 1.el7.x86. 64.rpm
   rpm -ivh mysql-community-devel- 5.7.25-1.el7.x86 64.rpm
   rpm -ivh mysql-community-libs-compat-5.7.25-1.el7 .x86_ 64.rpm
   rpm -ivh mysql-communit-client-5.7.25-1.el7.x86.64.rpm
   yum install net-tools
   rpm -ivh mysql-community-server-5.7.25-1.eI7.x86 64.rpm 
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   说明1:安装过程中提示缺少`net-tools`依赖，使用yum安装 说明2:可以通过指令升级现有软件及系统内核

   ```
   yum update
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.4.2 运行mysql

查看mysql服务状态

```
systemctl status mysqld
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动mysql服务

```
systemctl start mysqld
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/fe0c05c45eed44e3b1f883d292140676.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



说明:可以设置开机时启动mysq|服务，避免每次开机启动mysql

**开机启动mysql服务**

```
systemctl enable mysqld
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

查看已经启动的服务

```
netstat -tunlp
netstat -tunlp | grep mysql
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

查看mysql进程

```
ps -ef | grep mysql
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 4.4.3 登录mysql

1. 查阅临时密码

   查看文件内容

   ```
   cat /var/log/mysqld.log
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   查看文件内容中包含password的行信息

   ```
   cat /var/log/mysqld.log | grep password
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   ![在这里插入图片描述](Linux基础.assets/dfc8b2781ce240aaaf2d5918fb17581a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2. 登录mysql，修改密码，开放访问权限

   登录mysql (使用临时密码登录)

   ```
   mysql -uroot -p
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   设置密码长度最低位数

   ```bash
   #修改密码
   set global validate_password_length=4;
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   设置密码安全等级低，便于密码可以修改成root

   ```
   set global validate_password_policy=LOW;
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   设置密码为root

   ```bash
   set password = password('root');
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

   ```bash
   #开启访问权限
   grant all on . to 'root'@'%' identified by '123456';
   flush privileges;
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 4.5 安装文件上传工具lrzsz

安装成功之后命令行下输入rz回车，都可以上传文件。当然如果**使用finalshell则没必要安装了**：

![img](Linux基础.assets/c19fff72dbd0486ca1b6e1a3c5f21d85.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)







搜索lrzsz安装包,命令为

```bash
yum list lrzsz
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/a424e83bc3d54c4eba76b8a0e50ededb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



使用yum命令在线安装，命令为

```bash
yum install lrzsz.x86_64
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 4.6 Linux和Windows解决端口占用



### **4.6.1 Linux解决端口占用**

**方式一：lsof命令**

1、查看占用端口进程的PID：

```
lsof -i:{端口号}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)


 2、根据PID kill掉相关进程：

```
kill -9 {PID}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**方式二：netstat命令**

1、查看占用端口进程的PID：

```
netstat -tunlp|grep {port}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)


 2、kill方法如上。

```
kill -9 {PID}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**补充1：根据程序名查看对应的PID**

1、用[ps命令](https://so.csdn.net/so/search?q=ps命令&spm=1001.2101.3001.7020)（zb专用）：

```
ps -ef | grep {programName}
kill -9 {PID}

# 查看详细内存占用
ps aux -u root | grep {programName}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2、用pgrep命令：

pgrep命令的p表明了这个命令是专门用于进程查询的grep。

```
pgrep {programName}
kill -9 {PID}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**补充2：根据PID查看对应的进程**

```
ps -aux |grep -v grep|grep {$PID}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **4.6.2 Windows解决端口占用**

先查看占用端口的进程号 

```bash
netstat -ano | findstr "8080"
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

然后杀死进程号，例如进程号是12724：

```bash
taskkill -PID 12724 -F
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

示例：

![img](Linux基础.assets/4a7b593704c04111dd2f065f140b9b15.png)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)







# 5 项目部署

## 5.1 手工部署

### 5.1.1 前台部署 

**自己打包、手动上传Linux系统、java -jar运行jar包。** 

准备一个springboot项目：

![img](Linux基础.assets/cd19ba7f669e4abe9b088c1809127b21.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 打包：

![img](Linux基础.assets/965c6f5142f549dca8afebec8a6c3aba.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上传jar包到linux 

![img](Linux基础.assets/1f09a765fb674728a461168c7fa3fc24.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 运行jar包：

![img](Linux基础.assets/42cd38f8d5e140da9c7359fde67d73f4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**此时关闭窗口，项目就终止了。** 

### 5.1.2 后台部署，nohup

![img](Linux基础.assets/bbd06dbbc3cb4540964f807d0d634481.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```bash
cd /usr/local/app
nohup java -jar 项目名.jar &> hello.log &
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/1bae7bb5018140798945cdd35a8a92c2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

此时关闭窗口依然可以访问http://localhost:8080

**杀死进程**，直接搜索java：

![img](Linux基础.assets/5840985ce0c24dd88a7a475eed21ded2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 

## 5.2 通过shell脚本自动部署

这一节只写到一半，感觉比手动不熟麻烦很多，后面有时间再补

 ![img](Linux基础.assets/fe044da11d914a6aa022dd984ec78c3c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/109ccb36d6c94c55a4fcdfc41024dfe1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

1.Linux安装git：

```bash
yum install git
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.使用git克隆仓库

```bash
cd /usr/local/
git clone https://gitee.com/vincewm/reggie_takeout.git
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 需要输入账号密码的话输入即可。

3.Linux安装Maven

[Maven – Download Apache Maven](https://maven.apache.org/download.cgi)

国内网下载慢，建议开科技

![img](Linux基础.assets/4970cf8c9c9648788cd1828a976af253.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```bash
tar -zxvf apache-maven-3.8.6-bin.tar.gz -C /usr/local
vim /etc/profile
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

vim修改： 

```bash
export MAVEN_HOME=/usr/local/apache-maven-3.8.6
export PATH最后面加上		:$MAVEN_HOME/bin
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/3425651171d74c57ba4fea897c51131c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



 重新加载、查看版本：

```bash
source /etc/profile
mvn -version
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](Linux基础.assets/05b653c1a8f34e0b9b1bc87f79ac4436.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

修改settings.xml

```bash
cd /usr/local
mkdir repo
vim /usr/local/apache-maven-3.8.6/conf/settings.xml
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](Linux基础.assets/1fd2cc02a2f5470e9a017c2a7ad6deac.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)