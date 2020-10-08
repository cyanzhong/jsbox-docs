# 属性

小组件的属性指定了其展示效果和行为，部分属性支持所有类型的视图，部分属性是文本或图片独有的。

# 适用于所有视图

## props: frame

限定视图的大小和对齐方式：

```js
props: {
  frame: {
    width: 100,
    height: 100,
    alignment: $widget.alignment.center
  }
}
```

也可以提供更灵活的实现：

```js
props: {
  frame: {
    minWidth: 0,
    idealWidth: 100,
    maxWidth: Infinity,
    minHeight: 0,
    idealHeight: 100,
    maxHeight: Infinity,
  }
}
```

系统会自动推断得到合适的布局效果，当需要视图撑满父视图时，使用 `maxWidth: Infinity` 和 `maxHeight: Infinity`。

## props: position

指定视图的位置：

```js
props: {
  position: $point(0, 0) // {"x": 0, "y": 0}
}
```

## props: offset

指定视图的位置偏移：

```js
props: {
  offset: $point(-10, -10) // {"x": -10, "y": -10}
}
```

## props: padding

指定视图的边距：

```js
props: {
  padding: 10
}
```

这将让其上下左右四个方向的边距都是 10，也可以分别指定各个方向：

```js
props: {
  padding: $insets(10, 0, 10, 0) // {"top": 10, "left": 0, "bottom": 10, "right": 0}
}
```

## props: layoutPriority

指定布局流程中的优先级（默认为 0）：

```js
props: {
  layoutPriority: 1
}
```

## props: cornerRadius

圆角效果：

```js
props: {
  cornerRadius: 10
}
```

如需实现平滑圆角，可使用：

```js
props: {
  cornerRadius: {
    value: 10,
    style: 1 // 0: circular, 1: continuous
  }
}
```

## props: border

实现边框效果：

```js
props: {
  border: {
    color: $color("red"),
    width: 2
  }
}
```

## props: clipped

是否裁剪超出边框部分的内容：

```js
props: {
  clipped: true
}
```

也可以通过 `antialiased` 指定抗锯齿：

```js
props: {
  clipped: {
    antialiased: true
  }
}
```

## props: opacity

半透明效果：

```js
props: {
  opacity: 0.5
}
```

## props: blur

应用高斯模糊效果：

```js
props: {
  blur: 10
}
```

## props: color

视图的前景色，例如文字颜色：

```js
props: {
  color: $color("red")
}
```

## props: background

视图的背景填充，可以是颜色也可以是图片或者渐变效果：

```js
props: {
  background: {
    type: "gradient",
    props: {
      colors: [
        $color("#f9d423", "#4CA1AF"),
        $color("#ff4e50", "#2C3E50"),
      ]
    }
  }
}
```

## props: link

指定点击视图后会打开的链接（仅支持 2 * 4 和 4 * 4 的小组件）：

```js
props: {
  link: "jsbox://run?name="
}
```

不管这个链接填什么，iOS 都会先打开 JSBox 主应用，但可以将要执行的任务通过 URL scheme 的方式代理到主应用去执行。

另外，也可以使用 JSBox 支持的脚本即时执行功能：

```js
props: {
  link: "jsbox://run?script=alert%28%22hello%22%29"
}
```

这将跳转到 JSBox 主应用，并执行 `script` 参数指定的脚本。

## props: widgetURL

与 `link` 类似，但 `widgetURL` 指定的是点击整个小组件时候打开的链接：

```js
props: {
  widgetURL: "jsbox://run?script=alert%28%22hello%22%29"
}
```

2 * 2 小组件仅支持这种交互方式。

# 适用于文本

## props: bold

指定文本为粗体：

```js
props: {
  bold: true
}
```

## props: font

设置文本使用的字体：

```js
props: {
  font: {
    name: "AmericanTypewriter",
    size: 20,
    // monospaced: true
  }
}
```

也可以使用 `$font` 方法构建的字体：

```js
props: {
  font: $font("bold", 20)
}
```

## props: lineLimit

指定文本最多支持的行数：

```js
props: {
  lineLimit: 1
}
```

## props: minimumScaleFactor

当文本不足以显示时，iOS 可能会将字体缩小，该属性指定了最小可以接受的比例：

```js
props: {
  minimumScaleFactor: 0.5
}
```

无法完整显示时，内容将会被截断。

# 适用于图片

## props: resizable

指定图片是否可以被缩放：

```js
props: {
  resizable: true
}
```

## props: scaledToFill

与 [$contentMode.scaleAspectFill](data/constant.md?id=contentmode) 类似，该属性决定图片是否以拉伸并被裁剪的方式填充满父视图：

```js
props: {
  scaledToFill: true
}
```

## props: scaledToFit

与 [$contentMode.scaleAspectFit](data/constant.md?id=contentmode) 类似，该属性决定图片是否以拉伸并保持内容的方式放入父视图内：

```js
props: {
  scaledToFit: true
}
```

## props: accessibilityHidden

为图片指定 VoiceOver 是否禁用：

```js
props: {
  accessibilityHidden: false
}
```

## props: accessibilityLabel

为图片指定 VoiceOver 标签：

```js
props: {
  accessibilityLabel: "Hey"
}
```

## props: accessibilityHint

为图片指定 VoiceOver 提示语：

```js
props: {
  accessibilityHint: "Double tap to open"
}
```