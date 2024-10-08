> 本文适合Java入门和复习回顾，高级篇请参考导航：
> 
> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")
> 
> **本文最新版本：**
> 
> [【Java基础+进阶】Java修仙之路，十万字吐血整理全网最完整Java学习笔记（基础篇2024版）](https://blog.csdn.net/qq_40991313/article/details/134564921 "【Java基础+进阶】Java修仙之路，十万字吐血整理全网最完整Java学习笔记（基础篇2024版）")

**目录**

[一、JDK下载和hello world](#hello%20world)

[二、IDEA](#idea)

 [2.1 下载安装配置](#%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE)

[2.1.1 下载地址](#2.1.1%20%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80)

[2.1.2 配置](#2.1.2%20%E9%85%8D%E7%BD%AE)

[2.1.3 安装插件](#2.1.3%20%E5%AE%89%E8%A3%85%E6%8F%92%E4%BB%B6)

[2.1.4 操作](#2.1.4%20%E6%93%8D%E4%BD%9C)

[2.1.5 helloword](#2.1.5%20helloword%C2%A0) 

[2.2 快捷键](#%E5%BF%AB%E6%8D%B7%E9%94%AE)

[2.3 断点调试](#2.3%20%E8%B0%83%E8%AF%95) 

[2.3.1 断点](#2.3.1%20%E6%96%AD%E7%82%B9)

[2.3.2 调试](#2.3.2%20%E8%B0%83%E8%AF%95%C2%A0) 

[2.3.3 退帧](#2.3.3%20%E9%80%80%E5%B8%A7%C2%A0) 

[2.3.4 强制返回](#2.3.4%20%E5%BC%BA%E5%88%B6%E8%BF%94%E5%9B%9E)

[2.3.5 stream流调试](#2.3.5%20stream%E6%B5%81%E8%B0%83%E8%AF%95)

[2.3.6 评估表达式](#2.3.6%20%E8%AF%84%E4%BC%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F)

[2.3.7 多线程调试](#2.3.7%20%E5%A4%9A%E7%BA%BF%E7%A8%8B%E8%B0%83%E8%AF%95%C2%A0) 

[三、常用类](#%E7%B1%BB)

[3.1 Random](#Random)

[3.2 String](#String)

[3.2.1 概述](#3.2.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[3.2.2 与c++中string不同](#%E4%B8%8Ec%2B%2B%E4%B8%ADstring%E4%B8%8D%E5%90%8C)

[3.3 StringBuilder](#%C2%A0StringBuilder)

[3.4 ArrayList](#ArrayList)

[3.4.1 概述](#3.4.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[3.4.2 ArrayList学生管理系统](#ArrayList%E5%AD%A6%E7%94%9F%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F)

[3.5 Math](#Math)

[3.6 Object类](#Object)

[3.7 System](#System)

[3.8 Arrays](#Arrays)

[3.9 Integer](#Integer)

[3.10 Date类](#%C2%A0Date)

[3.11 SimpleDateformat](#SimpleDateformat)

[3.12 Scanner](#Scanner)

[四、基本数据类型](#%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)

[五、数组](#%E6%95%B0%E7%BB%84)

[六、方法](#%E6%96%B9%E6%B3%95)

[6.1 重载](#%E9%87%8D%E8%BD%BD)

[6.1.1 概念](#%E6%A6%82%E5%BF%B5)

[6.1.2 可变参数](#%E5%8F%AF%E5%8F%98%E5%8F%82%E6%95%B0)

[6.2 构造方法](#%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95)

[七、修饰符](#%E4%BF%AE%E9%A5%B0%E7%AC%A6)

[7.1 访问权限修饰符，public protected default private](#%E8%AE%BF%E9%97%AE%E6%9D%83%E9%99%90%E4%BF%AE%E9%A5%B0%E7%AC%A6) 

[private](#private)

[7.2 static](#static)

[7.3 abstract](#abstract)

[7.4 final](#final)

[八、关键字](#%C2%A0%E5%85%B3%E9%94%AE%E5%AD%97)

[8.1 this](#this)

[8.2 super](#super)

[九、面向对象](#%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1)

[9.1 类和对象](#%E7%B1%BB%E5%92%8C%E5%AF%B9%E8%B1%A1)

[9.1.1 概念](#9.1.1%20%E6%A6%82%E5%BF%B5%C2%A0) 

[9.1.2 内部类](#%E5%86%85%E9%83%A8%E7%B1%BB)

[9.2 封装](#%E5%B0%81%E8%A3%85)

[十、继承](#%E7%BB%A7%E6%89%BF)

[十一、多态](#%E5%A4%9A%E6%80%81)

[十二、接口](#%E6%8E%A5%E5%8F%A3)

[十三、异常](#%E5%BC%82%E5%B8%B8)

[13.1 Throwable](#Throwable)

[13.2 捕获异常](#%E6%8D%95%E8%8E%B7%E5%BC%82%E5%B8%B8)

[13.3 自定义异常](#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%BC%82%E5%B8%B8)

[十四、集合](#%E9%9B%86%E5%90%88)

[14.1 集合体系](#%E9%9B%86%E5%90%88%E4%BD%93%E7%B3%BB)

[14.2 HashMap和HashSet区别](#HashMap%E5%92%8CHashSet%E5%8C%BA%E5%88%AB)

[14.3 HashSet和TreeSet的区别](#articleContentId)

[14.4 ArrayList](#14.4%20ArrayList)

[14.5 ListIterator](#%C2%A0ListIterator)

[14.6 增强版for](#%E5%A2%9E%E5%BC%BA%E7%89%88for)

[14.7 LinkedList](#LinkedList)

[14.8 Hashset](#Hashset)

[14.9 LinkedHashSet](#LinkedHashSet)

[14.10 TreeSet](#TreeSet)

[14.11 泛型](#%E6%B3%9B%E5%9E%8B)

[14.11.1 概念](#14.11.1%20%E6%A6%82%E5%BF%B5)

[14.11.2 泛型类](#%E6%B3%9B%E5%9E%8B%E7%B1%BB)

[14.11.3 泛型方法](#%E6%B3%9B%E5%9E%8B%E6%96%B9%E6%B3%95)

[14.11.4 泛型接口](#%C2%A0%E6%B3%9B%E5%9E%8B%E6%8E%A5%E5%8F%A3)

[14.12 类型通配符](#%C2%A0%E7%B1%BB%E5%9E%8B%E9%80%9A%E9%85%8D%E7%AC%A6)

[14.13 可变参数](#14.13%20%E5%8F%AF%E5%8F%98%E5%8F%82%E6%95%B0)

[14.14 HashMap](#%C2%A0HashMap)

[14.15 Collections类](#Collections%E7%B1%BB)

[十五、i/o流](#i%2Fo%E6%B5%81)

[15.1 继承关系、路径斜杠](#%E7%BB%A7%E6%89%BF%E5%85%B3%E7%B3%BB%E3%80%81%E8%B7%AF%E5%BE%84%E6%96%9C%E6%9D%A0)

[15.2 io流分类](#io%E6%B5%81%E5%88%86%E7%B1%BB)

[15.3 File类](#File)

[15.4 字节输出流OutputStream](#%E5%AD%97%E8%8A%82%E8%BE%93%E5%87%BA%E6%B5%81OutputStream)

[15.5 字节输入流InputStream](#%E5%AD%97%E8%8A%82%E8%BE%93%E5%85%A5%E6%B5%81InputStream)

[15.6 文件输出流FileOutputStream](#%E5%AD%97%E8%8A%82%E8%BE%93%E5%87%BA%E6%B5%81)

[15.7 文件输入流 FileInputStream](#%E5%AD%97%E8%8A%82%E8%BE%93%E5%85%A5%E6%B5%81)

[15.7.1 概述](#15.7.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[15.7.2 练习，通过文件输入输出流复制图片](#%E5%A4%8D%E5%88%B6%E5%9B%BE%E7%89%87)

[15.8 字节缓冲流](#%E5%AD%97%E8%8A%82%E7%BC%93%E5%86%B2%E6%B5%81)

[15.8.1 字节缓冲输出流BufferedOutputStream](#BufferedOutputStream)

[15.8.2 字节缓冲输入流BufferedInputStream](#BufferedInputStream)

[15.9 字符流](#%E5%AD%97%E7%AC%A6%E6%B5%81)

[15.9.1 概要和继承关系](#%E6%A6%82%E8%A6%81%E5%92%8C%E7%BB%A7%E6%89%BF%E5%85%B3%E7%B3%BB)

[15.9.2 字符输出流OutputStreamWriter](#%C2%A0OutputStreamWriter)

[15.9.3 字符输入流InputStreamReader](#InputStreamReader)

[15.9.4 字符串的编码解码](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%BC%96%E7%A0%81%E8%A7%A3%E7%A0%81)

[15.9.5 字符流的编码解码](#%E5%AD%97%E7%AC%A6%E6%B5%81%E7%BC%96%E7%A0%81%E8%A7%A3%E7%A0%81)

[15.9.6 FileWriter和FileReader](#FileWriter%E5%92%8CFileReader)

[15.9.7 字符缓冲流BufferedWriter和BufferedReader](#%E5%AD%97%E7%AC%A6%E7%BC%93%E5%86%B2%E6%B5%81)

[15.9.8 练习，字符缓冲流文本复制](#%E5%AD%97%E7%AC%A6%E7%BC%93%E5%86%B2%E6%B5%81%E6%96%87%E6%9C%AC%E5%A4%8D%E5%88%B6)

[15.10 I/O流JDK7异常处理](#I%2FO%E6%B5%81JDK7%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86)

[15.11 特殊操作流](#%E7%89%B9%E6%AE%8A%E6%93%8D%E4%BD%9C%E6%B5%81%C2%A0) 

[15.11.1 标准输入输出流System.in和System.out](#%E6%A0%87%E5%87%86%E8%BE%93%E5%85%A5%E8%BE%93%E5%87%BA%E6%B5%81)

[15.11.2 字节打印流PrintStream](#%E5%AD%97%E8%8A%82%E6%89%93%E5%8D%B0%E6%B5%81PrintStream)

[15.11.3 字符打印流PrintWriter](#%E5%AD%97%E7%AC%A6%E6%89%93%E5%8D%B0%E6%B5%81)

[15.11.4 对象序列化流](#%E5%AF%B9%E8%B1%A1%E5%BA%8F%E5%88%97%E5%8C%96%E6%B5%81)

[15.11.5 对象反序列化流ObjectInputStream](#%E5%AF%B9%E8%B1%A1%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E6%B5%81ObjectInputStream)

[15.11.6 Properties和IO流结合](#%C2%A0Properties%E5%92%8CIO%E6%B5%81%E7%BB%93%E5%90%88)

[十六、多线程](#%E5%A4%9A%E7%BA%BF%E7%A8%8B)

[16.1 概念](#16.1%20%E6%A6%82%E5%BF%B5)

[16.2 创建线程方法1:继承Thread类](#%E9%80%9A%E8%BF%87%E7%BB%A7%E6%89%BFThread%E6%9D%A5%E5%88%9B%E5%BB%BA%E7%BA%BF%E7%A8%8B)

[16.3 创建线程方法2:实现 Runnable 接口](#%E9%80%9A%E8%BF%87%E5%AE%9E%E7%8E%B0%20Runnable%20%E6%8E%A5%E5%8F%A3%E6%9D%A5%E5%88%9B%E5%BB%BA%E7%BA%BF%E7%A8%8B)

[16.4 线程生命周期](#%E7%BA%BF%E7%A8%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

[16.5  线程同步](#%C2%A0%E7%BA%BF%E7%A8%8B%E5%90%8C%E6%AD%A5)

[16.5.1 同步代码块](#%E5%90%8C%E6%AD%A5%E4%BB%A3%E7%A0%81%E5%9D%97)

[16.5.2 同步方法](#%E5%90%8C%E6%AD%A5%E6%96%B9%E6%B3%95)

[16.5.3 线程安全的类](#%C2%A0%E7%BA%BF%E7%A8%8B%E5%AE%89%E5%85%A8%E7%9A%84%E7%B1%BB)

[16.5.4 Lock锁](#Lock%E9%94%81)

[16.6 生产者消费者模式](#%E7%94%9F%E4%BA%A7%E8%80%85%E6%B6%88%E8%B4%B9%E8%80%85%E6%A8%A1%E5%BC%8F)

[十七、 网络编程](#%C2%A0%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B)

[17.1 概念](#17.1%20%E6%A6%82%E5%BF%B5%C2%A0) 

[17.2 IP地址](#%C2%A0IP%E5%9C%B0%E5%9D%80)

[17.3 InetAddress 类](#InetAddress%20%E7%B1%BB)

[17.4 端口](#%E7%AB%AF%E5%8F%A3)

[17.5 UDP协议接收发送数据](#%C2%A0UDP%E5%8D%8F%E8%AE%AE%E6%8E%A5%E6%94%B6%E5%8F%91%E9%80%81%E6%95%B0%E6%8D%AE)

[17.6 TCP协议](#TCP%E5%8D%8F%E8%AE%AE)

[17.6.1 概念](#%C2%A0%E6%A6%82%E5%BF%B5)

[17.6.2 发送数据](#%E5%8F%91%E9%80%81%E6%95%B0%E6%8D%AE)

[17.6.3 接受数据](#%E6%8E%A5%E5%8F%97%E6%95%B0%E6%8D%AE)

[17.6.4 练习，TCP键盘录入字符通讯](#%C2%A0TCP%E9%94%AE%E7%9B%98%E5%BD%95%E5%85%A5%E5%AD%97%E7%AC%A6%E9%80%9A%E8%AE%AF)

[17.6.5 练习，服务器多线程接收文件](#%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%A4%9A%E7%BA%BF%E7%A8%8B%E6%8E%A5%E6%94%B6%E6%96%87%E4%BB%B6)

[十八、Lambda表达式](#Lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F)

[18.1 概念](#18.1%20%E6%A6%82%E5%BF%B5)

[18.2 实现类、匿名内部类、Lambda线程代码对比](#%E5%AE%9E%E7%8E%B0%E7%B1%BB%E3%80%81%E5%8C%BF%E5%90%8D%E5%86%85%E9%83%A8%E7%B1%BB%E3%80%81Lambda%E7%BA%BF%E7%A8%8B%E4%BB%A3%E7%A0%81%E5%AF%B9%E6%AF%94)

[18.3 Lambda和匿名内部类区别](#Lambda%E5%92%8C%E5%8C%BF%E5%90%8D%E5%86%85%E9%83%A8%E7%B1%BB%E5%8C%BA%E5%88%AB)

[十九、接口组成更新](#%E6%8E%A5%E5%8F%A3%E7%BB%84%E6%88%90%E6%9B%B4%E6%96%B0)

[19.1 接口中default默认方法](#%E6%8E%A5%E5%8F%A3%E4%B8%ADdefault%E9%BB%98%E8%AE%A4%E6%96%B9%E6%B3%95)

[19.2 接口中静态方法](#%E6%8E%A5%E5%8F%A3%E4%B8%AD%E9%9D%99%E6%80%81%E6%96%B9%E6%B3%95)

[19.3 接口中私有方法](#%E6%8E%A5%E5%8F%A3%E4%B8%AD%E7%A7%81%E6%9C%89%E6%96%B9%E6%B3%95)

[二十、方法引用](#%E6%96%B9%E6%B3%95%E5%BC%95%E7%94%A8)

[20.1 概念](#20.1%20%E6%A6%82%E5%BF%B5)

[20.2 引用类的方法](#%E5%BC%95%E7%94%A8%E7%B1%BB%E7%9A%84%E6%96%B9%E6%B3%95)

[20.3 引用对象](#%E5%BC%95%E7%94%A8%E5%AF%B9%E8%B1%A1)

[20.4 引用构造器](#%E5%BC%95%E7%94%A8%E6%9E%84%E9%80%A0%E5%99%A8)

[二十一、函数式接口](#%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3)

[21.1 概念](#21.1%20%E6%A6%82%E5%BF%B5%C2%A0) 

[21.2 函数式接口Supplier接口](#%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3Supplier%E6%8E%A5%E5%8F%A3)

[21.3 函数式接口Consumer](#%C2%A0%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3Consumer)

[21.4 函数式接口Predicate](#%C2%A0%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3Predicate)

[21.5 函数式接口Function](#%C2%A0%E5%87%BD%E6%95%B0%E5%BC%8F%E6%8E%A5%E5%8F%A3Function)

[二十二、Stream流](#%C2%A0Stream%E6%B5%81)

[22.1 Stream流生成：](#Stream%E6%B5%81%E7%94%9F%E6%88%90%EF%BC%9A)

[22.2 Stream流中间操作](#%C2%A0Stream%E6%B5%81%E4%B8%AD%E9%97%B4%E6%93%8D%E4%BD%9C)

[22.2.1 概述](#22.2.1%20%E6%A6%82%E8%BF%B0%C2%A0) 

[22.2.2 map和filter区分](#map%E5%92%8Cfilter%E5%8C%BA%E5%88%86)

[22.3 Stream流终结](#Stream%E6%B5%81%E7%BB%88%E7%BB%93)

[22.4 Stream流收集](#Stream%E6%B5%81%E6%94%B6%E9%9B%86)

[二十三、 反射](#%C2%A0%E5%8F%8D%E5%B0%84)

[23.1 类加载和类加载器](#%E7%B1%BB%E5%8A%A0%E8%BD%BD%C2%A0) 

[23.2 反射概述](#%E5%8F%8D%E5%B0%84%E6%A6%82%E8%BF%B0%C2%A0) 

[23.3 三种获取Class类的对象方法](#%E8%8E%B7%E5%8F%96Class%E7%B1%BB%E7%9A%84%E5%AF%B9%E8%B1%A1)

[23.4 反射获取构造方法并实例化](#%E5%8F%8D%E5%B0%84%E8%8E%B7%E5%8F%96%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95%E5%B9%B6%E5%AE%9E%E4%BE%8B%E5%8C%96)

[23.5 反射获取成员变量并赋值](#%E5%8F%8D%E5%B0%84%E8%8E%B7%E5%8F%96%E6%88%90%E5%91%98%E5%8F%98%E9%87%8F%E5%B9%B6%E8%B5%8B%E5%80%BC)

[23.6 获取成员方法对象并调用成员方法](#%E8%8E%B7%E5%8F%96%E6%88%90%E5%91%98%E6%96%B9%E6%B3%95%E5%AF%B9%E8%B1%A1%E5%B9%B6%E8%B0%83%E7%94%A8%E6%88%90%E5%91%98%E6%96%B9%E6%B3%95)

[23.7 Properties和反射结合](#Properties%E5%92%8C%E5%8F%8D%E5%B0%84%E7%BB%93%E5%90%88)

[二十四、模块化](#%E6%A8%A1%E5%9D%97%E5%8C%96)

[24.1 不同模块间访问类：](#%E4%B8%8D%E5%90%8C%E6%A8%A1%E5%9D%97%E9%97%B4%E8%AE%BF%E9%97%AE%E7%B1%BB%EF%BC%9A)

[24.2 模块服务](#%E6%A8%A1%E5%9D%97%E6%9C%8D%E5%8A%A1%C2%A0) 

[二十五、XML](#XML)

[25.1 概念](#25.1%20%E6%A6%82%E5%BF%B5)

[25.2 语法规则](#%E8%AF%AD%E6%B3%95%E8%A7%84%E5%88%99)

[25.3 文档约束](#%C2%A0%E6%96%87%E6%A1%A3%E7%BA%A6%E6%9D%9F)

--

## 一、JDK下载和hello world

先下载jdk8或11，这个版本最稳定，下面是jdk8的下载链接：[Java Downloads | Oracle](https://www.oracle.com/java/technologies/downloads/#java8-windows "Java Downloads | Oracle")

进入后选择windows64版本exe下载，安装后记得配置环境变量：

此电脑右键-属性-高级系统设置-环境变量： 

![](https://i-blog.csdnimg.cn/blog_migrate/bff1406c3746741bdbc06634f50c7261.png)

![](https://i-blog.csdnimg.cn/blog_migrate/154a2d9d732b73ffb8d8871703e37ed6.png)

```
public class hello{
    public static void main(String[] args){
        System.out.println("fe");
    }
}
```

![](https://i-blog.csdnimg.cn/blog_migrate/de420a55aa4f96d53bc86527fcaacb0c.png)

## 二、IDEA

###  2.1 下载安装配置

#### **2.1.1 下载地址**

[Other Versions - IntelliJ IDEA](https://www.jetbrains.com/idea/download/other.html "Other Versions - IntelliJ IDEA")

**建议安装专业版**， 右侧有数据库栏，写sql语句代码补全方便：

![](https://i-blog.csdnimg.cn/blog_migrate/c42ce015d89fbe933bdd75777cc3a2e1.png)

> **注意：所有设置都必须要关闭项目后，再进行设置，这样才是全局设置。**

#### **2.1.2 配置**

> **先关闭项目再点击设置**

**编码** 

![](https://i-blog.csdnimg.cn/blog_migrate/e1199bb70ccec48a77349abbd2a3bbc7.png)

maven，后面javaweb里用到 

![](https://i-blog.csdnimg.cn/blog_migrate/37063bcf5a24c6584ae64bce90ad8323.png) **maven配置依赖和插件后自动刷新**

![](https://i-blog.csdnimg.cn/blog_migrate/ff1daeca5c051e2ac6db459adae2a771.png)

#### **2.1.3 安装插件**

-   **Chinese(Simplified) Language Pack/中文语言包：**汉化idea
-   **Maven helper：**右键Maven模块，会出现打包，编译等选择。
-   **MybatisX：**mapper.xml,mapper.java出现小鸟图标，接口定义方法，自动在xml中生成statement语句。
-   **Alibaba Java Coding Guidelines：**阿里规约

#### 2.1.4 操作

**查看本地历史记录：**

idea是会自动保存各文件历史记录的，右键文件-查看本地历史记录即可：

![](https://i-blog.csdnimg.cn/blog_migrate/72b755fe731673292877a8a6d73f8cc1.png)

![](https://i-blog.csdnimg.cn/blog_migrate/6417e7821ab0b0cb3f14e4821ef556dc.png)

#### **2.1.5 helloword** 

 先创建项目（file-new-project-empty project-起名-finish，SDK开发工具包选JDK11，语言级别也选11）、模块（项目右键-new-module-java-next-起名，SDK开发工具包选JDK11，语言级别也选11）、包（模块下src右键-new-package-起名-ok）、类（包右键new-java class）。

然后psvm回车自动生成静态main方法，sout回车自动生成System.out.println()输出方法。

在当前包内IO流File类创建文件，例如"1.txt"，存的位置是在项目文件夹下，而不是包文件夹下。不确定可查看当前路径：

```java
System.out.println(System.getProperty("user.dir"));
```

 控制台中文乱码，就在设置里把文件编码页都改成utf-8。

导包：import 包名.类名;

![](https://i-blog.csdnimg.cn/blog_migrate/5dd1ebe0f46c2b4b7e99402033abe6af.png)

![](https://i-blog.csdnimg.cn/blog_migrate/8360c9afc7c589d1631e94d3db288336.png)

![](https://i-blog.csdnimg.cn/blog_migrate/eb8fba04decfaa5a841ea5f4d53f9e52.png)

### **2.2 快捷键**

**格式化ctrl+alt+L，**main方法psvm回车，输出sout回车，内容提示ctrl+alt+space。alt+insert生成构造、setget方法。

**Ctrl+Alt+v或.var或.for补全代码：**例如写new Dog();按快捷键会自动补全声明Dog dog=new Dog();或者写new Dog().var回车会自动补全成Dog dog=new Dog();或者写lists.for回车会自动生成for(List<String> list:lists){}

**alt+enter:万能快捷键**。获取警告、报错提示自动改正

**ctrl+r：**替换所有与选中内容相同的文本，出现

**ctrl+b跟进：**或者ctrl+鼠标左键、或者鼠标左键，跟进到该类的定义页面。如果选中的是标识符，可以查找页面内所有该标识符位置。

**alt+左键：整列编辑**

**ctrl+d：复制光标行并粘贴**

**ctrl+x：删除光标行**

**Ctrl+h：查看该类继承关系：**

**ctrl+alt+m：抽取选中代码为方法**

![](https://i-blog.csdnimg.cn/blog_migrate/58415cced51e56b1231dea908c682b42.png)

 **Ctrl+f12：查看类中所有方法。**

![](https://i-blog.csdnimg.cn/blog_migrate/7202cce8d609ab21eeb8782f176f25c3.png)

### 2.3 断点调试 

#### 2.3.1 断点

普通断点：如果断点打在普通代码行上，点击“debug”会自动运行到该行暂停；

方法断点：如果断点打在方法上，点击“debug”会自动运行到该方法入口处暂停；

接口断点：如果断点打在接口方法，点击“debug”会自动运行到实现类对应方法入口处暂停；

字段断点：如果断点打在字段上，点击“debug”会自动运行到修改此字段的代码行处暂停（可以在断点处右键设置成访问时也暂停）；

#### 2.3.2 调试 

打断点后代码运行到这一步会停止：下面红色方框是最常用的两个调试按钮：

![](https://i-blog.csdnimg.cn/blog_migrate/047ad455c438b74dba15962ddaca5bd5.png)

> 蓝色代码行代表此时调试运行到这一行（这一行还没运行），能看到上一行的结果。

> 调试的五个核心图标分别是：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/16f2ea0887185c0c6f3d287974ff2f6f.png)
> 
> 1.  **“Step over”：步过。**往下运行一行代码并**跳过**当前方法的调用。
> 2.  **“Step into”：步入。**进入方法内部并继续逐行执行。适用于自定义方法或第三方方法，但无法进入JDK方法的内部。注意如果蓝色光标行不是方法，则此按钮相当于step over。
> 3.  **“Force step into”：强制步入（不常用）。**强制进入方法的内部，即使常规的"Step into"操作无法进入方法内部时也可以使用。适用于**无法通过常规方式进入的方法**。例如Symtem.out.println()等JDK方法内部。
> 4.  **“Step out”：步出。**退出当前方法，即执行完当前方法后返回到调用该方法的位置。注意如果本方法是main方法，则将**直接步出这个main方法**。
> 5.  **“Resume Program”：运行到光标处。**继续运行程序直到下一个断点位置或程序结束。可用于暂停状态下的程序恢复运行。

#### 2.3.3 退帧 

 **退帧：**回退到此方法被调用之前。

当我们 Debug 从 A 方法进入 B 方法时，通过降帧（退帧）可以返回到调用 B 方法前，这样我们就可以再一次调用 B 方法。

通常用于当我们快执行完 B 方法后，发现某个重要流程被我们跳过了，想再看一下，则此时可以先回退到 A 方法，然后再次进入 B 方法。

![](https://i-blog.csdnimg.cn/blog_migrate/37627752c14dc0d5f6a97cbd2373a407.png)​​

#### 2.3.4 强制返回

 右键并点击“force return” 后，此方法栈将直接终止，恢复到上个方法栈。

使用场景：需要结束当前断点，并且不希望接下来的程序操作数据库时，使用强制返回。

> **注意：**注意如果点击红色方格![](https://i-blog.csdnimg.cn/blog_migrate/57f38d19d75482afc19b2513acf0b281.png)或重新调试![](https://i-blog.csdnimg.cn/blog_migrate/9ff4b43d13a9dbdb0a10d1dbd2a71d34.png)虽然也是终止，但它其实是运行完剩余代码后再终止。
> 
> -   强制返回：接下来的程序将不再继续执行。
> -   终止：接下来的程序将走完，然后再终止程序。

![](https://i-blog.csdnimg.cn/blog_migrate/8b1c0addf2618d2c95653ad845ba9d34.png)​​

#### 2.3.5 stream流调试

在stream流处打断点，debug后点击“trace current stream chain”：

![](https://i-blog.csdnimg.cn/blog_migrate/b80a0ce6b63bf6b25386a55e50050afe.png)

就可以看到整个流式处理的过程：

![](https://i-blog.csdnimg.cn/blog_migrate/ffba23580b22414db6a1e6ba1b3e7939.png)

#### 2.3.6 评估表达式

在if处打断点，debug后点击“evaluate expression”，可以在评估框下测试另一个分支：

![](https://i-blog.csdnimg.cn/blog_migrate/83db83b28835744cbfb60170475ff9cd.png)

#### 2.3.7 多线程调试 

多线程环境，打断点并右键设置Thread或All：

-   **Thread：**暂停进入断点的线程，不影响其他线程执行。所有线程依次debug（即你如果给多个线程都加断点，第一个线程debug期间其他线程将保持断点暂停状态）
-   **ALL：**暂停全部线程。只debug第一个暂停线程（即你如果给多个线程都加断点，那么只第一个断点对应的线程会正常debug，其他线程会并发运行）

![](https://i-blog.csdnimg.cn/blog_migrate/7575c47e393bc3a2965b5f120b57430b.png)

## 三、常用类

### 3.1 Random

```java
import java.util.Random;
public class hello{
	public static void main(String[] args){
		Random r=new Random();
// 生成 0 到 10（不包括10）之间的随机整数
		int num=r.nextInt(10);
		System.out.println(num);
	}
}
```

### 3.2 String

#### 3.2.1 概述 

字符串不可变，创建后不可更改。

效果相当于字符数组，底层是字节数组。

```java
//构造
String s1 = "Runoob";              // String 直接创建
String s2 = new String("Runoob");   // String 对象创建
String s3 = s1;                    // 相同引用

int len = s1.length();    //长度


//访问字符
//访问要s1.charAt(0),不能s1[0];

//格式化
String s=String.format("%d",2);
System.out.println(s);


//拼接字符串、数字、字符
s1="我的名字是 ".concat("Runoob");
s2+="abc";
s2+=123;        //字符串+数字，数字会转成字符串
s2+='c';

//根据指定字符串分割
s="1,2,3";
String arr[]=s.split(",");

//字符串翻转要自己写

//数字转String
String s=String.valueOf(12);

//String转数字
int c=Integer.parseInt(s);

//String转Integer转数字
int c=Integer.valueOf(s).intValue();
```

比较

```java
//比较地址
//只要new，就在堆内存开辟空间。直接赋值字符串在常量池里。
        String str1 = "hello";        //常量池里无“hello”对象，创建“hello”对象，str1指向常量池“hello”对象。
//先检查字符串常量池中有没有"hello"，如果字符串常量池中没有，则创建一个，然后 str1 指向字符串常量池中的对象，如果有，则直接将 str1 指向"hello"；
        String str2 = "hello";    //常量池里有“hello”对象，str2直接指向常量池“hello”对象。
        String str3 = new String("hello");   //堆中new创建了一个对象。假如“hello”在常量池中不存在，Jvm还会常量池中创建这个对象“hello”。
        String str4 = new String("hello");
        System.out.println(str1==str2);//true，因为str1和str2指向的是常量池中的同一个内存地址
        System.out.println(str1==str3);//fasle，str1常量池旧地址，str3是new出的新对象，指向一个全新的地址
        System.out.println(str4==str3);//fasle，因为它们引用不同
 
//比较内容
        System.out.println(str4.equals(str3));//true，因为String类的equals方法重写过，比较的是字符串值
```

#### 3.2.2 与c++中string不同

java中字符串：一个汉字长度是1，c++中字符串，一个汉字长度是2.

还有很多不同，不能弄混。

### 3.3 StringBuilder

String拼接字符串后原字符串还存在于内存中，浪费内存。

StringBuffer 类的对象能够被多次的修改，并且不产生新的未使用对象，所以涉及到字符串拼接，优先用StringBuffer 。

```java
//构造
        StringBuilder sb= new StringBuilder("abc");

//String转StringBuilder
        sb.append("d").append("e").append("f");

//StringBuilder转String
        String s=sb.toString();

//反转
        sb.reverse();

```

### 3.4 ArrayList

#### 3.4.1 概述 

可以动态修改的数组，没有固定大小的限制。

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites);        //[Google, Runoob, Taobao, Weibo]
        System.out.println(sites.get(1));  // 访问第二个元素Runoob
        sites.set(2, "Wiki"); // 第一个参数为索引位置，第二个为要修改的值
        sites.remove(3); // 删除第四个元素
        System.out.println(sites.size());//计算大小

    }
}
```

#### 3.4.2 ArrayList学生管理系统

要点：直接退出程序System.exit(0);修改学生时没查成功提示失败，成功提示成功,方法是静态。查找id时查到break；id如果是int型，之后要用(char)System.in.read()接收空格或回车.

可优化：学号不存在和学号重复，加入地址、成绩、年龄等其他信息，查询制表。

```java
//StudentManager.java
package package_test;

import java.util.Scanner;
import java.util.ArrayList;

public class StudentManager {
    public static void main(String args[]) {
        Scanner sc=new Scanner(System.in);
        ArrayList<Student> al = new ArrayList<>();
        while (true) {
            System.out.println("1增加学生，2删除学生，3修改学生，4查询学生，5退出系统");

            int choose = sc.nextInt();
            switch (choose) {
                case 1:
                    add(al);
                    break;
                case 2:
                    delete(al);
                    break;
                case 3:
                    update(al);
                    break;
                case 4:
                    search(al);
                    break;
                default:
                    System.exit(0);
            }
        }
    }

    public static void add(ArrayList<Student> al) {      //必须是静态方法，否则报错
        System.out.println("input id:");
        Scanner sc = new Scanner(System.in);
        Student child = new Student();
        String id = sc.nextLine();
        child.setId(id);
        System.out.println("input name: ");
        String name = sc.nextLine();
        child.setName(name);
        al.add(child);
    }

    public static void search(ArrayList<Student> al) {
        if (al.size() == 0) System.out.println("no information");
        Scanner sc = new Scanner(System.in);
        for (int i = 0; i < al.size(); i++) System.out.println(al.get(i).getId() + " " + al.get(i).getName());
    }

    public static void update(ArrayList<Student> al) {
        System.out.println("input id");
        Scanner sc = new Scanner(System.in);
        Student child = new Student();
        child.setId(sc.nextLine());
        System.out.println("Please enter the modified name");
        child.setName(sc.nextLine());
        int find = 0;
        for (int i = 0; i < al.size(); i++) {
            if (al.get(i).getId().equals(child.getId())) {
                find = 1;
                al.set(i, child);
                break;
            }
        }
        if (find == 0) {
            System.out.println("not found");
        } else {
            System.out.println("successful");
        }
        search(al);
    }

    public static void delete(ArrayList<Student> al) {
        System.out.println("input id");
        Scanner sc = new Scanner(System.in);
        String ipt = sc.nextLine();
        for (int i = 0; i < al.size(); i++) {
            if (al.get(i).getId().equals(ipt)) {
                System.out.println("successful");
                al.remove(i);
                return;

            }
        }
        System.out.println("not exsit");
        search(al);
    }
}
```

```java
//Student.java
package package_test;

public class Student {
    private String id;
    private String name;

    public Student(String id, String name) {
        this.name = name;
        this.id = id;
    }

    public Student() {

    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

### 3.5 Math

![](https://i-blog.csdnimg.cn/blog_migrate/72a788b643aa33c76e57601790e02743.png)

### 3.6 Object类

所有类都间接或直接继承自该类。

自动重写toString()和equlas()：在类中ctrl+insert。不重写默认比较地址。

```java
    public boolean equals(Object o) {
        if (this == o) return true;        //地址相同直接true
        if (o == null || getClass() != o.getClass()) return false;    //是否空或者不来自于同一个类

        Dog dog = (Dog) o;

        return weight == dog.weight;
    }

    @Override
    public int hashCode() {
        return weight;
    }

    @Override
    public String toString() {
        return "Dog{" +
                "weight=" + weight +
                '}';
    }
```

### 3.7 System

System类不能被实例化，要通过类名调用方法。

![](https://i-blog.csdnimg.cn/blog_migrate/0deb718b3187fe950ff95d7865ad91df.png)

 **练习：**获取for循环十万次的运行时长。

```java
public class Test {
    public static void main(String[] args) {
        long start=System.currentTimeMillis();
        for(int i=0;i<100000;i++){}
        long end=System.currentTimeMillis();
        System.out.println("for循环十万次的运行时长:"+(end-start)+"毫秒");
    }
}
```

结果：

![](https://i-blog.csdnimg.cn/blog_migrate/89bd0f15f5c6f3f1189261c4200ecffd.png)

### 3.8 Arrays

![](https://i-blog.csdnimg.cn/blog_migrate/6094150b5aab286b461ac29e27efa788.png)

### 3.9 Integer

java.lang包下。

基本数据类型封装成对象好处是：可以有更多的方法操作改数据。

```java
//装箱：基本数据类型转为包装类
        Integer a=Integer.valueOf(32);
        Integer a2=32;

//拆箱：包装类转为基本数据类型
        int b=a.intValue();

//数字转String
String s=String.valueOf(12);

//String转数字
int c=Integer.parseInt(s);

//String转Integer转数字
int c=Integer.valueOf(s).intValue();
```

### 3.10 Date类

getTime() 获取从1970年1月1日 0时0分0秒到此刻毫秒值

setTime() 自定义设置毫秒值

after()  
判断某个日期是否在指定日期之后

before()  
判断某个日期是否在指定日期之前

a.compareTo(b)  
对两个日期进行比较  
如果a时间在b之后，则返回1  
如果a时间在b之前，则返回-1  
如果a==b，则返回0

```java
        Date date=new Date();
        date.setTime(234);
        System.out.println(date.getTime());    //输出234
```

### 3.11 SimpleDateformat

为了格式化输出日期。

```java
    public static void main(String[] args) throws ParseException {    //throws只是把异常抛出，延迟处理。用trycatch处理比较好
        //Date转String
        Date d=new Date();
        SimpleDateFormat sdf=new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        String str=sdf.format(d);
        System.out.println(str);
        //String转Date
        d=sdf.parse(str);
        System.out.println(d);
    }
```

### 3.12 Scanner

```java
import java.util.Scanner;
public class hello{
	public static void main(String[] args){
		Scanner sc=new Scanner(System.in);
		int i=sc.nextInt();        //nextLine()是带空格的一行字符串
		System.out.println(i);
	}
}

next() 不能得到带有空格的字符串，nextLine()可以。
//注意：nextInt接下来nextLine，字符串会直接读取输入的数字之后的空格、回车，例如输入23回车，结果a的值是回车。
//int b=sc.nextInt();String a=sc.nextLine();
```

## 四、基本数据类型

java的八大基本数据类型分别是：

-   1、整型的byte、short、int、long；
-   2、字符型的char；
-   3、浮点型的float、double；
-   4、布尔型的boolean。 

## 五、数组

```java
//定义数组
int []a;
int b[];
int[][] x,y;//x和y都是二维数组
int[] z,t[];//z是一维数组，t是二维数组

//初始化，栈内存存储局部变量，使用后立即消失。new申请堆内存空间，使用后会在垃圾回收期空闲时回收
int d[]=new int[3];//动态初始化
int c[]={1,2,3};//或int c[]=new int[]{1,2,3};静态初始化

//直接输出数组会输出地址
System.out.println(a);    //[I@5b444398
//数组转字符串
System.out.println(Arrays.toString(c));    //[1, 2, 3]

//多数组指向相同堆内存，改动e内容后，c内容也会改变
int e[]=c;
```

## 六、方法

### 6.1 重载

#### 6.1.1 概念

重载（Overload）：指**一个类中**可以有多个方法具有**相同的方法名**，但这些方法的**参数类型不同、个数不同、顺序不同**。

> **注意：**方法返回值和[访问修饰符](https://so.csdn.net/so/search?q=%E8%AE%BF%E9%97%AE%E4%BF%AE%E9%A5%B0%E7%AC%A6&spm=1001.2101.3001.7020 "访问修饰符")可以不同。

示例： 

```java
public class hello {
    public static void main(String args[]) {
        f();

    }

    public static void f() {

        System.out.println("3f");
    }

    public static void f(int a) {        //重载，注意返回值同，参数不同

        System.out.println(a);
    }
//    下面两个注释的方法就不是重载，会报错
//    public static int f(){    //返回值不同
//        System.out.println("hello");
//    }
//    void f(){    //修饰符不同
//        return 666;
//    }
}
```

#### 6.1.2 可变参数

(int... a)是将所有int参数封装到a数组里。

![](https://i-blog.csdnimg.cn/blog_migrate/fde10d6ba02b80112b843c9552908ccc.png)

 注意可变参数要放在后面。例如(int a,int... b)正确，(int... a,int b)会报错。

### 6.2 构造方法

```java
public class Phone {

    public Phone() {
        System.out.println("hhh");//创建对象时会直接运行构造方法
    }
}
```

## 七、修饰符

### 7.1 访问权限修饰符，**public** **protected** **default** **private** 

-   **public** : 对所有类可见。使用对象：类、接口、变量、方法
    
-   **protected** : 对同包可见、对不同包子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。
    
-   **default** : 同包可见。使用对象：类、接口、变量、方法。
    
-   **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**
    

<table><caption id="accesscontrol-levels"></caption><tbody><tr><th>修饰符</th><th>当前类</th><th>同一包内</th><th>子孙类(同一包)</th><th>子孙类(不同包)</th><th>其他包</th></tr><tr><td><code>public</code></td><td>Y</td><td>Y</td><td>Y</td><td>Y</td><td>Y</td></tr><tr><td><code>protected</code></td><td>Y</td><td>Y</td><td>Y</td><td>Y/N（<a href="https://www.runoob.com/java/java-modifier-types.html#protected-desc" rel="nofollow" title="说明">说明</a>）</td><td>N</td></tr><tr><td><code>default</code></td><td>Y</td><td>Y</td><td>Y</td><td>N</td><td>N</td></tr><tr><td><code>private</code></td><td>Y</td><td>N</td><td>N</td><td>N</td><td>N</td></tr></tbody></table>

#### private

 在同一类内可见，保护成员不被别的类使用。可以修饰变量、方法。 **注意：不能修饰类（外部类）**

![](https://i-blog.csdnimg.cn/blog_migrate/a5c6f01bfc95e155d7c7eebc191bc1fc.png)

```java
public class Phone {
    int price;//成员变量在堆内存
    private int age;

    public void setAge(int a) {
        age = a;
    }
//或者用this
//    public void setAge(int age) {
//        this.age = age;
//    }

    public int getAge() {
        return age;
    }
}


//使用
public class hello {
    public static void main(String args[]) {
        Phone p = new Phone();
        p.setAge(12);
        System.out.println(p.getAge());

    }

}
```

### 7.2 static

静态成员变量被所有对象共享，可用类名调用。局部变量不能被声明为 static 变量。

```java
public class Phone {
    static int price;//成员变量在堆内存
}


//使用
public class hello {
    public static void main(String args[]) {
        Phone.price=4;
        //fun();会报错，静态方法只能访问静态方法或变量。
    }
    public fun(){};
}
```

静态方法只能访问静态变量和方法。非静态方法都可以访问。

静态方法中不能使用 this 关键字，因为在静态方法的局部变量表中并不存在this变量。

### 7.3 abstract

-   **一个类不能同时被 abstract 和 final 修饰**，抽象类的唯一目的是为了将来对该类进行**_扩充_**。
-   **抽象类可以包括抽象方法和非抽象方法，抽象方法只能存在于抽象类中。**
-   非抽象子类必须重写抽象父类中的**所有抽象方法**，抽象子类可以直接继承。

```java
public abstract class Animal{
    abstract void m(); //抽象方法
abstract void n(); //抽象方法
}
 
class Dog extends Animal{    //非抽象子类
     //实现父类所有抽象方法
      void m(){
          .........
      }
      void n(){
          .........
      }
}


abstract class Cat extends Animal{}//抽象子类，不需要重写父抽象类的抽象方法
```

### 7.4 final

-   final 变量必须显式指定初始值，不能被重新赋值（非final成员变量都会自动有默认值）。
-   final方法不能被子类重写。
-   final类不能被继承。
-   final引用不能变地址值，可以变地址内容。如final M m=new M();m.age=12;是正确，引用m始终指向对象M的内存地址。

## 八、关键字

### 8.1 this

①**指代当前类中的成员变量、方法**。可以用于方法的形参与成员变量同名时进行区分，

```java
public class Phone {
    private int age;

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}
```

### 8.2 super

指代父类的成员变量、方法。

看懂下面代码基本就能区分this和super

```java
public class Animal { 
    public String name;   
    int age=3; 
    public void eat() {  //吃东西方法的具体实现  } 
    public void sleep() { //睡觉方法的具体实现  } 
} 
//子类 
public class Penguin  extends  Animal{ 
    int age=4;
    public void show(){
        int age=5;
         System.out.println(age);   //5,子类可以访问父类非私有成员变量
        System.out.println(this.age);//4
        System.out.println(super.age);//3
    }
}
```

## 九、面向对象

### 9.1 类和对象

#### 9.1.1 概念 

![](https://i-blog.csdnimg.cn/blog_migrate/ea8766841bfb392d9a74beb87212d528.png)

```java
//定义类
public class Phone {
    int price;//对象在堆内存，成员变量便也在堆内存，创建对象时有初始值。

    public void fun() {
        int tmp;//局部变量在栈内存，不赋值就用会报错
        System.out.println("phone");
    }
}
```

```java

//创建对象，建议先写new Phone()然后ctrl+alt+v补全声明
Phone p=new Phone();
```

局部变量必须赋初值，不然会报错。

#### 9.1.2 内部类

**内部类：**在一个类中定义类。分为**成员内部类（成员位置），局部内部类（成员方法内），匿名内部类（方法内）。**

**匿名内部类**：一个**继承**了其他类**或者实现**了其他接口的子类对象。

> 内部类可以直接访问外部类私有、公有成员。外部类要访问内部类成员要创建对象。

```java
public class Outer {
    int num=10;
//定义成员内部类：在成员位置定义类
    public class Inner{        //一般private，用外部类访问内部类更安全
        public void show(){
            System.out.println("innershow"+num);    //内部类可直接访问外部类成员。
        }
    }

//外部类访问成员内部类
    public void fun(){        
        Inner in=new Inner();
        in.show();
    }

//局部内部类：在成员方法内定义类
    public void fun2(){
        class Inner2{        //成员内部类不能public和private
            void show(){
                System.out.println("成员内部类");
            }
        }
        Inner2 in=new Inner2();
        in.show();
    }

//匿名内部类：在成员方法内定义子类，实现接口或继承抽象类
    public void fun3(){
        Phone p=new Phone() {            //自己写的Phone接口
            @Override
            public void show() {
                System.out.println("实现接口的匿名内部类");
            }
        };            //注意是一个语句有分号
        p.show();
    }
}


//内部类创建对象（一般内部类私有，使用外部类访问内部类）
public class Test {
    public static void main(String[] args) {
    Outer.Inner i=new Outer().new Inner();
    i.show();
    }
}
```

### 9.2 封装

将类的某些信息隐藏在类的内部，不允许外部程序直接访问。

```java
public class Phone {
    int price;//成员变量在堆内存
    private int age;

    public void setAge(int age) {
       this.age = age;
    }

    public int getAge() {
        return age;
    }
}
```

**好处：**安全性和复用性。

![](https://i-blog.csdnimg.cn/blog_migrate/3b7c2ea9b565faaf1c7fce44ca5f4e1b.png)

## 十、继承

-   **优点：**提高代码复用性，维护性。**缺点：**高耦合性，父类改变子类也会改变。
    
-   **特点：**子类拥有父类非 private 的属性、方法。可以拥有自己的属性和方法，即子类可以对父类进行扩展。可以用自己的方式实现父类的方法。
    
-   **注意：** Java 不支持多继承，但支持多重继承。
    

> 单继承是子类只能继承一个父类。相对于实现是一个子类可以

-   子类所有构造方法会默认先运行super();
    

```java
public class Animal { 
    public String name;   
    int age=3; 
    public Animal(String name, int age) { 
        //初始化属性值
    } 
    public void show() {  //吃东西方法的具体实现  } 
    public void sleep() { //睡觉方法的具体实现  } 
} 
//子类 
public class Penguin  extends  Animal{ 
    int age=4;
    public Penguin(){
        super();    //不写也会默认运行
}
@Override        //注解重写，检查重写是否正确。例如修饰符（子类重写方法的访问权限要≥父类）、函数名错误。
    public void show(){    //重写父类中show(),如果去掉public会报错。想再用super.show();
        int age=5;
         System.out.println(age);   //5,子类可以访问父类非私有成员变量
        System.out.println(this.age);//4
        System.out.println(super.age);//3
    }
}
```

使用 implements 关键字可以变相的使java具有多继承的特性

```java
public interface A {
    public void eat();
    public void sleep();
}
 
public interface B {
    public void show();
}
 
public class C implements A,B {
}
```

## 十一、多态

 **接口引用指向实现类对象**

多态最常用的是接口引用指向实现类对象，这样当之后程序需要更新时候，只需要修改new后面的实现类即可，左边就不用修改了，从而降低耦合。

在Spring框架中，甚至可以通过配置或注解连实例化的new也不用了，从而更高层次的降低耦合。

**示例：**

```java
List<String> a=new ArrayList<String>();
```

这样写的话，等号右边换成_Vector 或 LinkedList_ 时，就可以很少修改代码量，降低耦合。

**向上转型：**

向上转型：父类引用指向子类对象。编译看左边（调用子类特有变量、方法会报错），运行看右边（优先运行子类重写后的方法）。

```java
Animal a=new Cat();
```

**向下转型：** 

向下转型：子类引用指向父类对象。编译看右边，运行看右边。

```java
    public static void main(String[] args) {
                
      Animal a = new Cat();  // 向上转型  
      a.eat();               // 调用的是 Cat 的 eat
      Cat c = (Cat)a;        // 向下转型  
      c.work();        // 调用的是 Cat 的 work
  } 
```

## 十二、接口

抽象类是对事物的抽象，如动物类，小狗类，接口是对行为的抽象，如吃饭类、睡觉类。

![](https://i-blog.csdnimg.cn/blog_migrate/44cc1fec1850bf4b31ed2c5612762f19.png)

除非实现接口的类是抽象类，否则该类要定义接口中的所有方法。

-   接口没有构造方法。
-   接口中的方法会被隐式的指定为 **public abstract方法，不能定义静态方法**。
-    接口中的变量会被隐式的指定为 **public static final** 变量，不能定义私有成员。因为是final所以也要显式赋初值。
-   接口和接口多继承，接口和类多实现。

```java
public interface Phone {
     public static final int price=4;    //修饰符可省略
     public abstract void show();        //修饰符可省略
}


public class PhoneImpl implements Phone{
    public void show(){        //必须是public，否则报错
        System.out.println("hello");
    }
}
```

## 十三、异常

### 13.1 Throwable

Throwable是所有异常的父类。

![](https://i-blog.csdnimg.cn/blog_migrate/2af2392e506f1d1fa5013ebbcdcbdb47.png)

**导图：** 

![](https://i-blog.csdnimg.cn/blog_migrate/fdc6803c1b289191f164e6910c8ac46d.png)

> **异常继承体系 ：**
> 
> ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/8bbc8b6f54907cf252fbcb90aab40bd8.png#pic_center)

RuntimeException是运行时异常，例如ArrayIndexOutOfBoundsException，编译不出错，运行出错，要try-catch处理。

非RuntimeException是编译时异常，throws可以抛出异常，使编译通过，运行时还会出错，要try-catch处理。

下面的列表是 Throwable 类的主要方法:

| **序号** | **方法及说明** |
| --- | --- |
| 1 | **public String getMessage()**  
返回关于发生的异常的详细信息。这个消息在Throwable 类的构造函数中初始化了。 |
| 2 | **public String toString()**  
返回此 Throwable 的简短描述。 |
| 3 | **public void printStackTrace()**  
将此 Throwable 及其回溯打印到标准错误流。。 |

程序运行出错，JVM会将异常的名称、原因、位置输出到控制台，并让程序停止运行。

### 13.2 捕获异常

throws只是抛出异常，并没有对异常进行实际处理，要用try-catch处理异常。

使用 try 和 catch 关键字可以捕获异常。try/catch 代码块放在异常可能发生的地方。

try/catch代码块中的代码称为保护代码，使用 try/catch 的语法如下：

```java
try
{
   // 程序代码
}catch(ExceptionName e1)
{
   //Catch 块
}
```

```java
        int[] arr = {1, 2, 3};

        try {
            System.out.println(arr[10]);
        } catch (Exception e) {        //ArrayIndexOutOfBoundsException 
            e.printStackTrace();
        }
        System.out.println("有异常处理后程序不会中断，此处也能输出");       
```

### 13.3 自定义异常

![](https://i-blog.csdnimg.cn/blog_migrate/66ec99cc37b37787c9e53b2bfd70dfc0.png)

![](https://i-blog.csdnimg.cn/blog_migrate/74fc1322396d03d39edcb534dcc46c0a.png)

-   如果希望写一个检查性异常类，则需要继承 Exception 类。
-   如果你想写一个运行时异常类，那么需要继承 RuntimeException 类。

```java
public class Student {
    public void checkScore(int score) throws ScoreException{    //要加throws，声明此方法会抛出异常
        if(score>100||score<0)throw new ScoreException("wrong Score");
        else System.out.println("分属正常");
    }
}


public class Demo {
    public static void main(String[] args) {
        Student s=new Student();
        try{
            s.checkScore(111);
        }catch (ScoreException e){
            e.printStackTrace();
        }
        System.out.println("这里也能输出");
    }
}

public class ScoreException extends Exception {     //自定义异常类

    public ScoreException() {
    }

    public ScoreException(String wrong_score) {
        super(wrong_score);    //带参构造，异常时控制台输出指定字符串
    }
}
```

## 十四、集合

### 14.1 集合体系

ArrayList底层是数组，查询快(get,contain)增删(add,remove)慢，LinkedList底层是链表，查询慢，增删快。

![](https://i-blog.csdnimg.cn/blog_migrate/3ee80d3136f2c94dc165355a945fe239.png)

**元素不可重复的集合：**HashXxx用hashCode()判断元素是否重复,TreeXxx用比较器。

Collection是add()和remove()，Map是put(),get().

![](https://i-blog.csdnimg.cn/blog_migrate/b62e8663feca3a442d177a68e642b504.png)

### 14.2 HashMap和HashSet区别

HashXxx用hashCode()判断元素是否重复. 

<table><tbody><tr><td><strong>*HashMap*</strong></td><td><strong>*HashSet*</strong></td></tr><tr><td>HashMap实现了Map接口</td><td>HashSet实现了Set接口</td></tr><tr><td>HashMap储存键值对</td><td>HashSet仅仅存储对象</td></tr><tr><td>使用put()方法将元素放入map中</td><td>使用add()方法将元素放入set中</td></tr><tr><td>HashMap中使用键对象来计算hashcode值</td><td>HashSet使用成员对象来计算hashcode值。</td></tr><tr><td>HashMap比较快，因为是使用唯一的键来获取对象</td><td>HashSet较HashMap来说比较慢，contains()时间复杂度也不是O(1)</td></tr></tbody></table>

### 14.3 HashSet和TreeSet的区别

相同点：单例集合，数据不可重复  
      
    不同点1：底层使用的储存数据结构不同：

  
      1，Hashset底层使用的是HashMap哈希表结构储存  
       2，而Treeset底层用的是TreeMap树结构储存。  
    

  
    不同点2：储存的数据保存唯一方式不用。

  
       1，Hashset是通过复写hashCode()方法和equals()方法来保证的。  
       2，而Treeset是通过Compareable接口的compareto方法来保证的。  
      
    不同点3：

        hashset无序   Treeset有序

### 14.4 ArrayList

可以动态修改的数组，没有固定大小的限制。

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        List<String> sites = new ArrayList<String>();
        sites.add("Google");        //增
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.add("Ai");
        System.out.println(sites);        //[Google, Runoob, Taobao, Weibo]

        Collections.sort(sites);        //字母顺序排序
        Collections.sort(sites, new Comparator<String>() {        //比较器长度排序
            @Override
            public int compare(String o1, String o2) {
                return o1.length()-o2.length();
            }
        });

        System.out.println(sites.get(1));  // 查，访问第二个元素Runoob
        System.out.println(sites.contains("Google"));   //查，是否包含
        sites.set(2, "Wiki"); // 改，第一个参数为索引位置，第二个为要修改的值
        sites.remove(3); // 删除第四个元素
        System.out.println(sites.size());//计算大小

        //迭代器
        Iterator<String> it=sites.iterator();
        while(it.hasNext()) System.out.println(it.next());
    }
}
```

List是接口，ArrayList是它的实现类  
以下两种方法都可以，但是不提倡第二种：

```java
List list=new ArrayList();
ArrayList list=new ArrayList();
```

 **List list=new ArrayList();好处**  
在设计模式中有对依赖倒置原则。程序要尽量依赖于抽象，不依赖于具体。 从Java语法上，这种方式是使用接口引用指向具体实现。  
比如，你若希望用LinkedList的实现来替代ArrayList的话，只需改动一行即可，其他的所有的都不需要改动：

```java
List list=new LinkedList()；
```

  
这也是一种很好的设计模式.一个接口有多种实现,当你想换一种实现方式时,你需要做的改动很小.

**面向接口编程**  
提高程序宽展性,以后修改维护好些  
声明一个接口的变量（接口的引用）可以指向一个实现类（实现该接口的类）的实例， 但是该接口的变量不能使用实现类中有，接口中没有的方法（实现类中没有重写的方法，自添加的方法）。。

并发修改异常：

![](https://i-blog.csdnimg.cn/blog_migrate/14131484dd9cba7d8e0670f863391865.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/390e3a0a1fccbb3bbafaf9a06902556a.png)

### 14.5 ListIterator

列表迭代器允许沿任一方向遍历列表

-   -   | Modifier and Type | Method and Description |
        | --- | --- |
        | `void` | `[add](../../java/util/ListIterator.html#add-E-)([E](../../java/util/ListIterator.html) e)`
        将指定的元素插入列表（可选操作）。
        
         |
        | `boolean` | `[hasNext](../../java/util/ListIterator.html#hasNext--)()`
        
        返回 `true`如果遍历正向列表，列表迭代器有多个元素。
        
         |
        | `boolean` | `[hasPrevious](../../java/util/ListIterator.html#hasPrevious--)()`
        
        返回 `true`如果遍历反向列表，列表迭代器有多个元素。
        
         |
        | `[E](../../java/util/ListIterator.html)` | `[next](../../java/util/ListIterator.html#next--)()`
        
        返回列表中的下一个元素，并且前进光标位置。
        
         |
        | `int` | `[nextIndex](../../java/util/ListIterator.html#nextIndex--)()`
        
        返回随后调用 [`next()`](../../java/util/ListIterator.html#next--)返回的元素的索引。
        
         |
        | `[E](../../java/util/ListIterator.html)` | `[previous](../../java/util/ListIterator.html#previous--)()`
        
        返回列表中的上一个元素，并向后移动光标位置。
        
         |
        | `int` | `[previousIndex](../../java/util/ListIterator.html#previousIndex--)()`
        
        返回由后续调用 [`previous()`](../../java/util/ListIterator.html#previous--)返回的元素的索引。
        
         |
        | `void` | `[remove](../../java/util/ListIterator.html#remove--)()`
        
        从列表中删除由 [`next()`](../../java/util/ListIterator.html#next--)或 [`previous()`](../../java/util/ListIterator.html#previous--)返回的最后一个元素（可选操作）。
        
         |
        | `void` | `[set](../../java/util/ListIterator.html#set-E-)([E](../../java/util/ListIterator.html) e)`
        
        用 [指定的](../../java/util/ListIterator.html#next--)元素替换由 [`next()`](../../java/util/ListIterator.html#next--)或 [`previous()`](../../java/util/ListIterator.html#previous--)返回的最后一个元素（可选操作）。
        
         |
        

```java
        ListIterator<String> it=sites.listIterator();
        while(it.hasNext()) System.out.println(it.next());
```

![](https://i-blog.csdnimg.cn/blog_migrate/26cc47490e016a6367f90ef61851b338.png)

这样就不会出现并发修改异常。

### 14.6 增强版for

内部原理是一个iterator迭代器。

 ![](https://i-blog.csdnimg.cn/blog_migrate/816517f597b1a2f97ab8f55f12fea311.png)

![](https://i-blog.csdnimg.cn/blog_migrate/21241b080ec10eccc384c6f50183bf7a.png)

### 14.7 LinkedList

| 方法 | 描述 |
| --- | --- |
| public void add(int index, E element) | 向指定位置插入元素。 |
| public void addFirst(E e) | 元素添加到头部。 |
| public void addLast(E e) | 元素添加到尾部。 |
| public void clear() | 清空链表。 |
| public E remove(int index) | 删除指定位置的元素。 |
| public E removeFirst() | 删除并返回第一个元素。 |
| public E removeLast() | 删除并返回最后一个元素。 |
| public boolean contains(Object o) | 判断是否含有某一元素。 |
| public E getFirst() | 返回第一个元素。 |
| public E getLast() | 返回最后一个元素。 |

```java
    public static void main(String[] args) {
        LinkedList<String> link=new LinkedList<String>();
        link.addLast("hello");
        link.addLast("world");
        for(String s:link) System.out.println(s);
        System.out.println(link);
    }
```

### 14.8 Hashset

**不包含重复元素，无序。**

允许有null值，不是线程安全的。

**无重原理：**通过hashCode值来判断重复元素的。

int hashCode():返回哈希值。同一对象哈希值相同，不同对象的哈希值默认不同，方法重写后可以相同。

哈希表是元素为链表的数组，默认容量16，负载因子0.75，处理冲突方法是链地址法。

```java
import java.util.HashSet;
import java.util.LinkedList;

public class Test2 {
    public static void main(String[] args) {
        HashSet<String > h=new HashSet<String>();
        h.add("nihao");
        String s1=new String("nihao");
        h.add(s1);
        System.out.println(s1=="nihao");        //false
        for(String s:h) System.out.println(s);     //不含重复元素 
    }
}
```

![](https://i-blog.csdnimg.cn/blog_migrate/6bd937ae10154820a66f7dceb15de847.png)

如果Hashset里的元素是对象，若想将成员变量相同视为对象相同，要重写hashCode()：

```java
import java.util.HashSet;

public class Test {
    public static void main(String[] args) {    //输出23
        Dog dog1=new Dog(23);
        Dog dog2=new Dog(23);
        HashSet<Dog> h=new HashSet<Dog>();
        h.add(dog1);h.add(dog2);
        for(Dog dog:h) System.out.println(dog.weight);   
    }
}
```

```java
package package1;

public class Dog extends Animal{
     int weight=4;
     public Dog(){
//         System.out.println("doggouzaao");
     }
     public Dog(int weight){
         this.weight=weight;
     }
    @Override
    public void show() {
        name="dogname";
        System.out.println("dog");
    }

    @Override
    public boolean equals(Object o) {    //alt+insert生成equals()和hashCode()方法。这里其实只需要重写hashCode方法就能保证自动去重，equals方法用于元素间的比较
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Dog dog = (Dog) o;

        return weight == dog.weight;
    }

    @Override
    public int hashCode() {
        return weight;
    }

    @Override
    public String toString() {
        return "Dog{" +
                "weight=" + weight +
                '}';
    }
}
```

### 14.9 LinkedHashSet

存取有序，不重复。

“LinkedHashSet的底层数据结构是由hash表和双向链表实现,双向链表维护了访问的次序。”

### 14.10 TreeSet

**有序，去重复。**

TreeSet():自然顺序排序

TreeSet(Comperable c):比较器排序。

如果TreeSet内元素是**基本数据类型**，它会自动去重有序。

如果TreeSet内元素是**对象**，要实现去重有序，有两种方法。**方法一，自然排序，**类要实现Comparable<>接口，并重写compareTo（Student s）方法；**方法二，比较器排序，**带比较器构造TreeSet，否则报错。

**方法一：自然排序**

**实现**Comparable<>**重写**compareTo（）方法

```java
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Dog dog1=new Dog(23);
        Dog dog2=new Dog(45);
        TreeSet<Dog> h=new TreeSet<Dog>();
        h.add(dog1);h.add(dog2);
        for(Dog dog:h) System.out.println(dog.weight);
    }
}
```

```java
package package1;

public class Dog extends Animal implements Comparable<Dog>{        //要实现Comperable<>并重写compareTo()方法
     int weight=4;
     public Dog(){
     }
     public Dog(int weight){
         this.weight=weight;
     }
    @Override
    public int compareTo(Dog dog){    //实参是上一只狗，本狗与上狗做比较
         return 1;        //按存取顺序排序，本狗比上只狗大
         //return -1;存储逆序排序
         //return 0;视为相等，重复删除。
            //return this.weight-dog.weight;按年龄从小到大排序，后狗-前狗。
    }
}
```

**方法二：比较器排序**

**无需重写，带参构造，参数为比较器Comparator<>。**

```java
        TreeSet<Dog> h=new TreeSet<Dog>(new Comparator<Dog>() {
            public int compare(Dog a,Dog b){
                if(a.weight!=b.weight) return a.weight-b.weight;
                else return a.name.compareTo(b.name);
            }
        });
```

### 14.11 泛型

#### 14.11.1 概念

泛型本质是将具体的类型参数化，提供了编译时类型安全检测机制。

定义格式：<类型>、<类型1，类型2...>

泛型是编译时类型安全检测，示例：

```java
import java.util.ArrayList;

public class Test2 {
    public static void main(String[] args) {
        Collection a=new ArrayList();
        Collection<String> b=new ArrayList<String>();    //泛型
        a.add("he");
        a.add(3);
        b.add("he");
//        b.add(3);   直接写时这里会报错，因为通过泛型指定了类型为String
        for(Object o:a) System.out.println(o);
        for(Object o:b) System.out.println(o);
    }
}
```

#### 14.11.2 泛型类

![](https://i-blog.csdnimg.cn/blog_migrate/94db66c2c54fc9b7c7ced7bed94b27a8.png)

泛型类将类型参数化、模板化，**创建对象时再指定具体类型**。

示例：

```java
package package2;

public class Generic<T> {
    private T t;

    public T getT() {
        return t;
    }

    public void setT(T t) {
        this.t = t;
    }
}
```

```java
package package2;

//创建对象时再指定具体类型
public class Test2 {
    public static void main(String[] args) {
        Generic<Integer> g=new Generic<Integer>();    //创建对象时指定具体类型为Integer
        g.setT(32);
        System.out.println(g.getT());

        Generic<String> g2=new Generic<String>();    //创建对象时指定具体类型为String
        g2.setT("hello");

//        g2.setT(34);指定了String，运行时安全检测报错
        System.out.println(g2.getT());
    }
}
```

#### 14.11.3 泛型方法

![](https://i-blog.csdnimg.cn/blog_migrate/ba9b24dbf667cb75e817c47c4b8c8fdd.png)

示例： 

```java
package package2;
public class Generic {
    public <T>void show(T t){
        System.out.println(t);
    }
}
```

#### 14.11.4 泛型接口

![](https://i-blog.csdnimg.cn/blog_migrate/5239d13863f82e119f15d979b7d7e5ac.png)

### 14.12 类型通配符

**类型通配符:<?>**

  
例如List<?>:表示元素类型未知的List,它的元素可以匹配任何类型。这种带通配符的List仅表示它是各种类型的父类,并不能把元素添加到其中

```java
List<?> l0=new ArrayList<Number>();    
```

  
**类型通配符的上限:List<?  extends 指定类型>**  
例:List<? extends Number> :它表示的类型是Number的子类型

```java
List<? extends Object> l1=new ArrayList<Number>();    //通配object的子类
```

  
**类型通配符的下限:List<?  super 指定类型>**  
例:List<? super Number>:它表示的类型是Number的父类

```java
List<? super Integer> l2=new ArrayList<Number>();    //通配Integer的父类
```

### 14.13 可变参数

(int... a)是将所有int参数封装到a数组里。

![](https://i-blog.csdnimg.cn/blog_migrate/fde10d6ba02b80112b843c9552908ccc.png)

 注意可变参数要放在后面。例如(int a,int... b)正确，(int... a,int b)会报错。

![](https://i-blog.csdnimg.cn/blog_migrate/ec1ede22f04d9f24b86f94f2146d3995.png)

### 14.14 HashMap

Interface Map<K,V>        k是键，V是值。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../java/util/HashMap.html#clear--" rel="nofollow">clear</a>()</code><p>从这张地图中删除所有的映射。</p></td></tr><tr><td><code>boolean</code></td><td><code><a href="../../java/util/HashMap.html#isEmpty--" rel="nofollow">isEmpty</a>()</code><p>如果此地图不包含键值映射，则返回 true 。</p></td></tr><tr><td><code><a href="../../java/util/HashMap.html" rel="nofollow">V</a></code></td><td><code><a href="../../java/util/HashMap.html#put-K-V-" rel="nofollow">put</a>(<a href="../../java/util/HashMap.html" rel="nofollow">K</a>&nbsp;key, <a href="../../java/util/HashMap.html" rel="nofollow">V</a>&nbsp;value)</code><p>将指定的值与此映射中的指定键相关联。</p></td></tr><tr><td><code><a href="../../java/util/HashMap.html" rel="nofollow">V</a></code></td><td><code><a href="../../java/util/HashMap.html#get-java.lang.Object-" rel="nofollow">get</a>(<a href="../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;key)</code><p>获取指定 key 对应对 value</p></td></tr><tr><td><code><a href="../../java/util/HashMap.html" rel="nofollow">V</a></code></td><td><code>getOrDefault(<a href="../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;key)</code><p>获取指定 key 对应对 value，如果找不到 key ，则返回设置的默认值</p></td></tr><tr><td><code><a href="../../java/util/HashMap.html" rel="nofollow">V</a></code></td><td><code><a href="../../java/util/HashMap.html#remove-java.lang.Object-" rel="nofollow">remove</a>(<a href="../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;key)</code><p>从该地图中删除指定键的映射（如果存在）。</p></td></tr><tr><td><code>boolean</code></td><td><code><a href="../../java/util/HashMap.html#containsKey-java.lang.Object-" rel="nofollow">containsKey</a>(<a href="../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;key)</code><p>如果此映射包含指定键的映射，则返回 true 。</p></td></tr><tr><td><code>boolean</code></td><td><code><a href="../../java/util/HashMap.html#containsValue-java.lang.Object-" rel="nofollow">containsValue</a>(<a href="../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;value)</code><p>如果此地图将一个或多个键映射到指定值，则返回 true 。</p></td></tr><tr><td><code><a href="../../java/util/Set.html" rel="nofollow">Set</a>&lt;<a href="../../java/util/HashMap.html" rel="nofollow">K</a>&gt;</code></td><td><code><a href="../../java/util/HashMap.html#keySet--" rel="nofollow">keySet</a>()</code><p>返回此地图中包含的键的<a href="../../java/util/Set.html" rel="nofollow"><code>Set</code></a>集合。</p><p></p></td></tr><tr><td><code><a href="../../java/util/Collection.html" rel="nofollow">Collection</a>&lt;<a href="../../java/util/HashMap.html" rel="nofollow">V</a>&gt;</code></td><td><code><a href="../../java/util/HashMap.html#values--" rel="nofollow">values</a>()</code><p>返回此地图中包含的值的<a href="../../java/util/Collection.html" rel="nofollow"><code>Collection</code></a>集合。</p></td></tr><tr><td><code><a href="../../java/util/Set.html" rel="nofollow">Set</a>&lt;<a href="../../java/util/Map.Entry.html" rel="nofollow">Map.Entry</a>&lt;<a href="../../java/util/HashMap.html" rel="nofollow">K</a>,<a href="../../java/util/HashMap.html" rel="nofollow">V</a>&gt;&gt;</code></td><td><code><a href="../../java/util/HashMap.html#entrySet--" rel="nofollow">entrySet</a>()</code><p>返回此地图中包含的映射的<a href="../../java/util/Set.html" rel="nofollow"><code>Set</code></a>集合。</p></td></tr></tbody></table>
        

遍历方法1：keySet()获取键的Set集合，遍历Set集合，通过get（）获取值。

方法2：entrySet（）获取键值对Map.Entry<K,V>的Set集合，遍历Set集合，通过getKey()和getValue()获取键值。

```java
import java.util.*;

public class Test2 {
    public static void main(String[] args) {
        //声明
        Map<String, String> map = new HashMap<>();
        //添加
        map.put("aaa","bbb");map.put("cc","dd");map.put("e","f");
        //获取,如果"aaa"对应value不为null则返回value；如果为null，则返回null。
        System.out.println(map.get("aaa"));
        //获取,如果"aaa"对应value不为null则返回value；如果为null，则返回"default"字符串。
        System.out.println(map.getOrDefault("aaa", "default"));
        //获取所有keys
        Set<String> strings = map.keySet();
        //获取所有values
        Collection<String> values = map.values();
        //遍历map
        Set<Map.Entry<String,String>> set=map.entrySet();
        for(Map.Entry<String,String> i:set){
            System.out.println(i.getKey()+i.getValue());
        }
    }

}
```

如果HashMap键是对象，并且要求对象内成员变量值相等视为同一对象，则重写hashCode().

### 14.15 Collections类

-   -   | Modifier and Type | Method and Description |
        | --- | --- |
        | `static <T extends [Comparable](../../java/lang/Comparable.html)<? super T>>  
        void` | `[sort](../../java/util/Collections.html#sort-java.util.List-)([List](../../java/util/List.html)<T> list)`
        根据其元素的[natural ordering](../../java/lang/Comparable.html)对指定的列表进行排序。
        
         |
        | `static void` | `[reverse](../../java/util/Collections.html#reverse-java.util.List-)([List](../../java/util/List.html)<?> list)`
        
        反转指定列表中元素的顺序。
        
         |
        | `static void` | `[shuffle](../../java/util/Collections.html#shuffle-java.util.List-)([List](../../java/util/List.html)<?> list)`
        
        使用默认的随机源随机排列指定的列表。
        
         |
        

## 十五、i/o流

### 15.1 继承关系、路径斜杠

![](https://i-blog.csdnimg.cn/blog_migrate/594d446ce13dc1a873b3e52ddea01a1b.png)

路径斜杠可以是//,/,\\\\,不能是\\，因为它是转义符。

### 15.2 io流分类

**按数据流向：**

**输入流：**读数据。

**输出流：**写数据。

**按数据类型：**

**字节流：**它处理单元为**1个字节**（byte），操作字节和字节数组，存储的是**二进制文件**。

应用范围：如果是音频文件、图片、歌曲，就用字节流好点（1byte = 8位）。

**字符流：**它处理的单元为**2个字节**的Unicode字符，分别操作字符、字符数组或字符串，字符流是由Java虚拟机将字节转化为2个字节的Unicode字符为单位的字符而成的。

应用范围：如果是关系到中文（文本）的，用字符流好点（1Unicode = 2字节 = 16位）；

### 15.3 File类

File封装的不是真正的文件，只是路径。

**创建文件示例：** 

```java
import java.io.File;
import java.io.IOException;

public class Demo {
    public static void main(String[] args) throws IOException {
        File f=new File("D:\\1\\2.txt");
      //只创建已存在文件夹“D://1”下的2.txt。若“D://1”不存在，报错IOException: 系统找不到指定的路径。
        System.out.println(f.createNewFile());  //true，当目标位置已存在同名文件则创建失败输出false
    }
}
```

> **注意：**在当前包内IO流，使用File类创建文件
> 
> ```java
> new File("1.txt");
> ```
> 
> 默认存的位置是在项目文件夹下，而不是包文件夹下。
> 
> **关于路径斜杠和反斜杠：**
> 
> 正斜杠“/”和“//”都可以，反斜杠必须“\\\\”，因为“\\”会ASCII转义，“\\\\”在字符串里才是“\\”。
> 
> ```java
>         File file = new File("D://1//1.txt");
>         File file1 = new File("D:/1/2.txt");
>         File file2 = new File("D:\\1\\3.txt");
> //        File file3 = new File("D:\1\4.txt");  //这样会报错，单个反斜杠会进行转义
>         System.out.println(file.createNewFile());   //true
>         System.out.println(file1.createNewFile());   //true
>         System.out.println(file2.createNewFile());   //true
> //        System.out.println(file3.createNewFile());   //false 
> ```
> 
> **查看当前路径：**
> 
> ```java
> System.out.println(System.getProperty("user.dir"));    //D:\workspace\java\test
> ```

**创建删除文件和文件夹的api：**

<table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>boolean</code></td><td><code><a href="../../java/io/File.html#createNewFile--" rel="nofollow">createNewFile</a>()</code><p>当且仅当具有该名称的文件尚不存在时，原子地创建一个由该抽象路径名命名的新的空文件。</p></td></tr><tr><td><code>boolean</code></td><td><code><a href="../../java/io/File.html#mkdir--" rel="nofollow">mkdir</a>()</code><p>创建由此抽象路径名命名的目录。</p></td></tr><tr><td><code>boolean</code></td><td><code><a href="../../java/io/File.html#mkdirs--" rel="nofollow">mkdirs</a>()</code><p>创建由此抽象路径名命名的目录，包括任何必需但不存在的父目录。</p></td></tr><tr><td><code>boolean</code></td><td><code><a href="../../java/io/File.html#delete--" rel="nofollow">delete</a>()</code><p>删除由此抽象路径名表示的文件或目录。</p></td></tr><tr><td><code><a href="../../java/io/File.html" rel="nofollow">File</a>[]</code></td><td><code><a href="../../java/io/File.html#listFiles--" rel="nofollow">listFiles</a>()</code><p>返回一个抽象路径名数组，表示由该抽象路径名表示的目录中的文件。</p></td></tr></tbody></table>

![](https://i-blog.csdnimg.cn/blog_migrate/c6c040557d40366d98e42ae7f61d2ddf.png)

**举例：**

```java
        File f=new File("1\\2\\3");
        System.out.println(f.mkdirs());
        File f1=new File("1\\2\\3\\4.txt");
        System.out.println(f1.createNewFile());

        File[] f2=f.listFiles();        //listFiles()是路径下的所有文件组成的数组，若f文件会报错
        for(File file:f2){
            if(file.isFile()) System.out.println(file.getName()+","+file.getPath());
        }
//删除
//删除目录时要确保目录下没文件。

        f1.delete();f.delete();
```

![](https://i-blog.csdnimg.cn/blog_migrate/dfe21214c351cc893f80b58fc60150ce.png)

 返回false是因为文件夹和文件已存在。

### 15.4 字节输出流OutputStream

**概念：** 

Java中的 InputStream 和 OutputStream 都是 io 包中面向字节操作的顶级抽象类，关于java同步 io字节流的操作都是基于这两个的。

**子类：**

-   网络数据传输：SocketInputStream 和 SocketOutputStream
-   文件操作：**FileInputStream 和 FileOutputStream**
-   字节数据操作：DataInputStream 和 DataOutputStream

**OutputStream类是所有输出字节流的超类：**

![这里写图片描述](https://i-blog.csdnimg.cn/blog_migrate/b88357186cfdb24cdbffdf5bd4ba4707.png)

**常用api：** 

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#close--" rel="nofollow">close</a>()</code><p>关闭此输出流并释放与此流相关联的任何系统资源。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#flush--" rel="nofollow">flush</a>()</code><p>刷新此输出流并强制任何缓冲的输出字节被写出。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#write-byte:A-" rel="nofollow">write</a>(byte[]&nbsp;b)</code><p>将 <code>b.length</code>字节从指定的字节数组写入此输出流。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#write-byte:A-int-int-" rel="nofollow">write</a>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code><p>从指定的字节数组写入 <code>len</code>个字节，从偏移 <code>off</code>开始输出到此输出流。</p></td></tr><tr><td><code>abstract void</code></td><td><code><a href="../../java/io/OutputStream.html#write-int-" rel="nofollow">write</a>(int&nbsp;b)</code><p>将指定的字节写入此输出流。</p></td></tr></tbody></table>
        

**示例，OutputStream封装到BufferedWriter：**

![](https://i-blog.csdnimg.cn/blog_migrate/abfe07e0033761f2557f728fed7a6af2.png)

字节输出流OutputStream转字符输出流OutputStreamWriter转缓冲字符输出流BufferedWriter。s是Socket对象。

### 15.5 字节输入流InputStream

**概念：** 

Java中的 InputStream 和 OutputStream 都是 io 包中面向字节操作的顶级抽象类，关于java同步 io字节流的操作都是基于这两个的。

**子类：**

-   网络数据传输：SocketInputStream 和 SocketOutputStream
-   文件操作：**FileInputStream 和 FileOutputStream**
-   字节数据操作：DataInputStream 和 DataOutputStream

**InputStream是所有输入字节流类的超类：**

![这里写图片描述](https://i-blog.csdnimg.cn/blog_migrate/c22e6a53d377ab3a117b79d5a53e02dc.png)

**常用api：** 

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>abstract int</code></td><td><code><a href="../../java/io/InputStream.html#read--" rel="nofollow">read</a>()</code><p>从输入流读取数据的下一个字节。</p></td></tr><tr><td><code>int</code></td><td><code><a href="../../java/io/InputStream.html#read-byte:A-" rel="nofollow">read</a>(byte[]&nbsp;b)</code><p>从输入流读取一些字节数，并将它们存储到缓冲区 <code>b，返回值为长度</code>&nbsp;。</p></td></tr><tr><td><code>int</code></td><td><code><a href="../../java/io/InputStream.html#read-byte:A-int-int-" rel="nofollow">read</a>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code><p>从输入流读取最多 <code>len</code>字节的数据到一个字节数组。</p></td></tr></tbody></table>
        

**字节输入流InputStream封装到字符缓冲输入流BufferedWriter：**

这里s是Socket对象：

![](https://i-blog.csdnimg.cn/blog_migrate/fd811e99892386613e9d6c32b617f0c4.png)

### 15.6 文件输出流FileOutputStream

是OutputStream子类。

输出流是写数据，把数据输出到文件里。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.io.File-" rel="nofollow">FileOutputStream</a>(<a href="../../java/io/File.html" rel="nofollow">File</a>&nbsp;file)</code><p>创建文件输出流以写入由指定的 <code>File</code>对象表示的文件。</p></td></tr><tr><td><code><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.lang.String-" rel="nofollow">FileOutputStream</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name)</code><p>创建文件输出流以指定的名称写入文件</p></td></tr><tr><td><code><a href="../../java/io/FileOutputStream.html#FileOutputStream-java.lang.String-boolean-" rel="nofollow">FileOutputStream</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name, boolean&nbsp;append)</code><p>创建文件输出流以指定的名称写入文件。</p></td></tr></tbody></table>
        

默认彻底覆盖写入，append为true是追加写入。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../java/io/FileOutputStream.html#write-byte:A-" rel="nofollow">write</a>(byte[]&nbsp;b)</code><p>将 <code>b.length</code>个字节从指定的字节数组写入此文件输出流。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/FileOutputStream.html#write-byte:A-int-int-" rel="nofollow">write</a>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code><p>将 <code>len</code>字节从位于偏移量 <code>off</code>的指定字节数组写入此文件输出流。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/FileOutputStream.html#write-int-" rel="nofollow">write</a>(int&nbsp;b)</code><p>将指定的字节写入此文件输出流。</p></td></tr></tbody></table>
        

**示例，将“abcde” 写入1.txt文件中：**

```java
        FileOutputStream fos=new FileOutputStream("1.txt");
        byte b[]="abcde".getBytes();
        fos.write(b);
        fos.close();
```

完整版： 

```java
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class Demo {
    public static void main(String[] args)  {
        FileOutputStream fos=null;
        try {
             fos=new FileOutputStream("z://1.txt");
            byte b[]="efe".getBytes();
            fos.write(b);
            fos.close();
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            System.out.println("finally");
            if(fos!=null){        //防止空指针异常
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

注意写数据时换行符，windows系统下是\\r\\n，linux的换行是\\n，mac换行\\r.

### 15.7 文件输入流 FileInputStream

#### 15.7.1 概述 

是InputStream子类。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/FileInputStream.html#FileInputStream-java.lang.String-" rel="nofollow">FileInputStream</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name)</code><p>通过打开与实际文件的连接来创建一个 <code>FileInputStream</code> ，该文件由文件系统中的路径名 <code>name</code>命名。</p></td></tr></tbody></table>
        

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td style="width:51px;"><code>int</code></td><td style="width:573px;"><code><a href="../../java/io/FileInputStream.html#read--" rel="nofollow">read</a>()</code><p>从该输入流读取一个字节的数据，如果读到文件末尾EOF，返回值是-1。</p></td></tr><tr><td style="width:51px;"><code>int</code></td><td style="width:573px;"><code><a href="../../java/io/FileInputStream.html#read-byte:A-" rel="nofollow">read</a>(byte[]&nbsp;b)</code><p>从该输入流读取最多 <code>b.length</code>个字节的数据为字节数组。</p></td></tr><tr><td style="width:51px;"><code>int</code></td><td style="width:573px;"><strong><code><a href="../../java/io/FileInputStream.html#read-byte:A-int-int-" rel="nofollow">read</a>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code></strong><p>从该输入流读取最多 <code>len</code>字节的数据为字节数组，off是偏移量，为0是从字节数组起始处开始读。</p></td></tr></tbody></table>
        

返回的int是读取字节的个数。

```java
        FileInputStream fis=new FileInputStream("1.txt");
        byte b[]=new byte[1024];    //一般是1024整数倍
        int len=-1;
        while ((len= fis.read())!=-1) System.out.println(new String(b,0,len));
        fis.close();
```

#### 15.7.2 练习，通过文件输入输出流复制图片

**常规方法：** 

```java
        FileInputStream fis=new FileInputStream("D://1.png");
        FileOutputStream fos=new FileOutputStream("D://1//1.png");
        byte []b=new byte[1024];
        int len=fis.read(b);
        while(len!=-1){
            System.out.println(len);
            fos.write(b,0,len);len=fis.read(b);
        }
```

> **扩展，Maven简单方法：**
> 
> 学maven后再用这个方法。
> 
>  使用IOUtils.copy(fis,os)进行流的复制（推荐）
> 
> (1)pom.xml添加依赖
> 
> ```XML
> <dependency>
>     <groupId>commons-io</groupId>
>     <artifactId>commons-io</artifactId>
>     <version>2.6</version>
> </dependency>
> ```
> 
> (2)调用工具类方法实现复制
> 
> ```java
> //fis:输入流
> //os:输出流
> IOUtils.copy(fis,os);
> ```

### 15.8 字节缓冲流

**特点：** 

字节缓冲流仅**提供缓冲区**，真正读写数据还要靠基本字节流对象操作。

字节缓冲流实现复制文件比基本字节流**快很多**。

#### 15.8.1 字节缓冲输出流BufferedOutputStream

该类实现缓冲输出流。 通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用。

-   -   <table border="0" cellpadding="3" cellspacing="0"><caption>构造方法 &nbsp;</caption><tbody><tr><th>Constructor and Description</th></tr><tr><td><code><a href="../../java/io/BufferedOutputStream.html#BufferedOutputStream-java.io.OutputStream-" rel="nofollow">BufferedOutputStream</a>(<a href="../../java/io/OutputStream.html" rel="nofollow">OutputStream</a>&nbsp;out)</code><p>创建一个新的缓冲输出流，以将数据写入指定的底层输出流。</p></td></tr><tr><td><code><a href="../../java/io/BufferedOutputStream.html#BufferedOutputStream-java.io.OutputStream-int-" rel="nofollow">BufferedOutputStream</a>(<a href="../../java/io/OutputStream.html" rel="nofollow">OutputStream</a>&nbsp;out, int&nbsp;size)</code><p>创建一个新的缓冲输出流，以便以指定的缓冲区大小将数据写入指定的底层输出流。</p></td></tr></tbody></table>
        

#### 15.8.2 字节缓冲输入流BufferedInputStream

当创建`BufferedInputStream`时，将创建一个内部缓冲区数组。 当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次有多个字节。

### 15.9 字符流

#### 15.9.1 概要和继承关系

**为什么要用字符流？**

GBK编码，一个汉字占用2个字节。

utf-8编码，一个汉字占用3个字节。

汉字存储时，无论使用哪种编码，第一个字节都是负数。

_所以**字节流**_在读中文的时候有可能会读到半个中文,造成**乱码**

**解决办法：**

1.使用字符流（底层是字节流，字符流=字节流+编码表）

2._字节流_直接操作字符,写出中文必须将字符串换成字节数组

```java
package com.heima.stream;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class Demo10_Chinese {

	public static void main(String[] args) throws IOException {
		//demo1();
		FileOutputStream fos = new FileOutputStream("zzz.txt");
		fos.write("我读书少,你不要骗我".getBytes());
		fos.write("\r\n".getBytes());
		fos.close();
	}

	public static void demo1() throws FileNotFoundException, IOException {
		FileInputStream fis = new FileInputStream("yyy.txt");
		byte[] arr = new byte[4];
		int len;
		while((len = fis.read(arr)) != -1) {
			System.out.println(new String(arr,0,len));
		}
		fis.close();
	}
}
```

**继承关系：**

![这里写图片描述](https://i-blog.csdnimg.cn/blog_migrate/490207179795979a9b6148b17c681164.png)

![这里写图片描述](https://i-blog.csdnimg.cn/blog_migrate/aecb41e463d1ac96ac50eb8ee04c3b0d.png)

#### 15.9.2 字符输出流OutputStreamWriter

只用于字符转字节，写入字节文件。

OutputStreamWriter:将字符编码为字节，再写入字节文件。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStreamWriter.html#write-char:A-int-int-" rel="nofollow">write</a>(char[]&nbsp;cbuf, int&nbsp;off, int&nbsp;len)</code><p>写入字符数组的一部分。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStreamWriter.html#write-int-" rel="nofollow">write</a>(int&nbsp;c)</code><p>写一个字符</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStreamWriter.html#write-java.lang.String-int-int-" rel="nofollow">write</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;str, int&nbsp;off, int&nbsp;len)</code><p>写一个字符串的一部分。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStreamWriter.html#flush--" rel="nofollow">flush</a>()</code><p>刷新流。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStreamWriter.html#close--" rel="nofollow">close</a>()</code><p>关闭流，先刷新。</p></td></tr></tbody></table>
        

刷新后还能继续写数据，关闭后不能再写数据。

#### 15.9.3 字符输入流InputStreamReader

只用于从字节文件解码出字符。

InputStreamReader:读取字节文件，并将字节解码为字符。构造函数传字节输入流FileInputStream或输入流InputStream.

-   -   | Modifier and Type | Method and Description |
        | --- | --- |
        | `void` | `[close](../../java/io/InputStreamReader.html#close--)()`
        关闭流并释放与之相关联的任何系统资源。
        
         |
        | `[String](../../java/lang/String.html)` | `[getEncoding](../../java/io/InputStreamReader.html#getEncoding--)()`
        
        返回此流使用的字符编码的名称。
        
         |
        | `int` | `[read](../../java/io/InputStreamReader.html#read--)()`
        
        读一个字符，返回值是字符
        
         |
        | `int` | `[read](../../java/io/InputStreamReader.html#read-char:A-int-int-)(char[] cbuf, int offset, int length)`
        
        将字符读入数组的一部分，返回值是字符串长度。
        
         |
        | `boolean` | `[ready](../../java/io/InputStreamReader.html#ready--)()`
        
        告诉这个流是否准备好被读取。
        
         |
        

#### 15.9.4 字符串的编码解码

**编码：**通过OutputStreamWriter将字符**编码为字节**，再写入字节文件。

**解码：**通过InputStreamReader读取字节文件，并将字节**解码为字符**

**编码解码方法：** 

![](https://i-blog.csdnimg.cn/blog_migrate/5a87261007856db2f38b068108213294.png)

#### 15.9.5 字符流的编码解码

编码：字符文件转字节文件

解码：字节文件转字符文件

先写再读：

```java
        OutputStreamWriter osw=new OutputStreamWriter(new FileOutputStream("1.txt"),"utf-8");
        osw.write("你好hello");
        osw.close();   //close很重要
        InputStreamReader isr=new InputStreamReader(new FileInputStream("1.txt"),"utf-8");
        int ch;
        while ((ch=isr.read())!=-1){
            System.out.println((char) ch);
        }
//        char []c=new char[1024];int len;
//        while ((len=isr.read(c))!=-1){
//            System.out.println(new String(c,0,len));
//        }
        isr.close();
```

![](https://i-blog.csdnimg.cn/blog_migrate/b349798162bf9efe1489ed73525c04bb.png)

#### 15.9.6 FileWriter和FileReader

字符输入输出流的子类，简化他们。涉及到编码解码问题，还是要使用字符输入输出流。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/FileWriter.html#FileWriter-java.lang.String-" rel="nofollow">FileWriter</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;fileName)</code><p>构造一个给定文件名的FileWriter对象。</p><p></p></td></tr><tr><td><code><a href="../../java/io/FileReader.html#FileReader-java.lang.String-" rel="nofollow">FileReader</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;fileName)</code><p>创建一个新的 FileReader ，给定要读取的文件的名称。</p></td></tr></tbody></table>
        

#### 15.9.7 字符缓冲流BufferedWriter和BufferedReader

**BufferedWriter**

-   将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入。
    
    可以指定缓冲区大小，或者可以接受默认大小。 默认值足够大，可用于大多数用途。
    
-   提供了一个newLine（）方法，它使用平台自己的系统属性line.separator定义的行分隔符概念。
    
-   每次写完bw.flush();可以将缓冲字符写入文本，虽然close()也能刷新后关闭，但加上flush更保险。
    
-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/BufferedWriter.html#BufferedWriter-java.io.Writer-" rel="nofollow">BufferedWriter</a>(<a href="../../java/io/Writer.html" rel="nofollow">Writer</a>&nbsp;out)</code><p>创建使用默认大小的输出缓冲区的缓冲字符输出流。</p></td></tr></tbody></table>
        

**BufferedReader**

从字符输入流读取文本，缓冲字符，以提供字符，数组和行的高效读取。

可以指定缓冲区大小，或者可以使用默认大小。 默认值足够大，可用于大多数用途。

BufferedReader实现读取键盘录入：

![](https://i-blog.csdnimg.cn/blog_migrate/2870a36ed7ef83d96fbbb48ca48d5ae7.png)

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/BufferedReader.html#BufferedReader-java.io.Reader-" rel="nofollow">BufferedReader</a>(<a href="../../java/io/Reader.html" rel="nofollow">Reader</a>&nbsp;in)</code><p>创建使用默认大小的输入缓冲区的缓冲字符输入流</p></td></tr></tbody></table>
        

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/lang/String.html" rel="nofollow">String</a></code></td><td><code><a href="../../java/io/BufferedReader.html#readLine--" rel="nofollow">readLine</a>()</code><p>读一行文字（仅内容，无换行符），到文件末尾返回null。</p></td></tr></tbody></table>
        

#### 15.9.8 练习，字符缓冲流文本复制

```java
//文本复制
import java.io.*;
import java.nio.charset.StandardCharsets;
import java.util.Arrays;

public class Demo {
    public static void main(String[] args) throws IOException {
        BufferedWriter bw=new BufferedWriter(new FileWriter("1//copy.txt"));
        BufferedReader br=new BufferedReader(new FileReader("1.txt"));
        char[] c=new char[1024];
        int len;
        while((len=br.read(c))!=-1){
            bw.write(c,0,len);bw.flush();
        }
        bw.close();br.close();
    }
}
```

或者

```java
        BufferedWriter bw=new BufferedWriter(new FileWriter("1//copy.txt"));
        BufferedReader br=new BufferedReader(new FileReader("1.txt"));
        String line;
        while ((line=br.readLine())!=null){
            bw.write(line);bw.newLine();bw.flush();
        }
        bw.close();br.close();
```

### 15.10 I/O流JDK7异常处理

![](https://i-blog.csdnimg.cn/blog_migrate/2f7d1340593bf21e30892cc25dad8019.png)

```java
//文本复制JDK7异常处理
import java.io.*;
import java.nio.charset.StandardCharsets;
import java.util.Arrays;

public class Demo {
    public static void main(String[] args){
        try(BufferedWriter bw=new BufferedWriter(new FileWriter("1\\2\\copy.txt"));
            BufferedReader br=new BufferedReader(new FileReader("1.txt"));){
            char[] c=new char[1024];
            int len;
            while((len=br.read(c))!=-1){
                bw.write(c,0,len);
            }
//            bw.close();br.close();不用close了，JDK7自动释放资源
        }catch (IOException e){
            e.printStackTrace();
        }

    }
}
```

### 15.11 特殊操作流 

#### 15.11.1 标准输入输出流System.in和System.out

![](https://i-blog.csdnimg.cn/blog_migrate/180a74f9963d612f19967853626af823.png)

标准输出流：System.out

标准输入流：System.in

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>static <a href="../../java/io/PrintStream.html" rel="nofollow">PrintStream</a></code></td><td><code><a href="../../java/lang/System.html#err" rel="nofollow">err</a></code><p>“标准”错误输出流。</p></td></tr><tr><td><code>static <a href="../../java/io/InputStream.html" rel="nofollow">InputStream</a></code></td><td><code><a href="../../java/lang/System.html#in" rel="nofollow">in</a></code><p>“标准”输入流。返回输入字节流</p></td></tr><tr><td><code>static <a href="../../java/io/PrintStream.html" rel="nofollow">PrintStream</a></code></td><td><code><a href="../../java/lang/System.html#out" rel="nofollow">out</a></code><p>“标准”输出流。返回字节打印流</p></td></tr></tbody></table>
        

```java
        PrintStream ps=System.out;
        ps.println("hello");
```

#### 15.11.2 字节打印流PrintStream

只负责输出数据，不负责读取数据。

```java
PrintStream pw=new PrintStream("1.txt");
pw.println("hello");
pw.println(23);
pw.close();
```

#### 15.11.3 字符打印流PrintWriter

```java
PrintWriter pw=new PrintWriter("1.txt",true);//自动刷新true
pw.println("hello");        //直接写一行加刷新
pw.println(23);
```

#### 15.11.4 对象序列化流

ObjectOutputStream

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/ObjectOutputStream.html#ObjectOutputStream-java.io.OutputStream-" rel="nofollow">ObjectOutputStream</a>(<a href="../../java/io/OutputStream.html" rel="nofollow">OutputStream</a>&nbsp;out)</code><p>创建一个写入指定的OutputStream的ObjectOutputStream。</p></td></tr></tbody></table>
        

对象序列化方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i25"><td><code>void</code></td><td><code><a href="../../java/io/ObjectOutputStream.html#writeObject-java.lang.Object-" rel="nofollow">writeObject</a>(<a href="../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;obj)</code><p>将指定的对象写入ObjectOutputStream。</p></td></tr></tbody></table>
        

-   只有支持java.io.Serializable接口的对象才能写入流中，将类实现Serializable接口即可，该接口是标识接口，不需要实现方法。
    

![](https://i-blog.csdnimg.cn/blog_migrate/62848aef595ba31ea18a26e08cbca971.png)

**异常java.io.InvalidClassException当序列化运行时检测到类中的以下问题之一时抛出。**

-   类的串行版本与从流中读取的类描述符的类型不匹配（序列化对象后修改了类文件）
-   该类包含未知的数据类型
-   该类没有可访问的无参数构造函数

_强烈建议_所有可序列化的类都明确声明serialVersionUID值，因为默认的serialVersionUID计算对类详细信息非常敏感，从而出现InvalidClassException。

为了保证不同Java编译器实现之间的一致的serialVersionUID值，一个可序列化的类必须声明一个显式的serialVersionUID值，尽量使用private修饰符。

![](https://i-blog.csdnimg.cn/blog_migrate/0a237ea52607cc341447ecab6568f186.png)

 **被transient修饰的成员变量不参与序列化。**

#### 15.11.5 对象反序列化流ObjectInputStream

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/ObjectInputStream.html#ObjectInputStream-java.io.InputStream-" rel="nofollow">ObjectInputStream</a>(<a href="../../java/io/InputStream.html" rel="nofollow">InputStream</a>&nbsp;in)</code><p>创建从指定的InputStream读取的ObjectInputStream。</p></td></tr></tbody></table>
        

反序列化方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i18"><td><code><a href="../../java/lang/Object.html" rel="nofollow">Object</a></code></td><td><code><a href="../../java/io/ObjectInputStream.html#readObject--" rel="nofollow">readObject</a>()</code><p>从ObjectInputStream读取一个对象。</p></td></tr></tbody></table>
        

![](https://i-blog.csdnimg.cn/blog_migrate/434a3b6a5d50b4ac36b3b75498698864.png)

#### 15.11.6 Properties和IO流结合

 ![](https://i-blog.csdnimg.cn/blog_migrate/aa92d9210c27745314dc91ba65ea654c.png)

Properties类虽然是Map的子类，但它不是泛型类，put方法添加键值时，键值都是Object类型的： 

![](https://i-blog.csdnimg.cn/blog_migrate/5eb7ce4970575229736b3d63119323a9.png)

用String类型键值对要用特有方法：

<table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/lang/String.html" rel="nofollow">String</a></code></td><td><code><a href="../../java/util/Properties.html#getProperty-java.lang.String-" rel="nofollow">getProperty</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;key)</code><p>使用此属性列表中指定的键搜索属性。</p></td></tr><tr><td><code><a href="../../java/lang/Object.html" rel="nofollow">Object</a></code></td><td><code><a href="../../java/util/Properties.html#setProperty-java.lang.String-java.lang.String-" rel="nofollow">setProperty</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;key, <a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;value)</code><p>添加字符串类型键值对。</p></td></tr><tr><td><code><a href="../../java/util/Set.html" rel="nofollow">Set</a>&lt;<a href="../../java/lang/String.html" rel="nofollow">String</a>&gt;</code></td><td><code><a href="../../java/util/Properties.html#stringPropertyNames--" rel="nofollow">stringPropertyNames</a>()</code><p>返回此属性列表中的一组键，其中键及其对应的值为字符串，包括默认属性列表中的不同键，如果尚未从主属性列表中找到相同名称的键。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/util/Properties.html#load-java.io.InputStream-" rel="nofollow">load</a>(<a href="../../java/io/InputStream.html" rel="nofollow">InputStream</a>&nbsp;inStream)</code><p>从输入字节流读取属性列表（键和元素对）。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/util/Properties.html#load-java.io.Reader-" rel="nofollow">load</a>(<a href="../../java/io/Reader.html" rel="nofollow">Reader</a>&nbsp;reader)</code><p>以简单的线性格式从输入字符流读取属性列表（关键字和元素对）。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/util/Properties.html#store-java.io.OutputStream-java.lang.String-" rel="nofollow">store</a>(<a href="../../java/io/OutputStream.html" rel="nofollow">OutputStream</a>&nbsp;out, <a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;comments)</code><p>将此属性列表（键和元素对）写入此 <code>Properties</code>表中，以适合于使用 <a href="../../java/util/Properties.html#load-java.io.InputStream-" rel="nofollow"><code>load(InputStream)</code></a>方法加载到 <code>Properties</code>表中的格式输出流。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/util/Properties.html#store-java.io.Writer-java.lang.String-" rel="nofollow">store</a>(<a href="../../java/io/Writer.html" rel="nofollow">Writer</a>&nbsp;writer, <a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;comments)</code><p>将此属性列表（键和元素对）写入此 <code>Properties</code>表中，以适合使用 <a href="../../java/util/Properties.html#load-java.io.Reader-" rel="nofollow"><code>load(Reader)</code></a>方法的格式输出到输出字符流。</p></td></tr><tr><td></td><td></td></tr></tbody></table>

遍历：

![](https://i-blog.csdnimg.cn/blog_migrate/5ae14d6134510b9bc5d728944be64387.png)

 **与IO流结合，写入配置文件并读**

```java
        Properties prop=new Properties();
        prop.setProperty("a","b");prop.setProperty("c","d");
        BufferedWriter bw=new BufferedWriter(new FileWriter("1.txt"));
        prop.store(bw,"hello");
        bw.close();


        Properties p2=new Properties();
        BufferedReader br = new BufferedReader(new FileReader("1.txt"));
        p2.load(br);
        Set<String> s=p2.stringPropertyNames();
        for(String key:s){
            System.out.println(key+p2.getProperty(key));
```

 ![](https://i-blog.csdnimg.cn/blog_migrate/08bb3b61a9bfc55309b8efd65a6364d4.png)

## 十六、多线程

### 16.1 概念

**进程：**一个进程包括由操作系统分配的内存空间，包含一个或多个线程。

**一个线程不能独立的存在**，它必须是进程的一部分。一个进程一直运行，直到所有的非守护线程都结束运行后才能结束。

**线程：**一条线程指的是进程中一个单一顺序的控制流，是一条执行路径。

一个进程中可以并发多个线程，每条线程并行执行不同的任务。

**单线程：**一条进程里只有一条执行路径。

**多线程：**一个进程里有多条执行路径。

**java是抢占式调度模型**

**优先级：**每一个 Java 线程都有一个优先级，优先级是一个整数，其取值范围是 1 （Thread.MIN\_PRIORITY ） - 10 （Thread.MAX\_PRIORITY ）。

默认情况下，每一个线程都会分配一个优先级 NORM\_PRIORITY（5）。

优先级高的线程只是获取CPU时间片的几率高，并不能保证先执行。

**创建线程方法：**

-   通过实现 Runnable 接口；
-   通过继承 Thread 类本身；
-   通过 Callable 和 Future 创建线程。

### 16.2 创建线程方法1:继承Thread类

1.  创建一个新的类，该类继承 Thread 类。
2.  继承类必须重写 run() 方法。该方法是新线程的入口点。
3.  创建对象。
4.  启动线程， start() 方法，虚拟机调用该线程run方法。

**run()和start()区别：**

**run（）：**封装线程执行的代码，直接调用相当于普通方法的调用。

**start（）：**启动线程，虚拟机**调用**该线程的**run（）**方法。

示例： 

```java
public class Demo {
    public static void main(String[] args){
        MyThread a=new MyThread("a"),b=new MyThread("b");
        a.start();b.start();
    }
}

public class MyThread extends Thread{
    @Override
    public void run(){
        for(int i=0;i<100;i++) System.out.println(getName()+":"+i);
    }

    public MyThread() {
    }

    public MyThread(String name) {
        super(name);
    }
}
```

运行结果：

![](https://i-blog.csdnimg.cn/blog_migrate/6c6fe7061901d392957567ffb4dda6c9.png)

**Thead类常用方法：**

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i12"><td><code><a href="../../java/lang/String.html" rel="nofollow">String</a></code></td><td><code><a href="../../java/lang/Thread.html#getName--" rel="nofollow">getName</a>()</code><p>返回此线程的名称。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/lang/Thread.html#setName-java.lang.String-" rel="nofollow">setName</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name)</code><p>将此线程的名称更改为等于参数 <code>name</code> 。</p></td></tr><tr><td><code>static <a href="../../java/lang/Thread.html" rel="nofollow">Thread</a></code></td><td><code><a href="../../java/lang/Thread.html#currentThread--" rel="nofollow">currentThread</a>()</code><p>返回对当前正在执行的线程对象的引用。</p></td></tr><tr><td><code>int</code></td><td><code><a href="../../java/lang/Thread.html#getPriority--" rel="nofollow">getPriority</a>()</code><p>返回此线程的优先级。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/lang/Thread.html#setPriority-int-" rel="nofollow">setPriority</a>(int&nbsp;newPriority)</code><p>更改此线程的优先级。</p></td></tr><tr><td><code>static void</code></td><td><code><a href="../../java/lang/Thread.html#sleep-long-" rel="nofollow">sleep</a>(long&nbsp;millis)</code><p>使当前正在执行的线程以指定的毫秒数暂停（暂时停止执行），具体取决于系统定时器和调度程序的精度和准确性。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/lang/Thread.html#join--" rel="nofollow">join</a>()</code><p>等待这个线程死亡。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/lang/Thread.html#setDaemon-boolean-" rel="nofollow">setDaemon</a>(boolean&nbsp;on)</code><p>将此线程标记为守护线程，当只剩守护线程运行时，java虚拟机将退出。</p></td></tr></tbody></table>
        

主线程设置名字：

```java
        Thread.currentThread().setName("主线程");
        System.out.println(Thread.currentThread().getName());
```

### 16.3 创建线程方法2:实现 Runnable 接口

> Runnable翻译：可运行的

**步骤：** 

1.  创建一个新的类，实现Runnable接口，重写run（）方法
2.  创建新类的对象a
3.  创建Thread类的对象b，**将a作为构造方法的参数1**
4.  启动线程

**这种办法更好，优点：**

（1）避免由于 Java 单继承带来的局限性

（2）逻辑和数据更好分离。通过实现 Runnable 接口的方法创建多线程更加适合**同一个资源被多段业务逻辑并行处理**的场景。在同一个资源被多个线程逻辑异步、并行处理的场景中，通过实现 Runnable 接口的方式设计多个 target 执行目标类可以更加方便、清晰地将执行逻辑和数据存储分离，更好地体现了面向对象的设计思想

**示例：**

```java
public class Demo {
    public static void main(String[] args){
        MyRunnable mr=new MyRunnable();
        Thread a=new Thread(mr,"a"),b=new Thread(mr,"b"),c=new Thread(mr);
        a.start();b.start();c.start();
    }
}

public class MyRunnable implements Runnable{
    @Override
    public void run(){
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+":"+i);
        }
    }
}
```

运行结果： 

 ![](https://i-blog.csdnimg.cn/blog_migrate/14b88f9b41d81a22b63d1e7c335ac953.png)

> **通过Lambda表达式实现Runnable接口来创建线程**
> 
> ```java
> package train;
> 
> public class Demo {
>     public static void main(String[] args) {
>         new Thread(()->{
>             System.out.println("hello");
>         }).start();
> 
> 
>         new Thread(()->{
>             Thread.currentThread().setName("a");
>             for(int i=0;i<100;i++) System.out.println(Thread.currentThread().getName()+":"+i);
>         }).start();
> 
> 
> 
>         new Thread(()->{
>             Thread.currentThread().setName("b");
>             for(int i=0;i<100;i++) System.out.println(Thread.currentThread().getName()+":"+i);
>         }).start();
>     }
> }
> ```

### 16.4 线程生命周期

![](https://i-blog.csdnimg.cn/blog_migrate/b02083126fb3210b0675db5ca27d8e45.png)

### 16.5  线程同步

多条语句共享数据时，多线程程序会出现**数据安全问题**。

#### 16.5.1 同步代码块

同步代码块简单来说就是将一段代码用一把锁给锁起来, 只有获得了这把锁的线程才访问, 并且同一时刻, 只有一个线程能持有这把锁, 这样就保证了同一时刻只有一个线程能执行被锁住的代码.

```java
    synchronized(同步对象) {
        //多条语句操作共享数据的代码 
    }
```

![](https://i-blog.csdnimg.cn/blog_migrate/ab73e2e0230d2cd1702f57ce5c588dbc.png)

 **同步代码块的好处：**解决了多线程的数据安全问题

**弊端：**线程很多时，每个线程都会去判断锁，这是很耗费资源和时间的。

#### 16.5.2 同步方法

**非静态同步方法的锁对象为this**。下面代码是相同功能的同步方法和同步代码块：

![](https://i-blog.csdnimg.cn/blog_migrate/a493eaf5e2c05c9a5154238b9d7827e3.png)

![](https://i-blog.csdnimg.cn/blog_migrate/17279cc36d37d52e034eda8019b1bba7.png)

 **静态同步方法的锁对象为：类名.class。**下面代码是相同功能的同步方法和同步代码块：

![](https://i-blog.csdnimg.cn/blog_migrate/58b637705e6d99393fcb7eace604d077.png)

![](https://i-blog.csdnimg.cn/blog_migrate/1f2eb653ceddc9e3dddebd77a107f145.png)

#### 16.5.3 线程安全的类

StringBuffer，Vector，Hashtable

若不考虑线程安全，分别替换为StringBuilder,ArrayList,HashMap.

#### 16.5.4 Lock锁

Lock提供比同步方法和代码块更广泛的锁定操作。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../../../java/util/concurrent/locks/Lock.html#lock--" rel="nofollow">lock</a>()</code><p>获得锁。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../../../java/util/concurrent/locks/Lock.html#unlock--" rel="nofollow">unlock</a>()</code><p>释放锁。</p></td></tr></tbody></table>
        

Lock是接口，ReentrantLock是它的实现类。

![](https://i-blog.csdnimg.cn/blog_migrate/9fa93063b746d94179ec7689a6a96416.png)

### 16.6 生产者消费者模式

一个十分经典的多线程协作模式。

 ![](https://i-blog.csdnimg.cn/blog_migrate/206797b1c4d22300dc4279b3c13711b5.png)

Object类的等待和唤醒方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../java/lang/Object.html#wait--" rel="nofollow">wait</a>()</code><p>导致当前线程等待，直到另一个线程调用该对象的 <a href="../../java/lang/Object.html#notify--" rel="nofollow"><code>notify()</code></a>方法或 <a href="../../java/lang/Object.html#notifyAll--" rel="nofollow"><code>notifyAll()</code></a>方法。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/lang/Object.html#notify--" rel="nofollow">notify</a>()</code><p>唤醒正在等待对象监视器的单个线程。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/lang/Object.html#notifyAll--" rel="nofollow">notifyAll</a>()</code><p>唤醒正在等待对象监视器的所有线程。</p></td></tr></tbody></table>
        

## 十七、 网络编程

### 17.1 概念 

**计算机网络：**_计算机网络_是指将地理位置不同的具有独立功能的多台计算机及其外部设备，通过通信线路连接起来，在网络操作系统，网络管理软件及网络通信协议的管理和协调下，实现资源共享和信息传递的计算机系统。

**网络编程：**指编写运行在多个设备（计算机）的程序，这些设备都通过网络连接起来。

![](https://i-blog.csdnimg.cn/blog_migrate/0c35471ff1b93099c48e14993d23cc52.png)

### 17.2 IP地址

![](https://i-blog.csdnimg.cn/blog_migrate/70b4322fea49e616898141b83eb1d171.png)

查看主机名和ip地址：控制面板--系统和安全-系统。

 **常用命令：**

ipconfig（查看计算机IP地址）

ping IP地址（测试连通性）

特殊IP地址：192.0.0.1是回送地址，可以代表本机地址，一般用来测试使用。

### 17.3 InetAddress 类

这个类表示**互联网协议(IP)地址。没有构造方法，**

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>static <a href="../../java/net/InetAddress.html" rel="nofollow">InetAddress</a></code></td><td><code><a href="../../java/net/InetAddress.html#getByName-java.lang.String-" rel="nofollow">getByName</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;host)</code><p>确定主机名称的IP地址。主机名称可以是ip地址，也可以是机器名称。</p></td></tr><tr><td><code><a href="../../java/lang/String.html" rel="nofollow">String</a></code></td><td><code><a href="../../java/net/InetAddress.html#getHostAddress--" rel="nofollow">getHostAddress</a>()</code><p>返回文本显示中的IP地址字符串。</p></td></tr><tr><td><code><a href="../../java/lang/String.html" rel="nofollow">String</a></code></td><td><code><a href="../../java/net/InetAddress.html#getHostName--" rel="nofollow">getHostName</a>()</code><p>获取此IP地址的主机名。</p></td></tr></tbody></table>
        

```java
        InetAddress administrator = InetAddress.getByName("diannaomingcheng");
        System.out.println(administrator.getHostAddress());
        System.out.println(administrator.getHostName());
```

### 17.4 端口

![](https://i-blog.csdnimg.cn/blog_migrate/1a35f306e0963cfed40f449992ef838e.png)

### 17.5 UDP协议接收发送数据

**概念：** 

 ![](https://i-blog.csdnimg.cn/blog_migrate/5c930c0340d465d91c253e573894bd10.png)

![](https://i-blog.csdnimg.cn/blog_migrate/3eb063addbced1042b69012a765dd089.png)

**发送数据的步骤：** 

![](https://i-blog.csdnimg.cn/blog_migrate/3232ba4c5fac86be9973b7ec7c4d1286.png)

**接收数据的步骤：**

 ![](https://i-blog.csdnimg.cn/blog_migrate/4d1d93e90cc40bd402cf90ec0598ac64.png)

 DatagramSocket构造方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>&nbsp;</code></td><td><code><a href="../../java/net/DatagramSocket.html#DatagramSocket--" rel="nofollow">DatagramSocket</a>()</code><p>构造数据报套接字并将其绑定到本地主机上的任何可用端口。</p></td></tr><tr><td><code>&nbsp;</code></td><td><code><a href="../../java/net/DatagramSocket.html#DatagramSocket-int-" rel="nofollow">DatagramSocket</a>(int&nbsp;port)</code><p>构造数据报套接字并将其绑定到本地主机上的指定端口。</p></td></tr></tbody></table>
        

一般方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i21"><td><code>void</code></td><td><code><a href="../../java/net/DatagramSocket.html#receive-java.net.DatagramPacket-" rel="nofollow">receive</a>(<a href="../../java/net/DatagramPacket.html" rel="nofollow">DatagramPacket</a>&nbsp;p)</code><p>从此套接字接收数据报包。</p></td></tr><tr id="i22"><td><code>void</code></td><td><code><a href="../../java/net/DatagramSocket.html#send-java.net.DatagramPacket-" rel="nofollow">send</a>(<a href="../../java/net/DatagramPacket.html" rel="nofollow">DatagramPacket</a>&nbsp;p)</code><p>从此套接字发送数据报包。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/net/DatagramSocket.html#close--" rel="nofollow">close</a>()</code><p>关闭此数据报套接字。</p></td></tr></tbody></table>
        

DatagramPacket构造方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/net/DatagramPacket.html#DatagramPacket-byte:A-int-java.net.InetAddress-int-" rel="nofollow">DatagramPacket</a>(byte[]&nbsp;buf, int&nbsp;length, <a href="../../java/net/InetAddress.html" rel="nofollow">InetAddress</a>&nbsp;address, int&nbsp;port)</code><p>构造用于<strong>发送</strong>长度的分组的数据报包 <code>length</code>指定主机上到指定的端口号。</p></td></tr><tr><td><code><a href="../../java/net/DatagramPacket.html#DatagramPacket-byte:A-int-" rel="nofollow">DatagramPacket</a>(byte[]&nbsp;buf, int&nbsp;length)</code><p>构造一个 <code>DatagramPacket</code>用于<strong>接收</strong>长度的数据包 <code>length</code> 。</p></td></tr></tbody></table>
        

一般方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>byte[]</code></td><td><code><a href="../../java/net/DatagramPacket.html#getData--" rel="nofollow">getData</a>()</code><p>返回数据缓冲区。</p></td></tr><tr><td><code>int</code></td><td><code><a href="../../java/net/DatagramPacket.html#getLength--" rel="nofollow">getLength</a>()</code><p>返回要发送的数据的长度或接收到的数据的长度。</p></td></tr></tbody></table>
        

**发送接收数据代码：**

```java
package udp_package;
//发送数据
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.nio.charset.StandardCharsets;

public class SendDemo {
    public static void main(String[] args) throws IOException {
        InetAddress ia = InetAddress.getByName("zhujiming");
        DatagramSocket ds=new DatagramSocket();
        byte []b="hello世界".getBytes();
        DatagramPacket dp=new DatagramPacket(b,b.length,ia,1234);
        ds.send(dp);
        ds.close();
    }
}
```

```java
package udp_package;
//接受数据
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;

public class ReceiveDemo {
    public static void main(String[] args) throws IOException {
        DatagramSocket ds=new DatagramSocket(1234);
        byte []b=new byte[1024];
        DatagramPacket dp=new DatagramPacket(b,1024);
        ds.receive(dp);
        System.out.println("接受到的数据："+new String(dp.getData(),0,dp.getLength()));
    }
}
```

先运行接收，再运行发送。

![](https://i-blog.csdnimg.cn/blog_migrate/c032a52673bb9422e1663ee155159799.png)

### 17.6 TCP协议

#### 17.6.1 概念

![](https://i-blog.csdnimg.cn/blog_migrate/c8ac78e38e8f34556097b48d2cc5737a.png)

客户端发送数据，服务端接受数据。

#### 17.6.2 发送数据

![](https://i-blog.csdnimg.cn/blog_migrate/c96a09044314a99d1a50148a23203b2d.png)

套接字是两台机器之间通讯的端点。

**客户端套接字类Socket方法：**

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/net/Socket.html#Socket-java.lang.String-int-" rel="nofollow">Socket</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;host, int&nbsp;port)</code><p>创建流套接字并将其连接到指定主机上的指定端口号。</p></td></tr><tr><td><code><a href="../../java/net/Socket.html#Socket-java.net.InetAddress-int-" rel="nofollow">Socket</a>(<a href="../../java/net/InetAddress.html" rel="nofollow">InetAddress</a>&nbsp;address, int&nbsp;port)</code><p>创建流套接字并将其连接到指定IP地址的指定端口号。</p></td></tr></tbody></table>
        

一般方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/io/OutputStream.html" rel="nofollow">OutputStream</a></code></td><td><code><a href="../../java/net/Socket.html#getOutputStream--" rel="nofollow">getOutputStream</a>()</code><p>返回此套接字的输出流。</p></td></tr><tr><td><code><a href="../../java/io/InputStream.html" rel="nofollow">InputStream</a></code></td><td><code><a href="../../java/net/Socket.html#getInputStream--" rel="nofollow">getInputStream</a>()</code><p>返回此套接字的输入流。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/net/Socket.html#shutdownOutput--" rel="nofollow">shutdownOutput</a>()</code><p>禁用此套接字的输出流。</p></td></tr></tbody></table>
        

**OutputStream类是所有输出字节流的超类：**

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#close--" rel="nofollow">close</a>()</code><p>关闭此输出流并释放与此流相关联的任何系统资源。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#flush--" rel="nofollow">flush</a>()</code><p>刷新此输出流并强制任何缓冲的输出字节被写出。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#write-byte:A-" rel="nofollow">write</a>(byte[]&nbsp;b)</code><p>将 <code>b.length</code>字节从指定的字节数组写入此输出流。</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../java/io/OutputStream.html#write-byte:A-int-int-" rel="nofollow">write</a>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code><p>从指定的字节数组写入 <code>len</code>个字节，从偏移 <code>off</code>开始输出到此输出流。</p></td></tr><tr><td><code>abstract void</code></td><td><code><a href="../../java/io/OutputStream.html#write-int-" rel="nofollow">write</a>(int&nbsp;b)</code><p>将指定的字节写入此输出流。</p></td></tr></tbody></table>
        

**OutputStream封装到BufferedWriter：**

字节输出流OutputStream转字符输出流OutputStreamWriter转缓冲字符输出流BufferedWriter。

这里s是Socket对象：

![](https://i-blog.csdnimg.cn/blog_migrate/abfe07e0033761f2557f728fed7a6af2.png)

```java
package tcp_package;
//客户端发送数据

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;

public class SendDemo {
    public static void main(String[] args) throws IOException {
        InetAddress ia=InetAddress.getByName("mingzi");
        Socket s=new Socket(ia,1234);
        OutputStream os=s.getOutputStream();    //这里就是IO流了，可以把字节输出流OutputStream转为缓冲字符输出流BufferedWriter，从而发送字符
        os.write("hello世界".getBytes());
        s.close();
    }
}
```

所谓_套接字_(Socket),就是对网络中不同主机上的应用进程之间进行双向通信的端点的抽象。 

#### 17.6.3 接受数据

![](https://i-blog.csdnimg.cn/blog_migrate/c7a61b73c5a078f52fe7782585b9fcb4.png)

**服务器套接字类ServerSocker方法：**

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/net/ServerSocket.html#ServerSocket-int-" rel="nofollow">ServerSocket</a>(int&nbsp;port)</code><p>创建绑定到指定端口的服务器套接字。</p></td></tr></tbody></table>
        

 ..

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/net/Socket.html" rel="nofollow">Socket</a></code></td><td><code><a href="../../java/net/ServerSocket.html#accept--" rel="nofollow">accept</a>()</code><p>侦听要连接到此套接字并接受它。</p></td></tr></tbody></table>
        

**InputStream是所有输入字节流类的超类：**

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>abstract int</code></td><td><code><a href="../../java/io/InputStream.html#read--" rel="nofollow">read</a>()</code><p>从输入流读取数据的下一个字节。</p></td></tr><tr><td><code>int</code></td><td><code><a href="../../java/io/InputStream.html#read-byte:A-" rel="nofollow">read</a>(byte[]&nbsp;b)</code><p>从输入流读取一些字节数，并将它们存储到缓冲区 <code>b，返回值为长度</code>&nbsp;。</p></td></tr><tr><td><code>int</code></td><td><code><a href="../../java/io/InputStream.html#read-byte:A-int-int-" rel="nofollow">read</a>(byte[]&nbsp;b, int&nbsp;off, int&nbsp;len)</code><p>从输入流读取最多 <code>len</code>字节的数据到一个字节数组。</p></td></tr></tbody></table>
        

**字节输入流InputStream封装到字符缓冲输入流BufferedWriter：**

这里s是Socket对象：

![](https://i-blog.csdnimg.cn/blog_migrate/fd811e99892386613e9d6c32b617f0c4.png)

 这样就能每次读取一行字符串，更方便。

**代码**

```java
package tcp_package;
//服务端接受数据

import java.io.IOException;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class ReceiveDemo {
    public static void main(String[] args) throws IOException {
        ServerSocket ss=new ServerSocket(1234);
        Socket s=ss.accept();
        InputStream is=s.getInputStream();
        byte[] b=new byte[1024];
        int len=is.read(b);
        System.out.println("data is:"+new String(b,0,len));
        ss.close();        //关ss就行了，因为s是从ss得到的。
    }
}
```

#### 17.6.4 练习，TCP键盘录入字符通讯

```java
package tcp_package;

import java.io.*;
import java.net.Socket;

public class ClientDemo{
    public static void main(String[] args) throws IOException {
        Socket s=new Socket("xx.xx.xx.xx",1234);
        BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        String line;
        while ((line=br.readLine())!=null){
            if(line.equals("886")) break;
            bw.write(line);
            bw.newLine();
            bw.flush();        //缓冲流别忘了刷新，不然发不出去
        }
        s.shutdowmOutput();
//shutdowmOutput（）代表停止发送数据，此处可加BufferedReader反馈代码，接收服务端传输成功的反馈
        s.close();        //s是bw的源头，关s就关了bw
        br.close();        
    }



}
```

```java
package tcp_package;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) throws IOException {
        ServerSocket ss=new ServerSocket(1234);
        Socket s=ss.accept();
        BufferedReader br=new BufferedReader(new InputStreamReader(s.getInputStream()));
        String line;
        while((line=br.readLine())!=null){
            System.out.println(line);
        }
        ss.close();
    }
}
```

#### 17.6.5 练习，服务器多线程接收文件

![](https://i-blog.csdnimg.cn/blog_migrate/8145e3ea90f5afea57e891c08e138c47.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/7f54a75321cde46fae7b74cb354f46d0.png)

![](https://i-blog.csdnimg.cn/blog_migrate/3eeaefdc45c76d738aac0e9386759d73.png)

## 十八、Lambda表达式

### 18.1 概念

 ![](https://i-blog.csdnimg.cn/blog_migrate/3fcbf37604b0063da8fdc69d3c1c54f3.png)

Lambda表达式是一个对象，必须有**上下文环境**，**作用是实现单方法的接口**。

上下文环境意思是能证明它是对象，例如让它处在方法或类的实参里，或者赋值给对象引用。

**注意事项：**

-   接口必须单方法。
-   Lambda

 **Lambda表达式****格式：**

```
(形参)->{方法内的代码块}
```

**可省略内容：** 

-   **形参类型、返回类型可以省略**。毕竟接口里也声明了类型，类型必须要么都写要么都省略。例如：

```java
public class Demo {
    public static void main(String[] args) {
        fun((a,b)->{    //Lambda形参类型、返回类型可以省略
            return a+b;
        });
    }
    public static void fun(Dog d){
        d.add(1,4);
    }
}

public interface Dog {    //单方法接口
    public int add(int a,int b);//只能有一个方法
}
```

-   如果只有一个参数，小括号可以省略。
-   如果代码句只有一条，大括号和分号可以省略。要么都省，**要么都不省略**。
-   若单语句是return，要么大括号、分号、return要么都省，**要么都不省略**。

单参数单语句省略示例： 

```java
public class Test {
    public static void main(String[] args) {
//Lambda表达式简化单方法接口实现类对象的创建过程
        fun((a,b)->{
            return a+b;
        });
//如果不用Lambda表达式，则要用下面的方式调用fun(Dog d)方法
        fun(new Dog() {
            @Override
            public int add(int a, int b) {
                return a+b;
            }
        });
    }
    public static void fun(Dog d){
        d.add(1,4);
    }
}
```

### 18.2 实现类、匿名内部类、Lambda线程代码对比

```java
        new Thread(()->{    //虚拟机根据上下文能推断出实现的接口是Runnable
            Thread.currentThread().setName("a");
            for(int i=0;i<100;i++) System.out.println(Thread.currentThread().getName()+":"+i);
        }).start();
```

![](https://i-blog.csdnimg.cn/blog_migrate/febd35ce56365128922dea8ab57bd63e.png)

可见Lambda表达式方法最简洁，匿名内部类名和方法名都省了。 

### 18.3 Lambda和匿名内部类区别

-   **接口：**Lambda只能是接口，匿名内部类可以是接口、抽象类、具体类。
-   **方法：**Lambda只能单方法，匿名内部类可以多方法。
-   **原理：**Lambda编译后字节码在运行时**动态生成**，匿名内部类编译后生成一个**字节码文件**。

## 十九、接口组成更新

java8后加入了默认方法、静态方法。java9后加入了私有方法。

### 19.1 接口中default默认方法

默认方法可被子类对象调用。

多态复习：接口不能初始化对象，只能接口引用指向实现类实例化对象，这时引用只能调用接口方法，实际执行的是实现类实现的对应方法。

默认方法不是抽象方法，实现类可以重写，也可以不重写。

```java
public interface Dog {
    public default void eat(){
        System.out.println("he");
    }
}
```

### 19.2 接口中静态方法

![](https://i-blog.csdnimg.cn/blog_migrate/6af9ad1857660f5da56cdab5a94a041f.png)

 接口中静态方法只能被接口名调用，不能被实现类对象调用。

假如类A实现了有同名静态方法的接口B、C，则A的对象分不清调用哪个接口的方法。

```java
public interface Dog {
    public static void eat(){
        System.out.println("he");
    }
}

public class Demo {
    public static void main(String[] args) {
        Dog.eat();

    }
}
```

### 19.3 接口中私有方法

起源：为了将接口中多个默认或静态方法中的共性方法抽离出来。

![](https://i-blog.csdnimg.cn/blog_migrate/6fdab8c9c0f6020cdb37026fe4dc2eb7.png)

 修饰符复习：私有方法权限最低，仅同类内可见。静态方法只能访问静态变量和方法，不能用this。

```java
public interface Dog {
    public static void eat(){    //静态方法只能访问静态变量和方法
        look();
    }
    public default void sleep(){        //非静态方法可以访问静态非静态成员
        look();
    }
    private static void look(){    //私有成员仅本类内可见
        System.out.println("look");
    }
}
```

## 二十、方法引用

### 20.1 概念

方法引用和Lambda都可以根据上下文推导。

**格式：**

```
引用类::不带括号的方法名
```

### **20.2 引用类的方法**

**引用Lambda中类的方法：**

```java
public class Demo {
    public static void main(String[] args) {
        fun((s)-> System.out.println(s));    //fruit
        fun(System.out::println);    //fruit        //根据上下文推导出标准输出流类的println方法
    }
    public static void fun(Dog dog){    //Dog是个接口
        dog.eat(" fruit");
    }
}
```

 **引用Lambda中类的方法：**

```java
        fun((s)->Integer.parseInt(s));    //字符串转数字，
        fun(Integer::parseInt);        //根据上下文推导Integer类的parseInt方法
```

**引用匿名内部类中类的方法：**

```java
        fun(new Dog() {
            @Override
            public void eat(String s) {
                System.out.println(s);
            }
        });
        fun(System.out::println);
```

### 20.3 引用对象

```java
public class Demo {
    public static void main(String[] args) {
        Dog dog=new Dog();        //Dog是类        
        fun(dog::eat);        引用对象的方法，实参为对象，形参是接口
    }
    public static void fun(Cat c){        //Cat是接口
        c.look("4346");
    }
}
```

### 20.4 引用构造器

![](https://i-blog.csdnimg.cn/blog_migrate/9849ef65cd4486e70c4577cfbab09308.png)

![](https://i-blog.csdnimg.cn/blog_migrate/964d83657e1d9b228bdb3e5e81fe4399.png)

## 二十一、函数式接口

### 21.1 概念 

函数式接口：**有且仅有一个抽象方法的接口。**

Java中函数式编程体现就是Lambda表达式。

函数式接口注解：**@FunctionalInterface**

**如果方法的返回值是函数式接口，可以使用Lambda表达式作为结果返回。**

**格式**： 函数式接口对象作为一个方法的形参，实参是Lambda表达式。

事实上，**JDK自带一些函数式接口**：函数式接口Supplier中get获取有返回值的数据，Predicate中test返回boolean型数据，Consumer中accept无返回值数据操作。

<table border="1" cellpadding="1" cellspacing="1"><tbody><tr><td>接口&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td><td>方法</td><td>作用</td><td>示例</td></tr><tr><td>Supplier</td><td>get，返回各类型的数据</td><td>选择</td><td>返回数组最大值</td></tr><tr><td>Function&nbsp;&nbsp;</td><td>apply，返回各类型数据</td><td>转换</td><td>数字字符串转换</td></tr><tr><td>Predicate</td><td>test，返回boolean型数据</td><td>判断</td><td>判断数字是否大于5</td></tr><tr><td>Consumer</td><td>accept，无返回值</td><td>处理</td><td>翻转字符串</td></tr><tr><td></td><td></td><td></td><td></td></tr></tbody></table>

### 21.2 函数式接口Supplier接口

-   [@FunctionalInterface](../../../java/lang/FunctionalInterface.html)
    public interface Supplier<T>
    

 作用：获取到生产出的数据

Supplier译作供应商，生产的数据类型由泛型指定。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../../java/util/function/Supplier.html" rel="nofollow">T</a></code></td><td><code><a href="../../../java/util/function/Supplier.html#get--" rel="nofollow">get</a>()</code><p>获得结果。</p></td></tr></tbody></table>
        

```java
public class Test {
    public static void main(String[] args) {
        // 定义一个int数组
        int[] arr = {19, 50, 28, 37, 46};
        // 调用getMax方法，方法的形参是函数式接口（单方法接口），
        // 实参Lambda表达式（接口方法的逻辑，相当于创建了一个Supplier对象）
        // 返回值是Lambda表达式的返回值，sup.get()
        int maxValue = getMax(() -> {
            int max = arr[0];
            for (int i = 1; i < arr.length; i++) {
                if (arr[i] > max) {
                    max = arr[i];
                }
            }
            return max;
        });
        System.out.println(maxValue);
    }

    /**
     * 返回一个int数组中的最大值
     * @param sup 生产者，是个函数式接口，实参是Lambda表达式（接口方法的逻辑，相当于一个Supplier对象）
     * @return int 最大值
     */
    private static int getMax(Supplier<Integer> sup) {
        return sup.get();
    }
}
```

### 21.3 函数式接口Consumer

-   [@FunctionalInterface](../../../java/lang/FunctionalInterface.html)
    public interface Consumer<T>
    

作用：对数据进行操作，无返回值。

Consumer是消费型接口，消费的数据类型由泛型指定。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../../java/util/function/Consumer.html#accept-T-" rel="nofollow">accept</a>(<a href="../../../java/util/function/Consumer.html" rel="nofollow">T</a>&nbsp;t)</code><p>对给定的参数执行此操作。</p></td></tr><tr><td><code>default <a href="../../../java/util/function/Consumer.html" rel="nofollow">Consumer</a>&lt;<a href="../../../java/util/function/Consumer.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/function/Consumer.html#andThen-java.util.function.Consumer-" rel="nofollow">andThen</a>(<a href="../../../java/util/function/Consumer.html" rel="nofollow">Consumer</a>&lt;? super <a href="../../../java/util/function/Consumer.html" rel="nofollow">T</a>&gt;&nbsp;after)</code><p>返回一个组合的 <code>Consumer</code> ，按顺序执行该操作，然后执行 <code>after</code>操作。</p></td></tr></tbody></table>
        

 a.andThen(b).accept(t);相当于a.accept(t);b.accept(t);

![](https://i-blog.csdnimg.cn/blog_migrate/25ce27f33e89ebfd2d279827f5cb6039.png)

### 21.4 函数式接口Predicate

-   [@FunctionalInterface](../../../java/lang/FunctionalInterface.html)
    public interface Predicate<T>
    

 作用：判断参数是否满足条件。

译作谓词，谓语。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>boolean</code></td><td><code><a href="../../../java/util/function/Predicate.html#test-T-" rel="nofollow">test</a>(<a href="../../../java/util/function/Predicate.html" rel="nofollow">T</a>&nbsp;t)</code><p>在给定的参数上评估这个谓词。</p></td></tr><tr><td><code>default <a href="../../../java/util/function/Predicate.html" rel="nofollow">Predicate</a>&lt;<a href="../../../java/util/function/Predicate.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/function/Predicate.html#and-java.util.function.Predicate-" rel="nofollow">and</a>(<a href="../../../java/util/function/Predicate.html" rel="nofollow">Predicate</a>&lt;? super <a href="../../../java/util/function/Predicate.html" rel="nofollow">T</a>&gt;&nbsp;other)</code><p>返回一个组合的谓词，表示该谓词与另一个谓词的短路逻辑AND。与。</p></td></tr><tr><td><code>default <a href="../../../java/util/function/Predicate.html" rel="nofollow">Predicate</a>&lt;<a href="../../../java/util/function/Predicate.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/function/Predicate.html#negate--" rel="nofollow">negate</a>()</code><p>返回表示此谓词的逻辑否定的谓词。非。</p></td></tr><tr><td><code>default <a href="../../../java/util/function/Predicate.html" rel="nofollow">Predicate</a>&lt;<a href="../../../java/util/function/Predicate.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/function/Predicate.html#or-java.util.function.Predicate-" rel="nofollow">or</a>(<a href="../../../java/util/function/Predicate.html" rel="nofollow">Predicate</a>&lt;? super <a href="../../../java/util/function/Predicate.html" rel="nofollow">T</a>&gt;&nbsp;other)</code><p>返回一个组合的谓词，表示该谓词与另一个谓词的短路逻辑或。或。</p></td></tr></tbody></table>
        

方法的形参Predicate对象是Lambda参数。 

```java
public class Demo {
    public static void main(String[] args) {
        boolean b = fun("hello", s -> s.length() > 5, s -> s.length() <100);
    }

    private static boolean fun(String s, Predicate<String> p1, Predicate<String> p2) {
        return p1.and(p2).test(s);
    }
    private static boolean fun(String s, Predicate<String> p) {
        return p.negate().test(s);
    }
}
```

### 21.5 函数式接口Function

-   [@FunctionalInterface](../../../java/lang/FunctionalInterface.html)
    public interface Function<T,R>
    

作用：用于对参数进行处理、转换，然后返回一个新值。

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../../java/util/function/Function.html" rel="nofollow">R</a></code></td><td><code><a href="../../../java/util/function/Function.html#apply-T-" rel="nofollow">apply</a>(<a href="../../../java/util/function/Function.html" rel="nofollow">T</a>&nbsp;t)</code><p>将此函数应用于给定的参数。</p></td></tr><tr><td><code>default &lt;V&gt;&nbsp;<a href="../../../java/util/function/Function.html" rel="nofollow">Function</a>&lt;<a href="../../../java/util/function/Function.html" rel="nofollow">T</a>,V&gt;</code></td><td><code><a href="../../../java/util/function/Function.html#andThen-java.util.function.Function-" rel="nofollow">andThen</a>(<a href="../../../java/util/function/Function.html" rel="nofollow">Function</a>&lt;? super <a href="../../../java/util/function/Function.html" rel="nofollow">R</a>,? extends V&gt;&nbsp;after)</code><p>返回一个组合函数，首先将该函数应用于其输入，然后将 <code>after</code>函数应用于结果。</p></td></tr></tbody></table>
        

![](https://i-blog.csdnimg.cn/blog_migrate/68656a06452cab3166eca7a69f56d587.png)

![](https://i-blog.csdnimg.cn/blog_migrate/43fa923342615a9241facbae3509590b.png)

```java
public class Demo {
    public static void main(String[] args) {
        String s="小明，33";
        fun(s,s1->s1.split("，")[1],s1->Integer.parseInt(s1),i->i+70);
    }
    //先分割，再转数字，再加70
    private static void fun(String s, Function<String,String> fun1,Function<String,Integer> fun2,Function<Integer,Integer> fun3){

        int i=fun1.andThen(fun2).andThen(fun3).apply(s);//fun1的结果给fun2，fun2的结果给fun3
        System.out.println(i);
    }
}
```

## 二十二、Stream流

Stream流真正把函数式编程风格引用java中。

![](https://i-blog.csdnimg.cn/blog_migrate/c7a2f20fbc07f48f4279627a8f50b96f.png)

**Stream流过程：**

![](https://i-blog.csdnimg.cn/blog_migrate/11f54cd1fbce3c7590d1ee8066176957.png)

filter()和forEach()参数都是Lambda或方法引用。

### **22.1 Stream流生成：**

![](https://i-blog.csdnimg.cn/blog_migrate/5080136aaddf098e3c88ba6e32fcc1c1.png)

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i29"><td><code>static &lt;T&gt;&nbsp;<a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;T&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#of-T-" rel="nofollow">of</a>(T&nbsp;t)</code><p>返回包含单个元素的顺序 <code>Stream</code> 。</p></td></tr></tbody></table>
        

代码：![](https://i-blog.csdnimg.cn/blog_migrate/ecff99457797bb4508c356eab124c45e.png)

### 22.2 Stream流中间操作

#### 22.2.1 概述 

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i9"><td><code><a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;<a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#filter-java.util.function.Predicate-" rel="nofollow">filter</a>(<a href="../../../java/util/function/Predicate.html" rel="nofollow">Predicate</a>&lt;? super <a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;&nbsp;predicate)</code><p>返回由与此给定谓词匹配的此流的元素组成的流。</p></td></tr><tr><td><code><a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;<a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#limit-long-" rel="nofollow">limit</a>(long&nbsp;maxSize)</code><p>返回由此流的元素组成的流，截短长度不能超过 <code>maxSize</code> 。</p></td></tr><tr><td><code><a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;<a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#skip-long-" rel="nofollow">skip</a>(long&nbsp;n)</code><p>在丢弃流的第一个 <code>n</code>元素后，返回由该流的 <code>n</code>元素组成的流。</p></td></tr><tr><td><code>static &lt;T&gt;&nbsp;<a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;T&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#concat-java.util.stream.Stream-java.util.stream.Stream-" rel="nofollow">concat</a>(<a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;? extends T&gt;&nbsp;a, <a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;? extends T&gt;&nbsp;b)</code><p>创建一个懒惰连接的流，其元素是第一个流的所有元素，后跟第二个流的所有元素。</p></td></tr><tr><td><code><a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;<a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#distinct--" rel="nofollow">distinct</a>()</code><p>返回由该流的不同元素（根据 <a href="../../../java/lang/Object.html#equals-java.lang.Object-" rel="nofollow"><code>Object.equals(Object)</code></a> ）组成的流。</p></td></tr><tr><td><code><a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;<a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#sorted--" rel="nofollow">sorted</a>()</code><p>返回由此流的元素组成的流，根据自然顺序排序。</p></td></tr><tr><td><code><a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;<a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#sorted-java.util.Comparator-" rel="nofollow">sorted</a>(<a href="../../../java/util/Comparator.html" rel="nofollow">Comparator</a>&lt;? super <a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;&nbsp;comparator)</code><p>返回由该流的元素组成的流，根据提供的 <code>Comparator</code>进行排序。</p></td></tr><tr><td><code>&lt;R&gt;&nbsp;<a href="../../../java/util/stream/Stream.html" rel="nofollow">Stream</a>&lt;R&gt;</code></td><td><code><a href="../../../java/util/stream/Stream.html#map-java.util.function.Function-" rel="nofollow">map</a>(<a href="../../../java/util/function/Function.html" rel="nofollow">Function</a>&lt;? super <a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>,? extends R&gt;&nbsp;mapper)</code><p>返回由给定函数应用于此流的元素的结果组成的流。</p></td></tr><tr><td><code><a href="../../../java/util/stream/IntStream.html" rel="nofollow">IntStream</a></code></td><td><code><a href="../../../java/util/stream/Stream.html#mapToInt-java.util.function.ToIntFunction-" rel="nofollow">mapToInt</a>(<a href="../../../java/util/function/ToIntFunction.html" rel="nofollow">ToIntFunction</a>&lt;? super <a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>&gt;&nbsp;mapper)</code><p>返回一个 <code>IntStream</code> ，其中包含将给定函数应用于此流的元素的结果。</p></td></tr></tbody></table>
        

**filter**

  filter 方法用于通过设置的条件过滤出元素。以下代码片段**使用 filter 方法过滤掉空字符串**，打印非空字符串。**filter的参数是Lambda，Lambda参数是list的每个元素，返回值是Boolean，为true时留下**

```java
        List<String>list = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
        //forEach终结后，原list不变，处理后的list遍历输出
        list.stream().filter(item -> !item.isEmpty()).forEach(System.out::println);
```

 ![](https://i-blog.csdnimg.cn/blog_migrate/e7acdf876130908deb669b5e398b5084.png)

 **skip&limit**

![](https://i-blog.csdnimg.cn/blog_migrate/d1131ae3deff8a70645bb3f5e4fa8042.png)

 **concat和distinct**

![](https://i-blog.csdnimg.cn/blog_migrate/77c6cfec0e18b1b5ed28b8834cc31794.png)

**sorted比较器**

**sorted()**

```java
list.stream().sorted(参数是Lambda，Lambda参数是list的两个元素，返回值>0是升序，返回值<0是降序)
```

先按字母序再按长度排序：

```java
        List<String> list = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
        //forEach终结后，原list不变，处理后的list遍历输出
        list=list.stream().sorted((item1,item2)->{
            if(item1.compareTo(item2)!=0) return item1.compareTo(item2);
            else return item1.length()-item2.length();
        }).collect(Collectors.toList());
        System.out.println(list);
    }
```

输出：\[, , abc, abcd, bc, efg, jkl\]

 **map**

 中间操作**map()**用法和filter类似，**map的参数是Lambda，Lambda参数是list的每个元素，返回值是加工后的list元素。**

```java
        List<String>list = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
        //collect收集后原list不变，处理后的list收集成返回值
        list=list.stream().map(item->item.toUpperCase()).collect(Collectors.toList());
        System.out.println(list);
```

![](https://i-blog.csdnimg.cn/blog_migrate/267ee2fdb9b7a1cf53b4d327bf70d7d4.png)

 **mapToInt**

![](https://i-blog.csdnimg.cn/blog_migrate/c8c3682420b27b7ee03e5e525ba460e3.png)

 IntStream是由Integer元素组成的流，可以取和、平均数、排序、skip、limit、conunt、forEach等。

#### 22.2.2 map和filter区分

filter是满足条件的留下，是对原数组的过滤；map则是对原数组的加工，映射成一对一映射的新数组。

说人话就是改变了了长度了用filter,没改变长度,只是对某一个或者几个做改变用map

### 22.3 Stream流终结

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>long</code></td><td><code><a href="../../../java/util/stream/IntStream.html#count--" rel="nofollow">count</a>()</code><p>返回此流中的元素数</p></td></tr><tr><td><code>void</code></td><td><code><a href="../../../java/util/stream/IntStream.html#forEach-java.util.function.IntConsumer-" rel="nofollow">forEach</a>(<a href="../../../java/util/function/IntConsumer.html" rel="nofollow">IntConsumer</a>&nbsp;action)</code><p>对此流的每个元素执行操作。</p></td></tr></tbody></table>
        

### 22.4 Stream流收集

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>&lt;R,A&gt;&nbsp;R</code></td><td><code><a href="../../../java/util/stream/Stream.html#collect-java.util.stream.Collector-" rel="nofollow">collect</a>(<a href="../../../java/util/stream/Collector.html" rel="nofollow">Collector</a>&lt;? super <a href="../../../java/util/stream/Stream.html" rel="nofollow">T</a>,A,R&gt;&nbsp;collector)</code><p>使用 <a href="package-summary.html#MutableReduction" rel="nofollow">Collector</a>对此流的元素执行 <a href="package-summary.html#MutableReduction" rel="nofollow">mutable reduction</a> <code>Collector</code> 。</p></td></tr></tbody></table>
        

参数**Collector**对象通过工具类**Collections**返回值得到：

![](https://i-blog.csdnimg.cn/blog_migrate/1d60d386299eca08a30a2512c5e645b9.png)

 示例：

![](https://i-blog.csdnimg.cn/blog_migrate/3a5bfd14425452ebd732d0f4715e901f.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/6bf384e318084757c310884185568f50.png)

![](https://i-blog.csdnimg.cn/blog_migrate/dd948a0ffc42fac4ba06bc5d41508563.png)

## 二十三、 反射

### 23.1 类加载和类加载器 

![](https://i-blog.csdnimg.cn/blog_migrate/81f79dc0581079dc8cd6d4e77421f397.png)

![](https://i-blog.csdnimg.cn/blog_migrate/fcd3d1ececf294dfc60b2536fb808caa.png)

类加载器ClassLoader

![](https://i-blog.csdnimg.cn/blog_migrate/50f259d89691be8b4e931795bd3406b7.png)

ClassLoader：负责加载类的对象。

内置类加载器：

![](https://i-blog.csdnimg.cn/blog_migrate/49375b2497aae8a8a98acdde9ccf218d.png)

 **ClassLoader的方法：** 

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i19"><td><code>static <a href="../../java/lang/ClassLoader.html" rel="nofollow">ClassLoader</a></code></td><td><code><a href="../../java/lang/ClassLoader.html#getSystemClassLoader--" rel="nofollow">getSystemClassLoader</a>()</code><p>返回用于委派的系统类加载器。</p></td></tr><tr><td><code><a href="../../java/lang/ClassLoader.html" rel="nofollow">ClassLoader</a></code></td><td><code><a href="../../java/lang/ClassLoader.html#getParent--" rel="nofollow">getParent</a>()</code><p>返回父类加载器进行委派。</p></td></tr></tbody></table>
        

![](https://i-blog.csdnimg.cn/blog_migrate/ba167da3e35f87b09cfe4bbd7cdf6a77.png)

### 23.2 反射概述 

**反射**就是把Java类中的各个成分映射成一个个的Java对象。

即在运行状态中，对于任意一个类，都能够知道这个类的所以属性和方法；对于任意一个对象，都能调用它的任意一个方法和属性。这种动态获取信息及动态调用对象方法的功能叫Java的**反射机制**。 

**反射机制有什么用？**

通过java语言中的反射机制可以操作字节码文件（可以读和修改[字节码](https://so.csdn.net/so/search?q=%E5%AD%97%E8%8A%82%E7%A0%81&spm=1001.2101.3001.7020 "字节码")文件，即xxx.class文件）  
通过反射机制可以操作代码片段。（class文件。）

 **构造方法、成员变量、方法对象取消访问检查可以访问私有成员：**

![](https://i-blog.csdnimg.cn/blog_migrate/b2cd8b37c6fa0724a6ac4bc7e9c1781e.png)

反射可以越过泛型检查，例如在ArrayList<Integer>中添加字符串： 

 ![](https://i-blog.csdnimg.cn/blog_migrate/32142a4144088d6d31862f35a510a673.png)

### 23.3 三种获取Class类的对象方法

Class类的对象：该类的字节码文件对象。

同一个类的字节码文件对象永远是相等的。

![](https://i-blog.csdnimg.cn/blog_migrate/57ff5e67567f13c0a60650ce38006879.png)

```java
    public static void main(String[] args) throws ClassNotFoundException {
        Class<Dog> c1=Dog.class;        //方法1：类的class属性
        Dog d=new Dog();
        Class<? extends Dog> c2=d.getClass();        //方法2：对象的getClass方法
        Class<?> c3= Class.forName("train.Dog");    //方法3：Class类的静态方法forName
        System.out.println(c1); //class train.Dog
        System.out.println(c1==c2&&c1==c3); //true
    }
```

Class类的引用也可以不加泛型：

```java
Class c1=Dog.class;
Class c2=d.getClass();
Class c3= Class.forName("train.Dog");
```

### 23.4 反射获取构造方法并实例化

Class类的方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../java/lang/reflect/Constructor.html" rel="nofollow">Constructor</a>&lt;<a href="../../java/lang/Class.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../java/lang/Class.html#getConstructor-java.lang.Class...-" rel="nofollow">getConstructor</a>(<a href="../../java/lang/Class.html" rel="nofollow">类</a>&lt;?&gt;...&nbsp;parameterTypes)</code><p>返回单个公共构造方法对象。</p></td></tr><tr><td><code><a href="../../java/lang/reflect/Constructor.html" rel="nofollow">Constructor</a>&lt;<a href="../../java/lang/Class.html" rel="nofollow">T</a>&gt;</code></td><td><code><a href="../../java/lang/Class.html#getDeclaredConstructor-java.lang.Class...-" rel="nofollow">getDeclaredConstructor</a>(<a href="../../java/lang/Class.html" rel="nofollow">类</a>&lt;?&gt;...&nbsp;parameterTypes)</code><p>返回单个构造方法对象。</p></td></tr><tr id="i15"><td><code><a href="../../java/lang/reflect/Constructor.html" rel="nofollow">Constructor</a>&lt;?&gt;[]</code></td><td><code><a href="../../java/lang/Class.html#getConstructors--" rel="nofollow">getConstructors</a>()</code><p>返回所有公共构造方法对象的数组。</p></td></tr><tr><td><code><a href="../../java/lang/reflect/Constructor.html" rel="nofollow">Constructor</a>&lt;?&gt;[]</code></td><td><code><a href="../../java/lang/Class.html#getDeclaredConstructors--" rel="nofollow">getDeclaredConstructors</a>()</code><p>返回所有构造方法对象的数组。</p></td></tr><tr><td><code><a href="../../java/lang/Class.html" rel="nofollow">T</a></code></td><td><code><a href="../../java/lang/Class.html#newInstance--" rel="nofollow">newInstance</a>()</code><p>调用类的指定构造方法，完成构造方法的对象创建。</p></td></tr></tbody></table>
        

Constructor译作构造方法，构造器。

Class.newInstance() 只能够调用无参的构造函数，即默认的构造函数；   
Constructor.newInstance() 可以根据传入的参数，调用任意构造函数。 

**构造方法、成员变量、方法对象取消访问检查可以访问私有成员：**

![](https://i-blog.csdnimg.cn/blog_migrate/b2cd8b37c6fa0724a6ac4bc7e9c1781e.png)

 **获取所有构造方法的对象：**

```java
    public static void main(String[] args) throws ClassNotFoundException {
        Class<?> c= Class.forName("train.Dog");
        Constructor<?>[] cons = c.getDeclaredConstructors();
        for(Constructor<?> con:cons){
            System.out.println(con);
        }
    }
```

![](https://i-blog.csdnimg.cn/blog_migrate/b8845e730f0127f84b7ee91727017948.png)

 **获取单个构造方法的对象：**

无参：

```java
        Class<?> c= Class.forName("train.Dog");
        Constructor<?> con=c.getDeclaredConstructor();    //获取单个构造方法对象
        Object obj = con.newInstance();    //构造方法对象实例化，会调用无参构造方法
        System.out.println(obj);    //重写Dog类的to_String方法可更直观。
```

带参：

```java
        Class<?> c= Class.forName("train.Dog");
        Constructor<?> con=c.getConstructor(String.class,int.class);
        Object obj = con.newInstance("wangcai",32);
        System.out.println(obj);
```

### 23.5 反射获取成员变量并赋值

Class对象获取成员变量的方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i31"><td><code><a href="../../java/lang/reflect/Field.html" rel="nofollow">Field</a></code></td><td><code><a href="../../java/lang/Class.html#getField-java.lang.String-" rel="nofollow">getField</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name)</code><p>返回一个 <code>Field</code>对象，它反映此表示的类或接口的指定公共成员字段 <code>类</code>对象。返回一个共有成员变量。</p></td></tr><tr id="i32"><td><code><a href="../../java/lang/reflect/Field.html" rel="nofollow">Field</a>[]</code></td><td><code><a href="../../java/lang/Class.html#getFields--" rel="nofollow">getFields</a>()</code><p>返回包含一个数组 <code>Field</code>对象反射由此表示的类或接口的所有可访问的公共字段 <code>类</code>对象。</p></td></tr><tr><td><code><a href="../../java/lang/reflect/Field.html" rel="nofollow">Field</a></code></td><td><code><a href="../../java/lang/Class.html#getDeclaredField-java.lang.String-" rel="nofollow">getDeclaredField</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name)</code><p>返回一个 <code>Field</code>对象，它反映此表示的类或接口的指定已声明字段 <code>类</code>对象。</p></td></tr><tr><td><code><a href="../../java/lang/reflect/Field.html" rel="nofollow">Field</a>[]</code></td><td><code><a href="../../java/lang/Class.html#getDeclaredFields--" rel="nofollow">getDeclaredFields</a>()</code><p>返回的数组 <code>Field</code>对象反映此表示的类或接口声明的所有字段 <code>类</code>对象。</p></td></tr></tbody></table>
        

Field是字段，成员变量属于字段。

Field类的方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code>void</code></td><td><code><a href="../../../java/lang/reflect/Field.html#set-java.lang.Object-java.lang.Object-" rel="nofollow">set</a>(<a href="../../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;obj, <a href="../../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;value)</code><p>给obj对象（构造方法对象）的成员变量赋值为value。</p></td></tr></tbody></table>
        

**获取成员变量对象并赋值：**

```java
//        1.获取构造方法对象并实例化
        Dog dog=new Dog();
        Class<? extends Dog> c = dog.getClass();
        Constructor<?> con=c.getConstructor();
        Object obj = con.newInstance();
//        2.获取成员变量对象
        Field field = c.getField("name");
//        3.通过成员变量对象的方法set，给构造方法对象赋值
        field.set(obj,"旺财");
        System.out.println(obj);    //Dog{age=0, name='旺财'}
        System.out.println(dog.name);   //null
```

### 23.6 获取成员方法对象并调用成员方法

Class对象获取成员方法的方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i36"><td><code><a href="../../java/lang/Class.html#getDeclaredMethods--" rel="nofollow">Method</a></code></td><td><code><a href="../../java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-" rel="nofollow">getMethod</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name, <a href="../../java/lang/Class.html" rel="nofollow">类</a>&lt;?&gt;...&nbsp;parameterTypes)</code><p>返回一个 <code>方法</code>对象，它反映此表示的类或接口的指定公共成员方法 <code>类</code>对象。</p></td></tr><tr id="i37"><td><code><a href="../../java/lang/Class.html#getDeclaredMethods--" rel="nofollow">Method</a>[]</code></td><td><code><a href="../../java/lang/Class.html#getMethods--" rel="nofollow">getMethods</a>()</code><p>返回包含一个数组 <code>方法</code>对象反射由此表示的类或接口的所有公共方法 <code>类</code>对象，<strong>包括那些由类或接口和那些从超类和超接口继承的声明。</strong></p></td></tr><tr><td><code><a href="../../java/lang/Class.html#getDeclaredMethods--" rel="nofollow">Method</a></code></td><td><code><a href="../../java/lang/Class.html#getDeclaredMethod-java.lang.String-java.lang.Class...-" rel="nofollow">getDeclaredMethod</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;name, <a href="../../java/lang/Class.html" rel="nofollow">类</a>&lt;?&gt;...&nbsp;parameterTypes)</code><p>返回一个 <code>方法</code>对象，它反映此表示的类或接口的指定声明的方法 <code>类</code>对象。</p></td></tr><tr><td><code><a href="../../java/lang/Class.html#getDeclaredMethods--" rel="nofollow">Method</a>[]</code></td><td><code><a href="../../java/lang/Class.html#getDeclaredMethods--" rel="nofollow">getDeclaredMethods</a>()</code><p>返回包含一个数组 <code>方法</code>对象反射的类或接口的所有声明的方法，通过此表示 <code>类</code>对象，包括公共，保护，默认（包）访问和私有方法，但不包括继承的方法。</p></td></tr></tbody></table>
        

Method类的方法：

-   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr><td><code><a href="../../../java/lang/Object.html" rel="nofollow">Object</a></code></td><td><code><a href="../../../java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-" rel="nofollow">invoke</a>(<a href="../../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;obj, <a href="../../../java/lang/Object.html" rel="nofollow">Object</a>...&nbsp;args)</code><p>在具有指定参数的 <code>方法</code>对象上调用此 <code>方法</code>对象表示的底层方法。</p></td></tr></tbody></table>
        

**获取成员变量对象并调用：**

```java
//        1.获取构造方法对象并实例化
        Class<?> c= Class.forName("train.Dog");
        Constructor<?> con=c.getConstructor();
        Object obj = con.newInstance();
//        2.获取成员方法对象
        Method eat = c.getMethod("eat");
//        3.通过成员方法对象的invoke方法，调用构造方法对象的成员方法
//无参无返回值方法
        eat.invoke(obj);
//带参有返回值方法
        Object sucess= eat.invoke(obj,"food");
        System.out.println((boolean)sucess);
```

### 23.7 Properties和反射结合

Properties类在特殊操作流那里有细讲。

![](https://i-blog.csdnimg.cn/blog_migrate/7ea6e88d47b3a5e87f0f562cd43647a1.png)

## 二十四、模块化

![](https://i-blog.csdnimg.cn/blog_migrate/6b1052a57352a199d7602026079c3ecc.png)

### 24.1 不同模块间访问类：

![](https://i-blog.csdnimg.cn/blog_migrate/dedda2921c743c0781e480e821e51e85.png)

### 24.2 模块服务 

 ![](https://i-blog.csdnimg.cn/blog_migrate/5cee5d7bde6ad1da3b5a0ff689790695.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/6a69cb9b9665a4a7d0b8c184e829bf18.png)

 ![](https://i-blog.csdnimg.cn/blog_migrate/04439c73b9a54bd5757ce499af097404.png)

## 二十五、XML

### 25.1 概念

 ![](https://i-blog.csdnimg.cn/blog_migrate/666e9226d49aedfd97f373c7b3a46ea8.png)

**示例：**

![](https://i-blog.csdnimg.cn/blog_migrate/10fc656e77c3960d3cfedee0c02daa8f.png)

**特点和使用场景**

![](https://i-blog.csdnimg.cn/blog_migrate/aa2e668216545fbc260c7e58558630a7.png)

### 25.2 语法规则

**文档声明：**

![](https://i-blog.csdnimg.cn/blog_migrate/0a276b5fe08aca4c0930eb7787409671.png)

 **标签（元素）规则跟HTML类似：**

![](https://i-blog.csdnimg.cn/blog_migrate/ed506cc8621b36a1ecc1d697bcf54aa4.png)

注释、特殊字符、CDATA区：

![](https://i-blog.csdnimg.cn/blog_migrate/aa6ac044dc6656122166bc19516ff8f5.png)

 CDATA区可以任意写文本而不用担心冲突的发生，输入CD加回车能快速打出本语句。

### 25.3 文档约束

![](https://i-blog.csdnimg.cn/blog_migrate/c528e4492d43946bc30b1f14a0612a13.png)

**文档约束的分类：DTD和schema**

**DTD约束步骤** 

![](https://i-blog.csdnimg.cn/blog_migrate/8b3a8021bb5e23b4becd59bb53260cd2.png)

 **示例：**

![](https://i-blog.csdnimg.cn/blog_migrate/c119263d305238ee54139dbdc79e86cc.png)

 作用和问题：

![](https://i-blog.csdnimg.cn/blog_migrate/0a5fcdec3125cae481433bfb850dae74.png)

 **schema约束：**

![](https://i-blog.csdnimg.cn/blog_migrate/1ece313c8770941777275f3ffcd56678.png)