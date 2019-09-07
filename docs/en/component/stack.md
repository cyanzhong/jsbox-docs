# type: "stack"

A special view that doesn't render anything, it's designed for laying out a collection of views.

Note that, stack view in JSBox is based on `UIStackView`, in order to understand how it works, you should take a look at Apple's documentation first: https://developer.apple.com/documentation/uikit/uistackview

# Overview

Here is a simple demo which creates a stack view:

```js
$ui.render({
  views: [
    {
      type: "stack",
      props: {
        spacing: 10,
        distribution: $stackViewDistribution.fillEqually,
        stack: {
          views: [
            {
              type: "label",
              props: {
                text: "Left",
                align: $align.center,
                bgcolor: $color("silver")
              }
            },
            {
              type: "label",
              props: {
                text: "Center",
                align: $align.center,
                bgcolor: $color("aqua")
              }
            },
            {
              type: "label",
              props: {
                text: "Right",
                align: $align.center,
                bgcolor: $color("lime")
              }
            }
          ]
        }
      },
      layout: $layout.fill
    }
  ]
});
```

If you want to arrange some views in a stack view, you should put them inside the `stack` prop, not directly under the `views` prop.

Also, you can control the layout with some properties, such as `axis`, `distribution`, `alignment`, and `spacing`.

# props: axis

The `axis` property determines the stack’s orientation, either vertically or horizontally.

Possible values:

```js
- $stackViewAxis.horizontal
- $stackViewAxis.vertical
```

# props: distribution

The `distribution` property determines the layout of the arranged views along the stack’s axis.

Possible values:

```js
- $stackViewDistribution.fill
- $stackViewDistribution.fillEqually
- $stackViewDistribution.fillProportionally
- $stackViewDistribution.equalSpacing
- $stackViewDistribution.equalCentering
```

# props: alignment

The `alignment` property determines the layout of the arranged views perpendicular to the stack’s axis.

Possible values:

```js
- $stackViewAlignment.fill
- $stackViewAlignment.leading
- $stackViewAlignment.top
- $stackViewAlignment.firstBaseline
- $stackViewAlignment.center
- $stackViewAlignment.trailing
- $stackViewAlignment.bottom
- $stackViewAlignment.lastBaseline
```

# props: spacing

The `spacing` property determines the minimum spacing between arranged views, should be a number.

You can also use the these two constants:

```js
- $stackViewSpacing.useDefault
- $stackViewSpacing.useSystem
```

# props: isBaselineRelative

The `isBaselineRelative` property determines whether the vertical spacing between views is measured from the baselines, should be a boolean value.

# props: isLayoutMarginsRelative

The `isLayoutMarginsRelative` property determines whether the stack view lays out its arranged views relative to its layout margins, should be a boolean value.

# Change a view dynamically

After arranged views initialized, you can change them dynamically like this:

```js
const stackView = $("stackView");
const views = stackView.stack.views;
views[0].hidden = true;

// This hides the first view in the stack
```

# Add a view

Other than initiate a stack view with `stack.views`, you can also append a view dynamically like this:

```js
const stackView = $("stackView");
stackView.stack.add(newView);

// newView can be created with $ui.create
```

# Remove a view

Remove a view from a stack:

```js
const stackView = $("stackView");
stackView.stack.remove(existingView);

// existingView can be retrieved with id
```

# Insert a view

Insert a new view into a stack, with index:

```js
const stackView = $("stackView");
stackView.stack.insert(newView, 2);
```

# Set spacing after a view

While stack view manages spacing automatically, you can specify custom spacing after a view:

```js
const stackView = $("stackView");
stackView.stack.setSpacingAfterView(arrangedView, 20);

// arrangedView must be a view that is contained in the stack
```

# Get spacing after a view

Get custom spacing after a particular view:

```js
const stackView = $("stackView");
const spacing = stackView.stack.spacingAfterView(arrangedView);

// arrangedView must be a view that is contained in the stack
```

# Demo

It's hard to understand stack views, since it's a bit more complicated than other view types.

We have built an example that shows you how do those properties work, you can check it out: https://github.com/cyanzhong/xTeko/blob/master/extension-demos/stack-view