# View

Compared to the `$ui.render` function, which supports a rich set of views, the widget supports a very limited set of view types.

Also, `$ui.render` is based on the UIKit, while `$widget.setTimeline` is based on the SwiftUI. Even though we designed a similar syntax for the widget, the differences between the two UI technologies meant that prior knowledge could not be completely transferred.

# Syntax

For any kind of view, we define it using the following syntax:

```js
{
  type: "",
  props: {}, // or modifiers: []
  views: []
}
```

This is similar to `$ui.render` in that `type` specifies the type, `props` or `modifiers` specifies the properties, and `views` specifies its child views.

The difference is that in SwiftUI we no longer use a UIKit-like layout system, so we don't use `layout` anymore.

We will cover the layout system later, let's get started by introducing some visible views.

# type: "text"

This view is used to display a piece of non-editable text, similar to the `type: "label"` in `$ui.render`, and can be constructed as following ways:

```js
{
  type: "text",
  props: {
    text: "Hey"
  }
}
```

This method displays a piece of text directly using the `text` property.

```js
{
  type: "text",
  props: {
    date: new Date(),
    style: $widget.dateStyle.time
  }
}
```

This method uses `date` and `style` to display a time or date, style can be referred to [$widget.dateStyle](en/home-widget/method.md?id=widgetdatestyle)。

```js
{
  type: "text",
  props: {
    startDate: startDate,
    endDate: endDate
  }
}
```

The method uses `startDate` and `endDate` to display a time interval.

Properties supported by the text view: [bold](en/home-widget/modifiers.md?id=props-bold), [font](en/home-widget/modifiers.md?id=props-font), [lineLimit](en/home-widget/modifiers.md?id=props-linelimit), [minimumScaleFactor](en/home-widget/modifiers.md?id=props-minimumscalefactor)。

# type: "image"

Display an image, like the `type: image` in `$ui.render`, and can be constructed in the following ways:

```js
{
  type: "image",
  props: {
    image: $image("assets/icon.png"),
    // data: $file.read("assets/icon.png")
  }
}
```

This method uses JSBox's existing APIs to provide `image` or `data` objects.

```js
{
  type: "image",
  props: {
    symbol: "trash"
  }
}
```

This method uses [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/sf-symbols/) to display an icon.

```js
{
  type: "image",
  props: {
    path: "assets/icon.png"
  }
}
```

This method uses the file path directly to set the image content.

```js
{
  type: "image",
  props: {
    uri: "https://..."
  }
}
```

This method can use either an online image address, or an image string in base64 format.

Properties supported by the image view: [resizable](en/home-widget/modifiers.md?id=props-resizable), [scaledToFill](en/home-widget/modifiers.md?id=props-scaledtofill), [scaledToFit](en/home-widget/modifiers.md?id=props-scaledtofit), [accessibilityHidden](en/home-widget/modifiers.md?id=props-accessibilityhidden), [accessibilityLabel](en/home-widget/modifiers.md?id=props-accessibilitylabel), [accessibilityHint](en/home-widget/modifiers.md?id=props-accessibilityhint)。

# type: "color"

In home screen widgets, a color can be a view, or a property of other views, it can be constructed in the following ways:

```js
{
  type: "color",
  props: {
    color: "#00EEEE"
  }
}
```

This methods creates a color using hex value.

```js
{
  type: "color",
  props: {
    light: "#00EEEE",
    dark: "#EE00EE"
  }
}
```

This methods provides both colors for `light` mode and `dark` mode.

```js
{
  type: "color",
  props: {
    color: $color("red")
  }
}
```

This methods uses the existing `$color` function provided by JSBox.

# type: "gradient"

Create a linear gradient effect, E.g.:

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

Use `startPoint` and `endPoint` to specify the start and end points, and `colors` and `locations` to determine the color and position of each gradient section. Note: if `locations` is specified, it must be equal in number to `colors`.

# type: "divider"

Create a divider, E.g.:

```js
{
  type: "divider",
  props: {
    background: $color("blue")
  }
}
```