> 原文链接：http://www.ckollars.org/canvas-two-coordinate-scales.html
> 


# canvas：在两个坐标系之间自动缩放  

HTML中的canvas既简单又强大。它看上去需要相当复杂的编程只是做ho-hum的东西，但是实际上它可以做很多事情且很容易，它不能证明书呆子只是标志。要解锁它的全部力量，你应该在一定程度上了解它的工作原理。

## canvas背景
canvas标签通过同时使用2个不同的坐标系统提供复杂的功能。（不幸的是canvas经常忽略甚至去到可用的复杂性）  

canvas标签不同于几乎所有的其他HTML元素，在同时使用两个不同的坐标系统。当您想要在画布上绘制任何东西时，模型坐标系统是非常用于的。显示坐标系标度用于控制专用于画布的物理屏幕空间。你应该明确指定模型坐标大小作为HTML中的属性，以及css中的显示坐标大小。  


一些时候两个坐标系是相同的，提供1：1的无缩放映射（可能没有太多征服感~太简单？？）。大多数时候，两个坐标系处于不同的缩放刻度。（实际上，在一些情况下，X/水平缩放因子甚至不与Y/垂直缩放因子相同。）每当模型（model）和显示（display）比例不同时，浏览器总是自动缩放（和自动重新缩放）画布上绘制的所有内容，所以你永远不需要关心显式缩放（甚至不会改变当屏幕旋转时改变大小的画布）。  

有两个不同的坐标系统，一个用于在画布上绘制，另一个用于在页面中定位画布，这意味着你可以稍后更改网页的外观，而不影响绘图说明。更改显示画布的大小只会更改显示坐标；javascript绘图命令使用的模型坐标不受影响，所以，你可以更改画布的显示大小，而不必对相关的javascript进行任何修改。画布甚至可以在不同的设备上以不同的大小显示，但是所以的情况下都由同一个简单的javascript代码驱动。（你实际上从来不改变它的高度/宽度属性/属性来改变画布的模型比例。）


## 显示两个坐标系的示例

这里是一个两个坐标系的插图，这个canvas的模型尺寸为HTML中指定的100*100.在25,25和75,75处的交叉线使用模型坐标系。但是画布的实际物理显示（包括你在此网页上看到的内容）占用225*225像素的空间。（显示坐标系指css/显示像素，它们通常与物理像素相同，但对于具有少量显示器（特别是非常高分辨率的显示器）的浏览器可能是不同的。画布后面的网格在显示器坐标系中每50像素显示一条线，刚好在画布角的外部的标签在显示器坐标中。

> canvas使用与所有其他HTML/CSS相同类型的坐标系统，实际上几乎所有的pc图像和几乎所有的其他计算机图形处理：具有原点[0, 0]在左上方并且Y坐标在向下方向上增加的笛卡尔网络。这种用于计算机图形的坐标系是自然的，并且很快变得直观；他们不需要额外的规格或计算-甚至不要添加减号。

> 画布坐标和CSS坐标都是从零开始的，因此例如100像素宽的画布的列实际上从0到99编号。为了简单和关注两个同时坐标系的概念，下面的例子只是快乐地忽略了这个事实。

![two coordinate](img/canvas_coordinate/canvas-coordinates-two-scales.gif)

```html
<canvas id="cvs" width="100" height="100"><p>canvas unsupported</p></canvas>
```

```css
#cvs{width:225px;height:225px;}
```

```javascript
var cvs = document.getElementById('cvs'); 
var ctx = cvs.getContext('2d'); 
ctx.font = 'italic bold 8px serif'; 
ctx.lineWidth = 1; 
ctx.fillStyle = '#aaaa00'; 

firstcross(ctx); 
secondcross(ctx); 

function firstcross(context) { 
  context.moveTo(25,0); 
  context.lineTo(25,100); 
  context.stroke(); 

  context.moveTo(0,25); 
  context.lineTo(100,25); 
  context.stroke(); 

  context.beginPath(); 
  context.arc(25,25, 2, 0,Math.PI*2); 
  context.closePath(); 
  context.fill(); 

  context.fillText("25,25", 1,22); 
} 

function secondcross(context) { 
  context.moveTo(75,0); 
  context.lineTo(75,100); 
  context.stroke(); 

  context.moveTo(0,75); 
  context.lineTo(100,75); 
  context.stroke(); 

  context.beginPath(); 
  context.arc(75,75, 2, 0,Math.PI*2); 
  context.closePath(); 
  context.fill(); 

  context.fillText("75,75", 76,83); 
} 
```