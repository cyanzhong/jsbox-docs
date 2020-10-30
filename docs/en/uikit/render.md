> We use render and push to draw views on the screen

# $ui.render(object)

Here's how `$ui.render` works, create a page:

```js
$ui.render({
  props: {
    id: "label",
    title: "Hello, World!"
  },
  views: [
    {
      type: "label",
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.size.equalTo($size(100, 100))
      }
    }
  ]
})
```

Because root view is also a view, it supports `props` as well, and you can set the title of the root view.

Other props:

Prop | Type | Description
---|---|---
theme | string | theme: light/dark/auto
title | string | title
titleColor | $color | title color
barColor | $color | bar color
iconColor | $color | icon color
debugging | bool | shows view debugging tool
navBarHidden | bool | whether hide navigation bar
statusBarHidden | bool | whether hide status bar
statusBarStyle | number | 0 for black, 1 for white
formSheet | bool | whether present as form sheet (iPad only)
pageSheet | bool | whether present as page sheet (iOS 13)
homeIndicatorHidden | bool | whether hide home indicator for iPhone X series
clipsToSafeArea | bool | whether clips to safe area
keyCommands | array | external keyboard commands

Starting from v1.36.0, you can render a page with $ui.render("main.ux") which is generated from UI editor.

# $ui.push(object)

Create a page, everthing is exactly same as $ui.render, but it pushes a new root view above previous view.

That's how native view navigation works, you can use it to implement `detail views` logic.

Starting from v1.36.0, you can push a page with $ui.push("detail.ux") which is generated from UI editor.

# $(id)

Get a view with id:

```js
var label = $("label")
```

If id is not provided, will search with type.

If you provided multiple views with same type, you need to provide id for each view.

# Life Cycle

Currently, $ui.render and $ui.push support below life cycle callback:

```js
events: {
  appeared: function() {

  },
  disappeared: function() {

  },
  dealloc: function() {

  }
}
```

As you can imagine, these will be called when page is appeared, disappeared and removed.

# Shake event

You can detect shake event with:

```js
events: {
  shakeDetected: function() {

  }
}
```

# Support external keyboard

Define keys with `keyCommands`:

```js
$ui.render({
  props: {
    keyCommands: [
      {
        input: "I",
        modifiers: 1 << 20,
        title: "Discoverability Title",
        handler: () => {
          console.log("Command+I triggered.");
        }
      }
    ]
  }
});
```

modifiers is a mask, values could be:

Type | Value
---|---
Caps lock | 1 << 16
Shift | 1 << 17
Control | 1 << 18
Alternate | 1 << 19
Command | 1 << 20
NumericPad | 1 << 21

For instance, (1 << 20 | 1 << 17) stands for hold `Command` + `Shift`.