# 时间线

正如我们前文提到，桌面小组件是基于时间的一系列快照。时间线是整个小组件工作方式的基石，我们会花一点时间解释这个概念。不过在此之前，请先阅读 Apple 提供的一篇文章：https://developer.apple.com/documentation/widgetkit/keeping-a-widget-up-to-date

这篇文章对理解时间线的工作原理极为重要，尤其是下面这个图：

<img src='https://docs-assets.developer.apple.com/published/2971813b6a098a34d134a04e38a50b83/2550/WidgetKit-Timeline-At-End@2x.png' width=360px/>

我们的代码扮演的是图中 Timeline Provider 的角色，系统在合适的时候向我们获取一个时间线和更新策略。然后系统会在合适的时间调用我们提供的方法显示小组件，并在策略满足的时候进行下一次获取。

所以，准确的时间线和合理的更新策略是小组件体验的保障。例如，天气应用可以知道接下来几个小时的天气状况，所以可以一次提供多个快照给系统，并在所有快照显示完成之后进行下一轮更新。

# $widget.setTimeline(object)

JSBox 使用 `$widget.setTimeline(...)` 函数来提供上述的时间线，使用样例：

```js
$widget.setTimeline({
  entries: [
    {
      date: new Date()
      info: {}
    }
  ],
  policy: {
    atEnd: true
  },
  render: ctx => {
    return {
      type: "text",
      props: {
        text: "Hello, World!"
      }
    }
  }
});
```

在 `setTimeline` 之前，我们可以进行一些数据获取的操作，例如请求网络或地理位置。但请注意，小组件必须在很短的时间内完成对时间线的提供，以免因为性能问题而无法完成。

## entries

指定快照相应的时间和额外的上下文信息，在时间线可以预测的情况下，可以一次性提供多个给系统。

在一个 `entry` 里面，用 `date` 指定该快照显示的时间，用 `info` 携带上下文信息，可以在 `render` 函数中通过 `ctx` 取出。

> 如未提供 entries，JSBox 将以当前的时间生成一个默认的 entry。

## policy

指定系统下次获取时间线的策略，有以下几种方式：

```js
$widget.setTimeline({
  policy: {
    atEnd: true
  }
});
```

该方式在最后一个 entry 被使用之后，进行一次新的时间线获取。

```js
$widget.setTimeline({
  policy: {
    afterDate: aDate
  }
});
```

该方式在时间到达 `afterDate` 之后，进行一次新的时间线获取。

```js
$widget.setTimeline({
  policy: {
    never: true
  }
});
```

该方式表示时间线为静态内容，不会周期性地更新。

上述策略仅仅是给系统一些“建议”，系统并不保证刷新一定会完成。为了避免系统过滤掉太过频繁的刷新，请设计有节制的策略以确保体验。

> 在不提供 `entries` 和 `policy` 的状况下，JSBox 为每个脚本提供了每小时刷新一次的默认实现。

## render

在到达每个 entry 指定的时间时，系统将调用上述的 `render` 函数，我们的代码在这里返回一个 JSON 数据作为视图的描述：

```js
$widget.setTimeline({
  render: ctx => {
    return {
      type: "text",
      props: {
        text: "Hello, World!"
      }
    }
  }
});
```

上述代码将在小组件上显示 "Hello, World!"，关于描述视图的语法，我们将在后面详细介绍。

`ctx` 包含了上下文，可以获取到包括 entry 在内的一些环境信息：

```js
$widget.setTimeline({
  render: ctx => {
    const entry = ctx.entry;
    const family = ctx.family;
    const displaySize = ctx.displaySize;
    const isDarkMode = ctx.isDarkMode;
  }
});
```

其中 `family` 表示小组件的尺寸，取值从 0 ~ 2 分别表示小、中、大三种布局。`displaySize` 反映了当前小组件的显示大小。

通过这些环境信息，我们可以动态地决定要返回什么样的视图给系统。

## 默认实现

当您的脚本并不需要刷新，或是默认的刷新策略满足需求，您可以仅提供一个 render 函数：

```js
$widget.setTimeline(ctx => {

});
```

这样，JSBox 会自动创建 entry 并设置每小时刷新一次的策略。

# 应用内预览

开发阶段，在主应用内调用 `$widget.setTimeline` 时，将打开预览小组件的模拟环境。同时支持三种尺寸，固定展示在时间线中的第一个 entry。

如需将脚本应用到实际桌面，请参考前述的设置方法。