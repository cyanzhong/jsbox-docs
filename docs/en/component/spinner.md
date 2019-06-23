# type: "spinner"

`spinner` is designed to display a loading state:

```js
{
  type: "spinner",
  props: {
    loading: true
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
  }
}
```

You can switch the state by set `on` to true/false.

# props

Prop | Type | Read/Write | Description
---|---|---|---
loading | boolean | rw | loading state
color | $color | rw | color
style | number | rw | 0 ~ 2 for styles

# start()

Equals to `spinner.loading = true`.

# stop()

Equals to `spinner.loading = false`.

# toggle()

Equals to `spinner.loading = !spinner.loading`.