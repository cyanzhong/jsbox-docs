> 在 JSBox 的视图系统里面，还提供了很多接口用于与用户进行交互

# $ui.pop()

可以将 push 进来的视图弹出去一层。

# $ui.popToRoot()

直接回到视图栈的第一层。

# $ui.get(id)

获得一个 view 实例，等同于 `$(id)`。

> 如果页面里面只有一个该类型的 view 则可以使用 type 获得，例如 $("list")，否则需要指定 id。

# $ui.alert(object)

给用户一个 alert 框，用于提示或者选择：

```js
$ui.alert({
  title: "Hello",
  message: "World",
  actions: [
    {
      title: "OK",
      disabled: false, // Optional
      handler: function() {

      }
    },
    {
      title: "Cancel",
      handler: function() {

      }
    }
  ]
})
```

创建一个有标题、信息和按钮的 alert，如果不提供 `actions` 的话，一个默认的确定按钮会被自动提供。

`title` 和 `message` 都是可选项，同时如果偷懒的话可以只：

```js
$ui.alert("Haha!")
```

通常可以这样来测试得到的数据，因为目前还没有提供 debug 用的组件。

# $ui.action(object)

和 `$ui.alert` 基本一样，不同的是将会采用 `action sheet` 风格提供选项，目前 iPad 上不可使用。

# $ui.menu(object)

用一种更偷懒的方式创建一个菜单：

```js
$ui.menu({
  items: ["A", "B", "C"],
  handler: function(title, idx) {

  },
  finished: function(cancelled) {
    
  }
})
```

# $ui.popover(object)

使用 Popover 的样式弹出一个浮窗，该接口提供两种使用方式。

方式一，构建一个简单的列表选择浮窗：

```js
const {index, title} = await $ui.popover({
  sourceView: sender,
  sourceRect: sender.bounds, // default
  directions: $popoverDirection.up, // default
  size: $size(320, 200), // fits content by default
  items: ["Option A", "Option B"],
  dismissed: () => {},
});
```

此方式通过 `items` 指定每个选项的标题，返回一个 Promise。

方式二，使用自定义的 `views` 构建一个浮窗：

```js
const popover = $ui.popover({
  sourceView: sender,
  sourceRect: sender.bounds, // default
  directions: $popoverDirection.any, // default
  size: $size(320, 200), // fits screen width by default
  views: [
    {
      type: "button",
      props: {
        title: "Button"
      },
      layout: (make, view) => {
        make.center.equalTo(view.super);
        make.size.equalTo($size(100, 36));
      },
      events: {
        tapped: () => {
          popover.dismiss();
        }
      }
    }
  ]
});
```

此方式通过 `views` 来绘制自定义的界面，返回 popover 本身，可以调用 `dismiss` 方法将其关闭。

其中 `sourceView` 为弹出 popover 所必需的来源，它通常是一个 button，或是 navButtons 回调中的 sender。`sourceRect` 则为 popover 箭头所指向的位置（默认为 sourceView.bounds），`directions` 表示箭头允许的方向。

请参考我们提供的 demo 项目了解更多：https://gist.github.com/cyanzhong/313b2c8d138691233658f1b8a52f02c6

# $ui.toast(message)

显示一个悬浮的提示信息，几秒后自动消失：

```js
$ui.toast("Hey!")
```

`toast` 也支持设置显示时间：

```js
$ui.toast("Hey!", 10)
```

此 Toast 将会显示持续 10 秒钟。

> 你可以通过 $ui.clearToast() 来清除已经显示的 toast。

# $ui.success(string)

与 `toast` 类似，但背景色为绿色，以表示成功：

```js
$ui.success("Done");
```

# $ui.warning(string)

与 `toast` 类似，但背景色为黄色，以表示警告：

```js
$ui.warning("Be careful!");
```

# $ui.error(string)

与 `toast` 类似，但背景色为红色，以表示错误：

```js
$ui.error("Something went wrong!");
```

# $ui.loading(boolean)

在主界面显示一个正在加载的提示框：

```js
$ui.loading(true)
```

PS: 由于历史原因这个接口设计有点问题，除了使用 `true` 和 `false` 来开始或停止一个提示框以外，也可以使用是一个字符串来进行提示：

```js
$ui.loading("加载中...")
```

# $ui.progress(number)

显示加载进度，number 不处于 [0, 1] 之间时自动消失：

```js
$ui.progress(0.5)
```

同样，也支持通过一个（可选的）参数来设置提示语：

```js
$ui.progress(0.5, "下载中...")
```

# $ui.preview(object)

为文件/数据预览提供一个更便捷的方法：

```js
$ui.preview({
  title: "URL",
  url: "https://images.apple.com/v/ios/what-is/b/images/performance_large.jpg"
})
```

支持的属性：

属性 | 类型 | 说明
---|---|---
title | string | 标题
url | string | 链接
html | string | html
text | string | 文本

# $ui.create(object)

手动创建一个 view，object 参数和 $ui.render 一致：

```js
var canvas = $ui.create({
  type: "image",
  props: {
    bgcolor: $color("clear"),
    tintColor: $color("gray"),
    frame: $rect(0, 0, 100, 100)
  }
})
```

请注意，这个时候 view 还没有父 view，所以在这个时候不能使用他的 `layout` 方法。

取而代之的是，应该在把它添加到父 view 之后，手动进行 layout:

```js
const subview = $ui.create(...);
superview.add(subview);
subview.layout((make, view) => {

});
```

# $ui.window

获得 $ui.push 页面的 window 对象。

# $ui.controller

获得应用内最顶部的 view controller 对象。

# $ui.title

获取或设置应用内最顶部视图的标题。

# $ui.selectIcon()

从图标库中选择图标：

```js
var icon = await $ui.selectIcon();
```