> 用于与系统自带的传感器交互，例如获取加速度

# $motion.startUpdates(object)

监听 motion 数据变化：

```js
$motion.startUpdates({
  interval: 0.1,
  handler: function(resp) {

  }
})
```

返回的数据请参考 [CMDeviceMotion](https://developer.apple.com/documentation/coremotion/cmdevicemotion)。

# $motion.stopUpdates()

停止更新 motion 数据。