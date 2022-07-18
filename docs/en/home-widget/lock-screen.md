# Lock Screen Widgets (Beta)

In iOS 16 Beta, lock screen can also have widgets, and JSBox supports building them as well (currently in TestFlight).

## Building Lock Screen Widgets

Lock screen widgets are essentially just widgets that you're familiar with on your home screen, with two major differences.

### Vibrant Colors

In lock screen, widgets are rendered with vibrant colors instead of full colors.

You're encouraged to use full-alpha colors, such as white or black to build lock screen widgets. Translucent color will be mixed with the wallpaper and the result will not be readable.

### Smaller Sizes

There are three new sizes compared to widgets on home screen:

```js
const $widgetFamily = {
  // small, medium, large, xLarge
  accessoryCircular: 4,
  accessoryRectangular: 5,
  accessoryInline: 6,
}
```

- `accessoryCircular`: 1 * 1 circular
- `accessoryRectangular`: 1 * 2 rectangular
- `accessoryInline`: one line info right after the date

To detect the current running environment, check [here](en/home-widget/timeline.md?id=render).

## In-app Preview

The in-app preview built for widgets currently doesn't support lock screen widgets previewing, please stay tuned for upcoming updates.

## Example Scripts

Please check out this [GitHub repo](https://github.com/cyanzhong/jsbox-widgets) for reference.