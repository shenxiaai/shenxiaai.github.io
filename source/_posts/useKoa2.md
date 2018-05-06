---
title: 使用Koa2
category: 前端
date: 2017-03-01
---

# 自定义方式

## 安装koa

```
node install -g koa(或node install koa --save)
```

<!-- more -->

## 新建一个app.js文件：

```
var koa = require('koa');
var app = new koa();
app.use(function *(){
  this.body = 'Hello World';
});
app.listen(3000);
console.log('Koa app started at port 3000...');
```

> 其实Koa框架已经用ES6啦，这里为了好理解还是用的ES5，后面会慢慢开始用ES6。

## 在控制台运行app.js:

`	
node app.js
`

## 运行结果：

**控制台：**

![](/assets/images/img4.jpg)

**页面上：**

![](/assets/images/img5.jpg)

# 使用koa应用生成器

使用Express时有express-generator，用koa时也有koa-generator。

## 安装koa-generator

`
npm install -g koa-generator（或npm install koa-generator --save）
`

然后使用koa命令创建koa 1.x项目

然后使用koa2命令创建koa 2.x项目

## 新建myKoa文件夹

```
mkdir myKoa
koa2 myKoa
cd myKoa
npm install
npm start
```

**运行结果：**

![](/assets/images/img6.jpg)

![](/assets/images/img8.jpg)

![](/assets/images/img9.jpg)

![](/assets/images/img10.jpg)