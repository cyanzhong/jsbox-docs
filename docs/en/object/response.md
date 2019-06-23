# response

`response` is the response object when we handle http requests:

```js
$http.get({
  url: "",
  handler: function(resp) {
    var response = resp.response
  }
})
```

Prop | Type | Read/Write | Description
---|---|---|---
url | string | r | url
MIMEType | string | r | MIME type
expectedContentLength | number | r | expected content length (bytes)
textEncodingName | string | r | text encoding
suggestedFilename | string | r | suggested file name
statusCode | number | r | HTTP status code
headers | object | r | HTTP header