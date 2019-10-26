# $context.query

获取通过 URL Scheme 启动扩展时的所有参数：

```js
var query = $context.query
```

用 `jsbox://runjs?file=demo.js&text=test` 启动时，query 值为：

```js
{
  "file": "demo.js",
  "text": "test"
}
```

# $context.text

返回一个文本（当用户选择文本进行分享时）：

```js
var text = $context.text
```

# $context.textItems

返回所有文本。

# $context.link

返回一个链接（当用户选择链接进行分享时）：

```js
var link = $context.link
```

# $context.linkItems

返回所有链接。

# $context.image

返回一个图片（当用户选择图片进行分享时）：

```js
var image = $context.image
```

# $context.imageItems

返回所有图片。

# $context.safari.items

当用户在 Safari 上启动扩展时，通过此方法拿到浏览器中的对象：

```js
var items = $context.safari.items
```

对象结构：

```json
{
  "baseURI": "",
  "source": "",
  "location": "",
  "contentType": "",
  "title": "",
  "selection": {
    "html": "",
    "text": "",
    "style": ""
  }
}
```

# $context.data

返回一个二进制文件（当用户选择文件进行分享时）：

```js
var data = $context.data
```

# $context.dataItems

返回所有二进制文件。

# $context.allItems

一次返回上述所有的内容在一个 JSON 对象里。

以上返回的对象和在其他地方使用的方法完全相同，也就是说 `$context` 本质上是提供了一种获取输入数据的方式。

就目前而言，`$context` 仅对从 Action Extension 运行这种场景有效。

# $context.clear()

清除 context 内的所有数据，包括传递进来的参数和 Action Extension 的数据：

```js
$context.clear();
```

# $context.close()

在 Action Extension 中运行时，通过这个方法可以关闭 Extension，请注意如果先调用了 `$app.close()`，这条语句将不会生效，因为 $app.close() 之后的代码都不会生效。