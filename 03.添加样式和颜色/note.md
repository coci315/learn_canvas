#### 色彩Colors

* `fillStyle = color` 设置图形的填充颜色。
* `strokeStyle = color` 设置图形轮廓的颜色。
* `color` 可以是表示 CSS 颜色值的字符串，渐变对象或者图案对象。
* 默认情况下，线条和填充颜色都是黑色（CSS 颜色值 #000000）。
  ```javascript
  // 这些 fillStyle 的值均为 '橙色'
  ctx.fillStyle = "orange";
  ctx.fillStyle = "#FFA500";
  ctx.fillStyle = "rgb(255,165,0)";
  ctx.fillStyle = "rgba(255,165,0,1)";
  ```

#### 透明度 Transparency

* 通过设置 `globalAlpha` 属性或者使用一个半透明颜色作为轮廓或填充的样式。

* `globalAlpha = transparencyValue` 这个属性影响到 canvas 里所有图形的透明度，有效的值范围是 0.0 （完全透明）到 1.0（完全不透明），默认是 1.0。

* 因为 `strokeStyle `和 `fillStyle` 属性接受符合 CSS 3 规范的颜色值，可以用下面的写法来设置具有透明度的颜色。
  ```javascript
  // 指定透明颜色，用于描边和填充样式
  ctx.strokeStyle = "rgba(255,0,0,0.5)";
  ctx.fillStyle = "rgba(255,0,0,0.5)";
  ```

#### 线型Line Styles

  * `lineWidth = value` 设置线条宽度。
  * `lineCap = type` 设置线条末端样式。
  * `lineJoin = type` 设定线条与线条间接合处的样式。
  * `miterLimit = value` 限制当两条线相交时交接处最大长度；所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度。
  * `getLineDash()` 返回一个包含当前虚线样式，长度为非负偶数的数组。
  * `setLineDash(segments)` 设置当前虚线样式。
  * `lineDashOffset = value` 设置虚线样式的起始偏移量。

#### 渐变 Gradients

* 用下面的方法可以新建一个 `canvasGradient` 对象，并且赋给图形的 fillStyle 或 strokeStyle 属性。
* `createLinearGradient(x1, y1, x2, y2)` createLinearGradient 方法接受 4 个参数，表示渐变的起点 (x1,y1) 与终点 (x2,y2)。
* `createRadialGradient(x1, y1, r1, x2, y2, r2)` createRadialGradient 方法接受 6 个参数，前三个定义一个以 (x1,y1) 为原点，半径为 r1 的圆，后三个参数则定义另一个以 (x2,y2) 为原点，半径为 r2 的圆。

```javascript
var lineargradient = ctx.createLinearGradient(0,0,150,150);
var radialgradient = ctx.createRadialGradient(75,75,0,75,75,100);
```

* 创建出 `canvasGradient` 对象后，我们就可以用 `addColorStop` 方法给它上色了。
* `gradient.addColorStop(position, color)` addColorStop 方法接受 2 个参数，position 参数必须是一个 0.0 与 1.0 之间的数值，表示渐变中颜色所在的相对位置。例如，0.5 表示颜色会出现在正中间。color 参数必须是一个有效的 CSS 颜色值（如 #FFF， rgba(0,0,0,1)，等等）。

```javascript
var lineargradient = ctx.createLinearGradient(0,0,150,150);
lineargradient.addColorStop(0,'white');
lineargradient.addColorStop(1,'black');
```

#### 图案样式 Patterns

* `createPattern(image, type)` 该方法接受两个参数。Image 可以是一个 Image 对象的引用，或者另一个 canvas 对象。Type 必须是下面的字符串值之一：repeat，repeat-x，repeat-y 和 no-repeat。
* 图案的应用跟渐变很类似的，创建出一个 pattern 之后，赋给 `fillStyle` 或 `strokeStyle` 属性即可。
  ```javascript
  var img = new Image();
  img.src = 'someimage.png';
  var ptrn = ctx.createPattern(img,'repeat');
  ```

#### 阴影 Shadows

* `shadowOffsetX = float` shadowOffsetX 和 shadowOffsetY 用来设定阴影在 X 和 Y 轴的延伸距离，它们是不受变换矩阵所影响的。负值表示阴影会往上或左延伸，正值则表示会往下或右延伸，它们默认都为 0。
* `shadowOffsetY = float`
* `shadowBlur = float` shadowBlur 用于设定阴影的模糊程度，其数值并不跟像素数量挂钩，也不受变换矩阵的影响，默认为 0。
* `shadowColor = color` shadowColor 是标准的 CSS 颜色值，用于设定阴影颜色效果，默认是全透明的黑色。

#### canvas 填充规则

* 当我们用到 fill（或者 clip和isPointinPath ）你可以选择一个填充规则，该填充规则根据某处在路径的外面或者里面来决定该处是否被填充，这对于自己与自己路径相交或者路径被嵌套的时候是有用的。
* 两个可能的值：`nonzero` , `evenodd`
