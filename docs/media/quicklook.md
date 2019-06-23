# $quicklook

通过 $quicklook.open 我们可以通过 iOS 内置的文件查看器打开一些常见的文件格式。

通过 URL:

```js
$quicklook.open({
  url: "",
  handler: function() {
    // Handle dismiss action, optional
  }
})
```

通过 Data:

```js
$quicklook.open({
  type: "jpg",
  data: data
})
```

预览 image 对象：

```js
$quicklook.open({
  image: image
})
```

预览纯文本内容：

```js
$quicklook.open({
  text: "Hello, World!"
})
```

预览 JSON 对象：

```js
$quicklook.open({
  json: "{\"a\": [1, 2, true]}"
})
```

预览 HTML 内容：

```js
$quicklook.open({
  html: "<p>HTML</p>"
})
```

预览多个文件（list 内容必须全部为 data 或者全部是链接）：

```js
$quicklook.open({
  list: ["", "", ""]
})
```

请注意，可以传递一个 `type` 用于指定文件类型，该参数是可选的，指定的话会让结果更精确，否则则会猜测文件类型。