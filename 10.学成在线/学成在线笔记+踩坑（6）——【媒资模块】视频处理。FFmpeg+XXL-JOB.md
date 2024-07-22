>  **导航：** 
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?spm=1001.2014.3001.5501)

[TOC]



# **1** **视频转码需求**

视频上传成功后需要对视频进行转码处理。

## **1.1** **视频编码格式和文件格式**

**什么是视频编码？**



所谓视频编码方式就是指通过压缩技术，将原始视频格式的文件转换成另—种视频格式文件的方式。视频流传输中最为重要的编解码标准有国际电联的H.261、H.263、H.264。

**文件格式：**

是指.mp4、.avi、.rmvb等 这些不同扩展名的视频文件的文件格式 ，视频文件的内容主要包括视频和音频，其文件格式是按照一 定的编码格式去编码，并且按照该文件所规定的封装格式**将视频、音频、字幕等信息封装**在一起，**播放器**会根据它们的封装格式去**提取出编码**，然后由播放器**解码**，最终播放音视频。

**音视频编码格式：**

通过音视频的压缩技术，将视频格式转换成另一种视频格式，通过视频编码实现流媒体的传输。



音视频编码格式主要有几下几类：

MPEG系列

（由ISO[国际标准组织机构]下属的MPEG[运动图象专家组]开发 ）视频编码方面主要是Mpeg1（vcd用的就是它）、Mpeg2（DVD使用）、Mpeg4（的DVDRIP使用的都是它的变种，如：divx，xvid等）、Mpeg4 AVC（正热门）；音频编码方面主要是MPEG Audio Layer 1/2、MPEG Audio Layer 3（大名鼎鼎的mp3）、MPEG-2 AAC 、MPEG-4 AAC等等。注意：DVD音频没有采用Mpeg的。

H.26X系列

（由ITU[国际电传视讯联盟]主导，侧重网络传输，注意：只是视频编码）

包括H.261、H.262、H.263、H.263+、H.263++、H.264（就是MPEG4 AVC-合作的结晶）

目前最常用的编码标准是视频H.264，音频AAC。

> 提问：
>
> H.264是编码格式还是文件格式？编码。
>
> mp4是编码格式还是文件格式？文件。



## **1.2 windows使用编码工具FFmpeg**

我们将视频录制完成后，使用视频编码软件对视频进行编码，本项目使用FFmpeg对视频进行编码 。

***FFmpeg\***是一套可以用来记录、转换数字音频、视频，并能将其转化为流的**开源计算机程序**。采用LGPL或GPL许可证。它提供了**录制、转换以及流化音视频**的完整解决方案。

FFmpeg被许多开源项目采用，QQ影音、暴风影音、VLC等。

**下载：**FFmpeg [Download FFmpeg](https://www.ffmpeg.org/download.html#build-windows)

环境变量：将ffmpeg.exe加入环境变量path中。

测试是否正常：cmd运行 ffmpeg -version

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/02098bdd54494997b54a5e95e0d86415.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**测试：**

将nacos.avi文件转成mp4，运行如下命令：

```
D:\soft\ffmpeg\ffmpeg.exe -i 1.avi 1.mp4
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如果已经将ffmpeg.exe配置到环境变量path中，进入视频目录直接运行：

```
ffmpeg.exe -i 1.avi 1.mp4
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

转成mp3：

```
ffmpeg -i nacos.avi nacos.mp3
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

转成gif：

```
ffmpeg -i nacos.avi nacos.gif
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

官方文档（英文）：[ffmpeg Documentation](http://ffmpeg.org/ffmpeg.html)

## **1.3** **视频处理工具类**

### **1.3.1 拼装FFmpeg命令的各工具类**

将工具类拷贝至base工程。

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/a8fb847d3b0e4526b7d9de5f0d167f2f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/f1509663d3ef48008b3cc8326552cef3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 这些工具类由流媒体程序员编写，主要是**拼装一些FFmpeg的命令**，我们直接用就行。 

### **1.3.2 Mp4VideoUtil工具类，将视频转为mp4格式**

用于**将视频转为mp4格式**，是我们项目要使用的工具类。

> 我们要通过ffmpeg对视频转码，Mp4VideoUtil工具类调用ffmpeg，使用java.lang.ProcessBuilder去完成，具体在Mp4VideoUtil类的63行。
>
> 下边的代码运行本机安装的QQ软件：
>
> ```java
> ProcessBuilder builder = new ProcessBuilder();
> builder.command("C:\\Program Files (x86)\\Tencent\\QQ\\Bin\\QQScLauncher.exe");
> //将标准输入流和错误输入流合并，通过标准输入流程读取信息
> builder.redirectErrorStream(true);
> Process p = builder.start();
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

使用Mp4VideoUtil工具类，将avi视频转为mp4视频：

```java
public static void main(String[] args) throws IOException {
    //ffmpeg的路径
    String ffmpeg_path = "D:\\soft\\ffmpeg\\ffmpeg.exe";//ffmpeg的安装位置
    //源avi视频的路径
    String video_path = "D:\\develop\\bigfile_test\\nacos01.avi";
    //转换后mp4文件的名称
    String mp4_name = "nacos01.mp4";
    //转换后mp4文件的路径
    String mp4_path = "D:\\develop\\bigfile_test\\nacos01.mp4";
    //创建工具类对象
    Mp4VideoUtil videoUtil = new Mp4VideoUtil(ffmpeg_path,video_path,mp4_name,mp4_path);
    //开始视频转换，成功将返回success
    String s = videoUtil.generateMp4();
    System.out.println(s);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

执行main方法，最终在控制台输出 success 表示执行成功。



# **2** **分布式任务处理**

## **2.1** **任务调度介绍**

对一个视频的转码可以理解为一个任务的执行，如果**视频的数量比较多**，如何去高效处理一批任务呢？

**1、多线程**

多线程是充分利用单机的资源。

**2、分布式加多线程**

充分利用**多台计算机**，每台计算机使用**多线程**处理。

方案2可扩展性更强。

方案2是一种分布式任务调度的处理方案。

**任务调度使用场景：**

​    每隔24小时执行数据备份任务。

​    12306网站会根据车次不同，设置几个时间点分批次放票。

​    某财务系统需要在每天上午10点前结算前一天的账单数据，统计汇总。

​    商品成功发货后，需要向客户发送短信提醒。

## **2.2 单例任务调度的四种方法**

### **2.2.1 方法1：多线程+sleep**

我们可以开启一个线程，每sleep一段时间，就去检查是否已到预期执行时间。

以下代码简单实现了任务调度的功能：

```java
public static void main(String[] args) {   
    //任务执行间隔时间
    final long timeInterval = 1000;
    Runnable runnable = new Runnable() {
        public void run() {
            while (true) {
                //TODO：something
                try {
                    Thread.sleep(timeInterval);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    };
    Thread thread = new Thread(runnable);
    thread.start();
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面的代码实现了按一定的间隔时间执行任务调度的功能。

Jdk也为我们提供了相关支持，如Timer、ScheduledExecutor，下边我们了解下。

### **2.2.2 方法2：Timer类**

```java
public static void main(String[] args){ 
    Timer timer = new Timer(); 
    timer.schedule(new TimerTask(){
        @Override 
        public void run() { 
           //TODO：something
        } 
    }, 1000, 2000);  //1秒后开始调度，每2秒执行一次
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

​    Timer 的优点在于简单易用，每个Timer对应一个线程，因此可以同时启动多个Timer并行执行多个任务，同一个Timer中的任务是串行执行。

### **2.2.3 方法3：ScheduledExecutor**

```java
public static void main(String [] agrs){
    ScheduledExecutorService service = Executors.newScheduledThreadPool(10);
    service.scheduleAtFixedRate(
            new Runnable() {
                @Override
                public void run() {
                    //TODO：something
                    System.out.println("todo something");
                }
            }, 1,
            2, TimeUnit.SECONDS);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

​    Java 5 推出了基于线程池设计的 ScheduledExecutor，其设计思想是，每一个被调度的任务都会由线程池中一个线程去执行，因此任务是并发执行的，相互之间不会受到干扰。

​    Timer 和 ScheduledExecutor 都仅能提供基于开始时间与重复间隔的任务调度，不能胜任更加复杂的调度需求。比如，设置每月第一天凌晨1点执行任务、复杂调度任务的管理、任务间传递数据等等。

### **2.2.4 方法4：Quartz**

详细参考下文5-2小节，这里只写Task用法：

[【Java笔记+踩坑】SpringBoot基础3——开发。热部署+配置高级+整合NoSQL/缓存/任务/邮件/监控_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126526529)



### **2.2.5 方法5：Task（单例推荐）**



spring根据定时任务的特征，将定时任务的开发简化到了极致。怎么说呢？要做定时任务总要告诉容器有这功能吧，然后定时执行什么任务直接告诉对应的bean什么时间执行就行了，就这么简单，一起来看怎么做 

**步骤①**：**开启定时任务功能**，在引导类上开启定时任务功能的开关，使用**注解@EnableScheduling**

```java
@SpringBootApplication
//开启定时任务功能
@EnableScheduling
public class Springboot22TaskApplication {
    public static void main(String[] args) {
        SpringApplication.run(Springboot22TaskApplication.class, args);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**步骤②**：在task包下**定义Bean**，在对应要定时执行的操作上方，使用注解@Scheduled定义执行的时间，执行时间的描述方式还是cron表达式

```java
@Component
public class MyBean {
    @Scheduled(cron = "0/1 * * * * ?")
    public void print(){
        System.out.println(Thread.currentThread().getName()+" :spring task run...");
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**如何想对定时任务进行详细配置，可以通过配置文件进行**

```bash
spring:
  task:
   	scheduling:
      pool:
       	size: 1							 #任务调度线程池大小 默认 1
      thread-name-prefix: ssm_      	 #调度线程名称前缀 默认 scheduling-      
        shutdown:
          await-termination: false		 #线程池关闭时等待所有任务完成
          await-termination-period: 10s	 #调度线程关闭前最大等待时间，确保最后一定关闭
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





## **2.3 分布式任务调度介绍**

### 2.3.1 介绍 

**任务调度顾名思义，就是对任务的调度，它是指系统为了完成特定业务，基于给定时间点，给定时间间隔或者给定执行次数自动执行任务。**

**什么是分布式任务调度？**

​    通常任务调度的程序是集成在应用中的，比如：优惠卷服务中包括了定时发放优惠卷的的调度程序，结算服务中包括了定期生成报表的任务调度程序，由于采用分布式架构，一个服务往往会部署多个冗余实例来运行我们的业务，在这种分布式系统环境下运行任务调度，我们称之为**分布式任务调度**，如下图：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/ae50d95a586345af8b61f100666983e7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**分布式调度要实现的目标：**

​    不管是任务调度程序集成在应用程序中，还是单独构建的任务调度系统，如果采用分布式调度任务的方式就相当于将任务调度程序分布式构建，这样就可以具有分布式系统的特点，并且提高任务的调度处理能力：

**1、并行任务调度**

​    并行任务调度实现靠多线程，如果有大量任务需要调度，此时光靠多线程就会有瓶颈了，因为一台计算机CPU的处理能力是有限的。

​    如果将任务调度程序分布式部署，每个结点还可以部署为集群，这样就可以让多台计算机共同去完成任务调度，我们可以将任务分割为若干个分片，由不同的实例并行执行，来提高任务调度的处理效率。

**2、高可用**

​    若某一个实例宕机，不影响其他实例来执行任务。

**3、弹性扩容**

​    当集群中增加实例就可以提高并执行任务的处理效率。

**4、任务管理与监测**

​    对系统中存在的所有定时任务进行统一的管理及监测。让开发人员及运维人员能够时刻了解任务执行情况，从而做出快速的应急处理响应。

**5、避免任务重复执行**

​    当任务调度以集群方式部署，同一个任务调度可能会执行多次，比如在上面提到的电商系统中到点发优惠券的例子，就会发放多次优惠券，对公司造成很多损失，所以我们需要控制相同的任务在多个运行实例上只执行一次。

### 2.3.2 传统定时任务对比分布式任务

**传统定时任务的局限性：**

- **任务与业务耦合：**业务逻辑与定时任务逻辑放入在同一个Jar包中，如果定时任务逻辑挂了也会影响到业务逻辑；没有实现解耦
- **影响业务线程性能：**定时任务执行非常消耗cpu的资源，可能会影响到业务线程的执行
- **集群下可能重复任务：**如果服务器集群的情况下，可能存在定时任务逻辑会重复触发执行；

**分布式任务优点：**

- **并行任务调度：**并行任务调度实现靠多线程，如果有大量任务需要调度，此时光靠多线程就会有瓶颈了，因为一台计算机CPU的处理能力是有限的。如果将任务调度程序分布式部署，每个结点还可以部署为集群，这样就可以让多台计算机共同去完成任务调度，我们可以将任务分割为若干个分片，由不同的实例并行执行，来提高任务调度的处理效率。
- **高可用：**若某一个实例宕机，不影响其他实例来执行任务。
- **弹性扩容：**当集群中增加实例就可以提高并执行任务的处理效率。
- **任务管理与监测：**对系统中存在的所有定时任务进行统一的管理及监测。让开发人员及运维人员能够时刻了解任务执行情况，从而做出快速的应急处理响应。

## **2.4 XXL-JOB**

### **2.4.1 介绍**

XXL-JOB是一个**轻量级分布式任务调度平台**，其核心设计目标是开发迅速、学习简单、轻量级、易扩展。现已开放源代码并接入多家公司线上产品线，开箱即用。

> 官网：https://www.xuxueli.com/xxl-job/
>
> 文档：https://www.xuxueli.com/xxl-job/#%E3%80%8A%E5%88%86%E5%B8%83%E5%BC%8F%E4%BB%BB%E5%8A%A1%E8%B0%83%E5%BA%A6%E5%B9%B3%E5%8F%B0XXL-JOB%E3%80%8B

XXL-JOB主要有**调度中心、执行器、任务：**

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/e0318b7b93c442c6821937b733bd371d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**调度中心：**

​    负责管理调度信息，按照调度配置发出调度请求，自身不承担业务代码；

​    主要职责为**执行器管理、任务管理、监控运维、日志管理**等

**任务执行器：**

​    负责接收调度请求并执行任务逻辑；

​    只要职责是注册服务、**任务执行服务**（接收到任务后会放入线程池中的任务队列）、**执行结果上报**、日志服务等

**任务：**负责执行具体的业务处理。



调度中心与执行器之间的工作流程如下：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/010b3ddbfb19418f8752c4070f038726.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**执行流程：**

​    1.任务**执行器**根据配置的调度中心的地址，自动**注册到调度中心**

​    2.达到任务触发条件，**调度中心下发任务**

​    3.**执行器**基于线程池执行任务，并把执行结果放入**内存队列**中、把执行日志写入**日志文件**中

​    4.执行器消费内存队列中的**执行结果**，主动**上报给调度中心**

​    5.当用户在调度中心查看任务日志，调度中心请求任务执行器，**任务执行器读取任务日志文件**并返回日志详情



### **2.4.2 搭建调度中心**

**下载XXL-JOB**

GitHub：[GitHub - xuxueli/xxl-job: A distributed task scheduling framework.（分布式任务调度平台XXL-JOB）](https://github.com/xuxueli/xxl-job)

码云：[xxl-job: 一个分布式任务调度平台，其核心设计目标是开发迅速、学习简单、轻量级、易扩展。现已开放源代码并接入多家公司线上产品线，开箱即用。](https://gitee.com/xuxueli0323/xxl-job)

项目使用Linux版本的2.3.1版本： https://github.com/xuxueli/xxl-job/releases/tag/2.3.1



> **Windows版本：**
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/6188ac2917094c6aab036693c7e04a2e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> **xxl-job-admin：**调度中心
>
> **xxl-job-core：**公共依赖
>
> **xxl-job-executor-samples：**执行器Sample示例（选择合适的版本执行器，可直接使用）
>
>   ：xxl-job-executor-sample-springboot：Springboot版本，通过Springboot管理执行器，推荐这种方式；
>
>   ：xxl-job-executor-sample-frameless：无框架版本；
>
> **doc :**文档资料，包含数据库脚本

**虚拟机安装Linux版本。**

**创建xxl_job_2.3.1数据库** 

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/2d917b94e74b4d4e86d80bca07baf72b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

运行sql脚本，如下图：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/46ed6e11e1f24af79ae57d4a54f3ac83.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 运行后：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/f96fdc7215894b0e85912984dc65c39e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**自动启动xxl-job调度中心：**

```java
sh /data/soft/restart.sh
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**访问：**

```java
http://192.168.101.65:8088/xxl-job-admin/
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

账号和密码：admin/123456

如果无法使用虚拟机运行xxl-job可以在本机idea运行xxl-job调度中心。



### **2.4.3 搭建执行器，应用名对应**

执行器负责与调度中心通信接收调度中心发起的任务调度请求。

**1、进入调度中心添加执行器**

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/e83c35fa22734fc6a9255d375058f492.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



点击新增，填写执行器信息。



![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/d62629a047cb4cf5b45edb7b7947c2fc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **appname**是下面第三步在nacos中配置xxl信息时指定的执行器的应用名。
>
> **机器地址**现在填空，以后执行器配置好，并启动项目后，机器地址会显示下面yml配置的xxl执行器地址。
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/898d73ab76bd4fceba47c75fea50b7fd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

添加成功：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/22a471ae5264401aabe93d5e02955344.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**2、添加依赖**

首先在媒资管理模块的service工程添加依赖，在项目的父工程已约定了版本2.3.1

```XML
<dependency>
    <groupId>com.xuxueli</groupId>
    <artifactId>xxl-job-core</artifactId>
</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3、yml配置**

在nacos下的media-service-dev.yaml下配置xxl-job

```bash
xxl:
  job:
    admin:
      addresses: http://192.168.101.65:8088/xxl-job-admin
    executor:
      appname: media-process-service    #appname这是第一步指定的执行器应用名
      address:
      ip:
      port: 9999
      logpath: /data/applogs/xxl-job/jobhandler
      logretentiondays: 30
    accessToken: default_token
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> bootstrap.yml配置了热更新，一修改nacos就生效。
>
> **注意：**配置中的**appname**这是第一步指定的**执行器应用名**，port是执行器启动的端口，如果本地启动多个执行器注意端口不能重复。



**4、配置xxl-job的执行器**

将GitHub下载的xxl-job工程的**配置类**拷贝到媒资管理的service工程下

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/a5f6ad3dade24d17a493e1668ee49ac2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

拷贝至：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/2983c6af2ce840e4907760b62dd9efe2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```java
@Configuration
public class XxlJobConfig {
    private Logger logger = LoggerFactory.getLogger(XxlJobConfig.class);

    @Value("${xxl.job.admin.addresses}")
    private String adminAddresses;

    @Value("${xxl.job.accessToken}")
    private String accessToken;

    @Value("${xxl.job.executor.appname}")
    private String appname;

    @Value("${xxl.job.executor.address}")
    private String address;

    @Value("${xxl.job.executor.ip}")
    private String ip;

    @Value("${xxl.job.executor.port}")
    private int port;

    @Value("${xxl.job.executor.logpath}")
    private String logPath;

    @Value("${xxl.job.executor.logretentiondays}")
    private int logRetentionDays;


    @Bean
    public XxlJobSpringExecutor xxlJobExecutor() {
        logger.info(">>>>>>>>>>> xxl-job config init.");
        XxlJobSpringExecutor xxlJobSpringExecutor = new XxlJobSpringExecutor();
        xxlJobSpringExecutor.setAdminAddresses(adminAddresses);
        xxlJobSpringExecutor.setAppname(appname);
        xxlJobSpringExecutor.setAddress(address);
        xxlJobSpringExecutor.setIp(ip);
        xxlJobSpringExecutor.setPort(port);
        xxlJobSpringExecutor.setAccessToken(accessToken);
        xxlJobSpringExecutor.setLogPath(logPath);
        xxlJobSpringExecutor.setLogRetentionDays(logRetentionDays);

        return xxlJobSpringExecutor;
    }

    /**
     * 针对多网卡、容器内部署等情况，可借助 "spring-cloud-commons" 提供的 "InetUtils" 组件灵活定制注册IP；
     *
     *      1、引入依赖：
     *          <dependency>
     *             <groupId>org.springframework.cloud</groupId>
     *             <artifactId>spring-cloud-commons</artifactId>
     *             <version>${version}</version>
     *         </dependency>
     *
     *      2、配置文件，或者容器启动变量
     *          spring.cloud.inetutils.preferred-networks: 'xxx.xxx.xxx.'
     *
     *      3、获取IP
     *          String ip_ = inetUtils.findFirstNonLoopbackHostInfo().getIpAddress();
     */


}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



到此完成媒资管理模块service工程配置xxl-job执行器，在xxl-job调度中心添加执行器。





**测试执行器与调度中心是否正常通信：**

因为接口工程依赖了service工程，所以启动媒资管理模块的接口工程。

启动后观察日志，出现下边的日志表示执行器在调度中心注册成功

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/6cb7c50c4087450d9170fb6897a294ce.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

同时观察调度中心中的执行器界面

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/b8f1bd597c414eaeaeda2739bc9983af.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在线机器地址处已显示1个执行器。



### **2.4.4 测试，调度中心和项目新增任务，任务名对应**

下边编写任务，参考示例工程中任务类的编写方法，如下图：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/719706d0737047da8ff5e4dddc62141e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**1.编写任务类** 

在媒资服务service包下新建jobhandler包存放任务类，下边参考示例工程编写一个任务类

```java
package com.xuecheng.media.service.jobhandler;

/**
 * @description 测试执行器
 */
 @Component
 @Slf4j
public class SampleJob {

 /**
  * 1、简单任务示例（Bean模式）
  */

 @XxlJob("testJob")    //指定任务名称为testJob
 public void testJob() throws Exception {
  log.info("开始执行.....");

 }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2.添加任务**

下边在调度中心添加任务，进入任务管理

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/287def27786e40dca86e59cd2590bc91.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

点击新增，填写任务信息

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/c1d8f5f8bb4241dcb4d2c4373a9a653f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 具体可以查看文档。
>
> **调度类型：分为固定速度和cron。**
>
> **固定速度：**指按固定的间隔定时调度。
>
> **Cron：**通过Cron表达式实现更丰富的定时调度策略。
>
> Cron表达式是一个字符串，通过它可以定义调度策略，格式如下：
>
> {秒数} {分钟} {小时} {日期} {月份} {星期} {年份(可为空)}
>
> **JobHandler：**填注解@XxlJob里指定的任务名称。
>
> **路由策略：**
>
> 第一个：表示调度中心每次把任务下发给第一个执行器。
>
> 一致性hash：根据任务id的哈希值决定哪个执行器执行任务。
>
> 故障转移：执行器集群中某一台机器故障，会自动故障转移到另一台正常的机器发起调度请求。
>
> 分片广播**（推荐）**：后文详解
>
> 
>
> **子任务：**执行的第二个任务和第一个任务有关联。
>
> **阻塞处理策略：**
>
> 单机串行：单机阻塞时排队等待。
>
> 丢弃后续调度：阻塞时丢弃新任务。
>
> 
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/d368a8eecef948288b4b3f928b882c8c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
>  ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/3446f2bcb4ab4eb6b6a14df1d0861038.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/f97efeff39774eca87c9f864247d485d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> xxl-job提供图形界面去配置cron：
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/34ec350d9f6f46aa8e41ab141e70995b.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 一些例子如下：
>
> 30 10 1 * * ? 每天1点10分30秒触发
>
> 0/30 * * * * ? 每30秒触发一次
>
> \* 0/10 * * * ? 每10分钟触发一次
>
> 运行模式有BEAN和GLUE，bean模式较常用就是在项目工程中编写执行器的任务代码，GLUE是将任务代码编写在调度中心。
>
> JobHandler即任务方法名，填写任务方法上边@XxlJob注解中的名称。
>
> 路由策略：当执行器集群部署时，调度中心向哪个执行器下发任务，这里选择第一个表示只向第一个执行器下发任务，路由策略的其它选项稍后在分片广播章节详细解释。
>
> 高级配置的其它配置项稍后在分片广播章节详细解释。



**3.选择执行器、启动任务**

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/8e6bd7e2f69540729e10734b2b5bc26c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

通过调度日志查看任务执行情况

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/dbb9c7c47db14da584bbc538a8f9e4a4.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**4.启动媒资管理的service工程，启动执行器。**

观察执行器方法的执行。

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/7e9b4b9b7790470a9fc5cb92a98ab0ee.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如果要停止任务需要在调度中心操作

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/4ae8870c77784cffbebbbc00a095bcdc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

任务跑一段时间注意清理日志

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/66ad4a3da9d9483e84fa585a6eaa6195.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **2.4.5** 任务配置详解

xxl-job官方文档**高级配置：**
   **- 路由策略：**当执行器集群部署时，提供丰富的路由策略，包括；
     FIRST（第一个）：固定选择第一个机器；
     LAST（最后一个）：固定选择最后一个机器；
     ROUND（轮询）：；
     RANDOM（随机）：随机选择在线的机器；
     CONSISTENT_HASH（一致性HASH）：每个任务按照Hash算法固定选择某一台机器，且所有任务均匀散列在不同机器上。
     LEAST_FREQUENTLY_USED（最不经常使用）：使用频率最低的机器优先被选举；
     LEAST_RECENTLY_USED（最近最久未使用）：最久未使用的机器优先被选举；
     FAILOVER（故障转移）：按照顺序依次进行心跳检测，第一个心跳检测成功的机器选定为目标执行器并发起调度；
     BUSYOVER（忙碌转移）：按照顺序依次进行空闲检测，第一个空闲检测成功的机器选定为目标执行器并发起调度；
     SHARDING_BROADCAST(分片广播)：广播触发对应集群中所有机器执行一次任务，同时系统自动传递分片参数；可根据分片参数开发分片任务；

  **- 子任务：**每个任务都拥有一个唯一的任务ID(任务ID可以从任务列表获取)，当本任务执行结束并且执行成功时，将会触发子任务ID所对应的任务的一次主动调度，通过子任务可以实现一个任务执行完成去执行另一个任务。
   **- 调度过期策略：**
     \- 忽略：调度过期后，忽略过期的任务，从当前时间开始重新计算下次触发时间；
     \- 立即执行一次：调度过期后，立即执行一次，并从当前时间开始重新计算下次触发时间；
   \- 阻塞处理策略：调度过于密集执行器来不及处理时的处理策略；
     单机串行（默认）：调度请求进入单机执行器后，调度请求进入FIFO队列并以串行方式运行；
     丢弃后续调度：调度请求进入单机执行器后，发现执行器存在运行的调度任务，本次请求将会被丢弃并标记为失败；
     覆盖之前调度：调度请求进入单机执行器后，发现执行器存在运行的调度任务，将会终止运行中的调度任务并清空队列，然后运行本地调度任务；
   \- 任务超时时间：支持自定义任务超时时间，任务运行超时将会主动中断任务；
   \- 失败重试次数；支持自定义任务失败重试次数，当任务失败时将会按照预设的失败重试次数主动进行重试；

### **2.4.6 分片广播**

**分片**

分片是指是调度中心**以执行器为维度进行分片**，将集群中的执行器标上序号：0，1，2，3...。

**广播**

广播是指每次调度会向集群中的所有执行器**发送任务调度**，请求中**携带分片参数（序号和数量）**。每个执行器收到调度请求同时接收**分片参数**。

调度中心调度集群中的所有执行器，让每个执行器执行任务群的一部分。

如下图：调度中心向第一个执行器发送任务调度，携带参数0和3，0是该执行器序号，3是集群里执行器数量。

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/5cc0ea212d1a4697a52e611ac9670737.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





xxl-job支持**动态扩容执行器集群**从而动态增加分片数量，当有任务量增加可以部署更多的执行器到集群中，调度中心会动态修改分片的数量。

**作业分片适用哪些场景呢？**

- 分片任务场景：10个执行器的集群来处理10w条数据，每台机器只需要处理1w条数据，耗时降低10倍；

- 广播任务场景：广播执行器同时运行shell脚本、广播集群节点进行缓存更新等。

所以，广播分片方式不仅可以充分发挥每个执行器的能力，并且根据分片参数可以控制任务是否执行，最终灵活控制了执行器集群分布式处理任务。



**使用说明：**

"分片广播" 和普通任务开发流程一致，不同之处在于可以**获取分片参数**进行分片业务处理。

**Java任务获取分片参数方式：**

BEAN、GLUE模式(Java)，可参考Sample示例执行器中的示例任务"ShardingJobHandler"：

```java
/**
 * 2、分片广播任务
 */
@XxlJob("shardingJobHandler")
public void shardingJobHandler() throws Exception {
    // 分片序号，从0开始
    int shardIndex = XxlJobHelper.getShardIndex();
    // 分片总数
    int shardTotal = XxlJobHelper.getShardTotal();
    ....
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **2.4.7 测试分片和动态扩容**

1、定义作业分片的任务方法

```java
/**
  * 2、分片广播任务
  */
 @XxlJob("shardingJobHandler")
 public void shardingJobHandler() throws Exception {

  // 分片参数
  int shardIndex = XxlJobHelper.getShardIndex();
  int shardTotal = XxlJobHelper.getShardTotal();

log.info("分片参数：当前分片序号 = {}, 总分片数 = {}", shardIndex, shardTotal);
log.info("开始执行第"+shardIndex+"批任务");

 }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2、在调度中心添加任务

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/2b358f2f94644bc2924812cfc47994cd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> JobHandler要和@XxlJob("shardingJobHandler")配置的任务名名一致。

添加成功：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/e0cee48df3fd47f3bb90cbce0a4de8f9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

启动任务，观察日志

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/5ce52d17991a44808cc59541353a6335.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**启动两个执行器实例** 

下边启动两个执行器实例，观察每个实例的执行情况

首先在nacos中配置media-service的本地优先配置：

```bash
#配置本地优先
spring:
 cloud:
  config:
    override-none: true
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

将media-service启动两个实例

两个实例的在启动时注意端口不能冲突：

实例1 在VM options处添加：-Dserver.port=63051 -Dxxl.job.executor.port=9998

实例2 在VM options处添加：-Dserver.port=63050 -Dxxl.job.executor.port=9999

例如：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/9142c34d56604d36a63440facc3b4dc1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



观察任务调度中心，稍等片刻执行器有两个



![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/1c58a59588a248b4a51561e9d2467d57.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**观察两个执行实例的日志：**

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/73c4155fe93140dc971d835227fe68d6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

另一实例的日志如下：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/e9c59a54bd944de9905fa86d61568e30.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

从日志可以看每个实例的分片序号不同。

**测试动态扩容**：

此时，如果其中一个执行器挂掉，只剩下一个执行器在工作，稍等片刻调用中心发现少了一个执行器将动态调整总分片数为1。如果新增实例，也会动态调整总片数。









# **3** **技术方案**

## **3.1** **作业分片方案**

> **思考：**如何分布式去执行学成在线平台中的视频处理任务？

> **思考：**
>
> 任务添加成功后，对于要处理的任务会添加到待处理任务表中，现在启动多个执行器实例去查询这些待处理任务，此时如何保证多个执行器不会查询到重复的任务呢？
>
> 答：**取余**。任务序号%分片数量。

XXL-JOB并不直接提供数据处理的功能，它只会给执行器分配好分片序号，在向执行器任务调度的同时下发分片总数以及分片序号等参数，执行器收到这些参数根据自己的业务需求去利用这些参数。

下图表示了多个执行器获取视频处理任务的结构：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/4ee46a5ba73a44f6b48ddc08ca1fd8ad.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

每个执行器收到广播任务有两个参数：分片总数、分片序号。每个执行从数据表取任务时可以让**任务id % 分片总数**，如果等于分片序号则执行此任务。

上边两个执行器实例那么分片总数为2，序号为0、1，从任务1开始，如下：

1 % 2 = 1  执行器2执行

2 % 2 = 0  执行器1执行

3 % 2 = 1   执行器2执行

以此类推.

## **3.2** **保证任务不重复执行，设置策略和保证幂等性（分布式锁）**

通过作业分片方案保证了执行器之间查询到不重复的任务，如果一个执行器在处理一个视频还没有完成，此时调度中心又一次请求调度，为了不重复处理同一个视频该怎么办？

结论：**调度过期策略为“忽略” ，阻塞处理策略为“丢弃后续调度”。并且要保证任务的幂等性（将所有任务存入一个表里，用一个字段标记此任务状态）。**

**首先配置调度过期策略：**

查看文档如下：

  **- 调度过期策略：**调度中心错过调度时间的补偿处理策略，比如理应10点调度，因为某些原因没有调度，就过期了。包括：忽略、立即补偿触发一次等；
     **- 忽略（推荐）：**调度过期后，忽略过期的任务，从当前时间开始**重新计算下次触发时间**；
     \- 立即执行一次：调度过期后，立即执行一次，并从当前时间开始重新计算下次触发时间；很可能重复执行
   **- 阻塞处理策略：**调度过于密集执行器来不及处理时的处理策略；

这里我们选择忽略，如果立即执行一次就可能重复执行相同的任务。

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/ae740b10825549cd906050a4785ed834.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

其次，再看**阻塞处理策略**，阻塞处理策略就是当前执行器正在执行任务还没有结束时调度中心进行任务调度，此时该如何处理。

查看文档如下：
     **单机串行（默认）：**调度请求进入单机执行器后，调度请求进入FIFO队列并以串行方式运行；
     **丢弃后续调度（推荐）：**调度请求进入单机执行器后，发现执行器存在运行的调度任务，本次请求将会被丢弃并标记为失败；
     **覆盖之前调度：**调度请求进入单机执行器后，发现执行器存在运行的调度任务，将会终止运行中的调度任务并清空队列，然后运行本地调度任务；

这里如果选择覆盖之前调度则可能重复执行任务，这里选择 丢弃后续调度或单机串行方式来避免任务重复执行。



**只做这些配置可以保证任务不会重复执行吗？**

做不到，还需要保证任务处理的幂等性，什么是任务的幂等性？任务的幂等性是指：对于数据的操作不论多少次，操作的结果始终是一致的。在本项目中要实现的是不论多少次任务调度同一个视频只执行一次成功的转码。

什么是幂等性？

它描述了一次和多次请求某一个资源**对于资源本身应该具有同样的结果**。

幂等性是为了解决重复提交问题，比如：**恶意刷单，重复支付**等。

**解决幂等性常用的方案：**

1)数据库约束，比如: 唯一索引，主键。同一个主键不可能两次都插入成功。

2)乐观锁。数据库表中增加一个版本字段，更新时判断是否等于某个版本

3)唯一序列号。Redis键为任务id，值为随机序列化uuid。请求前生成唯一的序列号，携带序列号去请求，执行时在redis记录该序列号表示以该序列号的请求执行过了，如果相同的序列号再次来执行说明是重复执行。

基于以上分析，在执行器接收调度请求去执行视频处理任务时要实现视频处理的幂等性，要有办法去**判断该视频是否处理完成**，如果正在处理中或处理完则不再处理。这里我们在数据库视频处理表中添加处理状态字段，视频处理完成更新状态为完成，执行视频处理前判断状态是否完成，如果完成则不再处理。



## **3.3** **视频处理业务流程图**

确定了分片方案，下边梳理整个视频上传及处理的业务流程。

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/bfbae53c597847fdb9fd27f4afd1ac0f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**上传视频成功向视频待处理表添加记录。**

视频处理的详细流程如下：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/75a9cdbc477c4b07a6aa8c2522b752be.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

1、任务调度中心广播作业分片。

2、执行器收到广播作业分片，从数据库读取待处理任务，读取未处理及处理失败的任务。

3、执行器更新任务为处理中，根据任务内容从MinIO下载要处理的文件。

4、执行器启动多线程去处理任务。

5、任务处理完成，上传处理后的视频到MinIO。

6、将更新任务处理结果，如果视频处理完成除了更新任务处理结果以外还要将文件的访问地址更新至任务处理表及文件表中，最后将任务完成记录写入历史表。





# **4** **查询待处理任务**

## **4.1** **需求，待处理任务表、历史任务表**

> 需求：
>
> 查询待处理任务只处理**未提交及处理失败**的任务，任务处理失败后进行重试，最多**重试3次**。任务处理成功将待处理记录移动到**历史任务表**。



下图是待处理任务表：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/5854a409f9d04b2cb33a31ec29f41b8f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



历史任务表与待处理任务表的结构相同，存放已经执行完成的任务。 









## **4.2** **添加待处理任务，在文件入库之后**

上传视频成功向视频处理待处理表添加记录，暂时只添加对avi视频的处理记录。

根据MIME Type去判断是否是avi视频，下边列出部分MIME Type

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/7c2813da5e1445dea892de5586e3756e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

avi视频的MIME Type是video/x-msvideo

修改文件信息入库方法，如果视频是avi类型（以后可以扩展mpeg等其他类型），就放入待处理任务表：

```java
@Transactional
public MediaFiles addMediaFilesToDb(Long companyId, String fileMd5, UploadFileParamsDto uploadFileParamsDto, String bucket, String objectName) {
    //从数据库查询文件
    MediaFiles mediaFiles = mediaFilesMapper.selectById(fileMd5);
    if (mediaFiles == null) {
        mediaFiles = new MediaFiles();
        //拷贝基本信息
        BeanUtils.copyProperties(uploadFileParamsDto, mediaFiles);
        mediaFiles.setId(fileMd5);
        mediaFiles.setFileId(fileMd5);
        mediaFiles.setCompanyId(companyId);
        //媒体类型
        mediaFiles.setUrl("/" + bucket + "/" + objectName);
        mediaFiles.setBucket(bucket);
        mediaFiles.setFilePath(objectName);
        mediaFiles.setCreateDate(LocalDateTime.now());
        mediaFiles.setAuditStatus("002003");
        mediaFiles.setStatus("1");
        //保存文件信息到文件表
        int insert = mediaFilesMapper.insert(mediaFiles);
        if (insert < 0) {
            log.error("保存文件信息到数据库失败,{}", mediaFiles.toString());
            XueChengPlusException.cast("保存文件信息失败");
        }
        //添加到待处理任务表
        addWaitingTask(mediaFiles);
        log.debug("保存文件信息到数据库成功,{}", mediaFiles.toString());

    }
    return mediaFiles;

}

/**
 * 添加待处理任务
 * @param mediaFiles 媒资文件信息
 */
private void addWaitingTask(MediaFiles mediaFiles){
    //文件名称
    String filename = mediaFiles.getFilename();
    //文件扩展名
    String extension = filename.substring(filename.lastIndexOf("."));
    //文件mimeType
    String mimeType = getMimeType(extension);
    //如果是avi视频添加到视频待处理表
    if(mimeType.equals("video/x-msvideo")){
        MediaProcess mediaProcess = new MediaProcess();
        BeanUtils.copyProperties(mediaFiles,mediaProcess);
        mediaProcess.setStatus("1");//未处理
        mediaProcess.setFailCount(0);//失败次数默认为0
        mediaProcessMapper.insert(mediaProcess);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**测试：**

进行前后端测试，上传4个avi视频，观察待处理任务表是否存在记录，记录是否完成。

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/665d1cf09d0e4f5cb04f43a3ac8b2aa9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

可以看见插入了待处理任务：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/6f7fb9fd024449879856af01cf251eb9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## **4.3** 根据分片参数和数量限制**查询待处理任务列表**

如何保证查询到的待处理视频记录不重复？



### 4.3.1 sql语句

假设有两个执行器，查询0号执行器未处理或失败次数小于3的任务，仅查两条： 

```sql
select * from media_process t where t.id % 2 = 0 and (t,status=1 or t,status=3) and t.fail_count<3 limit 2
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 4.3.2 mapper，查询待处理任务列表

编写根据分片参数获取待处理任务的DAO方法，定义DAO接口如下：

```java
public interface MediaProcessMapper extends BaseMapper<MediaProcess> {
    /**
     * @description 根据分片参数获取待处理任务
     * @param shardTotal  分片总数
     * @param shardindex  分片序号
     * @param count 任务数
     * @return java.util.List<com.xuecheng.media.model.po.MediaProcess
    */
    @Select("select * from media_process t where t.id % #{shardTotal} = #{shardIndex} and (t.status = '1' or t.status = '3') and t.fail_count < 3 limit #{count}")
    List<MediaProcess> selectListByShardIndex(@Param("shardTotal") int shardTotal,@Param("shardIndex") int shardIndex,@Param("count") int count);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 4.3.3 service，根据分片参数和数量限制**查询待处理任务列表**

```java
package com.xuecheng.media.service.impl;


@Slf4j
@Service
public class MediaFileProcessServiceImpl implements MediaFileProcessService {

 @Autowired
 MediaFilesMapper mediaFilesMapper;

 @Autowired
 MediaProcessMapper mediaProcessMapper;


 @Override
 public List<MediaProcess> getMediaProcessList(int shardIndex, int shardTotal, int count) {
  List<MediaProcess> mediaProcesses = mediaProcessMapper.selectListByShardIndex(shardTotal, shardIndex, count);
   return mediaProcesses;
 }


}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# **5** **开始执行任务**

## **5.1** **分布式锁**

### 5.1.1 调度中心弹性扩容导致重复任务问题

前边分析了保证任务不重复执行的方案，理论上每个执行器分到的任务是不重复的，但是当在执行器**弹性扩容时**无法绝对避免任务不重复执行。

比如：原来有四个执行器正在执行任务，由于网络问题原有的0、1号执行器无法与调度中心通信，调度中心就会对执行器重新编号，原来的2、3执行器可能就会执行和0、1号执行器相同的任务。

> **单例锁和分布式锁**
>
> 为了避免多线程去争抢同一个任务可以使用**synchronized同步锁**去解决，如下代码：
>
> ```java
> synchronized(锁对象){
>    执行任务...
> }
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> synchronized只能保证同一个虚拟机中多个线程去争抢锁。
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/2ff40db532b34880b76d07d9801187c2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 如果是多个执行器分布式部署，并不能保证同一个视频只有一个执行器去处理。
>
> 现在要实现分布式环境下所有虚拟机中的线程去同步执行就需要让多个虚拟机去共用一个锁，虚拟机可以分布式部署，锁也可以分布式部署，如下图：
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/6693357974064aca831164a98ab216c0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> 虚拟机都去抢占同一个锁，锁是一个单独的程序提供加锁、解锁服务。
>
> **该锁已不属于某个虚拟机，而是分布式部署，由多个虚拟机所共享，这种锁叫分布式锁。**

### 5.1.2 **实现分布式锁的三种方法，数据库、redis、zookeeper**

**1、基于数据库唯一索引实现分布锁（本项目使用）**

唯一索引：例如两个线程同时插入id为1的数据，将只有一个线程能插入成功，因为主键id具有唯一性。

**乐观锁**是这种方式。利用数据库主键唯一性的特点，或利用数据库唯一索引、行级锁的特点，比如：多个线程同时向数据库插入主键相同的同一条记录，谁插入成功谁就获取锁，多个线程同时去更新相同的记录，谁更新成功谁就抢到锁。

**2、基于redis实现锁**

redis提供了分布式锁的实现方案，比如：SETNX、set nx、redisson等。

拿SETNX举例说明，SETNX命令的工作过程是去set一个不存在的key，多个线程去设置同一个key只会有一个线程设置成功，设置成功的的线程拿到锁。

**3、使用zookeeper实现**

zookeeper是一个分布式协调服务，主要解决分布式程序之间的同步的问题。zookeeper的结构类似的文件目录，多线程向zookeeper创建一个子目录(节点)只会有一个创建成功，利用此特点可以实现分布式锁，谁创建该结点成功谁就获得锁。

本次我们选用数据库实现分布锁，后边的模块会选用其它方案到时再详细介绍。

## **5.2 开启任务**

### **5.2.1 乐观锁实现方法**

> **synchronized是一种悲观锁**，在执行被synchronized包裹的代码时需要**首先获取锁**，没有拿到锁则无法执行，是**总悲观的认为别的线程会去抢**，所以要悲观锁。
>
> **乐观锁**的思想是它不认为会有线程去争抢，**尽管去执行**，如果**没有执行成功就再去重试**。



**乐观锁实现步骤：** 

数据库的乐观锁实现方式是在表中**增加一个版本字段**，**更新时判断是否等于某个版本**，等于则更新否则更新失败，如下方式。

```sql
update t1 set t1.data1 = '',t1.version='2' where t1.version='1'
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### **5.2.2 sql语句，修改任务状态为“处理中”**



下边基于**数据库方式**实现分布锁，开始执行任务将任务执行状态更新为4表示任务执行中。

**使用乐观锁方式实现更新操作：**

第一个人把状态字段由“未处理”或“处理失败”改为“处理中” ，第一个人就拿到了锁；第二个人再想执行更新状态语句会发现条件不满足，因为状态不是“未处理”或“处理失败”了：

```sql
update media_process m set m.status='4' where (m.status='1' or m.status='3') and m.fail_count<3 and m.id=?
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 状态,1:未处理，2：处理成功  3处理失败 4处理中 

多个线程同时执行上边的sql只会有一个线程执行成功。



### **5.2.3** mapper**，修改任务状态为“处理中”**

```java
public interface MediaProcessMapper extends BaseMapper<MediaProcess> {

    /**
     * 开启一个任务
     * @param id 任务id
     * @return 更新记录数
     */
    @Update("update media_process m set m.status='4' where (m.status='1' or m.status='3') and m.fail_count<3 and m.id=#{id}")
    int startTask(@Param("id") long id);

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### **5.2.4** service**，修改任务状态为“处理中”**

MediaFileProcessServiceImpl

```java
/**
 *  开启一个任务
 * @param id 任务id
 * @return true开启任务成功，false开启任务失败
 */

public boolean startTask(long id) {
    int result = mediaProcessMapper.startTask(id);
    return result<=0?false:true;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# **6 保存任务结果**

> 需求：
>
> 任务处理完成需要更新任务处理结果。
>
> 任务执行成功更新视频的URL、及任务处理结果，将待处理任务记录删除，同时向历史任务表添加记录。

service：

```java
package com.xuecheng.media.service.impl;

@Slf4j
@Service
public class MediaFileProcessServiceImpl implements MediaFileProcessService {

 @Autowired
 MediaFilesMapper mediaFilesMapper;

 @Autowired
 MediaProcessMapper mediaProcessMapper;

 @Autowired
 MediaProcessHistoryMapper mediaProcessHistoryMapper;

/**
 * @description 保存任务结果
 * @param taskId  任务id
 * @param status 任务状态
 * @param fileId  文件id
 * @param url url
 * @param errorMsg 错误信息
 */

@Transactional
@Override
public void saveProcessFinishStatus(Long taskId, String status, String fileId, String url, String errorMsg) {
    //查出任务，如果不存在则直接返回
    MediaProcess mediaProcess = mediaProcessMapper.selectById(taskId);
    if(mediaProcess == null){
        return ;
    }
    //处理失败，更新任务处理结果
    LambdaQueryWrapper<MediaProcess> queryWrapperById = new LambdaQueryWrapper<MediaProcess>().eq(MediaProcess::getId, taskId);
    //处理失败
    if(status.equals("3")){
        MediaProcess mediaProcess_u = new MediaProcess();
        mediaProcess_u.setStatus("3");
        mediaProcess_u.setErrormsg(errorMsg);
        mediaProcess_u.setFailCount(mediaProcess.getFailCount()+1);
        mediaProcessMapper.update(mediaProcess_u,queryWrapperById);
        log.debug("更新任务处理状态为失败，任务信息:{}",mediaProcess_u);
        return ;
    }
    //任务处理成功
    MediaFiles mediaFiles = mediaFilesMapper.selectById(fileId);
    if(mediaFiles!=null){
        //更新媒资文件表中的访问url
        mediaFiles.setUrl(url);
        mediaFilesMapper.updateById(mediaFiles);
    }
    //处理成功，更新url和状态
    mediaProcess.setUrl(url);
    mediaProcess.setStatus("2");
    mediaProcess.setFinishDate(LocalDateTime.now());
    mediaProcessMapper.updateById(mediaProcess);

    //添加到历史记录
    MediaProcessHistory mediaProcessHistory = new MediaProcessHistory();
    BeanUtils.copyProperties(mediaProcess, mediaProcessHistory);
    mediaProcessHistoryMapper.insert(mediaProcessHistory);
    //删除mediaProcess
    mediaProcessMapper.deleteById(mediaProcess.getId());

}

 @Override
 public List<MediaProcess> getMediaProcessList(int shardIndex, int shardTotal, int count) {
  List<MediaProcess> mediaProcesses = mediaProcessMapper.selectListByShardIndex(shardTotal, shardIndex, count);
   return mediaProcesses;
 }


}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# **7 视频处理任务类，@Component和@XxlJob**

视频采用并发处理，每个视频使用一个**线程**去处理，每次处理的视频数量不要超过**cpu核心数**。

所有视频处理完成结束本次执行，为阻塞主线程并且防止代码异常出现无限期等待则添加**超时设置**，到达超时时间还没有处理完成仍结束任务。

定义任务类VideoTask 如下：

```java
package com.xuecheng.media.service.jobhander;

@Slf4j
@Component
public class VideoTask {

    @Autowired
    MediaFileService mediaFileService;
    @Autowired
    MediaFileProcessService mediaFileProcessService;


    @Value("${videoprocess.ffmpegpath}")
    String ffmpegpath;

    @XxlJob("videoJobHandler")
    public void videoJobHandler() throws Exception {

        // 分片参数
    int shardIndex = XxlJobHelper.getShardIndex();
    int shardTotal = XxlJobHelper.getShardTotal();
    List<MediaProcess> mediaProcessList = null;
    int size = 0;
    try {
        //取出可用的cpu核心数。这个方法返回可用处理器的Java虚拟机的数量
        int processors = Runtime.getRuntime().availableProcessors();
        //每次任务处理视频的数量不要超过cpu核心数
        mediaProcessList = mediaFileProcessService.getMediaProcessList(shardIndex, shardTotal, processors);
        size = mediaProcessList.size();
        log.debug("取出待处理视频任务{}条", size);
//没有待处理任务了
        if (size <= 0) {
            return;
        }
    } catch (Exception e) {
        e.printStackTrace();
        return;
    }
    //创建size个线程的线程池。这是执行器工具类方法创建线程池，也可以自定义线程池ThreadPoolExecutor配置类注入方式
    ExecutorService threadPool = Executors.newFixedThreadPool(size);
    //计数器，也叫闭锁。主要为了后面await()方法阻塞主线程直到子线程全部执行结束（计数器减为零）或到超时时间。
//本项目里其实不用计数器也可以，因为主线程后面并没有方法逻辑。
    CountDownLatch countDownLatch = new CountDownLatch(size);
    //将处理任务加入线程池
    mediaProcessList.forEach(mediaProcess -> {
//列表里每个任务启动一个线程。
        threadPool.execute(() -> {
            try {
                //任务id
                Long taskId = mediaProcess.getId();
                //开启任务，乐观锁防止重复消费，修改任务状态为“处理中”
                boolean b = mediaFileProcessService.startTask(taskId);
                if (!b) {
                    return;
                }
                log.debug("开始执行任务:{}", mediaProcess);
                //下边是处理逻辑
                //桶
                String bucket = mediaProcess.getBucket();
                //存储路径
                String filePath = mediaProcess.getFilePath();
                //原始视频的md5值
                String fileId = mediaProcess.getFileId();
                //原始文件名称
                String filename = mediaProcess.getFilename();
                //将要处理的文件下载到服务器上
                File originalFile = mediaFileService.downloadFileFromMinIO(mediaProcess.getBucket(), mediaProcess.getFilePath());
                if (originalFile == null) {
//下载待处理文件失败，保存任务结果
                    log.debug("下载待处理文件失败,originalFile:{}", mediaProcess.getBucket().concat(mediaProcess.getFilePath()));
                    mediaFileProcessService.saveProcessFinishStatus(mediaProcess.getId(), "3", fileId, null, "下载待处理文件失败");
                    return;
                }
                
//创建mp4临时文件
                File mp4File = null;
                try {
                    mp4File = File.createTempFile("mp4", ".mp4");
                } catch (IOException e) {
                    log.error("创建mp4临时文件失败");
                    mediaFileProcessService.saveProcessFinishStatus(mediaProcess.getId(),
                         "3", fileId, null, "创建mp4临时文件失败");
                    return;
                }
                //处理视频
                String result = "";
                try {
                    //开始处理视频，通过ffmpeg将下载的源文件转码成mp4文件
                    Mp4VideoUtil videoUtil = new Mp4VideoUtil(ffmpegpath, originalFile.getAbsolutePath(), mp4File.getName(), mp4File.getAbsolutePath());
                    //开始视频转换，成功将返回success
                    result = videoUtil.generateMp4();
                } catch (Exception e) {
                    e.printStackTrace();
                    log.error("处理视频文件:{},出错:{}", mediaProcess.getFilePath(), e.getMessage());
                }
                if (!result.equals("success")) {
                    //记录错误信息
                    log.error("处理视频失败,视频地址:{},错误信息:{}", bucket + filePath, result);
                    mediaFileProcessService.saveProcessFinishStatus(mediaProcess.getId(), "3", fileId, null, result);
                    return;
                }
   
                //将mp4上传至minio
                //mp4在minio的存储路径
                String objectName = getFilePath(fileId, ".mp4");
                //访问url
                String url = "/" + bucket + "/" + objectName;
                try {
                    mediaFileService.addMediaFilesToMinIO(mp4File.getAbsolutePath(), "video/mp4", bucket, objectName);
                    //将url存储至数据，并更新状态为成功，并将待处理视频记录删除存入历史
                    mediaFileProcessService.saveProcessFinishStatus(mediaProcess.getId(), "2", fileId, url, null);
                } catch (Exception e) {
                    log.error("上传视频失败或入库失败,视频地址:{},错误信息:{}", bucket + objectName, e.getMessage());
                    //最终还是失败了
                    mediaFileProcessService.saveProcessFinishStatus(mediaProcess.getId(), "3", fileId, null, "处理后视频上传或入库失败");
                }
            }finally {
//finally里，不管成功还是失败计数器都减一
                countDownLatch.countDown();
            }
        });
    });

    //计时器减成0之前或者指定时间之前一直阻塞。给一个充裕的超时时间,防止无限等待，到达超时时间还没有处理完成则结束任务
    countDownLatch.await(30, TimeUnit.MINUTES);
    log.info("本行代码将在计数器减为零或30分钟后，才能执行");
    }

    private String getFilePath(String fileMd5,String fileExt){
        return   fileMd5.substring(0,1) + "/" + fileMd5.substring(1,2) + "/" + fileMd5 + "/" +fileMd5 +fileExt;
    }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 上面任务将每5秒执行一次：
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/7b2d1da993d24f6d913f290d578b1790.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 8 上传视频存库后添加待处理任务

MediaFileServiceImpl 

```java
    /**
     * @param companyId           机构id
     * @param fileMd5             文件md5值
     * @param uploadFileParamsDto 上传文件的信息
     * @param bucket              桶
     * @param objectName          对象名称
     * @return com.xuecheng.media.model.po.MediaFiles
     * @description 将文件信息添加到文件表
     * @author Mr.M
     * @date 2022/10/12 21:22
     */
    @Transactional
    public MediaFiles addMediaFilesToDb(Long companyId, String fileMd5, UploadFileParamsDto uploadFileParamsDto, String bucket, String objectName) {
        //将文件信息保存到数据库
        MediaFiles mediaFiles = mediaFilesMapper.selectById(fileMd5);
        if (mediaFiles == null) {
            mediaFiles = new MediaFiles();
            BeanUtils.copyProperties(uploadFileParamsDto, mediaFiles);
            //文件id
            mediaFiles.setId(fileMd5);
            //机构id
            mediaFiles.setCompanyId(companyId);
            //桶
            mediaFiles.setBucket(bucket);
            //file_path
            mediaFiles.setFilePath(objectName);
            //file_id
            mediaFiles.setFileId(fileMd5);
            //url
            mediaFiles.setUrl("/" + bucket + "/" + objectName);
            //上传时间
            mediaFiles.setCreateDate(LocalDateTime.now());
            //状态
            mediaFiles.setStatus("1");
            //审核状态
            mediaFiles.setAuditStatus("002003");
            //插入数据库
            int insert = mediaFilesMapper.insert(mediaFiles);
            if (insert <= 0) {
                log.debug("向数据库保存文件失败,bucket:{},objectName:{}", bucket, objectName);
                return null;
            }
            //记录待处理任务
            addWaitingTask(mediaFiles);

            return mediaFiles;

        }
        return mediaFiles;

    }


    /**
     * 添加待处理任务
     *
     * @param mediaFiles 媒资文件信息
     */
    private void addWaitingTask(MediaFiles mediaFiles) {

        //文件名称
        String filename = mediaFiles.getFilename();
        //文件扩展名
        String extension = filename.substring(filename.lastIndexOf("."));
        //获取文件的 mimeType
        String mimeType = getMimeType(extension);
        if (mimeType.equals("video/x-msvideo")) {//如果是avi视频写入待处理任务
            MediaProcess mediaProcess = new MediaProcess();
            BeanUtils.copyProperties(mediaFiles, mediaProcess);
            //状态是未处理
            mediaProcess.setStatus("1");
            mediaProcess.setCreateDate(LocalDateTime.now());
            mediaProcess.setFailCount(0);//失败次数默认0
            mediaProcess.setUrl(null);
            mediaProcessMapper.insert(mediaProcess);

        }

    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# **9** 调度中心添加执行器和任务

1.linux安装调度中心，导入数据库表，访问网页新增执行器，设置**应用名**

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/95b23305e5f841309f055cf07eb9d457.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



2.导入依赖、yml配置调度中心地址和执行器**应用名**、配置类XxlJobSpringExecutor对象注入yml配置

媒资服务： 

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/7d186f865f724ef0a70380b91de974d7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3. @Component和@XxlJob("任务名")设置任务
4. 调度中心网页新增任务，设置任务名、cron、路由策略、阻塞策略、调度过期策略（设为忽略） 

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/7b2d1da993d24f6d913f290d578b1790.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/e5e80f4052424bff917e351b4b0162b3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 任务调度策略，防止任务重复消费。

5.启动服务，发现执行器已经自动注册，开启任务：

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/383505ba0b1641bf91f7771dd984b490.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/2ce63af4a6c741298876239412f6e3a2.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 



# 10 测试 

## 10.1 成功测试

> 将媒资任务表后两个任务路径故意弄错，从而模拟两个成功两个失败的情况：
>
> ![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/3f22601bbdc14370819878f826a7bd06.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

配置完成开始测试视频处理：

1、首先上传至少4个视频，非mp4格式。

2、在xxl-job启动视频处理任务

3、观察媒资管理服务后台日志

## 10**.2 失败测试**

1、先停止调度中心的视频处理任务。

2、上传视频，手动修改待处理任务表中file_path字段为一个不存在的文件地址

3、启动任务

观察任务处理失败后是否会重试，并记录失败次数。

## 10**.3 抢占任务测试**

1、修改调度中心中视频处理任务的阻塞处理策略为“覆盖之间的调度”

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/f835a567c7ea4e03adc60e3c55822830.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2、在抢占任务代码处打断点并选择支持多线程方式

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/ea286e43cee549c88895443c27d799d9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3、在抢占任务代码处的下边两行代码分别打上断点，避免观察时代码继续执行。

4、启动任务

此时多个线程执行都停留在断点处

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/1f4074b08d174f4eb26c32ed602e0210.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

依次放行，观察同一个任务只会被一个线程抢占成功。

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/6f559fe6f21a43af941ef1ce2b5e86ec.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](学成在线笔记+踩坑（6）——【媒资模块】视频处理。FFmpeg+XXL-JOB.assets/5c7093c5d20641e9a94924bb86cf4c00.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# **11** **其它问题**

## **11.1** **任务补偿机制，定期查询处理超时的任务**

如果有线程抢占了某个视频的处理任务，如果**线程处理过程中挂掉了**，该视频的状态将会**一直是处理中**，其它线程将无法处理，这个问题需要用**补偿机制**。

单独启动一个任务，定期查询待处理任务表中**超过执行期限但仍在处理中的任务**，将任务的状态改为**执行失败**。

任务执行期限是处理一个视频的最大时间，比如定为30分钟，通过任务的启动时间去判断任务是否超过执行期限。



## **11.2 失败次数****达到最大失败次数，人工处理**

当任务达到最大失败次数时一般就说明程序处理此视频存在问题，这种情况就需要**人工处理**，在页面上会提示失败的信息，人工可手动执行该视频进行处理，或通过其它转码工具进行视频转码，转码后直接上传mp4视频。



## **11.3 定期扫描清理垃圾****分块文件**

上传一个文件进行分块上传，上传一半不传了，之前上传到minio的分块文件要清理吗？怎么做的？

1、新建一个文件表记录minio中存储的文件信息。

2、文件开始上传时就写入文件表，状态为上传中，上传完成会更新状态为上传完成。

3、当一个文件传了一半不再上传了说明该文件没有上传完成，会有定时任务去查询文件表中的记录，如果文件未上传完成则删除minio中没有上传成功的文件目录。