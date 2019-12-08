> 用于与系统提醒事项进行交互，例如读取或写入

# $reminder.fetch(object)

用于读取提醒事项（会提示用户授权）：

```js
$reminder.fetch({
  startDate: new Date(),
  hours: 2 * 24,
  handler: function(resp) {
    var events = resp.events
  }
})
```

看起来和 `$calendar` 极为相似，返回的数据是如下结构：

属性 | 类型 | 读写 | 说明
---|---|---|---
title | string | 读写 | 标题
identifier | string | 只读 | id
location | string | 读写 | 位置
notes | string | 读写 | 备注
url | string | 读写 | 网址
modifiedDate | date | 只读 | 修改时间
creationDate | date | 只读 | 创建时间
completed | boolean | 读写 | 是否完成
completionDate | date | 只读 | 完成时间
alarmDate | date | 读写 | 闹钟时间
priority | number | 读写 | 优先级(1 ~ 9) 

# $reminder.create(object)

用于创建一个提醒事项：

```js
$reminder.create({
  title: "Hey!",
  alarmDate: new Date(),
  notes: "Hello, World!",
  url: "https://apple.com",
  handler: function(resp) {

  }
})
```

可以通过 `alarmDate` 和 `alarmDates` 来指定提醒闹钟时间。

# $reminder.save(object)

和 `$calendar.save` 类似，用于修改 event 后保存更新：

```js
$reminder.save({
  event: event,
  handler: function(resp) {

  }
})
```

# $reminder.delete(object)

删除某个提醒事项：

```js
$reminder.delete({
  event: event,
  handler: function(resp) {
    
  }
})
```

> 其实 `$reminder` 和 `$calendar` 极为类似，在 iOS 内部也的确如此，他们有类似的接口设计，并且继承同一个数据基类。