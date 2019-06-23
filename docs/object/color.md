# color

`color` 类型表示一个颜色，可以通过 `$color` 函数生成：

```js
var color = $color("#00eeee");
```

# color.hexCode

获得颜色对应的 hex 字符串：

```js
var hexCode = color.hexCode;
// -> "#00eeee"
```

# color.components

获得颜色对应的 RGB 数值：

```js
var components = color.components;
var red = components.red;
var green = components.green;
var blue = components.blue;
var alpha = components.alpha;
```