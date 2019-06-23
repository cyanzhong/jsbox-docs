# type: "picker"

`picker` 用于创建一个通用的数据选择器：

```js
{
  type: "picker",
  props: {
    items: Array(3).fill(Array.from(Array(256).keys()))
  },
  layout: function(make) {
    make.left.top.right.equalTo(0)
  }
}
```

上述代码会创建一个用于选择 RGB 颜色的三个滚轮，他们之间彼此的滚动是独立的。

除此之外，你也可以创建具有`级联（cascade）`关系的选择器，类似于级联表单，在创建的时候指定 `items` 的方式有所不同：

```js
items: [
  {
    title: "Language",
    items: [
      {
        title: "Web",
        items: [
          {
            title: "JavaScript"
          },
          {
            title: "PHP"
          }
        ]
      },
      {
        title: "Client",
        items: [
          {
            title: "Swift"
          },
          {
            title: "Objective-C"
          }
        ]
      }
    ]
  },
  {
    title: "Framework",
    // ...
  }
]
```

显而易见这是一个递归的结构，当用户选择了某个 `title` 之后，将会更新下一级滚轮的 `items`，要理解这个控件首先要理解级联的含义。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
data | object | 只读 | 选中的所有项
selectedRows | object | 只读 | 选中的所有序号

# events: changed

`changed` 事件在当前值变化时回调：

```js
changed: function(sender) {
  
}
```

# $picker.date(object)

创建一个日期选择器的快捷方式，参数和上面的方式相同，picker 将会直接从屏幕底部弹出。

# $picker.data(object)

创建一个通用选择器的快捷方式，参数和上面的方式相同，picker 将会直接从屏幕底部弹出。