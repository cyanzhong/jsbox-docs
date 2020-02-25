> 以最简单的配置文件为脚本应用提供配置项

# prefs.json

从 v1.51.0 开始，你只需要在应用根目录配置一个 `prefs.json` 文件，JSBox 就可以自动为你生成配置页面，从而为用户提供更为友好的设置界面。

来看一个例子：

```json
{
  "title": "SETTINGS",
  "groups": [
    {
      "title": "GENERAL",
      "items": [
        {
          "title": "USER_NAME",
          "type": "string",
          "key": "user.name",
          "value": "default user name"
        },
        {
          "title": "AUTO_SAVE",
          "type": "boolean",
          "key": "auto.save",
          "value": true
        },
        {
          "title": "OTHERS",
          "type": "child",
          "value": {
            "title": "OTHERS",
            "groups": [
              
            ]
          }
        }
      ]
    }
  ]
}
```

调用下面的代码即可打开配置界面，以供用户设置：

```js
$prefs.open(() => {
  // Done
});
```

# 配置文件结构

配置文件的根节点是一个 `title` 和 `groups` 的 JSON 对象，`title` 会被设置为页面的标题，`groups` 数组则表示当前的设置页的所有分组。

在 `groups` 下面，是由分组标题 `title` 以及所有选项 `items` 组成的 JSON 对象，`items` 数组里面的每一项就是一个具体的设置项。

如果当前页面只有一个分组，也可以简写成：

```json
{
  "title": "GENERAL",
  "items": [
    {
      "title": "USER_NAME",
      "type": "string",
      "key": "user.name",
      "value": "default user name"
    }
  ]
}
```

配置项节点由下列内容组成：

- `title`: 标题，显示在左侧
- `type`: 类型，比如字符串或是布尔值，下面会详细介绍
- `key`: 存储以及获取设置用的键，需要保证脚本内全局无冲突
- `value`: 在用户没有设置的时候，提供的缺省值，可以不提供

# title

为了简化多语言环境下的配置，上述配置内容所有的 title 首先会从 `strings` 文件夹配置的字符串里面寻找本地化的字符串，如果没有，才使用字符串本身。

# type

目前配置文件支持下面的类型：

- `string`: 字符串类型，支持多行
- `number`: 浮点数类型
- `integer`: 整数类型
- `boolean`: 布尔值，在页面中显示为一个开关
- `slider`: 0 ~ 1 的浮点数，在页面中显示为一个滑块
- `list`: 用于在一个列表里面选择一个值
- `info`: 显示一个不可变的信息，比如版本号
- `link`: 显示一个链接，点击后会直接打开
- `script`: 可配置一段脚本，点击后会执行
- `child`: 子设置项，点击之后打开一个新的设置页面

对于 `string`, `number` 以及 `integer` 等较为简单的类型，尝试一下即可了解，下面会介绍比较不同的几个。

# type: "slider"

将会显示一个滑块，用于设置 0 ~ 1 之间的浮点数，所以默认值 `value` 也需要符合 0 ~ 1 的定义。

如果你在程序中需要的值不是 0 ~ 1 的数，你需要做一些简单的变换来映射到你的取值区间，请将这个滑块理解成一个百分比滑块。

# type: "list"

在一个列表里面选择一个值，例如：

```json
{
  "title": "IMAGE_QUALITY",
  "type": "list",
  "key": "image.quality",
  "items": ["LOW", "MEDIUM", "HIGH"],
  "value": 1
}
```

界面会让用户在 "LOW", "MEDIUM" 和 "HIGH" 里面选一个值，而 `value` 则是选择的 `index`。同样的，为了本地化的方便，`items` 里面的内容也会从 `strings` 文件夹里面优先取值。

请注意，`items` 仅仅是显示给用户的内容，并不会被存储，而 `value` 存储的实际上是序号。

# type: "script"

有些时候，你可能希望设置项的某一行点击之后是你自己定义的行为，这种类型就是为了这个目的：

```json
{
  "title": "TEST",
  "type": "script",
  "value": "require('scripts/test').runTest();"
}
```

# type: "child"

有些时候，你可能希望将一些不那么重要的设置项放到二级甚至是三级设置里面，你可以通过这个类型做到：

```json
{
  "title": "OTHERS",
  "type": "child",
  "value": {
    "title": "OTHERS",
    "groups": []
  }
}
```

上述节点的 `value` 正是设置页面根节点的结构，你可以把这个结构无限嵌套下去来实现多级设置。

# key

`key` 是用来保存和读取一个设置项用的键，需要保证在脚本内全局唯一。

读取设置：

```js
const name = $prefs.get("user.name");
```

在多数情况下，设置项都应该是由用户通过界面配置的，但为了保证灵活性，你仍然可以像这样主动更新一个设置项：

```js
$prefs.set("user.name", "cyan");
```

# $prefs.all()

返回所有的键值对：

```js
const prefs = $prefs.all();
```

`$prefs` 显然并不能够应对任何设置项，但对于大部分的需求来说以及完全能够满足，并且使用极为简单。这里有一个完整的例子：https://github.com/cyanzhong/xTeko/tree/master/extension-demos/prefs