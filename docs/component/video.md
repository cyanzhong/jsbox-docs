# type: "video"

`video` 用于创建一个播放视频的控件：

```js
{
  type: "video",
  props: {
    src: "https://images.apple.com/media/cn/ipad-pro/2017/43c41767_0723_4506_889f_0180acc13482/films/feature/ipad-pro-feature-cn-20170605_1280x720h.mp4",
    poster: "https://images.apple.com/v/iphone/home/v/images/home/limited_edition/iphone_7_product_red_large_2x.jpg"
  },
  layout: function(make, view) {
    make.left.right.equalTo(0)
    make.centerY.equalTo(view.super)
    make.height.equalTo(256)
  }
}
```

由于 video 组件目前使用 WebView 实现，你也可以用 `local://` 协议来加载本地文件：

```js
{
  type: "video",
  props: {
    src: "local://assets/video.mp4",
    poster: "local://assets/poster.jpg"
  },
  layout: function(make, view) {
    make.left.right.equalTo(0)
    make.centerY.equalTo(view.super)
    make.height.equalTo(256)
  }
}
```

另外，你还可以像这个 demo 一样使用 `AVPlayerViewController` 来播放视频：https://gist.github.com/cyanzhong/c3992af39043c8e0f25424536c379595

# video.pause()

停止播放视频：

```js
$("video").pause()
```

# video.play()

继续播放视频：

```js
$("video").play()
```

# video.toggle()

切换视频播放状态：

```js
$("video").toggle()
```

`src`: 视频地址 `poster`: 封面图片地址。

内部通过一个 WKWebView 实现，所以理论上也完全可以通过 web 组件自行实现。