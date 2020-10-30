# type: "markdown"

Render markdown contents, it's good way to display rich text:

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

Prop | Type | Read/Write | Description
---|---|---|---
webView | $view | r | webView
content | string | rw | content
scrollEnabled | bool | rw | is scroll enabled
style | string | rw | custom style sheet