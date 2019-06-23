# Methods

As we mentioned before, we provided a series of methods.

# $rect(x, y, width, height)

Create a rectangle:

```js
var rect = $rect(0, 0, 100, 100)
```

# $size(width, height)

Create a size:

```js
var size = $size(100, 100)
```

# $point(x, y)

Create a point:

```js
var point = $point(0, 0)
```

# $insets(top, left, bottom, right)

Create an edge insets:

```js
var insets = $insets(10, 10, 10, 10)
```

# $color(string)

Create a color with hex string:

```js
var color = $color("#00EEEE")
```

Create a color with name:

```js
var blackColor = $color("black")
```

Available color names:

Name | Color
---|---
tint | JSBox theme color
black | black color
darkGray | dark gray
lightGray | light gray
white | white color
gray | gray color
red | red color
green | green color
blue | blue color
cyan | cyan color
yellow | yellow color
magenta | magenta color
orange | orange color
purple | purple color
brown | brown color
clear | clear color

# $rgb(red, green, blue)

Create a color with red, green, blue values.

The range of each number is 0 ~ 255:

```js
var color = $rgb(100, 100, 100)
```
# $rgba(red, green, blue, alpha)

Create a color with red, green, blue and alpha channel:

```js
var color = $rgba(100, 100, 100, 0.5)
```

# $font(name, size)

Create a font, name is an optional parameter:

```js
var font1 = $font(15)
var font2 = $font("bold", 15)
```

You can specify `"bold"` to use system font with bold weight, otherwise it will search fonts with the name.

Learn more: http://iosfonts.com/

# $range(location, length)

Create a range:

```js
var range = $range(0, 10)
```

# $indexPath(section, row)

Create an indexPath, to indicates the section and row:

```js
var indexPath = $indexPath(0, 10)
```

# $data(object)

Create a binary data:

```js
// string
var data = $data({
  string: "Hello, World!",
  encoding: 4 // default, refer: https://developer.apple.com/documentation/foundation/nsstringencoding
})
```

```js
// path
var data = $data({
  path: "demo.txt"
})
```

```js
// url
var data = $data({
  url: "https://images.apple.com/v/ios/what-is/b/images/performance_large.jpg"
})
```

```js
// base64
var data = $data({
  base64: "data:image/png;base64,..."
})
```

# $icon(code, color, size)

Get an icon provided by JSBox, refer: https://github.com/cyanzhong/xTeko/tree/master/extension-icons

For example:

```js
$ui.render({
  views: [
    {
      type: "button",
      props: {
        icon: $icon("005", $color("red"), $size(20, 20)),
        bgcolor: $color("clear")
      },
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.size.equalTo($size(24, 24))
      }
    }
  ]
})
```

`color` is optional, uses gray style if not provided.

`size` is also optional, uses raw size if not provided.