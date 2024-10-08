> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[一、基本介绍](#%E4%B8%80%E3%80%81%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D)

[二、环境准备](#%E4%BA%8C%E3%80%81%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)

[2.1 准备字节码文件](#2.1%20%E5%87%86%E5%A4%87%E5%AD%97%E8%8A%82%E7%A0%81%E6%96%87%E4%BB%B6)

[2.2 打开十六进制的字节码文件](#2.2%20%E6%89%93%E5%BC%80%E5%8D%81%E5%85%AD%E8%BF%9B%E5%88%B6%E7%9A%84%E5%AD%97%E8%8A%82%E7%A0%81%E6%96%87%E4%BB%B6%C2%A0) 

[2.3 分析字节码文件：javap命令](#2.3%20%E5%88%86%E6%9E%90%E5%AD%97%E8%8A%82%E7%A0%81%E6%96%87%E4%BB%B6%EF%BC%9Ajavap%E5%91%BD%E4%BB%A4)

[三、第一个基础单位：魔数和版本号](#%E4%B8%89%E3%80%81%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%9F%BA%E7%A1%80%E5%8D%95%E4%BD%8D%EF%BC%9A%E9%AD%94%E6%95%B0%E5%92%8C%E7%89%88%E6%9C%AC%E5%8F%B7%C2%A0) 

[四、常量池：字面量和符号引用](#%E5%9B%9B%E3%80%81%E5%B8%B8%E9%87%8F%E6%B1%A0%EF%BC%9A%E5%AD%97%E9%9D%A2%E9%87%8F%E5%92%8C%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8)

[4.1 基本介绍](#4.1%20%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D%C2%A0) 

[4.2 验证-常量项数量](#4.2%20%E9%AA%8C%E8%AF%81-%E5%B8%B8%E9%87%8F%E9%A1%B9%E6%95%B0%E9%87%8F)

[4.3 验证-第一个常量项：类中方法的符号引用](#4.3%20%E9%AA%8C%E8%AF%81-%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%B8%B8%E9%87%8F%E9%A1%B9%EF%BC%9A%E7%B1%BB%E4%B8%AD%E6%96%B9%E6%B3%95%E7%9A%84%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8)

[4.3.1 验证十六进制的字节码文件](#4.3.1%C2%A0%E9%AA%8C%E8%AF%81%E5%8D%81%E5%85%AD%E8%BF%9B%E5%88%B6%E7%9A%84%E5%AD%97%E8%8A%82%E7%A0%81%E6%96%87%E4%BB%B6)

[4.3.2 分析字节码文件：javap命令](#4.3.2%C2%A0%E5%88%86%E6%9E%90%E5%AD%97%E8%8A%82%E7%A0%81%E6%96%87%E4%BB%B6%EF%BC%9Ajavap%E5%91%BD%E4%BB%A4)

[4.4 验证-第二个常量项](#4.4%20%E9%AA%8C%E8%AF%81-%E7%AC%AC%E4%BA%8C%E4%B8%AA%E5%B8%B8%E9%87%8F%E9%A1%B9)

[4.5 扩展：所有常量项的标志位](#4.5%20%E6%89%A9%E5%B1%95%EF%BC%9A%E6%89%80%E6%9C%89%E5%B8%B8%E9%87%8F%E9%A1%B9%E7%9A%84%E6%A0%87%E5%BF%97%E4%BD%8D)

[7：类或接口的符号引用：Class](#7%EF%BC%9A%E7%B1%BB%E6%88%96%E6%8E%A5%E5%8F%A3%E7%9A%84%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8%EF%BC%9AClass)

[9：字段的符号引用：Fieldref](#9%EF%BC%9A%E5%AD%97%E6%AE%B5%E7%9A%84%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8%EF%BC%9AFieldref)

[10：方法的符号引用：Methodref](#10%EF%BC%9A%E6%96%B9%E6%B3%95%E7%9A%84%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8%EF%BC%9AMethodref)

[11：接口方法的符号引用：InterfaceMethodref](#11%EF%BC%9A%E6%8E%A5%E5%8F%A3%E6%96%B9%E6%B3%95%E7%9A%84%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8%EF%BC%9AInterfaceMethodref)

[8：字符串常量的符号引用：String](#8%EF%BC%9A%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%B8%B8%E9%87%8F%E7%9A%84%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8%EF%BC%9AString)

[3：整数常量：CONSTANT\_Integer\_info](#3%EF%BC%9A%E6%95%B4%E6%95%B0%E5%B8%B8%E9%87%8F%EF%BC%9ACONSTANT_Integer_info)

[4：浮点数常量：Float](#4%EF%BC%9A%E6%B5%AE%E7%82%B9%E6%95%B0%E5%B8%B8%E9%87%8F%EF%BC%9AFloat)

[5：长整数常量：Long](#5%EF%BC%9A%E9%95%BF%E6%95%B4%E6%95%B0%E5%B8%B8%E9%87%8F%EF%BC%9ALong)

[6：双精度浮点数常量：Double](#6%EF%BC%9A%E5%8F%8C%E7%B2%BE%E5%BA%A6%E6%B5%AE%E7%82%B9%E6%95%B0%E5%B8%B8%E9%87%8F%EF%BC%9ADouble)

[12：字段或方法的名称和描述符：NameAndType](#12%EF%BC%9A%E5%AD%97%E6%AE%B5%E6%88%96%E6%96%B9%E6%B3%95%E7%9A%84%E5%90%8D%E7%A7%B0%E5%92%8C%E6%8F%8F%E8%BF%B0%E7%AC%A6%EF%BC%9ANameAndType)

[1：UTF-8编码的字符串：Utf8](#1%EF%BC%9AUTF-8%E7%BC%96%E7%A0%81%E7%9A%84%E5%AD%97%E7%AC%A6%E4%B8%B2%EF%BC%9AUtf8)

[15：对方法句柄的符号引用：MethodHandle](#15%EF%BC%9A%E5%AF%B9%E6%96%B9%E6%B3%95%E5%8F%A5%E6%9F%84%E7%9A%84%E7%AC%A6%E5%8F%B7%E5%BC%95%E7%94%A8%EF%BC%9AMethodHandle)

[五、访问标识：类或接口的修饰符](#%E4%BA%94%E3%80%81%E8%AE%BF%E9%97%AE%E6%A0%87%E8%AF%86%EF%BC%9A%E7%B1%BB%E6%88%96%E6%8E%A5%E5%8F%A3%E7%9A%84%E4%BF%AE%E9%A5%B0%E7%AC%A6)

[六、类索引、父类索引、接口索引集合：继承信息](#%E5%85%AD%E3%80%81%E7%B1%BB%E7%B4%A2%E5%BC%95%E3%80%81%E7%88%B6%E7%B1%BB%E7%B4%A2%E5%BC%95%E3%80%81%E6%8E%A5%E5%8F%A3%E7%B4%A2%E5%BC%95%E9%9B%86%E5%90%88%EF%BC%9A%E7%BB%A7%E6%89%BF%E4%BF%A1%E6%81%AF)

[七、字段表集合：字段信息](#%E4%B8%83%E3%80%81%E5%AD%97%E6%AE%B5%E8%A1%A8%E9%9B%86%E5%90%88%EF%BC%9A%E5%AD%97%E6%AE%B5%E4%BF%A1%E6%81%AF)

[八、方法表集合：方法信息](#%E5%85%AB%E3%80%81%E6%96%B9%E6%B3%95%E8%A1%A8%E9%9B%86%E5%90%88%EF%BC%9A%E6%96%B9%E6%B3%95%E4%BF%A1%E6%81%AF)

[九、属性表集合](#uhHc5)

[9.1 基本介绍](#9.1%20%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D%C2%A0) 

[9.2 Code属性：字节码指令](#9.2%20Code%E5%B1%9E%E6%80%A7%EF%BC%9A%E5%AD%97%E8%8A%82%E7%A0%81%E6%8C%87%E4%BB%A4)

[9.3 Exceptions属性：异常类](#9.3%20Exceptions%E5%B1%9E%E6%80%A7%EF%BC%9A%E5%BC%82%E5%B8%B8%E7%B1%BB)

[9.4 LineNumberTable属性：行号映射](#9.4%20LineNumberTable%E5%B1%9E%E6%80%A7%EF%BC%9A%E8%A1%8C%E5%8F%B7%E6%98%A0%E5%B0%84)

[9.5 LocalVariableTable属性：局部变量映射](#9.5%20LocalVariableTable%E5%B1%9E%E6%80%A7%EF%BC%9A%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F%E6%98%A0%E5%B0%84)

[9.6 LocalVariableTypeTable属性：描述泛型](#9.6%20LocalVariableTypeTable%E5%B1%9E%E6%80%A7%EF%BC%9A%E6%8F%8F%E8%BF%B0%E6%B3%9B%E5%9E%8B)

[9.7 SourceFile及SourceDebugExtension属性：源码文件名](#9.7%20SourceFile%E5%8F%8ASourceDebugExtension%E5%B1%9E%E6%80%A7%EF%BC%9A%E6%BA%90%E7%A0%81%E6%96%87%E4%BB%B6%E5%90%8D)

[9.8 ConstantValue属性：静态变量](#9.8%20ConstantValue%E5%B1%9E%E6%80%A7%EF%BC%9A%E9%9D%99%E6%80%81%E5%8F%98%E9%87%8F)

[9.9 InnerClasses属性：内部类信息](#9.9%20InnerClasses%E5%B1%9E%E6%80%A7%EF%BC%9A%E5%86%85%E9%83%A8%E7%B1%BB%E4%BF%A1%E6%81%AF)

[9.10 Deprecated：@Deprecated注解元素](#9.10%20Deprecated%EF%BC%9A%40Deprecated%E6%B3%A8%E8%A7%A3%E5%85%83%E7%B4%A0)

[9.11 Synthetic属性：编译器生成元素](#9.11%20Synthetic%E5%B1%9E%E6%80%A7%EF%BC%9A%E7%BC%96%E8%AF%91%E5%99%A8%E7%94%9F%E6%88%90%E5%85%83%E7%B4%A0)

[9.12 StackMapTable属性](#9.12%20StackMapTable%E5%B1%9E%E6%80%A7)

[9.13 Signature属性](#9.13%20Signature%E5%B1%9E%E6%80%A7)

[9.14 BootstrapMethods属性](#9.14%20BootstrapMethods%E5%B1%9E%E6%80%A7)

[9.15 MethodParameters属性](#9.15%20MethodParameters%E5%B1%9E%E6%80%A7)

[9.16 模块化相关属性](#9.16%20%E6%A8%A1%E5%9D%97%E5%8C%96%E7%9B%B8%E5%85%B3%E5%B1%9E%E6%80%A7)

[9.17 运行时注解相关属性](#9.17%20%E8%BF%90%E8%A1%8C%E6%97%B6%E6%B3%A8%E8%A7%A3%E7%9B%B8%E5%85%B3%E5%B1%9E%E6%80%A7)

--

## 一、基本介绍

**类的二进制字节流：**即类的字节码文件，是一组以8个字节(64位)为基础单位的二进制流，各个单位内部及之间都排列紧凑，中间没有添加任何分隔符和空隙，这使得整个Class文件中存储的内容几乎都是程序运行的必要数据。

当遇到需要占用8个字节以上空间的数据项时，则会按照高位在前的方式分割成若干个8个字节进行存储，保证每个基础单位只有8个字节。

字节码文件的结构类似于C语言结构体，只有两种数据类型：“无符号数”和“表”：

-   **无符号数：**属于基本的数据类型，以**u1、u2、u4、u8来分别代表1个字节、2个字节、4个字节和8个字节的无符号数**。无符号数可以用来描述数字、索引引用、数量值或者按照UTF-8编码构成字符串值。
-   **表：**由多个无符号数或者其他表作为数据项构成的复合数据类型。为了便于区分，所有表的命名都习惯性地以“\_info”结尾。表用于描述有层次关系的复合结构的数据，整个Class文件本质上也可以视作是一张表，这张表由下图的数据项按严格紧密地按顺序排列构成。

 ![](https://i-blog.csdnimg.cn/blog_migrate/7e08a4580f3405ea47afb992256c9ea7.png) 

![](https://i-blog.csdnimg.cn/blog_migrate/d4f5cc30f8c84bd77cb2e9d5dea8d027.png)

## 二、环境准备

### 2.1 准备字节码文件

1.准备测试类 

```java
public class Test {
    public Test() {
    }

    public static void main(String[] args) {
        System.out.println("hello~~~~~~~");
    }
}
```

2.使用javac命令编译成字节码文件：

```java
javac Test.java
```

![](https://i-blog.csdnimg.cn/blog_migrate/05fe22a5dbc537c3710c39fb855f2e3f.png)

> 运行class文件：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/90180c0b8a9edbf37caf4c71056af7ec.png)

### 2.2 打开十六进制的字节码文件 

字节码文件直接用记事本打开会乱码，因为字节码文件是二进制文件，内容是一组以 8 位为最小基础的十六进制数据流： ![](https://i-blog.csdnimg.cn/blog_migrate/d5d89388480102c5f5e1dc2eda80942e.png)

所以需要给nodepad++下载HEX-Editor插件，以便于查看16进制的数据：

![](https://i-blog.csdnimg.cn/blog_migrate/949ef67d6254748cdb98a0628afc7616.png)

![](https://i-blog.csdnimg.cn/blog_migrate/c7e4f1c59edee3981801ec52d2fcc138.png)

然后就可以查看16进制的class文件：

![](https://i-blog.csdnimg.cn/blog_migrate/41cb28185b7f91b49025b922ec574c6e.png)

### 2.3 分析字节码文件：javap命令

JDK提供了javap工具(在JDK的bin目录下)可以解析此二进制文件，我们通过javap命令来解析此class文件：

> **javap：**
> 
> -   javap是Java开发工具包（JDK）提供的一个命令行工具。
> -   **作用：**用于反编译Java字节码。基于反射，将Java类文件解析为易于阅读的文本形式，展示其中的信息以及反编译出类的结构、方法、字段、常量池等信息。

```java
javap -v -p -s -sysinfo -constants Test.class
```

解析得到的结果为：

![](https://i-blog.csdnimg.cn/blog_migrate/c2ed23b7c5222cc4f6d8139f43883f3d.png)

**详细内容：**

```bash
Classfile /D:/workspace/test/test/Test.class
  Last modified 2024-4-8; size 418 bytes
  MD5 checksum b6ffe75707d6edf8814696b8f18ad8d9
  Compiled from "Test.java"
public class Test
  minor version: 0
  major version: 52
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #6.#15         // java/lang/Object."<init>":()V
   #2 = Fieldref           #16.#17        // java/lang/System.out:Ljava/io/PrintStream;
   #3 = String             #18            // hello~~~~~~~
   #4 = Methodref          #19.#20        // java/io/PrintStream.println:(Ljava/lang/String;)V
   #5 = Class              #21            // Test
   #6 = Class              #22            // java/lang/Object
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               main
  #12 = Utf8               ([Ljava/lang/String;)V
  #13 = Utf8               SourceFile
  #14 = Utf8               Test.java
  #15 = NameAndType        #7:#8          // "<init>":()V
  #16 = Class              #23            // java/lang/System
  #17 = NameAndType        #24:#25        // out:Ljava/io/PrintStream;
  #18 = Utf8               hello~~~~~~~
  #19 = Class              #26            // java/io/PrintStream
  #20 = NameAndType        #27:#28        // println:(Ljava/lang/String;)V
  #21 = Utf8               Test
  #22 = Utf8               java/lang/Object
  #23 = Utf8               java/lang/System
  #24 = Utf8               out
  #25 = Utf8               Ljava/io/PrintStream;
  #26 = Utf8               java/io/PrintStream
  #27 = Utf8               println
  #28 = Utf8               (Ljava/lang/String;)V
{
  public Test();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 2: 0
        line 3: 4

  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=1, args_size=1
         0: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
         3: ldc           #3                  // String hello~~~~~~~
         5: invokevirtual #4                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
         8: return
      LineNumberTable:
        line 6: 0
        line 7: 8
}
SourceFile: "Test.java"
```

## **三、第一个基础单位：魔数和版本号** 

Class文件的第一个基础单位同样占用8个字节，主要存储基础信息：

-   **魔数：**每个Class文件的头4个字节。唯一作用是确定这个文件是不是一个能被虚拟机接受的Class文件。
-   **版本号**：JVM可以通过版本号判断这个字节码文件所对应的JDK版本。版本号从45开始，JDK1.1之后每个大版本的主版本号向上加1，例如JDK2.0的主版本号46，JDK8的版本号52（转为16进制是0x34 hex）。高版本的JDK能够向下兼容更低版本的Class文件，但不能运行更高版本的Class文件。所以虚拟机会拒绝执行超过其版本号的Class文件。
    -   **次版本号（Minor Version）：**第5和第6个字节。
    -   **主版本号（Major Version）：**第7和第8个字节。数据类型为u2，即占两个字节

**常见JDK版本的版本号：**

JavaSE 8 = 52 (0x34 hex),  
JavaSE 7 = 51 (0x33 hex),  
JavaSE 6 = 50 (0x32 hex), 

> **验证：**
> 
> **前4位魔数：**cafebabe。
> 
> 截取下来表示为cafeBabe，可以翻译为咖啡宝贝。
> 
> **主次版本号：**我本地JDK版本是8.0，JDK8的版本号52（转为16进制是0x34 hex）。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/2c11c4d588ad285909aab9d1aac8a436.png)
> 
> 结果跟分析结果保持一致：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/40f529f7a4d060643a5f3aeb83522169.png)

## **四、常量池：字面量和符号引用**

### 4.1 基本介绍 

常量池入口紧接着主、次版本号之后，常量池中常量的数量是不固定的。 

**常量池：**就是一张表，JVM根据这张常量表找到要执行的类信息和方法信息。

**类常量池：**是.class字节码文件中的资源仓库，主要存放字面量和符号引用。

-   **字面量：**表示字符串值和数值，例如字符串值"abc"、**final常量、静态变量**
-   **符号引用：**类和接口的全限定名、字段名、方法名

> **运行时常量池和字符串常量池：**
> 
> JVM的运行时数据区还有运行时常量池、字符串常量池：
> 
> -   **运行时常量池：**类加载的“加载”阶段会创建运行时常量池，统一存放各个类常量池去重后的符号引用。在类加载的“解析”阶段JVM会把运行时常量池的这些符号引用转为直接引用。类常量池。类常量池在字节码文件中的，运行时常量池在内存中。
> -   **字符串常量池：**专门针对String类型设计的常量池。是当前应用程序里所有线程共享的，每个jvm只有一个字符串常量池。存储字符串对象的引用。在创建String对象时，JVM会先在字符串常量池寻找是否已存在相同字符串的引用，如果有的话就直接返回引用，没的话就在堆中创建一个对象，然后常量池保存这个引用并返回引用。
> 
> **具体参考：**[什么是JVM的内存模型？详细阐述Java中局部变量、常量、类名等信息在JVM中的存储位置-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/134742377?spm=1001.2014.3001.5501 "什么是JVM的内存模型？详细阐述Java中局部变量、常量、类名等信息在JVM中的存储位置-CSDN博客")

**常量池的项目类型：** 

![](https://i-blog.csdnimg.cn/blog_migrate/d4efd4acaf22248ae46c4c9b35ffaf64.png)

### **4.2 验证-常量项数量**

![](https://i-blog.csdnimg.cn/blog_migrate/96c728c6e9933c99fe9651f854ddfb4e.png)

这里显示“1d”，转为十进制就是1\*16+13=29个常量项（实际是28个，即1~28，0号位是预留的常量项，如果某些引用需要指向空则就直接指向0，表示空）。

分析得出的常量项数量也是28个（不包含0号位）：

![](https://i-blog.csdnimg.cn/blog_migrate/88dbf79419d88b67414a94353f1711cf.png)

### **4.3 验证-第一个常量项：类中方法的符号引用**

#### 4.3.1 验证十六进制的字节码文件

在常量池数量字节“1d”后面，紧接着的5个字节是第一个常量项：

第一个字节是0a，对应十进制10,查上表可以得到，10标志位对应的项目类型是CONSTANT\_Methodref\_info，即**类中方法的符号引用**。

紧接着的4个字节是常量项的值，包括06和0f，转为十进制是6和15。

![](https://i-blog.csdnimg.cn/blog_migrate/537ee4bf20933b23bca45ea6c0f3e208.png)

> **为什么第一个常量项一共占5个字节？**
> 
> 我们可以看下面标志位为10的常量项的结构，包含1个u1和两个u2类型，根据上面第一节基本介绍，我们可以知道u1占1个字节，u2占两个字节，1+2\*2=5，一共占5个字节。
> 
> **tag值:10：**CONSTANT\_Methodref\_info
> 
> ```java
> // 类中方法的符号引用
> CONSTANT_Methodref_info {
>     // 10
>     u1 tag;   
>     // 定义类或接口的常量项所在索引
>     u2 class_index; 
>     // 定义字段或方法部分符号引用的常量项所在索引
>     u2 name_and_type_index;
> }
> ```

所以：

-   **10标志位：**常量项的值是（10,6,15） 。即标志位10，定义类或接口的常量项所在索引是6，定义字段或方法部分符号引用的常量项所在索引是15。

#### 4.3.2 **分析字节码文件：javap命令**

分析字节码文件，可以知道我们的推断是正确的：

![](https://i-blog.csdnimg.cn/blog_migrate/e637e21effdb92f53183e40a4cb4e1b4.png)

> **注：**
> 
> -   `#`号后面是索引，索引从1开始，索引没有从0开始，是因为设计者考虑到不引用任何常量时，可以将索引设置为0来表示。
> -   `=`号后面是常量的类型。

-   #1常量的类型是Methodref，表示类中方法的符号引用，#1常量指向常量池中第6个和第15个的常量。
-   #6常量类型是Class，表示用来定义类或接口，指向#22常量。
-   #22常量类型是Utf8的字符串，值为java/lang/Object。
-   #15常量类型是NameAndType，表示字段或方法的部分符号引用，指向常量池中的#7和#28常量。
-   #7常量类型是Utf8的字符串，值为<init>，表示为构造方法。
-   #28常量类型是Utf8的字符串，值为()V，表示方法的返回值是void。

总结#1常量，Person类的使用默认的构造方法，来源自Object类。 

### 4.4 验证-第二个常量项

紧接着的是第二个常量项，标志位是是9，类型是Fieldref\_info，即存储字段的符号引用。

```java
CONSTANT_Fieldref_info {
    u1 tag;               // 标签，固定为9，表示常量类型为Fieldref
    u2 class_index;       // 对常量池中CONSTANT_Class_info类型的常量的索引，指向字段所属类或接口的符号引用
    u2 name_and_type_index; // 对常量池中CONSTANT_NameAndType_info类型的常量的索引，指向字段名和字段描述符的符号引用
}
```

![](https://i-blog.csdnimg.cn/blog_migrate/2bb685c6d555cf1a7fd887c895e8975f.png)

**分析可以得出：**

-   **tag：**tag是“09” ，转十进制是9；
-   **class\_index：**class\_index是“00 10”，转十进制是16，类型是符号引用，指向第16个常量项，第16个常量项是字段所属类或接口的符号引用（java/lang/System）；
-   **name\_and\_type\_index：**name\_and\_type\_index是“00 11”，转十进制是17，类型是符号引用，指向第17个常量项，第17个常量项是字段名和字段描述符的符号引用（out:Ljava/io/PrintStream;）；

![](https://i-blog.csdnimg.cn/blog_migrate/d58e6f43ec17752354fe166125a107e0.png)

### 4.5 扩展：所有常量项的标志位

以下是Java字节码文件的常量项各字段的详细介绍：

#### 7：类或接口的符号引用：Class

tag值: 7

功能：表示类或接口的符号引用。

格式：

```java
CONSTANT_Class_info {
    u1 tag;           // 标签，固定为7，表示常量类型为Class
    u2 name_index;    // 对常量池中CONSTANT_Utf8_info类型的常量的索引，指向类名的UTF-8字符串常量
}
```

#### 9：字段的符号引用：Fieldref

tag值: 9

功能：表示字段的符号引用。

格式：

```java
CONSTANT_Fieldref_info {
    u1 tag;               // 标签，固定为9，表示常量类型为Fieldref
    u2 class_index;       // 对常量池中CONSTANT_Class_info类型的常量的索引，指向字段所属类或接口的符号引用
    u2 name_and_type_index; // 对常量池中CONSTANT_NameAndType_info类型的常量的索引，指向字段名和字段描述符的符号引用
}
```

#### 10：方法的符号引用：Methodref

tag值: 10

功能：表示普通（非接口）方法的符号引用。

格式：

```java
CONSTANT_Methodref_info {
    u1 tag;               // 标签，固定为10，表示常量类型为Methodref
    u2 class_index;       // 对常量池中CONSTANT_Class_info类型的常量的索引，指向方法所属类的符号引用
    u2 name_and_type_index; // 对常量池中CONSTANT_NameAndType_info类型的常量的索引，指向方法名和方法描述符的符号引用
}
```

#### 11：接口方法的符号引用：InterfaceMethodref

tag值: 11

功能：表示接口方法的符号引用。

格式：

```java
CONSTANT_InterfaceMethodref_info {
    u1 tag;               // 标签，固定为11，表示常量类型为InterfaceMethodref
    u2 class_index;       // 对常量池中CONSTANT_Class_info类型的常量的索引，指向方法所属接口的符号引用
    u2 name_and_type_index; // 对常量池中CONSTANT_NameAndType_info类型的常量的索引，指向方法名和方法描述符的符号引用
}
```

#### 8：字符串常量的符号引用：String

tag值: 8

功能：表示字符串常量的符号引用。

格式：

```java
CONSTANT_String_info {
    u1 tag;               // 标签，固定为8，表示常量类型为String
    u2 string_index;      // 对常量池中CONSTANT_Utf8_info类型的常量的索引，指向字符串的UTF-8表示形式的符号引用
}
```

#### 3：整数常量：CONSTANT\_Integer\_info

tag值: 3

功能：表示整数常量。

格式：

```java
CONSTANT_Integer_info {
    u1 tag;               // 标签，固定为3，表示常量类型为Integer
    u4 bytes;             // 4字节整数值的符号引用
}
```

#### 4：浮点数常量：Float

tag值: 4

功能：表示浮点数常量。

格式：

```java
CONSTANT_Float_info {
    u1 tag;               // 标签，固定为4，表示常量类型为Float
    u4 bytes;             // 4字节浮点数值的符号引用
}
```

#### 5：长整数常量：Long

tag值: 5

功能：表示长整数常量。

格式：

```java
CONSTANT_Long_info {
    u1 tag;               // 标签，固定为5，表示常量类型为Long
    u4 high_bytes;        // 高位32位整数值的符号引用
    u4 low_bytes;         // 低位32位整数值的符号引用
}
```

#### 6：双精度浮点数常量：Double

tag值: 6

功能：表示双精度浮点数常量。

格式：

```java
CONSTANT_Double_info {
    u1 tag;               // 标签，固定为6，表示常量类型为Double
    u4 high_bytes;        // 高位32位浮点数值的符号引用
    u4 low_bytes;         // 低位32位浮点数值的符号引用
}
```

#### 12：字段或方法的名称和描述符：NameAndType

tag值: 12

功能：表示字段或方法的名称和描述符。

格式：

```java
CONSTANT_NameAndType_info {
    u1 tag;              // 标签，固定为12，表示常量类型为NameAndType
    u2 name_index;       // 对常量池中CONSTANT_Utf8_info类型的常量的索引，指向字段名或方法名的UTF-8表示形式的符号引用
    u2 descriptor_index; // 对常量池中CONSTANT_Utf8_info类型的常量的索引，指向字段描述符或方法描述符的UTF-8表示形式的符号引用
}
```

#### 1：UTF-8编码的字符串：Utf8

tag值: 1

功能：表示UTF-8编码的字符串。

格式：

```java
CONSTANT_Utf8_info {
    u1 tag;              // 标签，固定为1，表示常量类型为Utf8
    u2 length;           // 字符串长度
    u1 bytes[length];    // UTF-8编码的字节数组
}
```

#### 15：对方法句柄的符号引用：MethodHandle

tag值: 15

功能：表示对方法句柄的符号引用。

格式：

```java
CONSTANT_MethodHandle_info {
    u1 tag;              // 标签，固定为15，表示常量类型为MethodHandle
    u1 reference_kind;  // 方法句柄的类型
    u2 reference_index; // 对常量池中CONSTANT_Fieldref_info、CONSTANT_Methodref_info或CONSTANT_InterfaceMethod
```

## 五、访问标识：类或接口的修饰符

访问标志（access\_flags）在常量池之后紧接着的2个字节。

**访问标志：**用于识别类或者接口的访问信息。包括：

-   这个字节码文件是类还是接口；
-   是否定义为public类型；
-   是否定义为abstract 类型；
-   如果是类的话，是否被声明为final； 

![](https://i-blog.csdnimg.cn/blog_migrate/0a1ed3465cc51b1cc617bb60d09eab02.png)

> 验证：
> 
> Test类基本标识是0x 00 20(ACC\_SUPER在JDK1.0.2后都是true)，又因为它只有public访问修饰符（对应ACC\_PUBLIC是0x 00 01），两个标识加起来是0x 00 21  
>  

## 六、类索引、父类索引、接口索引集合：继承信息

这三项数据用来确定该类的继承关系。 

类索引（this\_class）和父类索引（super\_class）都是一个u2类型的数据，而接口索引集合 （interfaces）是一组u2类型的数据的集合。

-   **类索引：**确定类的全限定名；
-   **父类索引：**确定父类的全限定名。只有Object类的父类索引为0。所有Java类都是Object的直接或间接子类，除了Object类外，所有类的父类索引都不为0。
-   **接口索引集合：**确定该类实现了哪些接口、该接口继承了哪些接口。这些被实现的接口将按implements关键字（如果这个Class文件表示的是一个接口，则是extends关键字）后的接口顺序，从左到右依次排列在**接口索引集合**中。

## 七、字段表集合：字段信息

**字段表**（field\_info）**：**描述类或接口的成员变量。 

-   **access\_flags：**字段修饰符
-   **name\_index：**字段简单名称（不包含字段的类型和修饰） 。例如Test类中的fun()方法和num字段的简单名称分别就是“fun”和“num“。
-   **descriptor\_index ：**字段的数据类型、方法的参数列表（包括数量、类型以及顺序）和返回值。
    -   基本数据类型 ：（byte、char、double、float、int、long、short、boolean）以及代表无返回值的void类型都用一个大写字符来表示 。
    -   数组类型 ： 每一维度将使用一个前置的“\[”字符来描述，如一个定义为“java.lang.String\[\]\[\]”类型的二维数组将被记录成“\[\[Ljava/lang/String；”，一个整型数组“int\[\]”将被记录成“\[I“。  
         

## 八、方法表集合：方法信息

**字段表**（field\_info）**：**描述类或接口的方法。

特点： 

-   **未重写方法不存放：**如果父类方法在子类中没有被重写（Override），方法表集合中就不会出现来自父类的方法信息。
-   **构造器方法自动添加：**有可能会出现由编译器自动添加的方法，最常见的便是类构造器“()”方法和实例构造器“()”方法。

结构和字段表一样： 

![](https://i-blog.csdnimg.cn/blog_migrate/83912548cc7919dcdc398706b24466bc.png)

## 九、属性表集合

### 9.1 基本介绍 

**属性表集合：**Class文件、字段表、方法表都可以携带自己的属性表集合，以描述某些场景专有的信息。 限制宽松，不要求各个属性表具有严格顺序 。

**特点：**字节码文件中，只有属性表集合不再要求各个属性表具有严格顺序。

每一个属性的**名称**都要从常量池中引用一个CONSTANT\_Utf8\_info类型的常量来表示，而**属性值的结构则是完全宽松、自定义的**，只需要通过一个**u4的长度属性**去说明属性值所占用的位数即可。

![](https://i-blog.csdnimg.cn/blog_migrate/3427083bf0fc9412050ce47d7dc04494.png)

### 9.2 Code属性：字节码指令

Code属性：存放字节码指令。方法体中的代码逻辑在编译之后，会变为字节码指令。

Code属性出现在方法表的属性集合之中，但并非所有的方法表都必须存在这个属性，譬如接口或抽象类中的抽象方法就不存在Code属性。

### 9.3 Exceptions属性：异常类

Exceptions属性是在方法表中与Code属性平级的一项属性。 也就是方法描述时在**throws关键字后面列举的异常。** 

![](https://i-blog.csdnimg.cn/blog_migrate/eddd41e840dd055b766c6a861458e6da.png)

### 9.4 LineNumberTable属性：行号映射

LineNumberTable属性用于描述Java源码（.java）行号与字节码（.class）行号（字节码的偏移量）之间的对应关系。

Java源码编译成字节码文件的过程中，编译器会在不改变语义的前提下，对指令进行重排序，以提高程序的运行速度。所以，源码和字节码文件的行号一般是不一样的。

所以在调试当抛出异常时，JVM可以直接获取到字节码文件出错的行号，通过LineNumberTable属性，找到对应源码的行号，并输出到控制台。

> **指令重排序：**处理器为了提高运算速度会对指令重排序，重排序分三种类型：编译器优化重排序、处理器指令级并行重排序、内存系统重排序。 
> 
> -   **编译器优化的重排序：**编译器在不改变单线程程序的语义前提下，可以重新安排语句的执行顺序。
> -   **指令级并行的重排序：**现在处理器采用了指令集并行技术，将多条指令重叠执行。如果不存在依赖性，处理器可以改变语句对应的机器指令的执行顺序。
> -   **内存系统的重排序：**由于处理器使用缓存和读写缓冲区，这使得加载和存储操作看上去可能是在乱序执行。

### 9.5 LocalVariableTable属性：局部变量映射

**LocalVariableTable属性：**描述栈帧中局部变量表的变量与Java源码中定义的变量之间的关系，它记录了方法的局部变量在方法执行期间的名称、数据类型和作用域信息。

它也不是运行时必需的属性，但默认会生成到Class文件之中。可以在Javac中分别使用g:none或g:vars选项来取消或要求生成这项信息。

如果没有生成这项属性，最大的影响就是当其他人引用这个方法时，所有的参数名称都将会丢失，IDE将会使用诸如arg0、arg1之类的占位符代替原有的参数名，这对程序运行没有影响，但是会对代码编写带来较大不便，而且在调试期间无法根据参数名称从上下文中获得参数值。

### 9.6 LocalVariableTypeTable属性：描述泛型

对于非泛型类型来说，描述符和特征签名能描述的信息是能吻合一致的，但是泛型引入之后，由于描述符中泛型的参数化类型被擦除掉，描述符就不能准确描述泛型类型了。因此出现了LocalVariableTypeTable属性，使用**字段的特征签名**来完成泛型的描述。 

**LocalVariableTypeTable属性**：JDK 5新增的属性，主要用于存储泛型（JDK5新增）的局部变量信息。

LocalVariableTypeTable与LocalVariableTable非常相似，仅仅是把记录的字段描述符的descriptor\_index替换成了字段的特征签名（Signature）。

> **知识扩展：**
> 
> **泛型：**将具体的类型参数化，是一种编程范式，提供了编译时类型安全检测机制。
> 
> 通过使用泛型，我们可以将数据类型作为参数传递给类、接口或方法，可以在编译时期进行类型检查，避免在运行时期出现类型转换错误。
> 
> **泛型的范围：**泛型接口，泛型类（创建对象时再指定具体类型），泛型方法。
> 
> **实现方式：**以泛型类举例。我们只需要在类名后面使用尖括号<>将一个符号或多个符号包裹起来，这样在类里面就可以使用该符号代替具体类型了。使用泛型类时，调用者实际传进来什么类型，编译时就会将泛型符号擦除，替换成这个实际类型。泛型符号可以是任意符号，但我们约定使用T、E、K、V等符号。
> 
> **泛型擦除：**java的泛型是伪泛型，这是因为java在编译期间，所有的泛型类型都会被擦掉，并转换为普通类型。 
> 
> 泛型擦除的主要目的是为了向低版本兼容，因为Java泛型是在JDK 1.5之后才引入的特性，为了保证旧有的代码能正常运行，Java编译器采用了泛型擦除来兼容之前的代码。
> 
> **对比Object类：**泛型是在编译时泛型擦除和替换实际类型的，而使用Object类会很麻烦，需要经常强制转换。例如List集合里，如果直接声明存Object类的话，存的时候还好，可以通过多态机制直接向上转型，而取的时候就麻烦了，要强转Object类为String等对象，然后才能访问该对象的成员；而且你不知道实际元素到底是String类型还是Integer等其他类型，还要通过i instanceof String判断类型，就更麻烦了。
> 
> **泛型的好处：**
> 
> 1.  可以在编译时检查类型安全。
> 2.  所有的强制转换都是自动和隐式的，可以提高代码的重用率。
> 
> **向上转型：**泛型类或接口可以向上转型为父类，泛型符号不能向上转型。泛型向上转型指的是将一个泛型对象转换为其父类类型或者接口类型的过程。这个过程实际上是将泛型对象的类型参数擦除，重新赋值为其父类或接口类型。
> 
> -   ArrayList<T>可以向上转型为List<T>
> -   ArrayList<Integer>泛型不可以向上转化为ArrayList<Number>。因为ArrayList<Number>接收ArrayList<float>，但ArrayList< Integer>不可以接收ArrayList< Float>，不能转回来 
> 
> 除了向上转型，也有向下转型。 
> 
>  **泛型类：**
> 
> ```java
> public class Generic<T> {
>     private T t;
>  
>     public T getT() {
>         return t;
>     }
>  
>     public void setT(T t) {
>         this.t = t;
>     }
> }
> ```
> 
> **泛型接口：**
> 
> ```java
> public interface Generic<T> {...}
> ```
> 
> **泛型方法：**
> 
> ```java
>     public <T>void show(T t){
>         System.out.println(t);
>     }
> ```

### 9.7 SourceFile及SourceDebugExtension属性：源码文件名

SourceFile属性用于记录生成这个Class文件的源码文件名称。

如果不生成这项属性，当抛出异常时，堆栈中将不会显示出错代码所属的文件名。

### 9.8 ConstantValue属性：静态变量

ConstantValue属性的作用是通知虚拟机自动为静态变量赋值。只有被static关键字修饰的变量（类 变量）才可以使用这项属性。

### 9.9 InnerClasses属性：内部类信息

InnerClasses属性用于记录内部类与宿主类之间的关联。如果一个类中定义了内部类，那编译器将 会为它以及它所包含的内部类生成InnerClasses属性。

### 9.10 Deprecated：`@Deprecated`注解元素

Deprecated属性用于表示某个类、字段或者方法，已经被程序作者定为不再推荐使用，它可以通 过代码中使用“@Deprecated”注解进行设置。

Synthetic属性代表此字段或者方法并不是由Java源码直接产生的，而是由编译器自行添加的。

### 9.11 Synthetic属性：编译器生成元素

Synthetic属性：标识由编译器生成、而非源代码中显式声明的类成员（字段、方法）。

通常用于在字节码中标记一些由编译器自动生成的成员，这些成员对于程序运行而言是不可见的，仅在编译时需要。

### 9.12 StackMapTable属性

这个属性会在虚拟机类加载 的字节码验证阶段被新类型检查验证器（Type Checker）使用，目的在于代替以前比较消耗性能的基于数据流分析的类型推导验证器。

### 9.13 Signature属性

任何类、接口、初始化方法或成员的泛型签名如果包含了类型变量（Type Variable）或参数化类型（Parameterized Type），则Signature属性会为它记录泛型签名信息。之所以要专门使用这样一个属性去记录泛型类 型，是因为Java语言的泛型采用的是擦除法实现的伪泛型，字节码（Code属性）中所有的泛型信息编译（类型变量、参数化类型）在编译之后都通通被擦除掉。

### 9.14 BootstrapMethods属性

这个属性用于保存invokedynamic指令引用的引导方法限定符。

### 9.15 MethodParameters属性

MethodParameters的作用是记录方法的各个形参名称和信息。

### 9.16 模块化相关属性

JDK 9的一个重量级功能是Java的模块化功能，因为模块描述文件（module-info.java）最终是要编译成一个独立的Class文件来存储的，所以，Class文件格式也扩展了Module、ModulePackages和 ModuleMainClass三个属性用于支持Java模块化相关功能。 Module属性是一个非常复杂的变长属性，除了表示该模块的名称、版本、标志信息以外，还存储了这个模块requires、exports、opens、uses和provides定义的全部内容。

### 9.17 运行时注解相关属性

早在JDK 5时期，Java语言的语法进行了多项增强，其中之一是提供了对注解（Annotation）的支持。为了存储源码中注解信息，Class文件同步增加了RuntimeVisibleAnnotations、 RuntimeInvisibleAnnotations、RuntimeVisibleParameterAnnotations和RuntimeInvisibleParameterAnnotations四个属性。到了JDK 8时期，进一步加强了Java语言的注解使用范围，又新增类型注解 （JSR 308），所以Class文件中也同步增加了RuntimeVisibleTypeAnnotations和RuntimeInvisibleTypeAnnotations两个属性。

由于这六个属性不论结构还是功能都比较雷同，因此我们把它们合并到一起，以RuntimeVisibleAnnotations为代表进行介绍。

RuntimeVisibleAnnotations是一个变长属性，它记录了类、字段或方法的声明上记录运行时可见注解，当我们使用反射API来获取类、字段或方法上的注解时，返回值就是通过这个属性来取到的。