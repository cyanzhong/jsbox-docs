# type: "text"

`text` is more complicated than `label`, it is editable:

```js
{
  type: "text",
  props: {
    text: "Hello, World!\n\nThis is a demo for Text View in JSBox extension!\n\nCurrently we don't support attributed string in iOS.\n\nYou can try html! Looks pretty cool."
  },
  layout: $layout.fill
}
```

Create an editable text view, shows a paragraph of text with multiple lines.

# props

Prop | Type | Read/Write | Description
---|---|---|---
type | $kbType | rw | keyboard type
darkKeyboard | boolean | rw | dark mode
text | string | rw | text content
html | string | w | html content
font | $font | rw | font
textColor | $color | rw | text color
align | $align | rw | alignment
placeholder | string | rw | placeholder
selectedRange | $range | rw | selected range
editable | boolean | rw | is editable
selectable | boolean | rw | is selectable
insets | $insets | rw | edge insets

# focus()

Get the focus, show keyboard.

# blur()

Blur the focus, dismiss keyboard.

# events: didBeginEditing

`didBeginEditing` will be called after editing began:

```js
didBeginEditing: function(sender) {

}
```

# events: didEndEditing

`didEndEditing` will be called after editing ended:

```js
didEndEditing: function(sender) {
  
}
```

# events: didChange

`didChange` will be called once text changed:

```js
didChange: function(sender) {

}
```

# events: didChangeSelection

`didChangeSelection` will be called once selection changed:

```js
didChangeSelection: function(sender) {

}
```

`text` is a subclass of `scroll`, it works like a scroll view.

# Customize keyboard toolbar

You can customize toolbar as below:

```js
$ui.render({
  views: [
    {
      type: "input",
      props: {
        accessoryView: {
          type: "view",
          props: {
            height: 44
          },
          views: [

          ]
        }
      }
    }
  ]
});
```

# Customize keyboard view

You can customize keyboard as below:

```js
$ui.render({
  views: [
    {
      type: "input",
      props: {
        keyboardView: {
          type: "view",
          props: {
            height: 267
          },
          views: [

          ]
        }
      }
    }
  ]
});
```