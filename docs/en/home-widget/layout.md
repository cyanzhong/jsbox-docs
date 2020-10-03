# Layout System

As we have already mentioned, the layout system of the widget is completely different from `$ui.render`, so before learning the JSBox implementation, it is recommended to have a basic understanding of SwiftUI's layout system.

- [View Layout and Presentation](https://developer.apple.com/documentation/swiftui/view-layout-and-presentation)
- [SwiftUI Layout System](https://kean.blog/post/swiftui-layout-system)

In short, compared to UIKit where we specify an auto layout constraint for each view, in the widget we implement the layout of its child views by using `hstack`, `vstack`, `zstack` and so on.

# type: "hstack"

Create a horizontal layout space, for example:

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

Where `spacing` specifies the spacing between views, and `alignment` uses [$widget.verticalAlignment](en/home-widget/method?id=widgetverticalalignment) to specify the vertical alignment of views.

# type: "vstack"

Create a vertical layout space, for example:

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

Where `spacing` specifies the spacing between views, and `alignment` uses [$widget.horizontalAlignment](en/home-widget/method?id=widgethorizontalalignment) to specify the horizontal alignment of views.

# type: "zstack"

Create a space that stacks its children, for example:

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

Where `alignment` uses [$widget.alignment](en/home-widget/method?id=widgetalignment) to specify the views's alignment.

# type: "spacer"

Add spacing to the layout space, for example:

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

This will squeeze the two text views to the sides of the layout space, and `minLength` is the minimum length of the spacer.

# type: "hgrid"

Create a horizontal grid layout, E.g.:

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

The above code creates a horizontal grid of 4 rows and 2 columns, the contents of which are displayed as `Item`, and the item size can be used as follows:

```js
{
  fixed: 10
}
```

Refer: https://developer.apple.com/documentation/swiftui/griditem/size-swift.enum/fixed(_:)

```js
{
  flexible: {
    minimum: 10,
    maximum: Infinity
  }
}
```

Refer: https://developer.apple.com/documentation/swiftui/griditem/size-swift.enum/flexible(minimum:maximum:)

```js
{
  adaptive: {
    minimum: 10,
    maximum: Infinity
  }
}
```

Refer: https://developer.apple.com/documentation/swiftui/griditem/size-swift.enum/adaptive(minimum:maximum:)

# type: "vgrid"

Create a vertical grid layout, E.g.:

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

The above code creates a 2-row, 4-column vertical grid that is displayed as `Item`, the parameters have the same meaning as `hgrid`.