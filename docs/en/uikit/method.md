> In the UI system of JSBox, there are still something we need to talk

# $ui.pop()

Pop out the most front view from the stack.

# $ui.popToRoot()

Pop to the root view.

# $ui.get(id)

Get a view instance by id, same as `$(id)`.

> You can also get view by type, only if this type is distinct.

# $ui.alert(object)

Present an alert, usually used to show a message or options:

```js
$ui.alert({
  title: "Hello",
  message: "World",
  actions: [
    {
      title: "OK",
      disabled: false, // Optional
      handler: function() {

      }
    },
    {
      title: "Cancel",
      handler: function() {

      }
    }
  ]
})
```

You can create an alert with title, message and actions, if no `actions` is provided, a default `OK` will be shown.

`title` and `message` are optional, and the minimal implementation is:

```js
$ui.alert("Haha!")
```

Yes, you could simply provide a string, it will work also.

# $ui.action(object)

Present an action sheet, all parameters are same as `$ui.alert`.

PS: This control can only be used in main application, don't use it in app extensions.

# $ui.menu(object)

Present a menu, it can be used to provide a series of options:

```js
$ui.menu({
  items: ["A", "B", "C"],
  handler: function(title, idx) {

  },
  finished: function(cancelled) {
    
  }
})
```

# $ui.popover(object)

Present a popover, provides two different styles.

Style 1, it can be filled with some simple options (string array):

```js
const {index, title} = await $ui.popover({
  sourceView: sender,
  sourceRect: sender.bounds, // default
  directions: $popoverDirection.up, // default
  size: $size(320, 200), // fits content by default
  items: ["Option A", "Option B"],
  dismissed: () => {},
});
```

In this way, fill options with `items` property, it returns a Promise.

Style 2, it can be filled with custom `views`:

```js
const popover = $ui.popover({
  sourceView: sender,
  sourceRect: sender.bounds, // default
  directions: $popoverDirection.any, // default
  size: $size(320, 200), // fits screen width by default
  views: [
    {
      type: "button",
      props: {
        title: "Button"
      },
      layout: (make, view) => {
        make.center.equalTo(view.super);
        make.size.equalTo($size(100, 36));
      },
      events: {
        tapped: () => {
          popover.dismiss();
        }
      }
    }
  ]
});
```

Create custom UI with `views` property, returns the popover itself, you can close it by calling its `dismiss` method.

The `sourceView` and `sourceRect` specifies where to present the popover, and `sourceRect` default to sourceView.bounds, `directions` defines the permitted arrow directions.

Please refer to the demo project we provided for more information: https://gist.github.com/cyanzhong/313b2c8d138691233658f1b8a52f02c6

# $ui.toast(message)

Show a toast message at top of the root view.

```js
$ui.toast("Hey!")
```

There is an optional parameter to set the stay seconds:

```js
$ui.toast("Hey!", 10)
```

This toast will be dismissed after 10 seconds.

> You can clear toast with $ui.clearToast();

# $ui.success(string)

Similar to `toast`, but the bar color is green, indicates success:

```js
$ui.success("Done");
```

# $ui.warning(string)

Similar to `toast`, but the bar color is yellow, indicates warning:

```js
$ui.warning("Be careful!");
```

# $ui.error(string)

Similar to `toast`, but the bar color is red, indicates error:

```js
$ui.error("Something went wrong!");
```

# $ui.loading(boolean)

Show a loading indicator:

```js
$ui.loading(true)
```

You can also display a message here:

```js
$ui.loading("Loading...")
```

# $ui.progress(number)

Display a progress bar, the range of number is [0, 1]:

```js
$ui.progress(0.5)
```

Also, an optional message is supported:

```js
$ui.progress(0.5, "Downloading...")
```

# $ui.preview(object)

Preview a url quickly:

```js
$ui.preview({
  title: "URL",
  url: "https://images.apple.com/v/ios/what-is/b/images/performance_large.jpg"
})
```

Param | Type | Description
---|---|---
title | string | title
url | string | url
html | string | html content
text | string | text content

# $ui.create(object)

Create a view manually, the object should be a view like $ui.render:

```js
var canvas = $ui.create({
  type: "image",
  props: {
    bgcolor: $color("clear"),
    tintColor: $color("gray"),
    frame: $rect(0, 0, 100, 100)
  }
})
```

Note that, since there's no super view yet, you cannot use `layout` method at that moment.

Instead, you should do it after the view is added to its super:

```js
const subview = $ui.create(...);
superview.add(subview);
subview.layout((make, view) => {

});
```

# $ui.window

Get current window of $ui.render.

# $ui.controller

Get the most front view controller of the app.

# $ui.title

Get or set the most front view's title.

# $ui.selectIcon()

Select icon:

```js
var icon = await $ui.selectIcon();
```