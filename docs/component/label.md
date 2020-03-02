# type: "label"

`label` 用于显示一段不可编辑的文字，是最常用的控件之一：

```js
{
  type: "label",
  props: {
    text: "Hello, World!",
    align: $align.center
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
  }
}
```

在画布中显示一个 `Hello, World!`。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
text | string | 读写 | 文字内容
styledText | object | 读写 | 带格式的文本，[参考](component/text.md?id=styledtext)
font | $font | 读写 | 字体
textColor | $color | 读写 | 文字颜色
shadowColor | $color | 读写 | 阴影颜色
align | $align | 读写 | 对齐方式
lines | number | 读写 | 显示行数（0 表示任意多行）
autoFontSize | boolean | 读写 | 是否动态调整字体大小