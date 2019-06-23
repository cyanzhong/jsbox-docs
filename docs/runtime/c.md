# $defc

JSBox 也提供了调用 C 函数的方法，对于 iOS 提供的 C 函数，你可以通过这个方式来引入：

```js
$defc("NSClassFromString", "Class, NSString *")
```

第一个参数是函数名，第二个字符串依次是返回值类型和各个参数的类型（类似 $block 的定义）。

定义之后你就可以这样使用这个 C 函数了：

```js
NSClassFromString("NSURL")
```

类似的，对于这样一个 C 函数：`int func(void *ptr, NSObject *obj, float num)` 则需要这样定义：

```js
$defc("func", "int, void *, NSObject *, float")
```

注：目前不支持在 C 函数里面传递 struct 和 block 类型。