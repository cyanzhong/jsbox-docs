> render 和 push 是 JSBox 里面绘制界面最主要的方法

# $ui.render(object)

通过 `$ui.render` 我们可以在画布上绘制界面，他的基本用法是：

```js
$ui.render({
  props: {
    id: "label",
    title: "Hello, World!"
  },
  views: [
    {
      type: "label",
      layout: function(make, view) {
        make.center.equalTo(view.super)
        make.size.equalTo($size(100, 100))
      }
    }
  ]
})
```

因为本质上画布也是一个 view，所以一样支持 `props`，里面的 title 表示在界面中的标题。

views 表示画布中的所有子 view，其中每个 view 也可以嵌套的包含 `views`，是一个递归的结构。

画布支持的额外 props：

属性 | 类型 | 说明
---|---|---
theme | string | 外观：light/dark/auto
title | string | 标题
titleColor | $color | 标题颜色
barColor | $color | bar 背景色
iconColor | $color | 图标颜色
debugging | bool | 显示界面调试工具
navBarHidden | bool | 隐藏导航栏
statusBarHidden | bool | 隐藏状态栏
statusBarStyle | number | 0 为黑色，1 为白色
formSheet | bool | 是否显示成 form sheet（仅 iPad）
pageSheet | bool | 是否显示成 page sheet（iOS 13）
homeIndicatorHidden | bool | 是否为 iPhone X 系列隐藏 Home Indicator
clipsToSafeArea | bool | 是否以 Safe Area 为边界裁剪视图
keyCommands | array | 快捷键

# $ui.push(object)

基本上与 `$ui.render` 完全一致，只不过 render 直接绘制在画布上，而 `push` 则会滑进来一个新的画布（可以滑动返回），让整个界面变成一个视图栈，可以多次 push 用于表达查看详情等场景。

从 v1.36.0 版本开始，可以通过 $ui.push("detail.ux") 来推进一个通过可视化界面编辑器生成的页面。

# $(id)

该方法用于通过 `id` 在画布中查找一个 view，例如：

```js
var label = $("label")
```

当 id 没有被指定的时候，会通过 type 进行查找，如果画布中只有一个该类型的 view，也会被正确返回。

# 生命周期

目前对于 $ui.render 和 $ui.push，支持以下生命周期回调：

```js
events: {
  appeared: function() {

  },
  disappeared: function() {

  },
  dealloc: function() {

  }
}
```

顾名思义，分别在页面出现、消失和销毁时被调用。

# 摇一摇手势

你可以这样检测摇一摇手势：

```js
events: {
  shakeDetected: function() {

  }
}
```

# 支持外接键盘

可以通过 `keyCommands` 设置外接键盘快捷键：

```js
$ui.render({
  props: {
    keyCommands: [
      {
        input: "I",
        modifiers: 1 << 20,
        title: "Discoverability Title",
        handler: () => {
          console.log("Command+I triggered.");
        }
      }
    ]
  }
});
```

modifiers 是一个掩码，有如下取值：

属性 | 取值
---|---
Caps lock | 1 << 16
Shift | 1 << 17
Control | 1 << 18
Alternate | 1 << 19
Command | 1 << 20
NumericPad | 1 << 21

例如需要同时按住 `Command` 和 `Shift` 的话，则 modifiers 为 (1 << 20 | 1 << 17)。