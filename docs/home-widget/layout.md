# 布局

前文我们已经提到过，小组件的布局方式和 `$ui.render` 完全不一样，在阅读 JSBox 相关实现之前，推荐对 SwiftUI 的 layout 系统有个基本了解：

- [View Layout and Presentation](https://developer.apple.com/documentation/swiftui/view-layout-and-presentation)
- [SwiftUI Layout System](https://kean.blog/post/swiftui-layout-system)

简单来说，相比 UIKit 我们对每个视图指定 auto layout 约束的方式，在小组件里面，我们通过 `hstack`, `vstack`, `zstack` 等结构来实现对其子视图的布局。

# type: "hstack"

实现一个横向布局空间，例如：

```js
$widget.setTimeline(ctx => {
  return {
    type: "hstack",
    props: {
      alignment: $widget.verticalAlignment.center,
      spacing: 20
    },
    views: [
      {
        type: "text",
        props: {
          text: "Hello"
        }
      },
      {
        type: "text",
        props: {
          text: "World"
        }
      }
    ]
  }
});
```

其中 `spacing` 指定了控件间的间距，`alignment` 使用 [$widget.verticalAlignment](home-widget/method?id=widgetverticalalignment) 来指定控件的纵向对齐方式。

# type: "vstack"

实现一个纵向布局空间，例如：

```js
$widget.setTimeline(ctx => {
  return {
    type: "vstack",
    props: {
      alignment: $widget.horizontalAlignment.center,
      spacing: 20
    },
    views: [
      {
        type: "text",
        props: {
          text: "Hello"
        }
      },
      {
        type: "text",
        props: {
          text: "World"
        }
      }
    ]
  }
});
```

其中 `spacing` 指定了控件间的间距，`alignment` 使用 [$widget.horizontalAlignment](home-widget/method?id=widgethorizontalalignment) 来指定控件的横向对齐方式。

# type: "zstack"

实现一个层叠布局空间，例如：

```js
$widget.setTimeline(ctx => {
  return {
    type: "zstack",
    props: {
      alignment: $widget.alignment.center
    },
    views: [
      $color("red"),
      {
        type: "text",
        props: {
          text: "Hello, World!"
        }
      }
    ]
  }
});
```

其中 `alignment` 使用 [$widget.alignment](home-widget/method?id=widgetalignment) 来指定控件的对齐方式。

# type: "spacer"

为布局空间增加间距，例如：

```js
$widget.setTimeline(ctx => {
  return {
    type: "hstack",
    views: [
      {
        type: "text",
        props: {
          text: "Hello"
        }
      },
      {
        type: "spacer",
        props: {
          // minLength: 10
        }
      },
      {
        type: "text",
        props: {
          text: "World"
        }
      }
    ]
  }
});
```

这会把两个文本控件挤到布局空间的两侧，`minLength` 表示 spacer 最短的长度。

# type: "hgrid"

实现一个横向的网格空间，例如：

```js
$widget.setTimeline(ctx => {
  return {
    type: "hgrid",
    props: {
      rows: Array(4).fill({
        flexible: {
          minimum: 10,
          maximum: Infinity
        },
        // spacing: 10,
        // alignment: $widget.alignment.left
      })
    },
    views: Array(8).fill({
      type: "text",
      props: {
        text: "Item"
      }
    })
  }
});
```

上述代码创建了一个 4 行 2 列的横向网格，内容都显示成 `Item`，项目大小可以使用：

```js
{
  fixed: 10
}
```

参考：https://developer.apple.com/documentation/swiftui/griditem/size-swift.enum

```js
{
  flexible: {
    minimum: 10,
    maximum: Infinity
  }
}
```

参考：https://developer.apple.com/documentation/swiftui/griditem/size-swift.enum

```js
{
  adaptive: {
    minimum: 10,
    maximum: Infinity
  }
}
```

参考：https://developer.apple.com/documentation/swiftui/griditem/size-swift.enum

# type: "vgrid"

实现一个纵向的网格空间，例如：

```js
$widget.setTimeline(ctx => {
  return {
    type: "vgrid",
    props: {
      columns: Array(4).fill({
        flexible: {
          minimum: 10,
          maximum: Infinity
        },
        // spacing: 10,
        // alignment: $widget.alignment.left
      })
    },
    views: Array(8).fill({
      type: "text",
      props: {
        text: "Item"
      }
    })
  }
});
```

上述代码创建了一个 2 行 4 列的纵向网格，内容都显示成 `Item`，参数含义与 `hgrid` 一致。