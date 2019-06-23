# type: "stepper"

`stepper` is used to create a control with `minus` and `plus` buttons:

```js
{
  type: "stepper",
  props: {
    max: 10,
    min: 1,
    value: 5
  },
  layout: function(make, view) {
    make.centerX.equalTo(view.super)
    make.top.equalTo(24)
  },
  events: {
    changed: function(sender) {

    }
  }
}
```

Create a stepper with range from 1 to 10, default value is 5.

> Usually we combine this control with a label to display its value.

# props

Prop | Type | Read/Write | Description
---|---|---|---
value | number | rw | current value
min | number | rw | minimum value
max | number | rw | maximum value
step | number | rw | step
autorepeat | boolean | rw | responds long press
continuous | boolean | rw | continuous

# events: changed

`changed` will be called once the value changed:

```js
changed: function(sender) {
  
}
```