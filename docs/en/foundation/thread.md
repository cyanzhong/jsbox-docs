> This topic including thread switching, after delay and timer

# $thread.background(object)

Run on background thread:

```js
$thread.background({
  delay: 0,
  handler: function() {

  }
})
```

# $thread.main(object)

Run on main thread (with delay):

```js
$thread.main({
  delay: 0.3,
  handler: function() {
    
  }
})
```

Param | Type | Description
---|---|---
delay | number | delay (seconds)
handler | function | handler

It can be simplifies as below if no delay is needed:

```js
$thread.main(() => {
  
});
```

# $delay(number, function)

Run after delay easily:

```js
$delay(3, function() {
  $ui.alert("Hey!")
})
```

Present an alert after 3 seconds.

You can cancel the task by:

```js
var task = $delay(10, function() {

})

// Cancel it
task.cancel();
```

# $wait(sec)

It's similar to $delay but Promise is supported:

```js
await $wait(2);

alert("Hey!");
```

# $timer.schedule(object)

Schedule a timer:

```js
var timer = $timer.schedule({
  interval: 3,
  handler: function() {
    $ui.toast("Hey!")
  }
})
```

Show a toast "Hey!" in every 3 seconds, cancel it by:

```js
timer.invalidate()
```