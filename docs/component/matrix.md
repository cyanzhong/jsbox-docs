# type: "matrix"

`matrix` 用于创建一个矩阵：

```js
{
  type: "matrix",
  props: {
    columns: 4,
    itemHeight: 88,
    spacing: 5,
    template: {
      props: {},
      views: [
        {
          type: "label",
          props: {
            id: "label",
            bgcolor: $color("#474b51"),
            textColor: $color("#abb2bf"),
            align: $align.center,
            font: $font(32)
          },
          layout: $layout.fill
        }
      ]
    }
  },
  layout: $layout.fill
}
```

实际上，写过 iOS 的朋友应该知道，在 iOS 原生控件里面，上面提到的 `list` 其实是 `UITableView`，但是我觉得 tableView 这个名字起得不好，明明只能是单列的，所以在 JSBox 里面就叫 list。

在 iOS 6 的时候 Apple 引入了 `UICollectionView` 用于实现类似网格的布局。

`collection` 这个单词太长了，而 `grid` 又不够酷，所以在 JSBox 里面网格布局称为 `matrix`，这也是电影黑客帝国的英文名。

和 list 的构造和逻辑基本一样，但是布局策略稍有不同，因为是矩阵的形式，所以多了 `itemSize`, `spacing` 和 `columns` 等概念。

同样，matrix 也是支持单 section 和多 section 的构造形式，虽然在大部分时候我们用一个 section 就够了。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
data | object | 读写 | 数据源
spacing | number | 只写 | 方块边距
itemSize | $size | 只写 | 方块大小
columns | number | 只写 | 列数
square | boolean | 只写 | 是否正方形
direction | number | 只写 | 0: 纵向滚动 1: 横向滚动
selectable | boolean | 读写 | 是否可被选中
waterfall | boolean | 只写 | 是否瀑布流布局

# header & footer

`header` 和 `footer` 是放在头部和尾部的自定义 view，是可选项（在 props 里）：

```js
footer: {
  type: "label",
  props: {
    height: 20,
    text: "Write the Code. Change the world.",
    textColor: $color("#AAAAAA"),
    align: $align.center,
    font: $font(12)
  }
}
```

请在 props 里面指定他的高度 `height`。

# object($indexPath)

返回在 indexPath 位置的数据：

```js
var data = matrix.object($indexPath(0, 0))
```

# insert(object)

插入新的数据：

```js
// indexPath 和 index 可选其一
matrix.insert({
  indexPath: $indexPath(0, 0),
  value: {

  }
})
```

# delete(object)

删除一个数据：

```js
// 参数可以是 indexPath 或 index
matrix.delete($indexPath(0, 0))
```

# cell($indexPath)

返回在 indexPath 位置的元素：

```js
var cell = matrix.cell($indexPath(0, 0))
```

# events: didSelect

`didSelect` 事件在元素被点击时回调：

```js
didSelect: function(sender, indexPath, data) {

}
```

# events: didLongPress

`didLongPress` 在长按某一行时回调：

```js
didLongPress: function(sender, indexPath, data) {

}
```

同样的，matrix 也是继承自 `scroll`，所以也具有 scroll 的全部回调事件。

# events: forEachItem

按照顺序获得矩阵的每一项：

```js
forEachItem: function(view, indexPath) {
  
}
```

# events: highlighted

自定义高亮效果：

```js
highlighted: function(view) {

}
```

# events: itemSize

设置动态的 item 大小：

```js
itemSize: function(sender, indexPath) {
  var index = indexPath.item + 1;
  return $size(40 * index, 40 * index);
}
```

# scrollTo

滚动到某个元素：

```js
$("matrix").scrollTo({
  indexPath: $indexPath(0, 0),
  animated: true // 默认为 true
})
```

# 长按排序

matrix 组件支持让用户通过长按来进行排序，需要实现以下内容：

首先需要在 `props` 里面设置 `reorder: true` 来打开这个功能：

```js
props: {
  reorder: true
}
```

其次，matrix 组件提供了三个方法来对用户排序的结果进行处理：

用户触发了长按排序操作：

```js
reorderBegan: function(indexPath) {

}
```

用户把一个项目从 `fromIndex` 移动到了 `toIndex`:

```js
reorderMoved: function(fromIndexPath, toIndexPath) {
  // Reorder your data source here
}
```

用户结束了重新排序：

```js
reorderFinished: function(data) {
  // Save your data source here
}
```

可以通过 `canMoveItem` 来决定是否能被移动：

```js
canMoveItem: function(sender, indexPath) {
  return indexPath.row > 0;
}
```

上述代码将会使得除了第一个以外的内容都可以被长按排序。

简单说，我们通常需要在 `reorderMoved` 和 `reorderFinished` 里面对 `data` 进行一些处理。