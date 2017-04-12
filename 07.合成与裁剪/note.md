#### globalCompositeOperation

* 我们不仅可以在已有图形后面再画新图形，还可以用来遮盖指定区域，清除画布中的某些部分（清除区域不仅限于矩形，像clearRect()方法做的那样 ）以及更多其他操作。

* `globalCompositeOperation = type` 
* `type` 是下面 12 种字符串值之一：
  1. `source-over (default)` 这是默认设置，新图形会覆盖在原有内容之上。
  2. `destination-over` 会在原有内容之下绘制新图形。
  3. `source-in` 新图形会仅仅出现与原有内容重叠的部分。其它区域都变成透明的。
  4. `destination-in` 原有内容中与新图形重叠的部分会被保留，其它区域都变成透明的。
  5. `source-out` 结果是只有新图形中与原有内容不重叠的部分会被绘制出来。
  6. `destination-out` 原有内容中与新图形不重叠的部分会被保留。
  7. `source-atop` 新图形中与原有内容重叠的部分会被绘制，并覆盖于原有内容之上。
  8. `destination-atop` 原有内容中与新内容重叠的部分会被保留，并会在原有内容之下绘制新图形
  9. `lighter` 两图形中重叠部分作加色处理。
  10. `darken` 两图形中重叠的部分作减色处理。
  11. `xor` 重叠的部分会变成透明。
  12. `copy` 只有新图形会被保留，其它都被清除掉。

#### 裁切路径 Clipping paths

  * 裁切路径和普通的 canvas 图形差不多，不同的是它的作用是遮罩，用来隐藏不需要的部分。
  * 如果和上面介绍的 globalCompositeOperation 属性作一比较，它可以实现与 source-in 和 source-atop 差不多的效果。最重要的区别是裁切路径不会在 canvas 上绘制东西，而且它永远不受新图形的影响。这些特性使得它在特定区域里绘制图形时相当好用。
