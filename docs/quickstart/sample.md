> 以下内容是通过一些简单的样例展示 JSBox 的接口设计，可以对 JSBox 有个概括性的了解。

# Hello, World!

```js
// 弹出 alert
$ui.alert("Hello, World!")
```

```js
// 打印到控制台
console.info("Hello, World!")
```

# 获取并展示剪贴板内容

```js
$ui.preview({
  text: JSON.stringify($clipboard.items)
})
```

# 简单的 HTTP 请求

```js
$http.get({
  url: 'https://docs.xteko.com',
  handler: function(resp) {
    var data = resp.data
  }
})
```

# 创建一个按钮

```js
$ui.render({
  views: [
    {
      type: "button",
      props: {
        title: "Button"
      },
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.width.equalTo(64)
      },
      events: {
        tapped: function(sender) {
          $ui.toast("Tapped")
        }
      }
    }
  ]
})
```

以上几个例子可以简单的认识一下接口的基本设计，在之后的文档里面有更详尽的介绍。