> 原文链接：http://www.ckollars.org/canvas-two-coordinate-scales.html
> 


# canvas：在两个坐标系之间自动缩放  

HTML中的canvas既简单又强大。它看上去需要相当复杂的编程只是做ho-hum的东西，但是实际上它可以做很多事情且很容易，它不能证明书呆子只是标志。要解锁它的全部力量，你应该在一定程度上了解它的工作原理。

## canvas背景
canvas标签通过同时使用2个不同的坐标系统提供复杂的功能。（不幸的是canvas经常忽略甚至去到可用的复杂性）  

canvas标签不同于几乎所有的其他HTML元素，在同时使用两个不同的坐标系统。当您想要在画布上绘制任何东西时，模型坐标系统是非常用于的。显示坐标系标度用于控制专用于画布的物理屏幕空间。你应该明确指定模型坐标大小作为HTML中的属性，以及css中的显示坐标大小。  
