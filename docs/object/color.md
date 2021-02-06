# color

`color` 类型表示一个颜色，可以通过 `$color` 函数生成：

```js
const color = $color("#00eeee");
```

# color.hexCode

获得颜色对应的 hex 字符串：

```js
const hexCode = color.hexCode;
// -> "#00eeee"
```

# color.components

获得颜色对应的 RGB 数值：

```js
const components = color.components;
const red = components.red;
const green = components.green;
const blue = components.blue;
const alpha = components.alpha;
```