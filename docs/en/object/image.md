# image

`image` means a bitmap in memory:

Prop | Type | Read/Write | Description
---|---|---|---
size | $size | r | size
orientation | number | r | orientation
info | object | r | metadata
scale | number | r | scale
png | data | r | png format data

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

Returns a resized image:

```js
var resized = image.resized($size(100, 100))
```

# jpg(number)

Returns a data with jpeg format, the number means compress quality (0 ~ 1):

```js
var jpg = image.jpg(0.8)
```

# colorAtPixel($point)

Get color at a pixel:

```js
var color = image.colorAtPixel($point(0, 0));
var hexCode = color.hexCode;
```

# averageColor

Get average color of image:

```js
var avgColor = image.averageColor;
```

# orientationFixedImage

Get orientation fixed image:

```js
var fixedImage = image.orientationFixedImage
```