> 在 JSBox 中可以动态创建类和方法，用于实现更灵活的功能

# $define(object)

通过 `$define` 方法可以动态创建一个 Objective-C Class:

```js
$define({
  type: "MyHelper: NSObject",
  events: {
    instanceMethod: function() {
      $ui.alert("instance")
    },
    "indexPathForRow:inSection:": function(row, section) {
      $ui.alert("row: " + row + ", section: " + section)
    }
  },
  classEvents: {
    classMethod: function() {
      $ui.alert("class")
    }
  }
})
```

主要有三个部分：

- `type` 表示类名，声明方式与 Objective-C 相同
- `events` 中实现所有的实例方法
- `classEvents` 中实现所有的类方法

定义之后可以这样使用这个类：

```js
$objc("MyHelper").invoke("alloc.init").invoke("instanceMethod")
$objc("MyHelper").invoke("classMethod")
```

分别会弹出 `instance` 和 `class` 两个提示。

# $delegate(object)

在 Runtime 代码中，我们可能经常会需要创建一个 Delegate 对象，通过 $delegate 可以快速做到：

```js
const textView = $objc("UITextView").$new();
textView.$setDelegate($delegate({
  type: "UITextViewDelegate",
  events: {
    "textViewDidChange:": sender => {
      console.log(sender.$text().jsValue());
    }
  }
}));
```

简单来说，$delegate 使用和 $define 类似的定义。但无需指定类名，并且会自动创建实例。