# 基本概念

[Objective-C Runtime](https://developer.apple.com/documentation/objectivec/objective_c_runtime) 是一把利刃，类似于其他语言中的反射机制，却有着更灵活的运行时特性。

利用 Runtime 我们在 Objective-C 里面可以做到：

- 动态调用方法
- 动态创建类
- 动态创建实例
- 替换已有的方法

总之 Runtime 可以做到太多太多的事情，是 Objective-C 语言里面的黑魔法之一。

# 为什么要引入 Runtime

最根本的原因是为有缺陷的 API 提供一个备用方案，正如 Runtime 绝大多时候的应用场景一样，它是一把屠龙的刀，屠龙之技是不会用在日常生活中的。

假设你有一个功能要实现，JSBox 提供的 API 没有满足你，或者是满足的有缺陷，你可以考虑通过 JSBox 提供的 Runtime 接口直接调用 Objective-C 的 API。

当然，在你可以实现功能的时候，应该尽量避免使用 Runtime 接口，因为调用起来比较复杂，查错也相对困难。

# JSBox 提供的接口

- `$objc(className)` 用于动态获取一个 Objective-C 的类
- `invoke(methodName, arguments ...)` 用于动态调用一个 Objective-C 的方法
- `$define(object)` 用于动态创建一个 Objective-C 的类
- `jsValue()` 用于将 Objective-C 数据转换成 JavaScript 值
- `ocValue()` 用于将 JavaScript 值封装成 Objective-C 值
- `$objc_retain(object)` 维持 object
- `$objc_release(object)` 释放 object

# 一个例子

这个例子在 JSBox 的窗口中创建一个按钮和标签，点击按钮后会打开微信：

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

这个例子混合了原始的 JSBox 调用和 Runtime 调用两种方式，展示了两种数据类型如何处理。

一个更完善也更复杂的例子，完全使用 Runtime 构建一个 2048 小游戏：https://github.com/cyanzhong/xTeko/tree/master/extension-scripts/2048