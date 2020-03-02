# type: "input"

`input` 可以创建一个输入框，用于处理单行的文本输入：

```js
{
  type: "input",
  props: {
    type: $kbType.search,
    darkKeyboard: true,
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 32))
  }
}
```

在画布中显示一个搜索键盘，同时是黑色的主题。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
type | $kbType | 读写 | 类型
darkKeyboard | boolean | 读写 | 黑色主题
text | string | 读写 | 文本内容
styledText | object | 读写 | 带格式的文本，[参考](component/text.md?id=styledtext)
textColor | $color | 读写 | 文本颜色
font | $font | 读写 | 字体
align | $align | 读写 | 对齐方式
placeholder | string | 读写 | placeholder
clearsOnBeginEditing | boolean | 读写 | 开始时清除文本
autoFontSize | boolean | 读写 | 是否动态调整字体大小
editing | boolean | 只读 | 是否在编辑
secure | boolean | 读写 | 是否密码框

# focus()

获取焦点，弹出键盘。

# blur()

模糊焦点，收起键盘。

# events: changed

`changed` 事件可以在文本变化时回调：

```js
changed: function(sender) {

}
```

# events: returned

`returned` 事件在回车键按下时调用：

```js
returned: function(sender) {

}
```

# events: didBeginEditing

`didBeginEditing` 事件在开始编辑时调用：

```js
didBeginEditing: function(sender) {

}
```

# events: didEndEditing

`didEndEditing` 事件在结束编辑时调用：

```js
didEndEditing: function(sender) {
  
}
```

# 自定义键盘工具栏

通过这样的方式自定义键盘工具栏：

```js
$ui.render({
  views: [
    {
      type: "input",
      props: {
        accessoryView: {
          type: "view",
          props: {
            height: 44
          },
          views: [

          ]
        }
      }
    }
  ]
});
```

# 自定义键盘视图

通过这样的方式自定义键盘视图：

```js
$ui.render({
  views: [
    {
      type: "input",
      props: {
        keyboardView: {
          type: "view",
          props: {
            height: 267
          },
          views: [

          ]
        }
      }
    }
  ]
});
```

# $input.text(object)

文字输入也可以使用这个快捷方法，将会直接弹出键盘以供输入：

```js
$input.text({
  type: $kbType.number,
  placeholder: "Input a number",
  handler: function(text) {

  }
})
```

# $input.speech(object)

使用系统听写接口输入文字（语音转文字）：

```js
$input.speech({
  locale: "en-US", // 可选
  autoFinish: false, // 可选
  handler: function(text) {

  }
})
```