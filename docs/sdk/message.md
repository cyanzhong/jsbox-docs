> 用于处理和短信或邮件相关的操作

# $message.sms(object)

调用系统接口发送短信：

```js
$http.download({
  url: "https://images.apple.com/v/iphone/compare/f/images/compare/compare_iphone7_jetblack_large_2x.jpg",
  handler: function(resp) {
    $message.sms({
      recipients: ["18688888888", "10010"],
      body: "Message body",
      subject: "Message subject",
      attachments: [resp.data],
      handler: function(result) {

      }
    })
  }
})
```

参数 | 说明
---|---
recipients | 接受者
body | 内容
subject | 主题
attachments | 附件(图片或文件)
result | 0: 取消 1: 成功 2: 失败

# $message.mail(object)

调用系统接口发送邮件：

```js
$http.download({
  url: "https://images.apple.com/v/iphone/compare/f/images/compare/compare_iphone7_jetblack_large_2x.jpg",
  handler: function(resp) {
    $message.mail({
      subject: "Message subject",
      to: ["18688888888", "10010"],
      cc: [],
      bcc: [],
      body: "Message body",
      attachments: [resp.data],
      handler: function(result) {

      }
    })
  }
})
```

参数 | 说明
---|---
subject | 主题
to | 接受者
cc | 抄送
bcc | 密送
body | 内容
isHTML | 内容是否为 HTML
attachments | 附件(图片或文件)
result | 0: 取消 1: 保存 2: 成功 3: 失败