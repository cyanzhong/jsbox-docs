> 剪贴板对于 iOS 的数据分享和交换很重要，JSBox 提供了很多相关接口。

# $clipboard.text

```js
// 获取剪贴板文本
var text = $clipboard.text
// 设置剪贴板文本
$clipboard.text = "Hello, World!"
```

# $clipboard.image

```js
// 获取剪贴板图片，请注意返回的是二进制数据
var data = $clipboard.image
// 设置剪贴板图片
$clipboard.image = data
```

# $clipboard.items

```js
// 获取剪贴板中的所有项目
var items = $clipboard.items
// 设置剪贴板中的所有项目
$clipboard.items = items
```

# $clipboard.phoneNumbers

获取剪贴板中的所有电话号码。

# $clipboard.phoneNumber

获取剪贴板中的第一个电话号码。

# $clipboard.links

获取剪贴板中的所有链接。

# $clipboard.link

获取剪贴板中的第一个链接。

# $clipboard.emails

获取剪贴板中的所有 email。

# $clipboard.email

获取剪贴板中的第一个 email。

# $clipboard.dates

获取剪贴板中的所有日期。

# $clipboard.date

获取剪贴板中的第一个日期。

# $clipboard.setTextLocalOnly(string)

设置剪贴板的文本，但忽略 `Universal Clipboard`：

# $clipboard.set(object)

通过 `type` 和 `value` 设置剪贴板，例如：

```js
$clipboard.set({
  "type": "public.plain-text",
  "value": "Hello, World!"
})
```

# $clipboard.copy(object)

此方法可以设置剪贴板过期时间：

```js
$clipboard.copy({
  text: "Temporary text",
  ttl: 20
})
```

支持参数：

属性 | 类型 | 说明
---|---|---
text | string | 文本
image | image | 图片
data | data | 数据
ttl | number | 几秒之后过期
locally | bool | 本地剪贴板

*关于 `UTTypes` 的介绍：https://developer.apple.com/documentation/mobilecoreservices/uttype*

# $clipboard.clear()

清除剪贴板里面的全部内容。