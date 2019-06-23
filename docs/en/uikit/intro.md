# Basic Concept

In JSBox, build user interface is very easy, the only thing you need to provide is a JavaScript object, we actually based on [UIKit](https://developer.apple.com/documentation/uikit), but it's much easier, works like magic.

Unlike [React Native](https://facebook.github.io/react-native/) and [Weex](https://weex.incubator.apache.org/), you don't need to know `HTML` and `CSS`, JavaScript is enough to create delightful UI.

PS: Your can run without any user interface, absolutely.

# Example

Like we mentioned before, we can create a button with following code:

```js
$ui.render({
  views: [
    {
      type: "button",
      props: {
        title: "Button"
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
})
```

This is very small but included all concept we needed to create UI: `type`, `props`, `layout` and `events`.

# type

To specify view's type, such as `button` and `label`, they are work different.

# props

It means properties, or attributes of a view. For example `title` in button, different view has different props, we will explain all of them later. 

# layout

In short, layout is used to determine the location and size of a view.

JSBox uses [Auto Layout](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/index.html) as layout system, you don't need to fully understand how it works, because we provided a solution based on a third party framework: [Masonry](https://github.com/SnapKit/Masonry).

Masonry is very easy to use, we have several examples later.

PS: we are considering support more layout systems in the future, for example [Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes).

# events

Provide events here, for example `tapped` in button, we will show different events supported by different views soon.

# views

It's an array to provided its subviews (children):

```js
{
  views: [

  ]
}
```

Yes, a view system is actually works like a tree, trees have theirs children.