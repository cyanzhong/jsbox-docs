> 和 JSBox 本身相关或和正在运行的脚本相关的接口

# $app.theme

为脚本指定 `theme`，用于 [Dark Mode](uikit/dark-mode.md) 相关，可选值为 `light` / `dark` / `auto`。

如果某个页面指定了 `theme`，则这个全局的值会被覆盖。

# $app.minSDKVer

指定此扩展可用的最低 SDK 版本（SDK 版本即 JSBox 的版本）：

```js
$app.minSDKVer = "3.1.0"
```

# $app.minOSVer

指定此扩展可用的最低 iOS 版本：

```js
$app.minOSVer = "10.3.3"
```

注：版本号都是小数点分割的两个数字或三个数字，从前往后依次比较大小。

# $app.tips(string)

给用户展示一个使用提示，效果如同 `$ui.alert`，但请注意这个提示只会运行一次：

```js
$app.tips("在 App Store 内通过分享面板使用")
```

# $app.info

返回 app 本身的信息，例如：

```js
{
  "bundleID": "app.cyan.jsbox",
  "version": "3.0.0",
  "build": "9527",
}
```

# $app.idleTimerDisabled

设置成 true 时屏幕不会自动休眠：

```js
$app.idleTimerDisabled = true
```

# $app.close(delay)

关闭当前的扩展，请注意扩展被关闭之后的代码都不会再被执行。

`delay` 表示延迟的秒数，可以缺省，缺省即立即关闭。

> 注：当一个扩展没有界面时，建议在逻辑完成之后手动调用 $app.close()，这样可以把引擎关闭。

# $app.env

获得此扩展当前运行的环境：

```js
var env = $app.env
```

参数 | 说明
---|---
$env.app | 主应用
$env.today | 通知中心小组件
$env.action | Action 扩展
$env.safari | Safari 扩展
$env.keyboard | 键盘扩展
$env.siri | Siri 环境
$env.all | 所有环境（默认值）

我们可以如此来判断扩展是否运行在通知中心：

```js
if ($app.env == $env.today) {

}
```

# $app.widgetIndex

因为 JSBox 支持多个小组件，你可以通过这个值判断哪个小组件正在被使用：

```js
var index = $app.widgetIndex;

// 0 ~ 2，其他值表示不是小组件
```

# $app.autoKeyboardEnabled

在某些滚动列表里面，可能会出现键盘遮挡住输入框的情况，开启之后将会自动避免这个问题：

```js
$app.autoKeyboardEnabled = true
```

# $app.keyboardToolbarEnabled

同样在滚动列表里，为键盘展示一个工具栏将会让输入更加方便，尤其是对于多个输入框：

```js
$app.keyboardToolbarEnabled = true
```

# $app.rotateDisabled

设置为 true 时屏幕将不可以旋转：

```js
$app.rotateDisabled = true
```

# $app.openURL(string)

打开一个 URL，例如打开微信：

```js
$app.openURL("weixin://")
```

# $app.openBrowser(object)

在用户安装了某个浏览器的情况下，通过某个浏览器打开 URL，例如：

```js
$app.openBrowser({
  type: 10000,
  url: "https://apple.com"
})
```

type | 浏览器
---|---
10000 | Chrome
10001 | UC
10002 | Firefox
10003 | QQ
10004 | Opera
10005 | Quark
10006 | iCab
10007 | Maxthon
10008 | Dolphin
10009 | 2345

> 由于各浏览器频繁改动其接口，上述接口并不保证能正确运行。

# $app.openExtension(string)

打开另一个已安装的 JSBox 脚本，例如：

```js
$app.openExtension("demo.js")
```

# $app.listen(object)

监听消息，目前支持 `ready` 和 `exit` 等：

```js
$app.listen({
  // 在应用启动之后调用
  ready: function() {

  },
  // 在应用退出之前调用
  exit: function() {
    
  },
  // 在应用停止响应后调用
  pause: function() {

  },
  // 在应用恢复响应后调用
  resume: function() {

  }
});
```

# $app.notify(object)

发出一个自定义的消息，可被 listen 接收：

```js
$app.listen({
  eventName: function(object) {
    console.log(object);
  }
});

$app.notify({
  name: "eventName",
  object: {"a": "b"}
});
```