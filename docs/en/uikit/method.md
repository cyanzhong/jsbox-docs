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

> You can use `$ui.error("Error")` to show an error message.
> You can clear toast with $ui.clearToast();

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