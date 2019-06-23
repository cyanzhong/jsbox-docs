# type: "date-picker"

`date-picker` is designed to display a date picker:

```js
{
  type: "date-picker",
  layout: function(make) {
    make.left.top.right.equalTo(0)
  }
}
```

Create a simple date picker.

# props

Prop | Type | Read/Write | Description
---|---|---|---
date | object | rw | current date
min | object | rw | minimum date
max | object | rw | maximum date
mode | number | rw | [Refer](https://developer.apple.com/documentation/uikit/uidatepickermode)
interval | number | rw | step (in minute)

# events: changed

`changed` will be called if the date has changed:

```js
changed: function(sender) {
  
}
```