# 事件处理

从 v1.49.0 开始，我们引入了更为完善的事件处理机制，能够在视图生成之后对事件处理进行动态绑定，并且完整支持 iOS 内置的所有事件类型。

# view.whenTapped(handler)

当一个视图被按下时触发：

```js
button.whenTapped(() => {
  
});
```

# view.whenDoubleTapped(handler)

当一个视图被按下两次时触发：

```js
button.whenDoubleTapped(() => {
  
});
```

# view.whenTouched(args)

指定视图按下需要的触点个数和按下次数：

```js
button.whenTouched({
  touches: 2,
  taps: 2,
  handler: () => {

  }
});
```

上述代码在视图两指双击的状况下触发。

如果 button 是一个 Runtime 环境下的对象 (ocValue)，可以通过以下两种方式绑定事件：

```js
button.jsValue().whenTapped(() => {
  
});
```

或者使用 $block:

```js
button.$whenTapped($block("void, void", () => {

}));
```

# view.addEventHandler(args)

为视图添加自定义的事件响应：

```js
textField.addEventHandler({
  events: $UIEvent.editingChanged,
  handler: sender => {

  }
});
```

注意：此方法只能用于 `button`, `text`, `input` 等本身就支持事件响应的 UI controls，而对于 `image` 一类的视图则不支持。完整的事件类型请查看：[$UIEvent](data/constant.md?id=uievent)

# view.removeEventHandlers(events)

移除视图上已添加的事件：

```js
textField.removeEventHandlers($UIEvent.editingChanged);
```

同样的，上述代码也可以在 Runtime 环境使用：

```js
textField.$addEventHandler({
  events: $UIEvent.editingChanged,
  handler: $block("void, id", sender => {
    
  })
});
```