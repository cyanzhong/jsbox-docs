> 动画是 iOS 的强项之一，JSBox 也对其进行了简单的支持，并且提供了两种支持的方式。

# UIView animation

最简单的方式是使用 `$ui.animate`，例如：

```js
$ui.animate({
  duration: 0.4,
  animation: function() {
    $("label").alpha = 0
  },
  completion: function() {
    $("label").remove()
  }
})
```

这段代码会把 label 的透明度在 0.4 秒的时间里变成 0，然后移除这个 view（completion 是可选的）。

当然这个方法也支持更多的属性让你来实现一个 `spring animation`:

属性 | 类型 | 说明
---|---|---
delay | number | 延迟执行秒数
damping | number | 阻尼大小
velocity | number | 初始速度
options | number | 选项[请参考](https://developer.apple.com/documentation/uikit/uiviewanimationoptions)

# 链式调用

JSBox 引入了一种链式调用的机制，基于 [JHChainableAnimations](https://github.com/jhurray/JHChainableAnimations) 这个库：

```js
$("label").animator.makeBackground($color("red")).easeIn.animate(0.5)
```

比如这行代码可以让 label 的背景色在 0.5 秒的时间里变成红色，同时指定了动画曲线为 `easeIn`。

是的，对 view 调用 `animator` 对象，会返回一个 animator 实例，可以用一个链式语句完成整个动画过程。

具体细节请参考 `JHChainableAnimations` 的文档：https://github.com/jhurray/JHChainableAnimations

> 鉴于该项目缺乏持续的维护，目前不推荐使用此方式实现动画