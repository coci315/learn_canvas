#### 状态的保存和恢复 Saving and restoring state

* `save()restore()` save 和 restore 方法是用来保存和恢复 canvas 状态的，都没有参数。Canvas 的状态就是当前画面应用的所有样式和变形的一个快照。
* Canvas状态存储在栈中，每当`save()`方法被调用后，当前的状态就被推送到栈中保存。一个绘画状态包括：
  * 当前应用的变形（即移动，旋转和缩放）
  * strokeStyle, fillStyle, globalAlpha, lineWidth, lineCap, lineJoin, miterLimit, shadowOffsetX, shadowOffsetY, shadowBlur, shadowColor, globalCompositeOperation 的值
  * 当前的裁切路径（clipping path）
* 可以调用任意多次 save 方法。
* 每一次调用 restore 方法，上一个保存的状态就从栈中弹出，所有设定都恢复。

#### 移动 Translating

* 用来移动 canvas 和它的原点到一个不同的位置。
* `translate(x, y)` translate 方法接受两个参数。x 是左右偏移量，y 是上下偏移量。

#### 旋转 Rotating

* 用于以原点为中心旋转 canvas。
* `rotate(angle)` 这个方法只接受一个参数：旋转的角度(angle)，它是顺时针方向的，以弧度为单位的值。
* 旋转的中心点始终是 canvas 的原点，如果要改变它，我们需要用到 translate 方法。

#### 缩放 Scaling

* 用它来增减图形在 canvas 中的像素数目，对形状，位图进行缩小或者放大。
* `scale(x, y)` scale 方法接受两个参数。x,y 分别是横轴和纵轴的缩放因子，它们都必须是正值。值比 1.0 小表示缩小，比 1.0 大则表示放大，值为 1.0 时什么效果都没有。

#### 变形 Transforms

* 允许对变形矩阵直接修改。
* `transform(m11, m12, m21, m22, dx, dy)` 这个方法是将当前的变形矩阵乘上一个基于自身参数的矩阵，在这里我们用下面的矩阵：
  ```
  m11 m21 dx
  m12 m22 dy
  0   0   1
  ```
  如果任意一个参数是无限大，变形矩阵也必须被标记为无限大，否则会抛出异常。

  这个函数的参数各自代表如下：

  m11：水平方向的缩放

  m12：水平方向的偏移

  m21：竖直方向的偏移

  m22：竖直方向的缩放

  dx：水平方向的移动

  dy：竖直方向的移动

* `setTransform(m11, m12, m21, m22, dx, dy)` 这个方法会将当前的变形矩阵重置为单位矩阵，然后用相同的参数调用 transform 方法。如果任意一个参数是无限大，那么变形矩阵也必须被标记为无限大，否则会抛出异常。从根本上来说，该方法是取消了当前变形,然后设置为指定的变形,一步完成。

* `resetTransform()` 重置当前变形为单位矩阵，它和调用以下语句是一样的：`ctx.setTransform(1, 0, 0, 1, 0, 0);`