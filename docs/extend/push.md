> 用于构建本地的推送通知，例如一段时间之后提醒

# $push.schedule(object)

设定一个本地推送消息：

```js
$push.schedule({
  title: "标题",
  body: "内容",
  delay: 5,
  handler: function(result) {
    var id = result.id
  }
})
```

将会在代码执行后 5 秒接收到一个本地推送消息。

参数 | 类型 | 说明
---|---|---
title | string | 标题
body | string | 内容
id | string | 标识符（可选）
sound | string | 声音
mute | bool | 是否静音
repeats | bool | 是否重复
script | string | 脚本名称
height | number | 3D Touch 页面高度
query | json | 额外参数，会被传递到 $context.query
attachments | array | 媒体文件，例如 ["assets/icon.png"]
renew | bool | 是否重复创建（固定通知）

上述样例代码是通过 delay 来触发一个通知，你也可以通过 date 来触发：

```js
var date = new Date()
date.setSeconds(date.getSeconds() + 10)

$push.schedule({
  title: "标题",
  body: "内容",
  date: date,
  handler: function(result) {
    var id = result.id
  }
})
```

除此之外，你还能设置一个基于地理位置触发的通知：

```js
$push.schedule({
  title: "标题",
  body: "内容",
  region: {
    lat: 0, // latitude
    lng: 0, // longitude
    radius: 1000, // meters
    notifyOnEntry: true, // notify on entry
    notifyOnExit: true // notify on exit
  }
})
```

该方法调用后会请求用户授权地理位置，若用户拒绝授权则推送不会成功。

从 v1.10.0 开始，$push 支持了通过 script 字段来设置一个脚本，在用户点击推送之后会执行脚本，也可以通过 3D Touch 来预览。

# $push.cancel(object)

取消一个计划内的推送消息：

```js
$push.cancel({
  title: "标题",
  body: "内容",
})
```

将会取消以 `title` 和 `body` 组成的所有推送消息。

当你有多个标题和内容重复的推送时，你可以使用上述代码得到的 id 来取消：

```js
$push.cancel({id: ""})
```

# $push.clear()

清除当前脚本所有通知（在 Build 462 之前注册的通知会被忽略）：

```js
$push.clear()
```