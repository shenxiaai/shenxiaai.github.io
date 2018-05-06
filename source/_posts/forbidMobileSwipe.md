---
title: 禁止手机浏览器、微信浏览器的上下滑动问题
category: 前端
date: 2016-12-25
---

前端在编写移动端页面时，尤其微信端页面中，经常会发现微信自带的浏览器有一个很神奇的地方，就是网页可以在浏览器上上下左右的拖拽：

![](/assets/images/gif1.gif)

就像上图，如果在遇到需要在页面上绘制或者做拖拽功能时，很容易跟这个自带功能相冲突的情况。那怎么阻止移动端页面在维信、手机浏览器等上上下可拖拽滑动的问题呢？元宝君找到两个方法。

<!-- more -->

## 用JS在事件监听中添加阻止浏览器默认事件

```
<script type='text/javascript'>
	document.querySelector('body').addEventListener('touchstart', function (ev) {
	    event.preventDefault();
	});
</script>
```

**preventDefault()**：将通知 Web 浏览器不要执行与事件关联的默认动作（如果存在这样的动作）。例如，如果 type 属性是 “submit”，在事件传播的任意阶段可以调用任意的事件句柄，通过调用该方法，可以阻止提交表单。注意，如果 Event 对象的 cancelable 属性是 fasle，那么就没有默认动作，或者不能阻止默认动作。无论哪种情况，调用该方法都没有作用。

类似还有：

```
$(document).on($('a'),'click',function(event){
    event.preventDefault();    
})
```

目的是禁止标签<a>默认的跳转事件。也就说明了event.preventDefault();可以禁止a元素的专属动作。

但是这样用JS阻止了body的默认touch事件，会导致div里面也不能滚动，跟touch相关的事件都失效了，简单粗暴的方法治标不治本。

下面试试第二种方法。

## 使用meta标签

```
<meta name="x5-fullscreen" content="true">
<meta name="full-screen" content="yes">
```

将这两格meta放到head里面，可以让微信，qq，uc浏览器使用全屏模式，全屏模式里，浏览器是不会上下左右滑动出现背景的。