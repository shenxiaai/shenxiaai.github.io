---
title: 详解display:box
category: 前端
date: 2016-10-18
---

从css3发布以来出现了很多新颖的css属性，颠覆了css2的很多样式写法。其中改变最大要属的就是流式布局和弹性布局的变化了。移动端为了实现更好的兼容性，使用弹性布局无疑是最完美的布局方案了。一直以来对box-flex的属性不甚详解，今天好好分析整理，分享一些心得，另附上一些代码具体解释。

<!-- more -->

# display:box

box-flex属性，我们可以理解为box是父元素，flex是子元素。只有在父元素定义display:box后子容器才可以进行划分。目前box-flex属性还没有得到Firefox、Opera、Chrome浏览器的完全支持，但可以使用它们的私有属性定义Firefox(-moz-)、Opera(-o-)、Chrome/Safari（-webkit-)。

## 子元素等分

box-flex的值为至少为1的整数时起作用。具体看如下代码：

###### html代码

```
<div class="box">
	<div class="flex green"></div>
	<div class="flex blue"></div>
	<div class="flex yellow"></div>
</div>
```

###### css代码

```
.box{display: -webkit-box;width: 800px;height: 100px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;}
.green{background: lightgreen;}
.blue{background: lightblue;}
.yellow{background: orange;}
```

> 运行效果如下：

![](http://i.imgur.com/3ndFRyV.png)

## 子元素设置间距

###### css代码

```
.box{display: -webkit-box;width: 800px;height: 100px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;}
.green{background: lightgreen;}
.blue{background: lightblue;margin: 0 10px;}
.yellow{background: orange;}
```

> 运行效果如下：

![](http://i.imgur.com/U1b57Vw.png)

## 子元素不等比划分

###### css代码

```
.box{display: -webkit-box;width: 800px;height: 100px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;}
.green{background: lightgreen;}
.blue{background: lightblue;margin: 0 10px;-webkit-box-flex: 3;}
.yellow{background: orange;-webkit-box-flex: 2;}
```

> 运行效果如下：

![](http://i.imgur.com/m25j3Fx.png)

## 子元素定宽

###### html代码

```
<div class="box">
	<div class="flex green">width=120px</div>
	<div class="flex blue"></div>
	<div class="flex yellow"></div>
</div>
```

###### css代码

```
.box{display: -webkit-box;width: 800px;height: 100px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;text-align: center;}
.green{background: lightgreen;width: 120px;}
.blue{background: lightblue;margin: 0 10px;-webkit-box-flex: 3;}
.yellow{background: orange;-webkit-box-flex: 2;}
```

> 运行效果如下：

![](http://i.imgur.com/4yD2jf3.png)

## 父元素属性box-orient

box-orient用来确定子元素的方向。

*   inline-axis_（默认）_
*   horizontal
*   vertical
*   block-axis
*   inherit

###### css代码

```
.box{display: -webkit-box;-webkit-box-orient: vertical;width: 800px;height: 100px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;text-align: center;}
.green{background: lightgreen;width: 120px;}
.blue{background: lightblue;margin: 0 10px;-webkit-box-flex: 3;}
.yellow{background: orange;-webkit-box-flex: 2;}
```

> 运行效果如下：

![](http://i.imgur.com/6l7JKZS.png)

## 父元素属性box-direction

box-direction是用来确定子元素的排列顺序。

*   normal_（默认）_    →    从左往右
*   reverse    →    从右往左
*   inherit    →    从左往右

###### css代码

```
.box{display: -webkit-box;-webkit-box-direction: reverse;width: 800px;height: 100px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;text-align: center;}
.green{background: lightgreen;width: 120px;}
.blue{background: lightblue;margin: 0 10px;-webkit-box-flex: 3;}
.yellow{background: orange;-webkit-box-flex: 2;}
```

> 运行效果如下：

![](http://i.imgur.com/JtQqNJv.png)

## 父元素属性box-align

box-align与box-pack都是决定盒子内部剩余空间怎么使用的，box-align决定了垂直方向上的空间利用，也就是垂直方向上的对齐表现。

*   stretch_（默认）_
*   start
*   end
*   center
*   baseline

#### box-align:center

###### css代码

```
.box{display: -webkit-box;-webkit-box-align: center;width: 800px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;text-align: center;}
.green{background: lightgreen;width: 120px;height: 110px;}
.blue{background: lightblue;margin: 0 10px;-webkit-box-flex: 3;height: 290px;}
.yellow{background: orange;-webkit-box-flex: 2;height: 220px;}
```

> 运行效果如下：

![](http://i.imgur.com/0Rz8jxs.png)

#### box-align:start

###### css代码

```
.box{display: -webkit-box;-webkit-box-align: start;width: 800px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;text-align: center;}
.green{background: lightgreen;width: 120px;height: 110px;}
.blue{background: lightblue;margin: 0 10px;-webkit-box-flex: 3;height: 290px;}
.yellow{background: orange;-webkit-box-flex: 2;height: 220px;}
```

> 运行效果如下：

![](http://i.imgur.com/2pGDc94.png)

#### box-align:baseline

###### css代码

```
.box{display: -webkit-box;-webkit-box-align: baseline;width: 800px;border: 1px solid #888;}
.flex{-webkit-box-flex: 1;text-align: center;}
.green{background: lightgreen;width: 120px;height: 110px;}
.blue{background: lightblue;margin: 0 10px;-webkit-box-flex: 3;height: 290px;}
.yellow{background: orange;-webkit-box-flex: 2;height: 220px;}
```

> 运行效果如下：

![](http://i.imgur.com/nAhvyRJ.png)

## box-pack

box-pack决定了父标签水平遗留空间的使用。

*   start_（默认）_
*   end
*   center
*   justify

box-pack大部分的行为表现来说分别对应text-align属性的值：left | right | center | justify。

#### box-pack:end

###### css代码

```
.box{display: -webkit-box;-webkit-box-pack: end;border: 1px solid #888;width: 600px;}
.flex{text-align: center;padding: 0 40px;}
.green{background: lightgreen;height: 50px;}
.blue{background: lightblue;height: 90px;}
.yellow{background: orange;height: 20px;}
```

> 运行效果如下：

![](http://i.imgur.com/Z9vJpL9.png)

#### box-pack:justify

###### css代码

```
.box{display: -webkit-box;-webkit-box-pack: justify;border: 1px solid #888;width: 600px;}
.flex{text-align: center;padding: 0 40px;}
.green{background: lightgreen;height: 50px;}
.blue{background: lightblue;height: 90px;}
.yellow{background: orange;height: 20px;}
```

> 运行效果如下：

![](http://i.imgur.com/bd9bLii.png)

#### box-pack:center

###### css代码

```
.box{display: -webkit-box;-webkit-box-pack: center;border: 1px solid #888;width: 600px;}
.flex{text-align: center;padding: 0 40px;}
.green{background: lightgreen;height: 50px;}
.blue{background: lightblue;height: 90px;}
.yellow{background: orange;height: 20px;}
```

> 运行效果如下：

![](http://i.imgur.com/fg6sqis.png)

## 父元素属性box-lines

box-lines是用来决定子元素是可以换行显示还是就算挤出油还是单行显示。

*   single_（默认）_    →    单行显示
*   multiple    →    多行显示
> 不过目前无论Firefox还是Chrome似乎都对box-lines属性不支持，原因未知。

## 子元素属性box-ordinal-group

box-ordinal-group的属性值是有一个数字级别的，决定了你这个父元素的组织内的位置。数值越小，位置就越靠前。举例如下：

###### css代码

```
.box{display: -webkit-box;border: 1px solid #888;width: 600px;}
.flex{text-align: center;padding: 0 40px;}
.green{background: lightgreen;height: 50px;-webkit-box-ordinal-group: 3;}
.blue{background: lightblue;height: 90px;-webkit-box-ordinal-group: 1;}
.yellow{background: orange;height: 20px;-webkit-box-ordinal-group: 2;}
```

**注意：父元素中的每个子元素都要设置box-ordinal-group值，否则无效果。**

> 运行效果如下：

![](http://i.imgur.com/sYVuMO1.png)