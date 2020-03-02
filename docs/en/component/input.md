# type: "input"

`input` is used to create a text field, to receive text from users:

```js
{
  type: "input",
  props: {
    type: $kbType.search,
    darkKeyboard: true,
  },
  layout: function(make, view) {
    make.center.equalTo(view.super)
    make.size.equalTo($size(100, 32))
  }
}
```

This code shows a text field on screen, the keyboard will be dark mode.

# props

Prop | Type | Read/Write | Description
---|---|---|---
type | $kbType | rw | type
darkKeyboard | boolean | rw | dark mode
text | string | rw | text content
styledText | object | rw | styled text, [refer](en/component/text.md?id=styledtext)
textColor | $color | rw | text color
font | $font | rw | font
align | $align | rw | alignment
placeholder | string | rw | placeholder
clearsOnBeginEditing | boolean | rw | clears text on begin
autoFontSize | boolean | rw | adjust font size automatically
editing | boolean | r | is editing
secure | boolean | rw | is password

# focus()

Get the focus, show keyboard.

# blur()

Blur the focus, dismiss keyboard.

# events: changed

`changed` will be called when text changed:

```js
changed: function(sender) {

}
```

# events: returned

`returned` will be called once the return key pressed:

```js
returned: function(sender) {

}
```

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

# $input.text(object)

Instead of create a text field, you could also use `$input.text`:

```js
$input.text({
  type: $kbType.number,
  placeholder: "Input a number",
  handler: function(text) {

  }
})
```

# $input.speech(object)

Speech to text:

```js
$input.speech({
  locale: "en-US", // Optional
  autoFinish: false, // Optional
  handler: function(text) {

  }
})
```

It shows a popup text field to user directly, it's much easier.