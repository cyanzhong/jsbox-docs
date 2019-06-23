# type: "switch"

`switch` is used to create an on/off control:

```js
{
  type: "switch",
  props: {
    on: true
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
  }
}
```

It creates a switch, default is on.

# props

Prop | Type | Read/Write | Description
---|---|---|---
on | boolean | rw | on/off state
onColor | $color | rw | color of on state
thumbColor | $color | rw | color of off state

# events: changed

`changed` will be called after the state changed:

```js
changed: function(sender) {
  
}
```