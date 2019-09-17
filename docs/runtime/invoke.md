> 通过 JSBox 提供的接口，动态的与原生接口进行交互

# invoke(methodName, arguments ...)

当我们通过 `$objc("")` 拿到 Objective-C 类时，可以通过 `invoke` 方法动态的执行他的方法：

```js
var label = $objc("UILabel").invoke("alloc.init")
label.invoke("setText", "Runtime")
```

上面的代码动态创建了一个 `label`，同时把文字设置成了 `Runtime`。

`invoke("alloc.init")` 也等价于 `invoke("alloc").invoke("init")`。

如果你希望一次性导入多个 Objective-C 类，可以这么做：

```js
$objc("UIColor, UIApplication, NSIndexPath");

const color = UIColor.$redColor();
const application = UIApplication.$sharedApplication();
```

# selector

以 `NSIndexPath` 为例，Objective-C 中：

```objc
NSIndexPath *indexPath = [NSIndexPath indexPathForRow:0 inSection:0];
```

在 JSBox Runtime 中这么实现：

```js
var indexPath = $objc("NSIndexPath").invoke("indexPathForRow:inSection:", 0, 0)
```

`indexPathForRow:inSection:` 就是这个方法的 selector，而后面的就是参数列表。