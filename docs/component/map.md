# type: "map"

`map` 用于创建一个地图，目前只是简单地支持在地图上显示位置：

```js
{
  type: "map",
  props: {
    location: {
      lat: 31.2990,
      lng: 120.5853
    }
  },
  layout: $layout.fill
}
```

在地图上显示苏州。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
location | object | 只写 | 用户位置

在后续的更新中将会添加更多细节，例如导航。