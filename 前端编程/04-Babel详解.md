# Babel详解

## 简介

ES6的某些高级语法在浏览器环境甚至是Node.js环境中无法执行。

Babel是一个广泛使用的转码器，可以将ES6代码转为ES5代码，从而在现有环境执行执行。

这意味着，你可以现在就用 ES6 编写程序，而不用担心现有环境是否支持。

## 安装

安装命令行转码工具

> Babel提供babel-cli工具，用于命令行转码。它的安装命令如下：

```
npm install -g babel-cli
#查看是否安装成功
babel --version
```

## 使用

* 创建babel文件夹

* 初始化项目

```
npm install -y
```

* 创建ES6代码文件`test.js`，进行测试

```js
// 转码前
// 定义数据
let input = [1, 2, 3]
// 将数组的每个元素 +1
input = input.map(item => item + 1)
console.log(input)
```

* 配置`.babelrc`

Babel的配置文件是.babelrc，存放在项目的根目录下，该文件用来设置转码规则和插件，基本格式如下。

```
{
    "presets": [],
    "plugins": []
}
```

* presets字段设定转码规则，将es2015规则加入` .babelrc`：

```
{
    "presets": ["es2015"],
    "plugins": []
}
```

* 安装转码器，在项目中安装

```
npm install --save-dev babel-preset-es2015
```

* 转码

```
# npm install --save-dev csv-loader xml-loader

# 转码结果写入一个文件
mkdir dist1

# --out-file 或 -o 参数指定输出文件
babel test.js --out-file dist1/test.js 
# 或者
babel test.js -o dist1/compiled.js

# 整个目录转码
mkdir dist2
# --out-dir 或 -d 参数指定输出目录
babel src --out-dir dist2
# 或者
babel src -d dist2
```

## 自定义脚本

1、改写`package.json`

```
{
    // ...
    "scripts": {
        // ...
        "build":  "babel src\\example.js -o dist\\compiled.js"
    },
}
```

2、转码的时候，执行下面的命令

```
mkdir dist
npm run build
```

