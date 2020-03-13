# type: "blur"

`blur` is designed to add a blur effect:

```js
{
  type: "blur",
  props: {
    style: 1 // 0 ~ 20
  },
  layout: $layout.fill
}
```

`style` 0 ~ 20 stands for different blur styles, refer to: https://developer.apple.com/documentation/uikit/uiblureffectstyle

# props

Prop | Type | Read/Write | Description
---|---|---|---
style | number | w | effect style