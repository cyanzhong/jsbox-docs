# 锁屏小组件 (Beta)

在 iOS 16 Beta 中，锁屏界面也可以有小组件，JSBox 也支持构建它们（目前在 TestFlight 版本）。

## 构建锁屏小组件

锁屏小组件本质上就是您熟悉的桌面小组件，有两个主要区别。

### 明亮的颜色

在锁屏状态下，小组件是用明亮的颜色而不是全色来呈现的。

您应该使用没有透明度的颜色，如纯白或纯黑来构建锁屏小组件。半透明的颜色将与墙纸混合，结果将无法阅读。

### 更小的尺寸

与桌面小组件相比，锁屏小组件有三种新的尺寸：

```js
const $widgetFamily = {
  // small, medium, large, xLarge
  accessoryCircular: 5,
  accessoryRectangular: 6,
  accessoryInline: 7,
}
```

- `accessoryCircular`: 1 * 1 圆形
- `accessoryRectangular`: 1 * 2 长方形
- `accessoryInline`: 在日期后面的一行信息

要检测当前的运行环境，请参考[这里](home-widget/timeline.md?id=render)。

## 应用内预览

为小组件提供的应用内预览目前不支持锁屏小组件的预览，请继续关注即将到来的更新。

## 样例代码

请参考这个 [GitHub 仓库](https://github.com/cyanzhong/jsbox-widgets) 以了解更多。