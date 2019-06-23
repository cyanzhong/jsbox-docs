# $widget

$widget 接口提供对 Widget 的相关操作。

# $widget.height

获取或更改 widget 的高度：

```js
// Get
var height = $widget.height;
// Set
$widget.height = 400;
```

# $widget.mode

获取 widget 当前状态（展开/折叠）：

```js
var mode = $widget.mode; // 0: 折叠 1: 展开
```

# $widget.modeChanged

观察 widget 折叠展开状态的变化：

```js
$widget.modeChanged = function(mode) {
  
}
```