# type: "scroll"

`scroll` is used to create a scrollable view container:

```js
{
  type: "scroll",
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 500))
  },
  views: [
    {

    },
    {

    }
  ]
}
```

This container can be scrolled, but we should specify its content size first.

# Content Size

The content size means the size of scroll area, it might be larger than its frame.

We have two ways to set scroll views' content size.

The first one, provide size for all subviews that inside a scroll view:

```js
$ui.render({
  views: [{
    type: "scroll",
    layout: $layout.fill,
    views: [{
      type: "label",
      props: {
        text: text,
        lines: 0
      },
      layout: function(make, view) {
        make.width.equalTo(view.super)
        make.top.left.inset(0)
        make.height.equalTo(1000)
      }
    }]
  }]
})
```

Or, we could just set the `contentSize` of a scroll view manually:

```js
props: {
  contentSize: $size(0, 1000)
}
```

Specify content size of a scroll view is very important, otherwise it works weird.

# props

Prop | Type | Read/Write | Description
---|---|---|---
contentOffset | $point | rw | content offset
contentSize | $size | rw | content size
alwaysBounceVertical | boolean | rw | always bounce vertical
alwaysBounceHorizontal | boolean | rw | always bounce horizontal
pagingEnabled | boolean | rw | is paging enabled
scrollEnabled | boolean | rw | is scroll enabled
showsHorizontalIndicator | boolean | rw | shows horizontal indicator 
showsVerticalIndicator | boolean | rw | shows vertical indicator
indicatorInsets | $insets | rw | indicator insets
tracking | boolean | r | is tracking
dragging | boolean | r | is dragging
decelerating | boolean | r | is decelerating
keyboardDismissMode | number | rw | keyboard dismiss mode
zoomEnabled | bool | rw | zoom images with 2-finger pinch
maxZoomScale | number | rw | max zoom scale for images
doubleTapToZoom | number | rw | enables double tap to zoom

# beginRefreshing()

Begin the refreshing animation.

# endRefreshing()

End the refreshing animation.

# resize()

Resize the content size of itself.

# scrollToOffset($point)

Scroll to an offset with animation:

```js
$("scroll").scrollToOffset($point(0, 100));
```

# events: pulled

`pulled` will be called once user triggered a refresh:

```js
pulled: function(sender) {
  
}
```

# events: didScroll

`didScroll` will be called while scrolling:

```js
didScroll: function(sender) {

}
```

# events: willBeginDragging

`willBeginDragging` will be called while dragging:

```js
willBeginDragging: function(sender) {
  
}
```

# events: willEndDragging

`willEndDragging` will be called before dragging ends:

```js
willEndDragging: function(sender, velocity) {

}
```

# events: didEndDragging

`didEndDragging` will be called after dragging ended:

```js
didEndDragging: function(sender, decelerate) {

}
```

# events: willBeginDecelerating

`willBeginDecelerating` will be called before decelerating:

```js
willBeginDecelerating: function(sender) {

}
```

# events: didEndDecelerating

`didEndDecelerating` will be called after decelerating ended:

```js
didEndDecelerating: function(sender) {

}
```

# events: didEndScrollingAnimation

`didEndScrollingAnimation` will be called after decelerating ended (program triggered):

```js
didEndScrollingAnimation: function(sender) {

}
```

# events: didScrollToTop

`didScrollToTop` will be called once it did reach top:

```js
didScrollToTop: function(sender) {

}
```

# Auto Layout

It is hard to make Auto Layout work for scrollViews, we suggest using `layoutSubviews` to work around some issues:

```js
const contentHeight = 1000;
$ui.render({
  views: [
    {
      type: "scroll",
      layout: $layout.fill,
      events: {
        layoutSubviews: sender => {
          $("container").frame = $rect(0, 0, sender.frame.width, contentHeight);
        }
      },
      views: [
        {
          type: "view",
          props: {
            id: "container"
          },
          views: [
            {
              type: "view",
              props: {
                bgcolor: $color("red")
              },
              layout: (make, view) => {
                make.left.top.right.equalTo(0);
                make.height.equalTo(300);
              }
            }
          ]
        }
      ]
    }
  ]
});
```

In short, instead of using Auto Layout for scrollView's subviews, we can add a container view to the scrollView, and set its frame with `layoutSubviews`, then subviews that belong to the container view can work with Auto Layout correctly. Learn more: https://developer.apple.com/library/archive/technotes/tn2154/_index.html