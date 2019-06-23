# response

`response` 是 http 请求里面返回的内容，例如：

```js
$http.get({
  url: "",
  handler: function(resp) {
    var response = resp.response
  }
})
```

属性 | 类型 | 读写 | 说明
---|---|---|---
url | string | 只读 | url
MIMEType | string | 只读 | MIME 类型
expectedContentLength | number | 只读 | 长度
textEncodingName | string | 只读 | 编码
suggestedFilename | string | 只读 | 建议的文件名
statusCode | number | 只读 | HTTP 状态码
headers | object | 只读 | HTTP header