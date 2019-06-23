# $browser.exec

用来提供一个基于 webView 的 js 环境，这样的话你可以使用一些 Web APIs：

```js
$browser.exec({
  script: function() {
    var parser = new DOMParser();
    var doc = parser.parseFromString("<a>hey</a>", "application/xml");
    // $notify("customEvent", {"key": "value"})
    return doc.children[0].innerHTML;
  },
  handler: function(result) {
    $ui.alert(result);
  },
  customEvent: function(message) {

  }
})
```

# 方便的简写

你可以通过 Promise 写成非常简洁的形式：

```js
var result = await $browser.exec("return 1 + 1;");
```

# 如何访问 native 环境的变量

你可以通过类似这样的方式动态创建：

```js
var name = "JSBox"
$browser.exec({
  script: `
  var parser = new DOMParser();
  var doc = parser.parseFromString("<a>hey ${name}</a>", "application/xml");
  return doc.children[0].innerHTML;`,
  handler: function(result) {
    $ui.alert(result);
  }
})
```

通过字符串拼接的方法，name 会被填充为 native 环境的 `var name`。

关于 `$notify` 的使用，可以参考 [web 组件](component/web.md?id=notifyevent-message)。