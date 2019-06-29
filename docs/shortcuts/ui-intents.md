# 显示 JSBox 界面

你可以在 Siri 界面显示由 JSBox 脚本编写的界面，这种形式无需通过 `$intents.finish()` 结束运行，更确切地说这种模式运行的脚本，就是普通的带界面的 JSBox 脚本，你只需要在脚本设置里面将其添加到 Siri 或捷径应用即可。

例如：

```js
$ui.render({
  views: [
    {
      type: "label",
      props: {
        text: "Hey, Siri!"
      },
      layout: function(make, view) {
        make.center.equalTo(view.super);
      }
    }
  ]
});
```

这个代码可以在 Siri 界面显示一个文字：`Hey, Siri!`。

# 设置参数

在 iOS 13 的捷径应用上，你可以为 JSBox 的捷径模块指定两个参数：`脚本名`和`输入参数`。

输入参数在捷径应用中显示类型为字符串类型，但请填写一个捷径中的字典类型，JSBox 在获取到之后会解析成一个 JSON 数据，你可以通过 `$context.query` 获取：

```js
const query = $context.query;
```