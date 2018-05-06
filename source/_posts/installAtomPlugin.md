---
title: 安装atom插件
category: 前端
date: 2017-01-19
---

atom是Github开发的一款前端编辑软件，好用程度几乎直逼sublime，重点就是atom和sublime一样支持很多很多的插件。所以为了让atom更适合个人的编辑习惯，我们要自己安装一些喜欢的插件，跟元宝君一起来安装吧。
我们打开atom，在settings中会找到”Install”选项，我们可以在搜索框中查找所需的插件并安装。

<!-- more -->

![](/assets/images/img10.png)

但是相信很多朋友跟元宝君一样，发现这样的安装方式经常无法安装上插件，所以呢就需要我们自己从Github上找到插件的git仓库地址，自己动手安装啦。

在git bash中进入：**C:\Users\用户名.atom\packages**

打开Github上插件的主页，复制插件的git仓库地址

回到git bash中clone:

`	
git clone https://github.com/xxx/.../xxx.git
`
进入下载下来的文件夹中：

`	
cd tool-bar/
`

安装：

`	
npm install
`

**完成！**