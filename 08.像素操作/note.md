#### ImageData 对象

* `ImageData`对象中存储着canvas对象真实的像素数据，它包含以下几个只读属性：
  * `width` 图片宽度，单位是像素
  * `height` 图片高度，单位是像素
  * `data` Uint8ClampedArray类型的一维数组，包含着RGBA格式的整型数据，范围在0至255之间（包括255）。

* `Uint8ClampedArray`  包含高度 × 宽度 × 4 bytes数据，索引值从0到(高度×宽度×4)-1
* 例如，从行50，纵200的像素中读取图片的蓝色部份，你会写以下代码：
  ```javascript
  blueComponent = imageData.data[((50*(imageData.width*4)) + (200*4)) + 2];
  ```
* 使用`Uint8ClampedArray.length`属性来读取像素数组的大小（以bytes为单位）：
  ```javascript
  var numBytes = imageData.data.length;
  ```

#### 创建一个ImageData对象

* 有2个版本的`createImageData()`方法。
  * 创建了一个新的具体特定尺寸的ImageData对象。所有像素被预设为透明黑。
    ```javascript
    var myImageData = ctx.createImageData(width, height);
    ```
  * 创建一个被anotherImageData对像指定的相同像素的ImageData对像。这个新的对像像素全部被预设为透明黑。这个并非复制了图片数据。
    ```javascript
    var myImageData = ctx.createImageData(anotherImageData);
    ```

#### 得到场景像素数据

  ```javascript
  var myImageData = ctx.getImageData(left, top, width, height);
  ```
  * 这个方法会返回一个ImageData对像，它代表了画布区域的像素数据，此画布的四个角落分别表示为(left, top), (left + width, top), (left, top + height), 以及(left + width, top + height)四个点。这些坐标点被设定为画布坐标空间元素。

#### 在场景中写入像素数据

* `ctx.putImageData(myImageData, dx, dy);` dx和dy参数表示你希望在场景内左上角绘制的像素数据所得到的设备坐标。

#### 缩放和反锯齿

#### 保存图片

* `HTMLCanvasElement`  提供一个`toDataURL()`方法，此方法在保存图片的时候非常有用。它返回一个包含被类型参数规定的图像表现格式的数据链接。返回的图片分辨率是96dpi。

* `canvas.toDataURL('image/png')` 默认设定。创建一个PNG图片。
* `canvas.toDataURL('image/jpeg', quality)` 创建一个JPG图片。你可以有选择地提供从0到1的品质量，1表示最好品质，0基本不被辨析但有比较小的文件大小。当你从画布中生成了一个数据链接，例如，你可以将它用于任何`<image>`元素，或者将它放在一个有download属性的超链接里用于保存到本地。
* `canvas.toBlob(callback, type, encoderOptions)` 创建一个在画布中的代表图片的Blob对象。
