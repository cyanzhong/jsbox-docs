# type: "gradient"

用于创建一个渐变图层：

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

这个控件的实现与 iOS 的 CAGradientLayer 完全一致，请参考：https://developer.apple.com/documentation/quartzcore/cagradientlayer

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
colors | array | 读写 | 颜色
locations | array | 读写 | 控制点
startPoint | $point | 读写 | 起始点
endPoint | $point | 读写 | 终止点