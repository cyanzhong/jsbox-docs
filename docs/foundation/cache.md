> 持久化，是程序必备的内容，JSBox 提供了多种持久化方式，这里我们介绍对象缓存。

# 提示

JSBox 提供了对象的内存缓存和文件缓存，需注意缓存的对象要遵循 [NSCoding](https://developer.apple.com/documentation/foundation/nscoding)，默认的 JavaScript 对象都支持。

所有的接口均提供同步操作和异步操作（Async 结尾），可以根据需要选择。

# $cache.set(string, object)

写入缓存：

```js
$cache.set("sample", {
  "a": [1, 2, 3],
  "b": "1, 2, 3"
})
```

# $cache.setAsync(object)

异步写入缓存：

```js
$cache.setAsync({
  key: "sample",
  value: {
    "a": [1, 2, 3],
    "b": "1, 2, 3"
  },
  handler: function(object) {

  }
})
```

# $cache.get(string)

读取缓存：

```js
$cache.get("sample")
```

# $cache.getAsync(object)

异步读取缓存：

```js
$cache.getAsync({
  key: "sample",
  handler: function(object) {

  }
})
```

# $cache.remove(string)

移除缓存：

```js
$cache.remove("sample")
```

# $cache.removeAsync(object)

异步移除缓存：

```js
$cache.removeAsync({
  key: "sample",
  handler: function() {
    
  }
})
```

# $cache.clear()

清除该扩展的全部缓存，并不会影响其他扩展产生的任何缓存：

```js
$cache.clear()
```

# $cache.clearAsync(object)

异步清除该扩展的全部缓存：

```js
$cache.clearAsync({
  handler: function() {

  }
})
```