# Handy Methods

We added some new methods and constants for home screen widgets to the `$widget` module for ease of use.

# $widget.setTimeline(object)

Provide a timeline:

```js
$widget.setTimeline({
  entries: [
    {
      date: new Date(),
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

Please refer to [timeline](en/home-widget/timeline.md) for details.

# $widget.reloadTimeline()

Trigger timeline refresh manually, the system can decide whether to refresh or not:

```js
$widget.reloadTimeline();
```

# $widget.inputValue

Return the parameter set for the current widget:

```js
const inputValue = $widget.inputValue;
```

> `inputValue` is undefined when the main app is running, use a mock value for testing purposes

# $widget.family

Return the layout of the current widget, 0 ~ 3 means small, medium, large, and extra large (iPadOS 15) respectively:

```js
const family = $widget.family;
// 0, 1, 2, 3
```

In most cases, you should rely on the `ctx` returned in the `render` function to retrieve `family`. Use this API only if you need to get it before calling `setTimeline`.

By default, this value is 0 when the main app is running, and can be overridden by the test code:

```js
$widget.family = $widgetFamily.medium;
```

# $widget.displaySize

Return the display size of the current widget:

```js
const size = $widget.displaySize;
// size.width, size.height
```

In most cases, you should rely on the `ctx` returned in the `render` function to retrieve `displaySize`. Use this API only if you need to get it before calling `setTimeline`.

By default, this value refers to small size when the main app is running, and can be tweaked by modifying the family:

```js
$widget.family = $widgetFamily.medium;
```

# $widget.isDarkMode

Check if the current widget is running in dark mode:

```js
const isDarkMode = $widget.isDarkMode;
```

In most cases, you should rely on the `ctx` returned in the `render` function to retrieve `isDarkMode`. Use this API only if you need to get it before calling `setTimeline`.

# $widget.alignment

Return the `alignment` constants for layout:

```js
const alignment = $widget.alignment;
// center, leading, trailing, top, bottom
// topLeading, topTrailing, bottomLeading, bottomTrailing
```

You can also use string literals, such as "center", "leading"...

# $widget.horizontalAlignment

Return the `horizontalAlignment` constants for layout:

```js
const horizontalAlignment = $widget.horizontalAlignment;
// leading, center, trailing
```

You can also use string literals, such as "leading", "center"...

# $widget.verticalAlignment

Return the `verticalAlignment` constants for layout:

```js
const verticalAlignment = $widget.verticalAlignment;
// top, center, bottom
// firstTextBaseline, lastTextBaseline
```

You can also use string literals, such as "top", "center"...

# $widget.dateStyle

Return the `dateStyle` constants that is used when configure a `text` view using dates:

```js
const dateStyle = $widget.dateStyle;
// time, date, relative, offset, timer
```

You can also use string literals, such as "time", "date"...

# $env.widget

Check if it's running in a home screen widget environment:

```js
if ($app.env == $env.widget) {
  
}
```