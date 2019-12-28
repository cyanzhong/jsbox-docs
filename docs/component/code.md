# type: "code"

用于对代码进行高亮，以及简单的编辑，支持常见的几十种编程语言以及主题：

```js
$ui.render({
  views: [
    {
      type: "code",
      props: {
        text: "const value = 100"
      },
      layout: $layout.fill
    }
  ]
});
```

可以通过下面这些参数来配置代码编辑视图：

属性 | 类型 | 默认值 | 说明
---|---|---|---
language | string | javascript | 编程语言类型
theme | string | nord | 编辑器主题
darkKeyboard | bool | true | 是否使用黑色键盘
adjustInsets | bool | true | 是否根据键盘调整 insets
lineNumbers | bool | false | 是否显示行号
invisibles | bool | false | 是否显示不可见字符
linePadding | number | null | 自定义行高
keys | [string] | null | 自定义键盘工具栏

请注意，这些参数必须在初始化视图时确定，不能通过动态设置的方式覆盖。

与此同时，此组件继承自 Text View，所以 [`type: text`](component/text.md) 支持的功能它都支持。

例如，你可以通过 `editable: false` 来将视图设置为只读，不可编辑。可以通过 `text` 属性来读写代码内容：

```js
const view = $("codeView");
const code = view.text;
view.text = "console.log([1, 2, 3])";
```

当然，也支持全部 text 组件支持的事件：

```js
$ui.render({
  views: [
    {
      type: "code",
      props: {
        text: "const value = 100"
      },
      layout: $layout.fill,
      events: {
        changed: sender => {
          console.log("code changed");
        }
      }
    }
  ]
});
```

# props: language

`code` 组件的实现基于开源项目 [highlightjs](https://highlightjs.org/)，支持的编程语言名字列表可以在这里找到：https://github.com/highlightjs/highlight.js/tree/master/src/languages

例如需要对 Python 进行高亮：

```js
props: {
  language: "python"
}
```

# props: theme

`code` 组件的实现基于开源项目 [highlightjs](https://highlightjs.org/)，支持的主题列表可以在这里找到：https://github.com/highlightjs/highlight.js/tree/master/src/styles

例如需要使用 `atom-one-light` 主题：

```js
props: {
  theme: "atom-one-light"
}
```

# props: adjustInsets

在很多时候，我们需要处理键盘遮挡输入区域的问题，比如全屏的编辑页面。`code` 组件自动为你处理了这件事情，它会根据键盘的高度自动调整自己的 insets，以避免输入区域被遮挡。

自动实现的逻辑很难做到完美，当你不需要这个功能，可以通过 `adjustInsets: false` 关闭。

# props: keys

代码视图默认提供一个键盘工具栏，如果需要根据不同的编程语言自定义，可以这样：

```js
$ui.render({
  views: [
    {
      type: "code",
      props: {
        language: "markdown",
        keys: [
          "#",
          "-",
          "*",
          "`",
          //...
        ]
      },
      layout: $layout.fill
    }
  ]
});
```

如果想要完全去除自定义工具栏，可以通过覆盖 text view 的 `accessoryView` 实现。