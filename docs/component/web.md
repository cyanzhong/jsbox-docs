# type: "web"

`web` 用于创建一个简单的网页，在之后将会提供选项用于显示浏览器导航按钮：

```js
{
  type: "web",
  props: {
    url: "https://www.apple.com"
  },
  layout: $layout.fill
}
```

显示 Apple 首页。

# 加载本地文件

可以将 html, js 和 css 等文件都放在本地，然后用 html 属性加载：

```js
let html = $file.read("assets/index.html").string;
$ui.render({
  views: [
    {
      type: "web",
      props: {
        html: html
      },
      layout: $layout.fill
    }
  ]
});
```

```html
<html>
  <head>
    <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">
    <link rel="stylesheet" href="local://assets/index.css">
    <script src="local://assets/index.js"></script>
  </head>
  <body>
    <h1>Hey, there!</h1><img src="local://assets/icon.png">
  </body>
  <script>
    window.onload = () => {
      alert(sum(1, 1));
    }
  </script>
</html>
```

本地文件将会从安装包内寻找，同时也支持 `shared://` 和 `drive://` 等协议。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
title | string | 只读 | 网页标题
url | string | 只写 | 地址
toolbar | bool | 只写 | 显示工具栏
html | string | 只写 | html
text | string | 只写 | text
loading | boolean | 只读 | 是否在加载
progress | number | 只读 | 加载进度
canGoBack | boolean | 只读 | 是否可以后退
canGoForward | boolean | 只读 | 是否可以前进
ua | string | 只写 | UserAgent(iOS 9+)
scrollEnabled | bool | 读写 | 是否可以滚动
bounces | bool | 读写 | 是否滚动回弹
transparent | bool | 读写 | 是否背景透明
showsProgress | bool | 只写 | 是否显示进度条
inlineMedia | bool | 只写 | 是否允许 inline video
airPlay | bool | 只写 | 是否允许 AirPlay
pictureInPicture | bool | 只写 | 是否允许画中画
allowsNavigation | bool | 读写 | 是否允许滑动返回
allowsLinkPreview | bool | 读写 | 是否允许链接预览

# goBack()

后退。

# goForward()

前进。

# reload()

重新加载。

# reloadFromOrigin()

从初始的 URL 重新加载。

# stopLoading()

停止加载。

# eval(object)

运行一段 JavaScript：

```js
webView.eval({
  script: "var sum = 1 + 2",
  handler: function(result, error) {

  }
})
```

# exec(script)

与 `eval` 类似，但此函数为 async 函数：

```js
const {result, error} = await webView.exec("1 + 1");
```

# events: didClose

`didClose` 会在网页关闭时回调：

```js
didClose: function(sender) {

}
```

# events: decideNavigation

`decideNavigation` 可以决定是否加载网页，用于拦截某些请求：

```js
decideNavigation: function(sender, action) {
  if (action.requestURL === "https://apple.com") {
    return false
  }
  return true
}
```

# events: didStart

`didStart` 在网页开始加载时回调：

```js
didStart: function(sender, navigation) {

}
```

# events: didReceiveServerRedirect

`didReceiveServerRedirect` 在收到服务器重定向时回调：

```js
didReceiveServerRedirect: function(sender, navigation) {

}
```

# events: didFinish

`didFinish` 在网页成功加载时调用：

```js
didFinish: function(sender, navigation) {

}
```

# events: didFail

`didFail` 在网页加载失败时调用：

```js
didFail: function(sender, navigation, error) {

}
```

# events: didSendRequest

`didSendRequest` 在页面 JavaScript 发送了 XMLHttpRequest 时候调用：

```js
didSendRequest: function(request) {
  var method = request.method
  var url = request.url
  var header = request.header
  var body = request.body
}
```

# js 注入

web 组件通过向 WebView 注入 JavaScript 来控制页面的行为，只需在 `props` 里面定义：

```js
props: {
  script: function() {
    var images = document.getElementsByTagName("img")
    for (var i=0; i<images.length; ++i) {
      var element = images[i]
      element.onclick = function(event) {
        var source = event.target || event.srcElement
        $notify("share", {"url": source.getAttribute("data-original")})
        return false
      }
    }
  }
}
```

script 是一个 `function`，function 里面所有的代码会在网页加载完成之后执行。

或者 script 内容也可以是一个字符串字面量，可以通过 [Uglify](https://skalman.github.io/UglifyJS-online/) 和 [Escape](https://www.freeformatter.com/json-escape.html) 的方式转换成这样一个字符串：

```js
props: {
  script: "for(var images=document.getElementsByTagName(\"img\"),i=0;i<images.length;++i){var element=images[i];element.onclick=function(e){var t=e.target||e.srcElement;return $notify(\"share\",{url:t.getAttribute(\"data-original\")}),!1}}"
}
```

# $notify(event, message)

在 script 的内容里面，可以通过 `$notify` 方法来将事件传递到 `events` 里面去处理：

```js
props: {
  script: function() {
    $notify("customEvent", {"key": "value"})
  }
},
events: {
  customEvent: function(object) {
    // object = {"key": "value"}
  }
}
```

这样的话页面加载完成之后将会调用 `notify` 将事件传递到 `events` 里面的 `test` 事件，从而可以在这里进一步和 native 代码互通。

这套机制有一点点复杂，请参考下面这个完整的例子：

```js
$ui.render({
  props: {
    title: "斗图啦"
  },
  views: [
    {
      type: "button",
      props: {
        title: "搜索"
      },
      layout: function(make) {
        make.right.top.inset(10)
        make.size.equalTo($size(64, 32))
      },
      events: {
        tapped: function(sender) {
          search()
        }
      }
    },
    {
      type: "input",
      props: {
        placeholder: "输入关键字"
      },
      layout: function(make) {
        make.top.left.inset(10)
        make.right.equalTo($("button").left).offset(-10)
        make.height.equalTo($("button"))
      },
      events: {
        returned: function(sender) {
          search()
        }
      }
    },
    {
      type: "web",
      props: {
        script: "for(var images=document.getElementsByTagName(\"img\"),i=0;i<images.length;++i){var element=images[i];element.onclick=function(e){var t=e.target||e.srcElement;return $notify(\"share\",{url:t.getAttribute(\"data-original\")}),!1}}"
      },
      layout: function(make) {
        make.left.bottom.right.equalTo(0)
        make.top.equalTo($("input").bottom).offset(10)
      },
      events: {
        share: function(object) {
          $http.download({
            url: "http:" + object.url,
            handler: function(resp) {
              $share.universal(resp.data)
            }
          })
        }
      }
    }
  ]
})

function search() {
  var keyword = $("input").text
  var url = "https://www.doutula.com/search?keyword=" + encodeURIComponent(keyword)
  $("input").blur()
  $("web").url = url
}

$("input").focus()
```

# 注入 css

与注入 script 类似的，style 也可以注入：

```js
props: {
  style: ""
}
```

当然，你也可以通过 js 注入的方式执行实现上述效果。

# Native 调用 Web 组件

Native 代码可以通过 `notify(event, message)` 给 web 组件发送消息：

```js
var webView = $("webView");
webView.notify({
  "event": "foobar",
  "message": {"key": "value"}
});
```

这将可以实现 Native 调用网页上面的方法。