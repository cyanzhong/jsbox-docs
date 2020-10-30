# type: "blur"

`blur` 用来创建一个模糊效果：

```js
{
  type: "blur",
  props: {
    style: 1 // 0 ~ 20
  },
  layout: $layout.fill
}
```

`style` 0 ~ 20 表示了不同的模糊效果，[参考](data/constant.md?id=blurstyle)。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
style | $blurStyle | w | 效果类型