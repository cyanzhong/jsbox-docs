# $quicklook

iOS has a builtin previewer to open files, a lot of file formats are supported.

This is very useful, we can use it to open office files, PDFs, and much more.

We can use it through url:

```js
$quicklook.open({
  url: "",
  handler: function() {
    // Handle dismiss action, optional
  }
})
```

Binary data:

```js
$quicklook.open({
  type: "jpg",
  data: data
})
```

Image object:

```js
$quicklook.open({
  image: image
})
```

Plain text:

```js
$quicklook.open({
  text: "Hello, World!"
})
```

JSON object:

```js
$quicklook.open({
  json: "{\"a\": [1, 2, true]}"
})
```

HTML contents:

```js
$quicklook.open({
  html: "<p>HTML</p>"
})
```

Or, a content list (they should be same type, either file or url):

```js
$quicklook.open({
  list: ["", "", ""]
})
```

Please note, we can set `type` to indicate the file type, it's optional, but it's better to have one.