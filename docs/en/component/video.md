# type: "video"

`video` is used to play video:

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

Since video component is implemented with WebView internally, you can also load local videos with `local://` protocol:

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

Besides, there is a demo that uses `AVPlayerViewController` for video playing: https://gist.github.com/cyanzhong/c3992af39043c8e0f25424536c379595

# video.pause()

Pause the video:

```js
$("video").pause()
```

# video.play()

Play the video:

```js
$("video").play()
```

# video.toggle()

Toggle the state:

```js
$("video").toggle()
```

We can load the video by set `src`, and the the image by `poster`.

Video component is now implemented by a web view internally.

We're considering replace the implementation with native controls to have better performance in the future.