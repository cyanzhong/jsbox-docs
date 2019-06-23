# type: "switch"

`switch` 用于创建一个开关：

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

将会创建一个初始状态是开启的开关。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
on | boolean | 读写 | 开关状态
onColor | $color | 读写 | 开启时颜色
thumbColor | $color | 读写 | 滑块颜色

# events: changed

`changed` 事件在状态变化时回调：

```js
changed: function(sender) {
  
}
```