# type: "gradient"

Create a gradient layer:

```js
$ui.render({
  props: {
    bgcolor: $color("white")
  },
  views: [
    {
      type: "gradient",
      props: {
        colors: [$color("red"), $color("clear"), $color("blue")],
        locations: [0.0, 0.5, 1.0],
        startPoint: $point(0, 0),
        endPoint: $point(1, 1)
      },
      layout: function(make, view) {
        make.left.top.equalTo(0)
        make.size.equalTo($size(100, 100))
      }
    }
  ]
})
```

The design is exactly same as CAGradientLayer, for detail please refer to: https://developer.apple.com/documentation/quartzcore/cagradientlayer

# props

Prop | Type | Read/Write | Description
---|---|---|---
colors | array | rw | colors
locations | array | rw | locations
startPoint | $point | rw | start point
endPoint | $point | rw | end point