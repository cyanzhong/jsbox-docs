# 长按菜单

你可以为任意的 view 提供长按菜单（[Context Menus](https://developer.apple.com/design/human-interface-guidelines/ios/controls/context-menus/)），支持子菜单和 [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/sf-symbols/overview/)。

下面是一个最简单的样例：

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

除了显示标题，也可以用 `symbol` 属性指定图标，例如：

```js
{
  title: "Title",
  symbol: "paperplane",
  handler: sender => {}
}
```

查询 SF Symbols 相关的名字，你可以使用 Apple 官方提供的应用：https://developer.apple.com/design/downloads/SF-Symbols.dmg 或是这个 JSBox 脚本：https://xteko.com/install?id=141&lang=zh-Hans

# destructive

可以将标题显示成红色来表示这是个危险动作，提醒用户注意：

```js
{
  title: "Title",
  destructive: true,
  handler: sender => {}
}
```

# 子菜单

当一个菜单项包含 `items` 时，会被收纳为一个子菜单：

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

这个子菜单点击之后会显示两个二级选项，子菜单可以多层嵌套。

# Inline 子菜单

上述子菜单将会把菜单项作为二级菜单显示，也可以将其直接显示到当前菜单，用分割线隔开，只需设置 `inline` 属性：

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

# list 和 matrix

可以为 `list` 和 `matrix` 的某一行或某一个元素提供长按菜单，在这种情况下 `handler` 将会携带 `indexPath` 信息：

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

这种场景类似于其 `event: didSelect`，只是触发方式是通过长按某一个元素。

# Pull-Down 菜单

作为 iOS 14 的主要改进之一，您可以为 `button` 和 `navButtons` 提供更现代化的 [Pull-Down](https://developer.apple.com/design/human-interface-guidelines/ios/controls/buttons/) 菜单选项。`Pull-Down` 菜单不会将背景模糊，并可以作为主要菜单触发，无需长按。

为 `button` 类型支持 Pull-Down 菜单，仅需在上述配置中增加 `pullDown: true` 参数：

```js
$ui.render({
  views: [
    {
      type: "button",
      props: {
        title: "Long Press!",
        menu: {
          title: "Context Menu",
          pullDown: true,
          asPrimary: true,
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

为 `navButtons` 支持 Pull-Down 菜单也类似，仅需使用 `menu` 参数：

```js
$ui.render({
  props: {
    navButtons: [
      {
        title: "Title",
        symbol: "checkmark.seal",
        menu: {
          title: "Context Menu",
          asPrimary: true,
          items: [
            {
              title: "Title",
              handler: sender => {}
            }
          ]
        }
      }
    ]
  }
});
```

上述参数中，`asPrimary` 表示是否作为一级操作，也即短按触发。