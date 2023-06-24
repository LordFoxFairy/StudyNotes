## 自动生成Summary文件

gitbook安装参考官方文档：

https://toolchain.gitbook.com/setup.html

#### 方案1，[julianxhokaxhiu](https://github.com/julianxhokaxhiu)/**gitbook-plugin-summary**

Google基本上用的是 gitbook-plugin-summary

https://github.com/julianxhokaxhiu/gitbook-plugin-summary#readme

安装

```
npm i gitbook-plugin-summary --save
```

配置book.json

```
{
  "plugins": [
    "summary"
  ]
}
```

#### 方案2，[imfly](https://github.com/imfly)/**gitbook-summary**

github地址：https://github.com/imfly/gitbook-summary

安装

```
npm install -g gitbook-summary
```

简单使用：

```
cd d:\Users\TIA\Documents\笔记\GitBook\Library\notebook

book sm
```

demo：

```
tree .
.
├── ORDER
│   ├── 0-README.md
│   └── 1-orderInfo.md
├── README.md
├── SUMMARY.md
└── USER
    ├── 0-README.md
    └── 1-userInfo.md
```

result:

```
cat SUMMARY.md
# Your Book Title
 
- ORDER
  * [0 README](ORDER/0-README.md)
  * [1 Order Info](ORDER/1-orderInfo.md)
- USER
  * [0 README](USER/0-README.md)
```

总结，能使用方案1，感觉会更优雅一些，插件化形式，但对于基本使用而已，能用即可，后面需要改良或者扩展再看了
