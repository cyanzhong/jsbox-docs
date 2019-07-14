> 此接口用于创建 PDF 文档

# $pdf.make(object)

通过 URL 或者 html 来创建 PDF 文档：

```js
$pdf.make({
  html: "<p>Hello, World!</p><h1 style='background-color: red;'>xTeko</h1>",
  handler: function(resp) {
    var data = resp.data
    if (data) {
      $share.sheet(["sample.pdf", data])
    }
  }
})
```

也可以使用图片来创建 PDF 文件：

```js
let {data} = await $pdf.make({"images": images});
```

支持通过 `pageSize` 来设置页面大小，例如：

```js
$pdf.make({
  url: "https://github.com",
  pageSize: $pageSize.A5,
  handler: function(resp) {
    var data = resp.data
    if (data) {
      $share.sheet(["sample.pdf", data])
    }
  }
})
```

`$pageSize` 支持 A0 ~ A10, B0 ~ B10, C0 ~ C10 等取值，请参考：http://en.wikipedia.org/wiki/Paper_size

# $pdf.toImages(data)

将 PDF 文档渲染成一个 image 数组：

```js
const images = $pdf.toImages(pdf);
```

# $pdf.toImage(data)

将 PDF 文档渲染成一个 image 对象：

```js
const image = $pdf.toImage(pdf);
```