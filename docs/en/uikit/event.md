# Event handling

Starts from v1.49.0, we provide better event handling strategy for views, action can be connected after view is created. All iOS built-in control events are supported.

# view.whenTapped(handler)

Single tap action is triggered:

```js
button.whenTapped(() => {
  
});
```

# view.whenDoubleTapped(handler)

Double tap action is triggered:

```js
button.whenDoubleTapped(() => {
  
});
```

# view.whenTouched(args)

Customizable touch event is triggered:

```js
button.whenTouched({
  touches: 2,
  taps: 2,
  handler: () => {

  }
});
```

Above code will be executed for two fingers quickly tap twice.

If the button is a Runtime object (ocValue), here are two solutions:

```js
button.jsValue().whenTapped(() => {
  
});
```

Or, use $block instead:

```js
button.$whenTapped($block("void, void", () => {

}));
```

# view.addEventHandler(args)

Add custom event handlers:

```js
textField.addEventHandler({
  events: $UIEvent.editingChanged,
  handler: sender => {

  }
});
```

Note that: this only available on components like `button`, `text`, `input`, since they are UI controls, but it won't work on `image` like components. Full list of UI events can be found here: [$UIEvent](data/constant.md?id=uievent)

# view.removeEventHandlers(events)

Remove existing event handlers:

```js
textField.removeEventHandlers($UIEvent.editingChanged);
```

Of course, above code can be used in Runtime environment:

```js
textField.$addEventHandler({
  events: $UIEvent.editingChanged,
  handler: $block("void, id", sender => {
    
  })
});
```