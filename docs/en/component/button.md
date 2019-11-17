# type: "button"

`button` is designed to create a button to handle tap action:

```js
{
  type: "button",
  props: {
    title: "Click"
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
  }
}
```

It shows a `Click` button.

Similar to image view, it supports configure the image content with a `src`.

In addition, button also supports JSBox icon set, [refer](en/data/method.md?id=iconcode-color-size).

# props

Prop | Type | Read/Write | Description
---|---|---|---
title | string | rw | title
titleColor | $color | rw | title color
font | $font | rw | font
src | string | rw | image url
source | object | rw | image loading info
symbol | string | rw | SF symbols id
image | image | rw | icon image
icon | $icon | w | builtin icon
type | $btnType | r | button type
contentEdgeInsets | $insets | rw | content edge insets
titleEdgeInsets | $insets | rw | title edge insets
imageEdgeInsets | $insets | rw | image edge insets

# props: source

After v1.55.0, the image can be specified with `source` for more detailed information:

```js
source: {
  url: url,
  placeholder: image,
  header: {
    "key1": "value1",
    "key2": "value2",
  }
}
```

# events: tapped

To support tap event on buttons, implement `tapped`:

```js
events: {
  tapped: function(sender) {
    
  }
}
```