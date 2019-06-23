> 用于 Safari 交互，例如打开 Safari View Controller 或注入 JavaScript 到 Safari

# $safari.open(object)

通过 [Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 打开网页：

```js
$safari.open({
  url: "https://www.apple.com",
  entersReader: true,
  height: 360,
  handler: function() {

  }
})
```

`entersReader` 表示在可能的情况下自动进入阅读模式。

`height` 可以设置在 Widget 上运行时的打开高度，可选项。

`handler` 为完成后的回调，可选项。

# $safari.items

当你使用 Action Extension 时，可以使用这个方法获得 Safari 环境里的数据：

```js
var items = $safari.items // JSON format
```

# $safari.inject(script)

当你使用 Action Extension 时，可以使用这个方法向 Safari 注入 JavaScript:

```js
$safari.inject("window.location.href = 'https://apple.com';")
```

Action Extension 会被关闭，同时 JavaScript 会被运行在 Safari。

更多有用的例子：https://github.com/cyanzhong/xTeko/tree/master/extension-scripts/safari-extensions

# $safari.addReadingItem(object)

添加到 Safari 的阅读列表：

```js
$safari.addReadingItem({
  url: "https://sspai.com",
  title: "Title", // Optional
  preview: "Preview text" // Optional
})
```