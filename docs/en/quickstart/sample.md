> Introduce API design patterns with some simple examples, helps you have a general understanding

# Hello, World!

```js
// Show alert
$ui.alert("Hello, World!")
```

```js
// Log to console
console.info("Hello, World!")
```

# Preview Clipboard Text

```js
$ui.preview({
  text: JSON.stringify($clipboard.items)
})
```

# HTTP Request

```js
$http.get({
  url: 'https://docs.xteko.com',
  handler: function(resp) {
    var data = resp.data
  }
})
```

# Create a button

```js
$ui.render({
  views: [
    {
      type: "button",
      props: {
        title: "Button"
      },
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.width.equalTo(64)
      },
      events: {
        tapped: function(sender) {
          $ui.toast("Tapped")
        }
      }
    }
  ]
})
```

Just a simple tour, explanation is coming soon.