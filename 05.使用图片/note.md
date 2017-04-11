* 引入图像到`canvas`里需要以下两步基本操作：
  1.  获得一个指向`HTMLImageElement`的对象或者另一个`canvas`元素的引用作为源，也可以通过提供一个`URL`的方式来使用图片
  2. 使用`drawImage()`函数将图片绘制到画布上

#### 获得需要绘制的图片

* `HTMLImageElement` 这些图片是由`Image()`函数构造出来的，或者任何的`<img>`元素
* `HTMLVideoElement` 用一个`HTML`的` <video>`元素作为你的图片源，可以从视频中抓取当前帧作为一个图像
* `HTMLCanvasElement` 可以使用另一个` <canvas>` 元素作为你的图片源。
* `ImageBitmap` 这是一个高性能的位图，可以低延迟地绘制，它可以从上述的所有源以及其它几种源中生成。

#### 1.使用相同页面内的图片

* `document.images`集合
* ` document.getElementsByTagName()`方法
* 如果知道想使用的指定图片的`ID`，你可以用`document.getElementById()`获得这个图片

#### 2.使用其它域名下的图片

* 在 `HTMLImageElement`上使用`crossOrigin`属性，你可以请求加载其它域名上的图片。如果图片的服务器允许跨域访问这个图片，那么你可以使用这个图片而不污染`canvas`，否则，使用这个图片将会污染`canvas`。

#### 3.使用其它 canvas 元素

* 和引用页面内的图片类似地，用 `document.getElementsByTagName` 或 `document.getElementById` 方法来获取其它 `canvas` 元素。但你引入的应该是已经准备好的 `canvas`。

* 一个常用的应用就是将第二个`canvas`作为另一个大的 `canvas` 的缩略图。

#### 4.由零开始创建图像

* 用脚本创建一个新的 `HTMLImageElement` 对象。
* 用load事件来保证不会在加载完毕之前使用这个图片。
  ```javascript
  var img = new Image();   // 创建img元素
  img.onload = function(){
    // 执行drawImage语句
  }
  img.src = 'myImage.png'; // 设置图片源地址
  ```
#### 5.通过 data: url 方式嵌入图像

* 通过 `data:url` 方式来引用图像。`Data urls` 允许用一串 `Base64` 编码的字符串的方式来定义一个图片。
  ```javascript
  img.src = 'data:image/gif;base64,R0lGODlhCwALAIAAAAAA3pn/ZiH5BAEAAAEALAAAAAALAAsAAAIUhA+hkcuO4lmNVindo7qyrIXiGBYAOw==';
  ```
  其优点就是图片内容即时可用，无须再到服务器兜一圈。（还有一个优点是，可以将 CSS，JavaScript，HTML 和 图片全部封装在一起，迁移起来十分方便。）缺点就是图像没法缓存，图片大的话内嵌的 url 数据会相当的长。

#### 6.使用视频帧

* 使用`<video> `中的视频帧（即便视频是不可见的）。例如，如果你有一个ID为“`myvideo`”的`<video>` 元素，可以这样做：

  ```javascript
    function getMyVideo() {
    var canvas = document.getElementById('canvas');
    if (canvas.getContext) {
      var ctx = canvas.getContext('2d');

      return document.getElementById('myvideo');
      }
  }
  ```
  它将为这个视频返回`HTMLVideoElement`对象，它可以作为`Canvas`图片源。

#### 绘制图片

* `drawImage(image, x, y)` 其中 image 是 image 或者 canvas 对象，x 和 y 是其在目标 canvas 里的起始坐标。

#### 缩放 Scaling

* `drawImage(image, x, y, width, height)` 这个方法多了2个参数：width 和 height，这两个参数用来控制 当像canvas画入时应该缩放的大小

#### 切片 Slicing

* `drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)` 第一个参数和其它的是相同的，都是一个图像或者另一个 canvas 的引用。其它8个参数最好是参照右边的图解，前4个是定义图像源的切片位置和大小，后4个则是定义切片的目标显示位置和大小。
