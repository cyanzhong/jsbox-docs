> 提供了将图片或文字等信息分享到社交网络的相关方法

# $share.sheet(object)

调用系统的 `share sheet` 分享内容：

```js
$share.sheet(["https://apple.com", "apple"])
```

既可以分享一个数组，也可以分享单独的一个数据。

目前支持的数据类型：`文本`、`链接`、`图片`和`二进制数据`（data）。

当分享二进制数据的时候，可以指定文件名：

```js
$share.sheet([
  {
    "name": "sample.mp4",
    "data": data
  }
])
```

从 Build 80 开始，支持指定回调：

```js
$share.sheet({
  items: [
    {
      "name": "sample.mp4",
      "data": data
    }
  ], // 也支持 item
  handler: function(success) {

  }
})
```

# $share.wechat(object)

分享内容到微信：

```js
$share.wechat(image)
```

将会自动识别分享内容的数据类型，目前支持`文字`、`图片`和`图片二进制数据`。

# $share.qq(object)

分享内容到 QQ:

```js
$share.qq(image)
```

将会自动识别分享内容的数据类型，目前支持`文字`、`图片`和`图片`二进制数据。

# $share.universal(object)

调用 JSBox 内置的分享面板分享内容：

```js
$share.universal(image)
```

将会自动识别分享内容的数据类型，目前支持`图片`和`图片`二进制数据。