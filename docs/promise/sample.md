# 两种模式

JSBox 提供的异步接口里面，对 Promise 的支持两种模式：

- 直接支持 Promise 相关调用
- 需要传参 `async: true` 表明这是一个 Promise 调用

这两种形式其实很好理解，是为了兼容早期 JSBox 的 handler 风格接口而做的妥协，之后可能会全部迁移至第一种。

简单来说，在有些接口里面，你必须处理回调，例如：

```js
$ui.menu({
  items: ["A", "B", "C"],
  handler: (title, index) => {

  }
})
```

如果你弹出一个菜单，用户选择之后什么都不做，这是没有道理的，所以这种情况我们会认为这是一个“必须要回调”的接口，你可以直接：

```js
var result = await $ui.menu({ items: ["A", "B", "C"] })
var title = result.title
var index = result.index
// Or: var result = await $ui.menu(["A", "B", "C"])
```

但是有些情况则不然，比如你可以删除一个图片，这个时候回调也可以不回调也没事：

```js
$photo.delete({
  count: 3,
  screenshot: true,
  handler: success => {
    // It's OK to remove handler here
  }
})
```

对于这种可选回调的异步接口，你需要添加 async 参数来指明你需要 Promise 调用：

```js
var success = await $photo.delete({
  count: 3,
  screenshot: true,
  async: true
})
```

这样的取舍是为了兼容两种调用方式，如果不指明 `async: true` 的话，这将是一个可选的 callback 回调。

同时，请注意不是所有的接口都能异步，有些接口完全是同步接口，例如：

```js
var success = $file.delete("sample.txt")
```

这样的接口没有必要（也无法）Promise 调用，我们之后将会有一个表来详细说明各个接口的支持情况。

# 一些好用的简写

当你使用 Promise 之后，你可能会发现有时候参数只剩下一个，是没有必要包装成一个 JSON 数据的，所以我们提供了一些简写，例如上面提到过的：

```js
var resp = await $http.get('https://docs.xteko.com')
```

这样一些方便的形式可以少写很多代码，这是一些样例：

```js
// Thread
await $thread.main(3)
await $thread.background(3)

// HTTP
var resp = await $http.get('https://docs.xteko.com')
var result = await $http.shorten("http://docs.xteko.com")

// UIKit
var result = await $ui.menu(["A", "B", "C"])

// Cache
var cache = await $cache.getAsync("key")
```