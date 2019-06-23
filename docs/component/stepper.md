# type: "stepper"

`stepper` 用于创建控制加减的控件：

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

创建一个取值范围 1 ~ 10，初始值是 5 的步进器。

> 步进器仅显示一个加减控件，你可以用 label 组件显示其数值。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
value | number | 读写 | 当前数值
min | number | 读写 | 最小值
max | number | 读写 | 最大值
step | number | 读写 | 步长
autorepeat | boolean | 读写 | 响应长按
continuous | boolean | 读写 | 连续响应事件

# events: changed

`changed` 事件在数值变化时回调：

```js
changed: function(sender) {
  
}
```