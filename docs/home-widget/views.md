# 视图

与 `$ui.render` 函数支持丰富的控件相比，小组件支持的视图类型是极为有限的。

同时，`$ui.render` 底层基于 UIKit 实现，而 `$widget.setTimeline` 底层基于 SwiftUI 实现。尽管我们为小组件设计了类似的语法结构，但两种界面技术的差异决定了之前的知识不能完全平移过来。

# 语法结构

对于任何一种视图，我们都使用如下语法进行定义：

```js
{
  type: "",
  props: {},
  views: []
}
```

这和 `$ui.render` 的方式是类似的，通过 `type` 指定类型，`props` 指定相关属性，`views` 制定其子视图。

区别在于，在 SwiftUI 里面我们不再使用类似 UIKit 的布局方式，所以也就不再通过 `layout` 进行布局。

布局相关的内容之后我们会单独介绍，我们先来看看用于实际显示的视图。

# type: "text"

该组件用于展示一段不可编辑的文本，类似于 `$ui.render` 里面的 `type: "label"`，可以通过如下方式构造：

```js
{
  type: "text",
  props: {
    text: "Hey"
  }
}
```

该方法直接使用 `text` 属性显示一段文本。

```js
{
  type: "text",
  props: {
    date: new Date(),
    style: $widget.dateStyle.time
  }
}
```

该方法使用 `date` 和 `style` 显示一个时间或日期，style 可以参考 [$widget.dateStyle](home-widget/method.md?id=widgetdatestyle)。

```js
{
  type: "text",
  props: {
    startDate: startDate,
    endDate: endDate
  }
}
```

该方法使用 `startDate` 和 `endDate` 来显示一个时间区间。

文本组件支持的属性：[bold](home-widget/modifiers.md?id=props-bold), [font](home-widget/modifiers.md?id=props-font), [lineLimit](home-widget/modifiers.md?id=props-linelimit), [minimumScaleFactor](home-widget/modifiers.md?id=props-minimumscalefactor)。

# type: "image"

用于展示一个图片，与 `$ui.render` 里面的 `type: image` 类似，可以通过如下方式构造：

```js
{
  type: "image",
  props: {
    image: $image("assets/icon.png"),
    // data: $file.read("assets/icon.png")
  }
}
```

该方式使用 JSBox 现成的接口来提供 `image` 或 `data` 对象。

```js
{
  type: "image",
  props: {
    symbol: "trash"
  }
}
```

该方式使用 [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/sf-symbols/) 显示一个图标。

```js
{
  type: "image",
  props: {
    path: "assets/icon.png"
  }
}
```

该方式直接使用文件路径来设置图片内容。

```js
{
  type: "image",
  props: {
    uri: "https://..."
  }
}
```

该方式可以使用一个在线图片地址，或是一个 base64 格式的图片字符串。

图片控件支持的属性：[resizable](home-widget/modifiers.md?id=props-resizable), [scaledToFill](home-widget/modifiers.md?id=props-scaledtofill), [scaledToFit](home-widget/modifiers.md?id=props-scaledtofit), [accessibilityHidden](home-widget/modifiers.md?id=props-accessibilityhidden), [accessibilityLabel](home-widget/modifiers.md?id=props-accessibilitylabel), [accessibilityHint](home-widget/modifiers.md?id=props-accessibilityhint)。

# type: "color"

在小组件里面，颜色可以是一个组件也可以是其他组件的一个属性，可以通过如下方式构造：

```js
{
  type: "color",
  props: {
    color: "#00EEEE"
  }
}
```

该方式使用 hex 颜色构建。

```js
{
  type: "color",
  props: {
    light: "#00EEEE",
    dark: "#EE00EE"
  }
}
```

该方式使用 `light` 和 `dark` 分别指定浅色和深色的颜色。

```js
{
  type: "color",
  props: {
    color: $color("red")
  }
}
```

该方式使用 JSBox 现有的 `$color` 接口构造。

# type: "gradient"

用于实现渐变效果，可以通过如下方式构造：

```js
{
  type: "gradient",
  props: {
    startPoint: $point(0, 0), // {"x": 0, "y": 0}
    endPoint: $point(0, 1), // {"x": 0, "y": 1}
    // locations: [0, 1],
    colors: [
      $color("#f9d423", "#4CA1AF"),
      $color("#ff4e50", "#2C3E50"),
    ]
  }
}
```

使用 `startPoint` 和 `endPoint` 来指定起始和结束点，`colors` 和 `locations` 来决定每一段渐变的颜色和位置。注：`locations` 如果指定，数量必须和 `colors` 相等。