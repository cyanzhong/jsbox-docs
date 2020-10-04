# Handy Methods

We added some new methods and constants for home screen widgets to the `$widget` module for ease of use.

# $widget.setTimeline(object)

Provide a timeline:

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

Please refer to [timeline](en/home-widget/timeline.md) for details.

# $widget.inputValue

Return the parameter set for the current widget:

```js
const inputValue = $widget.inputValue;
```

# $widget.family

Return the layout of the current widget, 0 ~ 2 means small, medium and large respectively:

```js
const family = $widget.family;
// 0, 1, 2
```

# $widget.displaySize

Return the display size of the current widget:

```js
const size = $widget.displaySize;
// size.width, size.height
```

# $widget.isDarkMode

Check if the current widget is running in dark mode:

```js
const isDarkMode = $widget.isDarkMode;
```

# $widget.alignment

Return the `alignment` constants for layout:

```js
const alignment = $widget.alignment;
// center, leading, trailing, top, bottom
// topLeading, topTrailing, bottomLeading, bottomTrailing
```

# $widget.horizontalAlignment

Return the `horizontalAlignment` constants for layout:

```js
const horizontalAlignment = $widget.horizontalAlignment;
// leading, center, trailing
```

# $widget.verticalAlignment

Return the `verticalAlignment` constants for layout:

```js
const verticalAlignment = $widget.verticalAlignment;
// top, center, bottom
// firstTextBaseline, lastTextBaseline
```

# $widget.dateStyle

Return the `dateStyle` constants that is used when configure a `text` view using dates:

```js
const dateStyle = $widget.dateStyle;
// time, date, relative, offset, timer
```

# $env.widget

Check if it's running in a home screen widget environment:

```js
if ($app.env == $env.widget) {
  
}
```