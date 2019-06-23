# 内建函数

除了标准的 JavaScript 内建函数，例如 encodeURI, setTimeout 等，JSBox 还提供了很多内建函数，这些函数可以直接在全局使用。

例如：

```js
var text = $l10n("MAIN_TITLE");
```

可以获得一个本地化的字符串。

为了与 JavaScript 内置的函数有所区分，JSBox 提供的内建函数都以 `$` 开头。