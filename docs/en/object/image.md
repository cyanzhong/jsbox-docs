# image

`image` means a bitmap in memory:

Prop | Type | Read/Write | Description
---|---|---|---
size | $size | r | size
orientation | number | r | orientation
info | object | r | metadata
scale | number | r | scale
png | data | r | png format data

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