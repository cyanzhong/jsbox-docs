> Call Objective-C APIs directly using runtime APIs

# invoke(methodName, arguments ...)

We could get an Objective-C object, and call its method:

```js
var label = $objc("UILabel").invoke("alloc.init")
label.invoke("setText", "Runtime")
```

It creates a label, and sets the text to `Runtime`.

Methods are chainable, so `invoke("alloc.init")` equals to `invoke("alloc").invoke("init")`.

If you want to import many Objective-C classes in one go, here is the solution:

```js
$objc("UIColor, UIApplication, NSIndexPath");

const color = UIColor.$redColor();
const application = UIApplication.$sharedApplication();
```

# selector

Invoke a method that has multiple parameters (Objective-C):

```objc
NSIndexPath *indexPath = [NSIndexPath indexPathForRow:0 inSection:0];
```

In JSBox runtime, we could do:

```js
var indexPath = $objc("NSIndexPath").invoke("indexPathForRow:inSection:", 0, 0)
```

`indexPathForRow:inSection:` is a selector (function) in Objective-C, the following are parameters.