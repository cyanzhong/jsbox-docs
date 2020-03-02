# Basic Concept

[Objective-C Runtime](https://developer.apple.com/documentation/objectivec/objective_c_runtime) is a powerful ability in iOS, it looks like reflection system in other languages, but it's more flexible.

Base on runtime we could do a lot:

- Invoke method dynamically
- Create class dynamically
- Create instance dynamically
- Replace existing method

Overall, runtime can do a lot, is the most important feature of Objective-C.

# Why we need runtime?

The main purpose is provide backup for defective APIs, so please don't use it in most cases.

You should consider runtime only if you have no better choice.

If a JSBox API is not strong enough, you can consider use Runtime APIs, but a better way would be send a feedback to us.

# Methods

- `$objc(className)` Get a class dynamically
- `invoke(methodName, arguments ...)` Call a method dynamically
- `$define(object)` Create a class
- `jsValue()` Convert an Objective-C value to JavaScript value
- `ocValue()` Convert a JavaScript value to Objective-C value
- `$objc_retain(object)` retain object
- `$objc_release(object)` release object

# Example

This example creates a button on screen, tap it to open WeChat:

```js
$define({
  type: "MyHelper",
  classEvents: {
    open: function(scheme) {
      var url = $objc("NSURL").invoke("URLWithString", scheme)
      $objc("UIApplication").invoke("sharedApplication.openURL", url)
    }
  }
})

$ui.render({
  views: [
    {
      type: "button",
      props: {
        bgcolor: $objc("UIColor").invoke("blackColor").jsValue(),
        titleColor: $color("#FFFFFF").ocValue().jsValue(),
        title: "WeChat"
      },
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.size.equalTo($size(100, 32))
      },
      events: {
        tapped: function(sender) {
          $objc("MyHelper").invoke("open", "weixin://")
        }
      }
    }
  ]
})

var window = $ui.window.ocValue()
var label = $objc("UILabel").invoke("alloc.init")
label.invoke("setTextAlignment", 1)
label.invoke("setText", "Runtime")
label.invoke("setFrame", { x: $device.info.screen.width * 0.5 - 50, y: 240, width: 100, height: 32 })
window.invoke("addSubview", label)
```

You can learn how to handle values from this example.

Here's a complicated example, it shows you how to create a game (2048) with Runtime: https://github.com/cyanzhong/xTeko/tree/master/extension-scripts/2048