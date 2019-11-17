# type: "button"

`button` 可以创建一个按钮，用于处理用户的点击事件：

```js
{
  type: "button",
  props: {
    title: "Click"
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
  }
}
```

在画布中显示一个标题为 `Click` 的按钮。

类似 image 组件，button 也支持通过 src 属性来设置显示的图片。

另外 button 也支持显示 JSBox 自带的 icon，请参考 [$icon](data/method.md?id=iconcode-color-size)。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
title | string | 读写 | 标题
titleColor | $color | 读写 | 标题颜色
font | $font | 读写 | 字体
src | string | 读写 | 图片地址
source | object | 读写 | 图片加载信息
symbol | string | 读写 | SF symbols 名称
image | image | 读写 | 图片对象
icon | $icon | 只写 | 内置图标
type | $btnType | 只读 | 类型
contentEdgeInsets | $insets | 读写 | 内容边距
titleEdgeInsets | $insets | 读写 | 标题边距
imageEdgeInsets | $insets | 读写 | 图片边距

# props: source

从 v1.55.0 开始，可以通过 `source` 对图片进行更详细的设定，例如：

```js
source: {
  url: url,
  placeholder: image,
  header: {
    "key1": "value1",
    "key2": "value2",
  }
}
```

# events: tapped

尤其不要忘记的是，button 也支持 `tapped` 事件：

```js
events: {
  tapped: function(sender) {
    
  }
}
```