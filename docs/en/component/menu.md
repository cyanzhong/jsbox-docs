# type: "tab" & type: "menu"

JSBox provides two menu types, use `tab` if you only have few items, use `menu` to display a lot of items:

```js
$ui.render({
  views: [
    {
      type: "menu",
      props: {
        items: ["item 1", "item 2", "item 3", "item 4", "item 5", "item 6", "item 7", "item 8", "item 9"],
        dynamicWidth: true, // dynamic item width, default is false
      },
      layout: function(make) {
        make.left.top.right.equalTo(0)
        make.height.equalTo(44)
      },
      events: {
        changed: function(sender) {
          var items = sender.items
          var index = sender.index
          $ui.toast(index + ": " + items[index])
        }
      }
    }
  ]
})
```

It creates a menu, and shows a toast if the selected item has changed.

`sender.items` represents all items, `sender.index` means selected index (starts from 0).

`index` could be used to set the initial value as well:

```js
props: {
  index: 1
}
```

Select the second item by default.