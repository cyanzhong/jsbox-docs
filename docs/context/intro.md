# Action Extension 上的扩展

`Action Extension` 是指 iOS 分享面板下面那一排图标，JSBox 的扩展支持从这里启动，从这里启动扩展通常是因为用户触发了一个分享操作，所以我们可以取到用户传递过来的分享内容。

# Action Extension 上面限制

与 Widget 类似的是，Action Extension 同样有些限制，虽然限制没有 Widget 那么多。

目前而言，限制主要有两点：

- 可用内存较小，当扩展使用过大的内存时，系统会强制关闭掉这个扩展
- 在 Action Extension 里面无法拍照，即无法使用 `$photo.pick` 接口

# $context

我们通过 `$context` 这个对象来封装来自外部的参数，Action Extension 里面表现为用户分享的内容。具体方法请见[方法列表](context/method.md)