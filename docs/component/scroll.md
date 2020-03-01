# type: "scroll"

`scroll` 用于布局一系列 views 在一个滚动的容器里：

```js
{
  type: "scroll",
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 500))
  },
  views: [
    {

    },
    {

    }
  ]
}
```

其实和创建别的 views 没有什么区别，唯一的不同是这个容器是可以滚动的。

# 视图大小

`scroll` 组件的可滚动区域大小是一个复杂的话题，有两种方法来调整大小。

方法一，scroll 组件的每个子 view 都显式的设置了大小，这样 scroll 组件会自动调整自己的大小：

```js
$ui.render({
  views: [{
    type: "scroll",
    layout: $layout.fill,
    views: [{
      type: "label",
      props: {
        text: text,
        lines: 0
      },
      layout: function(make, view) {
        make.width.equalTo(view.super)
        make.top.left.inset(0)
        make.height.equalTo(1000)
      }
    }]
  }]
})
```

方法二，手动给 scroll 组件设置 contentSize:

```js
props: {
  contentSize: $size(0, 1000)
}
```

简而言之，`scroll` 组件的高度依赖于设置，他不能完全靠子 view 计算得到。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
contentOffset | $point | 读写 | 滚动偏移
contentSize | $size | 读写 | 滚动区域大小
alwaysBounceVertical | boolean | 读写 | 永远可以上下滚动
alwaysBounceHorizontal | boolean | 读写 | 永远可以左右滚动
pagingEnabled | boolean | 读写 | 是否分页
scrollEnabled | boolean | 读写 | 是否可以滚动
showsHorizontalIndicator | boolean | 读写 | 显示横向滚动条
showsVerticalIndicator | boolean | 读写 | 显示纵向滚动条
indicatorInsets | $insets | 读写 | 滚动条边距
tracking | boolean | 只读 | 用户是否在触摸
dragging | boolean | 只读 | 用户是否在拖动
decelerating | boolean | 只读 | 是否正在减速
keyboardDismissMode | number | 读写 | 键盘收起模式
zoomEnabled | bool | 读写 | 内置图片是否可以缩放
maxZoomScale | number | 读写 | 图片缩放最大比例
doubleTapToZoom | number | 读写 | 是否双击缩放

# beginRefreshing()

开始显示下拉刷新的加载动画。

# endRefreshing()

结束显示下拉刷新加载动画。

# resize()

根据内容自动调整可滚动区域的大小。

# scrollToOffset($point)

滚动到一个偏移量：

```js
$("scroll").scrollToOffset($point(0, 100));
```

# events: pulled

`pulled` 方法将触发下拉刷新：

```js
pulled: function(sender) {
  
}
```

# events: didScroll

`didScroll` 在视图滚动时回调：

```js
didScroll: function(sender) {

}
```

# events: willBeginDragging

`willBeginDragging` 在用户开始拖动时回调：

```js
willBeginDragging: function(sender) {
  
}
```

# events: willEndDragging

`willEndDragging` 在将要结束拖拽时回调：

```js
willEndDragging: function(sender, velocity) {

}
```

# events: didEndDragging

`didEndDragging` 在已经结束拖拽时回调：

```js
didEndDragging: function(sender, decelerate) {

}
```

# events: willBeginDecelerating

`willBeginDecelerating` 在将要开始减速时回调：

```js
willBeginDecelerating: function(sender) {

}
```

# events: didEndDecelerating

`didEndDecelerating` 在结束减速时回调：

```js
didEndDecelerating: function(sender) {

}
```

# events: didEndScrollingAnimation

`didEndScrollingAnimation` 也是在结束减速时回调（不同的是他会在非人为触发的滚动时回调）：

```js
didEndScrollingAnimation: function(sender) {

}
```

# events: didScrollToTop

`didScrollToTop` 在滚动到顶部时回调：

```js
didScrollToTop: function(sender) {

}
```

# Auto Layout

要让 Auto Layout 对 scrollView 正常工作有些困难，我们推荐通过 `layoutSubviews` 来解决某些问题：

```js
const contentHeight = 1000;
$ui.render({
  views: [
    {
      type: "scroll",
      layout: $layout.fill,
      events: {
        layoutSubviews: sender => {
          $("container").frame = $rect(0, 0, sender.frame.width, contentHeight);
        }
      },
      views: [
        {
          type: "view",
          props: {
            id: "container"
          },
          views: [
            {
              type: "view",
              props: {
                bgcolor: $color("red")
              },
              layout: (make, view) => {
                make.left.top.right.equalTo(0);
                make.height.equalTo(300);
              }
            }
          ]
        }
      ]
    }
  ]
});
```

也即，向 scrollView 添加一个用于布局的子 view，该子 view 通过 layoutSubviews 设置 frame，然后在上面添加的 view 就可以使用 Auto Layout 了。了解更多：https://developer.apple.com/library/archive/technotes/tn2154/_index.html