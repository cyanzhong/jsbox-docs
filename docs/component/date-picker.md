# type: "date-picker"

`date-picker` 用于创建一个日期选择器：

```js
{
  type: "date-picker",
  layout: function(make) {
    make.left.top.right.equalTo(0)
  }
}
```

创建一个默认的日期选择器。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
date | object | 读写 | 当前值
min | object | 读写 | 最小值
max | object | 读写 | 最大值
mode | number | 读写 | [请参考](https://developer.apple.com/documentation/uikit/uidatepickermode)
interval | number | 读写 | 步长（分钟）

# events: changed

`changed` 事件在当前值变化时回调：

```js
changed: function(sender) {
  
}
```