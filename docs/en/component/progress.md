# type: "progress"

`progress` is used to create a progress bar, for example show download progress:

```js
{
  type: "progress",
  props: {
    value: 0.5
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.width.equalTo(100)
  }
}
```

Create a progress bar, default value is 50%.

# props

Prop | Type | Read/Write | Description
---|---|---|---
value | number | rw | current value (0.0 ~ 1.0)
progressColor | $color | rw | color of the left part
trackColor | $color | rw | color of the right part