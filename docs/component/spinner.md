# type: "spinner"

`spinner` 用于创建一个 loading view：

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

将会创建一个初始状态是开启的开关。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
loading | boolean | 读写 | 是否加载中
color | $color | 读写 | 颜色
style | number | 读写 | 0 ~ 2 表示样式

# start()

开始加载，等同于 `spinner.loading = true`。

# stop()

结束加载，等同于 `spinner.loading = false`。

# toggle()

切换状态，等同于 `spinner.loading = !spinner.loading`。