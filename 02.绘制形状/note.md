#### 栅格

* 栅格的起点为左上角（坐标为（0,0））。所有元素的位置都相对于原点定位。

#### 绘制矩形

* 不同于SVG，HTML中的元素canvas只支持一种原生的图形绘制：矩形。
* 所有其他的图形的绘制都至少需要生成一条路径。
* canvas提供了三种方法绘制矩形：

    1. `fillRect(x, y, width, height)` 绘制一个填充的矩形
    2. `strokeRect(x, y, width, height)` 绘制一个矩形的边框
    3. `clearRect(x, y, width, height)` 清除指定矩形区域，让清除部分完全透明。

    x与y指定了在canvas画布上所绘制的矩形的左上角（相对于原点）的坐标。width和height设置矩形的尺寸。

#### 绘制路径

* 路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。
* 一个路径，甚至一个子路径，都是闭合的。
* 使用路径绘制图形需要一些额外的步骤:

     1. 首先，你需要创建路径起始点。
     2. 然后你使用画图命令去画出路径。
     3. 之后你把路径封闭。
     4. 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。

* 以下是所要用到的函数：

    1. `beginPath()` 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。
    2. `closePath()` 闭合路径之后图形绘制命令又重新指向到上下文中。
    3. `stroke()` 通过线条来绘制图形轮廓。
    4. `fill()` 通过填充路径的内容区域生成实心的图形。

    当你调用fill()函数时，所有没有闭合的形状都会自动闭合，所以你不需要调用closePath()函数。但是调用stroke()时不会自动闭合。

#### 移动笔触

* `moveTo(x, y)` 将笔触移动到指定的坐标x以及y上。

#### 绘制直线

* `lineTo(x, y)` 绘制一条从当前位置到指定x以及y位置的直线。

#### 圆弧

* `arc(x, y, radius, startAngle, endAngle, anticlockwise)` 画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。

  > 注意：arc()函数中的角度单位是弧度，不是度数。角度与弧度的js表达式:radians=(Math.PI/180)*degrees。

* `arcTo(x1, y1, x2, y2, radius)` 根据给定的控制点和半径画一段圆弧，再以直线连接两个控制点。

#### 贝塞尔（bezier）以及二次贝塞尔

* `quadraticCurveTo(cp1x, cp1y, x, y)` 绘制贝塞尔曲线，cp1x,cp1y为控制点，x,y为结束点。
* `bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)` 绘制二次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。

#### 矩形

* `rect(x, y, width, height)`  绘制一个左上角坐标为（x,y），宽高为width以及height的矩形。

#### Path2D对象

* 为了简化代码和提高性能，Path2D对象已可以在较新版本的浏览器中使用，用来缓存或记录绘画命令。
* `Path2D()`会返回一个新初始化的Path2D对象（可能将某一个路径作为变量——创建一个它的副本，或者将一个包含SVG path数据的字符串作为变量）。

```javascript
new Path2D();     // 空的Path对象
new Path2D(path); // 克隆Path对象
new Path2D(d);    // 从SVG建立Path对象
```

* 所有的路径方法比如 moveTo, rect, arc 或 quadraticCurveTo等，都可以在Path2D中使用。

#### 使用 SVG paths

* Path2D API有另一个强大的特点，就是使用SVG path data来初始化canvas上的路径。

```javascript
var p = new Path2D("M10 10 h 80 v 80 h -80 Z");
```

这条路径将先移动到点 (M10 10) 然后再水平移动80个单位 (h 80)，然后下移80个单位 (v 80)，接着左移80个单位 (h -80)，再回到起点处 (z)。