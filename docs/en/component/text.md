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
styledText | object | rw | styled text
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

# styledText

Styled text based on markdown syntax, supports bold, italic and links, styles can be nested:

```js
const text = `**Bold** *Italic* or __Bold__ _Italic_

[Inline Link](https://docs.xteko.com) <https://docs.xteko.com>

_Nested **styles**_`

$ui.render({
  views: [
    {
      type: "text",
      props: {
        styledText: text
      },
      layout: $layout.fill
    }
  ]
});
```

This uses the default font and color, for using custom values:

```js
$ui.render({
  views: [
    {
      type: "text",
      props: {
        styledText: {
          text: "",
          font: $font(15),
          color: $color("black")
        }
      },
      layout: $layout.fill
    }
  ]
});
```

For literals like `*`, `_`, escape them with `\\`.

If you want to control formats precisely, you can set `styles` for each range:

```js
const text = `
AmericanTypewriter Cochin-Italic

Text Color Background Color

Kern

Strikethrough Underline

Stroke

Link

Baseline Offset

Obliqueness
`;

const _range = keyword => {
  return $range(text.indexOf(keyword), keyword.length);
}

$ui.render({
  views: [
    {
      type: "text",
      props: {
        styledText: {
          text: text,
          font: $font(17),
          color: $color("black"),
          markdown: false, // whether to use markdown syntax
          styles: [
            {
              range: _range("AmericanTypewriter"),
              font: $font("AmericanTypewriter", 17)
            },
            {
              range: _range("Cochin-Italic"),
              font: $font("Cochin-Italic", 17)
            },
            {
              range: _range("Text Color"),
              color: $color("red")
            },
            {
              range: _range("Background Color"),
              color: $color("white"),
              bgcolor: $color("blue")
            },
            {
              range: _range("Kern"),
              kern: 10
            },
            {
              range: _range("Strikethrough"),
              strikethroughStyle: 2,
              strikethroughColor: $color("red")
            },
            {
              range: _range("Underline"),
              underlineStyle: 9,
              underlineColor: $color("green")
            },
            {
              range: _range("Stroke"),
              strokeWidth: 3,
              strokeColor: $color("black")
            },
            {
              range: _range("Link"),
              link: "https://xteko.com"
            },
            {
              range: _range("Baseline Offset"),
              baselineOffset: 10
            },
            {
              range: _range("Obliqueness"),
              obliqueness: 1
            }
          ]
        }
      },
      layout: $layout.fill
    }
  ]
});
```

Attribute | Type | Description
---|---|---
range | $range | text range
font | $font | font
color | $color | foreground color
bgcolor | $color | background color
kern | number | font kerning
strikethroughStyle | number | strikethrough style [Refer](https://developer.apple.com/documentation/uikit/nsunderlinestyle?language=objc)
strikethroughColor | $color | strikethrough color
underlineStyle | number | underline style [Refer](https://developer.apple.com/documentation/uikit/nsunderlinestyle?language=objc)
underlineColor | $color | underline color
strokeWidth | number | stroke width
strokeColor | $color | stroke color
link | string | link URL
baselineOffset | number | baseline offset
obliqueness | number | font obliqueness

Markdown syntax is disable when `styles` is used, it can be turned on by specifying `markdown: true`.

For underline and strikethrough, please refer to Apple's documentation, here is an example:

```js
NSUnderlineStyleNone = 0x00,
NSUnderlineStyleSingle = 0x01,
NSUnderlineStyleThick = 0x02,
NSUnderlineStyleDouble = 0x09,
NSUnderlineStylePatternSolid = 0x0000,
NSUnderlineStylePatternDot = 0x0100,
NSUnderlineStylePatternDash = 0x0200,
NSUnderlineStylePatternDashDot = 0x0300,
NSUnderlineStylePatternDashDotDot = 0x0400,
NSUnderlineStyleByWord = 0x8000,
```

If you want a single line with dots, you can combine `NSUnderlineStyleSingle` and `NSUnderlineStylePatternDot`:

```js
underlineStyle: 0x01 | 0x0100
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