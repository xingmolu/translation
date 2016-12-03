
> 原文链接：https://www.codeproject.com/articles/598955/coordinateplussystemplusinplushtml-pluscanvas-cpl  

# canvas中的坐标系

> 在某些动画类型中，默认坐标系是不方便的，幸好，你可以使用转型方式来改变它...

HTML5 Canvas中的坐标系统以其原点（0, 0）位于左上角的方式是设置。这个解决方案在屏幕图形学领域并不新鲜（例如windows窗体和svg也是如此）。过去标准的CRT监视器从上到下显示图像行，并且从左到右创建行中的图像。因此，定位原点（0，0）在左上角是直观的，它使创建硬件和软件处理图形更容易。  
不幸的是有些时候，canvas中的默认坐标系统是有点不切实际的。让我们假设你想创建弹丸运动动画，对于上升的弹丸，y坐标是上升的这看起来是很自然的，但是这会导致一个很奇怪的效果：  
![default coordinate](img/canvas_coordinate/default_coord.jpg)