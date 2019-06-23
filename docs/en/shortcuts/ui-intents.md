# Present JSBox views

You can present views that provided by JSBox script on Siri, it looks no differences compare to other JSBox scripts that shows a view:

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

This code shows a `Hey, Siri!` on Siri's view (You can add it to Siri/Shortcuts in script's setting view).