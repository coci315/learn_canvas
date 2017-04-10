```html
<canvas id="tutorial" width="150" height="150"></canvas>
```
* `<canvas>` 标签只有两个属性—— width和height
* 当没有设置宽度和高度的时候，`canvas`会初始化宽度为300像素和高度为150像素

#### 替换内容

* 在`<canvas></canvas>`标签内嵌套内容可以在不支持`canvas`的浏览器上显示这些替换内容，而在支持`canvas`的浏览器上则会忽略。如：

```html
<canvas id="stockGraph" width="150" height="150">
  current stock price: $3.15 +0.15
</canvas>

<canvas id="clock" width="150" height="150">
  <img src="images/clock.png" width="150" height="150" alt=""/>
</canvas>
```

#### 渲染上下文(`The rendering context`)

* `<canvas> `元素有一个做 getContext() 的方法，这个方法是用来获得渲染上下文和它的绘画功能。
* `getContext()`只有一个参数，上下文的格式。

```javascript
var canvas = document.getElementById('tutorial');
var ctx = canvas.getContext('2d');
```

#### 检查支持性

```javascript
var canvas = document.getElementById('tutorial');

if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  // drawing code here
} else {
  // canvas-unsupported code here
}
```