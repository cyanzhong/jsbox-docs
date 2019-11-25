# 手势识别

在触摸设备里面，手势是一个很重要的交互形式，这一伟大的创新得益于 2007 年 [iPhone 问世](https://www.youtube.com/watch?v=x7qPAY9JqE4)。

iOS 支持丰富的手势识别，在 JSBox 里面目前仅支持重要的几个。

# events: tapped

实现了 `tapped` 事件的 view 会响应点击手势：

```js
tapped: function(sender) {

}
```

# events: longPressed

实现了 `longPressed` 事件的 view 会响应长按手势：

```js
longPressed: function(info) {
  let sender = info.sender;
  let location = info.location;
}
```

# events: doubleTapped

实现了 `doubleTapped` 事件的 view 会响应双击事件：

```js
doubleTapped: function(sender) {

}
```

# events: touchesBegan

当点击事件触发时调用：

```js
touchesBegan: function(sender, location, locations) {

}
```

# events: touchesMoved

当点击发生移动时调用：

```js
touchesMoved: function(sender, location, locations) {

}
```

# events: touchesEnded

当点击事件结束时调用

```js
touchesEnded: function(sender, location, locations) {

}
```