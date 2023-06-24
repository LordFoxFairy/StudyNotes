# NPM详解

## 简介

官方网站：https://www.npmjs.com/
NPM全称`Node Package Manager`，是Node.js包管理工具，是全球最大的模块生态系统，里面所有的模块都是开源免费的；也是Node.js的包管理工具，相当于前端的Maven 。

```
# 查看当前版本
npm -v
```

![image-20210919203513048](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071256443.png)

其优势：

* 快速构建nodejs工程
* 快速安装和依赖第三方模块，比如`npm install mysql redis`等待。

## 使用npm管理项目

1. 创建文件夹npm
2. 项目初始化

```
#建立一个空文件夹，在命令提示符进入该文件夹  执行命令初始化
npm init
#按照提示输入相关信息，如果是用默认值则直接回车即可。
#name: 项目名称
#version: 项目版本号
#description: 项目描述
#keywords: {Array}关键词，便于用户搜索到我们的项目
#最后会生成package.json文件，这个是包的配置文件，相当于maven的pom.xml
#我们之后也可以根据需要进行修改。
```

![image-20210919204101325](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201071256444.png)

通过`npm init`得到`package.json`这个文件里的内容如下：

```
{
  "name": "npmpro", // 工程名
  "version": "1.0.0", // 版本号
  "description": "我是一个nodejs工程", // 描述
  "main": "index.js", // 入口js文件
  "scripts": { // 运行脚本
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "learn", // 开发者名称
  "license": "ISC" // 授权协议
}
```

如果想直接生成` package.json` 文件，那么可以使用命令

```
npm init -y
```

## 安装cnpm

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## 安装模块

* 安装命令

```
npm install 模块名
```

或者

```
npm i 模块名
```

> `npm install xxx`会记录在`package.json`中，便于集成第三方模块，避免重复下载模块

npm管理的项目在备份和传输的时候一般不携带`node_modules`文件夹

```
npm install  #根据package.json中的配置下载依赖，初始化项目
```

* 安装模块放在什么地方

安装的模块放在`node_modules`文件夹中

* 安装指定版本

```
#如果安装时想指定特定的版本
npm install jquery@2.1.x
```

* 添加依赖

```
#devDependencies节点：开发时的依赖包，项目打包到生产环境的时候不包含的依赖
#使用 -D参数将依赖添加到devDependencies节点
npm install --save-dev eslint
#或
npm install -D eslint
```

* 全局安装

`Node.js`全局安装的npm包和工具的位置：`用户目录\AppData\Roaming\npm\node_modules`

```
npm install -g webpack
```

## 导入模块

```js
const mysql = require("mysql")
```

或者

```
const redis = require('redis')

const client = redis.createClient(6379, '127.0.0.1');
client.on("error", function(error){
    console.error(error)
});
client.set("key","value",redis.print);
client.get("key",redis.print);
```

## 更换镜像

1、修改npm镜像

> NPM官方的管理的包都是从 [http://npmjs.com下载的，但是这个网站在国内速度很慢。](http://npmjs.xn--com%2C-794fngl0fq9g8opjmak71erncc6ioqt1y1ddrow2r8u2ecpbg0b./)
>
> 这里推荐使用淘宝 NPM 镜像 http://npm.taobao.org/
>
> 淘宝 NPM 镜像是一个完整 npmjs.com 镜像，同步频率目前为 10分钟一次，以保证尽量与官方服务同步。

2、设置镜像地址

```
#经过下面的配置，以后所有的 npm install 都会经过淘宝的镜像地址下载
npm config set registry https://registry.npm.taobao.org 
#查看npm配置信息
npm config list
```

## 其他命令

```
#更新包（更新到最新版本）
npm update 包名
#全局更新
npm update -g 包名
#卸载包
npm uninstall 包名
#全局卸载
npm uninstall -g 包名
```