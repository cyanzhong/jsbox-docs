# type: "slider"

`slider` 用于创建一个可拖动的进度选择器：

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

将会创建一个取值范围为 0.0 ~ 1.0 的选择器，初始值是 0.5。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
value | number | 读写 | 当前值
min | number | 读写 | 最小值
max | number | 读写 | 最大值
continuous | boolean | 读写 | 是否连续
minColor | $color | 读写 | 左边颜色
maxColor | $color | 读写 | 右边颜色
thumbColor | $color | 读写 | 滑块颜色

# events: changed

`changed` 事件在数值变化时回调：

```js
changed: function(sender) {

}
```