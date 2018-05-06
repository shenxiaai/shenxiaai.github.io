---
title: 前端解决跨域问题
category: 前端
date: 2016-11-12
toc: true
---

## 1.CORS

**CORS**（Corss-Origin Resource Sharing,跨资源共享），基本思想是使用自定义的HTTP头部让浏览器与服务器进行沟通，从而决定请求或响应的成功或失败。即给请求附加一个额外的Origin头部，其中包含请求页面的源信息（协议、域名和端口），以便服务器根据这个头部决定是否给予响应。

<!-- more -->

```
app.all('*', function (req, res, next) {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Headers', 'Content-Type,Content-Length, Authorization, Accept,X-Requested-With');
  res.header('Access-Control-Allow-Methods','PUT,POST,GET,DELETE,OPTIONS');
  res.header("Content-Type", "application/json;charset=utf-8");
  if (req.method == 'OPTIONS') {
    res.send(200);
  } else {
    next();
  }
});
```

## 2.document.domain

将页面的document.domain设置为相同的值，页面间可以互相访问对方的JavaScript对象。
注意：
不能将值设置为URL中不包含的域；
松散的域名不能再设置为紧绷的域名。

## 3.图像Ping

```
var img=new Image();
img.onload=img.onerror=function(){
... ...
}
img.src="url?name=value";
```

请求数据通过查询字符串的形式发送，响应可以是任意内容，通常是像素图或204响应。
图像Ping最常用于跟踪用户点击页面或动态广告曝光次数。
缺点：
只能发送GET请求；
无法访问服务器的响应文本，只能用于浏览器与服务器间的单向通信。

## 4.Jsonp

```
var script=document.createElement("script");
script.src="url?callback=handleResponse";
document.body.insertBefore(script,document.body.firstChild);
```

JSONP由两部分组成：回调函数和数据
回调函数是接收到响应时应该在页面中调用的函数，其名字一般在请求中指定。
数据是传入回调函数中的JSON数据。
优点：
能够直接访问响应文本，可用于浏览器与服务器间的双向通信。
缺点：
JSONP从其他域中加载代码执行，其他域可能不安全；
难以确定JSONP请求是否失败。

## 5.Comet

Comet可实现服务器向浏览器推送数据。
Comet是实现方式：长轮询和流
短轮询即浏览器定时向服务器发送请求，看有没有数据更新。
长轮询即浏览器向服务器发送一个请求，然后服务器一直保持连接打开，直到有数据可发送。发送完数据后，浏览器关闭连接，随即又向服务器发起一个新请求。其优点是所有浏览器都支持，使用XHR对象和setTimeout()即可实现。
流即浏览器向服务器发送一个请求，而服务器保持连接打开，然后周期性地向浏览器发送数据，页面的整个生命周期内只使用一个HTTP连接。

## 6.WebSocket

WebSocket可在一个单独的持久连接上提供全双工、双向通信。
WebSocket使用自定义协议，未加密的连接时ws://；加密的链接是wss://。
var webSocket=new WebSocket(“ws://“);
webSocket.send(message);
webSocket.onmessage=function(event){
var data=event.data;
… ….
}

> 注意：

必须给WebSocket构造函数传入绝对URL；
WebSocket可以打开任何站点的连接，是否会与某个域中的页面通信，完全取决于服务器；
WebSocket只能发送纯文本数据，对于复杂的数据结构，在发送之前必须进行序列化JSON.stringify(message))。
优点：
在客户端和服务器之间发送非常少的数据，减少字节开销。