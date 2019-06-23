> 控制台的使用和相关接口

# 前言

任何程序都会有 bug，这是 `debug` 存在的理由，JSBox 作为一个开发平台，应该提供各种查错的手段，这是一个需要长期优化的方向。

JSBox 里面引入了一个简单的 Console（控制台），可以用来输出日志，以及执行一些简单的代码。

# console

`console` 对象提供了以下几个方法用于向控制台输出内容：

```js
console.info("General Information")  // 输出通用信息
console.warn("Warning Message")      // 输出警告信息
console.error("Error Message")       // 输出错误信息
console.assert(false, "Message")     // Assertion
console.clear()                      // 清空控制台
console.open()                       // 打开控制台
console.close()                      // 关闭控制台
```

同时控制台也支持通过输入框执行一些代码，执行结果也将被展示到控制台。

另外，当 JavaScript 异常被捕获到的时候，异常信息将会以 `error` 的形式展示到控制台。

# 控制台使用方法

- 点击界面上的虫子按钮进入
- 点击某一行查看全文内容
- 长按某一行可以复制内容
- 底部输入框输入内容可以调试代码