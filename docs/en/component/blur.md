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

`style` 0 ~ 20 stands for different blur styles, [reference](en/data/constant.md?id=blurstyle).

# props

Prop | Type | Read/Write | Description
---|---|---|---
style | $blurStyle | w | effect style