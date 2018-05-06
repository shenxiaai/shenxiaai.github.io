---
title: 解决vue在build之后css中image路径错误问题
category: 前端
date: 2017-06-01
---

在vue的conponents中，我们经常需要写style scoped，但是不知道你们有木有遇到过需要写background-image的时候，一般大家都把image资源放在哪儿呢？

在npm run dev，开发状态，无论image放在/src中，还是/src/assets中、或者在/static中，在components中都是可以引用到的~ 一如vue-cli的API文档中写的：

<!-- more -->

*   相对路径 ./assets/logo.png 被视为模块依赖
*   无前缀 assets/logo.png 被视为相对路径
*   使用 ~ 被视为 require('some-module/image.png')

![](/assets/images/img28.jpg)

[具体可参考vue-cli API](https://ajimide.gitbooks.io/key-vue-cli-webpack/5.%20Handing%20Static%20Assets.html)

但是，当我们npm run build把项目打包，准备放到服务器上跟后台联调的时候，有木有发现，你直接打开/dist目录下的index.html页面是空白的，或者background-image都没有显示？

这里，还是上面vue-cli的url-loader打包工具出了问题。

元宝君现在也没有找到最佳的解决方案，暂时可以用下面这种方法解决：

1.  首先，把css/images/js资源放到assets中：

![](/assets/images/img29.jpg)

1.  第二步，安装anywhere
> Anywhere 是一个基于node.js的静态文件服务器工具，主要使用了express提供的两个中间件：serve-index和serve-static。具有使用简单快速、安装方便的优点，大多数场景下使用apache的静态文件服务器非常的臃肿，诸多特性用不到，配置复杂。而一些基于node.js的静态文件服务器大都配置简单甚至无需配置，方便在一些小的场景下使用。

`
npm install anywhere -g
`

1.  进入项目中的dist目录下，运行：

`
anywhere -s
`
> anywhere //不带任何参数，使用默认的8000端口，当前路径作为静态文件服务器根路径
> anywhere 8888 //使用8888端口
> anywhere -p 8989 //使用8989端口
> anywhere -s //启动后是否打开浏览器
> anywhere -h localhost //指定主机名（ip地址）
> anywhere -d /home //指定静态文件服务器根路径为/home

此时，在浏览器上打开localhost:8000页面就可以看到完整的打包好的项目啦！

1.  补充一个方法：

![](/assets/images/img30.jpg)