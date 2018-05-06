---
title: Hexo搭建Github博客
category: 前端
date: 2016-11-12
---

作为一名前端居然没有一个自己的个人网站简直low啊，元宝工作这么久一直想有一个自己的个人网站，之前有试过Github提供的[Github Page](https://pages.github.com/)创建个站，不过全部框架需要自己写，本君（最近深中“三生三世”的毒）平时工作也没有时间设计页面，所以那个网站就不了了之了。这里有一个[学习 Github Page 教你分分钟搭建自己的博客](https://github.com/dwqs/blog)的教程可以参考。

后来偶然间看到hexo搭配Github可以搭建一个有设计有框架的使用blog，元宝想都没想直接开始啦！特此用这篇文章记录一下完成的过程。

<!-- more -->

## 安装Node

到[Node.js官网](http://nodejs.cn/)下载相应平台的最新版本，一路安装即可。

## 安装Git bash

用于把本地的hexo内容提交到github上去.

## 安装Hexo

Node和Git bash都安装好后,本地创建一个文件夹,如myBlog,用于存放hexo的配置文件,然后进入myBlog里安装Hexo:

`	
npm install -g hexo
`

## 初始化hexo

`	
hexo init
`

## 利用hexo指令安装一个完整的hexo项目

`
hexo generate（简写：hexo g)
`

## 在本地运行hexo项目

`	
hexo server(简写：hexo s)
`

> 注意：运行hexo s后出现页面打不开的情况时，先检查端口号是否被占用。hexo项目默认端口号为**4000**。如果电脑上安装了**“福昕阅读器”**，4000端口就被该软件占用了。

### 解决方法:

`	
hexo s -p 5000 (换个新的未使用的端口号)
`

* * *

现在我们本地的hexo博客项目已经创建好了，看一下我们的项目结构：

![](/assets/images/img9.png)

在浏览器上打开：[localhost:5000](localhost:5000)

** mac上似乎端口号是4000

![](/assets/images/img2.png)

此时项目的框架主题用的是最初默认的：**landscape**

本宝觉得这个主题实在太单调了，百度了一个比较喜欢的主题： **yilia**

## 更换主题yilia

### 打开[yilia](https://github.com/litten/hexo-theme-yilia)的Github主页

### 安装yilia主题

在git bash命令行中进入hexo创建的项目中，如本宝的：myBlog路径

执行安装命令：

`
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
`

### 配置主题

![](/assets/images/img3.png)

修改hexo根目录下的 _config.yml ： theme: yilia

![](/assets/images/img4.png)

### 更新

```
cd themes/yilia
git pull
```

![](/assets/images/img1.png)

完成后效果如下：

![](/assets/images/img5.png)

很多自定义框架的部分，都可以在项目根目录下的——config.yml文件中修改。

* * *

好啦，本地的博客项目已经搭建好啦，怎样把它部署到Github上用Github域名访问我们的博客呢？

### 创建Github账号

这个不用我说了吧，直接去Github官网注册就好啦，以前有的就直接用咯。

### 创建git仓库

![](/assets/images/img6.png)

> 注意：仓库名必须为: **yourGithubUsername.github.io**

这样可以保证自己的博客可以用： **[https://yourGithubUsername.github.io/](https://yourGithubUsername.github.io/)** 直接访问

### 关联自己的Github账号

打开根目录下的_config.yml文件，翻到最下面：

![](/assets/images/img8.png)

修改deploy配置：

```
deploy:
  type: git
  repo: https://github.com/yourGithubUsername/yourGithubUsername.github.io.git
  branch: master
```

### 上传hexo博客项目

首先安装上传指令，在根目录下执行：

`
npm install hexo-deployer-git --save（hexo 3.0版本后执行此句无BUG）
`

安装成功后，执行上传命令：

`
hexo deploy(简写： hexo d)
`
### 浏览线上效果

然后再浏览器中输入[http://yourGithubUsername.github.io/](http://yourGithubUsername.github.io/)就行啦！

* * *

**补充：**

每次在本地发表文章的步骤是：

发布markdown文章
hexo框架支持markdown文档和语法，所有博客添加在source/_post目录下：

![](/assets/images/img7.png)

博客写好后，执行部署指令：

```
hexo clean
hexo generate
hexo deploy
```

#### hexo d报错集锦：

##### 情况一

![](/assets/images/img13.png)

解决方法：

`
git config --global core.autocrlf false
`