# Properties

The properties of a widget specify its display effects and behavior, some properties support all types of views, and some properties are unique to text or images.

You can set multiple properties inside `props`, something like this:

```js
props: {
  frame: {
    width: 100,
    height: 100
  },
  background: $color("red"),
  padding: 15
}
```

Note that this simplification differs from SwiftUI's native [View Modifier](https://developer.apple.com/documentation/swiftui/viewmodifier):

- The same property can only be applied once.
- Unable to specify the order in which properties are applied

The way SwiftUI modifiers work dictates that different sequences produce different results, and each modifier produces a new view, so you can apply the same type of modifier over and over again.

When you need to fully mimic the logic in SwiftUI, you can use the `modifiers` array.

```js
modifiers: [
  {
    frame: { width: 100, height: 100 },
    background: $color("red")
  },
  { padding: 15 }
]
```

In the above code, the order of `frame` and `background` is undefined, but `padding` will be applied later.

The syntax is exactly the same as in `props` and the following examples will not be repeated.

# Properties for All Views

## props: frame

Specify the size and alignment of the view to:

```js
props: {
  frame: {
    width: 100,
    height: 100,
    alignment: $widget.alignment.center
  }
}
```

It can be more flexible:

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

The appropriate layout is inferred automatically, using `maxWidth: Infinity` and `maxHeight: Infinity` when the view is needed to fill the parent view.

## props: position

Specify the position of the view:

```js
props: {
  position: $point(0, 0) // {"x": 0, "y": 0}
}
```

## props: offset

Specifies the view's position offset:

```js
props: {
  offset: $point(-10, -10) // {"x": -10, "y": -10}
}
```

## props: padding

Specify the padding of the view:

```js
props: {
  padding: 10
}
```

This will give it a padding of 10 in all edges, or you can specify each edge separately:

```js
props: {
  padding: $insets(10, 0, 10, 0) // {"top": 10, "left": 0, "bottom": 10, "right": 0}
}
```

## props: layoutPriority

Sets the priority by which a parent layout should apportion space to this child (default: 0):

```js
props: {
  layoutPriority: 1
}
```

## props: cornerRadius

Apply corner radius:

```js
props: {
  cornerRadius: 10
}
```

When smooth corners are needed:

```js
props: {
  cornerRadius: {
    value: 10,
    style: 1 // 0: circular, 1: continuous
  }
}
```

## props: border

Create a border:

```js
props: {
  border: {
    color: $color("red"),
    width: 2
  }
}
```

## props: clipped

Whether to clip any content that extends beyond the layout bounds of the shape:

```js
props: {
  clipped: true
}
```

You can also enable antialiasing with `antialiased`:

```js
props: {
  clipped: {
    antialiased: true
  }
}
```

## props: opacity

Change the opacity of the view:

```js
props: {
  opacity: 0.5
}
```

## props: blur

Apply a Gaussian blur:

```js
props: {
  blur: 10
}
```

## props: color

Set the foreground color, such as text color:

```js
props: {
  color: $color("red")
}
```

## props: background

Fill the background, it can be color, image, or gradient:

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

Specify the link that will open when the view is tapped (only for 2 * 4 and 4 * 4 layouts).

```js
props: {
  link: "jsbox://run?name="
}
```

Regardless of what this link fills in, iOS will first open the JSBox main app, but the task to be performed can be delegated to the main app using a URL scheme.

Also, you can also use a special URL scheme to run scripts directly:

```js
props: {
  link: "jsbox://run?script=alert%28%22hello%22%29"
}
```

It opens the JSBox main app, and runs the script specified by the `script` parameter.

## props: widgetURL

Similar to `link`, but `widgetURL` specifies the link that is opened when the entire widget is tapped.

```js
props: {
  widgetURL: "jsbox://run?script=alert%28%22hello%22%29"
}
```

2 * 2 layout only supports this type of interaction.

# Properties for Text Views

## props: bold

Use bold fonts:

```js
props: {
  bold: true
}
```

## props: font

Specify the font:

```js
props: {
  font: {
    name: "AmericanTypewriter",
    size: 20,
    // weight: "regular" (ultraLight, thin, light, regular, medium, semibold, bold, heavy, black)
    // monospaced: true
  }
}
```

It can also be a font created using `$font`:

```js
props: {
  font: $font("bold", 20)
}
```

## props: lineLimit

Limit the maximum number of lines:

```js
props: {
  lineLimit: 1
}
```

## props: minimumScaleFactor

iOS may reduce the font size when there is not enough text to display. This property specifies the minimum acceptable scale:

```js
props: {
  minimumScaleFactor: 0.5
}
```

If it cannot be displayed in full, the content will be truncated.

# Properties for Image Views

## props: resizable

Specifies whether the image can be scaled:

```js
props: {
  resizable: true
}
```

## props: scaledToFill

Similar to [$contentMode.scaleAspectFill](en/data/constant.md?id=contentmode), this property determines whether the image fills the parent view in a way that stretches and is cropped.

```js
props: {
  scaledToFill: true
}
```

## props: scaledToFit

Similar to [$contentMode.scaleAspectFit](en/data/constant.md?id=contentmode), this property determines whether the image is placed in the parent view in a way that stretches and holds the content.

```js
props: {
  scaledToFit: true
}
```

## props: accessibilityHidden

Whether to disable VoiceOver:

```js
props: {
  accessibilityHidden: false
}
```

## props: accessibilityLabel

Set VoiceOver label:

```js
props: {
  accessibilityLabel: "Hey"
}
```

## props: accessibilityHint

Set VoiceOver hint:

```js
props: {
  accessibilityHint: "Double tap to open"
}
```