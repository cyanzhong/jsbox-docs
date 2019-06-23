> Create PDF documents with simple API

# $pdf.make(object)

Here is an example:

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

Or, create PDF with images:

```js
let {data} = await $pdf.make({"images": images});
```

We could specify the `pageSize`:

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

To understand how `$pageSize` works, please refer to: http://en.wikipedia.org/wiki/Paper_size.