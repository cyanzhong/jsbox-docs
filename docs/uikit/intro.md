# 基本概念

JSBox 对 [UIKit](https://developer.apple.com/documentation/uikit) 进行了简单的封装和抽象，让用户可以通过简单的 `JavaScript` 在 JSBox 里面绘制界面，从而提供更好的交互。

JSBox 中界面绘制采用的方案和 [React Native](https://facebook.github.io/react-native/) 以及 [Weex](https://weex.incubator.apache.org/) 不同，不需要你掌握 `HTML` 和 `CSS`，只需要定义 JavaScript Object 就能完成所有工作。

PS: 当然，你写的扩展可以没有任何界面，不提供任何用户交互也是完全可以的。

# 样例

正如前文样例提到的那样，我们可以通过下面的代码在屏幕上创建一个按钮：

```js
$ui.render({
  views: [
    {
      type: "button",
      props: {
        title: "Button"
      },
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.width.equalTo(64)
      },
      events: {
        tapped: function(sender) {
          $ui.toast("Tapped")
        }
      }
    }
  ]
})
```

这段代码囊括了 view 的四个核心：`type`, `props`, `layout` 和 `events`。

# type

type 指定了这个 view 的类型，例如上述的 button，在之后的文档里面我们会详细介绍每种 view 如何使用。

# props

props 里面可以对 view 进行各种属性设置，例如 button 支持的 `title` 属性，不同类型的 view 支持的属性不尽相同，在之后会分别介绍。

# layout

对 view 进行布局，JSBox 沿用了 iOS 里面的 [Auto Layout](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/index.html) 语法，但你无需对原生的 Auto Layout 有深入的了解（那很难用），因为我们提供的是基于 Masonry 的 DSL：https://github.com/SnapKit/Masonry 在之后我们会示例如何简单的使用 Masonry。

PS: 使用这套布局引擎实际上是一个权衡的方案，之后时间充裕的话可能会提供其他的布局引擎，例如 [Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)。

# events

在这里响应这个 view 的各种事件，例如 button 支持的 `tapped` 事件，在事件回调方法里面进行各种处理，在之后的文档里面会详细介绍每种 view 支持的 events。

# views

在某个 view 里面定义 `views` 用于描述他的子 view:

```js
{
  views: [

  ]
}
```

子 view 的结构定义和 view 完全一样，递归定义构成一个视图树。

# 类型转换

Native 代码里面很多数据类型是 JavaScript 不具备的，所以 JSBox 提供了一系列的转换方法，这在绘制界面的时候尤其重要：[数据转换](data/intro.md)