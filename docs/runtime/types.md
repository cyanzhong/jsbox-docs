> 原生类型与 Runtime 类型的相互转换

# 类型转换

当使用上述 `invoke` 接口时，返回的数据类型是一个 Objective-C 类型，而 JSBox 其他的接口生成的都是 JavaScript 类型。

这两种代码要混合在一起的时候，需要通过下面两个方法进行转换：

- `jsValue()` 从 Objective-C 值转换成 JavaScript 值
- `ocValue()` 将 JavaScript 值封装成 Objective-C 值

# 例子

例如 JSBox 提供的 `$color` 生成的是一个 JavaScript 值：

```js
var color1 = $color("red")
```

这种值被应用在 invoke 方法时需要：`color1.ocValue()` 才行。

而 invoke 生成的都是 ocValue:

```js
var color2 = $objc("UIColor").invoke("grayColor")
```

这种值在应用在 JSBox 接口时需要调用 `color2.jsValue()` 才行，例如：

```js
props: {
  bgcolor: color2.jsValue()
}
```

通过这两个方法，我们可以在 Runtime 环境和原始环境中穿梭，从而将两种代码混合起来。