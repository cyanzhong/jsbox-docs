# type: "chart"

`chart` displays chart for data visualization:

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

It shows you a columnar chart, options are exactly the same as [echarts](https://ecomfe.github.io/echarts-doc/public/en/option.html).

# Dynamic Plotting

Sometimes we need to generate the data dynamically, it can be done with JavaScript functions, in that case you need to render the chart with template string:

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

Define the options with `options = `, you can use functions inside the string.

# chart.dispatchAction(args)

Trigger actions:

```js
chart.dispatchAction({
  type: "dataZoom",
  start: 20,
  end: 30
});
```

# chart.getWidth(handler)

Get width of the chart:

```js
let width = await chart.getWidth();
```

# chart.getHeight(handler)

Get height of the chart:

```js
let height = await chart.getHeight();
```

# chart.getOption(handler)

Get options of the chart:

```js
let options = await chart.getOption();
```

# chart.resize($size)

Resize the chart:

```js
chart.resize($size(100, 100));
```

# chart.showLoading()

Shows loading animation:

```js
chart.showLoading();
```

# chart.hideLoading()

Hides loading animation:

```js
chart.hideLoading();
```

# chart.clear()

Clear current chart:

```js
chart.clear();
```

# event: rendered

`rendered` will be called after rendered:

```js
events: {
  rendered: () => {

  }
}
```

# event: finished

`finished` will be called when finish:

```js
events: {
  finished: () => {

  }
}
```

# WebView

Chart view is an [ECharts](https://ecomfe.github.io/echarts-doc/public/en/index.html) wrapper that uses WebView, so you can use all features in WebView, such as JavaScript injection and $notify, please refer to [WebView](en/component/web.md) for details.

More examples: https://github.com/cyanzhong/xTeko/tree/master/extension-demos/charts