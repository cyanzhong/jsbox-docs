> JSBox 也提供了一套用于拍照或选择照片的接口

# $photo.take(object)

拍摄一张照片：

```js
$photo.take({
  handler: function(resp) {
    var image = resp.image
  }
})
```

支持的参数表，常量请参考[常量表](data/constant.md)：

参数 | 类型 | 说明
---|---|---
format | string | 可选 "image" 和 "data"，默认 "image"
edit | boolean | 是否编辑
mediaTypes | array | 媒体类型
maxDuration | number | 视频最大时长
quality | number | 质量
showsControls | boolean | 是否显示控制器
device | number | 前后镜头
flashMode | number | 闪光灯模式

# $photo.pick(object)

从系统相册选择一张图片：

```js
$photo.pick({
  handler: function(resp) {
    var image = resp.image
  }
})
```

所支持的参数与 `$photo.take` 完全一致，你可以认为他们只是数据来源不同。

此外，`$photo.pick` 支持通过 `multi: true` 来设置选择多个结果，多选时返回的结果结构如下：

参数 | 类型 | 说明
---|---|---
status | bool | 是否成功
results | array | 所有结果

results 里面的某一项，当 format 为 `image` 时结构为：

参数 | 类型 | 说明
---|---|---
image | image | 图片对象
metadata | object | 元数据

当 format 为 `data` 时结构为：

参数 | 类型 | 说明
---|---|---
data | data | 图片二进制数据
metadata | object | 元数据

# $photo.prompt(object)

弹出一个 action sheet 让用户选择是拍照还是从相册选择图片：

```js
$photo.prompt({
  handler: function(resp) {
    var image = resp.image
  }
})
```

# 获取图片的 metadata

在 `$photo.pick` 和 `$photo.take` 的返回结果中，可以取得图片的元数据，例如地理位置：

```js
$photo.pick({
  handler: function(resp) {
    var metadata = resp.metadata
    if (metadata) {
      var gps = metadata["{GPS}"]
      var url = "https://maps.apple.com/?ll=" + gps.Latitude + "," + gps.Longitude
      $app.openURL(url)
    }
  }
})
```

获取图片的 GPS 信息并在 Apple 地图中打开。

# $photo.scan()

使用内置的文档扫描工具（仅 iOS 13）：

```js
const response = await $photo.scan();
// response.status, response.results
```

# $photo.save(object)

将图片存储到相册：

```js
// data
$photo.save({
  data: data,
  handler: function(success) {

  }
})
```

```js
// image
$photo.save({
  image: image,
  handler: function(success) {

  }
})
```

# $photo.fetch(object)

在系统相册中读取图片：

```js
$photo.fetch({
  count: 3,
  handler: function(images) {

  }
})
```

支持一些参数来确定搜索的范围，比如图片类型，常量请参考[常量表](data/constant.md)：

参数 | 类型 | 说明
---|---|---
type | number | 媒体类型
subType | number | 媒体子类型
format | string | 可选 "image" 和 "data"，默认 "image"
size | $size | 图片大小，默认原图
count | number | 读取数量

# $photo.delete(object)

在系统相册中删除图片：

```js
$photo.delete({
  count: 3,
  handler: function(success) {

  }
})
```

支持的参数和 `$photo.fetch` 相同。

# image 转换成 data

`image` 类型提供了两个方法用于转换成二进制数据：

```js
// PNG
var png = image.png
// JPEG
var jpg = image.jpg(0.8)
```

jpg 格式使用 `0.0 ~ 1.0` 来表示质量。