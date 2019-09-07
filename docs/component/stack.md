# type: "stack"

这是一种特殊的视图，它本身并不渲染任何内容，而仅仅是用作对其子 view 自动布局。

请注意，JSBox 的 stack view 完全基于 `UIStackView`，所以为了更好地理解这一节的内容，请先阅读 Apple 的官方文档：https://developer.apple.com/documentation/uikit/uistackview

# 概览

请先看一个 Stack View 的简单样例：

```js
$ui.render({
  views: [
    {
      type: "stack",
      props: {
        spacing: 10,
        distribution: $stackViewDistribution.fillEqually,
        stack: {
          views: [
            {
              type: "label",
              props: {
                text: "Left",
                align: $align.center,
                bgcolor: $color("silver")
              }
            },
            {
              type: "label",
              props: {
                text: "Center",
                align: $align.center,
                bgcolor: $color("aqua")
              }
            },
            {
              type: "label",
              props: {
                text: "Right",
                align: $align.center,
                bgcolor: $color("lime")
              }
            }
          ]
        }
      },
      layout: $layout.fill
    }
  ]
});
```

如果你希望一些视图被 stack 自动布局，应该把它们放到 `stack` 里面，而不是直接放在 `views` 这个节点下面。

另外，你可以通过 `axis`, `distribution`, `alignment`, 和 `spacing` 等属性来控制布局策略。

# props: axis

`axis` 属性可以用来控制 stack 的布局方向，支持竖排或者横排，可选值：

```js
- $stackViewAxis.horizontal
- $stackViewAxis.vertical
```

# props: distribution

`distribution` 属性 stack 在 axis 方向上以何种策略分布，可选值：

```js
- $stackViewDistribution.fill
- $stackViewDistribution.fillEqually
- $stackViewDistribution.fillProportionally
- $stackViewDistribution.equalSpacing
- $stackViewDistribution.equalCentering
```

# props: alignment

`alignment` 属性决定了 stack 上的对齐方式，可选值：

```js
- $stackViewAlignment.fill
- $stackViewAlignment.leading
- $stackViewAlignment.top
- $stackViewAlignment.firstBaseline
- $stackViewAlignment.center
- $stackViewAlignment.trailing
- $stackViewAlignment.bottom
- $stackViewAlignment.lastBaseline
```

# props: spacing

`spacing` 属性决定了 stack 上各个子 view 之间的间距，应该填入一个数字，也可以使用下面这两个常量：

```js
- $stackViewSpacing.useDefault
- $stackViewSpacing.useSystem
```

# props: isBaselineRelative

`isBaselineRelative` 属性决定了垂直方向上的 spacing 是否基于 baseline，应该填入一个布尔值。

# props: isLayoutMarginsRelative

`isLayoutMarginsRelative` 属性决定了 stack 的布局策略是否基于 layoutMargins，应该填入一个布尔值。

# 动态改变一个视图

在视图初始化之后，你可以通过下面的方式动态改变他们：

```js
const stackView = $("stackView");
const views = stackView.stack.views;
views[0].hidden = true;

// This hides the first view in the stack
```

# 添加一个视图

除了在初始化的时候填入 `stack.views`，你还可以动态的添加一个视图到 stack：

```js
const stackView = $("stackView");
stackView.stack.add(newView);

// newView can be created with $ui.create
```

# 移除一个视图

可以通过这样的方式移除一个视图：

```js
const stackView = $("stackView");
stackView.stack.remove(existingView);

// existingView can be retrieved with id
```

# 插入一个视图

向 stack 插入一个视图到 index：

```js
const stackView = $("stackView");
stackView.stack.insert(newView, 2);
```

# 设置视图间距

Stack 视图会自动管理间距，你也可以为某个特定的视图自定义间距：

```js
const stackView = $("stackView");
stackView.stack.setSpacingAfterView(arrangedView, 20);

// arrangedView must be a view that is contained in the stack
```

# 获得视图间距

获得某个特定视图之后的间距：

```js
const stackView = $("stackView");
const spacing = stackView.stack.spacingAfterView(arrangedView);

// arrangedView must be a view that is contained in the stack
```

# 示例代码

相较于其他类型的视图，stack view 并不那么容易理解，所以我们构建了一个示例项目，方便让你理解上述的这些属性是如何工作的：https://github.com/cyanzhong/xTeko/blob/master/extension-demos/stack-view