>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?spm=1001.2014.3001.5501 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[三、String](#String%C2%A0) 

[3.1.String常量池](#String%E5%B8%B8%E9%87%8F%E6%B1%A0%E3%80%81new)

[3.2.请你说说String类](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4String%E7%B1%BB%2C%E4%BB%A5%E5%8F%8Anew%E5%92%8C)

[String常用方法](#String%E5%B8%B8%E7%94%A8%E6%96%B9%E6%B3%95)

[创建字符串的两种方式](#%E5%88%9B%E5%BB%BA%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E4%B8%A4%E7%A7%8D%E6%96%B9%E5%BC%8F)

[源码（JDK8）](#%E6%BA%90%E7%A0%81%EF%BC%88JDK8%EF%BC%89)

[源码（JDK9）](#%E6%BA%90%E7%A0%81%EF%BC%88JDK9%EF%BC%89)

[String类为什么不可被继承](#String%E7%B1%BB%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E5%8F%AF%E8%A2%AB%E7%BB%A7%E6%89%BF)

[String类为什么要设计成final](#String%E7%B1%BB%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E8%AE%BE%E8%AE%A1%E6%88%90final)

[String的字符串为什么不可被变](#String%E7%9A%84%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E5%8F%AF%E8%A2%AB%E5%8F%98)

 [String源码有用到什么设计模式？](#%C2%A0String%E6%BA%90%E7%A0%81%E6%9C%89%E7%94%A8%E5%88%B0%E4%BB%80%E4%B9%88%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%EF%BC%9F)

[享元模式和单例模式区别](#%E4%BA%AB%E5%85%83%E6%A8%A1%E5%BC%8F%E5%92%8C%E5%8D%95%E4%BE%8B%E6%A8%A1%E5%BC%8F%E5%8C%BA%E5%88%AB)

[3.3.new String("abc")创建了几个字符串对象？](#3.3.new%20String%28%22abc%22%29%E5%88%9B%E5%BB%BA%E4%BA%86%E5%87%A0%E4%B8%AA%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%AF%B9%E8%B1%A1%EF%BC%9F)

[3.4.String、StringBuffer、Stringbuilder有什么区别](#String%E3%80%81StringBuffer%E3%80%81Stringbuilder%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB)

[四、集合](#%E9%9B%86%E5%90%88%C2%A0) 

[4.1.请说说你对Java集合的了解](#%E8%AF%B7%E8%AF%B4%E8%AF%B4%E4%BD%A0%E5%AF%B9Java%E9%9B%86%E5%90%88%E7%9A%84%E4%BA%86%E8%A7%A3)

[4.2.请你说说List与Set的区别](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4List%E4%B8%8ESet%E7%9A%84%E5%8C%BA%E5%88%AB)

[4.3.说说你对ArrayList的理解](#%E8%AF%B4%E8%AF%B4%E4%BD%A0%E5%AF%B9ArrayList%E7%9A%84%E7%90%86%E8%A7%A3)

[4.4.请你说说ArrayList和LinkedList的区别](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4ArrayList%E5%92%8CLinkedList%E7%9A%84%E5%8C%BA%E5%88%AB)

[4.5.请你说说HashMap底层原理](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4HashMap%E5%BA%95%E5%B1%82%E5%8E%9F%E7%90%86)

[底层数据结构](#%E5%BA%95%E5%B1%82%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)

[扩容机制](#%E6%89%A9%E5%AE%B9%E6%9C%BA%E5%88%B6%C2%A0) 

[put()流程](#put%28%29%E6%B5%81%E7%A8%8B)

[HashMap容量为什么是2的n次方？](#HashMap%E5%AE%B9%E9%87%8F%E4%B8%BA%E4%BB%80%E4%B9%88%E6%98%AF2%E7%9A%84n%E6%AC%A1%E6%96%B9%EF%BC%9F)

[JDK7扩容时死循环问题](#JDK7%E6%89%A9%E5%AE%B9%E6%97%B6%E6%AD%BB%E5%BE%AA%E7%8E%AF%E9%97%AE%E9%A2%98)

[JDK8 尾插法](#JDK8%20%E5%B0%BE%E6%8F%92%E6%B3%95)

[JDK8 put时数据覆盖问题](#JDK8%20put%E6%97%B6%E6%95%B0%E6%8D%AE%E8%A6%86%E7%9B%96%E9%97%AE%E9%A2%98)

[modCount非原子性自增问题](#modCount%E9%9D%9E%E5%8E%9F%E5%AD%90%E6%80%A7%E8%87%AA%E5%A2%9E%E9%97%AE%E9%A2%98)

[源码](#%E6%BA%90%E7%A0%81)

[4.6.请你说说ConcurrentHashMap](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4ConcurrentHashMap)

[4.7.请你说说HashMap和Hashtable的区别](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4HashMap%E5%92%8CHashtable%E7%9A%84%E5%8C%BA%E5%88%AB)

[五、泛型](#%E6%B3%9B%E5%9E%8B%C2%A0) 

[5.1.请你说说泛型、泛型擦除](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4%E6%B3%9B%E5%9E%8B%E3%80%81%E6%B3%9B%E5%9E%8B%E6%93%A6%E9%99%A4)

[六、IO](#IO%C2%A0) 

[6.1.请你说说IO多路复用](#15.%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4IO%E5%A4%9A%E8%B7%AF%E5%A4%8D%E7%94%A8)

[6.2.请你说说BIO、NIO、O](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4BIO%E3%80%81NIO%E3%80%81O)

[6.3.请你讲一下Java NIO](#%E8%AF%B7%E4%BD%A0%E8%AE%B2%E4%B8%80%E4%B8%8BJava%20NIO)

[七、异常](#%E5%BC%82%E5%B8%B8%C2%A0) 

[7.0.说说异常体系](#7.0.%E8%AF%B4%E8%AF%B4%E5%BC%82%E5%B8%B8%E4%BD%93%E7%B3%BB)

[7.1.请你说说Java的异常处理机制](#%E8%AF%B7%E4%BD%A0%E8%AF%B4%E8%AF%B4Java%E7%9A%84%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86%E6%9C%BA%E5%88%B6)

[八、反射](#%E5%8F%8D%E5%B0%84%C2%A0) 

[8.1.请说说你对反射的了解](#%E8%AF%B7%E8%AF%B4%E8%AF%B4%E4%BD%A0%E5%AF%B9%E5%8F%8D%E5%B0%84%E7%9A%84%E4%BA%86%E8%A7%A3)

[九、多线程](#%E7%BA%BF%E7%A8%8B)

--

## 三、String 

### 3.1.String常量池

> 介绍、原理 

**常量池：**Java虚拟机有一个常量池机制，它会直接把字符串常量放入常量池中，从而实现复用。

**Java字符串存储原理：** 

1.  创建字符串常量时，JVM会通过equals()检查字符串常量池中是否存在这个字符串；
2.  若字符串常量池中存在该字符串，则直接返回引用实例；
3.  若不存在，先实例化该字符串，并且将该字符串的引用放入字符串常量池中，以便于下次使用时，直接取用，达到缓存快速使用的效果。

> str1和str2在赋值时，使用的是字符串常量。 因此str1和str2指向的是常量池中的同一个内存地址，所以返回值是true。
> 
> ```java
> //比较地址
> //只要new，就在堆内存开辟空间。直接赋值字符串在常量池里。
>         String str1 = "hello";        //常量池里无“hello”对象，创建“hello”对象，str1指向常量池“hello”对象。
> //先检查字符串常量池中有没有"hello"，如果字符串常量池中没有，则创建一个，然后 str1 指向字符串常量池中的对象，如果有，则直接将 str1 指向"hello"；
>         String str2 = "hello";    //常量池里有“hello”对象，str2直接指向常量池“hello”对象。
>         String str3 = new String("hello");   //堆中new创建了一个对象。假如“hello”在常量池中不存在，Jvm还会常量池中创建这个对象“hello”。
>         String str4 = new String("hello");
>         System.out.println(str1==str2);//true，因为str1和str2指向的是常量池中的同一个内存地址
>         System.out.println(str1==str3);//fasle，str1常量池旧地址，str3是new出的新对象，指向一个全新的地址
>         System.out.println(str4==str3);//fasle，因为它们引用不同
>  
> //比较内容
>         System.out.println(str4.equals(str3));//true，因为String类的equals方法重写过，比较的是字符串值
> ```

### 3.2.请你说说String类

> **得分点**
> 
> String常用方法,String能否被继承,创建字符串的两种方式、String不可变和不可被继承、源码享元

**标准回答**

#### **String常用方法**

String类包含了大量处理字符串的方法,包括charAt(),indexOf(),lastIndexOf(),substring(),split(),trim(),toUpperCase(),startsWith()等。

#### **创建字符串的两种方式**

创建字符串有两种方式，一种是使用字符串直接量，另一种是使用new+构造器。采用new的方式会多创建出一个对象来，占用了更多的内存 ，所以**建议采用直接量的方式来创建字符串。**

-   **字符串直接量创建：**JVM会使用常量池来管理这个字符串；
-   **new创建：**JVM会先使用常量池来管理字符串直接量（若已有此字符串则直接返回引用，若没有则实例化后再返回引用），再调用String类的构造器来创建一个新的String对象，新创建的String对象会被保存在堆内存中。

#### 源码（JDK8）

**最终类**：类名用final修饰，代表它不可被继承

> final类不可被继承、final方法不可被重写、final变量不可变。

**私有最终字符数组**： 底层数组用private final修饰，代表这个变量不可变

-   **final：**导致value不能指向新数组（但无法保证value这个引用变量指向的真实数组不可变）
-   **private：**导致value指向的原数组不可变。私有成员变量，且没对外暴露任何修改value的方法，所以value这个引用变量指向的真实数组不可变。

![](https://i-blog.csdnimg.cn/direct/c8e23b65aa24441c840319fa4804e8e9.png)

#### 源码（JDK9）

JDK9开始，为了节省内存，进而减少垃圾回收次数，String底层由char数组改成了byte\[\]。byte变量占1字节，char变量占2字节

> **基本数据类型内存空间**
> 
> 对于基本数据类型，你需要了解每种类型所占据的内存空间，这是面试官喜欢追问的问题：
> 
>  **- byte：1字节（8位）**,数据范围是 \`-2^7 ~ 2^7-1\`。  
>  - short：2字节（16位）,数据范围是 \`-2^15 ~ 2^15-1\`。  
>  - int：4字节（32位）,数据范围是 \`-2^31 ~ 2^31-1\`。  
>  - long：8字节（64位）,数据范围是 \`-2^63 ~ 2^63-1\`。c语言里long占4字节，long long占8字节。  
>  - float：4字节（32位）,数据范围大约是 \`-3.4\*10^38 ~ 3.4\*10^38\`。  
>  - double：8字节（64位）,数据范围大约是 \`-1.8\*10^308 ~ 1.8\*10^308\`。  
>  **- char：2字节（16位）**,数据范围是 \`\\u0000 ~ \\uffff\`，unicode编码英文和中文都占两个字节。c语言使用ASCII编码char占1字节，不能存汉字。ASCII编码是Unicode的一个子集，因此它们存在一些字符码值是相等的。  
>  - boolean：Java规范没有明确的规定,不同的JVM有不同的实现机制。

#### **String类为什么不可被继承**

因为String类是由final修饰的，final类不可被继承。

#### String类为什么要设计成final

-   **防止被继承**：定义成final安全，不能被继承，方法不能重写。保证了对象的不可重复性，防止在用String对象赋值时，该对象被赋值后的对象破坏。
-   **线程安全**：final对象不可被改变，在线程竞争写资源不会产生竞争。
-   **节省空间**：支持字符串常量池，两个字符串定义同样的值，实际上引用的是同一个内存地址空间，这样可以有效节省内存空间。（享元设计模式）

#### **String的字符串为什么不可被变**

 因为String底层**char类型**的value数组是private final修饰的：

-   **final：**导致value不能指向新数组（但无法保证value这个引用变量指向的真实数组不可变）
-   **private：**导致value指向的原数组不可变。私有成员变量，且没对外暴露任何修改value的方法，所以value这个引用变量指向的真实数组不可变。

JDK9开始，为了节省内存，进而减少垃圾回收次数，String底层由char数组改成了byte\[\]。 

**不可变的优点：**因为压根不会被改，所以线程安全、节省空间、效率高。

####  **String源码有用到什么设计模式？**

享元设计模式：当一个系统中存在大量重复对象，若这些重复的对象是不可变对象，就能利用享元模式将对象设计成享元，在内存中只保留一份实例，供引用。这就减少内存中对象的数量，最终节省内存。享元模式是结构型设计模式，用于对象的创建。

#### **享元模式和单例模式区别**

-   单例模式是类级别的，一个类只能有一个对象实例；
-   享元模式是对象级别的，一个类可以有多个不同的对象实例，主要为了解决重复对象问题，池技术一般是用享元模式实现的，例如字符串常量池、数据库连接池、缓冲池。
-   单例模式可以看作是享元模式的一种特立，享元模式只有一种对象实例时就是单例，有多种不重复的对象实例时就是享元。享元模式主要是为了节约内存空间，提高系统性能，而单例模式主要为了可以共享数据；

> **直接量是指在程序中通过源代码直接给出的值**。
> 
> String类是Java最常用的API,它包含了大量处理字符串的方法,比较常用的有：
> 
> -   \- char charAt(int index)：返回指定索引处的字符；
> -   \- String substring(int beginIndex, int endIndex)：从此字符串中截取出一部分子字符串；
> -   \- String\[\] split(String regex)：以指定的规则将此字符串分割成数组；
> -   \- String trim()：删除字符串前导和后置的空格；
> -   \- int indexOf(String str)：返回子串在此字符串首次出现的索引；
> -   \- int lastIndexOf(String str)：返回子串在此字符串最后出现的索引；
> -   \- boolean startsWith(String prefix)：判断此字符串是否以指定的前缀开头；
> -   \- boolean endsWith(String suffix)：判断此字符串是否以指定的后缀结尾；
> -    - String toUpperCase()：将此字符串中所有的字符大写；
> -    - String toLowerCase()：将此字符串中所有的字符小写；
> -    - String replaceFirst(String regex, String replacement)：用指定字符串替换第一个匹配的子串；
> -    - String replaceAll(String regex, String replacement)：用指定字符串替换所有的匹配的子串。
> 
>  **验证常量池：**
> 
> ```java
> //比较地址
> //只要new，就在堆内存开辟空间。直接赋值字符串在常量池里。
>         //常量池里无“hello”对象，创建“hello”对象，str1指向常量池“hello”对象。
>         String str1 = "hello";        
> //先检查字符串常量池中有没有"hello"，如果字符串常量池中没有，则创建一个，然后 str1 指向字符串常量池中的对象，如果有，则直接将 str1 指向"hello"；
>         //常量池里有“hello”对象，str2直接指向常量池“hello”对象。
>         String str2 = "hello";
>         //堆中new创建了一个对象。假如“hello”在常量池中不存在，Jvm还会常量池中创建这个对象“hello”。
>         String str3 = new String("hello");   
>         String str4 = new String("hello");
>         //下面输出true，因为str1和str2指向的是常量池中的同一个内存地址
>         System.out.println(str1 == str2);
>         //下面输出false，str1常量池旧地址，str3是new出的新对象，指向一个全新的地址
>         System.out.println(str1 == str3);
>         //下面输出false，因为它们引用不同
>         System.out.println(str4 == str3);
> 
> //比较内容
>         //下面输出true，因为String类的equals方法重写过，比较的是字符串值
>         System.out.println(str4.equals(str3));
> ```
> 
> 结果：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/44cc29c4bc2dba08d79c904cf66c7068.png)

### 3.3.new String("abc")创建了几个字符串对象？

> 答案、原理 

**答案：**一个或两个。

首先，new string 这边由于 new 关键字，所以这边肯定会在堆中**直接创建一个**字符串对象。

其次，**如果**字符串常量池中不存在 "abc"（通过equals比较）这个字符串的引用，则会在字符串常量池中**创建一个**字符串对象。如果已存在则不创建。注意这边说的在字符串常量池创建对象，最终对象还是在堆中创建，字符串常量池只放引用。

### 3.4.String、StringBuffer、Stringbuilder有什么区别

> **得分点**
> 
> 是否可变、复用率、效率、线程安全问题

**标准回答**

**String:**不可变字符序列，效率低，但是复用率高、线程安全。

不可变是指String对象创建之后,直到这个对象销毁为止,对象中的字符序列都不能被改变。

复用率高是指String类型对象创建出来后归常量池管，可以随时从常量池调用同一个String对象。StringBuffer和StringBuider在创建对象后一般要转化成String对象才调用。

**StringBuffer和StringBuilder**StringBuffer和Stringbuilder都是字符序列可变的字符串，方法也一样，有共同的父类AbstractStringBuilder。 

-   **StringBuffer:**可变字符序列、效率较高(增删)、线程安全
-   **StringBuilder:**可变字符序列、效率最高、线程不安全

> Java中提供了String,StringBuffer两个类来封装字符串,并且提供了一系列方法来操作字符串对象。
> 
> String是一个不可变类,也就是说,一个String对象创建之后,直到这个对象销毁为止,对象中的字符序列都不能被改变。
> 
> **StringBuffer**对象则代表一个字符序列可变的字符串,当一个StringBuffer对象被创建之后,我们可以通过StringBuffer提供的**append()、insert()、reverse()、setCharAt()、setLength()**、等方法来改变这个字符串对象的字符序列。当通过StringBuffer得到期待中字符序列的字符串时,就可以通过toString()方法将其转换为String对象。
> 
> StringBuilder类是JDK1.5中新增的类,他也代表了字符串对象。和StringBuffer类相比,它们有共同的父类\`AbstractStringBuilder\`,二者无论是构造器还是方法都基本相同,不同的一点是,**StringBuilder没有考虑线程安全问题,**也正因如此,StringBuilder比StringBuffer**性能略高**。因此,如果是在单线程下操作大量数据,应优先使用StringBuilder类；如果是在多线程下操作大量数据,应优先使用StringBuilder类。

## 四、集合 

### 4.1.请说说你对Java集合的了解

> **得分点**
> 
> Set、List、Quque、Map、Collection接口、线程安全的集合

**标准回答**

Java中的集合类分为4大类,分别由4个接口来代表,它们是Set、List、Queue、Map。其中,Set、List、Queue接口都继承自Collection接口，Map接口不继承自其他接口。

**Set**代表**无序的、元素不可重复**的集合。

**List**代表**有序的、元素可以重复**的集合。有序说的是元素顺序直接由插入顺序决定。

**Queue**代表**先进先出**（FIFO）的队列。

**Map**代表具有**映射关系**（key-value）的集合。

Java提供了众多集合的实现类,它们都是这些接口的直接或间接的实现类,其中比较常用的有：HashSet、TreeSet、ArrayList、LinkedList、ArrayDeque、HashMap、TreeMap等。这些集合都是线程不安全的。

**线程安全的集合：**

1.  **Collections工具类：**Collections工具类的synchronizedXxx()方法，将ArrayList等集合类包装成线程安全的集合类。例如List<String> synchronizedList = Collections.synchronizedList(list);
2.  **古老api：**java.util包下性能差的古老api，如Vector、Hashtable，它们在JDK1就出现了，不推荐使用，因为线程安全的方案不成熟，性能差。
3.  **降低锁粒度的并发容器：**JUC包下Concurrent开头的、以降低锁粒度来提高并发性能的容器，如ConcurrentHashMap。适用于读写操作都很频繁的场景。
4.  **复制技术实现的并发容器：**JUC包下以CopyOnWrite开头的、采用写时写入时复制技术实现的并发容器，如CopyOnWriteArrayList。写操作时，先将当前数组进行一次复制，对复制后的数组进行操作，操作完成后再将原来的数组引用指向复制后的数组。避免了并发修改同一数组的线程安全问题。适用于读操作比写操作频繁且数据量不大的场景。适用于读操作远多于写操作的场景。

> ```java
> List list = Collections.synchronizedList(new ArrayList());
> ```
> 
> 上面所说的集合类的接口或实现,都位于**java.util包下**,这些实现大多数都是**非线程安全的**。虽然非线程安全,但是这些类的性能较好。如果需要使用**线程安全的集合类**,则可以利用**Collections工具类**,该工具类提供的**synchronizedXxx()方法**,可以将这些集合类包装成线程安全的集合类。
> 
> java.util包下的集合类中,也有少数的线程安全的集合类,例如Vector、Hashtable,它们都是非常古老的API。虽然它们是线程安全的,但是性能很差,已经不推荐使用了。
> 
> 从JDK1.5开始,并发包下新增了大量高效的并发的容器,这些容器按照实现机制可以分为三类。
> 
> 第一类是以降低锁粒度来提高并发性能的容器,它们的类名以Concurrent开头,如ConcurrentHashMap。
> 
> 第二类是采用写时复制技术实现的并发容器,它们的类名以CopyOnWrite开头,如CopyOnWriteArrayList。
> 
> 第三类是采用**Lock实现的阻塞队列**,内部创建两个Condition分别用于生产者和消费者的等待,这些类都实现了BlockingQueue接口,如ArrayBlockingQueue。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/3ee80d3136f2c94dc165355a945fe239.png)

### 4.2.请你说说List与Set的区别

> **得分点**
> 
> Collection接口、有序性和重复性、TreeSet有序

**标准回答** 

List和Set都是Collection接口的子接口,它们的主要区别在于元素的**有序性和重复性**：

**List**代表**有序可以重复**的集合,集合中每个元素都有对应的**顺序索引**,它默认按元素的添加顺序设置元素的索引,并且可以通过索引来访问指定位置的集合元素。另外,List允许使用重复元素。

**Set**代表**无序不可重复**的集合，无序是指存取顺不是按照添加顺序。Set集合不允许包含相同的元素，如果试图把两个相同的元素加入同一个Set，则会引发失败，添加方法将会返回false。通过hashCode值来判断重复元素。

**加分回答-TreeSet支持自然有序和定制排序**

虽然Set代表无序的集合,但是它有支持排序的实现类,即TreeSet。TreeSet可以确保集合元素处于排序状态,并支持自然排序和定制排序两种排序方式,它的**底层是由TreeMap实现的**。TreeSet也是非线程安全的,但是它内部元素的值**不能为null。**

### 4.3.说说你对ArrayList的理解

> **得分点**
> 
> 数组实现、默认容量10、每次扩容1.5倍、缩容、迭代器ListIterator

**标准回答**

**数组实现：**

ArrayList是**基于数组实现的**,它的内部封装了一个**Object\[\]数组**。 通过**默认构造器**创建容器时,该数组先被**初始化为空数组**,之后在**首次添加数据**时再将其初始化成**长度为10的数组**。我们也可以使用有参构造器来创建容器,并通过参数来显式指定数组的容量,届时该数组被初始化为指定容量的数组。

**每次扩容1.5倍：**

如果向ArrayList中添加数据会造成超出数组长度限制,则会触发**自动扩容**,然后再添加数据。扩容就是**数组拷贝**,将**旧数组中的数据拷贝到新数组**里,而新数组的长度为原来**长度的1.5倍**。

**手动缩容：**

ArrayList支持缩容,但**不会自动缩容**,即便是ArrayList中只剩下少量数据时也不会主动缩容。如果我们希望缩减ArrayList的容量,则需要自己调用它的**trimToSize()方法**,届时数组将按照元素的实际个数进行缩减，底层也是通过创建新数组拷贝实现的。

**迭代器ListIterator：**

Set、List、Queue都是Collection的子接口,它们都继承了父接口的iterator()方法,从而具备了迭代的能力。Map使用迭代器必须通过先entrySet()转为Set，然后再使用迭代器或for遍历。

但是,相比于另外两个接口,**List**还单独提供了**listIterator()方法**,增强了迭代能力。iterator()方法返回Iterator迭代器,listIterator()方法返回ListIterator迭代器,并且**ListIterator是Iterator的子接口**。ListIterator在Iterator的基础上,增加了listIterator.previous()**向前遍历**的支持,增加了listIterator.set()在**迭代过程中修改数据**的支持。

**排序方法：**

-   **Collections工具类的sort()方法：**Collections.sort(list);
-   **stream流：**list.stream().sort();
-   **比较器：**list.sort(new Comparator<Integer>() {})
-   **手写排序：**冒泡排序、选择排序、插入排序、二分法排序、快速排序、堆排序。

> entrySet() 
> 
> ```java
>         HashMap<String,String> map=new HashMap<String,String>();
>         map.put("aaa","bbb");map.put("cc","dd");map.put("e","f");
>         Set<Map.Entry<String,String>> set=map.entrySet();
>         for(Map.Entry<String,String> i:set){
>             System.out.println(i.getKey()+i.getValue());
>         }
> ```
> 
> listIterator()
> 
> ```java
>         List<String> list = new ArrayList<String>();
>         list.add(1);
>         //迭代器
>         Iterator<String> it=list.iterator();
>         while(it.hasNext()) System.out.println(it.next());
>         // 使用ListIterator向前遍历并修改元素
>         ListIterator<Integer> listIterator = list.listIterator(list.size());
>         while (listIterator.hasPrevious()) {
>             int num = listIterator.previous();
>             listIterator.set(num + 1);
>         }
> ```

### 4.4.请你说说ArrayList和LinkedList的区别

> **得分点**
> 
> 数据结构（数组和链表）、访问增删效率、时间复杂度、内存占用率

**标准回答**

直接对比数组和链表的空间复杂度、对比插删查的时间复杂度、即可。

1\. ArrayList的实现是基于数组,**LinkedList**的实现是**基于双向链表**。

2\. 对于随机访问ArrayList要优于LinkedList,ArrayList可以根据下标以O(1)时间复杂度对元素进行随机访问,而LinkedList的每一个元素都依靠地址指针和它后一个元素连接在一起,查找某个元素的时间复杂度是O(N)。

3\. 对于插入和删除操作,LinkedList要优于ArrayList,因为当元素被添加到LinkedList任意位置的时候,不需要像ArrayList那样重新计算大小或者是更新索引。list首部、中间插删时ArrayList时间复杂度O(n)，因为要移动后面的元素，LinkedList时间复杂度O(1)，不需要移动。list尾部插删时两者时间复杂度都是O(1)，因为LinkedList是双向链表，有尾结点的指针。 

4\. **LinkedList比ArrayList更占内存**,因为LinkedList的节点除了存储数据,还存储了两个引用,一个指向前一个元素,一个指向后一个元素。 

**自然有序时间复杂度：**如果两者自然有序，ArrayList可以使用二分查找，时间复杂度O(logn)，LinkedList可以使用跳跃表，时间复杂度O(logn)。Redis的zset底层是采用压缩列表或跳跃表。

> **跳跃表：**链表基础上增加多级索引，跳跃查找：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/00f55c4aa0bd18526884fcd536ec87a9.png)

### 4.5.请你说说HashMap底层原理

> **得分点**
> 
> 底层数据结构、哈希表处理冲突、扩容机制、put()流程、为什么2的指数扩容、死循环问题
> 
> **关键字：**数组初始16、负载因子0.75、2的指数扩容、链表头结点地址、链表长度8、红黑树、hash&(2^n-1）

**标准回答** 

HashMap是线程不安全的，多线程环境下建议使用Collections工具类和JUC包的ConcurrentHashMap。

##### **底层数据结构**

-   **JDK7：**HashMap底层是采用“数组+单向链表”来实现的。数组用作哈希查找，链表用作链地址法**头插法**处理冲突。
-   **JDK8：**HashMap底层是采用“数组+单向链表+**红黑树**”来实现的。数组用作哈希查找，链表用作链地址法**尾插法**处理冲突，链表长度为8时转为红黑树。

##### HashMap是否允许重复？

key本质上是不能重复，如果两个value的key相同，到时候就无法准确读取value值了

但本质上相同不代表“表面上”不可以相同，当HashMap元素是类时，HashMap判断两个元素是否重复不是直接通过他们的地址，而是通过该类的重写hashCode()、equals()方法判断两个对象是否是一个对象。

> **示例：**下面Dog类没有重写hashCode()、equals()方法，所以HashMap计算哈希值是通过两个对象的地址，因为地址不同，所以HashMap将两个名字、体重Dog对象认为是两只狗
> 
> ```java
> /**
>  * @Author: vince
>  * @CreateTime: 2024/07/02
>  * @Description: 狗类
>  * @Version: 1.0
>  */
> public class Dog{
>     /**
>      * 体重
>      */
>     public int weight;
>     /**
>      * 名字
>      */
>     public String name;
> 
>     public Dog(int weight, String name) {
>         this.weight = weight;
>         this.name = name;
>     }
> 
>     // @Override
>     // public boolean equals(Object o) {
>     //     Dog dog = (Dog) o;
>     //     return weight == dog.weight && Objects.equals(name, dog.name);
>     // }
>     //
>     // @Override
>     // public int hashCode() {
>     //     return Objects.hash(weight, name);
>     // }
> 
>     @Override
>     public String toString() {
>         return "Dog{" +
>                 "weight=" + weight +
>                 ", name='" + name + '\'' +
>                 '}';
>     }
> }
> ```
> 
> ```java
> /**
>  * @Author: wangming
>  * @CreateTime: 2024/09/10
>  * @Description: 测试类
>  * @Version: 1.0
>  */
> public class Test {
>     public static void main(String[] args) {
>         HashMap<Dog, Integer> dogCountMap = new HashMap<>();
>         dogCountMap.put(new Dog(1, "dog1"), 2);
>         dogCountMap.put(new Dog(1, "dog1"), 2);
>         System.out.println(dogCountMap);
>     }
> }
> ```
> 
> ![](https://i-blog.csdnimg.cn/direct/ac966e3d33bf4969a23a05eb82fc1403.png)

##### **扩容机制** 

HashMap中，数组的默认初始容量为16，这个容量会以2的指数进行扩容。具体来说，当数组中的元素达到一定比例的时候HashMap就会扩容，这个比例叫做负载因子，默认为0.75。

自动扩容机制，是为了保证HashMap初始时不必占据太大的内存，而在使用期间又可以实时保证有足够大的空间。采用2的指数进行扩容，是为了利用位运算，提高扩容运算的效率。

数组每个元素存的是链表头结点地址，链地址法处理冲突，若链表的长度达到了8，红黑树代替链表。

##### **put()流程**

put()方法的执行过程中,主要包含四个步骤：

1.  计算key存取位置，与运算hash&(2^n-1），实际就是哈希值取余，位运算效率更高。
2.  判断数组，若发现数组为空，则进行首次扩容为初始容量16。
3.  判断数组存取位置的头节点，若发现头节点为空，则新建链表节点，存入数组。
4.  判断数组存取位置的头节点，若发现头节点非空，则看情况将元素覆盖或插入链表（JDK7头插法，JDK8尾插法）、红黑树。
5.  插入元素后，判断元素的个数，若发现超过阈值则以2的指数再次扩容。

其中，第3步又可以细分为如下三个小步骤：

1\. 若元素的key与头节点的key一致，则直接覆盖头节点。

2\. 若元素为树型节点，则将元素追加到树中。

3\. 若元素为链表节点，则将元素追加到链表中。追加后，需要判断链表长度以决定是否转为红黑树。若链表长度达到8、元素个数未达到64，则扩容。若链表长度达到8、元素个数达到64，则转为红黑树。

**哈希表处理冲突：**开放地址法（线性探测、二次探测、再哈希法）、链地址法

##### **HashMap容量为什么是2的n次方？**

**主要有以下两个原因：** 

-   **提高性能**：当n是2的幂次方时，散列公式(n - 1) & hash的结果等于hash%n。位运算比取余快，扩容时只需左移一位。
    -   例如2^n-1和2^(n+1)-1的二进制除了第一位，后几位都是相同的。扩容后只需要左移一次。例如15的二进制为1111，31的二进制为11111，63的二进制为111111，127的二进制为1111111。
-   **使元素均匀分布在底层数组**：以2的指数扩容，可以保证每次扩容后，索引值改变的元素都移动到新增加的位置，而不会再移动到旧数组上的位置，可以减少哈希碰撞。

> **例如：**从2^4扩容成2^5，取余公式key&(2^n-1)=index，index是要存储在数组的下标。
> 
> 0&(2^4-1)=0；0&(2^5-1)=0
> 
> 16&(2^4-1)=0；16&(2^5-1)=16。所以扩容后，key为0的一部分value位置没变，一部分value迁移到扩容后的新位置。
> 
> 1&(2^4-1)=1；1&(2^5-1)=1
> 
> 17&(2^4-1)=1；17&(2^5-1)=17。所以扩容后，key为1的一部分value位置没变，一部分value迁移到扩容后的新位置。

##### **JDK7扩容时死循环问题**

单线程扩容流程：JDK7中，HashMap链地址法处理冲突时采用头插法，在扩容时依然头插法，所以链表里结点顺序会反过来。

假如有T1、T2两个线程同时对某链表扩容，他们都标记头结点和第二个结点，此时T2阻塞，T1执行完扩容后链表结点顺序反过来，此时T2恢复运行再进行翻转就会产生环形链表，即B.next=A; A.next=B，从而死循环。

![](https://i-blog.csdnimg.cn/blog_migrate/b87febbd1cf67ce4ab62b727ae125a2b.jpeg)

##### **JDK8 尾插法**

JDK8中，HashMap采用尾插法，扩容时链表节点位置不会翻转，解决了扩容死循环问题，但是性能差了一点，因为要遍历链表再查到尾部。 

##### **JDK8 put时数据覆盖问题**

HashMap非线程安全，如果两个并发线程插入的数据hash取余后相等，就可能出现数据覆盖。

线程A刚找到链表null位置准备插入时就阻塞了，然后线程B找到这个null位置插入成功。借着线程A恢复，因为已经判过null，所以直接覆盖插入这个位置，把线程B插入的数据覆盖了。

```java
    final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        if ((p = tab[i = (n - 1) & hash]) == null)     // 如果没有 hash 碰撞，则直接插入
            tab[i] = newNode(hash, key, value, null);
    }
```

##### **modCount非原子性自增问题**

put会执行modCount++操作（modCount是HashMap的成员变量，用于记录HashMap被修改次数），这步操作分为读取、增加、保存，不是一个原子性操作，也会出现线程安全问题。 

**线程安全解决方案：**

-   使用Hashtable（古老api不推荐）
-   使用Collections工具类，将HashMap包装成线程安全的HashMap。
    
    ```java
    Collections.synchronizedMap(map);
    ```
    
-   使用更安全的ConcurrentHashMap（推荐），ConcurrentHashMap通过对槽（链表头结点）加锁，以较小的性能来保证线程安全。
-   使用synchronized或Lock加锁HashMap之后，再进行操作，相当于多线程排队执行（比较麻烦，也不建议使用）。

> HashMap是**基于哈希算法来确定元素的位置**（槽）的,当我们向集合中存入数据时,它会计算传入的Key的哈希值,并利用**哈希值取余**来确定槽的位置。如果元素发生碰撞,也就是这个槽已经存在其他的元素了,则HashMap会通过链表将这些元素组织起来（**链地址法处理冲突**）。如果碰撞进一步加剧,某个**链表的长度达到了8**,则HashMap会创建**红黑树来代替这个链表**,从而提高对这个槽中数据的查找的速度。
> 
> 向HashMap中添加数据时,有三个条件会触发它的扩容行为：
> 
> 1\. 如果数组为空,则进行首次扩容。
> 
> 2\. 将元素接入链表后,如果链表长度达到8,并且数组长度小于64,则扩容。
> 
> 3\. 添加后,如果数组中元素超过阈值,即比例超出限制（默认为0.75）,则扩容。 并且,每次扩容时都是将容量翻倍,即创建一个2倍大的新数组,然后再将旧数组中的数组迁移到新数组里。由于HashMap中数组的容量为2^N,所以可以用位移运算计算新容量,效率很高。
> 
> **加分回答-HashMap是非线程安全**
> 
> HashMap是非线程安全的,在多线程环境下,多个线程同时触发HashMap的改变时,有可能会发生冲突。所以,在多线程环境下不建议使用HashMap,可以考虑使用Collections将HashMap转为线程安全的HashMap,更为推荐的方式则是使用ConcurrentHashMap。
> 
> **红黑树：** 近似平衡二叉树，左右子树高差有可能大于 1，查找效率略低于平衡二叉树，但增删效率高于平衡二叉树，适合频繁插入删除。
> 
> -   结点非黑即红；
> -   根结点是黑色，叶节点是黑色空节点（常省略）；
> -   任何相邻节点不能同时为红色；
> -   从任一结点到其每个叶子的所有路径都包含相同数目的黑色结点；
> -   查询性能稳定O(logN)，高度最高2log(n+1)；  
>      

##### 源码

-   **元素：**HashMap的链表元素对应的是一个静态内部类Entry，Entry主要包含key，value，next三个元素
    
-   **put()：**通过hash%Entry.length计算index，此时记作Entry\[index\]=该元素。如果index相同就是新入的元素放置到Entry\[index\]，原先的元素记作Entry\[index\].next
    
-   **get()**：先遍历数组，再遍历链表元素。
    
-   **空键**：null key总是放在Entry数组的第一个元素
    
-   **再散列rehash的过程：**确定容量超过目前哈希表的容量，重新调整table 的容量大小，当超过容量的最大值时，取Integer.MAX\_VALUE，即2^31-1
    

### 4.6.请你说说ConcurrentHashMap

> **得分点**
> 
> 数组+链表+红黑树、锁的粒度、实现机制、多线程并发动态扩容、(数组长度 >>> 3) / CPU核心数、CAS

**标准答案** 

ConcurrentHashMap是在JUC（_Java.util.concurrent_）_并发包_下的一个类,它相当于是一个线程安全的HashMap。 

**数组+链表+红黑树：**ConcurrentHashMap的底层数据结构与HashMap一样,也是采用“数组+链表+红黑树”

**锁的粒度：**

JDK1.7采用分段锁，锁粒度是分段，JDK1.8采用synchronized+CAS，锁粒度是槽（头节点）

插入和扩容时采用锁定槽（头节点）的方式降低了锁粒度,以较低的性能代价实现了线程安全。

**实现机制：**

1.  初始化数组、初始化头节点、并发扩容搬运数据时，ConcurrentHashMap并没有加锁，而是CAS的方式进行原子替换。
2.  插入数据时，如果该数据是链表头结点则直接CAS，如果不是头结点则对头结点加synchronized锁。
3.  在扩容的过程中，依然支持查找操作。

**插入元素的过程：**  
1.put 时首先通过hash找到对应链表过后,查看是否是第一个 Node，如果是,直接用 CAS原则插入,无需加锁。

2.如果不是链表第一个 Node,则直接用链表第一个 Node 加锁，这里加的锁是synchronized 

**多线程并发扩容：**

当一个线程在插入数据时，若发现数组正在扩容，那么它就会立即参与扩容操作，完成扩容后再插入。

每个线程迁移数量是 ：(数组长度 >>> 3) / CPU核心数。

**CAS：**

不断对变量进行原子性比较和交换（比较内存中值和预期值，如果相等则交换，如果不相等就代表被其他线程改了则重试）。

CAS属于乐观锁，乐观地认为并发不高，所以让线程不断去重试更新。

**优点：**不使用锁，所以性能高。CAS在不使用锁的情况下通过原子性操作变量，实现多线程时的变量同步。

**缺点：**高并发时不断重试导致CPU开销过大。

**ABA问题：**CAS机制本身无法检测变量的值是否被修改过，只关心当前值和预期值。

例如，线程A刚读取完内存中变量值就阻塞，阻塞期间其他线程将变量更新后又恢复，这时线程A恢复，发现变量还是和预期值相等（其实变量已经不是原来那个变量了，它还以为是），就进行交换。

**解决ABA问题：**单靠CAS不能解决ABA问题，要用带版本号的原子引用才能解决。JDK5引入AtomicStampedReference类，解决ABA问题。它有获取当前对象引用、获取当前版本号，cas等方法。

stamped译为贴上邮票的、盖上印章的。

> 底层数据结构的逻辑可以参考HashMap的实现,下面我重点介绍它的线程安全的实现机制。
> 
> 1\. 初始化数组或头节点时,ConcurrentHashMap并没有加锁,而是CAS（比较并交换）的方式进行原子替换（原子操作,基于Unsafe类的原子操作API）。
> 
> **CAS，**compare and swap，目的是在不使用锁的情况下实现多线程之间的**变量同步，保证变量操作的原子性。**解决多线程并行情况下使用锁造成性能损耗的一种机制。CAS属于乐观锁，乐观地认为程序中的并发情况不那么严重，所以让线程不断去重试更新。
> 
> CAS操作包含三个操作数——内存位置（V）、预期原值（A）和新值(B)。**如果内存位置的值与预期原值相匹配，那么处理器会自动将该位置值更新为新值。**否则，处理器不做任何操作。无论哪种情况，它都会在CAS指令之前返回该位置的值。CAS有效地说明了“我认为位置V应该包含值A；如果包含该值，则将B放到这个位置；否则，不要更改该位置，只告诉我这个位置现在的值即可。
> 
> 2\. 插入数据时会进行加锁处理,但锁定的不是整个数组,而是槽中的头节点。所以,ConcurrentHashMap中锁的粒度是槽,而不是整个数组,并发的性能很好。
> 
> 3\. 扩容时会进行加锁处理,锁定的仍然是头节点。并且,支持多个线程同时对数组扩容,提高并发能力。每个线程需先以CAS操作抢任务,争抢一段连续槽位的数据转移权。抢到任务后,该线程会锁定槽内的头节点,然后将链表或树中的数据迁移到新的数组里。
> 
> 4\. **查找数据时并不会加锁**,所以性能很好。另外,在扩容的过程中,依然可以支持查找操作。如果某个槽还未进行迁移,则直接可以从旧数组里找到数据。如果某个槽已经迁移完毕,但是整个扩容还没结束,则扩容线程会创建一个转发节点存入旧数组,届时查找线程根据转发节点的提示,从新数组中找到目标数据。
> 
> **加分回答-ConcurrentHashMap多线程并发扩容**
> 
> ConcurrentHashMap实现线程安全的难点在于多线程并发扩容，即**当一个线程在插入数据时，若发现数组正在扩容，那么它就会立即参与扩容操作**，完成扩容后再插入数据到新数组。
> 
> 在扩容的时候，**多个线程共同分担数据迁移任务**，每个线程负责的**迁移数量是 ：(数组长度 >>> 3) / CPU核心数**。 也就是说，为线程分配的迁移任务，是**充分考虑了硬件的处理能力**的。多个线程依据硬件的处理能力，平均分摊一部分槽的迁移工作。另外，如果计算出来的迁移数量小于16，则强制将其改为16，这是考虑到目前服务器领域主流的CPU运行速度，每次处理的任务过少，对于CPU的算力也是一种浪费。

### 4.7.请你说说HashMap和Hashtable的区别

> **得分点**
> 
> 线程安全、null值、JDK1古老API同步方案不成熟、ConcurrentHashMap

**标准回答**

HashMap和Hashtable都是典型的Map实现,它们的**区别在于是否线程安全,是否可以存入null值。**

 1. **Hashtable**在实现Map接口时保证了**线程安全性**,而HashMap则是非线程安全的。所以,Hashtable的性能不如HashMap,因为为了保证线程安全它**牺牲了一些性能**。

 2. **Hashtable不允许存入null,**无论是以null作为key或value,都会引发异常。而HashMap是允许存入null的,无论是以null作为key或value,都是可以的。

**加分回答-Hashtable是古老api，推荐ConcurrentHashMap**

虽然Hashtable是线程安全的,但仍然不建议在多线程环境下使用Hashtable。因为它是一个古老的API,从Java 1.0开始就出现了,它的同步方案还不成熟,性能不好。如果要在多线程环下使用HashMap,建议使用ConcurrentHashMap。它不但保证了线程安全,也通过降低锁的粒度提高了并发访问时的性能。

## 五、泛型 

### 5.1.请你说说泛型、泛型擦除

> **得分点**
> 
> 泛型概念、范围、泛型擦除、好处、向上转型

**标准回答**

**泛型：**将具体的类型参数化，是一种编程范式，提供了编译时类型安全检测机制。

通过使用泛型，我们可以将数据类型作为参数传递给类、接口或方法，可以在编译时期进行类型检查，避免在运行时期出现类型转换错误。

**泛型的范围：**泛型接口，泛型类（创建对象时再指定具体类型），泛型方法。

**实现方式：**以泛型类举例。我们只需要在类名后面使用尖括号<>将一个符号或多个符号包裹起来，这样在类里面就可以使用该符号代替具体类型了。使用泛型类时，调用者实际传进来什么类型，编译时就会将泛型符号擦除，替换成这个实际类型。泛型符号可以是任意符号，但我们约定使用T、E、K、V等符号。

**泛型擦除：**java的泛型是伪泛型，这是因为java在编译期间，所有的泛型类型都会被擦掉，并转换为普通类型。 

泛型擦除的主要目的是为了向低版本兼容，因为Java泛型是在JDK 1.5之后才引入的特性，为了保证旧有的代码能正常运行，Java编译器采用了泛型擦除来兼容之前的代码。

**对比Object类：**泛型是在编译时泛型擦除和替换实际类型的，而使用Object类会很麻烦，需要经常强制转换。例如List集合里，如果直接声明存Object类的话，存的时候还好，可以通过多态机制直接向上转型，而取的时候就麻烦了，要强转Object类为String等对象，然后才能访问该对象的成员；而且你不知道实际元素到底是String类型还是Integer等其他类型，还要通过i instanceof String判断类型，就更麻烦了。

**泛型的好处：**

1.  **防止运行时报错：**可以在编译时检查类型安全，防止在程序运行期间出现BUG。
2.  **隐式转换：**所有的强制转换都是自动和隐式的，可以提高代码的重用率。

**向上转型：**泛型类或接口可以向上转型为父类，泛型符号不能向上转型。泛型向上转型指的是将一个泛型对象转换为其父类类型或者接口类型的过程。这个过程实际上是将泛型对象的类型参数擦除，重新赋值为其父类或接口类型。

-   ArrayList<T>可以向上转型为List<T>
-   ArrayList<Integer>泛型不可以向上转化为ArrayList<Number>。因为ArrayList<Number>接收ArrayList<float>，但ArrayList< Integer>不可以接收ArrayList< Float>，不能转回来 

除了向上转型，也有向下转型。 

> **泛型类：**
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
> 
> **编译时安全检查：**
> 
> Java在1.5版本中引入了泛型,**在没有泛型之前,每次从集合中读取对象都必须进行类型转换**,而这么做带来的结果就是：如果有人不小心插入了类型错误的对象,那么在运行时转换处理阶段就会出错。
> 
> 在提出**泛型**之后,我们可以告诉编译器集合中接受哪些对象类型。编译器会**自动的为你的插入进行转化,并在编译时告知是否插入了类型错误的对象**。这使程序变得更加安全更加清楚
> 
> **加分回答** **\-向上转型**
> 
> 在Java标准库中的\`ArrayList<t>\`实现了\`List<t>\`接口,它可以向上转型为\`List<t>\`：  
>  
> 
> ```java
> public class ArrayList<t> implements List<t> { ... }
> 
> List<string> list = new ArrayList<string>();
> ```
> 
> 即**类型\`ArrayList<t>\`可以向上转型为\`List<t>\`**。
> 
> **注意：**
> 
> **不能把\`ArrayList<Integer>\`向上转型为\`ArrayList<Number>\`或\`List<Number>\`。** 这是为什么呢？
> 
> **假设**\`ArrayList<Integer>\`可以向上转型为\`ArrayList<Number>\`,观察一下代码：
> 
> ```java
> // 创建ArrayList<integer>类型：
>         ArrayList<Integer> integerList = new ArrayList<>(); // 添加一个Integer：
>         integerList.add(new Integer(123)); // “向上转型”为ArrayList<number>：
>         ArrayList<Number> numberList = integerList; // 添加一个Float,因为Float也是Number：
>         numberList.add(new Float(12.34)); // 从ArrayList<integer>获取索引为1的元素（即添加的Float）：
>         Integer n = integerList.get(1); // ClassCastException!
> ```
> 
> 我们把一个\`ArrayList<integer>\`转型为\`ArrayList<number>\`类型后,这个\`ArrayList<number>\`就可以接受\`Float\`类型,因为\`Float\`是\`Number\`的子类。但是,\`ArrayList<number>\`实际上和\`ArrayList<integer>\`是同一个对象,也就是\`ArrayList<integer>\`类型,它不可能接受\`Float\`类型, 所以在获取\`Integer\`的时候将产生\`**ClassCastException**\`。
> 
> 实际上,编译器为了避免这种错误,根本就不允许把\`ArrayList<integer>\`转型为\`ArrayList<number>\`。

## 六、IO 

### 6.1.请你说说IO多路复用

> **得分点**
> 
> 特点（单线程可以处理多个客户端请求）、优势

**标准回答**

IO多路复用：一个线程处理多个IO操作。

一个线程中同时监听多个文件句柄（文件描述符，标记已打开文件的正整数），一旦有文件就绪（可读或可写）时，会通知应用程序进行读写操作。没有文件句柄就绪时就会阻塞应用程序，从而释放出CPU资源。

-   lO： 在操作系统中，数据在内核态和用户态之间的读写操作。大部分情况下指网络IO。
-   多路：多个IO操作。大部分情况下是指多个TCP连接(多个Socket或者多个Channel)
-   复用：复用同一个线程。
-   IO多路复用：一个线程处理多个IO操作，无需创建和维护过多的进程/线程。
-   文件描述符：写描述符、读描述符、异常描述符

**优势：**系统开销小，不需要创建、维护额外进程或者线程，避免了线程切换带来的开销。

实现I/O多路复用的三种模型：select、poll、epoll。 

**select调用：**底层是数组，通过轮询遍历文件描述符集合的方式监听文件，扫到就绪的文件描述符，通知应用程序读写。跨平台好（几乎所有平台都支持），轮询次数多，效率差（O(n)），内存开销大，支持文件描述符的个数有限。

**poll调用：**底层是单向链表。轮询次数多、系统开销大，不限制文件描述符个数（最大为操作系统最大文件句柄数，1G内存支持10万个句柄）。

**epoll调用：**底层的数据结构为红黑树加链表，红黑树存所有事件，链表存就绪事件，内核查红黑树将就绪事件插入链表，epoll调用通过epoll\_wait函数返回内核的就绪事件列表，通知应用程序读写操作。回调效率高（O(1)），不会随着文件描述符个数增多导致性能下降，不限制文件描述符个数。缺点是只能在Linux工作。

> IO 多路复用其实就是基于 NIO 的基础上加入了事件机制，程序会注册一组 socket 文件描述符给操作系统，然后监视这些 fd 是否有 IO 事件发生，如果有，程序会被通知，IO 多路复用的方式主要有 select、poll、epoll，这三个函数都会进行阻塞，所以可以放在 while(true)循环里使用，不会造成 CPU 的空转。
> 
> 在I/O编程过程中,当需要同时处理**多个客户端接入请求时**,可以利用多线程或者I/O多路复用技术进行处理。I/O多路复用技术通过把多个I/O的阻塞复用到同一个select的阻塞上,从而使得系统在**单线程的情况下可以同时处理多个客户端请求。**
> 
> 与传统的多线程/多进程模型比,I/O多路复用的**最大优势**是**系统开销小**,系统不需要创建新的额外进程或者线程,也不需要维护这些进程和线程的运行,降低了系统的维护工作量,节省了系统资源。
> 
> 目前**支持I/O多路复用**的系统调用有select、pselect、poll、epoll,在Linux网络编程过程中,很长一段时间都使用select做轮询和网络事件通知,然而select的一些固有缺陷导致了它的应用受到了很大的限制,最终Linux不得不在新的内核版本中寻找select的替代方案,最终选择了epoll。
> 
> **epoll调用**
> 
> 在使用epoll调用时，不需要轮询文件描述符集合。相比于select和poll调用需要轮询整个文件描述符集合的方式来等待I/O事件的发生，epoll调用使用**一组专门的系统调用来管理和等待I/O事件**，从而避免了文件描述符集合的轮询，提高了处理效率。
> 
> 具体地说，epoll调用使用了一组系统调用**(epoll\_create、epoll\_ctl和epoll\_wait)**来实现I/O多路复用机制。当应用程序调用epoll\_wait时，内核会等待任何一个被监控的文件描述符上的事件（例如套接字事件、管道事件等）。此时**内核会把就绪的事件记入到内存中的一个事件列表中**，应用程序再通过epoll\_wait函数**返回这个就绪事件列表**。在整个等待过程中，应用程序并不需要自己不停地轮询文件描述符集合，这样可以极大地减少系统调用和CPU资源的占用。
> 
> 总之，epoll调用不需要轮询整个文件描述符集合，这是它相比于select和poll等调用的一个关键优势。因此，在高并发的网络应用程序中，epoll调用更加适用且更加高效。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/0cc659680ce935c07cf092b440acc3e2.png)
> 
> **加分回答-epoll调用对比select**
> 
> epoll与select的原理比较类似,为了克服select的缺点,epoll作了很多重大改进：
> 
> 1\. 支持一个进程打开的socket描述符（FD）不受限制 **select最大的缺陷就是单个进程所打开的FD是有一定限制的**,它由FD\_SETSIZE设置,默认值是1024。对于那些需要支持上万个TCP连接的大型服务器来说显然太少了。可以选择修改这个宏然后重新编译内核,不过这会带来网络效率的下降。我们也可以通过选择多进程的方案（传统的Apache方案）解决这个问题,不过虽然在Linux上创建进程的代价比较小,但仍旧是不可忽视的,另外,进程间的数据交换非常麻烦,对于Java由于没有共享内存,需要通过Socket通信或者其他方式进行数据同步,这带来了额外的性能损耗,增加了程序复杂度,所以也不是一种完美的解决方案。值得庆幸的是,epoll并没有这个限制,它所支持的FD上限是操作系统的最大文件句柄数,这个数字远远大于1024。例如,在1GB内存的机器上大约是10万个句柄左右,具体的值可以通过cat /proc/sys/fs/file- max察看,通常情况下这个值跟系统的内存关系比较大。
> 
> 2\. I/O效率不会随着FD数目的增加而线性下降 传统的select/poll另一个致命弱点就是当你拥有一个很大的socket集合,由于网络延时或者链路空闲,任一时刻只有少部分的socket是“活跃”的,但是select/poll每次调用都会线性扫描全部的集合,导致效率呈现线性下降。epoll不存在这个问题,它只会对“活跃”的socket进行操作-这是因为在内核实现中epoll是根据每个fd上面的callback函数实现的,那么,只有“活跃”的socket才会主动的去调用callback函数,其他idle状态socket则不会。在这点上,epoll实现了一个伪O。针对epoll和select性能对比的benchmark测试表明：如果所有的socket都处于活跃态-例如一个高速LAN环境,epoll并不比select/poll效率高太多；相反,如果过多使用epoll\_ctl,效率相比还有稍微的下降。但是一旦使用idle connections模拟WAN环境,epoll的效率就远在select/poll之上了。
> 
> 3\. 使用mmap加速内核与用户空间的消息传递 无论是select,poll还是epoll都需要内核把FD消息通知给用户空间,如何避免不必要的内存复制就显得非常重要,epoll是通过内核和用户空间mmap同一块内存实现。
> 
> 4\. epoll的API更加简单 包括创建一个epoll描述符、添加监听事件、阻塞等待所监听的事件发生,关闭epoll描述符等。

### 6.2.请你说说BIO、NIO、O

> **得分点**
> 
> 阻塞IO模型、非阻塞IO模型、异步IO模型

**标准回答**

**BIO：阻塞I/O模型，同步并阻塞**。一个线程只能处理一个连接。客户端有连接请求时服务器需要特地启动一个线程处理。

阻塞：如果连接不做事，对应线程会一直被阻塞，导致不必要的线程开销。 

**NIO：非阻塞I/O模型，同步非阻塞**，一个线程通过多路复用器可以处理多个连接（即请求）。客户端发送的连接会通过通道注册到多路复用器上，多路复用器轮询所有就绪的通道处理IO。访问数据都是通过缓冲区操作。IO 多路复用=NIO+事件机制。

三个核心组件：Buffer（缓冲区）、Channel（通道）、Selector（多路复用器）。

非阻塞：一个连接不做事，线程不会被阻塞，可以轮询处理其他连接。

**AIO：异步I/O模型，异步非阻塞**，一个有效请求对应一个线程。应用程序把I/O请求交给os（操作系统）多路复用处理，自己则可以执行其他任务。os处理完后再通知应用程序进行后续处理。

异步：应用程序把IO请求交给os后自己就能做其他事了。

非阻塞：os多路复用处理IO请求。

> 根据UNIX网络编程对I/O模型的分类,UNIX提供了5种I/O模型,分别是阻塞I/O模型、非阻塞I/O模型、I/O复用模型、信号驱动I/O模型、异步I/O模型。
> 
> BIO、NIO、O这五种模型中的三种,它们分别是阻塞I/O模型、非阻塞I/O模型、异步I/O模型的缩写。
> 
> **BIO，阻塞I/O模型（blocking I/O）：**是**最常用**的I/O模型,缺省情形下,所有文件操作都是阻塞的。
> 
> 我们以套接字接口为例来理解此模型,即在进程空间中调用recvfrom,其系统调用直到数据包到达且被复制到应用进程的缓冲区中或者发生错误时才返回,在此期间一直会等待,进程在从调用recvfrom开始到它返回的整段时间内都是被阻塞的,因此被称为阻塞I/O模型。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/295c664feaa97ddc29a34d473cd72741.png)
> 
> **NIO，非阻塞I/O模型（nonblocking I/O）：**recvfrom从应用层到内核的时候,如果该缓冲区没有数据的话,就直接返回一个EWOULDBLOCK错误,一般都对非阻塞I/O模型进行轮询检查这个状态,看内核是不是有数据到来。
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/50d35593a81b477120670f0b00e0e598.png)
> 
> **AIO，异步I/O模型（asynchronous I/O）：**告知内核启动某个操作,并让内核在整个操作完成后（包括将数据从内核复制到用户自己的缓冲区）通知我们。
> 
> 这种模型与信号驱动模型的主要区别是：信号驱动I/O由内核通知我们何时可以开始一个I/O操作,异步I/O模型由内核通知我们I/O操作何时已经完成。
> 
> **加分回答**
> 
> **I/O复用模型（I/O multiplexing）：**Linux提供select/poll,进程通过将一个或多个fd传递给select或poll系统调用,阻塞在select操作上,这样select/poll可以帮我们侦测多个fd是否处于就绪状态。select/poll是顺序扫描fd是否就绪,而且支持的fd数量有限,因此它的使用受到了一些制约。Linux还提供了一个epoll系统调用,epoll使用基于事件驱动方式代替顺序扫描,因此性能更高。当有fd就绪时,立即回调函数rollback。
> 
> **信号驱动I/O模型（signal-driven I/O）：**首先开启套接口信号驱动I/O功能,并通过系统调用sigaction执行一个信号处理函数（此系统调用立即返回,进程继续工作,它是非阻塞的）。当数据准备就绪时,就为该进程生成一个SIGIO信号,通过信号回调通知应用程序调用recvfrom来读取数据,并通知主循环函数处理数据。

### 6.3.请你讲一下Java NIO

> **得分点**
> 
> 同步非阻塞、Buffer、Channel、Selector

**标准回答**

**NIO：非阻塞I/O模型，同步非阻塞**，一个线程通过多路复用器可以处理多个连接（即请求）。客户端发送的连接会通过通道注册到多路复用器上，多路复用器轮询所有就绪的通道处理IO。访问数据都是通过缓冲区操作。JDK1.4出现，底层是IO多路复用的epoll调用。IO 多路复用=NIO+事件机制。

三个核心组件：Buffer（缓冲区）、Channel（通道）、Selector（多路复用器）。

非阻塞：一个连接不做事，线程不会被阻塞，可以轮询处理其他连接。

> ![](https://i-blog.csdnimg.cn/blog_migrate/50d35593a81b477120670f0b00e0e598.png)
> 
> 新的输入/输出（NIO）库是在**JDK 1.4中引入**的。NIO弥补了原来同步阻塞I/O的不足,它在标准Java代码中提供了高速的、面向块的I/O。通过定义包含数据的类,以及通过以块的形式处理这些数据。
> 
> **NIO包含三个核心的组件：Buffer（缓冲区）、Channel（通道）、Selector（多路复用器）。**
> 
> **Buffer**是一个对象,它包含一些**要写入或者要读出的数据**。在NIO类库中加入Buffer对象,体现了新库与原I/O的一个重要区别。在面向流的I/O中,可以将数据直接写入或者将数据直接读到Stream对象中。**在NIO库中,所有数据都是用缓冲区处理的**。在读取数据时,它是直接读到缓冲区中的。在写入数据时,写入到缓冲区中。**任何时候访问NIO中的数据,都是通过缓冲区进行操作。**
> 
> **Channel是一个通道,**可以通过它读取和写入数据,它就像自来水管一样,网络数据通过Channel读取和写入。通道与流的不同之处在于**通道是双向的**,流只是在一个方向上移动而且**通道可以用于读、写或者同时用于读写**。因为Channel是全双工的,所以它可以比流更好地映射底层操作系统的API。特别是在UNIX网络编程模型中,底层操作系统的通道都是全双工的,同时支持读写操作。
> 
> **Selector会不断地轮询注册在其上的Channel,**如果某个Channel上面有新的TCP连接接入、读和写事件,这个**Channel就处于就绪状态,会被Selector轮询出来**,然后通过SelectionKey可以获取就绪Channel的集合,进行后续的I/O操作。**一个多路复用器Selector可以同时轮询多个Channel,**由于JDK使用了epoll()代替传统的select实现,所以它并没有最大连接句柄1024/2048的限制。这也就意味着只需要一个线程负责Selector的轮询,就可以接入成千上万的客户端,这确实是个非常巨大的进步。
> 
> **加分回答**
> 
> Java 7的NIO2提供了异步Channel支持,这种异步Channel可以提供更高效的IO,这种基于异步Channel的IO机制也被称为异步IO（AsynchronousIO）。NIO2为O提供了两个接口和三个实现类,其中AsynchronousSocketChannel和AsynchronousServerSocketChannel是支持TCP通信的异步Channel。

## 七、异常  

### 7.0.说说异常体系

>  Throwable、Error、Exception、编译时异常、RuntimeException、常见的RuntimeException

**Throwable类**

Throwable 是所有异常和错误（Exception 和 Error）的基类，译为可抛出的。

Throwable 最重要的两个方法：

-   **getMessage()：**返回此 throwable 的详细信息字符串。
    
-   **printStackTrace()：**将 throwable 的跟踪栈信息输出到标准错误输出。它包含 throwable 的类名、消息，以及每个方法的调用序列。
    

**Error类**

Java中的Error类表示严重的错误情况，通常由虚拟机或其他底层自身的失效造成的，例如内存溢出、栈溢出，会导致应用程序终止。

通常程序不应该捕获Error，特定情境下可以捕获OutOfMemoryError处理内存溢出问题。使用try-catch-finally块捕获异常，并在finally块中进行资源清理、销毁、报告错误、终止应用程序等操作。

常见的错误包括：

-   **OutOfMemoryError：**内存溢出错误，通常是由于应用程序试图分配比可用内存更多的内存而导致。
-   StackOverflowError：堆栈溢出错误，发生在方法递归调用所需的堆栈空间已经用完的情况下。
-   NoClassDefFoundError：类未找到错误，通常是由于JVM无法找到应用程序尝试使用的某个类而导致。
-   UnsatisfiedLinkError：链接未满足错误，通常是由于调用本地方法时出现的链接问题而导致。

**Exception类** 

Exception的子类包括编译时异常和运行时异常：

-   **编译时异常：**在编译阶段就能检查出来的异常。例如FileNotFoundException、ClassNotFoundException、NoSuchFieldException、NoSuchMethodException、SQLException、ParseException（解析异常）等。如果程序要去处理这些异常，必须显式地使用try-catch语句块或者在方法定义中使用throws子句声明异常。
    
-   **运行时异常：**在运行时才会出现的异常。例如，NullPointerException、ArrayIndexOutOfBoundsException等。这些异常通常是**由程序代码中的逻辑错误引起的，**在编程时不会提示，运行时才报错。 因此，在编写程序时，通常无法处理这些异常，但是在程序开发完毕后，需要对这些异常进行一些处理，以防程序运行时崩溃。
    
    -   NullPointerException **空指针异常**；出现原因：访问未初始化的对象或不存在的对象。
    -   ClassNotFoundException **类找不到异常**；出现原因：类的名称和路径加载错误；
    -   NumberFormatException **数字格式化异常**；出现原因：转数字的字符型中包含非数字型字符。
    -   IndexOutOfBoundsException **索引超出边界异常**；出现原因：访问数组越界元素
    -   IllegalArgumentException **不合法参数异常**。出现原因：传递了不合法参数
    -   MethodArgumentNotValidException **方法参数无效异常**。出现原因：JSR303校验不通过
    -   ClassCastException **类转换异常**。出现原因：把对象强制转为没继承关系对象时报错。这个异常是在类加载过程的元数据验证阶段验证继承关系时报错。
    -   ArithmeticException **算术异常**。出现原因：除以0时。  

![](https://i-blog.csdnimg.cn/blog_migrate/2af2392e506f1d1fa5013ebbcdcbdb47.png)

### 7.1.请你说说Java的异常处理机制

> **得分点**
> 
> 异常处理、禁止finally里throw或return、抛出异常、异常的跟踪栈、统一异常处理

**标准回答** 

Java的异常机制可以分成异常处理、抛出异常和异常跟踪栈的问题三个部分。

**异常处理：**处理异常的语句由try、catch、finally三部分组成。try块用于包裹业务代码，catch用于捕获并处理某个异常，finally块则用于回收资源。

**禁止finally里throw或return：**防止try-catch里抛异常失效。如果在finally里throw或return，会直接退出异常，无法跳回try或catch执行return或throw。正常情况下，当finally块执行完成后,系统才会再次跳回来执行try块或catch块里的return或throw语句。

**抛出异常：**throws只能在方法签名中使用，可以抛多个异常，表示出现异常的一种可能性。throw表示抛出一个确定的异常实例。

**异常的跟踪栈：**

程序出现异常后会打印异常的跟踪栈信息，根据跟踪栈信息我们可以找到异常的位置，并跟踪异常一路向上层方法传播的过程。

异常传播的顺序与方法的调用顺序相反，是从发生异常的方法开始，不断向调用它的上层方法传播，最终传到main方法。若依然没有得到处理，则JVM终止程序，打印异常跟踪栈的信息。

**日志规范不建议使用e.printStackTrace()：**改成log.error("你的程序有异常啦",e);  
日志混乱：e.printStackTrace()打印出的堆栈日志跟业务代码日志是交错混合在一起的，通常排查异常日志不太方便。  
性能问题：printStackTrace()方法会生成大量的字符串对象，对系统性能有一定的影响。  
 

**统一异常处理：**

1.  公共模块创建错误码枚举类，一般为五位数字，前两位代表不同业务场景，后三位表示错误码；
2.  在每个模块异常包下创建异常处理类，类注解  
    @RestControllerAdvice，各异常处理方法注解@ExceptionHandler，处理后返回带错误码的结果类；
3.  实际开发时出现异常或抛出异常就会直接被拦截处理，不用try-catch捕获处理。

> 异常处理机制可以让程序具有极好的容错性和健壮性,当程序运行出现了意料之外的状况时,系统会生成一个**Exception对象**来通知程序,从而实现“业务功能实现部分代码”与“错误处理部分代码”分离,使程序获得更好的可读性。
> 
> Java的异常机制可以分成**异常处理、抛出异常和异常跟踪栈问题**三个部分。
> 
> **异常处理** 
> 
> 处理异常的语句由try、catch、finally三部分组成。try块用于包裹业务代码,catch块用于捕获并处理某个类型的异常,finally块则用于回收资源。如果业务代码发生异常,系统就会创建一个异常对象,并将这个异常对象提交给JVM,然后由JVM寻找可以处理这个异常的catch块,并将异常对象交给这个catch块处理。如果JVM没有找到可以处理异常的catch代码块,那么运行环境会终止,Java程序也会退出。若业务代码打开了某项资源,则可以在finally块中关闭这项资源,因为无论是否发生异常,finally块一定会执行（一般情况下）。
> 
> **抛出异常** 
> 
> 当程序出现错误时,系统会自动抛出异常。除此以外,**Java也允许程序主动抛出异常**。当业务代码中,判断某项错误的条件成立时,可以使用**throw关键字向外抛出异常**。在这种情况下,如果当前方法不知道该如何处理这个异常,可以在方法签名上通过**throws关键字声明抛出异常**,则该异常将**交给JVM处理**。
> 
> **异常跟踪栈**
> 
> 程序运行时,经常会发生一系列方法调用,从而形成方法调用栈。异常机制会导致异常在这些方法之间传播,而**异常传播的顺序与方法的调用相反**。**异常从发生异常的方法向外传播**,首先传给该方法的调用者,再传给上层调用者,以此类推。**最终会传到main方法**,若依然没有得到处理,则JVM会终止程序,并打印异常跟踪栈的信息。
> 
> **示例：**
> 
> ```java
> public class Test {
>     public static void main(String[] args) {
>         fun();
>     }
> 
>     private static void fun() {
>         fun1();
>     }
> 
>     private static void fun1() {
>         System.out.println(6/0);
>     }
> }
> ```
> 
> 先打印出问题的fun1()，再打印调用它的fun2()，再打印调用它的main方法：
> 
> ```java
> Exception in thread "main" java.lang.ArithmeticException: / by zero
> 	at package1.Test.fun1(Test.java:17)
> 	at package1.Test.fun(Test.java:13)
> 	at package1.Test.main(Test.java:9)
> ```
> 
> **加分回答-throw、throws区别,避免在finally块中使用return或throw**
> 
> **throws：**
> 
>  - 只能在方法签名中使用
> 
>  - 可以声明抛出多个异常,多个一场之间用逗号隔开
> 
>  - 表示**当前方法不知道如何处理这个异常**,这个异常由该方法的调用者处理（如果mn方法也不知该怎么处理异常,这个异常就会交给JVM处理,JVM处理异常的方式是,打印异常跟踪栈信息并终止程序运行,这也就是为什么程序遇到异常会自动结束的的原因）
> 
>  - throws表示出现异常的**一种可能性**,并不一定会发生这些异常
> 
> **throw：**
> 
>  - 表示方法内抛出某种异常对象,throw语句可以单独使用。
> 
>  - throw语句**抛出的是一个异常实例**,不是一个异常类,而且**每次只能抛出一个异常实例**
> 
>  - 执行throw**一定抛出**了某种异常
> 
> **避免在finally块中使用return或throw**
> 
> 当Java程序执行try块、catch块时遇到了**return或throw语句**,这两个语句都**会导致该方法立即结束**,但是系统执行这两个语句并不会结束该方法,而是去寻找该异常处理流程中**是否包含finally块**,如果没有finally块,程序立即执行return或throw语句,方法终止；如果有finally块,系统立即开始执行finally块。只有**当finally块执行完成后**,系统才会再次**跳回来执行**try块、catch块里的**return或throw语句**；
> 
> 如果finally块里也使用了return或throw等语句,finally块会终止方法,系统将不会跳回去执行try块、catch块里的任何代码。这将会导致try块、catch块中的return、throw语句失效,所以,我们应该**尽量避免在finally块中使用return或throw。**
> 
> **finally代码块不执行的几种情况：**
> 
>  - 如果当一个线程在执行 try 语句块或者catch语句块时被打断interrupted或者被终止killed,与其相对应的 finally 语句块可能不会执行。
> 
>  - 如果在try块或catch块中使用 \`System.exit(1);\` 来退出虚拟机,则finally块将失去执行的机会。

## 八、反射 

### 8.1.请说说你对反射的了解

> **得分点**
> 
> 反射概念、通过反射机制可以实现、获取Class对象的三种方式、优缺点、应用场景

**反射：**在程序运行期间**动态地获取类的信息并对类进行操作**的机制。

**通过反射机制可以实现：**

-   **获取类或对象的Class对象：**程序运行时,可以通过反射获得任意一个类的Class对象,并通过这个对象查看这个类的所有方法和属性（包括私有，私有需要给该字段调用setAccessible(true)方法开启私有权限）。注意类的class对象是运行时生成的，类的class字节码文件是编译时生成的。
-   **创建实例：**程序运行时,可以利用反射先创建类的Class对象再创建该类的实例,并访问该实例的成员；Xxx.class.newInstance() ;例如在Spring容器类源码里，Bean实例化就是通过Bean类的Class对象。Bean类的Class对象是从BeanDefinition对象的type成员变量取的。BeanDefinition对象存储一些Bean的类型、名称、作用域等声明信息。
-   **生成动态代理类或对象：**程序运行时,可以通过反射机制生成一个类的动态代理类或动态代理对象。例如JDK中Proxy类的newProxyInstance静态方法，可以通过它创建基于接口的动态代理对象。

**获取类Class对象的JVM底层：**如果该类没有被加载过，会首先通过JVM实现类的加载过程，即加载、链接（验证、准备、解析）、初始化，加载阶段会生成类的Class对象。

**获取类Class对象的方法：**dog.getClass();Dog.class;Class.forName("package1.Dog");

**反射的优缺点：**

-   **优点：**
    -   **运行时获取属性：**运行期间能够动态的获取类，提高代码的灵活性。
    -   **访问私有成员：**构造方法、成员变量、方法对象取消访问检查可以访问私有成员；public void setAccessible(boolean flag):值为true，取消访问检查
    -   **越过泛型检查：**反射可以越过泛型检查，例如在ArrayList<Integer>中添加字符串
-   **缺点：性能差。**性能比直接的Java代码要差很多。  

**应用场景：**

-   **JDBC加载数据库的驱动：**使用JDBC时，如果要创建数据库的连接，则需要先通过反射机制加载数据库的驱动程序；
-   **Bean的生命周期：**
    -   **实例化xml解析出的类：**多数框架都支持注解或XML配置来定义应用程序中的类，从xml配置中解析出来的类是字符串，需要利用反射机制实例化；例如Spring通过<bean id="xx" class="类全限定名">和<property name="按名称注入" ref="被注入Bean的id">定义bean，然后通过Class.forName("xxx.Xxx")获取类的class对象，然后创建实例。
    -   **注解容器类加载Bean、实例化Bean：**Bean的生命周期中，注解容器类的构造方法会遍历@ComponentScan("扫描路径")下的.class文件，通过类加载器.load("类名")方式获得类的class对象，存入beanDefinitionMap。然后遍历beanDefinitionMap，通过class对象实例化等。
-   **AOP创建动态代理对象：**面向切面编程（AOP）的实现方案，是在程序运行时创建目标对象的代理对象，这必须由反射机制来实现。 

> **类加载过程：**加载、链接（验证、准备、解析）、初始化。这个过程是在类加载子系统完成的。
> 
> **加载：**生成类的Class对象。
> 
> 1.  通过一个类的全限定名获取定义此类的二进制字节流
> 2.  将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构。包括创建运行时常量池，将类常量池的部分符号引用放入运行时常量池。
> 3.  在内存中生成一个代表这个类的java.lang.Class对象，作为方法区这个类的各种数据的访问入口。注意类的class对象是运行时生成的，类的class字节码文件是编译时生成的。
> 
> **链接：**将类的二进制数据合并到JRE中。该过程分为以下3个阶段：
> 
> -   **验证：**确保代码符合JAVA虚拟机规范和安全约束。包括文件格式验证、元数据验证、字节码验证、符号引用验证。
>     -   **文件格式验证：**验证字节流是否符合Class文件格式规范。例如版本号是否在JVM兼容范围。
>     -   **元数据验证：**元数据是类的全名、方法信息、字段信息、继承关系等。例如验证类名接口名标识符有没有符合规范、有没有实现接口的所有方法、有没有实现抽象类的所有抽象方法、是不是继承了final类等。
>     -   **字节码验证：**对字节码进行验证,保证校验的类在运行时不会做出对JVM危险的行为。例如强制把父类对象强转为子类对象（只有父类引用指向子类对象时才能向下转型）。
>     -   **符号引用验证：**验证引用的对象是否存在，是否有权引用等。
> -   **准备：**为类变量（即static变量）分配内存并赋零值。
> -   **解析：**将方法区-运行时常量池内的符号引用（类的名字、成员名、标识符）转为直接引用（实际内存地址，不包含任何抽象信息，因此可以直接使用）。
> 
> **初始化：**类变量赋初值、执行静态语句块。
> 
> **aop：**
> 
> **一种编程思想，在不改原有代码的前提下对代码进行增强。**
> 
> -   **目标对象(Target)：**原始功能去掉共性功能对应的类产生的对象，这种对象是无法直接完成最终工作的
> -   **代理(Proxy)：**目标对象无法直接完成工作，需要对其进行功能回填，通过原始对象的代理对象实现
> 
> SpringAOP是在不改变原有设计(代码)的前提下对其进行增强的，它的底层采用的是代理模式实现的，所以要对原始对象进行增强，就需要**对原始对象创建代理对象，在代理对象中的方法把通知内容**\[如:MyAdvice中的method方法\]**加进去**，就实现了增强,这就是我们所说的代理(Proxy)。

> **反射**
> 
> Java程序中,许多对象在运行时都会有编译时异常和运行时异常两种,例如多态情况下Car c = new Audi(); 这行代码运行时会生成一个c变量,在编译时该变量的类型是Car,运行时该变量类型为Audi；另外还有更极端的情况,例如程序在运行时接收到了外部传入的一个对象,这个对象的编译时类型是Object,但程序又需要调用这个对象运行时类型的方法,这种情况下,有两种解决方法：
> 
> 第一种做法是假设在编译时和运行时都完全知道类型的具体信息,在这种情况下,可以先使用instanceof运算符进行判断,再利用强制类型转换将其转换成其运行时类型的变量。第二种做法是编译时根本无法预知该对象和类可能属于哪些类,程序只依靠运行时信息来发现该对象和类的真实信息,这就必须使用反射。
> 
> 具体来说,通过反射机制,我们可以实现如下的操作：
> 
> \- 程序运行时,可以通过反射获得任意一个类的Class对象,并通过这个对象查看这个类的信息；
> 
> \- 程序运行时,可以通过反射创建任意一个类的实例,并访问该实例的成员； - 程序运行时,可以通过反射机制生成一个类的动态代理类或动态代理对象。
> 
> **加分回答-反射应用场景**
> 
> Java的反射机制在实际项目中应用广泛,常见的应用场景有：
> 
> \- 使用JDBC时,如果要创建数据库的连接,则需要先通过反射机制加载数据库的驱动程序；
> 
> \- 多数框架都支持注解/XML配置,从配置中解析出来的类是字符串,需要利用反射机制实例化；
> 
> \- 面向切面编程（AOP）的实现方案,是在程序运行时创建目标对象的代理类,这必须由反射机制来实现。 

## 九、多线程

[【2023Java面试八股文】Java多线程篇\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/129446871 "【2023Java面试八股文】Java多线程篇_vincewm的博客-CSDN博客")