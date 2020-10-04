# 相关方法

我们在 `$widget` 模块上新增了一些适用于桌面小组件的方法和常量，方便使用。

# $widget.setTimeline(object)

为桌面小组件提供时间线：

```js
$widget.setTimeline({
  entries: [
    {
      date: new Date()
      info: {}
    }
  ],
  policy: {
    atEnd: true
  },
  render: ctx => {
    return {
      type: "text",
      props: {
        text: "Hello, World!"
      }
    }
  }
});
```

详情请参考[时间线](home-widget/timeline.md)。

# $widget.inputValue

返回当前小组件设置的参数：

```js
const inputValue = $widget.inputValue;
```

# $widget.family

返回当前小组件的尺寸，0 ~ 2 分别表示小、中、大：

```js
const family = $widget.family;
// 0, 1, 2
```

# $widget.displaySize

返回当前小组件的显示大小：

```js
const size = $widget.displaySize;
// size.width, size.height
```

# $widget.isDarkMode

当前小组件是否运行在深色模式下：

```js
const isDarkMode = $widget.isDarkMode;
```

# $widget.alignment

返回在视图里面会用到的 `alignment` 常量：

```js
const alignment = $widget.alignment;
// center, leading, trailing, top, bottom
// topLeading, topTrailing, bottomLeading, bottomTrailing
```

也可以直接使用字符串常量，例如 "center", "leading"...

# $widget.horizontalAlignment

返回在视图里面会用到的 `horizontalAlignment` 常量：

```js
const horizontalAlignment = $widget.horizontalAlignment;
// leading, center, trailing
```

也可以直接使用字符串常量，例如 "leading", "center"...

# $widget.verticalAlignment

返回在视图里面会用到的 `verticalAlignment` 常量：

```js
const verticalAlignment = $widget.verticalAlignment;
// top, center, bottom
// firstTextBaseline, lastTextBaseline
```

也可以直接使用字符串常量，例如 "top", "center"...

# $widget.dateStyle

返回在使用时间设置 `text` 组件时会用到的 `dateStyle` 常量：

```js
const dateStyle = $widget.dateStyle;
// time, date, relative, offset, timer
```

也可以直接使用字符串常量，例如 "time", "date"...

# $env.widget

检查是否运行在桌面小组件环境：

```js
if ($app.env == $env.widget) {
  
}
```