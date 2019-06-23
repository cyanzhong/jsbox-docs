> 和 iOS 系统本身相关的接口

# $system.brightness

设置屏幕，例如：

```js
$system.brightness = 0.5
```

# $system.volume

获取或设置设备音量 (0.0 ~ 1.0)：

```js
$system.volume = 0.5
```

# $system.call(number)

拨打电话，效果等同于 `$app.openURL("tel:number")`。

# $system.sms(number)

发送短信，效果等同于 `$app.openURL("sms:number")`。

# $system.mailto(email)

发送邮件，效果等同于 `$app.openURL("mailto:email")`。

# $system.facetime(number)

FaceTime，效果等同于 `$app.openURL("facetime:number")`。

# $system.makeIcon(object)

为链接创建一个桌面图标：

```js
$system.makeIcon({
  title: "Title",
  url: "https://sspai.com",
  icon: image
})
```