# 方法列表

基于上述的考虑，JSBox 提供了下列这些方法来进行数据转换。

# $rect(x, y, width, height)

生成一个矩形，例如：

```js
var rect = $rect(0, 0, 100, 100)
```

# $size(width, height)

生成一个大小，例如：

```js
var size = $size(100, 100)
```

# $point(x, y)

生成一个位置，例如：

```js
var point = $point(0, 0)
```

# $insets(top, left, bottom, right)

返回一个边距，例如：

```js
var insets = $insets(10, 10, 10, 10)
```

# $color(string)

返回一个颜色，这里支持两种表达式，十六进制表达式：

```js
var color = $color("#00EEEE")
```

常见颜色名称：

```js
var blackColor = $color("black")
```

名称 | 颜色
---|---
tint | JSBox 主题色
black | 黑色
darkGray | 深灰
lightGray | 浅灰
white | 白色
gray | 灰色
red | 红色
green | 绿色
blue | 蓝色
cyan | 青色
yellow | 黄色
magenta | 品红
orange | 橙色
purple | 紫色
brown | 棕色
clear | 透明

以下颜色为语义化颜色，方便用于 Dark Mode 的适配，他们会在 Dark 和 Light 时展示不同的颜色：

名称 | 颜色
---|---
tintColor | 主题色
primarySurface | 一级背景
secondarySurface | 二级背景
tertiarySurface | 三级背景
primaryText | 一级文字
secondaryText | 二级文字
backgroundColor | 背景颜色
separatorColor | 分割线颜色
groupedBackground | grouped 列表背景色
insetGroupedBackground | insetGrouped 列表背景色

以下颜色为系统默认颜色，参考 [UI Element Colors](https://developer.apple.com/documentation/uikit/uicolor/ui_element_colors)

名称 | 颜色
---|---
systemGray2 | UIColor.systemGray2Color
systemGray3 | UIColor.systemGray3Color
systemGray4 | UIColor.systemGray4Color
systemGray5 | UIColor.systemGray5Color
systemGray6 | UIColor.systemGray6Color
systemLabel | UIColor.labelColor
systemSecondaryLabel | UIColor.secondaryLabelColor
systemTertiaryLabel | UIColor.tertiaryLabelColor
systemQuaternaryLabel | UIColor.quaternaryLabelColor
systemLink | UIColor.linkColor
systemPlaceholderText | UIColor.placeholderTextColor
systemSeparator | UIColor.separatorColor
systemOpaqueSeparator | UIColor.opaqueSeparatorColor
systemBackground | UIColor.systemBackgroundColor
systemSecondaryBackground | UIColor.secondarySystemBackgroundColor
systemTertiaryBackground | UIColor.tertiarySystemBackgroundColor
systemGroupedBackground | UIColor.systemGroupedBackgroundColor
systemSecondaryGroupedBackground | UIColor.secondarySystemGroupedBackgroundColor
systemTertiaryGroupedBackground | UIColor.tertiarySystemGroupedBackgroundColor
systemFill | UIColor.systemFillColor
systemSecondaryFill | UIColor.secondarySystemFillColor
systemTertiaryFill | UIColor.tertiarySystemFillColor
systemQuaternaryFill | UIColor.quaternarySystemFillColor

这些颜色在分别在 Light 和 Dark 模式下使用不同的颜色，例如 `$color("tintColor")` 会在 Light 模式下使用主题色，在 Dark 模式下使用比较亮的蓝色。

可以使用 `$color("namedColors")` 来获取颜色盘里面所有可用的颜色，返回一个字典：

```js
const colors = $color("namedColors");
```

同时，`$color(...)` 接口也可用于返回适配 Dark Mode 需要的动态颜色，像是这样：

```js
const dynamicColor = $color({
  light: "#FFFFFF",
  dark: "#000000"
});
```

该颜色在两种模式下分别为黑色和白色，自动切换，也可以简写为：

```js
const dynamicColor = $color("#FFFFFF", "#000000");
```

写法支持嵌套，你可以用 `$rgba(...)` 接口生成颜色后，用 `$color(...)` 接口生成动态颜色：

```js
const dynamicColor = $color($rgba(0, 0, 0, 1), $rgba(255, 255, 255, 1));
```

另外，JSBox 的 Dark Mode 支持深灰或纯黑两种模式，如果需要对三种状态使用不同的颜色，可以使用：

```js
const dynamicColor = $color({
  light: "#FFFFFF",
  dark: "#141414",
  black: "#000000"
});
```

# $rgb(red, green, blue)

同样是生成颜色，但这里用的是十进制 `0 ~ 255` 的数值：

```js
var color = $rgb(100, 100, 100)
```
# $rgba(red, green, blue, alpha)

同样是生成颜色，但这个支持 `alpha` 通道：

```js
var color = $rgba(100, 100, 100, 0.5)
```

# $font(name, size)

返回一个字体，`name` 字段是可选的：

```js
var font1 = $font(15)
var font2 = $font("bold", 15)
```

其中 name 是 `"bold"` 和 `default` 时，分别会使用粗体和正常字体，否则根据 name 查找系统支持的字体。

有关 iOS 自带的字体请参考：http://iosfonts.com/

# $range(location, length)

返回一个范围，例如：

```js
var range = $range(0, 10)
```

# $indexPath(section, row)

返回一个 indexPath，表示区域和位置，这在 list 和 matrix 视图里面会很常用：

```js
var indexPath = $indexPath(0, 10)
```

# $data(object)

返回一个二进制数据，支持以下构造形式：

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

```js
// byte array
const data = $data({
  byteArray: [116, 101, 115, 116]
})
```

# $image(object, scale)

创建一个 image 对象，支持多种参数类型：

```js
// file path
const image = $image("assets/icon.png");
```

```js
// sf symbols
const image = $image("sunrise");
```

```js
// url
const image = $image("https://images.apple.com/v/ios/what-is/b/images/performance_large.jpg");
```

```js
// base64
const image = $image("data:image/png;base64,...");
```

其中 `scale` 为可选参数，用于设置比例，默认为 1，设置成 0 的时候表示屏幕比例。

在最新版里面，可以使用 `$image(...)` 函数来创建适用于 Dark Mode 的动态图片，例如：

```js
const dynamicImage = $image({
  light: "light-image.png",
  dark: "dark-image.png"
});
```

该图片会分别在 Light 模式和 Dark 模式下使用不同的资源，自动完成切换，也可以简写成：

```js
const dynamicImage = $image("light-image.png", "dark-image.png");
```

除此之外，此接口还支持将图片嵌套，像是这样：

```js
const lightImage = $image("light-image.png");
const darkImage = $image("dark-image.png");
const dynamicImage = $image(lightImage, darkImage);
```

# $icon(code, color, size)

获得一个 JSBox 内置的图标，图标编号请参考：https://github.com/cyanzhong/xTeko/tree/master/extension-icons

使用样例：

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

`color` 是可选参数，不填的话使用默认颜色。

`size` 是可选参数，不填的话使用默认大小。