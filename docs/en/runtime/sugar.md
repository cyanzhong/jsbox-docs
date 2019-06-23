# Syntactic Sugar

Runtime is running code in another language, it's kind of like reflection, so you will feel tired to write code like:

```js
var app = $objc("UIApplication").invoke("sharedApplication");
var url = $objc("NSURL").invoke("URLWithString", "https://sspai.com");
app.invoke("openURL", url);
```

So we need a syntactic sugar to avoid this complex, since v1.24.0, we have new syntax:

```js
var app = $objc("UIApplication").$sharedApplication();
var url = $objc("NSURL").$URLWithString("https://sspai.com");
app.$openURL(url);
```

You can write less code and achieve the same effect, and it looks more like nature code.

# Rules

This syntax has very simple rules:

- Begin with `$` (dollar sign) to announce this is a runtime method
- Use `_` (dash sign) to replace `:` in Objective-C method
- Use `__` (2 dash signs) to replace `_` in Objective-C method

For instance:

```js
var app = $objc("UIApplication").$sharedApplication();
app.$sendAction_to_from_forEvent(action, target, null, null);
```

This works exactly the same as this Objective-C code:

```objc
UIApplication *app = [UIApplication sharedApplication];
[app sendAction:action to:target from:nil forEvent:nil];
```

For more detailed example, you can take a look this game (2048): https://github.com/cyanzhong/xTeko/tree/master/extension-scripts/%242048

# Auto generated classes

Some classes are used very frequently, so we import it automatically for you:

Class | Refer
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

These classes can be used directly without declare:

```js
var url = NSURL.$URLWithString("https://sspai.com");
```

Other classes you need to declare with $objc, you can use the return value:

```js
var appClass = $objc("UIApplication");

var app = appClass.$sharedApplication();

// Or
var app = UIApplication.$sharedApplication();
```

In short, $objc("UIApplication") also creates a variable named `UIApplication`, it's very convenient if you want to use it many times.