>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[0\. tab键：代码补全](#0.%20tab%E9%94%AE%EF%BC%9A%E4%BB%A3%E7%A0%81%E8%A1%A5%E5%85%A8)

[1\. ls：列出文件列表list](#1.%20ls%EF%BC%9A%E5%88%97%E5%87%BA%E6%96%87%E4%BB%B6%E5%88%97%E8%A1%A8list)

[2\. cd：切换目录change directory](#2.%20cd%EF%BC%9A%E5%88%87%E6%8D%A2%E7%9B%AE%E5%BD%95change%20directory)

[3\. cp：复制粘贴文件copy](#3.%20cp%EF%BC%9A%E5%A4%8D%E5%88%B6%E7%B2%98%E8%B4%B4%E6%96%87%E4%BB%B6copy)

[4\. mv：移动move](#4.%20mv%EF%BC%9A%E7%A7%BB%E5%8A%A8move)

[5\. rm：删除文件、目录remove](#5.%20rm%EF%BC%9A%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6%E3%80%81%E7%9B%AE%E5%BD%95remove)

[6\. mkdir：创建目录make directory](#6.%20mkdir%EF%BC%9A%E5%88%9B%E5%BB%BA%E7%9B%AE%E5%BD%95make%20directory)

[7\. rmdir：删除空目录remove directory](#7.%20rmdir%EF%BC%9A%E5%88%A0%E9%99%A4%E7%A9%BA%E7%9B%AE%E5%BD%95remove%20directory)

[8\. chown：更改所有者change owner](#8.%20chown%EF%BC%9A%E6%9B%B4%E6%94%B9%E6%89%80%E6%9C%89%E8%80%85change%20owner)

[9\. chmod：更改文件的权限模式change mode](#9.%20chmod%EF%BC%9A%E6%9B%B4%E6%94%B9%E6%96%87%E4%BB%B6%E7%9A%84%E6%9D%83%E9%99%90%E6%A8%A1%E5%BC%8Fchange%20mode)

[10\. find：查找文件](#10.%20find%EF%BC%9A%E6%9F%A5%E6%89%BE)

[11\. |：管道](#11.%20%7C%EF%BC%9A%E7%AE%A1%E9%81%93)

[12\. grep：查找文件内容，按行查找并匹配](#12.%20grep%EF%BC%9A%E6%8C%89%E8%A1%8C%E6%9F%A5%E6%89%BE%E5%B9%B6%E5%8C%B9%E9%85%8D)

[13\. tar：打包，压缩，解压](#13.%20tar%EF%BC%9A%E6%89%93%E5%8C%85%EF%BC%8C%E5%8E%8B%E7%BC%A9%EF%BC%8C%E8%A7%A3%E5%8E%8B)

[13.3 touch:创建空文件](#13.3%20touch%3A%E5%88%9B%E5%BB%BA%E7%A9%BA%E6%96%87%E4%BB%B6)

[13.6 vim编辑器:创建修改文件](#13.5%20vim%3A%E5%88%9B%E5%BB%BA%E4%BF%AE%E6%94%B9%E6%96%87%E4%BB%B6)

[13.9 clear:清空命令行](#13.9%20clear%3A%E6%B8%85%E7%A9%BA%E5%91%BD%E4%BB%A4%E8%A1%8C)

[14\. cat（more,less,tail）：查看文件，打印文件内容](#14.%20cat%EF%BC%9A%E6%9F%A5%E7%9C%8B%E6%96%87%E4%BB%B6%EF%BC%8C%E6%89%93%E5%8D%B0%E6%96%87%E4%BB%B6%E5%86%85%E5%AE%B9%EF%BC%8Cmore%EF%BC%8Cless)

[15\. ps：查看进程process select](#15.%20ps%EF%BC%9A%E6%9F%A5%E7%9C%8B%E8%BF%9B%E7%A8%8Bprocess%20select)

[16\. kill：杀死进程](#16.%20kill%EF%BC%9A%E6%9D%80%E6%AD%BB%E8%BF%9B%E7%A8%8B)

[17\. passwd：修改密码password](#17.%20passwd%EF%BC%9A%E4%BF%AE%E6%94%B9%E5%AF%86%E7%A0%81password)

[18\. pwd：显示当前目录路径print work directory](#18.%20pwd%EF%BC%9A%E6%98%BE%E7%A4%BA%E5%BD%93%E5%89%8D%E7%9B%AE%E5%BD%95%E8%B7%AF%E5%BE%84print%20work%20directory)

[19\. tee：显示并保存](#19.%20tee%EF%BC%9A%E6%98%BE%E7%A4%BA%E5%B9%B6%E4%BF%9D%E5%AD%98)

[20\. reboot：重启](#20.%20reboot%EF%BC%9A%E9%87%8D%E5%90%AF)

--

## 0\. tab键：代码补全

例如输入文件夹cd con，按tab键可以自动补全成该目录下config。

## 1\. ls：列出文件列表list

**ls**命令是**列出目录内容**(List Directory Contents)的意思。

“**ls -l”**，简写成**ll**。命令以**详情模式**(long listing fashion)列出文件夹的内容。

**"ls -a"**命令会列出文件夹里的**所有内容**，包括以"."开头的隐藏文件。 

 ![](https://i-blog.csdnimg.cn/blog_migrate/4073059df4277350a3838a6ad6ce5edf.png)

注意：在**Linux**中，文件以“**.**”开头的就是隐藏文件，并且每个文件，文件夹，设备或者命令都是以文件对待。 

## 2\. cd：切换目录change directory

文件夹输到一半时候按“tab”键是可以自动补全的。

**cd.. **       ：退回上一级目录。

**cd /**       :退回根目录。

**cd ～**      :会改变工作目录为root目录

**cd - **       ：返回上一**次**目录 

## 3\. cp：复制粘贴文件copy

 **cp \[拷贝前路径\] 文件 路径\[拷贝并重命文件名\]**

示例： 

![](https://i-blog.csdnimg.cn/blog_migrate/7f670c37c7bc0a280a2403e505c3bb73.png)

## 4\. mv：移动move

## 5\. rm：删除文件、目录remove

**rm a.txt **       ：回车后输入y确认删除，n取消删除

![](https://i-blog.csdnimg.cn/blog_migrate/eee49f27fdaf66205eb68af58bbb594e.png)

**rm -r xxx       **  删除文件或递归删除目录

**rm -f xxx**       删除目录，**无提示，不建议用**

**rm -rf xxx** 不带提示删除文件，是由-f和-r合并的

**rm -rf /\***           ** 很危险，删库跑路**，无提示递归删除该路径下所有文件目录

![](https://i-blog.csdnimg.cn/blog_migrate/32fe5fee56af621e611bb65d6593740a.png)

## 6\. mkdir：创建目录make directory

**mkdir -p xxx/xxx**        ：创建多级目录

## 7\. rmdir：删除空目录remove directory

**rmdir xxx       ：删除名为xxx的空目录**

只能删除空目录，非空目录会报错：

![](https://i-blog.csdnimg.cn/blog_migrate/75c3c8a43241aad0ded7ca74703339de.png)

先删除目录下文件再删除目录：

![](https://i-blog.csdnimg.cn/blog_migrate/56700cd19b6f3ace06da531194433588.png)

## 8\. chown：更改所有者change owner

## 9\. chmod：更改文件的权限模式change mode

## 10\. find：查找文件

find / -name aaa.txt        ：递归查找文件 

![](https://i-blog.csdnimg.cn/blog_migrate/c0326d91ddcd895afd9f6be913160876.png)

 其他命令，引号可以去除。

![](https://i-blog.csdnimg.cn/blog_migrate/40cb2a061ae4b6e9f4fc71812ebee3f6.png)

> **示例：**
> 
> 查找MySQL配置文件：
> 
> ```
> find / -name "my.cnf"
> ```

## 11\. |：管道

![](https://i-blog.csdnimg.cn/blog_migrate/14433d7b0259d3cfd3fae72eecdd0311.png)

ls --help | more        左边是列表查看帮助信息，右边是分段回车查看文件。 

## 12\. grep：查找文件内容，按行查找并匹配

![](https://i-blog.csdnimg.cn/blog_migrate/2f8e22184d8d70dc9c08f19f57fda40c.png)

## 13\. tar：打包，压缩，解压

![](https://i-blog.csdnimg.cn/blog_migrate/14b1ffcc68ec311af89060d3d1f2d47b.png)

tar -cvf xxx.tar 目录/                打包 

**tar -zcvf xxx.tar.gz 待压缩目录/**         打包并压缩特定目录。

![](https://i-blog.csdnimg.cn/blog_migrate/869947979b6bae49bafbba65bd8010e6.png)

tar -zxvf xxx.tar.gz                 解压

解压到特定目录：

![](https://i-blog.csdnimg.cn/blog_migrate/34f776493b0a22c6680872bf2274f0c2.png)

一般下载网站，linux下载方式文件后缀名都是tar.gz，意思是打包加压缩

![](https://i-blog.csdnimg.cn/blog_migrate/b39a4c0e5539b368a515fec06ad2408a.png)

## 13.3 touch:创建空文件

![](https://i-blog.csdnimg.cn/blog_migrate/c096b9603f6e7baacee394d87ade90ad.png)

## 13.6 vim编辑器:创建修改文件

**三种模式：**

命令行、插入、底层模式（命令行模式时按冒号）。

**进入vim编译器：**

`vim hello.txt` 

**vim编辑模式：**

然后按 **i** 键进入 INSERT进行编辑。

**vim删除一行：**

先esc退出编辑模式，光标移到删除的行，输入**dd**

**vim删除给定范围的行**  
① 删除从第3行到第5行  
按ESC，然后输入下面的命令，然后回车。

:3,5d

  
② 删除最后一行  
按ESC，然后输入下面的命令，然后回车。

:$d

  
③ 删除当前行之前的所有行  
按ESC，然后输入下面的命令，然后回车。

:1,.-1d

  
④ 删除当前行之后的所有行  
按ESC，然后输入下面的命令，然后回车。

:.+1,$d

**vim复制粘贴：**

先按 esc 键退出编辑模式，之后 **`yy`** 复制一行，**`p`** 粘贴一行

**vim保存：**

先esc退出insert模式，再输入:wq进行保存

## 13.9 clear:清空命令行

清空命令行。输入回车即可。或者ctrl+L

## 14\. cat（more,less,tail）：查看文件，打印文件内容

如果文件较大，查看不完全要用more，分段回车查看

**cat xxx.xxx**             ：查看文件，打印文件内容 

![](https://i-blog.csdnimg.cn/blog_migrate/7d8d94316caa2c591ea17c3ec7f68df1.png)

cat a.txt > b.txt        ：a的内容覆盖复制粘贴到b.txt

cat a.txt >> b.txt        ：a的内容追加复制粘贴到b.txt

**more xxx.txt **       ：大文件分段回车查看，按q或者Ctrl+c退出

**less xxx.txt**                ：大文件逐行查看，空格或回车或下方向键查看下一行，上方向键查看上一行，按q或者Ctrl+c退出。按G看最后一页，按g看第一页。

**tail -10 xxx.txt **               ：查看最后10行，数字可改，适用于看日志

**tail -n 10 xxx.txt**             ：查看最后10行，数字可改，适用于看日志

**tail -f xxx.txt** ：动态查看日志

> **案例：**实时查看日志文件最后100行：
> 
> ```bash
> tail -f -n 100 zcy_backend.log
> ```

## 14.5 nohup：不挂起运行命令no hang up

**后台运行并指定日志：** 

```
nohup /root/runoob.sh > runoob.log 2>&1 &
```

**2>&1** 解释：

将标准错误 2 重定向到标准输出 &1 ，标准输出 &1 再被重定向输入到 runoob.log 文件中。

-   0 – stdin (standard input，标准输入)
-   1 – stdout (standard output，标准输出)
-   2 – stderr (standard error，标准错误输出)

## 15\. ps：查看进程process select

![](https://i-blog.csdnimg.cn/blog_migrate/3e01dffb7f7151ccf642eae354bff7a9.png)

ps -ef | grep ssh        查找某一进程，中间竖杠是管道，左边输入作为右边输出。 

## 16\. kill：杀死进程

kill 进程号：告诉进程，你需要被关闭，请自行停止运行并退出。

kill -9 进程号：强制退出进程，表示“无条件终止”；这个信号不能被捕获或忽略，同时接收这个信号的进程在收到这个信号时不能执行任何清理。

## 17\. passwd：修改密码password

## 18\. pwd：显示当前目录路径print work directory

![](https://i-blog.csdnimg.cn/blog_migrate/e971cb76e977b361ecd770b011dd3999.png)

## 19\. tee：显示并保存

## 20\. reboot：重启