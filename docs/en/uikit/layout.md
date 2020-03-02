> Layout is a series of constraints to determine the size and position of views

# Layout System

Layout is very important in a UI system, different platform has different design, for example [Auto Layout](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/index.html) in iOS, and [Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes) which is used widely in web applications.

In short: size & position.

*PS: This part is a little bit complicated, but it is also very important.*

In the early iOS, due to the limitation of screen, iOS only provides frame based layout. It's based on absolute position and size, so you can set `frame` in `props` as well (not recommend).

Because frame layout is clumsy:

- Hard to calculate, the ability is poor
- Need to know super view's size, won't update automatically
- Can not make sure everthing is fine on different screens

Use auto layout as much as you can, as an iOS developer I will tell you auto layout is much better than frame layout.

When you are using frame layout, you can use events->layoutSubview to retrieve super view's frame:

```js
$ui.render({
  views: [
    {
      type: "view",
      layout: $layout.fill,
      events: {
        layoutSubviews: function(view) {
          console.log("frame: " + JSON.stringify(view.frame))
        }
      }
    }
  ]
})
```

# Basic Concept

We are trying to describe auto layout with most simple words:

> Create some constraints in a view tree, to describe relationship between each views, for example super view, children and siblings

Constraints need to be complete, for example:

- The height is 40
- The relative position to super view is (10, 10)
- The training margin to super view is 10

We don't know the width of this view, but this view's layout is complete.

No matter how the screen looks, we can always have a view, the relationship is clear enough:

```js
layout: function(make) {
  make.height.equalTo(40)
  make.left.top.right.inset(10)
}
```

You can use `view` itself by:

```js
layout: function(make, view) {
  make.height.equalTo(40)
  make.width.equalTo(view.height)
}
```

In case you want to get the width/height, or `view.super`.

# What's constraint?

Basically it is a value to describe a relationship of a property.

The property could be top/bottom/left/right, the relationship could be equalTo/offset etc.

In short, constraint is property and relationship combined.

# Properties

Like we mentioned before, `height` and `left` are relationship, here are more examples, you can refer: [Masonry](https://github.com/SnapKit/Masonry) to check out all of them.

Prop | Description
---|---
width | width
height | height
size | size
center | center
centerX | x center
centerY | y center
left | left side
top | top side
right | right side
bottom | bottom side
leading | leadin
trailing | trailing
edges | 4 edges

Please note sometimes we need to support RTL (Right to Left) languages, consider use leading/trailing in that case.

# Relations

Describe relationship between two views, such as `equalTo`, `offset`：

Relation | Description
---|---
equalTo(object) | ==
greaterThanOrEqualTo(object) | >=
lessThanOrEqualTo(object) | <=
offset(number) | offset by
inset(number) | inset by
insets($insets) | edge insets
multipliedBy(number) | multiplied by
dividedBy(number) | divided by
priority(number) | set priority

We can create constraints with chainable syntax:

```js
layout: function(make) {
  make.left.equalTo($("label").right).offset(10)
  make.bottom.inset(0)
  make.size.equalTo($size(40, 40))
}
```

This view is 40x40pt, align to the bottom of its super view, and at the right of `label` with a small offset.

We have to know, layout is not an easy task, there's no best solution for all situations. Auto Layout has its disadvantages too.

However, understand concept above is enough to handle most cases, please check documents when you need:

[Masonry](https://github.com/SnapKit/Masonry) [Apple](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/index.html).

This document is still under construction, we will provide more examples soon.

# Flex

Sometimes, auto resizing is enough for you, you can use view's `flex` property:

```js
$ui.render({
  views: [
    {
      type: "view",
      props: {
        bgcolor: $color("red"),
        frame: $rect(0, 0, 0, 100),
        flex: "W"
      }
    }
  ]
});
```

This creates a view which has the same width as its parent, and the height is 100. The `flex` property is a string, acceptable characters are:

- `L`: [UIViewAutoresizingFlexibleLeftMargin](https://developer.apple.com/documentation/uikit/uiviewautoresizing/uiviewautoresizingflexibleleftmargin?language=objc)
- `W`: [UIViewAutoresizingFlexibleWidth](https://developer.apple.com/documentation/uikit/uiviewautoresizing/uiviewautoresizingflexiblewidth?language=objc)
- `R`: [UIViewAutoresizingFlexibleRightMargin](https://developer.apple.com/documentation/uikit/uiviewautoresizing/uiviewautoresizingflexiblerightmargin?language=objc)
- `T`: [UIViewAutoresizingFlexibleTopMargin](https://developer.apple.com/documentation/uikit/uiviewautoresizing/uiviewautoresizingflexibletopmargin?language=objc)
- `H`: [UIViewAutoresizingFlexibleHeight](https://developer.apple.com/documentation/uikit/uiviewautoresizing/uiviewautoresizingflexibleheight?language=objc)
- `B`: [UIViewAutoresizingFlexibleBottomMargin](https://developer.apple.com/documentation/uikit/uiviewautoresizing/uiviewautoresizingflexiblebottommargin?language=objc)

For example, using "LRTB" to describe `UIViewAutoresizingFlexibleLeftMargin | UIViewAutoresizingFlexibleRightMargin | UIViewAutoresizingFlexibleTopMargin | UIViewAutoresizingFlexibleBottomMargin`.