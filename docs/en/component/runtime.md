# type: "runtime"

Initiate a view with Runtime APIs:

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

With this solution, you can mix native views and runtime views.