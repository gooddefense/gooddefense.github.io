---
title: canvas
date: 2023-11-26 21:19:02
tags:
categories: 前端
---

# Canvas

## 什么是Canvas？
HTML5 元素用于图形的绘制，通过**脚本** (通常是JavaScript)来完成.

**适配问题**
基本上大多数的浏览器都支持canvas元素，除了一些很老旧的版本，比如**Internet Explorer 8 及更早 IE 版本的浏览器**，这些浏览器是不支持canvas元素的。


## 创建一个画布
画布在网页上是一个矩形，默认条件下，画布是没有边框和内容的。因此，在设置canvas元素时，需要提前给canvas元素设置边框。

通过JavaScript设置canvas标签时，canvas标签一般都需要带一个id属性（方便引用）;通过设置**width**和**height**属性，定义画布的大小；使用style属性设置边框；

示例代码如下：
```HTML
<p>test_demo_1</p>
<canvas id="canvas1" width="200" height="100" style="border: 1px solid #000000;">
    
</canvas>
```

## canvas绘图
### canvas - 坐标
canvas是一个二维网格，画布的左上角坐标为(0,0)。

想要使用canvas绘图，必须要使用JavaScript，canvas本身是没有绘图功能的。

JavaScript怎么使用canvas进行绘图()？
- 找到canvas元素
```JavaScript
    var c = document.getElementById("canvas1")
```

- 创建context对象
```JavaScript
    var ctx = c.getContext("2d")
```
- 根据自己的需求，对context对象进行操作

这里使用绘制一个矩形作为参考
```JavaScript
    ctx.fillStyle="ff0000"
    ctx.fillRect(0,0,150,75)
```

**fillStyle属性可以是CSS颜色，渐变或图案。fillStyle的默认值是#000000(黑色)**

**fillRect(x,y,width,height) 方法定义了矩形当前的填充方式**


### canvas - 路径
画线的两种方法：
- moveTo(x,y)  定义线条开始坐标
- lineTo(x,y)  定义线条结束坐标

设置完开始坐标和结束坐标后，需要加上**stroke()**

画圆的方法：
- arc(x,y,r,start,stop)

设置完开始坐标和结束坐标后，需要加上**stroke()**

### canvas - 文本
重要属性和方法：
- font - 定义字体
- fillText(text,x,y) - 在 canvas 上绘制实心的文本
- strokeText(text,x,y) - 在 canvas 上绘制空心的文本
### canvas - 渐变
设置渐变的两种方法：
- createLinearGradient(x,y,x1,y1) - 创建线条渐变
- createRadialGradient(x,y,r,x1,y1,r1) - 创建一个径向/圆渐变

**createRadialGradient(x,y,r,x1,y1,r1)各个参数的含义：**
- x 表示渐变的开始圆的 x 坐标
- y 表示渐变的开始圆的 y 坐标
- r 表示开始圆的半径
- x1 表示渐变的结束圆的 x 坐标
- y1 表示渐变的结束圆的 y 坐标
- r1 表示结束圆的半径

使用渐变对象时，必须使用两种或两种以上的渐变颜色
**addColorStop()** 方法指定颜色停止，参数使用坐标来描述，可以是0至1
### canvas - 图像
把一幅图像放置到画布上, 使用以下方法:
- drawImage(image,x,y)

实例代码：
```JavaScript
        //在画布上画线
        var c =document.getElementById("canvas1")
        var ctx = c.getContext("2d")
        ctx.fillStyle="#FF0000"
        ctx.fillRect(0,0,200,100)
        ctx.moveTo(0,0)
        ctx.lineTo(200,100)
        ctx.stroke()

        //在画布上画圆
        var c =document.getElementById("canvas2")
        var ctx_2 = c.getContext("2d")
        ctx_2.fillStyle="#FF0000"
        ctx_2.fillRect(0,0,200,100)
        ctx_2.beginPath()
        ctx_2.arc(95,50,40,0,2*Math.PI)
        ctx_2.stroke()

        //在画布上写字
        var c =document.getElementById("canvas3")
        var ctx_3 = c.getContext("2d")
        ctx_3.font="30px Arial";
        ctx_3.fillText("Hello World",10,50)

        //在画布上实现渐变效果
        var c =document.getElementById("canvas4")
        var ctx_4 = c.getContext("2d")
        
        //创造gradient
        //实现线性渐变
        var grd = ctx_4.createLinearGradient(0,0,200,0)
        //实现圆形渐变
        //var grd = ctx_4.createRadialGradient(75,50,5,90,60,100)
        grd.addColorStop(0,"red")
        grd.addColorStop(1,"white")

        //将grd对象当成fillStyle覆盖整个画板
        ctx_4.fillStyle = grd
        ctx_4.fillRect(10,10,150,80)


```


[canvas参考手册](https://www.w3cschool.cn/htmltags/ref-canvas.html)