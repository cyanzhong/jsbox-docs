# $editor

在 JSBox 里，你可以通过 $editor 实现代码编辑器插件，用来控制编辑器的行为，起到辅助编辑的作用。

你可以通过这些接口实现很多功能，例如自己的代码排版规则，或是文字编码工具。

# $editor.text

获取或设置编辑器内的全部文本：

```js
var text = $editor.text;

$editor.text = "Hey!";
```

# $editor.view

获取当前编辑器正在使用的视图：

```js
const editorView = $editor.view;
editorView.alpha = 0.5;
```

# $editor.selectedRange

获取或设置编辑器内选中的范围：

```js
var range = $editor.selectedRange;

$editor.selectedRange = $(0, 10);
```

# $editor.selectedText

获取或设置编辑器内选中的文本：

```js
var text = $editor.selectedText;

$editor.selectedText = "Hey!";
```

# $editor.isActive

获取编辑器当前是否处于激活状态：

```js
var isActive = $editor.isActive;
```

# $editor.canUndo

判断当前的编辑器是否可以执行撤销操作：

```js
var canUndo = $editor.canUndo;
```

# $editor.canRedo

判断当前的编辑器是否可以执行重做操作：

```js
var canRedo = $editor.canRedo;
```

# $editor.save()

保存当前编辑器的改动：

```js
$editor.save();
```

# $editor.undo()

对当前编辑器执行撤销操作：

```js
$editor.undo();
```

# $editor.redo()

对当前编辑器执行重做操作：

```js
$editor.redo();
```

# $editor.activate()

激活当前的编辑器：

```js
$editor.activate()
```

# $editor.deactivate()

结束当前编辑器的激活状态：

```js
$editor.deactivate()
```

# $editor.textInRange(range)

获取当前编辑器里某个范围内的文本：

```js
var text = $editor.textInRange($range(0, 10));
```

# $editor.setTextInRange(text, range)

设置当前编辑器里某个范围内的文本：

```js
$editor.setTextInRange("Hey!", $range(0, 10));
```