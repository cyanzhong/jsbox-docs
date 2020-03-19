# type: "markdown"

用来显示 Markdown 格式的文本，当你需要显示富文本内容时，除了使用 HTML 以外，Markdown 是一个不错的选择：

```js
$ui.render({
  views: [
    {
      type: "markdown",
      props: {
        content: "# Hello, *World!*",
        style: // optional, custom style sheet
        `
        body {
          background: #f0f0f0;
        }
        `
      },
      layout: $layout.fill
    }
  ]
})
```

属性 | 类型 | 读写 | 说明
---|---|---|---
webView | $view | r | webView
content | string | rw | 内容
scrollEnabled | bool | rw | 是否滚动
style | string | rw | 自定义样式