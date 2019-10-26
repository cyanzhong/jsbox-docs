> Provides APIs to share media to social network services, such as WeChat, QQ

# $share.sheet(object)

Using system builtin `share sheet`:

```js
$share.sheet(["https://apple.com", "apple"])
```

The object could be either a file or an array.

Currently we support `text`, `link`, `image` and `data`.

It's better to specify file name if the object is a file:

```js
$share.sheet([
  {
    "name": "sample.mp4",
    "data": data
  }
])
```

Start from Build 80, you can use following style:

```js
$share.sheet({
  items: [
    {
      "name": "sample.mp4",
      "data": data
    }
  ], // or item
  handler: function(success) {

  }
})
```

# $share.wechat(object)

Share content to WeChat:

```js
$share.wechat(image)
```

The object will be detected automatically, either image or text is correct.

# $share.qq(object)

Share content to QQ:

```js
$share.qq(image)
```

The object will be detected automatically, either image or text is correct.

# $share.universal(object)

Deprecated, please use `$share.sheet` instead.