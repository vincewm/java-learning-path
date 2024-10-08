>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[1，VUE](#1%EF%BC%8CVUE)

[1.1 Vue概述，MVVM设计模式](#1.1%20%E6%A6%82%E8%BF%B0)

[1.2 快速入门](#1.2%20%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)

[1.3 Vue 指令](#1.3%20Vue%20%E6%8C%87%E4%BB%A4)

[1.3.1 双向绑定，v-bind & v-model 指令](#1.3.1%20v-bind%20%26%20v-model%20%E6%8C%87%E4%BB%A4)

[1.3.2 绑定事件，v-on 指令](#1.3.2%20v-on%20%E6%8C%87%E4%BB%A4)

[1.3.3 条件判断指令，v-if和v-show](#1.3.3%20%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD%E6%8C%87%E4%BB%A4)

[1.3.4 列表渲染，v-for 指令](#1.3.4%20v-for%20%E6%8C%87%E4%BB%A4)

[1.4 生命周期](#1.4%20%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

[1.4.1 概述](#%E6%A6%82%E8%BF%B0%C2%A0) 

[1.4.2 created和mounted的区别](#created%E5%92%8Cmounted%E7%9A%84%E5%8C%BA%E5%88%AB)

[1.5 this和$](#1.4.5%20this%E5%92%8C%24)

[1.6 案例，vue展示品牌列表](#1.5%20%E6%A1%88%E4%BE%8B)

[1.6.1 需求](#1.5.1%20%E9%9C%80%E6%B1%82)

[1.6.2 查询所有功能](#1.5.2%20%E6%9F%A5%E8%AF%A2%E6%89%80%E6%9C%89%E5%8A%9F%E8%83%BD)

[1.6.3 添加功能](#1.5.3%20%E6%B7%BB%E5%8A%A0%E5%8A%9F%E8%83%BD)

[1.7 vue脚手架进行模块化开发](#3.%20vue-dome)

[1.7.1 全局安装webpack](#1%E3%80%81%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85webpack)

[1.7.2 全局安装vue脚手架](#2%E3%80%81%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85vue%E8%84%9A%E6%89%8B%E6%9E%B6)

[1.7.3 初始化vue项目](#3%E3%80%81%E5%88%9D%E5%A7%8B%E5%8C%96vue%E9%A1%B9%E7%9B%AE)

[1.7.4 vue项目目录结构](#4%E3%80%81vue%E9%A1%B9%E7%9B%AE%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)

[1.7.5 分析主页展示逻辑](#5.3.5%E3%80%81%E4%BF%AE%E6%94%B9vue%E9%A1%B9%E7%9B%AE)

[1.7.6 新建Hello组件，负责/hello路径](#5.3.6%E3%80%81%E6%96%B0%E5%BB%BAHello%E7%BB%84%E4%BB%B6%EF%BC%8C%E8%B4%9F%E8%B4%A3%2Fhello%E8%B7%AF%E5%BE%84)

[1.7.7 快速生成组件模板](#5.3.6%E3%80%81%E5%BF%AB%E9%80%9F%E7%94%9F%E6%88%90%E7%BB%84%E4%BB%B6%E6%A8%A1%E6%9D%BF)

[2，Element](#2%EF%BC%8CElement)

[2.1 快速入门，使用el-button组件](#2.1%20%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)

[2.2 Element 布局](#2.2%20Element%20%E5%B8%83%E5%B1%80)

[2.2.1 Layout 局部](#2.2.1%20Layout%20%E5%B1%80%E9%83%A8)

[2.2.2 Container 布局容器](#2.2.2%20Container%20%E5%B8%83%E5%B1%80%E5%AE%B9%E5%99%A8)

[2.3 案例，element商品列表展示](#2.3%20%E6%A1%88%E4%BE%8B)

[2.3.1 准备基本页面](#2.3.1%20%E5%87%86%E5%A4%87%E5%9F%BA%E6%9C%AC%E9%A1%B5%E9%9D%A2)

[2.3.2 完成表格展示商品](#2.3.2%20%E5%AE%8C%E6%88%90%E8%A1%A8%E6%A0%BC%E5%B1%95%E7%A4%BA)

[2.3.3 完成搜索表单展示](#2.3.3%20%E5%AE%8C%E6%88%90%E6%90%9C%E7%B4%A2%E8%A1%A8%E5%8D%95%E5%B1%95%E7%A4%BA)

[2.3.4 完成批量删除和新增按钮展示](#2.3.4%20%E5%AE%8C%E6%88%90%E6%89%B9%E9%87%8F%E5%88%A0%E9%99%A4%E5%92%8C%E6%96%B0%E5%A2%9E%E6%8C%89%E9%92%AE%E5%B1%95%E7%A4%BA)

[2.3.5 完成对话框展示](#2.3.5%20%E5%AE%8C%E6%88%90%E5%AF%B9%E8%AF%9D%E6%A1%86%E5%B1%95%E7%A4%BA)

[2.3.6 完成分页条展示](#2.3.6%20%E5%AE%8C%E6%88%90%E5%88%86%E9%A1%B5%E6%9D%A1%E5%B1%95%E7%A4%BA)

[2.3.7 完整页面代码](#2.3.7%20%E5%AE%8C%E6%95%B4%E9%A1%B5%E9%9D%A2%E4%BB%A3%E7%A0%81)

[3，综合案例，element商品列表展示增删改查](#3%EF%BC%8C%E7%BB%BC%E5%90%88%E6%A1%88%E4%BE%8B)

[3.1 功能介绍](#3.1%20%E5%8A%9F%E8%83%BD%E4%BB%8B%E7%BB%8D)

[3.1.5 坑点总结](#3.1.5%20%E5%9D%91%E7%82%B9%E6%80%BB%E7%BB%93)

[3.2 环境准备](#3.2%20%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)

[3.2.1 工程准备和最终目录结构](#3.2.1%20%E5%B7%A5%E7%A8%8B%E5%87%86%E5%A4%87)

[3.2.2 创建表](#3.2.2%20%E5%88%9B%E5%BB%BA%E8%A1%A8)

[3.3 查询所有功能](#3.3%20%E6%9F%A5%E8%AF%A2%E6%89%80%E6%9C%89%E5%8A%9F%E8%83%BD)

[3.3.1 后端实现，service优化](#3.3.1%20%E5%90%8E%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[3.3.2 前端实现](#3.3.2%20%E5%89%8D%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[4，添加功能](#3.4%20%E6%B7%BB%E5%8A%A0%E5%8A%9F%E8%83%BD)

[4.1 后端实现](#4.1%20%E5%90%8E%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[4.1.1 dao方法实现](#4.1.1%20dao%E6%96%B9%E6%B3%95%E5%AE%9E%E7%8E%B0)

[4.1.2 service方法实现](#4.1.2%20service%E6%96%B9%E6%B3%95%E5%AE%9E%E7%8E%B0)

[4.1.3 servlet实现](#4.1.3%20servlet%E5%AE%9E%E7%8E%B0)

[4.2 前端实现](#4.2%20%E5%89%8D%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[5，servlet优化](#5%EF%BC%8Cservlet%E4%BC%98%E5%8C%96)

[5.1 优化方法，BaseServlet](#5.1%20%E9%97%AE%E9%A2%98%E5%AF%BC%E5%85%A5)

[5.2 代码优化](#5.2%20%E4%BB%A3%E7%A0%81%E4%BC%98%E5%8C%96)

[5.2.1 后端优化](#5.2.1%20%E5%90%8E%E7%AB%AF%E4%BC%98%E5%8C%96)

[5.2.2 前端优化](#5.2.2%20%E5%89%8D%E7%AB%AF%E4%BC%98%E5%8C%96)

[6，批量删除](#6%EF%BC%8C%E6%89%B9%E9%87%8F%E5%88%A0%E9%99%A4)

[6.1 后端实现](#6.1%20%E5%90%8E%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[6.1.1 dao方法实现](#6.1.1%20dao%E6%96%B9%E6%B3%95%E5%AE%9E%E7%8E%B0)

[6.1.2 service方法实现](#6.1.2%20service%E6%96%B9%E6%B3%95%E5%AE%9E%E7%8E%B0)

[6.1.3 servlet实现](#6.1.3%20servlet%E5%AE%9E%E7%8E%B0)

[6.2 前端实现](#6.2%20%E5%89%8D%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[6.2.1 获取选中的id值](#6.2.1%20%E8%8E%B7%E5%8F%96%E9%80%89%E4%B8%AD%E7%9A%84id%E5%80%BC)

[6.2.2 发送异步请求](#6.2.2%20%E5%8F%91%E9%80%81%E5%BC%82%E6%AD%A5%E8%AF%B7%E6%B1%82)

[6.2.3 确定框实现](#6.2.3%20%E7%A1%AE%E5%AE%9A%E6%A1%86%E5%AE%9E%E7%8E%B0)

[7，分页查询](#7%EF%BC%8C%E5%88%86%E9%A1%B5%E6%9F%A5%E8%AF%A2)

[7.1 分析](#7.1%20%E5%88%86%E6%9E%90)

[7.1.1 分页查询sql](#7.1.1%20%E5%88%86%E9%A1%B5%E6%9F%A5%E8%AF%A2sql)

[7.1.2 前后端数据分析](#7.1.2%20%E5%89%8D%E5%90%8E%E7%AB%AF%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90)

[7.1.25 JavaBean](#7.1.25%C2%A0JavaBean)

[7.1.3 流程、参数分析](#7.1.3%20%E6%B5%81%E7%A8%8B%E5%88%86%E6%9E%90)

[7.2 后端实现](#7.2%20%E5%90%8E%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[7.2.1 dao方法实现](#7.2.1%20dao%E6%96%B9%E6%B3%95%E5%AE%9E%E7%8E%B0)

[7.2.2 service方法实现](#7.2.2%20service%E6%96%B9%E6%B3%95%E5%AE%9E%E7%8E%B0)

[7.2.3 servlet实现](#7.2.3%20servlet%E5%AE%9E%E7%8E%B0)

[7.2.4 测试](#7.2.4%20%E6%B5%8B%E8%AF%95)

[7.3 前端实现](#7.3%20%E5%89%8D%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[7.3.1 selectAll 代码改进](#7.3.1%20selectAll%20%E4%BB%A3%E7%A0%81%E6%94%B9%E8%BF%9B)

[7.3.2 改变每页条目数](#7.3.2%20%E6%94%B9%E5%8F%98%E6%AF%8F%E9%A1%B5%E6%9D%A1%E7%9B%AE%E6%95%B0)

[7.3.3 改变当前页码](#7.3.3%20%E6%94%B9%E5%8F%98%E5%BD%93%E5%89%8D%E9%A1%B5%E7%A0%81)

[8，条件查询](#8%EF%BC%8C%E6%9D%A1%E4%BB%B6%E6%9F%A5%E8%AF%A2)

[8.1 后端实现](#8.1%20%E5%90%8E%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[8.1.1 dao实现](#8.1.1%20dao%E5%AE%9E%E7%8E%B0)

[8.1.2 service实现](#8.1.2%20service%E5%AE%9E%E7%8E%B0)

[8.1.3 servlet实现](#8.1.3%20servlet%E5%AE%9E%E7%8E%B0)

[8.2 前端实现](#8.2%20%E5%89%8D%E7%AB%AF%E5%AE%9E%E7%8E%B0)

[9，箭头函数，前端代码优化](#9%EF%BC%8C%E5%89%8D%E7%AB%AF%E4%BB%A3%E7%A0%81%E4%BC%98%E5%8C%96)

--

## 1，VUE

### 1.1 Vue概述，MVVM设计模式

**Vue 是一套前端框架，免除原生JavaScript中的DOM操作，简化书写。**

> **回顾DOM：**Document Object Model 文档对象模型。也就是 JavaScript 将 HTML 文档的各个组成部分封装为对象。作用：使javascript有能力操作HTML文档（获取HTML标记元素，添加HTML标记元素，删除HTML标记元素等）

`类似Mybatis` 框架是用来简化 `jdbc` 代码编写的。而 **`VUE` 是前端的框架**，是用来**简化 `JavaScript` 代码**编写的。

> 上节axios时候有一个案例，里面进行了大量的DOM操作，如下
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/8a231e3b9343dafb496f5df43d9978fd.png)
> 
> 学习了 `VUE` 后，这部分代码我们就不需要再写了。那么 `VUE` 是如何简化 DOM 书写呢？ 

**vue基于MVVM(Model-View-ViewModel)思想，实现数据的双向绑定，将编程的关注点放在数据上。**

之前我们是将关注点放在了 DOM 操作上。

**MVVM设计模式：**

它本质上就是MVC 的改进版。_MVVM_ 就是将其中的View 的状态和行为抽象化，让我们**将视图 UI 和业务逻辑分开**。

> **MVC回顾：** 
> 
> **`MVC` 思想**图解
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/4a731c4b4ef03593a5cd607bd2c37fd1.png)
> 
> C 就是咱们 js 代码，M 就是数据，而 V 是页面上展示的内容，如下图是我们之前写的代码
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/5108441bd6420ba642257af708415dc0.png)
> 
> `MVC` 思想只能模型到视图的单向展示，是**没法**进行**双向绑定**的。

**MVVC可以实现模型和视图双向绑定：**

双向绑定是指当模型发生变化时，视图的会随之发生变化；而如果视图发生变化，绑定的模型数据也随之发生变化。

**双向绑定作用**

从界面的操作能实时反映到数据，数据的变更能实时展现到界面

**`MVVM` 思想三个组件图解**

![](https://i-blog.csdnimg.cn/blog_migrate/391a98cc068c24da699974febba83a58.png)

图中的 **`Model` 是数据**，**`View` 是视图**，也就是页面标签，用户可以通过浏览器看到的内容；

`Model` 和 `View` 是通过 `ViewModel` 对象进行**双向绑定**的，而 `ViewModel` 对象是 `Vue` 提供的。

**双向绑定的效果**，下图输入框绑定了 `username` 模型数据，而在页面上也使用 **`{{}}` 绑定**了 `username` 模型数据

**示例：** 

![](https://i-blog.csdnimg.cn/blog_migrate/3c003acf97b179cd3f60c5f2c3bc6f9f.png)

通过浏览器打开该页面可以看到如下页面

![](https://i-blog.csdnimg.cn/blog_migrate/6de03b6d6dfa210ed16b0ff2d3986c36.png)

当我们在输入框中输入内容，而输入框后面随之实时的展示我们输入的内容，这就是双向绑定的效果。

### 1.2 快速入门

Vue 使用分为如下三步：

<table><tbody><tr><td>v-model</td><td>在表单元素上创建双向数据绑定</td></tr></tbody></table>

vue里data()**设置**username值并展示在输入框，反过来又可以手动修改输入框内容**设置**vue里username值 

1.  **新建 HTML 页面，引入 Vue.js文件。**这里vue.js版本v2.7.8，下载地址[Installation — Vue.js](https://v2.vuejs.org/v2/guide/installation.html#Vue-Devtools "Installation — Vue.js")
    
    ```html
    <script src="js/vue.js"></script>
    ```
    
2.  **在JS代码区域，创建Vue核心对象，传入JSON对象进行数据绑定**
    
    ```javascript
    new Vue({
        el: "#app",
        // data() 是 ECMAScript 6 版本的新的写法，旧写法data:function(){}
        data() {
            return {
                username: ""
            }
        }
        //methods不是method，并且后面没括号
        methods:{
                
        }
        mounted(){}
    });
    ```
    
    创建 Vue 对象时，需要传递一个 js 对象，而该对象中需要如下属性：
    
    -   **`el` ：** 用来**指定哪些id的标签受 Vue 管理**。 该属性取值 `#app` 中的 `app` 需要是受管理的标签的**id属性值**
        
    -   **`data` ：**用来定义数据模型
        
    -   **`methods` ：**用来定义函数。
        
3.  **编写视图**
    
    ```html
    <div id="app">
        <input v-model="username" >
        {{username}}
    </div>
    ```
    
    `{{}}` 是 Vue 中定义的 `插值表达式` ，在里面写数据模型，到时候会将该模型的数据值展示在这个位置。
    

**整体代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <input v-model="username"><br>
    <!--插值表达式-->
    input里的值是：{{username}}
</div>
<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){  // data() 是 ECMAScript 6 版本的新的写法
            return {
                username:"默认值"
            }
        }

        /*data: function () {
            return {
                username:""
            }
        }*/
    });

</script>
</body>
</html>
```

![](https://i-blog.csdnimg.cn/blog_migrate/18e00b3e5ee5893c86dc39883aa713bd.png)

### 1.3 Vue 指令

**指令：**HTML 标签上带有 **v- 前缀的特殊属性**，不同指令具有不同含义。例如：v-if，v-for…

常用的指令有：

| **指令** | **作用** |
| --- | --- |
| v-bind | 为HTML标签绑定属性值，如设置 href , css样式等，bind译为捆绑。v-bind:href="url" |
| v-model | 在表单元素上创建双向数据绑定。v-model="username"        {{username}} |
| v-on | 为HTML标签绑定事件。v-on:click="show()" |
| v-if | 条件性的渲染某元素，判定为true时渲染,否则不渲染。v-if="count==3" |
| v-else |  |
| v-else-if |  |
| v-show | 根据条件展示某元素，区别在于切换的是display属性的值。v-show="count==3" |
| v-for | 列表渲染，遍历容器的元素或者对象的属性。v-for="(str,i) in strs" |

只有v-bind,v-on中间有冒号，因为属性和事件都有多种。

#### 1.3.1 双向绑定，v-bind & v-model 指令

![](https://i-blog.csdnimg.cn/blog_migrate/78607d3ad1acab421752faffda1219f7.png)

-   **v-bind**
    
    该指令可以**给标签原有属性绑定模型数据**。这样vue的data()里模型数据发生变化，标签属性值也随之发生变化
    
    例如：
    
    ```html
    <a v-bind:href="url">百度一下</a>
    ```
    
    上面的 `v-bind:"` 可以简化写成 `:` ，如下：
    
    ```html
    <!--
    	v-bind 可以省略
    -->
    <a :href="url">百度一下</a>
    ```
    
-   **v-model**
    
    该指令可以给表单项标签绑定模型数据。这样就能实现双向绑定效果（vue里data()**设置**username值并展示在输入框，反过来又可以手动修改输入框内容**设置**vue里username值）。例如：
    
    ```html
    <input name="username" v-model="username">
    ```
    

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <a v-bind:href="url">点击一下</a>
    <a :href="url">点击一下</a>
    <input v-model="url">
</div>

<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                username:"",
                url:"https://www.baidu.com"
            }
        }
    });
</script>
</body>
</html>
```

通过浏览器打开上面页面，并且使用检查查看超链接的路径，该路径会根据输入框输入的路径变化而变化，这是因为超链接和输入框绑定的是同一个模型数据

![](https://i-blog.csdnimg.cn/blog_migrate/8f4843fab2bfe338f4055895ffc67119.png)

#### 1.3.2 绑定事件，v-on 指令

![](https://i-blog.csdnimg.cn/blog_migrate/9eafbeba5f993969a80d12acb3c043c4.png)

我们在页面定义一个按钮，并给该按钮使用 `v-on` 指令绑定单击事件，html代码如下

```html
<input type="button" value="一个按钮" v-on:click="show()">
```

而使用 `v-on` 时还可以使用简化的写法，将 `v-on:` 替换成 `@`，html代码如下

```html
<input type="button" value="一个按钮" @click="show()">
```

上面代码绑定的 `show()` 需要在 Vue 对象中的 `methods` 属性中定义出来

```javascript
new Vue({
    el: "#app",
    methods: {
        show(){
            alert("我被点了");
        }
    }
});
```

> **注意：`v-on:` 后面的事件名称是之前原生事件属性名去掉on。**
> 
> 例如：
> 
> -   单击事件 ： 事件属性名是 onclick，而在vue中使用是 `v-on:click`
>     
> -   失去焦点事件：事件属性名是 onblur，而在vue中使用时 `v-on:blur`
>     

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <input type="button" value="一个按钮" v-on:click="show()"><br>
    <input type="button" value="一个按钮" @click="show()">
</div>
<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                username:"",
            }
        },
        methods:{
            show(){
                alert("我被点了...");
            }
        }
    });
</script>
</body>
</html>
```

#### 1.3.3 条件判断指令，v-if和v-show

![](https://i-blog.csdnimg.cn/blog_migrate/65a5c1b5d73b54b537de3163636dee1a.png)

接下来通过代码演示一下。在 Vue中定义一个 `count` 的数据模型，如下

```javascript
//1. 创建Vue核心对象
new Vue({
    el:"#app",
    data(){
        return {
            count:3
        }
    }
});
```

现在要实现，当 `count` 模型的数据是3时，在页面上展示 `div1` 内容；当 `count` 模型的数据是4时，在页面上展示 `div2` 内容；`count` 模型数据是其他值时，在页面上展示 `div3`。这里为了动态改变模型数据 `count` 的值，再定义一个输入框绑定 `count` 模型数据。html 代码如下：

```html
<div id="app">
    <div v-if="count == 3">div1</div>
    <div v-else-if="count == 4">div2</div>
    <div v-else>div3</div>
    <hr>
    <input v-model="count">
</div>
```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <div v-if="count == 1">div1</div>
    <div v-else-if="count == 2">div2</div>
    <div v-else>div3</div>
    <hr>
    设置count的值：<input v-model="count"><br>
    目前count的值：{{count}}
</div>

<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                count:3
            }
        }
    });
</script>
</body>
</html>
```

通过浏览器打开页面并在输入框输入不同的值，效果如下

![](https://i-blog.csdnimg.cn/blog_migrate/40d0264b1fcf92fc8300d8eef81fd4ef.png)

**`v-show`**

然后我们在看看 `v-show` 指令的效果，如果模型数据 `count` 的值是3时，展示 `div v-show` 内容，否则不展示，html页面代码如下

```html
<div v-show="count == 3">div v-show</div>
<br>
<input v-model="count">
```

浏览器打开效果如下：

![](https://i-blog.csdnimg.cn/blog_migrate/b43e3cf0c7cc57666e4a6b77fe7cb529.png)

**v-if和v-show区别** 

通过下图可以看出 `v-show` 不展示的原理是给对应的标签添加 `display` css属性，并将该属性值设置为 `none` ，这样就达到了隐藏的效果。而 `v-if` 指令是条件不满足时根本就不会渲染。在网页源码只能看见v-show的标签，看不见不满足判断条件的v-if标签。

![](https://i-blog.csdnimg.cn/blog_migrate/399281e6523ddcf529032ba738e7bdf1.png)

#### 1.3.4 列表渲染，v-for 指令

![](https://i-blog.csdnimg.cn/blog_migrate/c5b6a210188e157d13999b18c676cbfc.png)

这个指令看到名字就知道是用来遍历的，该指令使用的格式如下：

```html
<标签 v-for="变量名 in 集合模型数据">
    {{变量名}}
</标签>
```

```html
    <div v-for="addr in addrs">
        {{addr}} <br>
    </div>
```

> **注意：需要循环哪个标签，`v-for` 指令就写在哪个标签上。**

如果在页面需要使用到集合模型数据的**索引**，就需要使用如下格式：

```html
<标签 v-for="(变量名,索引变量) in 集合模型数据">
    <!--索引变量是从0开始，所以要表示序号的话，需要手动的加1-->
   {{索引变量 + 1}} {{变量名}}
</标签>
```

```html
    <div v-for="(addr,i) in addrs">
        {{i+1}}--{{addr}} <br>
    </div>
```

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <div v-for="addr in addrs">
        {{addr}} <br>
    </div>

    <hr>
    <div v-for="(addr,i) in addrs">
        {{i+1}}--{{addr}} <br>
    </div>
</div>

<script src="js/vue.js"></script>
<script>

    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                //注意：Java中的数组静态初始化使用的是{}定义，而 JavaScript 中使用的是 [] 定义


                addrs:["北京","上海","西安"]
            }
        }
    });
</script>
</body>
</html>
```

通过浏览器打开效果如下

![](https://i-blog.csdnimg.cn/blog_migrate/6f9f5922edf12d4afc82448db13fff4c.png)

### 1.4 生命周期

#### 1.4.1 概述 

生命周期的八个阶段：每触发一个生命周期事件，会自动执行一个生命周期方法，这些生命周期方法也被称为**钩子方法**。

![](https://i-blog.csdnimg.cn/blog_migrate/f99c7576d80a3f9b219a1c731dc88296.png)

其他了解即可，最常**用的是created和mounted**，类似于window.onload

下图是 Vue 官网提供的从创建 Vue 到效果 Vue 对象的整个过程及各个阶段对应的钩子函数

![](https://i-blog.csdnimg.cn/blog_migrate/eb3c6dd900b85b47607f0d757af54326.png)

看到上面的图，大家无需过多的关注这张图。这些钩子方法我们只关注 `mounted` 就行了。

`mounted`：挂载完成，Vue初始化成功，HTML页面渲染成功。而以后我们会在该方法中**发送异步请求，加载数据。**

```javascript
    new Vue({
        el:"#app",
        data(){
            return {
                addrs:["北京","上海","西安"]
            }
        },
        mounted(){    //跟data类似，是简化后的版本
            alert("加载完成");
        }
    });
```

#### 1.4.2 created和mounted的区别

**created：在模板渲染成html前调用**，即通常初始化某些属性值，然后再渲染成识图。  
**mounted：在模板渲染成html后调用**，通常初始化页面完成后，再对html的dom节点进行一些需要的操作。 

`created()` 和 `mounted()` 之间的**根本区别在于访问DOM**，如果尝试引用 `this.$el`，在 `created()` 中返回 `null`，在 `mounted()` 中返回 DOM 元素：

<table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td><p>1</p><p>2</p><p>3</p><p>4</p><p>5</p><p>6</p><p>7</p><p>8</p><p>9</p><p>10</p></td><td><p><code>export </code><code>default</code> <code>{</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><code>created() {</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code>// 打印 null</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code>console.log(</code><code>this</code><code>.$el);</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><code>},</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><code>mounted() {</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code>// 打印 DOM 元素</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code>console.log(</code><code>this</code><code>.$el);</code></p><p><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><code>},</code></p><p><code>};</code></p></td></tr></tbody></table>

因此，任何 DOM 操作，甚至使用诸如 `querySelector` 之类的方法获取 DOM 元素结构将无法在 `created()` 中使用。因此根据这点区别 `created()` 非常适合调用 API，而 `mounted()` 非常适合在 DOM 元素完全加载后执行任何操作。

### 1.5 this和$

**this：**

Vue中生命周期钩子、自定义方法，axios和axios中then(箭头函数)的**this指向当前的 Vue 实例**。

![](https://i-blog.csdnimg.cn/blog_migrate/14c9aa883c41773530d4e29731327101.png)

方法内方法或axios的then(非箭头函数)中**this指向window**。 

> **注意：普通函数和箭头函数内this指向不同。**axios内的this：
> 
> ```javascript
>             selectAll(){
>                 //这里this指向vue
>                 axios({
>                     这里this指向vue
>                 }).then(function (response){
>                     这里this指向window
>                 })
>             },
> ```
> 
> ```javascript
>             selectAll(){
>                 //这里this指向vue
>                 axios({
>                     这里this指向vue
>                 }).then(response=>{    //箭头函数
>                     这里this指向vue
>                 })
>             },
> ```

![](https://i-blog.csdnimg.cn/blog_migrate/c5b1a645170e03eb81ab15f22cd4f3f9.png)

-   **this指向vue：**可以通过this.xxx和this.xxx()调用vue中的数据和方法。        
-   **$:挂载在this上的vue内部属性**，一个特殊标记。增强区分的，来说明这是内置的实例方法属性。

### 1.6 案例，vue展示品牌列表

#### 1.6.1 需求

使用 Vue 简化我们在前一天ajax学完后做的品牌列表数据查询和添加功能

[JavaWeb基础9——Filter&Listener&Ajax\_vincewm的博客-CSDN博客](https://blog.csdn.net/qq_40991313/article/details/126156944?spm=1001.2014.3001.5501 "JavaWeb基础9——Filter&Listener&Ajax_vincewm的博客-CSDN博客")

![](https://i-blog.csdnimg.cn/blog_migrate/6f7041d0c64e1a925ca0bab781ce92e1.png)

此案例只是使用 Vue 对前端代码进行优化，后端代码无需修改。

#### 1.6.2 查询所有功能

![](https://i-blog.csdnimg.cn/blog_migrate/e2e746f92efc47d4bd747f0ad59bf097.png)

1.  **在 brand.html 页面引入 vue 的js文件**
    
    ```html
    <script src="js/vue.js"></script>
    ```
    
2.  **创建 Vue 对象**
    
    -   在 Vue 对象中定义模型数据
        
    -   在钩子函数中发送异步请求，并将响应的数据赋值给数据模型
        
    
    ```javascript
    new Vue({
        el: "#app",
        data(){
            return{
                brands:[]
            }
        },
        mounted(){
            // 页面加载完成后，发送异步请求，查询数据
            //this指代当前vue对象，要用this才能取出vue对象中的数据
            var _this = this;
            axios({
                method:"get",
                url:"http://localhost:8080/brand-demo/selectAllServlet"
            }).then(function (resp) {
                //这里如果直接this.brands，则this指代当前axios对象
                _this.brands = resp.data;
            })
        }
    })
    ```
    
3.  **修改视图**
    
    -   定义 `<div id="app"></div>` ，指定该 `div` 标签受 Vue 管理
        
    -   将 `body` 标签中所有的内容拷贝作为上面 `div` 标签中
        
    -   删除表格的多余数据行，只留下一个
        
    -   在表格中的数据行上使用 `v-for` 指令遍历
        
        ```html
                <tr v-for="(brand,i) in brands">
                    <td>{{i+1}}</td>
                    <td>{{brand.brandName}}</td>
                    <td>{{brand.companyName}}</td>
                    <td>{{brand.ordered}}</td>
                    <td>{{brand.description}}</td>
                    <td v-if="brand.status==1">启用</td>
                    <td v-else>禁用</td>
                    <td><a href="#">修改</a> <a href="#">删除</a></td>
                </tr>
        ```
        

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <a href="addBrand.html"><input type="button" value="新增"></a><br>
    <hr>
    <table id="brandTable" border="1" cellspacing="0" width="100%">
        <tr>
            <th>序号</th>
            <th>品牌名称</th>
            <th>企业名称</th>
            <th>排序</th>
            <th>品牌介绍</th>
            <th>状态</th>
            <th>操作</th>
        </tr>
        <!--
            使用v-for遍历tr
        -->
        <tr v-for="(brand,i) in brands">
            <td>{{i+1}}</td>
            <td>{{brand.brandName}}</td>
            <td>{{brand.companyName}}</td>
            <td>{{brand.ordered}}</td>
            <td>{{brand.description}}</td>
            <td v-if="brand.status==1">启用</td>
            <td v-else>禁用</td>
            <td><a href="#">修改</a> <a href="#">删除</a></td>
        </tr>
    </table>
</div>
<script src="js/axios-0.18.0.js"></script>
<script src="js/vue.js"></script>

<script>
    new Vue({
        el: "#app",
        data(){
            return{
                brands:[]
            }
        },
        mounted(){
            // 页面加载完成后，发送异步请求，查询数据
            var _this = this;
            axios({
                method:"get",
                url:"http://localhost:8080/brand-demo/selectAllServlet"
            }).then(function (resp) {
                _this.brands = resp.data;
            })
        }
    })
</script>
</body>
</html>
```

#### 1.6.3 添加功能

页面操作效果如下：

![](https://i-blog.csdnimg.cn/blog_migrate/23d083e594267304f212aa45e4bb4893.png)

整体流程如下

![](https://i-blog.csdnimg.cn/blog_migrate/29dffb27aa83c7d6057534d8c1cf881a.png)

> **注意：前端代码的关键点在于使用 `v-model` 指令给标签项绑定模型数据，利用双向绑定特性，在发送异步请求时提交数据。**

1.  **在 addBrand.html 页面引入 vue 的js文件**
    
    ```html
    <script src="js/vue.js"></script>
    ```
    
2.  **创建 Vue 对象**
    
    -   在 Vue 对象中定义模型数据 `brand`
        
    -   定义一个 `submitForm()` 函数，用于给 `提交` 按钮提供绑定的函数
        
    -   在 `submitForm()` 函数中发送 ajax 请求，并将模型数据 `brand` 作为参数进行传递
        
    
    ```javascript
    new Vue({
        el: "#app",
        data(){
            return {
                brand:{}
            }
        },
        methods:{
            submitForm(){
                // 发送ajax请求，添加
                var _this = this;
                axios({
                    method:"post",
                    url:"http://localhost:8080/brand-demo/addServlet",
                    data:_this.brand
                }).then(function (resp) {
                    // 判断响应数据是否为 success
                    if(resp.data == "success"){
                        location.href = "http://localhost:8080/brand-demo/brand.html";
                    }
                })
    
            }
        }
    })
    ```
    
3.  **修改视图**
    
    -   定义 `<div id="app"></div>` ，指定该 `div` 标签受 Vue 管理
        
    -   将 `body` 标签中所有的内容拷贝作为上面 `div` 标签中
        
    -   给每一个表单项标签绑定模型数据。最后这些数据要被封装到 `brand` 对象中
        
        ```html
        <div id="app">
            <h3>添加品牌</h3>
            <form action="" method="post">
                品牌名称：<input id="brandName" v-model="brand.brandName" name="brandName"><br>
                企业名称：<input id="companyName" v-model="brand.companyName" name="companyName"><br>
                排序：<input id="ordered" v-model="brand.ordered" name="ordered"><br>
                描述信息：<textarea rows="5" cols="20" id="description" v-model="brand.description" name="description"></textarea><br>
                状态：
                <input type="radio" name="status" v-model="brand.status" value="0">禁用
                <input type="radio" name="status" v-model="brand.status" value="1">启用<br>
        
                <input type="button" id="btn" @click="submitForm" value="提交">
            </form>
        </div>
        ```
        

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>添加品牌</title>
</head>
<body>
<div id="app">
    <h3>添加品牌</h3>
    <form action="" method="post">
        品牌名称：<input id="brandName" v-model="brand.brandName" name="brandName"><br>
        企业名称：<input id="companyName" v-model="brand.companyName" name="companyName"><br>
        排序：<input id="ordered" v-model="brand.ordered" name="ordered"><br>
        描述信息：<textarea rows="5" cols="20" id="description" v-model="brand.description" name="description"></textarea><br>
        状态：
        <input type="radio" name="status" v-model="brand.status" value="0">禁用
        <input type="radio" name="status" v-model="brand.status" value="1">启用<br>

        <input type="button" id="btn" @click="submitForm" value="提交">
    </form>
</div>
<script src="js/axios-0.18.0.js"></script>
<script src="js/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data(){
            return {
                brand:{}
            }
        },
        methods:{
            submitForm(){
                // 发送ajax请求，添加
                var _this = this;
                axios({
                    method:"post",
                    url:"http://localhost:8080/brand-demo/addServlet",
                    data:_this.brand
                }).then(function (resp) {
                    // 判断响应数据是否为 success
                    if(resp.data == "success"){
                        location.href = "http://localhost:8080/brand-demo/brand.html";
                    }
                })
            }
        }
    })
</script>
</body>
</html>
```

通过上面的优化，前端代码确实简化了不少。但是页面依旧是不怎么好看，那么接下来我们学习 Element，它可以美化页面。

### 1.7 vue脚手架进行模块化开发

#### 1.7.1 全局安装webpack

在任意目录下cmd，注意命令尾部“-g” 是全局安装的意思。

```
npm install webpack -g
```

默认安装到目录：

![](https://i-blog.csdnimg.cn/blog_migrate/51ffabbe0b5637b0a21e37bfd1d05dd0.png)

#### 1.7.2 全局安装vue脚手架

```bash
npm install -g @vue/cli@4.0.3
```

> **注意：**脚手架版本和node版本要匹配，我node版本10.16.3，匹配脚手架4.0.3 

#### 1.7.3 初始化vue项目

在工程文件夹下cmd，输入以下命令初始化vue项目。建议工程名与文件夹名一致

```bash
vue init webpack 想要起的工程名
#vue init webpack vue-demo
```

![image-20210927110259380](https://i-blog.csdnimg.cn/blog_migrate/712ffa1d36a054c851fea3a0dae4d726.png)​

> standalone单例是选择运行+编译：![](https://i-blog.csdnimg.cn/blog_migrate/230738f37a3bfa9f049bdd643614be4f.png)
> 
> ESLint是检查代码规范的，这里不选否。 
> 
> test是否使用单元测试，这里也是否

> 如果一直卡在downloading template，配置淘宝镜像
> 
> ```
> npm config set chromedriver_cdnurl https://npm.taobao.org/mirrors/chromedriver
> ```

**初始化成功，运行项目**

```bash
cd vue-demo

```

```bash
npm run dev
```

>  **为什么运行命令是npm run dev?**
> 
> 在项目目录下，我们可以看到一个名为package.json的文件，该文件是对项目、模块包的描述，在package.json文件中，有一个scripts的字段:
> 
> ```javascript
>   "scripts": {
>     "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
>     "start": "npm run dev",
>     "build": "node build/build.js"
>   },
> ```
> 
> 修改后运行命令就是npm run serve：
> 
> ```javascript
> // 运行npm run serve的scripts字段
>   "scripts": {
>     "serve": "vue-cli-service serve",
>     "build": "vue-cli-service build",
>     "lint": "vue-cli-service lint"
>   },
> ```

**启动成功**

![](https://i-blog.csdnimg.cn/blog_migrate/d0775746ef4540e85b878c436ad0af2e.png)

**访问默认端口**[http://localhost:8080/#/](http://localhost:8080/#/ "http://localhost:8080/#/")**。**

![image-20210927110328858](https://i-blog.csdnimg.cn/blog_migrate/79ea857002cfa71819c17322db577e75.png)​

关闭cmd窗口，在vscode打开项目，重新启动： 

```bash
npm run dev
```

#### 1.7.4 vue项目目录结构

![](https://i-blog.csdnimg.cn/blog_migrate/022c4d96bf23a2dc647c6ebc198f1f7b.png)

| 
目录/文件

 | 

说明

 |
| --- | --- |
| 

build

 | 

项目构建(webpack)相关代码

 |
| 

config

 | 

配置目录，包括端口号等。我们初学可以使用默认的。

 |
| 

node\_modules

 | 

npm 加载的项目依赖模块。类似于maven的本地仓库

 |
| 

**src**

 | 

这里是我们**要开发的目录**，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：`assets`: 放置一些图片，如logo等。`components`: 目录里面放了一个组件文件，可以不用。`App.vue`: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。`main.js`: 项目的核心文件。

 |
| 

**static**

 | 

**静态资源目录，如图片、字体等。**

 |
| 

test

 | 

初始测试目录，可删除

 |
| 

.xxxx文件

 | 

这些是一些配置文件，包括语法配置，git配置等。例如.env配置端口

 |
| 

index.html

 | 

首页入口文件。

 |
| 

package.json

 | 

项目配置文件。类似于maven的pom

 |
| 

README.md

 | 

项目的说明文档，markdown 格式

 |

#### 1.7.5 **分析主页展示逻辑**

> /config/**index.js配置端口：**
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/d2c68bb4afc111829f0b390776ee00d8.png)

**/index.html主页**

其中只有一个`div，内容由src/main.js主程序决定。`

```html
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
```

src/**main.js****主程序，里面有vue实例挂载id为“app”元素：**

```java
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
//创建vue实例挂载“app”元素
new Vue({
  el: '#app',
  router, //采用router路由，导入位置./router。这里是简写，完整是router:router
  components: { App },//绑定App组件。完整是App:App
  template: '<App/>'    //元素渲染模板
})
```

**主组件/src/App.vue，显示页面并引入路由规则**

-   首先显示一张图片，图片路径为`"./assets/logo.png`
    
-   其中的`<router-view/>`是根据url要决定访问的vue,在main.js中提及了使用的是`./router`规则
    

```html
<!--模板标签，编写页面展示内容-->
<template>
  <div id="app">
<!--这里引进了一个图片-->
    <img src="./assets/logo.png">
<!--路由视图，/src/router/index.js路由规则配置访问的模块-->
    <router-view/>
  </div>
</template>

<!--vue实例代码-->
<script>
export default {
  name: 'App'
}
</script>

<!--当前模板样式-->
<style>
...
</style>
```

**配置路由规则**/src/router/**index.js**

routes表示路由规则

当访问`/`时， 显示组件`Helloword`

```javascript
import Vue from 'vue'
import Router from 'vue-router'
import HelloWorld from '@/components/HelloWorld'

Vue.use(Router)

export default new Router({
  routes: [
//访问跟路径时，路由到helloworld模块
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    }
  ]
})
```

/src/components/**HelloWorld.vue组件**

```html
<!--模板，设置内容-->
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li>
        <a
          href="https://vuejs.org"
          target="_blank"
        >
          Core Docs
        </a>
      </li>
      <li>
        <a
          href="https://forum.vuejs.org"
          target="_blank"
        >
          Forum
        </a>
      </li>
      <li>
        <a
          href="https://chat.vuejs.org"
          target="_blank"
        >
          Community Chat
        </a>
      </li>
      <li>
        <a
          href="https://twitter.com/vuejs"
          target="_blank"
        >
          Twitter
        </a>
      </li>
      <br>
      <li>
        <a
          href="http://vuejs-templates.github.io/webpack/"
          target="_blank"
        >
          Docs for This Template
        </a>
      </li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li>
        <a
          href="http://router.vuejs.org/"
          target="_blank"
        >
          vue-router
        </a>
      </li>
      <li>
        <a
          href="http://vuex.vuejs.org/"
          target="_blank"
        >
          vuex
        </a>
      </li>
      <li>
        <a
          href="http://vue-loader.vuejs.org/"
          target="_blank"
        >
          vue-loader
        </a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/awesome-vue"
          target="_blank"
        >
          awesome-vue
        </a>
      </li>
    </ul>
  </div>
</template>

<!--script，vue实例代码。-->
<script>
<!--这里导出组件，名为“HelloWorld”，在路由文件/src/router/index.js会进行导入-->
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!--style ，设置样式-->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
```

#### 1.7**.6 新建Hello组件，负责/hello路径**

/src/components**创建hello.vue组件，编写组件三标签：**

```html
<template>
    <div>
        <h1>你好，hello，{{name}}</h1>
    </div>
</template>

<script>
<!--导出组件，在路由文件/src/router/index.js会导入-->
export default {
    data(){
        return {
            name: "张三"
        }
    }
}
</script>

<style>

</style>
```

**编写路由文件**，修改/src/router/index.js

```java
import Vue from 'vue'
import Router from 'vue-router'
import HelloWorld from '@/components/HelloWorld'
import Hello from '@/components/hello' //导入自定义的组件

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    },
    //新增路由
    {
      path: '/hello',
      name: "Hello",
      component: Hello
    }
  ]
})
```

**此时访问**[http://localhost:8080/#/hello](http://localhost:8080/#/hello "http://localhost:8080/#/hello")

![](https://i-blog.csdnimg.cn/blog_migrate/0164084f137693be04ae293bb8c060ac.png)

**添加App.vue点击跳转**，修改/src/App.vue的template标签：

```html
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-link to="/hello">去hello</router-link> <!--新增去hello-->
    <router-link to="/">去首页</router-link><!--新增去首页-->
    <router-view/>
  </div>
</template>
```

运行测试效果

![](https://i-blog.csdnimg.cn/blog_migrate/7ad9285646aa70d63ab59951f33b971d.png)

#### 1.7.7 快速生成组件模板

1、文件->首选项->用户代码 新建全局代码片段

2、把下面代码粘贴进去

```java
{
    "Print to console": {
        "prefix": "vue",
        "body": [
            "<!-- $1 -->",
            "<template>",
            "<div class='$2'>$5</div>",
            "</template>",
            "",
            "<script>",
            "//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）",
            "//例如：import 《组件名称》 from '《组件路径》';",
            "",
            "export default {",
            "//import引入的组件需要注入到对象中才能使用",
            "components: {},",
            "data() {",
            "//这里存放数据",
            "return {",
            "",
            "};",
            "},",
            "//监听属性 类似于data概念",
            "computed: {},",
            "//监控data中的数据变化",
            "watch: {},",
            "//方法集合",
            "methods: {",
            "",
            "},",
            "//生命周期 - 创建完成（可以访问当前this实例）",
            "created() {",
            "",
            "},",
            "//生命周期 - 挂载完成（可以访问DOM元素）",
            "mounted() {",
            "",
            "},",
            "beforeCreate() {}, //生命周期 - 创建之前",
            "beforeMount() {}, //生命周期 - 挂载之前",
            "beforeUpdate() {}, //生命周期 - 更新之前",
            "updated() {}, //生命周期 - 更新之后",
            "beforeDestroy() {}, //生命周期 - 销毁之前",
            "destroyed() {}, //生命周期 - 销毁完成",
            "activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发",
            "}",
            "</script>",
            "<style scoped>",
            "$4",
            "</style>"
        ],
        "description": "生成vue模板"
    }
    
}
```

3、在创建组件时直接输入`vue`点击回车就可生成模板

## 2，Element

**Element：**是饿了么公司前端开发团队提供的一套**基于 Vue 的网站组件库，用于快速构建网页。**

Element 提供了很多**组件**（组成网页的部件）供我们使用。例如 超链接、按钮、图片、表格等等~

如下图左边的是我们编写页面看到的按钮，上图右边的是 Element 提供的页面效果，效果一目了然。

![](https://i-blog.csdnimg.cn/blog_migrate/7d75feb21c2a2db56867ff27007296d7.png)

我们学习 Element 其实就是学习怎么**从官网拷贝组件到我们自己的页面并进行修改。**

**官网网址**（基于vue2）

```
https://element.eleme.cn/#/zh-CN
```

进入官网能看到如下页面

![](https://i-blog.csdnimg.cn/blog_migrate/b058487aed9d11fa78ab3f7dba269919.png)

接下来直接点击 `组件` ，页面如下

![](https://i-blog.csdnimg.cn/blog_migrate/1deff34985457e2cfb7f7f6b65b160a3.png)

### 2.1 快速入门，使用el-button组件

1.  将资源 `element-ui` 文件夹直接拷贝到项目的 `webapp` 下。目录结构如下
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/f19043bd901bbe6a1d29a81137412409.png)
    
2.  创建页面，并在页面引入**Element 的css、js文件 和 Vue.js**
    
    ```html
    <script src="js/vue.js"></script>
    <script src="element-ui/lib/index.js"></script>
    <link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">
    ```
    
3.  .创建Vue核心对象
    
    Element 是基于 Vue 的，所以使用Element时必须要创建 Vue 对象
    
    ```html
    <script>
        new Vue({
            el:"#app"
        })
    </script>
    ```
    
4.  官网复制Element组件代码![](https://i-blog.csdnimg.cn/blog_migrate/090df77fb35a1b1f3d97ab69a8f2ee9d.png)
    
    在左菜单栏找到 `Button 按钮` ，然后找到自己喜欢的按钮样式，点击 `显示代码` ，在下面就会展示出对应的代码，将这些代码拷贝到我们自己的页面即可。
    

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">


    <el-row>
     	<el-button>默认按钮</el-button>
        <el-button type="primary">主要按钮</el-button>
        <el-button type="success">成功按钮</el-button>
        <el-button type="info">信息按钮</el-button>
        <el-button type="warning">警告按钮</el-button>
        <el-button type="danger">删除</el-button>
    </el-row>

</div>

<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el:"#app"
    })
</script>

</body>
</html>
```

### 2.2 Element 布局

**网站：** 

[Element - The world's most popular Vue UI framework](https://element.eleme.cn/#/zh-CN/component/layout "Element - The world's most popular Vue UI framework")

Element 提供了两种布局方式，分别是：

-   Layout 布局
    
-   Container 布局容器
    

#### 2.2.1 Layout 局部

通过基础的 24 分栏，迅速简便地创建布局。也就是默认将一行分为 24 栏，根据页面要求给每一列设置所占的栏数。

![](https://i-blog.csdnimg.cn/blog_migrate/a5ca1074ba10f2d5e3bd9c7f5776cedf.png)

在左菜单栏找到 `Layout 布局` ，点击 `显示代码` ，在下面就会展示出对应的代码，显示出的代码中有样式，有html标签。

将样式<style>拷贝我们自己页面的 `head` 标签内，将html标签拷贝到 `<div id="app"></div>` 标签内。

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        .el-row {
            margin-bottom: 20px;
        }
        .el-col {
            border-radius: 4px;
        }
        .bg-purple-dark {
            background: #99a9bf;
        }
        .bg-purple {
            background: #d3dce6;
        }
        .bg-purple-light {
            background: #e5e9f2;
        }
        .grid-content {
            border-radius: 4px;
            min-height: 36px;
        }
        .row-bg {
            padding: 10px 0;
            background-color: #f9fafc;
        }
    </style>
</head>
<body>
<div id="app">
    <el-row>
        <el-col :span="24"><div class="grid-content bg-purple-dark"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="12"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="6"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="6"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
</div>
<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el:"#app"
    })
</script>
</body>
</html>
```

现在需要添加一行，要求该行显示8个格子，通过计算每个格子占 3 栏，具体的html 代码如下

```html
<!--
添加一行，8个格子  24/8 = 3
-->
<el-row>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
</el-row>
```

#### 2.2.2 Container 布局容器

用于布局的容器组件，方便快速搭建页面的基本结构。如下图就是布局容器效果。

如下图是官网提供的 Container 布局容器实例：

![](https://i-blog.csdnimg.cn/blog_migrate/021dca13bb6ba2581c2ce53e49a99937.png)

该效果代码中包含了样式、页面标签、模型数据。将里面的样式 `<style>` 拷贝到我们自己页面的 `head` 标签中；将html标签拷贝到 `<div id="app"></div>` 标签中，再将数据模型拷贝到 `vue` 对象的 `data()` 中。

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        .el-header {
            background-color: #B3C0D1;
            color: #333;
            line-height: 60px;
        }

        .el-aside {
            color: #333;
        }
    </style>
</head>
<body>
<div id="app">
    <el-container style="height: 500px; border: 1px solid #eee">
        <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
            <el-menu :default-openeds="['1', '3']">
                <el-submenu index="1">
                    <template slot="title"><i class="el-icon-message"></i>导航一</template>
                    <el-menu-item-group>
                        <template slot="title">分组一</template>
                        <el-menu-item index="1-1">选项1</el-menu-item>
                        <el-menu-item index="1-2">选项2</el-menu-item>
                    </el-menu-item-group>
                    <el-menu-item-group title="分组2">
                        <el-menu-item index="1-3">选项3</el-menu-item>
                    </el-menu-item-group>
                    <el-submenu index="1-4">
                        <template slot="title">选项4</template>
                        <el-menu-item index="1-4-1">选项4-1</el-menu-item>
                    </el-submenu>
                </el-submenu>
                <el-submenu index="2">
                    <template slot="title"><i class="el-icon-menu"></i>导航二</template>
                    <el-submenu index="2-1">
                        <template slot="title">选项1</template>
                        <el-menu-item index="2-1-1">选项1-1</el-menu-item>
                    </el-submenu>
                </el-submenu>
                <el-submenu index="3">
                    <template slot="title"><i class="el-icon-setting"></i>导航三</template>
                    <el-menu-item-group>
                        <template slot="title">分组一</template>
                        <el-menu-item index="3-1">选项1</el-menu-item>
                        <el-menu-item index="3-2">选项2</el-menu-item>
                    </el-menu-item-group>
                    <el-menu-item-group title="分组2">
                        <el-menu-item index="3-3">选项3</el-menu-item>
                    </el-menu-item-group>
                    <el-submenu index="3-4">
                        <template slot="title">选项4</template>
                        <el-menu-item index="3-4-1">选项4-1</el-menu-item>
                    </el-submenu>
                </el-submenu>
            </el-menu>
        </el-aside>

        <el-container>
            <el-header style="text-align: right; font-size: 12px">
                <el-dropdown>
                    <i class="el-icon-setting" style="margin-right: 15px"></i>
                    <el-dropdown-menu slot="dropdown">
                        <el-dropdown-item>查看</el-dropdown-item>
                        <el-dropdown-item>新增</el-dropdown-item>
                        <el-dropdown-item>删除</el-dropdown-item>
                    </el-dropdown-menu>
                </el-dropdown>
                <span>王小虎</span>
            </el-header>

            <el-main>
                <el-table :data="tableData">
                    <el-table-column prop="date" label="日期" width="140">
                    </el-table-column>
                    <el-table-column prop="name" label="姓名" width="120">
                    </el-table-column>
                    <el-table-column prop="address" label="地址">
                    </el-table-column>
                </el-table>
            </el-main>
        </el-container>
    </el-container>
</div>
<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el:"#app",
        data() {
            const item = {
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            };
            return {
                tableData: Array(20).fill(item)
            }
        }
    })
</script>
</body>
</html>
```

### 2.3 案例，element商品列表展示

其他的组件我们通过完成一个页面来学习。

我们要完成如下页面效果

![](https://i-blog.csdnimg.cn/blog_migrate/ebc1b2ff345df26d5f9a1bb2843b45a8.png)

要完成该页面，我们需要先对这个页面进行分析，看页面由哪儿几部分组成，然后到官网进行拷贝并修改。页面总共有如下组成部分

![](https://i-blog.csdnimg.cn/blog_migrate/4322a48b564f925094465d3617d5a28d.png)

还有一个是当我们点击 `新增` 按钮，会在页面正中间弹出一个对话框，如下

![](https://i-blog.csdnimg.cn/blog_migrate/11eb7c917709a97f3913949f8d56d6fd.png)

#### 2.3.1 准备基本页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
	
</div>

<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el: "#app"
    })
</script>
</body>
</html>
```

#### 2.3.2 完成表格展示商品

使用 Element 整体的思路就是 **拷贝 + 修改**。

**拷贝**

![](https://i-blog.csdnimg.cn/blog_migrate/4a0c8707ffaeaf840af4802f3f91afd9.png)

在左菜单栏找到 `Table 表格`并点击，右边主体就会定位到表格这一块，找到我们需要的表格效果**带状态表格**（主要样式，像按钮、复选框等都后面自定义），点击 `显示代码` 就可以看到这个表格的代码了，拷贝并修改：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .el-table .warning-row {
            background: oldlace;
        }

        .el-table .success-row {
            background: #f0f9eb;
        }
    </style>
</head>
<body>
<div id="app">
    <template>
        <el-table
                :data="tableData"
                style="width: 100%"
                :row-class-name="tableRowClassName">
            <el-table-column
                    prop="date"
                    label="日期"
                    width="180">
            </el-table-column>
            <el-table-column
                    prop="name"
                    label="姓名"
                    width="180">
            </el-table-column>
            <el-table-column
                    prop="address"
                    label="地址">
            </el-table-column>
        </el-table>
    </template>
</div>

<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el:"#app",
        methods: {
            tableRowClassName({row, rowIndex}) {
                if (rowIndex === 1) {
                    return 'warning-row';
                } else if (rowIndex === 3) {
                    return 'success-row';
                }
                return '';
            }
        },
        data() {
            return {
                tableData: [{
                    date: '2016-05-02',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄',
                }, {
                    date: '2016-05-04',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄'
                }, {
                    date: '2016-05-01',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄',
                }, {
                    date: '2016-05-03',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄'
                }]
            }
        }
    })
</script>
</body>
</html>
```

拷贝完成后通过浏览器打开可以看到表格的效果

![](https://i-blog.csdnimg.cn/blog_migrate/93bcda570559062c943cc335ad6562ec.png)

表格效果出来了，但是显示的表头和数据并不是我们想要的，所以接下来就需要对页面代码进行修改了。

**修改**

1.  **修改表头和数据**
    
    下面是对表格代码进行分析的图解。根据下图说明修改自己的列数和列名![](https://i-blog.csdnimg.cn/blog_migrate/cfb0e7a5d1a284c6dd9b24ce40e40ffa.png)
    
    修改完页面后，还需要对绑定的模型数据进行修改，下图是对模型数据进行分析的图解![](https://i-blog.csdnimg.cn/blog_migrate/6318d22bae23186e8d21e8eb6b7bd4ad.png)
    
2.  **给表格添加操作列**
    
    从之前的表格拷贝一列出来并对其进行修改。按钮是从官网的 `Button 按钮` 组件中拷贝并修改的![](https://i-blog.csdnimg.cn/blog_migrate/21a19f7b9c27328bd8030aa99a4f1a2d.png)
    
3.  **给表格添加复选框列和标号列**
    
    给表格添加复选框和标号列，效果如下![](https://i-blog.csdnimg.cn/blog_migrate/d41b1bf6b6f5e1cc6a3f2392b9ac58a2.png)
    
    此效果也是从 Element 官网进行拷贝，先找到对应的表格效果，然后将其对应代码拷贝到我们的代码中，如下是复选框列官网效果图和代码![](https://i-blog.csdnimg.cn/blog_migrate/f5e88536dae11cb3d840dbec7baca6a9.png)
    
    这里需要注意在 `<el-table>` 标签上有一个事件 `@selection-change="handleSelectionChange"` ，这里绑定的函数也需要从官网拷贝到我们自己的页面代码中，函数代码如下：![](https://i-blog.csdnimg.cn/blog_migrate/63e90d7ec63f00ffd4fe88c3718360cc.png)
    
    从该函数中又发现还需要一个模型数据 `multipleSelection` ，所以还需要定义出该模型数据
    

标号列也用同样的方式进行拷贝并修改。

![](https://i-blog.csdnimg.cn/blog_migrate/a07c21476cd45228279d1a4558d75702.png)

#### 2.3.3 完成搜索表单展示

在 Element 官网找到横排的表单效果，然后拷贝代码并进行修改

![](https://i-blog.csdnimg.cn/blog_migrate/36099bd0abe59f83fe1f7ae6d1371ac0.png)

点击上面的 `显示代码` 后，就会展示出对应的代码，下面是对这部分代码进行分析的图解

inline是行内表单模式 

![](https://i-blog.csdnimg.cn/blog_migrate/d245960dccde8c2842a352c5023ee080.png)

然后根据我们要的效果修改代码。

#### 2.3.4 完成批量删除和新增按钮展示

从 Element 官网找具有着色效果的按钮，并将代码拷贝到我们自己的页面上

![](https://i-blog.csdnimg.cn/blog_migrate/54a69f98bcd2bb172fff7165e8e2bfce.png)

#### 2.3.5 完成对话框展示

在 Element 官网找对话框，如下：![](https://i-blog.csdnimg.cn/blog_migrate/b097cd807441f17c70f8b05bd3d9ff49.png)

下面对官网提供的代码进行分析

![](https://i-blog.csdnimg.cn/blog_migrate/19dc50ade4afef60d3534edb3c6c724a.png)

上图分析出来的模型数据需要在 Vue 对象中进行定义。

#### 2.3.6 完成分页条展示

在 Element 官网找到 `Pagination 分页` ，在页面主体部分找到我们需要的效果，如下

![](https://i-blog.csdnimg.cn/blog_migrate/2c5fea84f8becb52ad527ee1ba58fa36.png)

点击 `显示代码` ，找到 `完整功能` 对应的代码，接下来对该代码进行分析

![](https://i-blog.csdnimg.cn/blog_migrate/797b53b0db9a317b219960769a1d8778.png)

上面代码属性说明：

-   `page-size` ：每页显示的条目数
    
-   `page-sizes` ： 每页显示个数选择器的选项设置。
    
    `:page-sizes="[100,200,300,400]"` 对应的页面效果如下：![](https://i-blog.csdnimg.cn/blog_migrate/41f7c074c24ebd1dc10d2a44203ae6df.png)
    
-   `currentPage` ：当前页码。我们点击那个页码，此属性值就是几。
    
-   `total` ：总记录数。用来设置总的数据条目数，该属性设置后， Element 会自动计算出需分多少页并给我们展示对应的页码。
    

事件说明：

-   `size-change` ：pageSize 改变时会触发。也就是当我们改变了每页显示的条目数后，该事件会触发。
    
-   `current-change` ：currentPage 改变时会触发。也就是当我们点击了其他的页码后，该事件会触发。
    

#### 2.3.7 完整页面代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .el-table .warning-row {
            background: oldlace;
        }
        .el-table .success-row {
            background: #f0f9eb;
        }
    </style>
</head>
<body>
<div id="app">
    <!--搜索表单-->
    <!--inline是行内表单模式-->
    <el-form :inline="true" :model="brand" class="demo-form-inline">
        <el-form-item label="当前状态">
            <el-select v-model="brand.status" placeholder="当前状态">
                <el-option label="启用" value="1"></el-option>
                <el-option label="禁用" value="0"></el-option>
            </el-select>
        </el-form-item>

        <el-form-item label="企业名称">
            <el-input v-model="brand.companyName" placeholder="企业名称"></el-input>
        </el-form-item>

        <el-form-item label="品牌名称">
            <el-input v-model="brand.brandName" placeholder="品牌名称"></el-input>
        </el-form-item>

        <el-form-item>
            <el-button type="primary" @click="onSubmit">查询</el-button>
        </el-form-item>
    </el-form>

    <!--按钮-->
    <el-row>
        <el-button type="danger" plain>批量删除</el-button>
        <el-button type="primary" plain @click="dialogVisible = true">新增</el-button>
    </el-row>

    <!--添加数据对话框表单-->
    <el-dialog
            title="编辑品牌"
            :visible.sync="dialogVisible"
            width="30%">
        <el-form ref="form" :model="brand" label-width="80px">
            <el-form-item label="品牌名称">
                <el-input v-model="brand.brandName"></el-input>
            </el-form-item>

            <el-form-item label="企业名称">
                <el-input v-model="brand.companyName"></el-input>
            </el-form-item>

            <el-form-item label="排序">
                <el-input v-model="brand.ordered"></el-input>
            </el-form-item>

            <el-form-item label="备注">
                <el-input type="textarea" v-model="brand.description"></el-input>
            </el-form-item>

            <el-form-item label="状态">
                <el-switch v-model="brand.status"
                           active-value="1"
                           inactive-value="0"
                ></el-switch>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="addBrand">提交</el-button>
                <el-button @click="dialogVisible = false">取消</el-button>
            </el-form-item>
        </el-form>
    </el-dialog>

    <!--表格-->
    <template>
        <!--row-class-name设置行颜色。通过指定 Table 组件的 row-class-name 属性来为 Table 中的某一行添加 class，表明该行处于某种状态。-->
<!--        @selection-change="handleSelectionChange"复选框方法-->
        <el-table
                :data="tableData"
                style="width: 100%"

                :row-class-name="tableRowClassName"
                @selection-change="handleSelectionChange">
            <el-table-column
                    type="selection"
                    width="55">
            </el-table-column>
            <el-table-column
                    type="index"
                    width="50">
            </el-table-column>
            <el-table-column
                    prop="brandName"
                    label="品牌名称"
                    align="center">
            </el-table-column>
            <el-table-column
                    prop="companyName"
                    label="企业名称"
                    align="center">
            </el-table-column>
            <el-table-column
                    prop="ordered"
                    align="center"
                    label="排序">
            </el-table-column>
            <el-table-column
                    prop="status"
                    align="center"
                    label="当前状态">
            </el-table-column>
            <el-table-column
                    align="center"
                    label="操作">
                <el-row>
                    <el-button type="primary">修改</el-button>
                    <el-button type="danger">删除</el-button>
                </el-row>
            </el-table-column>

        </el-table>
    </template>

    <!--分页工具条-->
    <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="currentPage"
            :page-sizes="[5, 10, 15, 20]"
            :page-size="5"
            layout="total, sizes, prev, pager, next, jumper"
            :total="400">
    </el-pagination>

</div>
<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">
<script>
    new Vue({
        el: "#app",
        methods: {
            // row-class-name="tableRowClassName"，设置行颜色
            tableRowClassName({row, rowIndex}) {
                if (rowIndex %4== 1) {
                    return 'warning-row';
                } else if (rowIndex%4 === 3) {
                    return 'success-row';
                }
                return '';
            },
            // 复选框选中后执行的方法
            handleSelectionChange(val) {
                this.multipleSelection = val;

                console.log(this.multipleSelection)
            },
            // 查询方法
            onSubmit() {
                console.log(this.brand);
            },
            // 添加数据
            addBrand(){
                console.log(this.brand);
            },
            //分页
            handleSizeChange(val) {
                console.log(`每页 ${val} 条`);
            },
            handleCurrentChange(val) {
                console.log(`当前页: ${val}`);
            }
        },
        data() {
            return {
                // 当前页码
                currentPage: 4,
                // 添加数据对话框是否展示的标记
                dialogVisible: false,

                // 品牌模型数据
                brand: {
                    status: '',
                    brandName: '',
                    companyName: '',
                    id:"",
                    ordered:"",
                    description:""
                },
                // 复选框选中数据集合
                multipleSelection: [],
                // 表格数据
                tableData: [{
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }]
            }
        }
    })
</script>
</body>
</html>
```

## 3，综合案例，element商品列表展示增删改查

### 3.1 功能介绍

以上是我们在综合案例要实现的功能。对数据的除了对数据的增删改查功能外，还有一些复杂的功能，如 `批量删除`、`分页查询`、`条件查询` 等功能

-   `批量删除` 功能：每条数据前都有复选框，当我选中多条数据并点击 `批量删除` 按钮后，会发送请求到后端并删除数据库中指定的多条数据。
    
-   `分页查询` 功能：当数据库中有很多数据时，我们不可能将所有的数据展示在一页里，这个时候就需要分页展示数据。
    
-   `条件查询` 功能：数据库量大的时候，我们就需要精确的查询一些想看到的数据，这个时候就需要通过条件查询。 
    

这里的 `修改品牌` 和 `删除品牌` 功能在课程上不做讲解，留作同学来下的练习。

### 3.1.5 坑点总结

**0.Servlet层问题：**

（1）request.getReader()类型是BufferedReader，response.getWriter()类型是PrintWriter

**1.service层问题：**

（1）创建SqlSessionFactory对象是类名.方法创建不是，new创建。

```java
SqlSessionFactory sqlSessionFactory=SqlSessionFactoryUtils.getSqlSessionFactory();
```

（2）运行不报错，但数据没更改，一般都是忘了提交事务。添加修改删除在ServiceImpl别忘了sqlSession.commit();提交事务。

**2.dao层问题**

（1）添加的insert语句别忘了加#{}：

```java
    @Insert("insert into tb_brand values (null,#{brandName},#{companyName},#{ordered},#{description},#{status})")
    void add(Brand brand);
```

（2） like模糊查询的字符串前后要在service里判断非空非null加替换符%。

（3）mapper传参数，如果参数包括对象和散装参数，那么对象必须也注解，写SQL语句时候不能忘记对象.属性，例如brand.status.

下面都是可以的

```java
    List<Brand> selectByPageAndCondition(@Param("begin") int begin,@Param("size") int size,@Param("brand") Brand brand);

//BrandMapper.java
List<Brand> selectByCondition(Brand brand);
//BrandMapper.java
​​​​​​​List<Brand> selectByCondition(Map map);
```

 下面是错误的：

```html
  List<Brand> selectByPageAndCondition(@Param("begin") int begin,Brand brand);
```

**3.前端问题**

（1）注意需要用到\_this的情况，特别是从element组件官网复制过来的组件在方法内别忘了改\_this。 

### 3.2 环境准备

环境准备我们主要完成以下两件事即可

-   将资料的 brand-case 模块导入到 idea中
    
-   执行资料中提供的 tb\_brand.sql脚本
    

#### 3.2.1 工程准备和最终目录结构​​​​​​​

将 `04-资料\01-初始工程` 中的 `brand-case` 工程导入到我们自己的 idea 中。工程结构如下：

![](https://i-blog.csdnimg.cn/blog_migrate/6b34ce44bcbb64a40829b08cf91fc893.png)

下面是开发完成后的目录结构：

 ![](https://i-blog.csdnimg.cn/blog_migrate/b7d6bd8d8060048fdc125a58bf5ebfb4.png)

> 跟以前不同点：web下创建Servlet文件夹存储Servlet文件，service中定义service接口和Imp文件夹存储实现类。 

pom.xml导入Servlet、mybatis,mysql,fastjson依赖,tomcat插件。

```java
package com.itheima.pojo;

public class Brand {
    // id 主键
    private Integer id;
    // 品牌名称
    private String brandName;
    // 企业名称
    private String companyName;
    // 排序字段
    private Integer ordered;
    // 描述信息
    private String description;
    // 状态：0：禁用  1：启用
    private Integer status;


    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getBrandName() {
        return brandName;
    }

    public void setBrandName(String brandName) {
        this.brandName = brandName;
    }

    public String getCompanyName() {
        return companyName;
    }

    public void setCompanyName(String companyName) {
        this.companyName = companyName;
    }

    public Integer getOrdered() {
        return ordered;
    }

    public void setOrdered(Integer ordered) {
        this.ordered = ordered;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public Integer getStatus() {
        return status;
    }
    //逻辑视图
    public String getStatusStr(){
        if (status == null){
            return "未知";
        }
        return status == 0 ? "禁用":"启用";
    }

    public void setStatus(Integer status) {
        this.status = status;
    }

    @Override
    public String toString() {
        return "Brand{" +
                "id=" + id +
                ", brandName='" + brandName + '\'' +
                ", companyName='" + companyName + '\'' +
                ", ordered=" + ordered +
                ", description='" + description + '\'' +
                ", status=" + status +
                '}';
    }
}
```

```java
package com.itheima.util;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class SqlSessionFactoryUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        //静态代码块会随着类的加载而自动执行，且只执行一次
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


    public static SqlSessionFactory getSqlSessionFactory(){
        return sqlSessionFactory;
    }
}
```

#### 3.2.2 创建表

下面是创建表的语句

```sql
-- 删除tb_brand表
drop table if exists tb_brand;
-- 创建tb_brand表
create table tb_brand (
    -- id 主键
    id           int primary key auto_increment,
    -- 品牌名称
    brand_name   varchar(20),
    -- 企业名称
    company_name varchar(20),
    -- 排序字段
    ordered      int,
    -- 描述信息
    description  varchar(100),
    -- 状态：0：禁用  1：启用
    status       int
);
-- 添加数据
insert into tb_brand (brand_name, company_name, ordered, description, status)
values 
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1);
```

### 3.3 查询所有功能

![](https://i-blog.csdnimg.cn/blog_migrate/fd0f051a3cfa75efc56724038388dc54.png)

如上图所示是查询所有品牌数据在页面展示的效果。要实现这个功能，要先搞明白如下问题：

-   什么时候发送异步请求？
    
    页面加载完毕后就需要在页面上看到所有的品牌数据。所以在 `mounted()` 这个构造函数中写发送异步请求的代码。
    
-   请求需要携带参数吗？
    
    查询所有功能不需要携带什么参数。
    
-   响应的数据格式是什么样？
    
    后端是需要将 `List<Brand>` 对象转换为 JSON 格式的数据并响应回给浏览器。响应数据格式如下：
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/8525019c8d9a3f94a2fb464ea7e86663.png)
    

整体流程如下

![](https://i-blog.csdnimg.cn/blog_migrate/930e40dda28a33f58b85382e148f8609.png)

我们先实现后端程序，然后再实现前端程序。

#### 3.3.1 后端实现，service优化

**dao方法实现**

在 `com.itheima.mapper.BrandMapper` 接口中定义抽象方法，并使用 `@Select` 注解编写 sql 语句

```java
/**
     * 查询所有
     * @return
     */
@Select("select * from tb_brand")
List<Brand> selectAll();
```

由于表中有些字段名和实体类中的属性名没有对应，所以需要在 `com/itheima/mapper/BrandMapper.xml` 映射配置文件中定义结果映射 ，使用`resultMap` 标签。映射配置文件内容如下：

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.BrandMapper">

    <resultMap id="brandResultMap" type="brand">
        <result property="brandName" column="brand_name" />
        <result property="companyName" column="company_name" />
    </resultMap>
</mapper>
```

定义完结果映射关系后，在接口 `selectAll()` 方法上引用该结构映射。使用 `@ResultMap("brandResultMap")` 注解

完整接口的 `selectAll()` 方法如下：

```java
/**
     * 查询所有
     * @return
     */
@Select("select * from tb_brand")
@ResultMap("brandResultMap")
List<Brand> selectAll();
```

**service方法实现**

在 `com.itheima.service` 包下**创建 `BrandService` 接口**，在该接口中定义查询所有的抽象方法

```java
public interface BrandService {

    /**
     * 查询所有
     * @return
     */
    List<Brand> selectAll();
}
```

并在 `com.itheima.service` 下再创建 `impl` 包；`impl` 表示是放 service 层接口的实现类的包。 在该包下创建名为 `BrandServiceImpl` 类

```java
public class BrandServiceImpl implements BrandService {

    @Override
    public List<Brand> selectAll() {
    }
}
```

> **定义service 接口的好处**
> 
> 因为service定义了接口后，在 servlet 中就可以使用**多态**的形式创建Service实现类的对象，如下：
> 
> ![](https://i-blog.csdnimg.cn/blog_migrate/611e75903d2b6a70b4c1c46b6c9e3191.png)
> 
> 这里使用多态是因为方便我们**后期解除 `Servlet` 和 `service` 的耦合**。
> 
> 从上面的代码我们可以看到 `SelectAllServlet` 类和 `BrandServiceImpl` 类之间是耦合在一起的，如果后期 `BrandService` 有其它更好的实现类（例如叫 `BrandServiceImpl`），那就需要修改 `SelectAllServlet` 类中的service引用和实例化名代码，而使用多态形式就只需要修改实例化，引用和引用调用的方法、属性就不用更改。
> 
> 后面我们学习了 `Spring` 框架后就可以解除 `SelectAllServlet` 类和红色框括起来的代码耦合。而现在咱们还做不到解除耦合，在这里只需要理解为什么定义接口即可。
> 
> **剧透一下**
> 
> Spring在applicationContext.xml中配置：
> 
> ```XML
>     <bean id="brandService" class="package1.service.impl.BrandServiceImpl"/>
> ```
> 
> 在Servlet里创建Service对象：
> 
> ```java
>         ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
>         BrandService brandService= (BrandService) applicationContext.getBean("BrandService");
> ```
> 
> 至于service和dao之间，通过依赖注入进行解耦：
> 
> ```XML
>     <bean id="bookDao" class="package1.dao.impl.BookDaoImpl"/>
>     <bean id="bookService" class="package1.service.impl.BookServiceImpl">
>         <property name="bookDao" ref="bookDao"/>
>     </bean>
> ```
> 
> ```java
> public class BookServiceImpl implements BookService {
>     public void setBookDao(BookDao bookDao) {
>         this.bookDao = bookDao;
>     }
> 
>     private BookDao bookDao=new BookDaoImpl();
>     @Override
>     public void save() {
> 
>         System.out.println("service save...");
>         bookDao.save();
>     }
> }
> ```

`BrandServiceImpl` 类代码如下：

```java
public class BrandServiceImpl implements BrandService {
    //1. 创建SqlSessionFactory 工厂对象
    SqlSessionFactory factory = SqlSessionFactoryUtils.getSqlSessionFactory();

    @Override
    public List<Brand> selectAll() {
        //2. 获取SqlSession对象
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

        //4. 调用方法
        List<Brand> brands = mapper.selectAll();

        //5. 释放资源
        sqlSession.close();

        return brands;
    }
}
```

**servlet实现**

在 `com.itheima.web.servlet` 包下定义名为 `SelectAllServlet` 的查询所有的 `servlet`。该 `servlet` 逻辑如下：

-   调用service的 `selectAll()` 方法查询所有的品牌数据，并接口返回结果
    
-   将返回的结果转换为 json 数据
    
-   响应 json 数据
    

代码如下：

```java
@WebServlet("/selectAllServlet")
public class SelectAllServlet extends HttpServlet {

    private BrandService brandService = new BrandServiceImpl();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 调用service查询
        List<Brand> brands = brandService.selectAll();
        //2. 转为JSON
        String jsonString = JSON.toJSONString(brands);
        //3. 写数据
        response.setContentType("text/json;charset=utf-8"); //告知浏览器响应的数据是什么， 告知浏览器使用什么字符集进行解码
        response.getWriter().write(jsonString);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

**测试后端程序**

在浏览器输入访问 servlet 的资源路径 `http://localhost:8080/brand-case/selectAllServlet` ，如果没有报错，并能看到如下信息表明后端程序没有问题

![](https://i-blog.csdnimg.cn/blog_migrate/b310174d51e6521f3c2c3b1a8310e72c.png)

#### 3.3.2 前端实现

前端需要在页面加载完毕后发送 ajax 请求，所以发送请求的逻辑应该放在 `mounted()` 钩子函数中。而响应回来的数据需要赋值给表格绑定的数据模型，从下图可以看出表格绑定的数据模型是 `tableData`

![](https://i-blog.csdnimg.cn/blog_migrate/c57035c44aacfc4f43a19b635f7c5131.png)

前端代码如下：

```javascript
 mounted(){
     //当页面加载完成后，发送异步请求，获取数据
     var _this = this;

     axios({
         method:"get",
         url:"http://localhost:8080/brand-case/selectAllServlet"
     }).then(function (resp) {
         _this.tableData = resp.data;
     })
 }
```

## 4，添加功能

![](https://i-blog.csdnimg.cn/blog_migrate/d097b6b710f6aa36374f4795b8644de3.png)

上图是添加数据的对话框，当点击 `提交` 按钮后就需要将数据提交到后端，并将数据保存到数据库中。下图是整体的流程：

![](https://i-blog.csdnimg.cn/blog_migrate/4ca00b83e38120af22757312aecb64b7.png)

页面发送请求时，需要将输入框输入的内容提交给后端程序，而这里是以 json 格式进行传递的。而具体的数据格式如下：

![](https://i-blog.csdnimg.cn/blog_migrate/9acbf4826800db0a501d638381c6dfbc.png)

> **注意：由于是添加数据，所以上述json数据中id是没有值的。**

### 4.1 后端实现

#### 4.1.1 dao方法实现

在 `BrandMapper` 接口中定义 `add()` 添加方法，并使用 `@Insert` 注解编写sql语句

```java
/**
     * 添加数据
     * @param brand
     */
@Insert("insert into tb_brand values(null,#{brandName},#{companyName},#{ordered},#{description},#{status})")
void add(Brand brand);
```

#### 4.1.2 service方法实现

在 `BrandService` 接口中定义 `add()` 添加数据的业务逻辑方法

```java
/**
     * 添加数据
     * @param brand
     */
void add(Brand brand);
```

在 `BrandServiceImpl` 类中重写 `add()` 方法，并进行业务逻辑实现

```java
@Override
public void add(Brand brand) {
    //2. 获取SqlSession对象
    SqlSession sqlSession = factory.openSession();
    //3. 获取BrandMapper
    BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

    //4. 调用方法
    mapper.add(brand);
    sqlSession.commit();//提交事务

    //5. 释放资源
    sqlSession.close();
}
```

> **注意：增删改操作一定要提交事务。**

#### 4.1.3 servlet实现

在 `com.itheima.web.servlet` 包写定义名为 `AddServlet` 的 Servlet。该 Servlet 的逻辑如下：

-   接收页面提交的数据。页面到时候提交的数据是 json 格式的数据，所以此处需要使用输入流读取数据
    
-   将接收到的数据转换为 `Brand` 对象
    
-   调用 service 的 `add()` 方法进行添加的业务逻辑处理
    
-   给浏览器响应添加成功的标识，这里直接给浏览器响应 `success` 字符串表示成功
    

servlet 代码实现如下：

```java
@WebServlet("/addServlet")
public class AddServlet extends HttpServlet {

    private BrandService brandService = new BrandServiceImpl();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 接收品牌数据
        BufferedReader br = request.getReader();
        String params = br.readLine();//json字符串
        //转为Brand对象
        Brand brand = JSON.parseObject(params, Brand.class);
        //2. 调用service添加
        brandService.add(brand);
        //3. 响应成功的标识
        response.getWriter().write("success");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

### 4.2 前端实现

![](https://i-blog.csdnimg.cn/blog_migrate/be6c3577b5dc89943f0c99f230e919ab.png)

上图左边是页面效果，里面的 `提交` 按钮可以通过上图右边看出绑定了一个 单击事件，而该事件绑定的是 `addBrand` 函数，所以添加数据功能的逻辑代码应该写在 `addBrand()` 函数中。在此方法中需要发送异步请求并将表单中输入的数据作为参数进行传递。如下

```javascript
// 添加数据
addBrand() {
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/addServlet",
        data:_this.brand
    }).then(function (resp) {
       	//响应数据的处理逻辑
    })
}
```

在 `then` 函数中的匿名函数是成功后的回调函数，而 `resp.data` 就可以获取到响应回来的数据，如果值是 `success` 表示数据添加成功。成功后我们需要做一下逻辑处理：

1.  **关闭新增对话框窗口**
    
    如下图所示是添加数据的对话框代码，从代码中可以看到此对话框绑定了 `dialogVisible` 数据模型，只需要将该数据模型的值设置为 false，就可以关闭新增对话框窗口了。![](https://i-blog.csdnimg.cn/blog_migrate/8c97d6ec11934169e11efa721a8504c2.png)
    
2.  **重新查询数据**
    
    数据添加成功与否，用户只要能在页面上查看到数据说明添加成功。而此处需要重新发送异步请求获取所有的品牌数据，而这段代码在 `查询所有` 功能中已经实现，所以我们可以将此功能代码进行抽取，抽取到一个 `selectAll()` 函数中
    
    ```javascript
    // 查询所有数据
    selectAll(){
        var _this = this;
    
        axios({
            method:"get",
            url:"http://localhost:8080/brand-case/selectAllServlet"
        }).then(function (resp) {
            _this.tableData = resp.data;
        })
    }
    ```
    
    那么就需要将 `mounted()` 钩子函数中代码改进为
    
    ```javascript
    mounted(){
        //当页面加载完成后，发送异步请求，获取数据
        this.selectAll();
    }
    ```
    
    同时在新增响应的回调中调用 `selectAll()` 进行数据的重新查询。
    
3.  **弹出消息给用户提示添加成功**![](https://i-blog.csdnimg.cn/blog_migrate/c338f98272b28cff3e1794c71217b663.png)
    
    上图左边就是 elementUI 官网提供的成功提示代码，而上图右边是具体的效果。
    
    > **注意：上面的this需要的是表示 VUE 对象的this。**
    

综上所述，前端代码如下：

```javascript
// 添加数据
addBrand() {
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/addServlet",
        data:_this.brand
    }).then(function (resp) {
        if(resp.data == "success"){
            //添加成功
            //关闭窗口
            _this.dialogVisible = false;
            // 重新查询数据
            _this.selectAll();
            // 弹出消息提示
            _this.$message({
                message: '恭喜你，添加成功',
                type: 'success'
            });
        }
    })
}
```

## 5，servlet优化

### 5.1 优化方法，BaseServlet

**问题：** 

**Web 层的 Servlet 个数太多了，不利于管理和编写**

**优化方向：**

一个模块只定义一个 `servlet`，而每一个功能只需要在该 `servlet` 中定义对应的方法。

**具体方案：**

为了做到通用，我们定义一个**通用的 `servlet` 类`BaseServlet`**，在定义其他的 `servlet` 是不需要继承 `HttpServlet`，而**继承我们定义的 `BaseServlet`**。

在`BaseServlet` 中调用具体 `servlet`（如`BrandServlet`）中的对应方法。

**在发送请求时，请求资源的二级路径（/brandServlet/selectAll）和需要调用的方法名保持相同**，如：

查询所有数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/selectAll`

添加数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/add`

修改数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/update`

删除数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/delete`

**BaseServlet：**

```java
public class BaseServlet extends HttpServlet {

    //根据请求的最后一段路径来进行方法分发
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1. 获取请求路径
        String uri = req.getRequestURI(); // 例如路径为：/brand-case/brand/selectAll
        //2. 获取最后一段路径，方法名
        int index = uri.lastIndexOf('/');
        String methodName = uri.substring(index + 1); //  获取到资源的二级路径  selectAll   

        //2. 执行methodName 方法，也就是请求路径最后一段
        //2.1 获取BrandServlet /UserServlet 字节码对象 Class，通过字节码对象获取方法Method对象
        //this代表BaseServlet子类，因为实际应用中，都是子类继承BaseServlet调用这个方法，BaseServlet类不会直接创建对象。
        //System.out.println(this);    

        Class<? extends BaseServlet> cls = this.getClass();
        //2.2 获取方法 Method对象
        try {   
            Method method = cls.getMethod(methodName, HttpServletRequest.class, HttpServletResponse.class);
            //2.3 执行方法
            method.invoke(this,req,resp);
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
    }
}
```

> 回顾Class类的获取方法对象的函数：
> 
> -   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i36"><td>Method</td><td><code><a href="../../java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-" rel="nofollow">getMethod</a>(<a href="../../java/lang/String.html" rel="nofollow">String</a>&nbsp;方法名methodName, <a href="../../java/lang/Class.html" rel="nofollow">类</a>&lt;?&gt;... parameterTypes所有方法参数的字节码)</code><p>返回一个 <code>方法</code>对象，它反映此表示的类或接口的指定公共成员方法 <code>类</code>对象。</p></td></tr></tbody></table>
>         
> 
>  Method类的执行方法的函数：
> 
> -   -   <table border="0" cellpadding="3" cellspacing="0"><tbody><tr id="i18"><td><code><a href="../../../java/lang/Object.html" rel="nofollow">Object</a></code></td><td><code><a href="../../../java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-" rel="nofollow">invoke</a>(<a href="../../../java/lang/Object.html" rel="nofollow">Object</a>&nbsp;obj, <a href="../../../java/lang/Object.html" rel="nofollow">Object</a>...&nbsp;args)</code><p>在具有指定参数的 <code>方法</code>对象上调用此 <code>方法</code>对象表示的底层方法。</p></td></tr></tbody></table>
>         

**BrandServlet：** 

```java
@WebServlet("/brand/*")
public class BrandServlet extends BaseServlet {
    //用户实现分页查询
	public void selectAll(HttpServletRequest req, HttpServletResponse resp) {}
    
    //添加企业信息
    public void add(HttpServletRequest req, HttpServletResponse resp) {}
    
    //修改企业信息
    public void update(HttpServletRequest req, HttpServletResponse resp) {}
    
    //删除企业信息
    public void delete(HttpServletRequest req, HttpServletResponse resp) {}
}
```

### 5.2 代码优化

#### 5.2.1 后端优化

定义了 `BaseServlet` 后，针对品牌模块我们定义一个 `BrandServlet` 的 Servlet，并使其继承 `BaseServlet` 。在`BrandServlet`中定义 以下功能的方法：

-   `查询所有` 功能：方法名声明为 `selectAll` ，并将之前的 `SelectAllServlet` 中的逻辑代码拷贝到该方法中
    
-   `添加数据` 功能：方法名声明为 `add` ，并将之前的 `AddServlet` 中的逻辑代码拷贝到该方法中
    

具体代码如下：

```java
@WebServlet("/brand/*")
public class BrandServlet extends BaseServlet{
    private BrandService brandService = new BrandServiceImpl();

    public void selectAll(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 调用service查询
        List<Brand> brands = brandService.selectAll();

        //2. 转为JSON
        String jsonString = JSON.toJSONString(brands);
        //3. 写数据
        response.setContentType("text/json;charset=utf-8");
        response.getWriter().write(jsonString);
    }

    public void add(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 接收品牌数据
        BufferedReader br = request.getReader();
        String params = br.readLine();//json字符串

        //转为Brand对象
        Brand brand = JSON.parseObject(params, Brand.class);

        //2. 调用service添加
        brandService.add(brand);

        //3. 响应成功的标识
        response.getWriter().write("success");
    }
}
```

#### 5.2.2 前端优化

页面中之前发送的请求的路径都需要进行修改，`selectAll()` 函数中发送异步请求的 `url` 应该改为 `http://localhost:8080/brand-case/brand/selectAll` 。具体代码如下：

```javascript
// 查询分页数据
selectAll(){
    var _this = this;

    axios({
        method:"get",
        url:"http://localhost:8080/brand-case/brand/selectAll"
    }).then(function (resp) {
        _this.tableData = resp.data;
    })
}
```

`addBrand()` 函数中发送异步请求的 `url` 应该改为 `http://localhost:8080/brand-case/brand/add` 。具体代码如下：

```javascript
// 添加数据
addBrand() {
    //console.log(this.brand);
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/brand/add",
        data:_this.brand
    }).then(function (resp) {
        if(resp.data == "success"){
            //添加成功
            //关闭窗口
            _this.dialogVisible = false;
            // 重新查询数据
            _this.selectAll();
            // 弹出消息提示
            _this.$message({
                message: '恭喜你，添加成功',
                type: 'success'
            });
        }
    })
}
```

## 6，批量删除

![](https://i-blog.csdnimg.cn/blog_migrate/5d967e3134fc8fb9e06f4eebe5e3a51e.png)

如上图所示点击多条数据前的复选框就意味着要删除这些数据，而点击了 `批量删除` 按钮后，需要让用户确认一下，因为有可能是用户误操作的，当用户确定后需要给后端发送请求并携带者需要删除数据的多个id值，后端程序删除数据库中的数据。具体的流程如下：

![](https://i-blog.csdnimg.cn/blog_migrate/3e197bbf00bf88b06428aee4cb680da7.png)

**注意：**

前端发送请求时需要将要删除的多个id值以json格式提交给后端，而该json格式数据如下：

```
[1,2,3,4]
```

### 6.1 后端实现

#### 6.1.1 dao方法实现

在 `BrandMapper` 接口中定义 `deleteByIds()` 添加方法，由于这里面要用到动态 sql ，属于复杂的sql操作，建议使用映射配置文件。

接口方法声明如下：

```java
 /**
     * 批量删除
     * @param ids
     */
void deleteByIds(@Param("ids") int[] ids);
```

在 `BrandMapper.xml` 映射配置文件中添加 statement

```XML
<delete id="deleteByIds">
    delete from tb_brand where id in
    <foreach collection="ids" item="id" separator="," open="(" close=")">
        #{id}
    </foreach>
</delete>
```

#### 6.1.2 service方法实现

在 `BrandService` 接口中定义 `deleteByIds()` 批量删除的业务逻辑方法

```java
/**
     * 批量删除
     * @param ids
     */
void deleteByIds( int[] ids);
```

在 `BrandServiceImpl` 类中重写 `deleteByIds()` 方法，并进行业务逻辑实现

```java
@Override
public void deleteByIds(int[] ids) {
    //2. 获取SqlSession对象
    SqlSession sqlSession = factory.openSession();
    //3. 获取BrandMapper
    BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

    //4. 调用方法
    mapper.deleteByIds(ids);

    sqlSession.commit();//提交事务

    //5. 释放资源
    sqlSession.close();
}
```

#### 6.1.3 servlet实现

在 `BrandServlet` 类中定义 `deleteByIds()` 方法。而该方法的逻辑如下：

-   接收页面提交的数据。页面到时候提交的数据是 json 格式的数据，所以此处需要使用输入流读取数据
    
-   接收页面提交的数据。页面到时候提交的数据是 json 格式的数据，所以此处需要使用输入流读取数据
    
-   将接收到的数据转换为 `int[]` 数组
    
-   调用 service 的 `deleteByIds()` 方法进行批量删除的业务逻辑处理
    
-   给浏览器响应添加成功的标识，这里直接给浏览器响应 `success` 字符串表示成功
    

servlet 中 `deleteByIds()` 方法代码实现如下：

```java
public void deleteByIds(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //1. 接收数据 json  [1,2,3]
    BufferedReader br = request.getReader();
    String params = br.readLine();//json字符串
    //转为 int[]
    int[] ids = JSON.parseObject(params, int[].class);
    //2. 调用service添加
    brandService.deleteByIds(ids);
    //3. 响应成功的标识
    response.getWriter().write("success");
}
```

### 6.2 前端实现

此功能的前端代码实现稍微有点麻烦，分为以下几步实现

#### 6.2.1 获取选中的id值

![](https://i-blog.csdnimg.cn/blog_migrate/0a521d328f9a38ac7dd680c010ef0a03.png)

从上图可以看出表格复选框绑定了一个 `selection-change` 事件，该事件是当选择项发生变化时会触发。该事件绑定了 `handleSelectionChange` 函数，而该函数有一个参数 `val` ，该参数是获取选中行的数据，如下

![](https://i-blog.csdnimg.cn/blog_migrate/5b5a56e33790d7af8296877c0230aece.png)

而我们只需要将所有选中数据的id值提交给服务端即可，获取id的逻辑我们书写在 `批量删除` 按钮绑定的函数中。

在 `批量删除` 按钮绑定单击事件，并给绑定触发时调用的函数，如下

![](https://i-blog.csdnimg.cn/blog_migrate/106fc6addeebf7eb831ce2427f6516fb.png)

并在Vue对象中的 methods 中定义 `deleteByIds()` 函数，在该函数中从 `multipleSelection` 数据模型中获取所选数据的id值。要完成这个功能需要在 Vue 对象中定义一个数据模型 `selectedIds:[]`，在 `deleteByIds()` 函数中遍历 `multipleSelection` 数组，并获取到每一个所选数据的id值存储到 `selectedIds` 数组中，代码实现如下：

```javascript
//1. 创建id数组 [1,2,3], 从 this.multipleSelection 获取即可
for (let i = 0; i < this.multipleSelection.length; i++) {
    let selectionElement = this.multipleSelection[i];
    this.selectedIds[i] = selectionElement.id;
}
```

#### 6.2.2 发送异步请求

使用 axios 发送异步请求并经上一步获取到的存储所有的 id 数组作为请求参数

```javascript
//2. 发送AJAX请求
var _this = this;

// 发送ajax请求，添加数据
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/deleteByIds",
    data:_this.selectedIds
}).then(function (resp) {
    if(resp.data == "success"){
        //删除成功
        // 重新查询数据
        _this.selectAll();
        // 弹出消息提示
        _this.$message({
            message: '恭喜你，删除成功',
            type: 'success'
        });
    }
})
```

#### 6.2.3 确定框实现

由于删除操作是比较危险的；有时候可能是由于用户的误操作点击了 `批量删除` 按钮，所以在点击了按钮后需要先给用户确认提示。而确认框在 `elementUI` 中也提供了，如下图

![](https://i-blog.csdnimg.cn/blog_migrate/934e8bdb19b589f0e2d032d63d7642f8.png)

而在点击 `确定` 按钮后需要执行之前删除的逻辑。因此前端代码实现如下：

```javascript
 // 批量删除
deleteByIds(){
    // 弹出确认提示框
    this.$confirm('此操作将删除该数据, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
    }).then(() => {
        //用户点击确认按钮
        //1. 创建id数组 [1,2,3], 从 this.multipleSelection 获取即可
        for (let i = 0; i < this.multipleSelection.length; i++) {
            let selectionElement = this.multipleSelection[i];
            this.selectedIds[i] = selectionElement.id;
        }
        //2. 发送AJAX请求
        var _this = this;
        // 发送ajax请求，添加数据
        axios({
            method:"post",
            url:"http://localhost:8080/brand-case/brand/deleteByIds",
            data:_this.selectedIds
        }).then(function (resp) {
            if(resp.data == "success"){
                //删除成功
                // 重新查询数据
                _this.selectAll();
                // 弹出消息提示
                _this.$message({
                    message: '恭喜你，删除成功',
                    type: 'success'
                });
            }
        })
    }).catch(() => {
        //用户点击取消按钮
        this.$message({
            type: 'info',
            message: '已取消删除'
        });
    });
}
```

## 7，分页查询

我们之前做的 `查询所有` 功能中将数据库中所有的数据查询出来并展示到页面上，试想如果数据库中的数据有很多（假设有十几万条）的时候，将数据全部展示出来肯定不现实，那如何解决这个问题呢？几乎所有的网站都会使用分页解决这个问题。每次只展示一页的数据，比如一页展示10条数据，如果还想看其他的数据，可以通过点击页码进行查询

![](https://i-blog.csdnimg.cn/blog_migrate/315c0c67d3a4fe1f639dcb84e5938278.png)

### 7.1 分析

#### 7.1.1 分页查询sql

分页查询也是从数据库进行查询的，所以我们要分页对应的SQL语句应该怎么写。分页查询使用 `LIMIT` 关键字，格式为：**`LIMIT 开始索引 每页显示的条数`**。以后前端页面在发送请求携带参数时，它并不明确开始索引是什么，但是它知道查询第几页。所以 `开始索引` 需要在后端进行计算，计算的公式是 ：**开始索引 = （当前页码 - 1）\* 每页显示条数**

比如查询第一页的数据的 SQL 语句是：

```sql
select * from tb_brand  limit 0,5;
```

查询第二页的数据的 SQL 语句是：

```sql
select * from tb_brand  limit 5,5;
```

查询第三页的数据的 SQL 语句是：

```sql
select * from tb_brand  limit 10,5;
```

#### 7.1.2 前后端数据分析

分页查询功能时候比较复杂的，所以我们要先分析清楚以下两个问题：

-   **前端需要传递什么参数给后端**
    
    根据上一步对分页查询 SQL 语句分析得出，前端需要给后端两个参数
    
    -   当前页码 ： currentPage
        
    -   每页显示条数：pageSize
        
-   **后端需要响应什么数据给前端**![](https://i-blog.csdnimg.cn/blog_migrate/7d20f9bb13fe55f4b3a77fca2a532586.png)
    
    **后端需要响应的数据**
    
    -   **当前页需要展示的数据。**一般会存储到 List 集合中
        
    -   **总共记录数。**在上图页面中需要展示总的记录数，所以这部分数据也需要。总的页面 elementUI 的分页组件会自动计算，我们不需要关心
        
    
    而这两部分需要封装到 **PageBean 对象**中，并将该对象转换为 json 格式的数据响应回给浏览器![](https://i-blog.csdnimg.cn/blog_migrate/1271c46e2a767d33effa121ae754b4a6.png)
    

通过上面的分析我们需要先在 `pojo` 包下创建 `PageBean` 类，为了做到通过会将其定义成**泛型类**，代码如下：

```java
//分页查询的JavaBean
public class PageBean<T> {
    // 总记录数
    private int totalCount;
    // 当前页数据
    private List<T> rows;


    public int getTotalCount() {
        return totalCount;
    }

    public void setTotalCount(int totalCount) {
        this.totalCount = totalCount;
    }

    public List<T> getRows() {
        return rows;
    }

    public void setRows(List<T> rows) {
        this.rows = rows;
    }
}
```

#### 7.1.25 JavaBean

**JavaBean定义：**

JavaBean 是一种[JAVA语言](https://baike.baidu.com/item/JAVA%E8%AF%AD%E8%A8%80/4148931 "JAVA语言")写成的可重用组件。

**JavaBean特点：**

1.  public 修饰的类 ,具有无参构造方法
2.  所有属性(如果有) 都是private，并且提供set/get (如果boolean 则get 可以替换成is)

**javaBean分两种**

1.  第一种：封装数据的JavaBean  
    这种JavaBean也被叫做实体类，一般来说对应的是数据库中的一张表，例如这样的↓：

```java
public class UserDemo {
	private int id;
	private String uname;
	private String upwd;
	
	public Login() {
	}
	
	public Login( String uname, String upwd) {
		this.uname = uname;
		this.upwd = upwd;
	}
	
	
	public Login(int id, String uname, String upwd) {
		this.id = id;
		this.uname = uname;
		this.upwd = upwd;
	}
	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getUname() {
		return uname;
	}
	public void setUname(String uname) {
		this.uname = uname;
	}
	public String getUpwd() {
		return upwd;
	}
	public void setUpwd(String upwd) {
		this.upwd = upwd;
	}
}


```

2\. 第二种：封装逻辑的JavaBean  
这种JavaBean用于实现业务逻辑。目的是为了提高代码的复用和解耦。 

#### 7.1.3 流程、参数分析

后端需要响应`总记录数` 和 `当前页的数据` 两部分数据给前端，所以在 `BrandMapper` 接口中需要定义两个方法：

-   selectByPage() ：查询当前页的数据的方法
    
-   selectTotalCount() ：查询总记录的方法
    

整体流程如下：

![](https://i-blog.csdnimg.cn/blog_migrate/f0e8f56debd0589bada0e3cf152f6279.png)​

**dao层参数：**开始索引begin、查询条数size

**service层参数：**当前页码currentPage ，每页展示条数pageSize。这些是从前端传进来的分页数据。

**pagebean参数：**总记录数totalCount，当前页数据rows。这些是要传给前端的商品数据。

### 7.2 后端实现

#### 7.2.1 dao方法实现

在 `BrandMapper` 接口中定义 `selectByPage()` 方法进行分页查询，代码如下：

```java
/**
     * 分页查询
     * @param begin
     * @param size
     * @return
     */
@Select("select * from tb_brand limit #{begin} , #{size}")
@ResultMap("brandResultMap")
List<Brand> selectByPage(@Param("begin") int begin,@Param("size") int size);
```

在 `BrandMapper` 接口中定义 `selectTotalCount()` 方法进行统计记录数，代码如下：

```java
/**
     * 查询总记录数
     * @return
     */
@Select("select count(*) from tb_brand ")
int selectTotalCount();
```

#### 7.2.2 service方法实现

在 `BrandService` 接口中定义 `selectByPage()` 分页查询数据的业务逻辑方法

```java
/**
     * 分页查询
     * @param currentPage  当前页码
     * @param pageSize   每页展示条数
     * @return
     */
    PageBean<Brand>  selectByPage(int currentPage,int pageSize);
```

在 `BrandServiceImpl` 类中重写 `selectByPage()` 方法，并进行业务逻辑实现

```java
@Override
public PageBean<Brand> selectByPage(int currentPage, int pageSize) {
    //2. 获取SqlSession对象
    SqlSession sqlSession = factory.openSession();
    //3. 获取BrandMapper
    BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);
    //4. 计算开始索引
    int begin = (currentPage - 1) * pageSize;
    // 计算查询条目数
    int size = pageSize;
    //5. 查询当前页数据
    List<Brand> rows = mapper.selectByPage(begin, size);
    //6. 查询总记录数
    int totalCount = mapper.selectTotalCount();
    //7. 封装PageBean对象
    PageBean<Brand> pageBean = new PageBean<>();
    pageBean.setRows(rows);
    pageBean.setTotalCount(totalCount);

    //8. 释放资源
    sqlSession.close();
    return pageBean;
}
```

#### 7.2.3 servlet实现

在 `BrandServlet` 类中定义 `selectByPage()` 方法。而该方法的逻辑如下：

-   获取页面提交的 `当前页码` 和 `每页显示条目数` 两个数据。这两个参数是在url后进行拼接的，格式是 `url?currentPage=1&pageSize=5`。获取这样的参数需要使用 `requet.getparameter()` 方法获取。
    
-   调用 service 的 `selectByPage()` 方法进行分页查询的业务逻辑处理
    
-   将查询到的数据转换为 json 格式的数据
    
-   响应 json 数据
    

servlet 中 `selectByPage()` 方法代码实现如下：

```java
public void selectByPage(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //1. 接收 当前页码 和 每页展示条数    url?currentPage=1&pageSize=5
    String _currentPage = request.getParameter("currentPage");
    String _pageSize = request.getParameter("pageSize");

    int currentPage = Integer.parseInt(_currentPage);
    int pageSize = Integer.parseInt(_pageSize);

    //2. 调用service查询
    PageBean<Brand> pageBean = brandService.selectByPage(currentPage, pageSize);

    //2. 转为JSON
    String jsonString = JSON.toJSONString(pageBean);
    //3. 写数据
    response.setContentType("text/json;charset=utf-8");
    response.getWriter().write(jsonString);
}
```

#### 7.2.4 测试

在浏览器上地址栏输入 `http://localhost:8080/brand-case/brand/selectByPage?currentPage=1&pageSize=5` ，查询到以下数据

![](https://i-blog.csdnimg.cn/blog_migrate/8b05ea100edbd1408c55f461a8b3181f.png)​

### 7.3 前端实现

#### 7.3.1 selectAll 代码改进

`selectAll()` 函数之前是查询所有数据，现需要改成分页查询。 请求路径应改为 `http://localhost:8080/brand-case/brand/selectByPage?currentPage=1&pageSize=5` ，而 `currentPage` 和 `pageSize` 是需要携带的参数，分别是 当前页码 和 每页显示的条目数。

刚才我们对后端代码进行测试可以看出响应回来的数据，所以在异步请求的成功回调函数（`then` 中的匿名函数）中给页面表格的数据模型赋值 `_this.tableData = resp.data.rows;`。整体代码如下

```javascript
var _this = this;
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPage？currentPage=1&pageSize=5"
}).then(resp =>{
    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
})
```

响应的数据中还有总记录数，要进行总记录数展示需要在页面绑定数据模型

![](https://i-blog.csdnimg.cn/blog_migrate/6901c7a3e3b31ff208219464d857a1e1.png)​

> **注意：该数据模型需要在Vue对象中声明出来。**

那异步请求的代码就可以优化为

```javascript
var _this = this;
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPage?currentPage=1&pageSize=5"
}).then(resp =>{
    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    _this.totalCount = resp.data.totalCount;
})
```

页组件给 `当前页码` 和 `每页显示的条目数` 都绑定了数据模型

![](https://i-blog.csdnimg.cn/blog_migrate/62ccf629b45fdf9e983c7902234068a8.png)​

所以 `selectAll()` 函数中发送异步请求的资源路径中不能将当前页码和 每页显示条目数写死，代码就可以优化为

```javascript
var _this = this;
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPage?currentPage="+this.currentPage+"&pageSize=" + this.pageSize
}).then(resp =>{
    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    _this.totalCount = resp.data.totalCount;
})
```

#### 7.3.2 改变每页条目数

![](https://i-blog.csdnimg.cn/blog_migrate/63194b20323fa8f9bd31b261451d14c6.png)​

当我们改变每页显示的条目数后，需要重新发送异步请求。而下图是分页组件代码，`@size-change` 就是每页显示的条目数发生变化时会触发的事件

![](https://i-blog.csdnimg.cn/blog_migrate/0d671f270bc1701541651c6e0b345233.png)​

而该事件绑定了一个 `handleSizeChange` 函数，整个逻辑如下：

```javascript
handleSizeChange(val) { //我们选择的是 ‘5条/页’ 此值就是 5.而我们选择了 `10条/页` 此值就是 10
    // 重新设置每页显示的条数
    this.pageSize  = val; 
    //调用 selectAll 函数重新分页查询数据
    this.selectAll();
}
```

#### 7.3.3 改变当前页码

当我们改变页码时，需要重新发送异步请求。而下图是分页组件代码，`@current-change` 就是页码发生变化时会触发的事件

![](https://i-blog.csdnimg.cn/blog_migrate/0db3e86f3e43f7bc59ffe6c41222cda4.png)​

而该事件绑定了一个 `handleSizeChange` 函数，整个逻辑如下：

```javascript
handleCurrentChange(val) { //val 就是改变后的页码
    // 重新设置当前页码
    this.currentPage  = val;
    //调用 selectAll 函数重新分页查询数据
    this.selectAll();
}
```

## 8，条件查询

![](https://i-blog.csdnimg.cn/blog_migrate/6dda71951359ea3e86018a6e7bca0af0.png)​

上图就是用来输入条件查询的条件数据的。要做条件查询功能，先明确以下三个问题

-   3个条件之间什么关系？
    
    同时满足，所用 SQL 中多个条件需要使用 and 关键字连接
    
-   3个条件必须全部填写吗？
    
    不需要。想根据哪儿个条件查询就写那个，所以这里需要使用动态 sql 语句
    
-   条件查询需要分页吗？
    
    需要
    

根据上面三个问题的明确，我们就可以确定sql语句了：

![](https://i-blog.csdnimg.cn/blog_migrate/21b68acd5b8a318d1290eb96aa402614.png)​

整个条件分页查询流程如下

![](https://i-blog.csdnimg.cn/blog_migrate/8a5e26a3a4ac663a0709b81d49de3450.png)​

### 8.1 后端实现

#### 8.1.1 dao实现

在 `BrandMapper` 接口中定义 `selectByPageAndCondition()` 方法 和 `selectTotalCountByCondition` 方法，用来进行条件分页查询功能，方法如下：

```java
/**
     * 分页条件查询
     * @param begin
     * @param size
     * @return
     */
List<Brand> selectByPageAndCondition(@Param("begin") int begin,@Param("size") int size,@Param("brand") Brand brand);

/**
     * 根据条件查询总记录数
     * @return
     */
int selectTotalCountByCondition(Brand brand);
```

参数：

-   `begin` 分页查询的起始索引
    
-   `size` 分页查询的每页条目数
    
-   `brand` 用来封装条件的对象
    

由于这是一个复杂的查询语句，需要使用动态sql；所以我们在映射配置文件中书写 sql 语句。`brand_name` 字段和 `company_name` 字段需要进行模糊查询，所以需要使用 `%` 占位符。映射配置文件中 statement 书写如下：

```XML
<!--查询满足条件的数据并进行分页-->
<select id="selectByPageAndCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    <where>
        <if test="brand.brandName != null and brand.brandName != '' ">
            and  brand_name like #{brand.brandName}
        </if>

        <if test="brand.companyName != null and brand.companyName != '' ">
            and  company_name like #{brand.companyName}
        </if>

        <if test="brand.status != null">
            and  status = #{brand.status}
        </if>
    </where>
    limit #{begin} , #{size}
</select>

<!--查询满足条件的数据条目数-->
<select id="selectTotalCountByCondition" resultType="java.lang.Integer">
    select count(*)
    from tb_brand
    <where>
        <if test="brandName != null and brandName != '' ">
            and  brand_name like #{brandName}
        </if>

        <if test="companyName != null and companyName != '' ">
            and  company_name like #{companyName}
        </if>

        <if test="status != null">
            and  status = #{status}
        </if>
    </where>
</select>
```

#### 8.1.2 service实现

在 `BrandService` 接口中定义 `selectByPageAndCondition()` 分页查询数据的业务逻辑方法

```java
 /**
     * 分页条件查询
     * @param currentPage
     * @param pageSize
     * @param brand
     * @return
     */
PageBean<Brand>  selectByPageAndCondition(int currentPage,int pageSize,Brand brand);
```

在 `BrandServiceImpl` 类中重写 `selectByPageAndCondition()` 方法，并进行业务逻辑实现

```java
 @Override
    public PageBean<Brand> selectByPageAndCondition(int currentPage, int pageSize, Brand brand) {
        //2. 获取SqlSession对象
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);


        //4. 计算开始索引
        int begin = (currentPage - 1) * pageSize;
        // 计算查询条目数
        int size = pageSize;

        // 处理brand条件，模糊表达式
        String brandName = brand.getBrandName();
        if (brandName != null && brandName.length() > 0) {
            brand.setBrandName("%" + brandName + "%");
        }

        String companyName = brand.getCompanyName();
        if (companyName != null && companyName.length() > 0) {
            brand.setCompanyName("%" + companyName + "%");
        }

        //5. 查询当前页数据
        List<Brand> rows = mapper.selectByPageAndCondition(begin, size, brand);

        //6. 查询总记录数
        int totalCount = mapper.selectTotalCountByCondition(brand);

        //7. 封装PageBean对象
        PageBean<Brand> pageBean = new PageBean<>();
        pageBean.setRows(rows);
        pageBean.setTotalCount(totalCount);

        //8. 释放资源
        sqlSession.close();

        return pageBean;
    
```

> **注意：brandName 和 companyName 属性值到时候需要进行模糊查询，所以前后需要拼接上 `%`**。

#### 8.1.3 servlet实现

在 `BrandServlet` 类中定义 `selectByPageAndCondition()` 方法。而该方法的逻辑如下：

-   获取页面提交的 `当前页码` 和 `每页显示条目数` 两个数据。这两个参数是在url后进行拼接的，格式是 `url?currentPage=1&pageSize=5`。获取这样的参数需要使用 `requet.getparameter()` 方法获取。
    
-   获取页面提交的 `条件数据` ，并将数据封装到一个Brand对象中。由于这部分数据到时候是需要以 json 格式进行提交的，所以我们需要通过流获取数据，具体代码如下：
    
    ```java
    // 获取查询条件对象
    BufferedReader br = request.getReader();
    String params = br.readLine();//json字符串
    
    //转为 Brand
    Brand brand = JSON.parseObject(params, Brand.class);
    ```
    
-   调用 service 的 `selectByPageAndCondition()` 方法进行分页查询的业务逻辑处理
    
-   将查询到的数据转换为 json 格式的数据
    
-   响应 json 数据
    

servlet 中 `selectByPageAndCondition()` 方法代码实现如下：

```java
/**
     * 分页条件查询
     * @param request
     * @param response
     * @throws ServletException
     * @throws IOException
     */

public void selectByPageAndCondition(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //1. 接收 当前页码 和 每页展示条数    url?currentPage=1&pageSize=5
    String _currentPage = request.getParameter("currentPage");
    String _pageSize = request.getParameter("pageSize");

    int currentPage = Integer.parseInt(_currentPage);
    int pageSize = Integer.parseInt(_pageSize);

    // 获取查询条件对象
    BufferedReader br = request.getReader();
    String params = br.readLine();//json字符串

    //转为 Brand
    Brand brand = JSON.parseObject(params, Brand.class);


    //2. 调用service查询
    PageBean<Brand> pageBean = brandService.selectByPageAndCondition(currentPage,pageSize,brand);

    //2. 转为JSON
    String jsonString = JSON.toJSONString(pageBean);
    //3. 写数据
    response.setContentType("text/json;charset=utf-8");
    response.getWriter().write(jsonString);
}
```

### 8.2 前端实现

前端代码我们从以下几方面实现：

1.  **查询表单绑定查询条件对象模型**
    
    这一步在页面上已经实现了，页面代码如下：![](https://i-blog.csdnimg.cn/blog_migrate/c2b2fee18fa43eb0c75422ab6b5c06b7.png)​
    
2.  **点击查询按钮查询数据**![](https://i-blog.csdnimg.cn/blog_migrate/120797d082248612e778eea3a5dfb76b.png)​
    
    从上面页面可以看到给 `查询` 按钮绑定了 `onSubmit()` 函数，而在 `onSubmit()` 函数中只需要调用 `selectAll()` 函数进行条件分页查询。
    
3.  **改进 selectAll() 函数**
    
    子页面加载完成后发送异步请求，需要携带当前页码、每页显示条数、查询条件对象。接下来先对携带的数据进行说明：
    
    -   `当前页码` 和 `每页显示条数` 这两个参数我们会拼接到 URL 的后面
        
    -   `查询条件对象` 这个参数需要以 json 格式提交给后端程序
        
    
    修改 `selectAll()` 函数逻辑为
    
    ```javascript
    var _this = this;
    
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/brand/selectByPageAndCondition?currentPage="+this.currentPage+"&pageSize="+this.pageSize,
        data:this.brand
    }).then(function (resp) {
    
        //设置表格数据
        _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
        //设置总记录数
        _this.totalCount = resp.data.totalCount;
    })
    ```
    

## 9，箭头函数，前端代码优化

咱们已经将所有的功能实现完毕。而针对前端代码中的发送异步请求的代码，如下

```javascript
var _this = this;

axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPageAndCondition?currentPage="+this.currentPage+"&pageSize="+this.pageSize,
    data:this.brand
}).then(function (resp) {

    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    _this.totalCount = resp.data.totalCount;
})
```

**then里匿名函数的this特点：** 

需要在成功的回调函数（也就是`then` 函数中的匿名函数）中使用this，都需要在外边使用 `_this` 记录一下 `this` 所指向的对象；因为在外边的 `this` 表示的是 Vue 对象，而回调函数中的 `this` 表示的是window对象。

**箭头函数示例：**

这里我们可以使用 `ECMAScript6` 中的新语法**（箭头函数）**来替代传统函数function() {}。

```javascript
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPageAndCondition?currentPage="+this.currentPage+"&pageSize="+this.pageSize,
    data:this.brand
}).then((resp) => {

    //设置表格数据
    this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    this.totalCount = resp.data.totalCount;
})
```

**箭头函数的作用：**

替换（简化）匿名函数。then(箭头函数)里面的this是vue不是window。

**箭头函数语法：**

思想和省略方法都类似于Lambda表达式，只是箭头是**\=>**不是->。

```javascript
(参数) => {
	逻辑代码
}
```

**示例：**

作为常规功能：

```javascript
function sum(a, b) {
   return a + b
}
```

 替换成箭头函数：

```javascript
const sum = (a, b) => a + b
```