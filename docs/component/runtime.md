# type: "runtime"

可以使用 Runtime 来初始化一个 view:

```js
var label = $objc("UILabel").$new();
label.$setText("Hey!");

$ui.render({
  views: [
    {
      type: "runtime",
      props: {
        view: label
      },
      layout: function(make, view) {
        make.center.equalTo(view.super);
      }
    }
  ]
});
```

通过这种方式，你可以将 JSBox 提供的组件与 Runtime 生成的组件混合在一起。