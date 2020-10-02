> 用于与 GPS 模块进行交互，例如获取位置或追踪位置

# $location.available

检查位置服务是否可用：

```js
let available = $location.available;
```

# $location.fetch(object)

获取地理位置：

```js
$location.fetch({
  handler: function(resp) {
    var lat = resp.lat
    var lng = resp.lng
    var alt = resp.alt
  }
})
```

# $location.startUpdates(object)

监听地理位置变化：

```js
$location.startUpdates({
  handler: function(resp) {
    var lat = resp.lat
    var lng = resp.lng
    var alt = resp.alt
  }
})
```

# $location.trackHeading(object)

监听罗盘数据变化：

```js
$location.trackHeading({
  handler: function(resp) {
    var magneticHeading = resp.magneticHeading
    var trueHeading = resp.trueHeading
    var headingAccuracy = resp.headingAccuracy
    var x = resp.x
    var y = resp.y
    var z = resp.z
  }
})
```

# $location.stopUpdates()

停止更新。

# $location.select(object)

从 iOS 内置的地图上选取一个点：

```js
$location.select({
  handler: function(result) {
    var lat = result.lat
    var lng = result.lng
  }
})
```

# $location.get()

获取当前位置，和 $location.fetch 类似但使用 async await 实现。

```js
const location = await $location.get();
```

# $location.snapshot(object)

生成地图的一个截图：

```js
const loc = await $location.get();
const lat = loc.lat;
const lng = loc.lng;
const snapshot = await $location.snapshot({
  region: {
    lat,
    lng,
    // distance: 10000
  },
  // size: $size(256, 256),
  // showsPin: false,
  // style: 0 (0: unspecified, 1: light, 2: dark)
});
```