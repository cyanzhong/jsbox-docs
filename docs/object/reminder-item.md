# reminderItem

`reminderItem` 是使用 `$reminder` 接口时返回的数据对象。

属性 | 类型 | 读写 | 说明
---|---|---|---
title | string | 读写 | 标题
location | string | 读写 | 位置
notes | string | 读写 | 备注
url | string | 读写 | 链接
priority | number | 读写 | 优先级
completed | bool | 读写 | 是否完成
completionDate | date | 只读 | 完成时间
alarmDate | date | 读写 | 提醒时间
creationDate | date | 只读 | 创建时间
modifiedDate | date | 只读 | 修改时间