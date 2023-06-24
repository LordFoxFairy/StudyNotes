# NodeJS

## 概述

​	[前端开发](https://baike.baidu.com/item/前端开发)是创建Web页面或app等前端界面呈现给用户的过程，通过[HTML](https://baike.baidu.com/item/HTML/97049)，[CSS](https://baike.baidu.com/item/CSS/5457)及[JavaScript](https://baike.baidu.com/item/JavaScript/321142)以及衍生出来的各种技术、框架、解决方案，来实现互联网产品的用户界面交互 [1] 。它从[网页制作](https://baike.baidu.com/item/网页制作/14680719)演变而来，名称上有很明显的时代特征。在[互联网](https://baike.baidu.com/item/互联网/199186)的演化进程中，网页制作是[Web1.0](https://baike.baidu.com/item/Web1.0)时代的产物，**==早期网站主要内容都是静态，以图片和文字为主==**，用户使用网站的行为也以浏览为主。随着[互联网技术](https://baike.baidu.com/item/互联网技术/617749)的发展和[HTML5](https://baike.baidu.com/item/HTML5)、[CSS3](https://baike.baidu.com/item/CSS3)的应用，现代网页更加美观，交互效果显著，功能更加强大。

​	Node 是一个让 JavaScript 运行在服务端的开发平台，它让 JavaScript 成为与`PHP、Python、Perl、Ruby `等服务端语言平起平坐的脚本语言。  发布于2009年5月，由Ryan Dahl开发，实质是对`Chrome V8`引擎进行了封装。

​	简单的说 `Node.js `就是运行在服务端的 JavaScript。 `Node.js` 是一个基于Chrome JavaScript 运行时建立的一个平台。底层架构是：`javascript.` 文件后缀：`.js`

​	`Node.js`是一个事件驱动I/O服务端JavaScript环境，基于Google的`V8`引擎，`V8`引擎执行`Javascript`的速度非常快，性能非常好。

![img](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255984.png)

## VScode

* 安装

下载地址：https://code.visualstudio.com/

![image-20210917181410834](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255986.png)

* 配置中文插件

![image-20210917182023416](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255987.png)

* 安装插件
  * `ESLint`
  * `ESLint`
  * `Vetur`
  * `VueHelper`
  * `Node.js Modules Intellisense`

* 设置字体大小

左边栏Manage `-> `settings `->` 搜索 `font` `->` Font size

* 开启完整的Emmet语法支持

设置中搜索 Emmet：启用如下选项，必要时重启vs

![image-20210917182451480](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255988.png)

* 视图

查看`—> `外观`—> `向左移动侧边栏

## NodeJS安装

下载对应你系统的Node.js版本:
下载地址：https://nodejs.org/zh-cn/download
帮助文档：https://nodejs.org/zh-cn/docs
关于Nodejs：https://nodejs.org/zh-cn/about

```
node -v
```

![image-20210917182818125](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255989.png)

## 入门

### 教程

学习地址：http://nodejs.cn/learn

### 目标

控制台输出字符串、使用函数、进行模块化编程

### hello world

1、创建文件夹 `NodeJS`

![image-20210917195620127](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255990.png)

2、创建 `helloworld.js`

```js
// 类似于 Java中的 System.out.println("hello world")
console.log("hello world")
```

3. 运行

![image-20210917195717925](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255991.png)

或者在命令控制平台中输入`node helloworld.js`

> ==`Node.js`是脱离浏览器环境运行的JavaScript程序，基于`V8 `引擎==

### 实现请求响应

创建 `httpserver.js`

```js
// 导入模块 require 类似于 import java.sql
const http = require("http")

// 1. 创建一个httpserver服务
http.createServer(function(request, response){
    // 浏览器怎么认识 hello server
    /* 
        这句话的含义是：告诉浏览器将以text-html的方式去解析hello server这段数据
    */
    response.writeHead(200,{"Content-type":'text/html'}); 

    // 给浏览器输出内容
    response.end("<h1>hello server</strong>");

}).listen(8888) // 监听端口
// 2. 监听一个端口，例如 8888
console.log("启动的服务是：http://localhost:8888 以启动成功")

// 3. 启动运行服务 node httpserver.js
// 4. 在浏览器访问 http://localhost:8888
```

运行服务器程序

```
node httpserver.js
```

服务器启动成功后，在浏览器中输入：http://localhost:8888/ 查看`webserver`成功运行，并输出`html`页面

![image-20210917201913834](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255992.png)

停止服务：`ctrl + c`

### 操作MySQL数据库

参考：https://www.npmjs.com/package/mysql

* 安装`mysql`依赖

```
npm install mysql
```

* 创建测试数据库`testdb`

```sql
create database testdb charset=utf8;
use testdb;
create table user(
	id int(10) not null,
	name varchar(20) not null,
	PRIMARY KEY(id)
)ENGINE=INNODB DEFAULT charset=utf8;


insert into user(id,name) values(1,"小明");
insert into user(id,name) values(2,"小红");
```

* 创建`db.js`

* 定义`db.js`进行操作

```js
// 1. 导入mysql依赖包， mysql属于第三方的模块类似于 java.sql

/**
 *  注意const不可变，var可变，都属于全局变量
 */
var mysql = require("mysql")
const { createConnection } = require("net")

// 2. 创建一个mysql的Connection对象
// 3. 配置数据库相关信息

var connection = mysql.createConnection({
    host:"localhost",
    port:"3306",
    user:"root",
    password:"123456",
    database:"testdb"
})

// 4. 连接数据库
connection.connect()

// 5. 执行数据库的增删改查（curd）
connection.query("select * from user",function(error,results,fields){
    // 如果查询出错，直接抛出
    if(error) throw error;
    // 查询成功
    console.log("results = ",results)
})

// 6. 关闭数据库链接
connection.end()
```

运行后，出现`没有调试适配器，无法发送“variables”`问题，解决如下：

1. 需要看到他具体的值，在打印的地方加上断点即可。
2. 如果是`node.js `可以 创建一个`httpserver`并 监听一个端口

运行

```
node db.js
```

![image-20210917205210329](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071255993.png)

> **如果想开发更复杂的基于Node.js的应用程序后台，需要进一步学习Node.js的Web开发相关框架 express，art-template、koa等**

