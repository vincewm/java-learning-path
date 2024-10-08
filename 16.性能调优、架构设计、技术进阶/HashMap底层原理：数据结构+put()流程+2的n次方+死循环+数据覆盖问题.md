> **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289 "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[一、底层](#%E5%BA%95%E5%B1%82)

[1.1 HashMap数据结构](#%E5%BA%95%E5%B1%82%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)

[1.2 扩容机制](#%E6%89%A9%E5%AE%B9%E6%9C%BA%E5%88%B6)

[1.3 put()流程](#put%28%29%E6%B5%81%E7%A8%8B)

[1.4 HashMap是如何计算key的？](#HashMap%E6%98%AF%E5%A6%82%E4%BD%95%E8%AE%A1%E7%AE%97key%E7%9A%84%EF%BC%9F)

[1.5 HashMap容量为什么是2的n次方？](#HashMap%E5%AE%B9%E9%87%8F%E4%B8%BA%E4%BB%80%E4%B9%88%E6%98%AF2%E7%9A%84n%E6%AC%A1%E6%96%B9%EF%BC%9F)

[1.5.1 原因](#%E6%A6%82%E8%BF%B0%C2%A0)

[1.5.2 扩容均匀散列演示：从2^4扩容成2^5](#%E6%89%A9%E5%AE%B9%E5%9D%87%E5%8C%80%E6%95%A3%E5%88%97%E6%BC%94%E7%A4%BA%EF%BC%9A%E4%BB%8E2%5E4%E6%89%A9%E5%AE%B9%E6%88%902%5E5)

[二、线程安全问题](#%E7%BA%BF%E7%A8%8B%E5%AE%89%E5%85%A8%E9%97%AE%E9%A2%98)

[2.1 HashMap线程安全吗？](#HashMap%E7%BA%BF%E7%A8%8B%E5%AE%89%E5%85%A8%E5%90%97%EF%BC%9F%C2%A0) 

[2.2 线程安全的解决方案](#%E7%BA%BF%E7%A8%8B%E5%AE%89%E5%85%A8%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)

[2.3 JDK7扩容时死循环问题](#JDK7%E6%89%A9%E5%AE%B9%E6%97%B6%E6%AD%BB%E5%BE%AA%E7%8E%AF%E9%97%AE%E9%A2%98)

[2.3.1 死循环问题演示](#%E6%AD%BB%E5%BE%AA%E7%8E%AF%E9%97%AE%E9%A2%98%E6%BC%94%E7%A4%BA%C2%A0) 

[2.3.2 JDK8是怎么解决死循环问题的？](#JDK8%E6%98%AF%E6%80%8E%E4%B9%88%E8%A7%A3%E5%86%B3%E6%AD%BB%E5%BE%AA%E7%8E%AF%E9%97%AE%E9%A2%98%E7%9A%84%EF%BC%9F)

[2.4 JDK8 put时数据覆盖问题](#JDK8%20put%E6%97%B6%E6%95%B0%E6%8D%AE%E8%A6%86%E7%9B%96%E9%97%AE%E9%A2%98)

[2.5 modCount非原子性自增问题](#modCount%E9%9D%9E%E5%8E%9F%E5%AD%90%E6%80%A7%E8%87%AA%E5%A2%9E%E9%97%AE%E9%A2%98)

--

## 一、底层

### **1.1 HashMap数据结构**

JDK1.7及之前版本，HashMap底层是“数组+单向链表”。

在JDK8中,HashMap底层是采用“数组+单向链表+红黑树”来实现的，使用红黑树主要是为了提高查询性能。

-   **数组：**用于实现哈希表，存放HashMap的key；
-   **链表：**存放HashMap的value，用链地址法处理冲突；链表时间复杂度O(n)。
-   **红黑树：**当 链表长度大于等于8, 且数组的长度大于64时，链表转为红黑树，存放HashMap的value。红黑树时间复杂度稳定的O(logn)。

![](https://i-blog.csdnimg.cn/blog_migrate/f927b68778ddb45a7c8da635bcb754ab.png)

> **红黑树：** 近似平衡二叉树，左右子树高差有可能大于 1，查找效率略低于平衡二叉树，但增删效率高于平衡二叉树，适合频繁插入删除。
> 
> -   结点非黑即红；
> -   根结点是黑色，叶节点是黑色空节点（常省略）；
> -   任何相邻节点不能同时为红色；
> -   从任一结点到其每个叶子的所有路径都包含相同数目的黑色结点；
> -   查询性能稳定O(logN)，高度最高2log(n+1)；
> 
>  ![](https://i-blog.csdnimg.cn/blog_migrate/e16334348a5a64d03dae414cbd64469f.png)

### **1.2 扩容机制**

HashMap中，数组的默认初始容量为16，这个容量会以2的指数进行扩容。具体来说，当数组中的元素达到一定比例的时候HashMap就会扩容，这个比例叫做负载因子，默认为0.75。

自动扩容机制，是为了保证HashMap初始时不必占据太大的内存，而在使用期间又可以实时保证有足够大的空间。采用2的指数进行扩容，是为了利用位运算，提高扩容运算的效率。

数组每个元素存的是链表头结点地址，链地址法处理冲突，若链表的长度达到了8，红黑树代替链表。

### **1.3 put()流程**

put()方法的执行过程中,主要包含四个步骤：

1.  计算key存取位置，与运算hash&(2^n-1），实际就是哈希值取余，位运算效率更高。
2.  判断数组，若发现数组为空，则进行首次扩容为初始容量16。
3.  判断数组存取位置的头节点，若发现头节点为空，则新建链表节点，存入数组。
4.  判断数组存取位置的头节点，若发现头节点非空，则看情况将元素覆盖或插入链表（JDK7头插法，JDK8尾插法）、红黑树。
5.  插入元素后，判断元素的个数，若发现超过阈值则以2的指数再次扩容。

其中，第3步又可以细分为如下三个小步骤：

1\. 若元素的key与头节点的key一致，则直接覆盖头节点。

2\. 若元素为树型节点，则将元素追加到树中。

3\. 若元素为链表节点，则将元素追加到链表中。追加后，需要判断链表长度以决定是否转为红黑树。若链表长度达到8、数组容量未达到64，则扩容。若链表长度达到8、数组容量达到64，则转为红黑树。

**哈希表处理冲突：**开放地址法（线性探测、二次探测、再哈希法）、链地址法

### **1.4 HashMap是如何计算key的？**

```bash
key=value&(2^n-1) #结果相当于value%(2^n)，使用位运算只要是为了提高计算速度。
```

例如当前数组容量是16，我们要存取18，那么就可以用18&15==2。相当于18%16==2.

> put()里，计算key的部分源码：
> 
> ```java
> final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
>                    boolean evict) {
>         // 此处省略了代码
>         // i = (n - 1) & hash]
>         if ((p = tab[i = (n - 1) & hash]) == null)
>             
>             tab[i] = newNode(hash, key, value, null);
>         
>  
>         else {
>             // 省略了代码
>         }
> }
> ```

### **1.5 HashMap容量为什么是2的n次方？**

#### 1.5.1 原因

计算value对应key的Hash运算：

```bash
key=value&(2^n-1）#结果相当于value%(2^n)。例如18&15和18%16值是相等的
```

2^n-1和2^(n+1)-1的二进制除了第一位，后几位都是相同的。这样可以使得添加的元素均匀分布在HashMap的每个位置上，防止哈希碰撞。

例如15（即2^4-1）的二进制为1111，31的二进制为11111，63的二进制为111111，127的二进制为1111111。

#### **1.5.2 扩容均匀散列演示：从2^4扩容成2^5**

0&(2^4-1)=0；0&(2^5-1)=0

16&(2^4-1)=0；16&(2^5-1)=16。所以扩容后，key为0的一部分value位置没变，一部分value迁移到扩容后的新位置。

1&(2^4-1)=1；1&(2^5-1)=1

17&(2^4-1)=1；17&(2^5-1)=17。所以扩容后，key为1的一部分value位置没变，一部分value迁移到扩容后的新位置。

> **用取余演示扩容：**
> 
> 如果觉得与运算有点难理解，我们可以用取余演示：
> 
> 假设从16扩容到32：1%16=1,17%16=1；1%32=1,17%32=17。
> 
> 1和17本来key都是1，扩容后1的key还是1，17的key变成17。这样原来key为1的value就均匀的散列在扩容后的哈希表里了（一部分value不变，一部分value移动到扩容后新位置）。

## 二、线程安全问题

### 2.1 HashMap线程安全吗？ 

HashMap是线程不安全的，多线程环境下可能出现死循环问题、数据覆盖问题。

多线程下建议使用Collections工具类和JUC包的ConcurrentHashMap。

### **2.2 线程安全的解决方案**

-   使用Hashtable（古老api不推荐）
-   使用Collections工具类，将HashMap包装成线程安全的HashMap。
    
    ```java
    Collections.synchronizedMap(map);
    ```
    
-   使用更安全的ConcurrentHashMap（推荐），ConcurrentHashMap通过对槽（链表头结点）加锁，以较小的性能来保证线程安全。
-   使用synchronized或Lock加锁HashMap之后，再进行操作，相当于多线程排队执行（比较麻烦，也不建议使用）。

### **2.3 JDK7扩容时死循环问题**

#### **2.3.1 死循环问题演示** 

单线程扩容流程：

JDK7中，HashMap链地址法处理冲突时采用头插法，在扩容时依然头插法，所以链表里结点顺序会反过来。

假如有T1、T2两个线程同时对某链表扩容，他们都标记头结点和第二个结点，此时T2阻塞，T1执行完扩容后链表结点顺序反过来，此时T2恢复运行再进行翻转就会产生环形链表，即B.next=A; A.next=B，从而死循环。

![](https://i-blog.csdnimg.cn/blog_migrate/02ac37229afadfc9aca780f9a167eec2.png)

#### 2.3.2 JDK8是怎么解决死循环问题的？

**JDK8 尾插法解决了死循环问题。**

JDK8中，HashMap采用尾插法，扩容时链表节点位置不会翻转，解决了扩容死循环问题，但是性能差了一点，因为要遍历链表再查到尾部。 

例如A——>B——>C要迁移，迁移时先移动头结点A，再移动B并插入A的尾部，再移动C插入尾部，这样结果还是A——>B——>C。顺序没变，扩容线程

### **2.4 JDK8 put时数据覆盖问题**

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

### **2.5 modCount非原子性自增问题**

modCount： HashMap的成员变量，用于记录HashMap被修改次数

put会执行modCount++操作，这步操作分为读取、增加、保存，不是一个原子性操作，也会出现线程安全问题。 

```java
    final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
//put会执行modCount++操作，这步操作分为读取、增加、保存，不是一个原子性操作，也会出现线程安全问题。 
        ++modCount;
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }
```