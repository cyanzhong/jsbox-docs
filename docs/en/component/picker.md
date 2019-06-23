# type: "picker"

`picker` is used to display a general picker:

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

It shows a rgb wheel, each part of them is independent.

Besides, you could also create a `cascade` picker, each colum is related tightly: 

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

This is a recursive structure, when user select `title`, the next wheel will update its rows.

# props

Prop | Type | Read/Write | Description
---|---|---|---
data | object | r | all selected items
selectedRows | object | r | all selected rows

# events: changed

`changed` will be called once the selected item changed:

```js
changed: function(sender) {
  
}
```

# $picker.date(object)

We provided an easy way to popup a date picker with `$picker.date(object)`.

# $picker.data(object)

We also provided an easy way to popup a general picker with `$picker.data(object)`.

The parameter of these 2 methods are exactly same as we mentioned before.