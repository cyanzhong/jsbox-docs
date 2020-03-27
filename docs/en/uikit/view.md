> Explain JSBox view system

# type: "view"

`view` is the base component of all views:

```js
$ui.render({
  views: [
    {
      type: "view",
      props: {
        bgcolor: $color("#FF0000")
      },
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.size.equalTo($size(100, 100))
      },
      events: {
        tapped: function(sender) {

        }
      }
    }
  ]
})
```

Render a red rectangle on the screen.

# props

Prop | Type | Read/Write | Description
---|---|---|---
theme | string | rw | light, dark, auto
alpha | number | rw | alpha
bgcolor | $color | rw | background color
cornerRadius | number | rw | corner radius
smoothCorners | boolean | rw | use continuous curve for corners
radius | number | w | corner radius (deprecated, use `cornerRadius`)
smoothRadius | number | w | smooth corner radius (deprecated, use `smoothCorners`)
frame | $rect | rw | frame
size | $size | rw | size
center | $point | rw | center
flex | string | rw | auto resizing flexible mask
userInteractionEnabled | boolean | rw | user interaction enable
multipleTouchEnabled | boolean | rw | multiple touch support
super | view | r | super view
prev | view | r | previous view
next | view | r | next view
window | view | r | window
views | array | r | subviews
clipsToBounds | boolean | rw | clip subviews
opaque | boolean | rw | opaque
hidden | boolean | rw | hidden
contentMode | $contentMode | rw | [Refer](https://developer.apple.com/documentation/uikit/uiview/1622619-contentmode)
tintColor | $color | rw | tint color
borderWidth | number | rw | border width
borderColor | $color | rw | border color
circular | bool | rw | whether a circular shape
animator | object | r | animator
snapshot | object | r | create snapshot
info | object | rw | bind extra info
accessibilityLabel | string | rw | accessibility label
accessibilityHint | string | rw | accessibility hint
accessibilityValue | string | rw | accessibility value

Note: you can't use `prev` or `next in layout functions, because the view hierarchy hasn't been generated.

# navButtons

Create custom navigation buttons:

```js
$ui.render({
  props: {
    navButtons: [
      {
        title: "Title",
        image: image, // Optional
        icon: "024", // Or you can use icon name
        symbol: "checkmark.seal", // SF symbols are supported
        handler: sender => {
          $ui.alert("Tapped!")
        }
      }
    ]
  }
})
```

You can create 2 buttons at most, on debug mode there will be only 1 button.

# titleView

Other than setting title with `title`, you can also change the title view with `titleView`:

```js
$ui.render({
  props: {
    titleView: {
      type: "tab",
      props: {
        bgcolor: $rgb(240, 240, 240),
        items: ["A", "B", "C"]
      },
      events: {
        changed: sender => {
          console.log(sender.index);
        }
      }
    }
  },
  views: [

  ]
});
```

# layout(function)

Trigger layout method manually, arguments are exactly the same as the `layout` function in its view definition:

```js
view.layout((make, view) => {
  make.left.top.right.equalTo(0);
  make.height.equalTo(100);
});
```

# updateLayout(function)

Update a view's layout:

```js
$("label").updateLayout(function(make) {
  make.size.equalTo($size(200, 200))
})
```

Note that, `updateLayout` can only be used for existing constraints, or it won't work.

# remakeLayout(function)

Similar to updateLayout, but remake costs more performance, try to use update as much as you can.

# add(object)

Add a view to another view's hierarchy, refer `$ui.render(object)` to see how to create a view, it can also be a view instance that is created with `$ui.create(...)`.

# get(id)

Get a subview with specific identifier.

# remove()

Remove a view from its super view's hierarchy.

# insertBelow(view, other)

Insert a new view below an existing view:

```js
view.insertBelow(newView, existingView);
```

# insertAbove(view, other)

Insert a new view above an existing view:

```js
view.insertAbove(newView, existingView);
```

# insertAtIndex(view, index)

Insert a new view at a specific index:

```js
view.insertAtIndex(newView, 4);
```

# moveToFront()

Move self to super's front:

```js
existingView.moveToFront();
```

# moveToBack()

Move self to super's back:

```js
existingView.moveToBack();
```

# relayout()

Trigger layouting of a view, you can use this during animations.

# setNeedsLayout()

Mark a view as needs layout, it will be applied in the next drawing cycle.

# layoutIfNeeded()

Forces layout early before next drawing cycle, can be used with `setNeedsLayout`:

```js
view.setNeedsLayout();
view.layoutIfNeeded();
```

# sizeToFit()

Resize the view to its best size based on the current bounds.

# scale(number)

Scale a view (0.0 ~ 1.0):

```js
view.scale(0.5)
```

# snapshotWithScale(scale)

Create snapshot with scale:

```js
const image = view.snapshotWithScale(1)
```

# rotate(number)

Rotate a view:

```js
view.rotate(Math.PI)
```

# events: ready

`ready` event is supported for all views, it will be called when view is ready:

```js
ready: function(sender) {
  
}
```

# events: tapped

Observe tap gesture:

```js
tapped: function(sender) {

}
```

The sender is the source of event, usually means the view itself.

You can also use this syntax:

```js
tapped(sender) {

}
```

This has same effect.

# events: pencilTapped

Detect tap events from Apple Pencil:

```js
pencilTapped: function(info) {
  var action = info.action; // 0: Ignore, 1: Switch Eraser, 2: Switch Previous, 3: Show Color Palette
  var enabled = info.enabled; // whether the system reports double taps on Apple Pencil to your app
}
```

# events: hoverEntered

For iPadOS 13.4 (and above) with trackpad, this is called when pointer enters the view:

```js
hoverEntered: sender => {
  sender.alpha = 0.5;
}
```

# events: hoverExited

For iPadOS 13.4 (and above) with trackpad, this is called when pointer exits the view:

```js
hoverExited: sender => {
  sender.alpha = 1.0;
}
```

# events: themeChanged

Detect [dark mode](en/uikit/dark-mode.md) changes:

```js
themeChanged: (sender, isDarkMode) => {
  
}
```

Refer [Component](en/component/label.md) to see how to use other controls.