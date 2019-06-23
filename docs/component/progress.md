# type: "progress"

`progress` 用于创建一个不可交互的进度条，例如用来指示下载进度：

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

创建一个初始值在 50% 的进度条。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
value | number | 读写 | 进度(0.0 ~ 1.0)
progressColor | $color | 读写 | 已走进度的颜色
trackColor | $color | 读写 | 进度条背景色