> JSBox 自带的二维码模块，可以进行编解码和扫描

# $qrcode.encode(string)

将字符串转换成一个二维码图片：

```js
var image = $qrcode.encode("https://apple.com")
```

# $qrcode.decode(image)

将二维码图片解码成字符串：

```js
var text = $qrcode.decode(image)
```

# $qrcode.scan(function)

开始扫描二维码，用户完成扫描之后返回字符串：

```js
$qrcode.scan(function(text) {
  
})
```

当用户取消扫描时，也支持回调，例如：

```js
$qrcode.scan({
  useFrontCamera: false, // Optional
  turnOnFlash: false, // Optional
  handler(string) {
    $ui.toast(string)
  },
  cancelled() {
    $ui.toast("Cancelled")
  }
})
```