---
title: HTML5 Web存储——localStorage
category: 前端
date: 2016-04-12
---
   
自从开始做H5开发以后，接触了很多h5的新特性，今天元宝君就来说一下H5的新存储属性。

localStorage是H5新增的特性，主要功能是本地存储，解决了cookie存储空间不足的问题(cookie中每条cookie的存储空间为4k)，localStorage中一般浏览器支持近5M大小，不同的浏览器中localStorage会有所不同。

# 一、localStorage的优缺点

## localStorage的优点

1.  localStorage拓展了cookie的4K限制
2.  localStorage会可以将第一次请求的数据直接存储到本地，这个相当于一个5M大小的针对于前端页面的数据库，相比于cookie可以节约带宽（_仅在高版本的浏览器中支持_）

## localStorage的缺点

1.  各个浏览器localstorage的大小不同
2.  仅IE8以上支持
3.  localstorage限定为string类型，需要**JSON.stringify()**和**JSON.parse()**方法转换
4.  localStorage在浏览器的**隐私模式**下不可读取
5.  localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，导致页面卡顿
6.  localStorage不能被爬虫抓取到

# 二、sessionStorage

sessionStorage 方法针对一个 session 进行数据存储。**当用户关闭浏览器窗口后，数据会被删除。**

# 三、使用localStorage

## 判断浏览器是否支持localStorage

```
if(!window.localStorage){
    alert('浏览器不支持localstorage!');
}else{
    alert("浏览器支持localstorage");
}
```

### IE7

![](/assets/images/img11.jpg)

### Chrome

![](/assets/images/img12.jpg)

## 写入localStorage

写入localStroage有三种方法，推荐使用**setItem**:

```
var storage=window.localStorage;
storage["a"]=1;
   storage.a=1;
   storage.setItem("a",1);	//三种写法任意使用一个
console.log(typeof(storage.a));
```

运行结果：

![](/assets/images/img13.jpg)

## 读取localStorage

读取localStroage同样有三种方法，推荐使用**getItem**:

```
var storage=window.localStorage;
var result = storage["a"];
   var result = storage.a;
   var result = storage.getItem("a");	//三种写法任意使用一个
console.log(result);
```

## 删除全部localStorage

```
var storage=window.localStorage;
storage.setItem("a",3);
storage.clear();
```

## 删除localStorage中的一条

```
var storage=window.localStorage;
storage.setItem("a",3);
storage.removeItem("a");
```

> 特别提醒：
将JSON存入localStorage中时会被自动转换成为字符串形式，此时可以使用**JSON.stringify()**方法将JSON转换成为JSON字符串；在读取JSON型localStorage时，使用**JSON.parse()**方法读将JSON字符串转换成为JSON对象。