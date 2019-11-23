# image

`image` 类型表示图片对象。

属性 | 类型 | 读写 | 说明
---|---|---|---
size | $size | 只读 | 尺寸
orientation | number | 只读 | 方向
info | object | 只读 | metadata
scale | number | 只读 | scale
png | data | 只读 | png 表示的二进制数据

# alwaysTemplate

返回一个使用 `template` 模式渲染的图片，结合 `tintColor` 可以用于对模板图片进行着色：

```js
{
  type: "image",
  props: {
    tintColor: $color("red"),
    image: rawImage.alwaysTemplate
  }
}
```

上述 `rawImage` 是原始的图片。

# alwaysOriginal

与 `alwaysTemplate` 相对于，此属性返回的图片总是渲染自身的颜色，而非 `tintColor`。

# resized($size)

返回调整尺寸的图片：

```js
var resized = image.resized($size(100, 100))
```

# jpg(number)

返回 jpg 表示的二进制数据，number 表示压缩质量(0 ~ 1)：

```js
var jpg = image.jpg(0.8)
```

# colorAtPixel($point)

获得某个点的颜色值：

```js
var color = image.colorAtPixel($point(0, 0));
var hexCode = color.hexCode;
```

# averageColor

获得整张图片的平均颜色：

```js
var avgColor = image.averageColor;
```

# orientationFixedImage

获得旋转方向修正了的图片：

```js
var fixedImage = image.orientationFixedImage
```