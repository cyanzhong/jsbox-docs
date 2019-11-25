# Gesture

Gesture recognization on mobile is the most important innovation in last 10 years!

Let's see Steve introduces the 1st generation iPhone: https://www.youtube.com/watch?v=x7qPAY9JqE4.

iOS supports various gestures, such as tap, pinch, pan etc, currently JSBox supports few of them.

# events: tapped

Triggers when tap gesture received:

```js
tapped: function(sender) {

}
```

# events: longPressed

Triggers when long press gesture received:

```js
longPressed: function(info) {
  let sender = info.sender;
  let location = info.location;
}
```

# events: doubleTapped

Triggers when double tap gesture received:

```js
doubleTapped: function(sender) {

}
```


# events: touchesBegan

When touch event is triggered:

```js
touchesBegan: function(sender, location, locations) {

}
```

# events: touchesMoved

When touch is moving:

```js
touchesMoved: function(sender, location, locations) {

}
```

# events: touchesEnded

When touch event finished:

```js
touchesEnded: function(sender, location, locations) {

}
```