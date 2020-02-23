# Scripts on Keyboard

Since v1.12.0, JSBox supports design a keyboard extension with JavaScript, you can create a plugin to improve editing experience.

There's no need to understand how it works, you just leverage abilities of `$keyboard`

Here are two examples for demonstrating how to build a keyboard plugin: 

https://github.com/cyanzhong/xTeko/tree/master/extension-demos/keyboard

[Try it out](https://xteko.com/redir?url=https://github.com/cyanzhong/xTeko/raw/master/extension-demos/keyboard.box)

https://github.com/cyanzhong/xTeko/tree/master/extension-demos/emoji-key

[Try it out](https://xteko.com/redir?url=https://github.com/cyanzhong/xTeko/raw/master/extension-demos/emoji-key.box)

# $keyboard.insert(string)

Insert a string into current editing context:

```js
$keyboard.insert("Hey!")
```

# $keyboard.delete()

Delete selected text or delete backward:

```js
$keyboard.delete()
```

# $keyboard.moveCursor(number)

Move cursor by an offset:

```js
$keyboard.moveCursor(5)
```

# $keyboard.playInputClick()

Play sound effect of keyboard clicking:

```js
$keyboard.playInputClick()
```

# $keyboard.hasText

Check whether current input context has text:

```js
var hasText = $keyboard.hasText
```

# $keyboard.selectedText

Get current selected text (iOS 11 only):

```js
var selectedText = $keyboard.selectedText
```

# $keyboard.textBeforeInput

Get text before input:

```js
const textBeforeInput = $keyboard.textBeforeInput;
```

# $keyboard.textAfterInput

Get text after input:

```js
const textAfterInput = $keyboard.textAfterInput;
```

# $keyboard.getAllText(handler)

Get all text (iOS 11 only):

```js
$keyboard.getAllText(function(text) {

});
```

# $keyboard.next()

Switch to next keyboard:

```js
$keyboard.next()
```

# $keyboard.send()

Simulate send action in the keyboard:

```js
$keyboard.send()
```

# $keyboard.dismiss()

Dismiss the keyboard:

```js
$keyboard.dismiss()
```

# $keyboard.barHidden

Whether hides the bottom bar, this is a configuration, you should use it before the UI starts.

Please note, above APIs are only available for keyboard, if you try it on other environments, it will raise an error.

# $keyboard.height

Get or set keyboard height:

```js
let height = $keyboard.height;

$keyboard.height = 500;
```