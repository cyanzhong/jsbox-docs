> 网络模块将是 JSBox 里面最重要的模块之一，他能帮助你完成很多需求。

# $http.request(object)

发起一个 HTTP 请求：

```js
$http.request({
  method: "POST",
  url: "https://apple.com",
  header: {
    k1: "v1",
    k2: "v2"
  },
  body: {
    k1: "v1",
    k2: "v2"
  },
  handler: function(resp) {
    var data = resp.data
  }
})
```

参数 | 类型 | 说明
---|---|---
method | string | GET/POST/DELETE 等
url | string | 链接
header | object | http header
body | object | http body
timeout | number | 请求超时
form | object | form-data 参数
files | array | 文件列表
proxy | json | 代理设置
progress | function | upload/download 中进度回调
showsProgress | bool | 是否显示进度条
message | string | upload/download 中的提示语
handler | function | 回调函数

`body` 可以是一个 JSON 结构或是一个二进制数据，

如果 `body` 是一个 JSON 结构：

- 当 header 中的 `Content-Type` 为 `application/json` 时，body 将会以 `json` 的形式编码
- 当 header 中的 `Content-Type` 为 `application/x-www-form-urlencoded` 时，body 将会转换成 `a=b&c=d` 的 query 结构
- `Content-Type` 默认值是 `application/json`

如果 `body` 是一个二进制数据：

这 http body 不会进行编码，会直接使用传进来的数据。

`form` 和 `files` 样例见 `$http.upload`。

返回数据 `resp` 的结构：

参数 | 类型 | 说明
---|---|---
data | string | json 数据会自动 parse
rawData | data | 原始返回的二进制数据
response | response | [请参考](object/response.md)
error | error | [请参考](object/error.md)

代理设置：

```js
{
  proxy: {
    "HTTPEnable": true,
    "HTTPProxy": "",
    "HTTPPort": 0,
    "HTTPSEnable": true,
    "HTTPSProxy": "",
    "HTTPSPort": 0
  }
}
```

# $http.get(object)

发起一个 `GET` 请求，例如：

```js
$http.get({
  url: "https://apple.com",
  handler: function(resp) {
    var data = resp.data
  }
})
```

除 `method` 为 `GET` 以外，参数和 `$http.request` 一致。

# $http.post(object)

发起一个 `POST` 请求，例如：

```js
$http.post({
  url: "https://apple.com",
  handler: function(resp) {
    var data = resp.data
  }
})
```

除 `method` 为 `POST` 以外，参数和 `$http.request` 一致。

# $http.download(object)

参数和上述完全一样，不同之处在于此方法返回的 `data` 是一个二进制数据：

```js
$http.download({
  url: "https://images.apple.com/v/ios/what-is/b/images/performance_large.jpg",
  showsProgress: true, // Optional, default is true
  backgroundFetch: true, // Optional, default is false
  progress: function(bytesWritten, totalBytes) {
    var percentage = bytesWritten * 1.0 / totalBytes
  },
  handler: function(resp) {
    $share.sheet(resp.data)
  }
})
```

# $http.upload(object)

文件上传接口，此处以[七牛云](https://www.qiniu.com/)为例：

```js
$photo.pick({
  handler: function(resp) {
    var image = resp.image
    if (image) {
      $http.upload({
        url: "http://upload.qiniu.com/",
        form: {
          token: "<token>"
        },
        files: [
          {
            "image": image,
            "name": "file",
            "filename": "file.png"
          }
        ],
        progress: function(percentage) {

        },
        handler: function(resp) {
          
        }
      })
    }
  }
})
```

从相册选取一张图片上传到七牛云，需要填入你自己的 token，此处仅为示例。

`form` 参数表示 form-data 中其他的参数，例如上述的 `token`。

`files` 参数文件结构定义：

参数 | 类型 | 说明
---|---|---
image | object | 图片
data | object | 二进制数据
name | string | 上传表单中的名称
filename | string | 上传之后的文件名
content-type | string | 文件格式

# $http.startServer(object)

启动一个 Web 服务器，将本地目录放到服务器以提供 HTTP 接口访问：

```js
$http.startServer({
  port: 5588, // port number
  path: "", // script root path
  handler: function(result) {
    var url = result.url
  }
})
```

这将会把脚本的根目录作为 server 的根目录，你可以通过获取到的 url 访问这个目录，我们提供了一个 Web 界面供用户在浏览器中访问。

同时这个 Web 服务器提供以下几个 HTTP 接口来进行操作：

- `GET` /list?path=path 获得文件列表
- `GET` /download?path=path 下载文件
- `POST` /upload `{"files[]": file}` 上传文件
- `POST` /move `{"oldPath": "", "newPath": ""}` 移动文件
- `POST` /delete `{"path": ""}` 删除文件
- `POST` /create `{"path": ""}` 创建文件夹

请使用你的 HTTP 相关知识理解上述内容，在此不再赘述。

# $http.stopServer()

将启动的 Web 服务器停掉：

```js
$http.stopServer()
```

# $http.shorten(object)

生成短连接：

```js
$http.shorten({
  url: "https://apple.com",
  handler: function(url) {

  }
})
```

# $http.lengthen(object)

展开一个短连接：

```js
$http.lengthen({
  url: "http://t.cn/RJZxkFD",
  handler: function(url) {

  }
})
```

# $network.ifa_data

获得网卡`接收/发送`数据：

```js
var ifa_data = $network.ifa_data
console.log(ifa_data)
```

样例输出：

```json
{
  "en0" : {
    "received" : 2581234688,
    "sent" : 469011456
  },
  "awdl0" : {
    "received" : 2231296,
    "sent" : 8180736
  },
  "utun0" : {
    "received" : 0,
    "sent" : 0
  },
  "pdp_ip1" : {
    "received" : 2048,
    "sent" : 2048
  },
  "pdp_ip0" : {
    "received" : 2215782400,
    "sent" : 211150848
  },
  "en2" : {
    "received" : 5859328,
    "sent" : 6347776
  },
  "utun2" : {
    "received" : 0,
    "sent" : 0
  },
  "lo0" : {
    "received" : 407684096,
    "sent" : 407684096
  },
  "utun1" : {
    "received" : 628973568,
    "sent" : 35312640
  }
}
```

# $network.startPinging(object)

开始 Ping:

```js
$network.startPinging({
  host: "google.com",
  timeout: 2.0, // default
  period: 1.0, // default
  payloadSize: 56, // default
  ttl: 49, // default
  didReceiveReply: function(summary) {

  },
  didReceiveUnexpectedReply: function(summary) {

  },
  didSendPing: function(summary) {

  },
  didTimeout: function(summary) {

  },
  didFail: function(error) {

  },
  didFailToSendPing: function(response) {

  }
})
```

`summary` 结构：

```json
{
  "sequenceNumber": 0,
  "payloadSize": 0,
  "ttl": 0,
  "host": "",
  "sendDate": null,
  "receiveDate": null,
  "rtt": 0,
  "status": 0
}
```

更多信息请参考：https://github.com/lmirosevic/GBPing

# $network.stopPinging()

停止 Ping。

# $network.proxy_settings

与 [CFNetworkCopySystemProxySettings](https://developer.apple.com/documentation/cfnetwork/1426754-cfnetworkcopysystemproxysettings) 效果相同。