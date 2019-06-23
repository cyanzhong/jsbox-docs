# type: "image"

`image` 用于显示图片，可以加载远程的图片或本地图片：

```js
{
  type: "image",
  props: {
    src: "https://images.apple.com/v/ios/what-is/b/images/performance_large.jpg"
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 100))
  }
}
```

从远程加载一张图片，屏幕上尺寸是 100*100。

src 同样也支持 `data:image` 开头的 base64 字符串格式，例如：

```js
{
  type: "image",
  props: {
    src: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAASCAMAAAB7LJ7rAAAANlBMVEUAAABnZ2dmZmZmZmZnZ2dmZmZmZmZmZmZnZ2dnZ2dnZ2dmZmZoaGhnZ2dnZ2dubm5paWlmZmbvpwLOAAAAEXRSTlMA9h6lQ95r4cmLdHNbTzksJ9o8+Y0AAABcSURBVCjPhc1JDoAwFAJQWus8cv/LqkkjMXwjCxa8BfjLWuI9L/nqhmwiLYnpAMjqpuQMDI+bcgNyW921A+Sxyl3NXeWu7lL3WOXS0Ck1N3WXut/HEz6z92l8Lyf1mAh1wPbVFAAAAABJRU5ErkJggg=="
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 100))
  }
}
```

src 还支持以 `shared://` 或 `drive://` 开头的文件。

另外 image 也支持显示 JSBox 自带的 icon，[请参考](data/method.md?id=iconcode-color-size)。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
src | string | 只写 | 图片地址
symbol | string | 读写 | SF symbols 名称
data | $data | 只写 | 二进制数据
size | $size | 只读 | 图片大小
orientation | number | 只读 | 图片方向
info | object | 只读 | 图片信息
scale | number | 只读 | 图片比例

# resized($size)

返回一个重新调整大小后的图片：

```js
var resizedImage = image.resized($size(60, 60))
```

# resizableImage(args)

返回一个可伸缩的图片：

```js
const resizableImage = image.resizableImage($insets(10, 10, 10, 10));
```

也可以指定填充模式为 `tile` (默认为 stretch):

```js
const resizableImage = image.resizableImage({
  insets: $insets(10, 10, 10, 10),
  mode: "tile"
});
```