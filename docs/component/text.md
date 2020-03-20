# type: "text"

`text` 用于创建一个可多行编辑的文本框，目前不支持富文本（但支持 HTML)：

```js
{
  type: "text",
  props: {
    text: "Hello, World!\n\nThis is a demo for Text View in JSBox extension!\n\nCurrently we don't support attributed string in iOS.\n\nYou can try html! Looks pretty cool."
  },
  layout: $layout.fill
}
```

将会在画布上显示一大段话，并且可以编辑。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
type | $kbType | 读写 | 键盘类型
darkKeyboard | boolean | 读写 | 是否黑色键盘
text | string | 读写 | 文本内容
styledText | object | 读写 | 带格式的文本
html | string | 只写 | 通过 html 渲染富文本
font | $font | 读写 | 字体
textColor | $color | 读写 | 文本颜色
align | $align | 读写 | 对齐方式
placeholder | string | 读写 | placeholder
selectedRange | $range | 读写 | 选中区域
editable | boolean | 读写 | 是否可编辑
selectable | boolean | 读写 | 是否可选择
insets | $insets | 读写 | 边距

# focus()

获取焦点，弹出键盘。

# blur()

模糊焦点，收起键盘。

# events: didBeginEditing

`didBeginEditing` 在开始编辑后回调：

```js
didBeginEditing: function(sender) {

}
```

# events: didEndEditing

`didEndEditing` 在结束编辑后回调：

```js
didEndEditing: function(sender) {
  
}
```

# events: didChange

`didChange` 在内容变化时回调：

```js
didChange: function(sender) {

}
```

# events: didChangeSelection

`didChangeSelection` 在选择区域变化时回调：

```js
didChangeSelection: function(sender) {

}
```

同时，`text` 继承自 `scroll`，所以 scroll 支持的全部事件和属性 text 也一样支持。

# styledText

用于设置带格式的文本，使用 Markdown 语法，支持粗体、斜体和链接，支持格式的嵌套：

```js
const text = `**Bold** *Italic* or __Bold__ _Italic_

[Inline Link](https://docs.xteko.com) <https://docs.xteko.com>

_Nested **styles**_`

$ui.render({
  views: [
    {
      type: "text",
      props: {
        styledText: text
      },
      layout: $layout.fill
    }
  ]
});
```

这将使用默认的字体和颜色进行渲染，也可以进行自定义：

```js
$ui.render({
  views: [
    {
      type: "text",
      props: {
        styledText: {
          text: "",
          font: $font(15),
          color: $color("black")
        }
      },
      layout: $layout.fill
    }
  ]
});
```

若需表示 `*`, `_` 等特殊符号，请使用 `\\` 进行转义。

如果需要对格式进行更精细的控制，可以通过 `styles` 为文字的不同位置指定样式：

```js
const text = `
AmericanTypewriter Cochin-Italic

Text Color Background Color

Kern

Strikethrough Underline

Stroke

Link

Baseline Offset

Obliqueness
`;

const _range = keyword => {
  return $range(text.indexOf(keyword), keyword.length);
}

$ui.render({
  views: [
    {
      type: "text",
      props: {
        styledText: {
          text: text,
          font: $font(17),
          color: $color("black"),
          markdown: false, // whether to use markdown syntax
          styles: [
            {
              range: _range("AmericanTypewriter"),
              font: $font("AmericanTypewriter", 17)
            },
            {
              range: _range("Cochin-Italic"),
              font: $font("Cochin-Italic", 17)
            },
            {
              range: _range("Text Color"),
              color: $color("red")
            },
            {
              range: _range("Background Color"),
              color: $color("white"),
              bgcolor: $color("blue")
            },
            {
              range: _range("Kern"),
              kern: 10
            },
            {
              range: _range("Strikethrough"),
              strikethroughStyle: 2,
              strikethroughColor: $color("red")
            },
            {
              range: _range("Underline"),
              underlineStyle: 9,
              underlineColor: $color("green")
            },
            {
              range: _range("Stroke"),
              strokeWidth: 3,
              strokeColor: $color("black")
            },
            {
              range: _range("Link"),
              link: "https://xteko.com"
            },
            {
              range: _range("Baseline Offset"),
              baselineOffset: 10
            },
            {
              range: _range("Obliqueness"),
              obliqueness: 1
            }
          ]
        }
      },
      layout: $layout.fill
    }
  ]
});
```

属性 | 类型 | 说明
---|---|---
range | $range | 文字范围
font | $font | 字体
color | $color | 前景色
bgcolor | $color | 背景色
kern | number | 字距
strikethroughStyle | number | 删除线样式（0: 无 1: 细线 2: 细线 9: 双线）
strikethroughColor | $color | 删除线颜色
underlineStyle | number | 下划线样式（0: 无 1: 细线 2: 细线 9: 双线）
underlineColor | $color | 下划线颜色
strokeWidth | number | 描边宽度
strokeColor | $color | 描边颜色
link | string | 链接 URL
baselineOffset | number | 基线偏移
obliqueness | number | 字体倾斜

使用 `styles` 默认不使用 markdown 语法，也可以通过 `markdown: true` 开启。

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