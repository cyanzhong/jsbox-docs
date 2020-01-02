# type: "tab" & type: "menu"

提供两种方式用于显示一个菜单，当项目较少时，使用 `tab`，项目较多可以滚动时，使用 `menu`：

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

上述代码生成一个菜单，并且处理用户点击的动作。

`sender.items` 表示所有项目，`sender.index` 表示被选中的 index（从 0 开始）。

`index` 属性也可以定义初始选中：

```js
props: {
  index: 1
}
```

默认选中第二个。