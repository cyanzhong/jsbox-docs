# 对象属性

在 JavaScript 和 Native 通信的过程中，`对象传递`是一个比较麻烦的话题，以下数据类型可以自动完成 JavaScript 和 Native 的转换：

  Objective-C type  |   JavaScript type
--------------------|---------------------
        nil         |     undefined
      NSNull        |        null
      NSString      |       string
      NSNumber      |   number, boolean
    NSDictionary    |   Object object
      NSArray       |    Array object
      NSDate        |     Date object
      NSBlock (1)   |   Function object (1)
        id (2)      |   Wrapper object (2)
      Class (3)     | Constructor object (3)

但是显然，在我们通过 JavaScript 调用原生接口时，会通过接口返回各种各样的类型，例如返回一个图片，当我们调用接口的时候，也可能传递一个图片/二进制文件等等数据。

当 Native 给 JavaScript 返回数据时，将会把数据封装成一个 Object 类型，JavaScript 可以通过属性名获取到内部的 property。

例如，当我们实现列表点击事件时，会实现这样的代码：

```js
didSelect: function(tableView, indexPath) {
  var row = indexPath.row
}
```

其中的 `indexPath` 本质上是 iOS 内部的 IndexPath 类型，在这个例子里面我们可以通过 `.section` 和 `.row` 来访问到它内部的属性。

对于具体有哪些属性，我们需要一个专门的表来列举全部内容，方便随时查阅：[对象属性表](object/data.md)。

# $props

`$props` 方法可以获取一个对象所有的属性名：

```js
var props = $props("string")
```

$props 是一个简单的 js 方法，实现如下：

```js
var $props = function(object) {
  var result = []
  for (; object != null; object = Object.getPrototypeOf(object)) {
    var names = Object.getOwnPropertyNames(object)
    for (var idx=0; idx<names.length; idx++) {
      var name = names[idx]
      if (result.indexOf(name) === -1) {
        result.push(name)
      }
    }
  }
  return result
}
```

# $desc

`$desc` 方法可以获取一个对象的结构：

```js
let desc = $desc(object);
console.log(desc);
```