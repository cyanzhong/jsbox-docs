# type: "slider"

`slider` is used to create a slide control:

```js
{
  type: "slider",
  props: {
    value: 0.5,
    max: 1.0,
    min: 0.0
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.width.equalTo(100)
  }
}
```

It creates a slider with range from 0.0 to 1.0, default is 0.5.

# props

Prop | Type | Read/Write | Description
---|---|---|---
value | number | rw | current value
min | number | rw | minimum value
max | number | rw | maximum value
continuous | boolean | rw | is continuous
minColor | $color | rw | color of left part
maxColor | $color | rw | color of right part
thumbColor | $color | rw | color of the knob

# events: changed

`changed` will be called once the value changed:

```js
changed: function(sender) {

}
```