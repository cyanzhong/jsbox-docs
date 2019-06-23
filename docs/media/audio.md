> 对于简单的音频播放，JSBox 通过 $audio 提供了支持

# $audio.play(object)

播放一个音频：

```js
// 通过 sound id 播放系统音频
$audio.play({
  id: 1000
})
```

iOS 系统内置 sound id 请参考：https://github.com/TUNER88/iOSSystemSoundsLibrary 。

```js
// 播放网络上的音频
$audio.play({
  url: "https://"
})
```

```js
// 播放本地音频
$audio.play({
  path: "audio.wav"
})
```

```js
// 暂停播放
$audio.pause()
```

```js
// 恢复播放
$audio.resume()
```

```js
// 停止播放
$audio.stop()
```

```js
// 设置播放进度（秒）
$audio.seek(60)
```

```js
// 获得当前的状态
var status = $audio.status
// 0: 已停止, 1: 等待播放, 2: 正在播放
```

```js
// 获取时长
var duration = $audio.duration
```

```js
// 获取当前的播放时间
var offset = $audio.offset
```

# 事件消息

音频播放过程中可以监听一些消息，例如：

```js
$audio.play({
  events: {
    itemEnded: function() {},
    timeJumped: function() {},
    didPlayToEndTime: function() {},
    failedToPlayToEndTime: function() {},
    playbackStalled: function() {},
    newAccessLogEntry: function() {},
    newErrorLogEntry: function() {},
  }
})
```

参考：https://developer.apple.com/documentation/avfoundation/avplayeritem?language=objc