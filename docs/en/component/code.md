# type: "code"

Text view that provides syntax highlighting, and code editing, supports many commonly used languages and themes:

```js
$ui.render({
  views: [
    {
      type: "code",
      props: {
        text: "const value = 100"
      },
      layout: $layout.fill
    }
  ]
});
```

You can control its behavior with parameters like below:

Prop | Type | Default | Description
---|---|---|---
language | string | javascript | programming language
theme | string | nord | editor theme
darkKeyboard | bool | true | uses dark mode
adjustInsets | bool | true | adjust insets automatically
lineNumbers | bool | false | shows line numbers
invisibles | bool | false | show invisible characters
linePadding | number | null | line padding
keys | [string] | null | toolbar keys

Note that, those parameters have to be defined when creating a code view, cannot be overridden later.

Besides, code view inherits from text view, it behaves exactly the same as [`type: text`](en/component/text.md).

For instance, disable editing with `editable: false`. Or, control its content with the `text` property:

```js
const view = $("codeView");
const code = view.text;
view.text = "console.log([1, 2, 3])";
```

Of course, all events are supported:

```js
$ui.render({
  views: [
    {
      type: "code",
      props: {
        text: "const value = 100"
      },
      layout: $layout.fill,
      events: {
        changed: sender => {
          console.log("code changed");
        }
      }
    }
  ]
});
```

# props: language

`code` view is based on [highlightjs](https://highlightjs.org/), you can find all supported languages here: https://github.com/highlightjs/highlight.js/tree/master/src/languages

For example, syntax highlighting for Python:

```js
props: {
  language: "python"
}
```

# props: theme

`code` view is based on [highlightjs](https://highlightjs.org/), you can find all supported themes here: https://github.com/highlightjs/highlight.js/tree/master/src/styles

For example, use the `atom-one-light` theme:

```js
props: {
  theme: "atom-one-light"
}
```

# props: adjustInsets

In many cases, the keyboard is annoying because it hides the editing area. `code` view handles that for you, by default. It observes the keyboard height, and adjust the content insets automatically.

However, it's hard to make it perfect, you can disable it with `adjustInsets: false`.

# props: keys

By default, there will be an editing toolbar, here is how to customize:

```js
$ui.render({
  views: [
    {
      type: "code",
      props: {
        language: "markdown",
        keys: [
          "#",
          "-",
          "*",
          "`",
          //...
        ]
      },
      layout: $layout.fill
    }
  ]
});
```

If you want to remove the toolbar, you can override `accessoryView`.