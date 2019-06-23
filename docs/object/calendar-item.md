# calendarItem

`calendarItem` 是使用 `$calendar` 接口时返回的数据对象。

属性 | 类型 | 读写 | 说明
---|---|---|---
title | string | 读写 | 标题
location | string | 读写 | 位置
notes | string | 读写 | 备注
url | string | 读写 | 链接
allDay | bool | 读写 | 是否全天时间
startDate | date | 读写 | 开始时间
endDate | date | 读写 | 结束时间
status | number | 只读 | 状态
eventIdentifier | string | 只读 | 标识符
creationDate | date | 只读 | 创建时间
modifiedDate | date | 只读 | 修改时间