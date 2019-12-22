> 在这里涉及到线程切换、延时执行、重复执行等内容。

# $thread.background(object)

在子线程执行一段代码：

```js
$thread.background({
  delay: 0,
  handler: function() {

  }
})
```

# $thread.main(object)

在主线程执行一段代码：

```js
$thread.main({
  delay: 0.3,
  handler: function() {
    
  }
})
```

参数 | 类型 | 说明
---|---|---
delay | number | 延迟执行的时间，可选
handler | function | 回调

如果不需要延迟执行，也可以简单地写为：

```js
$thread.main(() => {
  
});
```

# $delay(number, function)

一种更简单的执行延时任务的方法：

```js
$delay(3, function() {
  $ui.alert("Hey!")
})
```

3 秒钟后弹出一个 alert。

你可以通过这个方式取消执行：

```js
var task = $delay(10, function() {

})

// Cancel it
task.cancel();
```

# $wait(sec)

与 $delay 类似但支持 Promise:

```js
await $wait(2);

alert("Hey!");
```

# $timer.schedule(object)

用于执行一个重复的任务：

```js
var timer = $timer.schedule({
  interval: 3,
  handler: function() {
    $ui.toast("Hey!")
  }
})
```

上述代码每隔三秒显示一次 `Hey!`，已经设置的任务可以取消：

```js
timer.invalidate()
```