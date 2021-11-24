# $editor

In JSBox, you can create plugins for the code editor, it helps you like an assistant.

Many useful features can be made with these APIs, such as custom indentation, or text encoding tools.

# $editor.text

Get or set all text in the code editor:

```js
const text = $editor.text;

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
const range = $editor.selectedRange;

$editor.selectedRange = $(0, 10);
```

# $editor.selectedText

Get or set selected text in the code editor:

```js
const text = $editor.selectedText;

$editor.selectedText = "Hey!";
```

# $editor.hasText

Returns true when the editor has text:

```js
const hasText = $editor.hasText;
```

# $editor.isActive

Check whether the code editor is active:

```js
const isActive = $editor.isActive;
```

# $editor.canUndo

Check whether undo action can be taken:

```js
const canUndo = $editor.canUndo;
```

# $editor.canRedo

Check whether redo action can be taken:

```js
const canRedo = $editor.canRedo;
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

# $editor.insertText(text)

Insert text into the selected range:

```js
$editor.insertText("Hello");
```

# $editor.deleteBackward()

Remove the character just before the cursor:

```js
$editor.deleteBackward();
```

# $editor.textInRange(range)

Get text in a range:

```js
const text = $editor.textInRange($range(0, 10));
```

# $editor.setTextInRange(text, range)

Set text in a range:

```js
$editor.setTextInRange("Hey!", $range(0, 10));
```