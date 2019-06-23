# 语法糖

Runtime 的本质是在一门语言里面写另一门语言，也就是通过字符串的方式来反射调用，类似这样的做法写起来极为繁琐：

```js
var app = $objc("UIApplication").invoke("sharedApplication");
var url = $objc("NSURL").invoke("URLWithString", "https://sspai.com");
app.invoke("openURL", url);
```

所以我们需要一种语法糖来缓解这种复杂，在 v1.24.0 以后，我们引入了一种新的语法结构：

```js
var app = $objc("UIApplication").$sharedApplication();
var url = $objc("NSURL").$URLWithString("https://sspai.com");
app.$openURL(url);
```

这不仅可以少写很多代码，更能让反射代码看起来更像原生的代码（虽然本质上是一样的）。

# 规则

这个语法规则十分简单，一共只有三个规则：

- 使用 `$` 符号（美元符）来表示这是一个 Runtime 调用
- 使用 `_` 符号（下划线）来表示 Objective-C 方法名里面的 `:` 号
- 使用 `__` 符号（两个下划线）来表示 Objective-C 方法名里面的 `_` 号

例如：

```js
var app = $objc("UIApplication").$sharedApplication();
app.$sendAction_to_from_forEvent(action, target, null, null);
```

这个代码等同于 Objective-C 里面的：

```objc
UIApplication *app = [UIApplication sharedApplication];
[app sendAction:action to:target from:nil forEvent:nil];
```

更完善的例子，请参考这个使用新语法实现的 2048 小游戏：https://github.com/cyanzhong/xTeko/tree/master/extension-scripts/%242048

# 自动生成的类

有些 Objective-C 十分常用，所以 JSBox 现在默认支持，而无需再使用 $objc("ClassName") 去获得：

类名 | 参考
---|---
NSDictionary | https://developer.apple.com/documentation/foundation/nsdictionary
NSMutableDictionary | https://developer.apple.com/documentation/foundation/nsmutabledictionary
NSArray | https://developer.apple.com/documentation/foundation/nsarray
NSMutableArray | https://developer.apple.com/documentation/foundation/nsmutablearray
NSSet | https://developer.apple.com/documentation/foundation/nsset
NSMutableSet | https://developer.apple.com/documentation/foundation/nsmutableset
NSString | https://developer.apple.com/documentation/foundation/nsstring
NSMutableString | https://developer.apple.com/documentation/foundation/nsmutablestring
NSData | https://developer.apple.com/documentation/foundation/nsdata
NSMutableData | https://developer.apple.com/documentation/foundation/nsmutabledata
NSNumber | https://developer.apple.com/documentation/foundation/nsnumber
NSURL | https://developer.apple.com/documentation/foundation/nsurl
NSEnumerator | https://developer.apple.com/documentation/foundation/nsenumerator

这些你可以直接使用，就像是这样：

```js
var url = NSURL.$URLWithString("https://sspai.com");
```

其他的类你需要通过 $objc 定义，你可以使用它的返回值，但同时他也会生成一个同名的对象：

```js
var appClass = $objc("UIApplication");

var app = appClass.$sharedApplication();

// Or
var app = UIApplication.$sharedApplication();
```

也即 $objc("UIApplication") 会生成一个叫做 `UIApplication` 的对象方便你下次使用。