# $l10n

扩展在显示文字的时候支持多种语言，JSBox 提供了简单的本地化支持，`l10n` 是 `Localization` 的缩写，因为刚好有 10 个字母。

当然，你也可以通过 `$device.info` 获取当前设备的语言，进而手动提供多种语言，`$l10n` 是一个简单的封装，让代码可以更简单。

```js
var text = $l10n("MAIN_TITLE");
```

# $delay(number, function)

一种更简单的执行延时任务的方法：

```js
$delay(3, function() {
  $ui.alert("Hey!")
})
```

3 秒钟后弹出一个 alert。

你可以通过这个方式取消执行：

```js
var task = $delay(10, function() {

})

// Cancel it
task.cancel();
```

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

# $objc_retain(object)

在有些时候通过 Runtime 声明的对象会被系统释放掉，如果你想要长期持有一个对象，可以使用这个方法：

```js
var manager = $objc("Manager").invoke("new")
$objc_retain(manager)
```

这将在整个脚本运行期间保持 manger 不被释放。

# $objc_release(object)

与 retain 相对应的函数，目的是手动释放掉对象：

```js
$objc_release(manager)
```

# $get_protocol(name)

获得一个 Objective-C 的 Protocol:

```js
var p = $get_protocol(name);
```

# $objc_clean()

清除所有的 Objective-C 定义：

```js
$objc_clean();
```
