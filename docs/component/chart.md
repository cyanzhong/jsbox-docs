# type: "chart"

`chart` 用来绘制图表来实现数据可视化：

```js
{
  type: "chart",
  props: {
    options: {
      "legend": {
        "data": ["Chart"]
      },
      "xAxis": {
        "data": [
          "A",
          "B",
          "C",
          "D"
        ]
      },
      "yAxis": {},
      "series": [
        {
          "name": "foo",
          "type": "bar",
          "data": [5, 20, 36, 10]
        }
      ]
    }
  },
  layout: $layout.fill
}
```

这将在页面上画出一个柱状图，options 支持的参数请参考 [ECharts 文档](http://www.echartsjs.com/option.html)。

# 动态绘制

在某些时候数据不是静态的，绘制可以通过一个函数来完成，在 JSBox 里面你可以使用模板字符串来实现：

```js
$ui.render({
  views: [
    {
      type: "chart",
      layout: $layout.fill,
      events: {
        ready: chart => {
          let options = `
          options = {
            tooltip: {},
            backgroundColor: "#fff",
            visualMap: {
              show: false,
              dimension: 2,
              min: -1,
              max: 1,
              inRange: {
                color: [
                  "#313695",
                  "#4575b4",
                  "#74add1",
                  "#abd9e9",
                  "#e0f3f8",
                  "#ffffbf",
                  "#fee090",
                  "#fdae61",
                  "#f46d43",
                  "#d73027",
                  "#a50026"
                ]
              }
            },
            xAxis3D: {
              type: "value"
            },
            yAxis3D: {
              type: "value"
            },
            zAxis3D: {
              type: "value"
            },
            grid3D: {
              viewControl: {
                // projection: 'orthographic'
              }
            },
            series: [
              {
                type: "surface",
                wireframe: {
                  // show: false
                },
                equation: {
                  x: {
                    step: 0.05
                  },
                  y: {
                    step: 0.05
                  },
                  z: function(x, y) {
                    if (Math.abs(x) < 0.1 && Math.abs(y) < 0.1) {
                      return "-";
                    }
                    return Math.sin(x * Math.PI) * Math.sin(y * Math.PI);
                  }
                }
              }
            ]
          };`;
          chart.render(options);
        }
      }
    }
  ]
});
```

用 `options = ` 的方式定义，这种方式和静态绘制的区别是 options 可以含有函数调用。

# chart.dispatchAction(args)

用于触发事件：

```js
chart.dispatchAction({
  type: "dataZoom",
  start: 20,
  end: 30
});
```

# chart.getWidth(handler)

用于获取视图的宽度：

```js
let width = await chart.getWidth();
```

# chart.getHeight(handler)

用于获取视图的高度：

```js
let height = await chart.getHeight();
```

# chart.getOption(handler)

用于获取当前的 options:

```js
let options = await chart.getOption();
```

# chart.resize($size)

用于更新视图的大小：

```js
chart.resize($size(100, 100));
```

# chart.showLoading()

显示加载状态：

```js
chart.showLoading();
```

# chart.hideLoading()

隐藏加载状态：

```js
chart.hideLoading();
```

# chart.clear()

清除当前绘制的图表：

```js
chart.clear();
```

# event: rendered

`rendered` 会在绘制时被调用：

```js
events: {
  rendered: () => {

  }
}
```

# event: finished

`finished` 会在绘制完成时被调用：

```js
events: {
  finished: () => {

  }
}
```

# WebView

当前图表控件使用 WebView 封装 [ECharts](http://www.echartsjs.com/index.html) 来实现，所以支持所有 WebView 支持的特性，例如 JavaScript 注入以及 $notify 机制，详情请参考[网页视图](component/web.md)。

更多样例：https://github.com/cyanzhong/xTeko/tree/master/extension-demos/charts