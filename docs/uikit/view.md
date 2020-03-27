> JSBox 提供了一套绘制视图的方案，这里我们介绍这套方案的核心概念

# type: "view"

`view` 是最基层的控件，所有控件的父类：

```js
$ui.render({
  views: [
    {
      type: "view",
      props: {
        bgcolor: $color("#FF0000")
      },
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.size.equalTo($size(100, 100))
      },
      events: {
        tapped: function(sender) {

        }
      }
    }
  ]
})
```

将会绘制一个红色的视图，`view` 是所有控件的父类，所以 view 支持的属性其他控件都支持。

PS: 关于各种属性的类型转换请参考：[数据转换](data/intro.md)

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
theme | string | 读写 | light, dark, auto
alpha | number | 读写 | 透明度
bgcolor | $color | 读写 | 背景色
cornerRadius | number | 读写 | 圆角半径
smoothCorners | boolean | 读写 | 圆角是否使用平滑曲线
radius | number | 只写 | 圆角半径（过时，请使用 `cornerRadius`）
smoothRadius | number | 只写 | 平滑圆角半径（过时，请使用 `smoothCorners`）
frame | $rect | 读写 | 位置和大小
size | $size | 读写 | 大小
center | $point | 读写 | 中心位置
flex | string | 读写 | 自动缩放规则
userInteractionEnabled | boolean | 读写 | 是否响应触摸事件
multipleTouchEnabled | boolean | 读写 | 是否支持多点触摸
super | view | 只读 | 父视图
prev | view | 只读 | 前一个视图
next | view | 只读 | 后一个视图
window | view | 只读 | 所属的 window
views | array | 只读 | 子视图
clipsToBounds | boolean | 读写 | 是否裁剪子 view
opaque | boolean | 读写 | 是否不透明
hidden | boolean | 读写 | 是否隐藏
contentMode | $contentMode | 读写 | [请参考](https://developer.apple.com/documentation/uikit/uiview/1622619-contentmode)
tintColor | $color | 读写 | 着色
borderWidth | number | 读写 | 边框宽度
borderColor | $color | 读写 | 边框颜色
circular | bool | 读写 | 是否圆形
animator | object | 只读 | 动画对象
snapshot | object | 只读 | 生成截图
info | object | 读写 | 用于绑定一些信息，例如上下文参数
accessibilityLabel | string | 读写 | accessibility label
accessibilityHint | string | 读写 | accessibility hint
accessibilityValue | string | 读写 | accessibility value

注意：你不能在 layout 函数里面使用 `prev` 和 `next`，因为这个时候视图结构还没有被生成。

从 v1.36.0 版本开始，可以通过 $ui.render("main.ux") 来渲染一个通过可视化界面编辑器生成的页面。

# navButtons

我们可以在界面右上角自定义按钮，例如：

```js
$ui.render({
  props: {
    navButtons: [
      {
        title: "Title",
        image: image, // Optional
        icon: "024", // Or you can use icon name
        symbol: "checkmark.seal", // SF symbols are supported
        handler: sender => {
          $ui.alert("Tapped!")
        }
      }
    ]
  }
})
```

最多可以配置两个按钮，并且在调试模式下只会显示一个。

# titleView

除了通过 `title` 来指定标题，还可以通过 `titleView` 来指定 navBar 顶部展示的视图：

```js
$ui.render({
  props: {
    titleView: {
      type: "tab",
      props: {
        bgcolor: $rgb(240, 240, 240),
        items: ["A", "B", "C"]
      },
      events: {
        changed: sender => {
          console.log(sender.index);
        }
      }
    }
  },
  views: [

  ]
});
```

# layout(function)

手动触发 view 的 layout 方法，参数和 view 定义时的 `layout` 函数完全相同：

```js
view.layout((make, view) => {
  make.left.top.right.equalTo(0);
  make.height.equalTo(100);
});
```

# updateLayout(function)

`updateLayout` 方法可以更新一个控件的 layout：

```js
$("label").updateLayout(function(make) {
  make.size.equalTo($size(200, 200))
})
```

请注意，`updateLayout` 只能对**已存在**的约束进行更新，否则的话将没有效果。

# remakeLayout(function)

和 updateLayout 类似，但是重新设置 layout 会导致更多性能消耗，在可能时应该使用 updateLayout。

# add(object)

动态添加一个子 view，object 的结构定义和 `$ui.render(object)` 中 view 的完全一致，也可以是通过 `$ui.create(...)` 创建出来的 view 实例。

# get(id)

通过 id 获取一个子 view。

# remove()

将此 view 从父视图中移除。

# insertBelow(view, other)

将一个新的视图插入到一个已存在视图的下方：

```js
view.insertBelow(newView, existingView);
```

# insertAbove(view, other)

将一个新的视图插入到一个已存在视图的上方：

```js
view.insertAbove(newView, existingView);
```

# insertAtIndex(view, index)

将一个新的视图插入到一个指定的位置：

```js
view.insertAtIndex(newView, 4);
```

# moveToFront()

将自己移动到父视图的顶部：

```js
existingView.moveToFront();
```

# moveToBack()

将自己移动到父视图的底部：

```js
existingView.moveToBack();
```

# relayout()

更新 layout，此方法可能在动画中调用。

# setNeedsLayout()

将此 view 标记为需要 layout，会在下一个绘制循环中被 layout。

# layoutIfNeeded()

强制触发下一个绘制循环，可以配合 `setNeedsLayout` 使用：

```js
view.setNeedsLayout();
view.layoutIfNeeded();
```

# sizeToFit()

将 view 调整到当前 bounds 下最合适的大小。

# scale(number)

将控件缩放到一个比例，例如：

```js
view.scale(0.5)
```

# snapshotWithScale(scale)

指定比例得到一个截图：

```js
const image = view.snapshotWithScale(1)
```

# rotate(number)

将控件旋转一个角度，例如：

```js
view.rotate(Math.PI)
```

# events: ready

所有的 view 都支持 `ready` 事件，将会在 view 初始化完成之后调用：

```js
ready: function(sender) {
  
}
```

# events: tapped

所有的 view 都支持 `tapped` 事件：

```js
tapped: function(sender) {

}
```

该事件会在被点击的时候调用，`sender` 表示触发此事件的对象，在上述例子中就是 view 本身。

另外，events 也可以简写成：

```js
tapped(sender) {

}
```

和上述代码具有同样效果。

# events: pencilTapped

所有的 view 都支持 `pencilTapped` 来检测来自 Apple Pencil 的点击：

```js
pencilTapped: function(info) {
  var action = info.action; // 0: Ignore, 1: Switch Eraser, 2: Switch Previous, 3: Show Color Palette
  var enabled = info.enabled; // whether the system reports double taps on Apple Pencil to your app
}
```

# events: hoverEntered

在 iPadOS 13.4 及以上使用 Trackpad，指针进入时调用：

```js
hoverEntered: sender => {
  sender.alpha = 0.5;
}
```

# events: hoverExited

在 iPadOS 13.4 及以上使用 Trackpad，指针移出时调用：

```js
hoverExited: sender => {
  sender.alpha = 1.0;
}
```

# events: themeChanged

用于监听 [Dark Mode](uikit/dark-mode.md) 的改变：

```js
themeChanged: (sender, isDarkMode) => {
  
}
```

更多控件如何使用请参考 [控件列表](component/label.md) 一章。