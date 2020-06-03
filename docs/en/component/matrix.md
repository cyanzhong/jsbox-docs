# type: "matrix"

`matrix` is designed to show a grid view:

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

Why we call it `matrix` instead of `grid` or `collection`?

Because `collection` looks so long and `grid` looks not cool.

The most important is, `The Matrix` is one of my favourite movie!

You can consider matrix is a special list with multiple columns anyway.

# props

Prop | Type | Read/Write | Description
---|---|---|---
data | object | rw | data source
spacing | number | w | spacing between items
itemSize | $size | w | item size of each item
autoItemSize | boolean | w | whether auto sizing
estimatedItemSize | $size | w | estimated item size
columns | number | w | column numbers
square | boolean | w | is square
direction | $scrollDirection | w | .vertical: vertically .horizontal: horizontally
selectable | boolean | rw | is selectable
waterfall | boolean | w | whether a waterfall layout (Pinterest-like)

# header & footer

`header` and `footer` are views, they are attached at the top/bottom of a matrix:

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

For fixed height, please specify the `height` manually in `props`. For dynamic height, provide a `height` function in its `events`:

```js
footer: {
  type: "label",
  props: {
    text: "Write the Code. Change the world."
  },
  events: {
    height: sender => {
      return _height;
    }
  }
}
```

When you want to change the height, update the `_height` value in the above example, then call `matrix.reload()` to trigger the update. For horizontal views, use `width` instead of `height` to specify its width.

# object($indexPath)

Returns the item data at indexPath:

```js
var data = matrix.object($indexPath(0, 0))
```

# insert(object)

Insert new data to matrix:

```js
// Either indexPath or index is fine
matrix.insert({
  indexPath: $indexPath(0, 0),
  value: {

  }
})
```

# delete(object)

Delete a item at indexPath or index:

```js
// object could be either indexPath or index
matrix.delete($indexPath(0, 0))
```

# cell($indexPath)

Returns the cell at indexPath:

```js
var cell = matrix.cell($indexPath(0, 0))
```

# events: didSelect

`didSelect` will be called once item selected:

```js
didSelect: function(sender, indexPath, data) {

}
```

# events: didLongPress

`didLongPress` will be called when cell is long pressed:

```js
didLongPress: function(sender, indexPath, data) {

}
```

Of course, matrix is a subclass of scroll view, same as list.

# events: forEachItem

Iterate all items:

```js
forEachItem: function(view, indexPath) {
  
}
```

# events: highlighted

Customize highlighted visual:

```js
highlighted: function(view) {

}
```

# events: itemSize

Provide dynamic item size:

```js
itemSize: function(sender, indexPath) {
  var index = indexPath.item + 1;
  return $size(40 * index, 40 * index);
}
```

# scrollTo

Scroll to a specific indexPath programmatically:

```js
$("matrix").scrollTo({
  indexPath: $indexPath(0, 0),
  animated: true // Default to true
})
```

# Auto sizing cells

Starting from v2.5.0, matrix view supports auto sizing, just set `autoItemSize` and `estimatedItemSize`, then provide proper layout constraints:

```js
const sentences = [
  "Although moreover mistaken kindness me feelings do be marianne.",
  "Effects present letters inquiry no an removed or friends. Desire behind latter me though in.",
  "He went such dare good mr fact.",
];

$ui.render({
  views: [
    {
      type: "matrix",
      props: {
        autoItemSize: true,
        estimatedItemSize: $size(120, 0),
        spacing: 10,
        template: {
          props: {
            bgcolor: $color("#F0F0F0")
          },
          views: [
            {
              type: "image",
              props: {
                symbol: "sun.dust"
              },
              layout: (make, view) => {
                make.centerX.equalTo(view.super);
                make.size.equalTo($size(24, 24));
                make.top.equalTo(10);
              }
            },
            {
              type: "label",
              props: {
                id: "label",
                lines: 0
              },
              layout: (make, view) => {
                make.left.bottom.inset(10);
                make.top.equalTo(44);
                make.width.equalTo(100);
              }
            }
          ]
        },
        data: sentences.map(text => {
          return {
            "label": {text}
          }
        })
      },
      layout: $layout.fill
    }
  ]
});
```

# Long press rows

Matrix view supports long press to reorder items, we need to turn on this feature:

```js
props: {
  reorder: true
}
```

In addition, we need to implement several methods:

Reorder action began:

```js
reorderBegan: function(indexPath) {

}
```

User moved a row:

```js
reorderMoved: function(fromIndexPath, toIndexPath) {
  // Reorder your data source here
}
```

User finished reordering:

```js
reorderFinished: function(data) {
  // Save your data source here
}
```

Decide whether it can be reordered by:

```js
canMoveItem: function(sender, indexPath) {
  return indexPath.row > 0;
}
```

It disables the first item's long press.

In short, we need to update data in `reorderMoved` and `reorderFinished`.