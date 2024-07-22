>  **导航：**
>
> [【Java笔记+踩坑汇总】JavaSE+JavaWeb+SSM+SpringBoot+瑞吉外卖+SpringCloud/SpringCloudAlibaba+黑马旅游+谷粒商城](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"126646289"%2C"source"%3A"qq_40991313"})

[TOC]



> 可以参考w3s school：
>
> [w3school 在线教程](https://www.w3school.com.cn/index.html)

# 一、HTML

## 1.1 介绍

HTML 是一门语言，所有的网页都是用HTML 这门语言编写出来的，也就是HTML是用来写网页的。

**HTML(HyperText Markup Language)：超文本标记语言：**

- 超文本：超越了文本的限制，比普通文本更强大。除了文字信息，还可以定义图片、音频、视频等内容

  如上图看到的页面，我们除了能看到一些文字，同时也有大量的图片展示；有些网页也有视频，音频等。这种展示效果超越了文本展示的限制。

- 标记语言：由标签构成的语言

  之前学习的XML就是标记语言，由一个一个的标签组成，HTML 也是由标签组成 。

HTML标签不像XML那样可以自定义，**HTML中的标签都是预定义好的，运行在浏览器上并由浏览器解析，然后展示出对应的效果。**例如我们想在浏览器上展示出图片就需要使用预定义的 `img` 标签；想展示可以点击的链接的效果就可以使用预定义的 `a` 标签等。

**HTML标签参考手册**：[HTML 标签参考手册](https://www.w3school.com.cn/tags/index.asp)

**W3C标准：**

W3C是万维网联盟，这个组成是用来定义标准的。他们规定了一个网页是由三部分组成，分别是：

- 结构：对应的是 HTML 语言
- 表现：对应的是 CSS 语言
- 行为：对应的是 JavaScript 语言

HTML定义页面的整体结构；CSS是用来美化页面，让页面看起来更加美观；JavaScript可以使网页动起来，比如轮播图也就是多张图片自动的进行切换等效果。

## 1.2 helloworld

```html
<!--html5标识-->
<!DOCTYPE html>
<!--向搜索引擎表示该页面是html语言,并且语言为英文网站,其"lang"的意思就是“language”,语言的意思,而“en”即表示english-->
<html lang="en">
<head>
    <!--    定义字符集-->
    <meta charset="UTF-8">
    <title>标题</title>
</head>
<body>
<h1>h1标题</h1>
<p>hello</p>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- HTML 文件以.htm或.html为扩展名
- HTML 结构标签



| [](https://www.w3school.com.cn/tags/tag_doctype.asp) | 定义文档类型。                                      |
| ---------------------------------------------------- | --------------------------------------------------- |
| [](https://www.w3school.com.cn/tags/tag_html.asp)    | 定义 HTML 文档，属性lang定义页面语言，如lang="en"。 |
| [](https://www.w3school.com.cn/tags/tag_meta.asp)    | 定义关于 HTML 文档的字符集等元信息。                |



- ![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\0a86aaf523544316bdb0fbb5f4937954.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- HTML 标签不区分大小写

  如上案例中的 `font` 写成 `Font` 也是一样可以展示出对应的效果的。

- HTML 标签属性值 单双引皆可

  如上案例中的color属性值使用双引号也是可以的。<font color="red"></font>

- HTML 语法松散

  比如 font 标签不加结束标签也是可以展示出效果的。但是建议同学们在写的时候还是不要这样做，严格按照要求去写。

## 1.3 元素

**元素**Element：在HTML中从开始标签到结束标签的所有代码。

标签和元素不同：<p>这就是一个标签; <p>这里是内容</p>这就是一个元素 

- HTML 元素以**开始标签**起始
- HTML 元素以**结束标签**终止
- **元素的内容**是开始标签与结束标签之间的内容
- 某些 HTML 元素具有**空内容（empty content），如<br>**
- 空元素**在开始标签中进行关闭**（以开始标签的结束而结束）
- 大多数 HTML 元素可拥有**属性**，如class,id,style,title

## 1.4 标签

### 1.4.1 基础标签（文字相关）

基础标签就是一些和文字相关的标签，如下：

| [](https://www.w3school.com.cn/tags/tag_doctype.asp) | 定义文档类型。                       |
| ---------------------------------------------------- | ------------------------------------ |
| [](https://www.w3school.com.cn/tags/tag_html.asp)    | 定义 HTML 文档。                     |
| [](https://www.w3school.com.cn/tags/tag_meta.asp)    | 定义关于 HTML 文档的字符集等元信息。 |

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\57df9daf5d71449b85e9aa9fce7ddac6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**演示：**

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\5a5b0fa8d7e64c48bbe90eb11dd5207d.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

跟xml一样，一些特殊符号不能直接打出，要用**转义字符：**

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\6cabdb75b1fd4d3e8e6e74c0f44f5723.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.4.2 图片、音频、视频标签

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\f35b9e3c461c4e58a27a2a7ce7cedb38.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**标签属性** 

- img：定义图片
  - src：规定显示图像的 URL（统一资源定位符）
  - height：定义图像的高度
  - width：定义图像的宽度
- audio：定义音频。支持的音频格式：MP3、WAV、OGG
  - src：规定音频的 URL
  - controls：显示播放控件，controls="controls"
- video：定义视频。支持的音频格式：MP4, WebM、OGG
  - src：规定视频的 URL
  - controls：显示播放控件

**尺寸单位：**

height属性和width属性有两种设置方式：

- 像素：单位是px
- 百分比。占父标签的百分比。例如宽度设置为 50%，意思就是占它的父标签宽度的一般（50%）

**URL路径** 

图片，音频，视频标签都有src属性，而src是用来指定对应的图片，音频，视频文件的路径。此处的图片，音频，视频就称为资源。资源路径有如下两种设置方式：

- 绝对路径：完整路径

  这里的绝对路径是网络中的绝对路径。 格式为： 协议://ip地址:端口号/资源名称。

  如：

  ```
  <img src="https://th.bing.com/th/id/R33674725d9ae34f86e3835ae30b20afe?rik=Pb3C9e5%2b%2b3a9Vw&riu=http%3a%2f%2fwww.desktx.com%2fd%2ffile%2fwallpaper%2fscenery%2f20180626%2f4c8157d07c14a30fd76f9bc110b1314e.jpg&ehk=9tpmnrrRNi0eBGq3CnhwvuU8PPmKuy1Yma0zL%2ba14T0%3d&risl=&pid=ImgRaw" width="300" height="400">
  ```

  这里src属性的值就是网络中的绝对路径。

- 相对路径：相对位置关系

  找页面和其他资源的相对路径。

  > ./ 表示当前路径，同一级目录，可省略
  >
  > ../ 表示上一级路径
  >
  > ../../ 表示上两级路径

### 1.4.3 超链接标签

`a` 标签属性：

- href：指定访问资源的URL。*href*是超文本引用Hypertext Reference的缩写。
- target：指定打开资源的方式
  - _self：默认值。在当前页面打开
  - _blank：在空白页面打开



### 1.4.4 列表标签

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\8b5dc2ff83894dbb84f90bc1b98bf2f7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**一般不用type，用css样式修改类型更好。**

有序列表中的 `type` 属性用来指定标记的标号的类型（数字、字母、罗马数字等）。

无序列表中的 `type` 属性用来指定标记的形状

 演示：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <ol type="A">
        <li>咖啡</li>
        <li>茶</li>
        <li>牛奶</li>
    </ol>
    
    <ul type="circle">
        <li>咖啡</li>
        <li>茶</li>
        <li>牛奶</li>
    </ul>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.4.5 表格标签

演示：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<table border="1" cellspacing="0" width="500">
    <tr>
        <th>序号</th>
        <th>品牌logo</th>
        <th>品牌名称</th>
        <th>企业名称</th>
    </tr>
    <tr align="center">
        <td>010</td>
        <td><img src="../img/三只松鼠.png" width="60" height="50"></td>
        <td>三只松鼠</td>
        <td>三只松鼠</td>
    </tr>

    <tr align="center">
        <td>009</td>
        <td><img src="../img/优衣库.png" width="60" height="50"></td>
        <td>优衣库</td>
        <td>优衣库</td>
    </tr>

    <tr align="center">
        <td>008</td>
        <td><img src="../img/小米.png" width="60" height="50"></td>
        <td>小米</td>
        <td>小米科技有限公司</td>
    </tr>
</table>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**属性：**

- table ：定义表格
  - border：规定表格边框的宽度
  - width ：规定表格的宽度
  - cellspacing：规定单元格之间的空白
- tr ：定义行
  - align：定义表格行的内容对齐方式
- td ：定义单元格
  - **rowspan**:规定单元格可横跨的行数，即多行合并单元格
  - **colspan**:规定单元格可横跨的列数，即多列合并单元格
- th：定义表头单元格

### 1.4.6 布局标签

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\3026296ee43346bea912935e442a4b54.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这两个标签，一般都是和css结合到一块使用来实现页面的布局。

`div`标签 在浏览器上会有换行的效果，而 `span` 标签在浏览器上没有换行效果。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div>hello</div>
    <div>hello</div>
    <span>world</span>
    <span>world</span>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\4cea7939662247b8a84394a12aab47d7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 1.4.7 表单标签

**概述** 

> 表单：在网页中主要负责数据采集功能，使用<form>标签定义表单
>
> 表单项(元素)：不同类型的 input 元素、下拉列表、文本域等

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\4b3a92255cb74ba18468ffcfbe014ce9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

`form` 是表单标签，它在页面上没有任何展示的效果。需要借助于表单项标签来展示不同的效果。如下图就是不同的表单项标签展示出来的效果。  

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\72ff1eaea72c41fabd759874661dd183.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**form标签属性**

- **action：规定当提交表单时向何处发送表单数据，该属性值就是URL**

  以后会将数据提交到服务端，该属性需要书写服务端的URL。而今天我们可以书写 `#` ，表示提交到当前页面来看效果。

- **method ：规定用于发送表单数据的方式**

  method取值有如下两种：

  - get：默认值。如果不设置method属性则默认就是该值
    - 请求参数会拼接在URL后边
    - url的长度有限制 4KB
  - post：
    - 浏览器会将数据放到http请求消息体中
    - 请求参数无限制的，所以经常用post

**示例：**



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="ceshi.html" method="get">
        <input type="text" name="username">
        <input type="text" name="password">
        <input type="submit">
    </form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

输入内容提交后，action指定的URL后面拼接了我们提交的数据

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\3c89f62cbdc3403ea563adcf21f1cb48.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 如果提交方式改为post，则提交的数据会放在http请求消息体中：

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\c06a3f963cac43ee81607a5b2dc9070e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





### 1.4.8 表单项标签

- **<input>**：表单项，通过type属性控制输入形式

  `input` 标签有个 `type` 属性。 `type` 属性的取值不同，展示的效果也不一样

  ![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\d69118f62097424eb0a21d246e6b6d09.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

  checkbox译为复选框，检查框，box有方框的意思。

**<select>**：定义下拉列表，<option> 定义列表项

如果option有设置value，则提交的是value；如果没设置，提交的是文本

如下图就是下拉列表的效果：

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\feac8a54281b4066bb18a2abf947e509.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **示例：**

```html
    城市:
    <select name="city">
        <option>北京</option>
        <option value="shanghai">上海</option>
        <option>广州</option>
    </select>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**<textarea>**：文本域

如下图就是文本域效果。它可以输入多行文本，而 `input` 数据框只能输入一行文本。

可以通过属性cols和rows设置显示列行数。

示例：

```html
    个人描述：
    <textarea cols="20" rows="5" name="desc"></textarea>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\46e19300db2345f8bd32789fceb86672.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**<label>**：定义 input 元素的标注，作用是通过指定id**扩大点击区域**。

"for" 属性可把 label 绑定到另外一个元素。绑定时要把 "for" 属性的值设置为相关元素的 id 属性的值。例如for="username"，可以使用户点击label时，光标聚焦到id为username的文本框里

**示例：**

```html
<!--    例如for="username"，可以使用户点击label时，光标聚焦到username的文本框里-->
    <label for="username">用户名：</label>
    <input type="text" name="username" id="username"><br>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - 以上标签项的内容要想提交，必须得定义 **`name`** 属性。
> - **id**属性值是每个标签的唯一标识。一般用于css和js中引用,它只在前端页面中起作用。
> - 单选框、复选框、下拉列表需要使用 `value` 属性指定提交的值。

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="#" method="post">
    <input type="hidden" name="id" value="123">
<!--    label定义 input 元素的标注。"for" 属性可把 label 绑定到另外一个元素。请把 "for" 属性的值设置为相关元素的 id 属性的值。-->
<!--    例如for="username"，可以使用户点击label时，光标聚焦到username的文本框里-->
    <label for="username">用户名：</label>
    <input type="text" name="username" id="username"><br>

    <label for="password">密码：</label>
    <input type="password" name="password" id="password"><br>

    性别：
    <input type="radio" name="gender" value="1" id="male"> <label for="male">男</label>
    <input type="radio" name="gender" value="2" id="female"> <label for="female">女</label>
    <br>

    爱好：
    <input type="checkbox" name="hobby" value="1"> 旅游
    <input type="checkbox" name="hobby" value="2"> 电影
    <input type="checkbox" name="hobby" value="3"> 游戏
    <br>

    头像：
    <input type="file"><br>

    城市:
    <select name="city">
        <option>北京</option>
        <option value="shanghai">上海</option>
        <option>广州</option>
    </select>
    <br>

    个人描述：
    <textarea cols="20" rows="5" name="desc"></textarea>
    <br>
    <br>
    <input type="submit" value="免费注册">
    <input type="reset" value="重置">
    <input type="button" value="一个按钮">
</form>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在浏览器的效果如下：

 ![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\e20ae74ef22d4f2790637848ccf55035.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 1.5 id和name区别

- **`name`** 属性在表单提交时用到，只有加了name属性的标签元素才会提交到服务器，在后台进行处理。
- **id**属性值是每个标签的唯一标识。一般用于css和js中引用,它只在前端页面中起作用。

## 1.6 href、src、url的区别

**RUL**：Uniform Resource Locators **统一资源定位符**的简写，浏览器通过URL向web服务器发出请求。

**scr**：src是source的缩写，**表示引入文件**，目的是使文件加载到HTML页面中，当浏览器解析时会先加载scr的资源，然后才会执行页面的其他内容。scr的内容是页面必不可少的一部分，包含scr属性的常见标签有**：img、script、iframe。**

**href**：Hypertext Reference的缩写，表示超文本引用，**指向网络资源所在的位置**，建立和当前元素（锚点）或当前文档链接之间的链接，他与页面直接的关系为链接关系，在加载href中的内容时页面本身不会停止其他内容的加载，包含href的常见标签有：**a、link**。

**三者区别：**
 URL是资源定位规则，而src、href是标签的属性，而且scr可以利用url进行页面请求

浏览器解析html时会先加载scr中的资源，此时会阻塞HTML页面的加载，而href则不会，这也是引用的js文件要放在标签后面的原因，否则如果放在head中js代码要放在window.onload中，而引用的css文件直接可以放在head中，它是通过link加载的不会阻塞页面。

href用于在当前文档和引用资源之间确立关系，scr引用的路径使用img、video、audio等要加载的路径，即，href引用的路径是要跳转的地方，scr引用的是页面所使用的图片视频等资源。

# 二、CSS

CSS 是一门语言，用于控制网页表现。

CSS也有一个专业的名字：**Cascading Style Sheet（层叠样式表）**。



## 2.1 css 导入方式



css 导入方式其实就是 css 代码和 html 代码的结合方式。

**CSS 导入 HTML有三种方式：**

- **内联样式**：在标签内部使用style属性，属性值是css属性键值对

  ```html
  <div style="color: red">Hello CSS~</div>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > 给方式只能作用在这一个标签上，如果其他的标签也想使用同样的样式，那就需要在其他标签上写上相同的样式。复用性太差。

- **内部样式**：定义<style>标签，在标签内部定义css样式

  ```html
  <style type="text/css">
      div{
          color: red;
      }
  </style>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > 这种方式可以做到在该页面中复用。

- **外部样式**：定义link标签，引入外部的css文件

  编写一个css文件。名为：demo.css，内容如下:

  ```css
  div{
      color: red;
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  在html中引入 css 文件，rel指定引入文本类型，stylesheet是样式表的意思，css是层叠样式表，href超文本引用指定引入url。

  ```html
  <link rel="stylesheet"  href="demo.css">
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > 这种方式可以在多个页面进行复用。其他的页面想使用同样的样式，只需要使用 `link` 标签引入该css文件。

**示例：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        span{
            color: red;
        }
    </style>
    <link href="../css/demo.css" rel="stylesheet">
</head>
<body>
    <div style="color: red">hello css</div>

    <span>hello css </span>

    <p>hello css</p>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.2 css 选择器

> **id和class区别：**
>
> 　1、唯一性和重复可用性。id在网页结构中只能是唯一的，如果指定了一个元素的id为aa，那么网页中就不能再出现一个id为aa的HTML元素。虽然强大的浏览器会支持多个重复id并赋予对应样式，但这是不标准不允许的。而class相反，它可以在网页结构中重复使用，你指定了一个元素的class 为bb，同时可以指定下一个元素的class为 bb，这两个元素可以同时被应用bb的样式。此外，你还可以为一个元素制定多个class属性值，这样就会同时获得多个属性的样式。
>
> 　　2、CSS中优先级不同。id的样式优先级要高于class的样式优先级。
>
> 　　3、跳转功能。使用id属性可以增加锚标记跳转功能，而class没有这个功能。
>
> **选择器优先级顺序：行内样式**(例如<p class="style"></p>) > **ID选择器**(#) > **Class选择器**(.) > **元素选择器**(p/div) > 通配符(*) > 自带样式 > 继承

css 选择器就是选取需设置样式的元素（标签），比如如下css代码：

```html
div {
    color:red;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如上代码中的 `div` 就是 css 中的选择器。我们只讲下面三种选择器：



- **元素选择器**

  格式：

  ```css
  元素名称{color: red;}
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  例子：

  ```css
  div {color:red}  /*该代码表示将页面中所有的div标签的内容的颜色设置为红色*/
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **id选择器**

  格式：

  ```css
  #id属性值{color: red;}
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  例子：

  html代码如下：

  ```html
  <div id="name">hello css2</div>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  css代码如下：

  ```css
  #name{color: red;}/*该代码表示将页面中所有的id属性值是 name 的标签的内容的颜色设置为红色*/
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **类选择器**

  格式：

  ```css
  .class属性值{color: red;}
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  例子：

  html代码如下：

  ```html
  <div class="cls">hello css3</div>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  css代码如下：

  ```css
  .cls{color: red;} /*该代码表示将页面中所有的class属性值是 cls 的标签的内容的颜色设置为红色*/
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>title</title>
    <style>
        /*优先级：id》class》元素，范围越小越优先*/
        h1 {
            color:red;
        }
        .helloClass{
            color:yellow;
        }
        /*最终颜色是蓝色*/
        #helloId{
            color:blue;
        }

    </style>
</head>
<body>
<h1 id="helloId" class="helloClass">hello</h1>
<script>alert("hello")</script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.3 css属性

[CSS 参考手册](https://www.w3school.com.cn/cssref/index.asp)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\71add0ff0fc6460e9ff0a28215f2cbc6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 三、JavaScript

## 3.1 简介

JavaScript 是一门**跨平台**、**面向对象**的脚本语言。

**与Java区别：**

而Java语言也是跨平台的、面向对象的语言，只不过**Java是编译语言**，是需要编译成字节码文件才能运行的；**JavaScript是脚本语言**，不需要编译，由**浏览器直接解析并执行**。

JavaScript 和 Java 是完全不同的语言，不论是概念还是设计，只是名字比较像而已。  

**与Java相似点：**

**基础语法类似**，所以我们有java的学习经验，再学习JavaScript 语言就相对比较容易些。  

**作用：**

JavaScript 是用来控制网页行为的，它能使网页可交互；

> **JavaScript可以做什么？**
>
> **改变页面内容**
>
> ![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\07e752f6231946df8c0ef7a538464e42.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> 当我点击上面左图的 `点击我` 按钮，按钮上面的文本就改为上面右图内容，这就是js 改变页面内容的功能。
>
> 
>
> 
>
> **修改指定元素的属性值**
>
> ![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\604e505422eb4f609ebc3bfa07553915.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> 当我们点击上图的 `开灯` 按钮，效果就是上面右图效果；当我点击 `关灯` 按钮，效果就是上面左图效果。其他这个功能中有两张灯泡的图片（使用img标签进行展示），通过修改 img 标签的 src 属性值改变展示的图片来实现。
>
> 
>
> **对表单进行校验**
>
> 
>
> ![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\7316b46858694a988ebbacc30d2ccd4e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> 在上面左图的输入框输入用户名，如果输入的用户名是不满足规则的就展示右图(上) 的效果；如果输入的用户名是满足规则的就展示右图(下) 的效果。





## 3.2 引入方式

JavaScript 引入方式就是 HTML 和 JavaScript 的结合方式。JavaScript引入方式有两种：

- **内部脚本：**将 JS代码定义在HTML页面中
- **外部脚本：**将 JS代码定义在外部 JS文件中，然后引入到 HTML页面中

### 3.2.1 内部脚本

在 HTML 中，JavaScript 代码必须位于 `<script>` 与 `</script>` 标签之间

**代码如下：**

`alert(数据)` 是 JavaScript 的一个方法，作用是将参数数据以浏览器弹框的形式输出出来。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script>
    alert("hello js1");
</script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **提示：**

- 在 HTML 文档中可以在任意地方，放置任意数量的<script>标签。如下图

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <script>
          alert("hello js1");
      </script>
  </head>
  <body>
  <!--    script放这个位置最好-->
  <script>
      alert("hello js1");
  </script>
  
  </body>
  </html>
  <script>
      alert("hello js1");
  </script>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



> **一般把脚本置于 <body> 元素的底部，可改善显示速度**
>
> 因为浏览器在加载页面的时候会从上往下进行加载并解析。 我们应该让用户看到页面内容，然后再展示动态的效果。





### 3.2.2 外部脚本

**第一步：定义外部 js 文件。如定义名为 demo.js的文件**

项目结构如下：

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\505eb409943e40468b4f67bc1d8639de.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





demo.js 文件内容如下：

```javascript
alert("hello js");
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**第二步：在页面中引入外部的js文件**

在页面使用 `script` 标签中使用 `src` 属性指定 js 文件的 URL 路径。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script src="../js/demo.js"></script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - 外部脚本不能包含 `<script>` 标签
>
>   在js文件中直接写 js 代码即可，不要在 js文件 中写 `script` 标签
>
> - `<script>` 标签不能自闭合
>
>   在页面中引入外部js文件时，不能写成 `<script src="../js/demo.js" />`。
>
> - link用href，script用src

## 3.3 JavaScript基础语法

### 3.3.1 书写语法

- **区分大小写：**与 Java 一样，变量名、函数名以及其他一切东西都是区分大小写的

- **每行结尾的分号可有可无**

  如果一行上写多个语句时，必须加分号用来区分多个语句。

- **注释**

  - 单行注释：// 注释内容
  - 多行注释：/* 注释内容 */

  > **注意：**JavaScript 没有文档注释，@xxx就是文档注释

- **大括号表示代码块**

  下面语句大家肯定能看懂，和 java 一样 大括号表示代码块。

```javascript
if (count == 3) { 
   alert(count); 
} 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.3.2 输出语句

js 可以通过以下方式进行内容的输出，只不过不同的语句输出到的位置不同

**写入警告框:**使用 window.alert() 写入警告框，可省略成alert();

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    
<script>
    window.alert("hello js");//写入警告框
    alert("hello js2");//写入警告框
</script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面代码通过浏览器打开，我们可以看到如下图弹框效果![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\2cb576d47347431aba75c6307873dc6f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**写入 HTML :**使用 document.write() 写入 HTML 输出

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    
<script>
    document.write("hello js 2~");//写入html页面
</script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面代码通过浏览器打开，我们可以在页面上看到 `document.write(内容)` 输出的内容![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\f585a8d67d3d4bdf8fe77787f641bbd5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**控制台输出：**使用 console.log() 写入浏览器控制台

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script>
    console.log("hello js 3");//写入浏览器的控制台
</script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面代码通过浏览器打开，我们可以在不能页面上看到 `console.log(内容)` 输出的内容，它是输出在控制台了，而怎么在控制台查看输出的内容呢？在浏览器界面按 `F12` 就可以看到下图的控制台

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\a3a69af085b74107b4079c3aa18adddd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 3.3.3 变量

**var关键字弱类型**

JavaScript 中用 var 关键字（variable 的缩写）来声明变量。格式 `var 变量名 = 数据值;`。而在JavaScript 是一门**弱类型**语言，变量**可以存放不同类型的值**；如下在定义变量时赋值为数字数据，还可以将变量的值改为字符串类型的数

```javascript
var test = 20;
test = "张三";
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**命名规则**

和java语言基本都相同：

- 组成字符可以是任何字母、数字、下划线（_）或美元符号（$）
- 数字不能开头
- 建议使用驼峰命名

和java不同点： 

**var是弱类型、全局变量，且可重复定义** 

JavaScript 中 `var` 关键字有点特殊，有以下地方和其他语言不一样

- 作用域：全局变量

  ```javascript
  {
      var age = 20;
  }
  alert(age);  // 在代码块中定义的age 变量，在代码块外边还可以使用
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 变量可以重复定义

  ```javascript
  {
      var age = 20;
      var age = 30;//JavaScript 会用 30 将之前 age 变量的 20 替换掉
  }
  alert(age); //打印的结果是 30
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**let关键字** 

针对var全局变量和可重复定义的问题，ECMAScript 6 新增了 `let`关键字来定义变量。

它的用法类似于 `var`，但是所声明的变量**，只在 `let` 关键字所在的代码块内有效，且不允许重复声明。**

例如：

```javascript
{
    let age = 20;
}
alert(age); 
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

运行上面代码，浏览器并没有弹框输出结果，说明这段代码是有问题的。通过 `F12` 打开开发者模式可以看到如下错误信息![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\412494b67faa468996d3615d6a9d9053.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





而如果在代码块中定义两个同名的变量，IDEA 开发工具就直接报错了

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\7f9d04b482594331928243293a8da741.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 **const关键字**

ECMAScript 6 新增了 const关键字，用来声明一个**只读的常量**。一旦声明，常量的值就不能改变。 

通过下面的代码看一下常用的特点就可以了。

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\c5df1489682d49fa8d1f71b8d534b8dd.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 我们可以看到给 PI 这个常量重新赋值时报错了。

### 3.3.3 数据类型

JavaScript 中提供了两类数据类型：原始类型 和 引用类型。

> 使用 **typeof 运算符可以获取数据类型**
>
> `alert(typeof age);` 以弹框的形式将 age 变量的数据类型输出

**原始数据类型：number、string、boolean、null、undefined**

> **注意：首字母都是小写**

- **number**：数字（整数、小数、NaN(Not a Number)）

  ```javascript
  var age = 20;
  var price = 99.8;
  
  alert(typeof age); // 结果是 ： number
  alert(typeof price);// 结果是 ： number
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > **注意：** NaN是一个特殊的number类型的值，字面值不是数字的string转换成number，则为NaN类型。

- **string**：字符、字符串，单双引皆可（Java字符串只能双引号，SQL字符串单双引号都可以）

  ```javascript
  var ch = 'a';
  var name = '张三'; 
  var addr = "北京";
  
  alert(typeof ch); //结果是  string
  alert(typeof name); //结果是  string
  alert(typeof addr); //结果是  string
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > **注意：**在 js 中 双引号和单引号都表示字符串类型的数据。
  >
  > string类型的变量可以调用String对象的属性和方法，例如length,charAt(),trim()

- **boolean**：布尔。true，false

  ```javascript
  var flag = true;
  var flag2 = false;
  
  alert(typeof flag); //结果是 boolean
  alert(typeof flag2); //结果是 boolean
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **null**：对象为空

  ```javascript
  var obj = null;
  
  alert(typeof obj);//结果是 object
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > **为什么打印上面的 obj 变量的数据类型，结果是object？**
  >
  > 这个官方给出了解释，下面是从官方文档截的图![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\3475b911a14b4f74b888739cc4aaf0b0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
  >
  > 

  

- **undefined**：当声明的变量未初始化时，该变量的默认值是 undefined

  ```javascript
  var a ;
  alert(typeof a); //结果是 undefined
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

### 3.3.4 运算符

JavaScript 除了==和 `===`，其他和java一样。

- 一元运算符：++，--
- 算术运算符：+，-，*，/，%
- 赋值运算符：=，+=，-=…
- 关系运算符：>，<，>=，<=，!=，**==，===**
- 逻辑运算符：&&，||，!
- 三元运算符：条件表达式 ? true_value : false_value

**==和===区别**

- ==：值等于，只比较值
  1. 判断类型是否一样，如果不一样，则进行类型转换
  2. 再去比较其值
- ===：全等于，比较类型和值
  1. 判断类型是否一样，如果不一样，直接返回false
  2. 再去比较其值

**代码：**

```javascript
var age1 = 20;
var age2 = "20";

alert(age1 == age2);// true
alert(age1 === age2);// false
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.3.5 类型转换

> 上述讲解 `==` 运算符时，发现会进行类型转换，所以接下来我们来详细的讲解一下 JavaScript 中的类型转换。

- **其他类型转为number**

  - **string 转换为 number 类型：**按照字符串的字面值，转为数字。如果字面值不是数字，则转为NaN

    将 string 转换为 number 有两种方式：

    - 使用 **`+` 正号运算符**：

      ```javascript
      var str = +"20";
      alert(str + 1) //21
          var a="-23";
          console.log(+(+a));    //-23
      ```

      ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

      

    - 使用 **`parseInt()`** 函数(方法)：

      ```javascript
      var str = "20";
      alert(parseInt(str) + 1);
      ```

      ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

      

    > 建议使用 `parseInt()` 函数进行转换。

  - **boolean 转换为 number 类型：**true 转为1，false转为0

    ```javascript
    var flag = +false;
    alert(flag); // 0
    ```

    ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

    

- **其他类型转为boolean**

  - number 类型转换为 boolean 类型：0和NaN转为false，其他的数字转为true
  - string 类型转换为 boolean 类型：**空字符串转为false，其他的字符串转为true,**示例：**"null"是true，"0"是true**
  - null类型转换为 boolean 类型是 false
  - undefined 转换为 boolean 类型是 false

  **代码如下：**

  ```javascript
  // var flag = 3;
  // var flag = "";
  var flag = undefined;
  
  if(flag){
      alert("转为true");
  }else {
      alert("转为false");
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**使用场景：**

在 Java 中使用字符串前，一般都会先判断字符串不是null，并且不是空字符才会做其他的一些操作，JavaScript也有类型的操作，代码如下：

```javascript
var str = "abc";

//健壮性判断
if(str != null && str.length > 0){
    alert("转为true");
}else {
    alert("转为false");
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

但是由于 JavaScript 会自动进行类型转换，所以上述的判断可以进行简化，代码如下：

```javascript
var str = "abc";

//健壮性判断
if(str){
    alert("转为true");
}else {
    alert("转为false");
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.3.6 流程控制语句

JavaScript的流程控制语句与java一样.

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\746755d4fe8f4755a521b8626458041c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 3.3.7 函数

函数（就是Java中的方法）是被设计为执行特定任务的代码块；JavaScript 函数通过 function 关键词进行定义。

**函数定义：**

格式有两种：

- 方式1

  ```javascript
  function 函数名(参数1,参数2..){
      要执行的代码
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 方式2

  ```javascript
  var 函数名 = function (参数列表){
      要执行的代码
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> - 形式参数和返回值不需要类型。因为JavaScript是弱类型语言
>
>   ```javascript
>   function add(a, b){
>       return a + b;
>   }
>   ```
>
>   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
>   上述函数的参数 a 和 b 不需要定义数据类型，因为在每个参数前加上 var 也没有任何意义。

**函数调用：**

```
函数名称(实际参数列表);
```

eg：

```javascript
let result = add(10,20);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> **注意：**
>
> JS中，函数调用可以传递任意个数参数。
>
> 例如 `let result = add(1,2,3);`
>
> 它是将数据 1 传递给了变量a，将数据 2 传递给了变量 b，而数据 3 没有变量接收。

**应用：**

window对象setTimeout，定时器时间后运行函数：

```javascript
setTimeout(function (){
    alert("hehe");
},3000);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

通过DOM元素实现 事件绑定

```html
<input type="button" id="btn">
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```javascript
document.getElementById("btn").onclick = function (){
    alert("我被点了");
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



## 3.4 JavaScript对象

[JavaScript 和 HTML DOM 参考手册](https://www.w3school.com.cn/jsref/index.asp)

### 3.4.1 Array对象

**作用：**Array对象用于定义数组，JavaScript数组类似于Java集合，变长变类型。

**定义格式**

- 方式1

  ```javascript
  var 变量名 = new Array(元素列表); 
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  例如：

  ```javascript
  var arr = new Array(1,2,3); //1,2,3 是存储在数组中的数据（元素）
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 方式2

  ```javascript
  var 变量名 = [元素列表];
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  例如：

  ```javascript
  var arr = [1,2,3]; //1,2,3 是存储在数组中的数据（元素）
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  > **注意：**Java中的数组静态初始化使用的是{}定义，而 JavaScript 中使用的是 [] 定义

**元素赋值**

赋值数组中的元素和 Java 语言的一样，格式如下：

```javascript
arr[索引] = 值;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**代码演示：**

```javascript
 // 方式一
var arr = new Array(1,2,3);
// alert(arr);

// 方式二
var arr2 = [1,2,3];
//alert(arr2);

// 赋值
arr2[0] = 10;
alert(arr2)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**数组特点：变长变类型**

JavaScript 中的数组相当于 Java 中集合。数组的长度是可以变化的，而 JavaScript 是弱类型，所以可以存储任意的类型的数据（number,string,null,boolean,undefined）。

例如如下代码：

```javascript
    var arr=[1,2,3];
    arr[6]="hello";
    console.log(arr);
    console.log(arr[6]);    //hello
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\3795a15a02964130be3e5b36299473b0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 



**在 JavaScript 中没有赋值的话，默认就是 `undefined`**。



**属性**

Array 对象提供了很多属性，如下图是官方文档截取的

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\74196d5125a24f61b124f68a42abeb8c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



length属性示例:

```javascript
var arr = [1,2,3];
for (let i = 0; i < arr.length; i++) {
    alert(arr[i]);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**方法**

Array 对象同样也提供了很多方法，如下图是官方文档截取的

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\e51efd0d4ded489d9721aa1bdea76d58.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- **push 函数**：给数组添加元素，也就是在数组的末尾添加元素

  参数表示要添加的元素

  ```javascript
  // push:添加方法
  var arr5 = [1,2,3];
  arr5.push(10);
  alert(arr5);  //数组的元素是 {1,2,3,10}
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **splice (索引，个数)函数**：删除元素

  参数1：索引。表示从哪个索引位置删除

  参数2：个数。表示删除几个元素

  ```javascript
  // splice:删除元素
  var arr5 = [1,2,3];
  arr5.splice(0,1); //从 0 索引位置开始删除，删除一个元素 
  alert(arr5); // {2,3}
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

### 3.4.2 String对象

String对象的创建方式有两种

- 方式1：

  ```javascript
  var 变量名 = new String(s); 
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 方式2：

  ```javascript
  var 变量名 = "你好hello"; 
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**属性：**

String对象提供了很多属性，常用属性 `length` ，该属性是用于动态的获取字符串的长度：

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\18b653da61db476fb0312f250bebeccb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**函数：**

String对象提供了很多函数（方法），下面给大家列举了两个方法。

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\0be356c20b234601a6fe938b5ed45769.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





String对象还有一个函数 **`trim()`** ，该方法在文档中没有体现，但是所有的浏览器都支持；它是用来**去掉字符串两端的空格**。

代码演示：

```javascript
var str4 = '  abc   ';
alert(1 + str4 + 1);        //1 abc 1
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

上面代码会输出内容 `1 abc 1`，很明显可以看到 abc 字符串左右两边是有空格的。接下来使用 `trim()` 函数

```javascript
var str4 = '  abc   ';
alert(1 + str4.trim() + 1);    //1abc1
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

输出的内容是 `1abc1` 。这就是 `trim()` 函数的作用。

`trim()` 函数在以后开发中还是比较常用的，例如下图所示是登陆界面

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\9e80257f7d0c4950a222f44dfedef3d5.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





用户在输入用户名和密码时，可能会习惯的输入一些空格，这样在我们后端程序中判断用户名和密码是否正确，结果肯定是失败。所以我们一般都会对用户输入的字符串数据进行去除前后空格的操作。



### 3.4.3 自定义对象

在 JavaScript 中自定义对象特别简单，下面就是自定义对象的格式：

```javascript
var 对象名称 = {
    属性名称1:属性值1,
    属性名称2:属性值2,
    ...,
    函数名称:function (形参列表){},
    ...
};
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

调用属性的格式：

```
对象名.属性名
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

调用函数的格式：

```
对象名.函数名()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

接下来通过代码演示一下，让大家体验一下 JavaScript 中自定义对象

```javascript
var person = {
        name : "zhangsan",
        age : 23,
        eat: function (){
            alert("干饭~");
        }
    };


alert(person.name);  //zhangsan
alert(person.age); //23

person.eat();  //干饭~
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 3.5 BOM浏览器对象模型

### 3.5.1 概述 

**BOM：**Browser Object Model 浏览器对象模型。也就是 JavaScript 将浏览器的各个组成部分封装为对象。

我们要操作浏览器的各个组成部分就可以通过操作 BOM 中的对象来实现。比如：我现在想将浏览器地址栏的地址改为 `https://www.xxx.com` 就可以通过使用 BOM 中定义的 `Location` 对象的 `href` 属性，代码： `location.href = "https://xxx.com";`

**BOM 中包含了如下对象：**

- Window：浏览器窗口对象
- Navigator：浏览器对象，不常用，返回浏览器版本、名称等信息
- Screen：屏幕对象，不常用，返回屏幕亮度、尺寸、分辨率等信息
- History：历史记录对象
- Location：地址栏对象

下图是 BOM 中的各个对象和浏览器的各个组成部分的对应关系

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\b4a01ff5c3464cb8b0aac6a01d45dcaf.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.5.2 Window对象

window 对象是 JavaScript 对浏览器的窗口进行封装的对象。

**获取window对象不需要创建，可以直接使用 `window`，其中 `window.` 可以省略。**

比如我们之前使用的 `alert()` 函数，其实就是 `window` 对象的函数，在调用是可以写成如下两种

- 显式使用 `window` 对象调用

  ```javascript
  window.alert("abc");
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- 隐式调用

  ```javascript
  alert("abc")
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**属性**

`window` 对象提供了用于获取其他 BOM 组成对象的属性

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\eb3adc388318401f9e06a34c2242a979.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 



也就是说，我们想使用 `Location` 对象的话，就可以使用 `window` 对象获取；写成 `window.location`，而 `window.` 可以省略，简化写成 `location` 来获取 `Location` 对象。

示例：

```javascript
console.log(location);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\768f15b805b844b79e10bdb2f6f97f46.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**函数**

`window` 对象提供了很多函数供我们使用，而很多都不常用；下面给大家列举了一些比较常用的函数

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\06da51a214a74e23bb46eefa1ab9c526.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 



> `setTimeout(function,毫秒值)` : 一次性定时器，在一定的时间间隔后执行一个function，只执行一次 `setInterval(function,毫秒值)` :循环定时器，在一定的时间间隔后执行一个function，循环执行

**confirm代码演示：**

```javascript
// confirm()，点击确定按钮，返回true，点击取消按钮，返回false
var flag = confirm("确认删除？");

alert(flag);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

下图是 `confirm()` 函数的效果。当我们点击 `确定` 按钮，`flag` 变量值记录的就是 `true` ；当我们点击 `取消` 按钮，`flag` 变量值记录的就是 `false`。

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\e7acd3681591453babfeeab4eef9b753.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





而以后我们在页面删除数据时候如下图每一条数据后都有 `删除` 按钮，有可能是用户的一些误操作，所以对于删除操作需要用户进行再次确认，此时就需要用到 `confirm()` 函数。

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\600aad081559471bbbb347c1f35f9157.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**定时器代码演示：**

```javascript
setTimeout(function (){
    alert("hehe");
},3000);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

当我们打开浏览器，3秒后才会弹框输出 `hehe`，并且只会弹出一次。

```javascript
setInterval(function (){
    alert("hehe");
},2000);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

当我们打开浏览器，每隔2秒都会弹框输出 `hehe`。



### 3.5.3 History历史记录对象

History 对象是 JavaScript 对历史记录进行封装的对象。

History 对象的**获取**

使用 window.history获取，其中window. 可以省略

**函数**

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\a1dbaca0ebd04808be7fb0738b41a808.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



```javascript
    history.back();
    history.forward();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



这两个函数我们平时在访问其他的一些网站时经常使用对应的效果，如下图

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\8cc1e8ced3084236b80f0c04cdcd8369.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





当我们点击向左返回的箭头，就跳转到前一个访问的页面，这就是 `back()` 函数的作用；当我们点击向右前进的箭头，就跳转到下一个访问的页面，这就是 `forward()` 函数的作用。



### 3.5.4 Location地址栏对象

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\03a3bc0a9b00487d996c70062778b521.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





Location 对象是 JavaScript 对地址栏封装的对象。可以通过操作该对象，跳转到任意页面。

**获取Location对象**

使用 window.location获取，其中window. 可以省略

```javascript
window.location.方法();
location.方法();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**属性**

Location对象提供了很对属性。以后常用的只有一个属性 `href`

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\e388d64b874f480a8f7ae0ef0370ff80.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**代码演示：**

```javascript
alert("要跳转了");
location.href = "https://www.baidu.com";
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在浏览器首先会弹框显示 `要跳转了`，当我们点击了 `确定` 就会跳转到 百度 的首页。

## 3.6 DOM文档对象模型

### 3.6.1 概述

**DOM：**Document Object Model 文档对象模型。也就是 JavaScript 将 HTML 文档的各个组成部分封装为对象。

**作用：**使javascript有能力操作HTML文档（获取HTML标记元素，添加HTML标记元素，删除HTML标记元素等）。

JavaScript 通过 DOM， 就能够对 HTML进行操作了

- 改变 HTML 元素的内容
- 改变 HTML 元素的样式（CSS）
- 对 HTML DOM 事件作出反应
- 添加和删除 HTML 元素

**所有DOM相关概念：**

DOM 是 W3C（万维网联盟）定义了访问 HTML 和 XML 文档的标准。该标准被分为 3 个不同的部分：

1. **核心 DOM：**针对任何结构化文档的标准模型。 XML 和 HTML 通用的标准

   - **Document：整个文档对象**
   - **Element：元素对象**
   - Attribute：属性对象
   - Text：文本对象
   - Comment：注释对象

2. **XML DOM：** 针对 XML 文档的标准模型

3. **HTML DOM：** 针对 HTML 文档的标准模型

   该标准是在核心 DOM 基础上，对 HTML 中的每个标签都封装成了不同的对象

   - 例如：`<img>` 标签在浏览器加载到内存中时会被封装成 `Image` 对象，同时该对象也是 `Element` 对象。
   - 例如：`<input type='button'>` 标签在浏览器加载到内存中时会被封装成 `Button` 对象，同时该对象也是 `Element` 对象。

**封装的对象分为**

- Document：整个文档对象
- Element：元素对象
- Attribute：属性对象
- Text：文本对象
- Comment：注释对象

如下图，左边是 HTML 文档内容，右边是 DOM 树

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\b48b127b45294799b4dd42928679942c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)







### 3.6.2 元素对象

**元素**Element：在HTML中从开始标签到结束标签的所有代码。

标签和元素不同：<p>这就是一个标签; <p>这里是内容</p>这就是一个元素 

- HTML 元素以**开始标签**起始
- HTML 元素以**结束标签**终止
- **元素的内容**是开始标签与结束标签之间的内容
- 某些 HTML 元素具有**空内容（empty content），如<br>**
- 空元素**在开始标签中进行关闭**（以开始标签的结束而结束）
- 大多数 HTML 元素可拥有**属性**，如class,id,style,title

**元素对象：**DOM中，代表着一个 HTML 元素。

元素可以有属性。属性属于属性节点。

### 3.6.3 获取 Element对象

HTML 中的 **Element** 对象可以通过 **`Document`** 对象获取，而 **`Document`** 对象是通过 **`window`** 对象获取。

**`Document` 对象**中提供了以下**获取 `Element` 元素对象**的函数

- **`getElementById()`**：根据id属性值获取，返回单个Element对象
- **`getElementsByTagName()`**：根据标签名称获取，返回Element对象数组
- **`getElementsByName()`**：根据name属性值获取，返回Element对象数组
- **`getElementsByClassName()`**：根据class属性值获取，返回Element对象数组

**代码演示：**

下面有提前准备好的页面：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <img id="light" src="../imgs/off.gif"> <br>

    <div class="cls">你好</div>   <br>
    <div class="cls">世界</div> <br>

    <input type="checkbox" name="hobby"> 电影
    <input type="checkbox" name="hobby"> 旅游
    <input type="checkbox" name="hobby"> 游戏
    <br>
    <script>
		//在此处书写js代码
    </script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**1.根据 `id` 属性值获取上面的 `img` 元素对象，返回单个对象**

```javascript
    var img=document.getElementById("light");
    console.log(img);    //类型是object
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

结果如下：

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\a8821da8577f4944a643a2deb27a6008.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**2.根据标签名称获取所有的 `div` 元素对象**

```javascript
console.log(document.getElementsByTagName("div"));
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\dd79633c145d4c9fa2a8371ca82f9466.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**3.获取所有的满足 `name = 'hobby'` 条件的元素对象**

```javascript
    var hobbys = document.getElementsByName("hobby");
    console.log(hobbys);
    for (let i = 0; i < hobbys.length; i++) {
        console.log(hobbys[i]);
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\2310fa9fc18d45639815d0395160b3d1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**4.获取所有的满足 `class='cls'` 条件的元素对象**

```javascript
//4. getElementsByClassName：根据class属性值获取，返回Element对象数组
var clss = document.getElementsByClassName("cls");
for (let i = 0; i < clss.length; i++) {
    alert(clss[i]);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\decc58d382e84753823f70cedf4b236e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 3.6.4 HTML Element对象使用

HTML 中的 `Element` 元素对象有很多，不可能全部记住，以后是根据具体的需求查阅文档使用。

[JavaScript 和 HTML DOM 参考手册](https://www.w3school.com.cn/jsref/index.asp)

下面我们通过具体的案例给大家演示文档的查询和对象的使用；下面提前给大家准备好的页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <img id="light" src="../imgs/off.gif"> <br>

    <div class="cls">传智教育</div>   <br>
    <div class="cls">黑马程序员</div> <br>

    <input type="checkbox" name="hobby"> 电影
    <input type="checkbox" name="hobby"> 旅游
    <input type="checkbox" name="hobby"> 游戏
    <br>
    <script>
        //在此处写js低吗
    </script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**需求：**

**1.点亮灯泡**

此案例由于需要改变 `img` 标签 的图片，所以我们查询文档，下图是查看文档的流程：

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\3f9be19691274c95ba3839a529489912.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





代码实现：

```javascript
//1，根据 id='light' 获取 img 元素对象
var img = document.getElementById("light");
//2，修改 img 对象的 src 属性来改变图片
img.src = "../imgs/on.gif";
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2.将所有的 `div` 标签的标签体内容替换为 `呵呵`**

查参考手册查不到div的属性，因为div是继承element元素的，所以使用element的属性也可以。 

| [element.innerHTML](https://www.w3school.com.cn/jsref/prop_html_innerhtml.asp) | 设置或返回元素的内容。        |
| ------------------------------------------------------------ | ----------------------------- |
| element.style                                                | 设置或返回元素的 style 属性。 |
| [element.tagName](https://www.w3school.com.cn/jsref/prop_element_tagname.asp) | 返回元素的标签名。            |



```javascript
//1，获取所有的 div 元素对象
var divs = document.getElementsByTagName("div");
/*
        style:设置元素css样式
        innerHTML：设置元素内容
    */
//2，遍历数组，获取到每一个 div 元素对象，并修改元素内容
for (let i = 0; i < divs.length; i++) {
    //divs[i].style.color = 'red';
    divs[i].innerHTML = "呵呵";
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**3.使所有的复选框呈现被选中的状态**

此案例我们需要看 复选框 元素对象有什么属性或者函数是来操作 复选框的选中状态。下图是文档的查看

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\f83dec83824241c885102e118b6bdeb9.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



| [checked](https://www.w3school.com.cn/jsref/prop_checkbox_checked.asp) | 设置或返回 checkbox 是否应被选中。 |
| ------------------------------------------------------------ | ---------------------------------- |
|                                                              |                                    |



代码实现：

```javascript
    var hobbys=document.getElementsByName("hobby");
    console.log(hobbys);
    for(let i=0;i<hobbys.length;i++){
        hobbys[i].checked=false;
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 3.7 事件监听

[JavaScript HTML DOM 事件](https://www.w3school.com.cn/js/js_htmldom_events.asp)

### 3.7.1 概述 

**事件：**

HTML 事件是发生在 HTML 元素上的“事情”。比如：页面上的 `按钮被点击`、`鼠标移动到元素之上`、`按下键盘按键` 等都是事件。

**事件监听：**

事件监听是JavaScript 可以在事件被侦测到时**执行代码**。

例如下图当我们点击 `开灯` 按钮，就需要通过 js 代码实现替换图片

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\8e446aaf321d4fb9b8d08ebf98929d69.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





再比如下图输入框，当我们输入了用户名 `光标离开` 输入框，就需要通过 js 代码对输入的内容进行校验，没通过校验就在输入框后提示 `用户名格式有误!`

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\d806d75507a34396b06bbe104ca8e283.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





### 3.7.2 事件绑定

JavaScript 提供了两种事件绑定方式：

- **方式一：通过 HTML标签中的事件属性进行绑定**

  如下面代码，有一个按钮元素，我们是在该标签上定义 `事件属性`，在事件属性中绑定函数。**`onclick` 就是 `单击事件` 的事件属性。**`onclick='on（）'` 表示该点击事件绑定了一个名为 `on()` 的函数。注意函数名后有括号。

  ```html
  <input type="button" onclick='on()’>
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  下面是点击事件绑定的 `on()` 函数

  ```javascript
  function on(){
  	alert("我被点了");
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **方式二：通过 DOM 元素属性绑定**

  推荐这种方式。如下面代码是按钮标签，在该标签上我们并没有使用 `事件属性`，绑定事件的操作需要在 js 代码中实现

  ```html
  <input type="button" id="btn">
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  下面 js 代码是获取了 `id='btn'` 的元素对象，然后将 `onclick` 作为该对象的属性，并且绑定匿名函数。该函数是在事件触发后自动执行。

  ```javascript
  document.getElementById("btn").onclick = function (){
      alert("我被点了");
  }
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <!--方式1：在下面input标签上添加 onclick 属性，并绑定 on() 函数-->
    <input type="button" value="点我" onclick="on()"> <br>
    <input type="button" value="再点我" id="btn">

    <script>
        function on(){
            alert("我被点了");
        }
      	//方式2：获取 id="btn" 元素对象，通过调用 onclick 属性 绑定点击事件
        document.getElementById("btn").onclick = function (){
            alert("我被点了");
        }
    </script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.7.3 常见事件

上面案例中使用到了 `onclick` 事件属性，那都有哪些事件属性供我们使用呢？下面就给大家列举一些比较常用的事件属性

| 事件属性名  | 说明                     |
| ----------- | ------------------------ |
| onclick     | 鼠标单击事件             |
| onblur      | 元素失去焦点             |
| onfocus     | 元素获得焦点             |
| onload      | 某个页面或图像被完成加载 |
| onsubmit    | 当表单提交时触发该事件   |
| onmouseover | 鼠标被移到某元素之上     |
| onmouseout  | 鼠标从某元素移开         |

**`onfocus` 获得焦点事件。**

如下图，当点击了输入框后，输入框就获得了焦点。而下图示例是当获取焦点后会更改输入框的背景颜色。

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\e16ba5d920f04367be2ddb127b368841.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**`onblur` 失去焦点事件。**

如下图，当点击了输入框后，输入框就获得了焦点；再点击页面其他位置，那输入框就失去焦点了。下图示例是将输入的文本转换为大写。



![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\addb4a86f5f84cd7bce4ffd575ee1370.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

onload 某个页面或图像被完成加载事件



```html
<body onload="fun()">

<div class="cls">你好</div>   <br>
<div class="cls">世界</div> <br>
<script>
    function fun(){
        console.log("heloo");
    }
</script>
</body>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**`onmouseout` 鼠标移出事件。**

**`onmouseover` 鼠标移入事件。**

如下图，当鼠标移入到 苹果 图片上时，苹果图片变大；当鼠标移出 苹果图片时，苹果图片变小。



![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\da01e50f407d41ed820154d420c23a0f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





**`onsubmit` 表单提交事件**

如下是带有表单的页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form id="register" action="#" >
        <input type="text" name="username" />
        <input type="submit" value="提交">
    </form>
    <script>
        
    </script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如上代码的表单，当我们点击 `提交` 按钮后，表单就会提交，此处默认使用的是 `GET` 提交方式，会将提交的数据拼接到 URL 后。现需要通过 js 代码实现阻止表单提交的功能，js 代码实现如下：

```javascript
document.getElementById("register").onsubmit = function (){
    //onsubmit 返回true，则表单会被提交，返回false，则表单不提交
    return true;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



1. 获取 `form` 表单元素对象。
2. 给 `form` 表单元素对象绑定 `onsubmit` 事件，并绑定匿名函数。
3. 该匿名函数如果返回的是true，提交表单；如果返回的是false，阻止表单提交。

## 3.8 表单验证案例

### 3.8.1 需求

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\dfeb8cfb597f4b1daa431ba3fdb12132.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





有如下注册页面，对表单进行校验，如果输入的用户名、密码、手机号符合规则，则允许提交；如果不符合规则，则不允许提交。

完成以下需求：

1. 当输入框失去焦点时，验证输入内容是否符合要求
2. 当点击注册按钮时，判断所有输入框的内容是否都符合要求，如果不合符则阻止表单提交

### 3.8.2 环境准备

下面是初始页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>欢迎注册</title>
    <link href="../css/register.css" rel="stylesheet">
</head>
<body>
    <div class="form-div">
        <div class="reg-content">
            <h1>欢迎注册</h1>
            <span>已有帐号？</span> <a href="#">登录</a>
        </div>
        <form id="reg-form" action="#" method="get">
            <table>
                <tr>
                    <td>用户名</td>
                    <td class="inputs">
                        <input name="username" type="text" id="username">
                        <br>
                        <span id="username_err" class="err_msg" style="display: none">用户名不太受欢迎</span>
                    </td>
                </tr>

                <tr>
                    <td>密码</td>
                    <td class="inputs">
                        <input name="password" type="password" id="password">
                        <br>
                        <span id="password_err" class="err_msg" style="display: none">密码格式有误</span>
                    </td>
                </tr>

                <tr>
                    <td>手机号</td>
                    <td class="inputs"><input name="tel" type="text" id="tel">
                        <br>
                        <span id="tel_err" class="err_msg" style="display: none">手机号格式有误</span>
                    </td>
                </tr>
            </table>
            <div class="buttons">
                <input value="注 册" type="submit" id="reg_btn">
            </div>
            <br class="clear">
        </form>

    </div>


    <script>

    </script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```css
* {
    margin: 0;
    padding: 0;
    list-style-type: none;
}
.reg-content{
    padding: 30px;
    margin: 3px;
}
a, img {
    border: 0;
}

body {
    background-image: url("../imgs/reg_bg_min.jpg") ;
    text-align: center;
}

table {
    border-collapse: collapse;
    border-spacing: 0;
}

td, th {
    padding: 0;
    height: 90px;

}
.inputs{
    vertical-align: top;
}

.clear {
    clear: both;
}

.clear:before, .clear:after {
    content: "";
    display: table;
}

.clear:after {
    clear: both;
}

.form-div {
    background-color: rgba(255, 255, 255, 0.27);
    border-radius: 10px;
    border: 1px solid #aaa;
    width: 424px;
    margin-top: 150px;
    margin-left:1050px;
    padding: 30px 0 20px 0px;
    font-size: 16px;
    box-shadow: inset 0px 0px 10px rgba(255, 255, 255, 0.5), 0px 0px 15px rgba(75, 75, 75, 0.3);
    text-align: left;
}

.form-div input[type="text"], .form-div input[type="password"], .form-div input[type="email"] {
    width: 268px;
    margin: 10px;
    line-height: 20px;
    font-size: 16px;
}

.form-div input[type="checkbox"] {
    margin: 20px 0 20px 10px;
}

.form-div input[type="button"], .form-div input[type="submit"] {
    margin: 10px 20px 0 0;
}

.form-div table {
    margin: 0 auto;
    text-align: right;
    color: rgba(64, 64, 64, 1.00);
}

.form-div table img {
    vertical-align: middle;
    margin: 0 0 5px 0;
}

.footer {
    color: rgba(64, 64, 64, 1.00);
    font-size: 12px;
    margin-top: 30px;
}

.form-div .buttons {
    float: right;
}

input[type="text"], input[type="password"], input[type="email"] {
    border-radius: 8px;
    box-shadow: inset 0 2px 5px #eee;
    padding: 10px;
    border: 1px solid #D4D4D4;
    color: #333333;
    margin-top: 5px;
}

input[type="text"]:focus, input[type="password"]:focus, input[type="email"]:focus {
    border: 1px solid #50afeb;
    outline: none;
}

input[type="button"], input[type="submit"] {
    padding: 7px 15px;
    background-color: #3c6db0;
    text-align: center;
    border-radius: 5px;
    overflow: hidden;
    min-width: 80px;
    border: none;
    color: #FFF;
    box-shadow: 1px 1px 1px rgba(75, 75, 75, 0.3);
}

input[type="button"]:hover, input[type="submit"]:hover {
    background-color: #5a88c8;
}

input[type="button"]:active, input[type="submit"]:active {
    background-color: #5a88c8;
}
.err_msg{
    color: red;
    padding-right: 170px;
}
#password_err,#tel_err{
    padding-right: 195px;
}

#reg_btn{
    margin-right:50px; width: 285px; height: 45px; margin-top:20px;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 3.8.3 验证输入框

此小节完成如下功能：

- 校验用户名。当用户名输入框失去焦点时，判断输入的内容是否符合 `长度是 6-12 位` 规则，不符合使 `id='username_err'` 的span标签显示出来，给出用户提示。
- 校验密码。当密码输入框失去焦点时，判断输入的内容是否符合 `长度是 6-12 位` 规则，不符合使 `id='password_err'` 的span标签显示出来，给出用户提示。代码基本和用户名一样，复制粘贴，Ctrl+r把username替换成password即可。
- 校验手机号。当手机号输入框失去焦点时，判断输入的内容是否符合 `长度是 11 位` 规则，不符合使 `id='tel_err'` 的span标签显示出来，给出用户提示。

代码如下：

```javascript
//1. 验证用户名是否符合规则
//1.1 获取用户名的输入框
var usernameInput = document.getElementById("username");

//1.2 绑定onblur事件 失去焦点
usernameInput.onblur = function () {
    //1.3 获取用户输入的用户名
    var username = usernameInput.value.trim();

    //1.4 判断用户名是否符合规则：长度 6~12
    if (username.length >= 6 && username.length <= 12) {
        //符合规则
        document.getElementById("username_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("username_err").style.display = '';
    }
}

//1. 验证密码是否符合规则
//1.1 获取密码的输入框
var passwordInput = document.getElementById("password");

//1.2 绑定onblur事件 失去焦点
passwordInput.onblur = function() {
    //1.3 获取用户输入的密码
    var password = passwordInput.value.trim();

    //1.4 判断密码是否符合规则：长度 6~12
    if (password.length >= 6 && password.length <= 12) {
        //符合规则
        document.getElementById("password_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("password_err").style.display = '';
    }
}

//1. 验证手机号是否符合规则
//1.1 获取手机号的输入框
var telInput = document.getElementById("tel");

//1.2 绑定onblur事件 失去焦点
telInput.onblur = function() {
    //1.3 获取用户输入的手机号
    var tel = telInput.value.trim();

    //1.4 判断手机号是否符合规则：长度 11
    if (tel.length == 11) {
        //符合规则
        document.getElementById("tel_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("tel_err").style.display = '';
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.8.4 验证表单

当用户点击 `注册` 按钮时，需要同时对输入的 `用户名`、`密码`、`手机号` ，如果都符合规则，则提交表单；如果有一个不符合规则，则不允许提交表单。实现该功能需要获取表单元素对象，并绑定 `onsubmit` 事件

```javascript
//1. 获取表单对象
var regForm = document.getElementById("reg-form");

//2. 绑定onsubmit 事件
regForm.onsubmit = function () {
    
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

`onsubmit` 事件绑定的函数需要对输入的 `用户名`、`密码`、`手机号` 进行校验，这些校验我们之前都已经实现过了，这里我们还需要再校验一次吗？不需要，只需要对之前校验的代码进行改造，把每个校验的代码专门抽象到有名字的函数中，方便调用；并且每个函数都要返回结果来去决定是提交表单还是阻止表单提交，代码如下：

```javascript
//1. 验证用户名是否符合规则
//1.1 获取用户名的输入框
var usernameInput = document.getElementById("username");

//1.2 绑定onblur事件 失去焦点
usernameInput.onblur = checkUsername;

function checkUsername() {
    //1.3 获取用户输入的用户名
    var username = usernameInput.value.trim();

    //1.4 判断用户名是否符合规则：长度 6~12
    var flag = username.length >= 6 && username.length <= 12;
    if (flag) {
        //符合规则
        document.getElementById("username_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("username_err").style.display = '';
    }
    return flag;
}

//1. 验证密码是否符合规则
//1.1 获取密码的输入框
var passwordInput = document.getElementById("password");

//1.2 绑定onblur事件 失去焦点
passwordInput.onblur = checkPassword;

function checkPassword() {
    //1.3 获取用户输入的密码
    var password = passwordInput.value.trim();

    //1.4 判断密码是否符合规则：长度 6~12
    var flag = password.length >= 6 && password.length <= 12;
    if (flag) {
        //符合规则
        document.getElementById("password_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("password_err").style.display = '';
    }
    return flag;
}

//1. 验证手机号是否符合规则
//1.1 获取手机号的输入框
var telInput = document.getElementById("tel");

//1.2 绑定onblur事件 失去焦点
telInput.onblur = checkTel;

function checkTel() {
    //1.3 获取用户输入的手机号
    var tel = telInput.value.trim();

    //1.4 判断手机号是否符合规则：长度 11
    var flag = tel.length == 11;
    if (flag) {
        //符合规则
        document.getElementById("tel_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("tel_err").style.display = '';
    }
    return flag;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

而 `onsubmit` 绑定的函数需要调用 `checkUsername()` 函数、`checkPassword()` 函数、`checkTel()` 函数。

```javascript
//1. 获取表单对象
var regForm = document.getElementById("reg-form");

//2. 绑定onsubmit 事件
regForm.onsubmit = function () {
    //挨个判断每一个表单项是否都符合要求，如果有一个不合符，则返回false

    var flag = checkUsername() && checkPassword() && checkTel();

    return flag;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.8.5 正则表达式优化后最终版本

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>欢迎注册</title>
    <link href="../css/register.css" rel="stylesheet">
</head>
<body>

<div class="form-div">
    <div class="reg-content">
        <h1>欢迎注册</h1>
        <span>已有帐号？</span> <a href="#">登录</a>
    </div>
    <form id="reg-form" action="#" method="get">

        <table>

            <tr>
                <td>用户名</td>
                <td class="inputs">
                    <input name="username" type="text" id="username">
                    <br>
                    <span id="username_err" class="err_msg" style="display: none">用户名不太受欢迎</span>
                </td>

            </tr>

            <tr>
                <td>密码</td>
                <td class="inputs">
                    <input name="password" type="password" id="password">
                    <br>
                    <span id="password_err" class="err_msg" style="display: none">密码格式有误</span>
                </td>
            </tr>


            <tr>
                <td>手机号</td>
                <td class="inputs"><input name="tel" type="text" id="tel">
                    <br>
                    <span id="tel_err" class="err_msg" style="display: none">手机号格式有误</span>
                </td>
            </tr>

        </table>

        <div class="buttons">
            <input value="注 册" type="submit" id="reg_btn">
        </div>
        <br class="clear">
    </form>

</div>


<script>

    //1. 验证用户名是否符合规则
    //1.1 获取用户名的输入框
    var usernameInput = document.getElementById("username");

    //1.2 绑定onblur事件 失去焦点
    usernameInput.onblur = checkUsername;

    function checkUsername() {
        //1.3 获取用户输入的用户名
        var username = usernameInput.value.trim();

        //1.4 判断用户名是否符合规则：长度 6~12,单词字符组成
        var reg = /^\w{6,12}$/;
        var flag = reg.test(username);

        //var flag = username.length >= 6 && username.length <= 12;
        if (flag) {
            //符合规则
            document.getElementById("username_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("username_err").style.display = '';
        }
        return flag;
    }

    //1. 验证密码是否符合规则
    //1.1 获取密码的输入框
    var passwordInput = document.getElementById("password");

    //1.2 绑定onblur事件 失去焦点
    passwordInput.onblur = checkPassword;

    function checkPassword() {
        //1.3 获取用户输入的密码
        var password = passwordInput.value.trim();

        //1.4 判断密码是否符合规则：长度 6~12
        var reg = /^\w{6,12}$/;
        var flag = reg.test(password);

        //var flag = password.length >= 6 && password.length <= 12;
        if (flag) {
            //符合规则
            document.getElementById("password_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("password_err").style.display = '';
        }
        return flag;
    }

    //1. 验证手机号是否符合规则
    //1.1 获取手机号的输入框
    var telInput = document.getElementById("tel");

    //1.2 绑定onblur事件 失去焦点
    telInput.onblur = checkTel;

    function checkTel() {
        //1.3 获取用户输入的手机号
        var tel = telInput.value.trim();

        //1.4 判断手机号是否符合规则：长度 11，数字组成，第一位是1
        //var flag = tel.length == 11;
        var reg = /^[1]\d{10}$/;
        var flag = reg.test(tel);
        if (flag) {
            //符合规则
            document.getElementById("tel_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("tel_err").style.display = '';
        
        return flag;
    }

    //1. 获取表单对象
    var regForm = document.getElementById("reg-form");

    //2. 绑定onsubmit 事件
    regForm.onsubmit = function () {
        //挨个判断每一个表单项是否都符合要求，如果有一个不合符，则返回false

        var flag = checkUsername() && checkPassword() && checkTel();

        return flag;
    }
</script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)







## 3.9 正则对象RegExp

在 js 中对正则表达式封装的对象就是正则对象。正则对象用来判断指定字符串是否符合规则。

### 3.9.1 正则对象使用

**创建对象**

正则对象有两种创建方式：

- **创建方式一：**直接量方式：**注意两边是斜杠，不是引号**

  ```javascript
  var reg = /正则表达式/;        //注意没引号
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

- **创建方式二：**创建 RegExp 对象

  ```javascript
  var reg = new RegExp("正则表达式");
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  

**函数**

**`test(str)` ：判断指定字符串是否符合规则**，返回 true或 false，如/^\w{1,32}$/.test("hello")

### 3.9.2 正则表达式

正则表达式定义了字符串组成的规则。也就是判断指定的字符串是否符合指定的规则，如果符合返回true，如果不符合返回false。

**正则表达式是和语言无关的。**

很多语言都支持正则表达式，Java语言也支持，只不过正则表达式在不同的语言中的**使用方式不同，js 中需要使用正则对象来使用正则表达式。**

正则表达式的**常用规则：**

```
^     表示开始

$     表示结束




[ ]   代表某个范围内的单个字符，比如： [0-9] 单个数字字符

.     代表任意单个字符，除了换行和行结束符

\w    代表单词字符：字母、数字、下划线()，相当于 [A-Za-z0-9]

\d    代表数字字符： 相当于 [0-9]
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**量词：**

```
+     至少一个

*     零个或多个

？     零个或一个

{x}    x个

{m,}   至少m个

{m,n}  至少m个，最多n个
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**代码演示：**

```javascript
// 规则：单词字符，6~12
//1,创建正则对象，对正则表达式进行封装
var reg = /^\w{6,12}$/;

var str = "abcccc";
//2,判断 str 字符串是否符合 reg 封装的正则表达式的规则
var flag = reg.test(str);
alert(flag);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.9.3 Java使用正则表达式

####  3.9.3.1 使用方法

```java
//声明正则表达式，校验手机号
        String regex = "^1[3-9]\\d{9}$";
//校验
        Pattern pattern = Pattern.compile(regex );
        Matcher matcher = pattern.matcher("13485687874");
        matcher.matches();//如果返回是true则校验通过，false则校验失败。
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



#### 3.9.3.2 案例：使用正则表达式校验手机号格式

```java
import java.util.regex.*;

public class PhoneNumberValidator {
    private static final String PHONE_NUMBER_REGEX = "^1[3-9]\\d{9}$";

    public static boolean validatePhoneNumber(String phoneNumber) {
        Pattern pattern = Pattern.compile(PHONE_NUMBER_REGEX);
        Matcher matcher = pattern.matcher(phoneNumber);
        return matcher.matches();
    }

    public static void main(String[] args) {
        String phoneNumber1 = "13812345678";  // 测试合法手机号码
        String phoneNumber2 = "19812345678";  // 测试合法手机号码
        String phoneNumber3 = "12345678901";  // 测试非法手机号码
        String phoneNumber4 = "138123456789"; // 测试非法手机号码

        // 校验合法性
        System.out.println(phoneNumber1 + " 格式是否正确？ " + validatePhoneNumber(phoneNumber1));
        System.out.println(phoneNumber2 + " 格式是否正确？ " + validatePhoneNumber(phoneNumber2));
        System.out.println(phoneNumber3 + " 格式是否正确？ " + validatePhoneNumber(phoneNumber3));
        System.out.println(phoneNumber4 + " 格式是否正确？ " + validatePhoneNumber(phoneNumber4));
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

####  3.9.3.3 案例：给定一个六位数，中间两位不为0即通过

```java
public class SixDigitNumberValidator {
 private static final String NUMBER_REGEX = "^[0-9]{2}(?!00)[0-9]{2}[0-9]{2}$";

 public static boolean validateNumber(String number) {
 Pattern pattern = Pattern.compile(NUMBER_REGEX);
 Matcher matcher = pattern.matcher(number);
 return matcher.matches();
 }

 public static void main(String[] args) {
 String number1 = "120456"; // 测试通过
 String number2 = "100456"; // 测试不通过
 String number3 = "120006"; // 测试不通过
 String number4 = "123456"; // 测试通过
 String number5 = "120156"; // 测试不通过
 
 System.out.println(number1 + "通过校验？ " + validateNumber(number1));
 System.out.println(number2 + "通过校验？ " + validateNumber(number2));
 System.out.println(number3 + "通过校验？ " + validateNumber(number3));
 System.out.println(number4 + "通过校验？ " + validateNumber(number4));
 System.out.println(number5 + "通过校验？ " + validateNumber(number5));
 }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

#### 3.9.3.4 案例：给定一个六位数，中间两位不为00且不为01即通过

```java
public class SixDigitNumberValidator {
 private static final String NUMBER_REGEX = "^[0-9]{2}(?!00|01)[0-9]{2}[0-9]{2}$";

 public static boolean validateNumber(String number) {
 Pattern pattern = Pattern.compile(NUMBER_REGEX);
 Matcher matcher = pattern.matcher(number);
 return matcher.matches();
 }

 public static void main(String[] args) {
 String number1 = "120456"; // 测试通过
 String number2 = "100456"; // 测试不通过
 String number3 = "120006"; // 测试不通过
 String number4 = "123456"; // 测试通过
 String number5 = "120156"; // 测试不通过
 
 System.out.println(number1 + "通过校验？ " + validateNumber(number1));
 System.out.println(number2 + "通过校验？ " + validateNumber(number2));
 System.out.println(number3 + "通过校验？ " + validateNumber(number3));
 System.out.println(number4 + "通过校验？ " + validateNumber(number4));
 System.out.println(number5 + "通过校验？ " + validateNumber(number5));
 }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





## 3.10 ES6基础

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\b0bd3e9f6ea94a86967d838b7ae9562e.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\e6676765d6734c358be70d64c50f2282.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 



### 3.10.1 let & const

vscode快捷键：`！+ 回车`生成html模板

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\0354bd242db54e318cbafab14d045fee.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

​     

- **let声明后不能作用于{}外**，var可以
- **let只能声明一次**（let a=1;let a=2;报错），var可以声明多次
- **var会变量提升**（使用在定义之前，console.log(x);var x = 10;  // undefined），let必须先定义再使用
- const一旦初始化后，不能改变

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        // var 声明的变量往往会越域
        // let 声明的变量有严格局部作用域
        {
            var a = 1;
            let b = 2;
        }
        console.log(a);  // 1
        console.log(b);  // ReferenceError: b is not defined

        // var 可以声明多次
        // let 只能声明一次
        var m = 1
        var m = 2
        let n = 3
        //         let n = 4
        console.log(m)  // 2
        console.log(n)  // Identifier 'n' has already been declared

        // var 会变量提升
        // let 不存在变量提升
        console.log(x);  // undefined
        var x = 10;
        console.log(y);   //报错ReferenceError: y is not defined
        let y = 20;

        // let
        // 1. const声明之后不允许改变
        // 2. 一但声明必须初始化，否则会报错
        const a = 1;
        a = 3; //Uncaught TypeError: Assignment to constant variable.

    </script>
</body>

</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

打开Chrome控制台可以查看报错信息。 



### 3.10.2 解构表达式

- **数组解构（批量赋值）**`let arr = [1,2,3];` `let [a,b,c] = arr`
- **对象解构**`const{name:abc, age, language} = person;console.log(abc);` 其中`name:abc`代表把name改名为abc
- **字符串扩展**`str.startsWith();str.endsWith();str.includes();str.includes()`
- **字符串模板**，``符号，支持一个字符串定义为多行

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\76c2dc3c4db64e319f555301b51f4677.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](JavaWeb基础4——HTML,JavaScript&CSS.assets\79e5a15a84164484b55584f07cb5cbb1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 



- **占位符功能** ${}，字符串插入变量

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        //数组解构
        let arr = [1,2,3];
        // // let a = arr[0];
        // // let b = arr[1];
        // // let c = arr[2];

        let [a,b,c] = arr;
        console.log(a,b,c)

        const person = {
            name: "jack",
            age: 21,
            language: ['java', 'js', 'css']
        }
        //         const name = person.name;
        //         const age = person.age;
        //         const language = person.language;

        //对象解构 // 把name属性变为abc，声明了abc、age、language三个变量
        const { name: abc, age, language } = person;
        console.log(abc, age, language)

        //4、字符串扩展
        let str = "hello.vue";
        console.log(str.startsWith("hello"));//true
        console.log(str.endsWith(".vue"));//true
        console.log(str.includes("e"));//true
        console.log(str.includes("hello"));//true

        //字符串模板 ``可以定义多行字符串
        let ss = `<div>
                    <span>hello world<span>
                </div>`;
        console.log(ss);
        
        function fun() {
            return "这是一个函数"
        }

        // 2、字符串插入变量和表达式。变量名写在 ${} 中，${} 中可以放入 JavaScript 表达式。
        let info = `我是${abc}，今年${age + 10}了, 我想说： ${fun()}`;
        console.log(info);

    </script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.10.3 函数优化

- 支持函数**形参默认值**`function add(a, **b = 1**){}`
- 支持**不定参数数量**`function fun(...values){}，此时能传多个参数，values.length获取数量。`
- 支持**箭头函数**`var print = obj => console.log(obj);有点**像Lambda表达式**`
- 支持**箭头函数+解构对象**`var hello2 = ({name}) => console.log("hello," +name); hello2(person);这里参数{name}是解构出person对象的name属性`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

    <script>
        //在ES6以前，我们无法给一个函数参数设置默认值，只能采用变通写法：
        function add(a, b) {
            // 判断b是否为空，为空就给默认值1
            b = b || 1;
            return a + b;
        }
        // 传一个参数
        console.log(add(10));


        //现在可以这么写：直接给参数写上默认值，没传就会自动使用默认值
        function add2(a, b = 1) {
            return a + b;
        }
        console.log(add2(20));


        //2）、不定参数
        function fun(...values) {
            console.log(values.length)
        }
        fun(1, 2)      //2
        fun(1, 2, 3, 4)  //4

        //3）、箭头函数。lambda
        //以前声明一个方法
        // var print = function (obj) {
        //     console.log(obj);
        // }
        var print = obj => console.log(obj);
        print("hello");

        var sum = function (a, b) {
            c = a + b;
            return a + c;
        }

        var sum2 = (a, b) => a + b;
        console.log(sum2(11, 12));

        var sum3 = (a, b) => {
            c = a + b;
            return a + c;
        }
        console.log(sum3(10, 20))


        const person = {
            name: "jack",
            age: 21,
            language: ['java', 'js', 'css']
        }

        function hello(person) {
            console.log("hello," + person.name)
        }

        //箭头函数+解构
        var hello2 = ({name}) => console.log("hello," +name);
        hello2(person);

    </script>
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.10.4 对象优化

- 可以**获取map的键值对**`Object.keys(personMap)`、`Object.values(personMap)`、`Object.entries(personMap)`
- `Object.assgn(target,source1,source2)` **合并对象**source1，source2到target
- 支持**对象名声明简写**：如果属性名和属性值的变量名相同可以省略
- `let someone = {...person}`取出person对象所有的属性拷贝到当前对象

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <script>
        const person = {
            name: "jack",
            age: 21,
            language: ['java', 'js', 'css']
        }

        console.log(Object.keys(person));//["name", "age", "language"]
        console.log(Object.values(person));//["jack", 21, Array(3)]
        console.log(Object.entries(person));//[Array(2), Array(2), Array(2)]，这里每个Array能点开查看键值对

        const target = { a: 1 };
        const source1 = { b: 2 };
        const source2 = { c: 3 };

        // 合并
        //{a:1,b:2,c:3}
        Object.assign(target, source1, source2);

        console.log(target);//["name", "age", "language"]

        //2）、声明对象简写
        const age = 23
        const name = "张三"
        const person1 = { age: age, name: name }
        // 等价于
        const person2 = { age, name }//声明对象简写
        console.log(person2);

        //3）、对象的函数属性简写
        let person3 = {
            name: "jack",
            // 以前：
            eat: function (food) {
                console.log(this.name + "在吃" + food);
            },
            //箭头函数this不能使用，要使用的话需要使用：对象.属性
            eat2: food => console.log(person3.name + "在吃" + food),
            eat3(food) {
                console.log(this.name + "在吃" + food);
            }
        }

        person3.eat("香蕉");
        person3.eat2("苹果")
        person3.eat3("橘子");

        //4）、对象拓展运算符

        // 1、拷贝对象（深拷贝）
        let p1 = { name: "Amy", age: 15 }
        let someone = { ...p1 }
        console.log(someone)  //{name: "Amy", age: 15}

        // 2、合并对象
        let age1 = { age: 15 }
        let name1 = { name: "Amy" }
        let p2 = { name: "zhangsan" }
        p2 = { ...age1, ...name1 }
        console.log(p2)
    </script>
</body>

</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.10.5 map和reduce

- `arr.map()`接收一个函数，将arr中的所有元素用接收到的函数处理后放入新的数组
- `arr.reduce()`为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>

    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>

    <body>


        <script>
            //数组中新增了map和reduce方法。
            //map()：接收一个函数，将原数组中的所有元素用这个函数处理后放入新数组返回。
            let arr = ['1', '20', '-5', '3'];

            //  arr = arr.map((item)=>{
            //     return item*2
            //  });
            arr = arr.map(item => item * 2);



            console.log(arr);
            //reduce() 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，
            //[2, 40, -10, 6]
            //arr.reduce(callback,[initialValue])
            /**
             1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
        2、currentValue （数组中当前被处理的元素）
        3、index （当前元素在数组中的索引）
        4、array （调用 reduce 的数组）*/
            let result = arr.reduce((a, b) => {
                console.log("上一次处理后：" + a);
                console.log("当前正在处理：" + b);
                return a + b;
            }, 100);
            console.log(result)


        </script>
    </body>

    </html>
    <script>
        //数组中新增了map和reduce方法。
        //map()：接收一个函数，将原数组中的所有元素用这个函数处理后放入新数组返回。
        let arr = ['1', '20', '-5', '3'];

        //  arr = arr.map((item)=>{
        //     return item*2
        //  });
        arr = arr.map(item => item * 2);



        console.log(arr);
        //reduce() 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，
        //[2, 40, -10, 6]
        //arr.reduce(callback,[initialValue])
        /**
        1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
        2、currentValue （数组中当前被处理的元素）
        3、index （当前元素在数组中的索引）
        4、array （调用 reduce 的数组）*/
        let result = arr.reduce((a, b) => {
            console.log("上一次处理后：" + a);
            console.log("当前正在处理：" + b);
            return a + b;
        }, 100);
        console.log(result)


    </script>
</body>

</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 5.1.6、promise

- 优化异步操作。封装ajax
- 把Ajax封装到Promise中，赋值给let p
- 在Ajax中成功使用resolve(data)，失败使用reject(err)
- p.then().catch()

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>
</head>

<body>

    <script>
        //1、查出当前用户信息
        //2、按照当前用户的id查出他的课程
        //3、按照当前课程id查出分数
        // $.ajax({
        //     url: "mock/user.json",
        //     success(data) {
        //         console.log("查询用户：", data);
        //         $.ajax({
        //             url: `mock/user_corse_${data.id}.json`,
        //             success(data) {
        //                 console.log("查询到课程：", data);
        //                 $.ajax({
        //                     url: `mock/corse_score_${data.id}.json`,
        //                     success(data) {
        //                         console.log("查询到分数：", data);
        //                     },
        //                     error(error) {
        //                         console.log("出现异常了：" + error);
        //                     }
        //                 });
        //             },
        //             error(error) {
        //                 console.log("出现异常了：" + error);
        //             }
        //         });
        //     },
        //     error(error) {
        //         console.log("出现异常了：" + error);
        //     }
        // });


        //1、Promise可以封装异步操作
        // let p = new Promise((resolve, reject) => {
        //     //1、异步操作
        //     $.ajax({
        //         url: "mock/user.json",
        //         success: function (data) {
        //             console.log("查询用户成功:", data)
        //             resolve(data);
        //         },
        //         error: function (err) {
        //             reject(err);
        //         }
        //     });
        // });

        // p.then((obj) => {
        //     return new Promise((resolve, reject) => {
        //         $.ajax({
        //             url: `mock/user_corse_${obj.id}.json`,
        //             success: function (data) {
        //                 console.log("查询用户课程成功:", data)
        //                 resolve(data);
        //             },
        //             error: function (err) {
        //                 reject(err)
        //             }
        //         });
        //     })
        // }).then((data) => {
        //     console.log("上一步的结果", data)
        //     $.ajax({
        //         url: `mock/corse_score_${data.id}.json`,
        //         success: function (data) {
        //             console.log("查询课程得分成功:", data)
        //         },
        //         error: function (err) {
        //         }
        //     });
        // })

        function get(url, data) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    url: url,
                    data: data,
                    success: function (data) {
                        resolve(data);
                    },
                    error: function (err) {
                        reject(err)
                    }
                })
            });
        }

        get("mock/user.json")
            .then((data) => {
                console.log("用户查询成功~~~:", data)
                return get(`mock/user_corse_${data.id}.json`);
            })
            .then((data) => {
                console.log("课程查询成功~~~:", data)
                return get(`mock/corse_score_${data.id}.json`);
            })
            .then((data)=>{
                console.log("课程成绩查询成功~~~:", data)
            })
            .catch((err)=>{
                console.log("出现异常",err)
            });

    </script>
</body>

</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3.10.7 模块化

- `export`用于规定模块的对外接口,`export`不仅可以导出对象，一切JS变量都可以导出。比如：基本类型变量、函数、数组、对象
- `import`用于导入其他模块提供的功能

```javascript
// user.js

var name = "jack"
var age = 21
function add(a,b){
    return a + b;
}
// 导出变量和函数
export {name,age,add}

---------------------------------------------------------------
// hello.js
    
// 导出后可以重命名
export default {
    sum(a, b) {
        return a + b;
    }
}


--------------------------------------------------------------
// main.js

import abc from "./hello.js"
import {name,add} from "./user.js"

abc.sum(1,2);
console.log(name);
add(1,3);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)