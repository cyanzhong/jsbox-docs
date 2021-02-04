# type: "image"

`image` is used to display an image, the resource could be local or remote.

```js
{
  type: "image",
  props: {
    src: "https://images.apple.com/v/ios/what-is/b/images/performance_large.jpg"
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 100))
  }
}
```

Load an image using remote resource, the size is 100*100.

scr could be a base64 data starts with `data:image`:

```js
{
  type: "image",
  props: {
    src: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAASCAMAAAB7LJ7rAAAANlBMVEUAAABnZ2dmZmZmZmZnZ2dmZmZmZmZmZmZnZ2dnZ2dnZ2dmZmZoaGhnZ2dnZ2dubm5paWlmZmbvpwLOAAAAEXRSTlMA9h6lQ95r4cmLdHNbTzksJ9o8+Y0AAABcSURBVCjPhc1JDoAwFAJQWus8cv/LqkkjMXwjCxa8BfjLWuI9L/nqhmwiLYnpAMjqpuQMDI+bcgNyW921A+Sxyl3NXeWu7lL3WOXS0Ck1N3WXut/HEz6z92l8Lyf1mAh1wPbVFAAAAABJRU5ErkJggg=="
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 100))
  }
}
```

In addition, src supports url starts with `share://` and `drive://` to load files in JSBox.

Finally, JSBox icon set is also supported by image, [refer](en/data/method.md?id=iconcode-color-size).

# props

Prop | Type | Read/Write | Description
---|---|---|---
src | string | w | source url
source | object | rw | image loading info
symbol | string | rw | SF symbols id
data | $data | w | binary file
size | $size | r | image size
orientation | number | r | image orientation
info | object | r | information, metadata
scale | number | r | image scale

# props: source

After v1.55.0, the image can be specified with `source` for more detailed information:

```js
source: {
  url: url,
  placeholder: image,
  header: {
    "key1": "value1",
    "key2": "value2",
  }
}
```

# Zoomable

Since `v1.56.0`, you can create zoomable images easily:

```js
$ui.render({
  views: [
    {
      type: "scroll",
      props: {
        zoomEnabled: true,
        maxZoomScale: 3, // Optional, default is 2,
        doubleTapToZoom: false // Optional, default is true
      },
      layout: $layout.fill,
      views: [
        {
          type: "image",
          props: {
            src: "https://..."
          },
          layout: $layout.fill
        }
      ]
    }
  ]
});
```

All you need to do is just wrapping the image view with a `scroll` view, and set it as `zoomEnabled`.

# alwaysTemplate

Returns a new image with the `template` rendering image, it can be used with `tintColor` to change the image color:

```js
{
  type: "image",
  props: {
    tintColor: $color("red"),
    image: rawImage.alwaysTemplate
  }
}
```

The ahove `rawImage` is the original image you have.

# alwaysOriginal

It's similar to `alwaysTemplate`, but it returns an image with the `original` rendering mode, `tintColor` will be ignored.

# resized($size)

Get a resized image:

```js
var resizedImage = image.resized($size(60, 60))
```

# resizableImage(args)

Get a resizable image:

```js
const resizableImage = image.resizableImage($insets(10, 10, 10, 10));
```

You can specify the fill mode as `tile` (default to stretch):

```js
const resizableImage = image.resizableImage({
  insets: $insets(10, 10, 10, 10),
  mode: "tile"
});
```