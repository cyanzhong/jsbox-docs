# 在捷径应用里运行 JavaScript

JSBox 还能为捷径应用增加运行 JavaScript 的功能，当你需要在捷径应用里面处理复杂的数据时，不如通过这个方案实现。

由于捷径应用并不支持第三方应用处理输入和输出数据，所以这套逻辑借助于剪贴板实现：

- 将 JavaScript 拷贝到剪贴板
- 执行 JSBox 提供的运行 JavaScript 动作
- 读取剪贴板中的结果

简单说，JSBox 执行动作的时候会读取剪贴板中的 JavaScript，执行之后把结果写回到剪贴板，进而完成了通过 JSBox 执行 JavaScript 的过程。

同样的，异步任务需要通过 $intents.finish 来告诉捷径应用已经执行完成：

```js
var a = "Hello";
var b = "World";
var result = [a, b].join(", ");

$intents.finish(result);
```

你可以通过安装这个 Shortcut 体验这个功能：[Run JavaScript](shortcuts://import-workflow?url=https://github.com/cyanzhong/xTeko/raw/master/extension-demos/scripting.shortcut&name=Run%20JavaScript)。