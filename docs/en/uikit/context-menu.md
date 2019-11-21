# Context Menu

In iOS 13 and above, you can provide [Context Menus](https://developer.apple.com/design/human-interface-guidelines/ios/controls/context-menus/) for any views, sub menus and SF Symbols are supported as well.

Here's a minimal example:

```js
$ui.render({
  views: [
    {
      type: "button",
      props: {
        title: "Long Press!",
        menu: {
          title: "Context Menu",
          items: [
            {
              title: "Title",
              handler: sender => {}
            }
          ]
        }
      },
      layout: (make, view) => {
        make.center.equalTo(view.super);
        make.size.equalTo($size(120, 36));
      }
    }
  ]
});
```

# SF Symbols

Other than just title, you can also set up an icon with the `symbol` property:

```js
{
  title: "Title",
  symbol: "paperplane",
  handler: sender => {}
}
```

For more information about SF Symbols, you can use the Apple official app: https://developer.apple.com/design/downloads/SF-Symbols.dmg or this JSBox script: https://xteko.com/install?id=141

# destructive

For important actions that may be dangerous, you can use the destructive style:

```js
{
  title: "Title",
  destructive: true,
  handler: sender => {}
}
```

# Sub Menus

When a menu item has `items` property, it becomes a sub-menu:

```js
{
  title: "Sub Menu",
  items: [
    {
      title: "Item 1",
      handler: sender => {}
    },
    {
      title: "Item 2",
      handler: sender => {}
    }
  ]
}
```

This sub-menu has two sub-items, sub-menus can be nested.

# Inline Menu

The above sub-menu items will be collapsed as secondary items, you can also display them directly, with some separators, just use the `inline` property:

```js
{
  title: "Sub Menu",
  inline: true,
  items: [
    {
      title: "Item",
      handler: sender => {}
    }
  ]
}
```

# list & matrix

For an element in `list` or `matrix`, an `indexPath` will be provided in the `handler` function:

```js
$ui.render({
  views: [
    {
      type: "list",
      props: {
        data: ["A", "B", "C"],
        menu: {
          title: "Context Menu",
          items: [
            {
              title: "Action 1",
              handler: (sender, indexPath) => {}
            }
          ]
        }
      },
      layout: $layout.fill
    }
  ]
});
```

It's very similar to `event: didSelect` in each case, the only difference is how to trigger the action.