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