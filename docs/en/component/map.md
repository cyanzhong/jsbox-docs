# type: "map"

`map` is designed to display a map view:

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

It shows a map and locates at Suzhou, China.

# props

Prop | Type | Read/Write | Description
---|---|---|---
location | object | w | user location

We are still working on it, we might introduce new features like navigation in the future.