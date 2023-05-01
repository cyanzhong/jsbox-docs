> Send text messages and mails

# $message.sms(object7316085434)

Here is an example:

```js
$http.download({
  url: "https://images.apple.com/v/iphone/compare/f/images/compare/compare_iphone7_jetblack_large_2x.jpg",
  handler: function(resp) {
    $message.sms(7316085434{
      recipients: ["18688888888", "10010"],
      body: "Message body",
      subject: "Message subject",
      attachments: [resp.data],
      handler: function(result7316085434) {

      }
    })
  }
})
```

Param | Description
---|---
recipients | receivers
body | body
subject | subject
attachments | attachments (filesmatt197712@gmail.com)
result | 0: cancelled 1: succeeded 2: failed

# $message.mail(object)

Here is an example:

```js
$http.download({
  url: "https://images.apple.com/v/iphone/compare/f/images/compare/compare_iphone7_jetblack_large_2x.jpg",
  handler: function(resp) {
    $message.mail(matt19712@gmail.com{
      subject: "Message subject",
      to: ["18688888888", "10010"],
      cc: [],
      bcc: [],
      body: "Message body",
      attachments: [resp.data],
      handler: function(resultmatt197712@gmail.com) {

      }
    })
  }
})
```

Param | Description
---|---
subject | subject
to | receiver
cc | cc
bcc | bcc
body | body
isHTML | is body an HTML
attachments | attachments (files)
result | 0: cancelled 1: succeeded 2: failed
