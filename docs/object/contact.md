# contact

`contact` 是使用 `$contact` 接口时返回的数据对象。

属性 | 类型 | 读写 | 说明
---|---|---|---
identifier | string | 只读 | 标识符
content | string | 只读 | 内容
contactType | number | 只读 | 类型
namePrefix | string | 读写 | name prefix
givenName | string | 读写 | given name
middleName | string | 读写 | middle name
familyName | string | 读写 | family name
nameSuffix | string | 读写 | name suffix
nickname | string | 读写 | nick name
organizationName | string | 读写 | 组织
departmentName | string | 读写 | 部门
jobTitle | string | 读写 | 职位
note | string | 读写 | 备注
imageData | data | 读写 | 头像
phoneNumbers | array | 读写 | 电话
emailAddresses | array | 读写 | 邮件
postalAddresses | array | 读写 | 邮编
urlAddresses | array | 读写 | 链接
instantMessageAddresses | array | 读写 | 即时通讯

# group

`group` 是使用 `$contact.fetchGroup` 接口时返回的对象

属性 | 类型 | 读写 | 说明
---|---|---|---
identifier | string | 只读 | 标识符
name | string | 读写 | 名称