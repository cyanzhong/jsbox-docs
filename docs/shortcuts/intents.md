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

# 设置参数

在 iOS 13 的捷径应用上，你可以为 JSBox 的捷径模块指定两个参数：`脚本名`和`输入参数`。

输入参数在捷径应用中显示类型为字符串类型，但请填写一个捷径中的字典类型，JSBox 在获取到之后会解析成一个 JSON 数据，你可以通过 `$context.query` 获取：

```js
const query = $context.query;
```

同时，`$intents.finish(result)` 会将 result 作为结果输出给下一个捷径动作。