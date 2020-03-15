> iOS animation is awesome, JSBox provides two ways to implement animations

# UIView animation

The most simple way is use `$ui.animate`:

```js
$ui.animate({
  duration: 0.4,
  animation: function() {
    $("label").alpha = 0
  },
  completion: function() {
    $("label").remove()
  }
})
```

This code changes alpha value of the label to 0 in 0.4 seconds, then remove this view.

Yes, you just need to put your code inside `animation`, everything works like magic.

You can create a `spring animation` by set:

Param | Type | Description
---|---|---
delay | number | delay
damping | number | damping
velocity | number | initial value
options | number | [Refer](https://developer.apple.com/documentation/uikit/uiviewanimationoptions)

# Chainable

We also introduced a chainable API based on [JHChainableAnimations](https://github.com/jhurray/JHChainableAnimations):

```js
$("label").animator.makeBackground($color("red")).easeIn.animate(0.5)
```

We could do same effect with a much cleaner syntax, just use an animator.

For more details, please refer to the official docs of [JHChainableAnimations](https://github.com/jhurray/JHChainableAnimations).

> It is no longer recommended, because that project is not being maintained actively