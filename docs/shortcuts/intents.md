# 运行 JSBox 脚本

在 Siri 或 Shortcuts 应用中运行 JSBox 脚本非常简单，你可以发送一个请求并将返回的结果（字符串）。

做到这一点你仅需要通过 `$intents.finish()` 接口，例如：

```js
var result = await $http.get("");

$intents.finish(result.data);
```

简单来说，代码可以进行异步操作，最后通过 `$intents.finish()` 告诉 Siri 运行结束即可。

当代码中没有显式调用 `$intents.finish()`，将会在运行完之后自动结束，也即不能进行异步操作。

# 设置视图的高度

在 Siri 或 Shortcuts 应用运行带界面的脚本时，默认高度为 320，你可以这样设置高度：

```js
$intents.height = 180;
```