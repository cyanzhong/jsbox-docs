# type: "list"

`list` is the most complicated control in JSBox, it used to arrange a series of views:

```js
{
  type: "list",
  props: {
    data: ["JavaScript", "Swift"]
  },
  layout: $layout.fill,
}
```

It creates a list with only one section, each row inside is a label.

If you want to create a list with multiple sections, you need to:

```js
{
  type: "list",
  props: {
    data: [
      {
        title: "Section 0",
        rows: ["0-0", "0-1", "0-2"]
      },
      {
        title: "Section 1",
        rows: ["1-0", "1-1", "1-2"]
      }
    ]
  },
  layout: $layout.fill,
}
```

It creates 2 sections, each section has 3 rows, choose what you want.

Above samples are plain text list, actually list cells could be customized, we call it `template`:

```js
template: {
  props: {
    bgcolor: $color("clear")
  },
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
```

Views in template is just a common view like you know in `$ui.render`.

Now you could construct your `data` as:

```js
data: [
  {
    label: {
      text: "Hello"
    }
  },
  {
    label: {
      text: "World"
    }
  }
]
```

While rendering a row, JSBox searches each view by `id`, then configures all properties.

With `template` and `data`, we almost can implement any style if we want, and don't forget, we also can use multiple sections with templates.

# header & footer

`header` and `footer` are views, they are attached at the top/bottom of a list:

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

Note: please specify the `height` manually in props.

# Static cells

Cells in template are reused by iOS automatically, sometimes you want to static data to render them.

JSBox could do that for you, you just need to put your view in `data`:

```js
data: [
  {
    title: "System (Text)",
    rows: [
      {
        type: "button",
        props: {
          title: "Button",
          selectable: false
        },
        layout: function(make, view) {
          make.center.equalTo(view.super)
          make.width.equalTo(64)
        },
        events: {
          tapped: function(sender) {
            $ui.toast("Tapped")
          }
        }
      }
    ]
  },
  {
    title: "System (Contact Add)",
    rows: [
      {
        type: "button",
        props: {
          type: 5
        },
        layout: $layout.center
      }
    ]
  }
]
```

It creates some static cells, instead of reuse them dynamically.

The `selectable` property indicates whether the cell is selectable, default to false.

# props

Prop | Type | Read/Write | Description
---|---|---|---
style | number | w | style 0 ~ 2
data | object | rw | data source
separatorInset | $insets | rw | separator inset
separatorHidden | boolean | rw | hide separator
separatorColor | $color | rw | separator color
header | object | rw | header view
footer | object | rw | footer view
rowHeight | number | w | row height
autoRowHeight | boolean | w | whether auto sizing
estimatedRowHeight | number | w | estimated row height
sectionTitleHeight | number | w | section title height
selectable | bool | w | is row selectable
stickyHeader | boolean | w | section/header are sticky
reorder | boolean | rw | whether can be reordered
crossSections | boolean | rw | whether recorder can cross sections
hasActiveAction | boolean | r | whether an action is being used

# props: actions

`actions` is designed to provide swipe actions:

```js
actions: [
  {
    title: "delete",
    color: $color("gray"), // default to gray
    handler: function(sender, indexPath) {

    }
  },
  {
    title: "share",
    handler: function(sender, indexPath) {

    }
  }
]
```

It creates 2 swipe actions, named `delete` and `share`.

Use `swipeEnabled` to decide whether users can swipe a row:

```js
swipeEnabled: function(sender, indexPath) {
  return indexPath.row > 0;
}
```

That means the first row can't be swiped.

# object($indexPath)

Returns the row data at indexPath:

```js
var data = tableView.object($indexPath(0, 0))
```

# insert(object)

Insert new data at indexPath or index:

```js
// Either indexPath or index, the value shoule be a row data
tableView.insert({
  indexPath: $indexPath(0, 0),
  value: "Hey!"
})
```

# delete(object)

Delete a row at indexPath or index:

```js
// object could be indexPath or index
tableView.delete(0)
```

# cell($indexPath)

Returns the cell at indexPath (might be null):

```js
var cell = tableView.cell($indexPath(0, 0))
```

# events: rowHeight

We could specify row height dynamically by making the `rowHeight` a function:

```js
rowHeight: function(sender, indexPath) {
  if (indexPath.row == 0) {
    return 88.0
  } else {
    return 44.0
  }
}
```

# events: sectionTitleHeight

We could specify section title height dynamically by making the `sectionTitleHeight` a function:

```js
sectionTitleHeight: (sender, section) => {
  if (section == 0) {
    return 30;
  } else {
    return 40;
  }
}
```

# events: didSelect

`didSelect` will be called once a row selected:

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

# events: forEachItem

Iterate all items:

```js
forEachItem: function(view, indexPath) {
  
}
```

# Auto sizing cells

In many cases, we want to calculate row height manually. For example, we want to display sentences that have different length.

Starting from v2.5.0, list view supports auto sizing, just set `autoRowHeight` and `estimatedRowHeight`, then provide proper layout constraints:

```js
const sentences = [
  "Although moreover mistaken kindness me feelings do be marianne.",
  "Effects present letters inquiry no an removed or friends. Desire behind latter me though in. Supposing shameless am he engrossed up additions. My possible peculiar together to. Desire so better am cannot he up before points. Remember mistaken opinions it pleasure of debating. Court front maids forty if aware their at. Chicken use are pressed removed.",
  "He went such dare good mr fact. The small own seven saved man age ﻿no offer. Suspicion did mrs nor furniture smallness. Scale whole downs often leave not eat. An expression reasonably cultivated indulgence mr he surrounded instrument. Gentleman eat and consisted are pronounce distrusts.",
];

$ui.render({
  views: [
    {
      type: "list",
      props: {
        autoRowHeight: true,
        estimatedRowHeight: 44,
        template: [
          {
            type: "image",
            props: {
              id: "icon",
              symbol: "text.bubble"
            },
            layout: (make, view) => {
              make.left.equalTo(10);
              make.size.equalTo($size(24, 24));
              make.centerY.equalTo(view.super);
            }
          },
          {
            type: "label",
            props: {
              id: "label",
              lines: 0
            },
            layout: (make, view) => {
              const insets = $insets(10, 44, 10, 10);
              make.edges.equalTo(view.super).insets(insets);
            }
          }
        ],
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

For simple list that shows strings, also supports auto-sizing:

```js
const sentences = [
  "Although moreover mistaken kindness me feelings do be marianne.",
  "Effects present letters inquiry no an removed or friends. Desire behind latter me though in. Supposing shameless am he engrossed up additions. My possible peculiar together to. Desire so better am cannot he up before points. Remember mistaken opinions it pleasure of debating. Court front maids forty if aware their at. Chicken use are pressed removed.",
  "He went such dare good mr fact. The small own seven saved man age ﻿no offer. Suspicion did mrs nor furniture smallness. Scale whole downs often leave not eat. An expression reasonably cultivated indulgence mr he surrounded instrument. Gentleman eat and consisted are pronounce distrusts.",
];

$ui.render({
  views: [
    {
      type: "list",
      props: {
        autoRowHeight: true,
        data: sentences
      },
      layout: $layout.fill
    }
  ]
});
```

# Long press rows

List view supports long press to reorder items, we need to turn on this feature:

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

More example: https://github.com/cyanzhong/xTeko/blob/3ac0d3f5ac552a1c72ea39d0bd1099fd02f5ca70/extension-scripts/xteko-menu.js

# Paging

Let's see an example first:

```js
var data = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15"]
$ui.render({
  views: [
    {
      type: "list",
      props: { data: data },
      layout: $layout.fill,
      events: {
        didReachBottom: function(sender) {
          $ui.toast("fetching...")
          $delay(1.5, function() {
            sender.endFetchingMore()
            data = data.concat(data.map(function(item) {
              return (parseInt(item) + 15).toString()
            }))
            $("list").data = data
          })
        }
      }
    }
  ]
})
```

When list view reaches bottom, it triggers `didReachBottom` method, we load more data here.

When load more finished, we call `endFetchingMore` first to terminate the loading state, and update data source.

Finally, we setup the data back to the list view.

# setEditing

Set editing state programmatically:

```js
$("list").setEditing(false)
```

# scrollTo

Scroll to a specific indexPath programmatically:

```js
$("list").scrollTo({
  indexPath: $indexPath(0, 0),
  animated: true // Default is true
})
```

# One more thing

List views are subclasses of scroll view, they have all abilities inherited from scroll view.