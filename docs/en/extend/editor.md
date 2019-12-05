# $editor

In JSBox, you can create plugins for the code editor, it helps you like an assistant.

Many useful features can be made with these APIs, such as custom indentation, or text encoding tools.

# $editor.text

Get or set all text in the code editor:

```js
var text = $editor.text;

$editor.text = "Hey!";
```

# $editor.view

Returns the text view of the current running editor:

```js
const editorView = $editor.view;
editorView.alpha = 0.5;
```

# $editor.selectedRange

Get or set selected range in the code editor:

```js
var range = $editor.selectedRange;

$editor.selectedRange = $(0, 10);
```

# $editor.selectedText

Get or set selected text in the code editor:

```js
var text = $editor.selectedText;

$editor.selectedText = "Hey!";
```

# $editor.isActive

Check whether the code editor is active:

```js
var isActive = $editor.isActive;
```

# $editor.canUndo

Check whether undo action can be taken:

```js
var canUndo = $editor.canUndo;
```

# $editor.canRedo

Check whether redo action can be taken:

```js
var canRedo = $editor.canRedo;
```

# $editor.save()

Save changes in the current editor:

```js
$editor.save();
```

# $editor.undo()

Perform undo action in the current editor:

```js
$editor.undo();
```

# $editor.redo()

Perform redo action in the current editor:

```js
$editor.redo();
```

# $editor.activate()

Activate the current editor:

```js
$editor.activate()
```

# $editor.deactivate()

Deactivate the current editor:

```js
$editor.deactivate()
```

# $editor.textInRange(range)

Get text in a range:

```js
var text = $editor.textInRange($range(0, 10));
```

# $editor.setTextInRange(text, range)

Set text in a range:

```js
$editor.setTextInRange("Hey!", $range(0, 10));
```