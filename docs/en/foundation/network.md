> Network module is very important in JSBox, you can leverage this ability to achieve more

# $http.request(object)

Send a general HTTP request:

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

Param | Type | Description
---|---|---
method | string | GET/POST/DELETE etc
url | string | url
header | object | http header
body | object | http body
timeout | number | timeout (second)
form | object | form-data
files | array | file list
proxy | json | proxy configuration
progress | function | upload/download callback
showsProgress | bool | shows progress
message | string | upload/download message
handler | function | finished callback

`body` could be a JSON object or a binary data,

If `body` is a JSON object:

- When `Content-Type` is `application/json`, body will be encoded as JSON object
- When `Content-Type` is `application/x-www-form-urlencoded`, body will be converted to `a=b&c=d` formatted string
- The default value of `Content-Type` is `application/json`

If `body` is a binary data:

body won't be converted, it directly pass to body field. 

For `form` and `files`, refer `$http.upload` to see details.

`resp` properties:

Param | Type | Description
---|---|---
data | string | json object will be parsed automatically
rawData | data | raw response binary data
response | response | [Refer](en/object/response.md)
error | error | [Refer](en/object/error.md)

Proxy configuration:

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

Send a `GET` request:

```js
$http.get({
  url: "https://apple.com",
  handler: function(resp) {
    var data = resp.data
  }
})
```

It just like a general request, but the method is always `GET`.

# $http.post(object)

Send a `POST` request:

```js
$http.post({
  url: "https://apple.com",
  handler: function(resp) {
    var data = resp.data
  }
})
```

It just like a general request, but the method is always `POST`.

# $http.download(object)

It just like a general request, but the `data` inside resp is a binary data (file):

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

File upload request, here's an example based on [qiniu](https://www.qiniu.com/):

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

Pick a photo from photo library, upload it to qiniu (fill your own token).

You can fill form-data parameters in `form`, like `token` in this example.

`files` properties:

Param | Type | Description
---|---|---
image | object | image
data | object | binary data
name | string | form name
filename | string | file name
content-type | string | content type

# $http.startServer(object)

Start a web server, serve local files to provide HTTP interfaces:

```js
$http.startServer({
  port: 5588, // port number
  path: "", // script root path
  handler: function(result) {
    var url = result.url
  }
})
```

This code will create a server based on root path, you can access by url, we also provide a web interface that allows use access on browser.

At the same time, you can access server by following APIs:

- `GET` /list?path=path list contents
- `GET` /download?path=path download file
- `POST` /upload `{"files[]": file}` upload file
- `POST` /move `{"oldPath": "", "newPath": ""}` move file
- `POST` /delete `{"path": ""}` delete file
- `POST` /create `{"path": ""}` create folder

Please understand above contents by using your knowledge of HTTP.

# $http.stopServer()

Stop a web server:

```js
$http.stopServer()
```

# $http.shorten(object)

Shorten a link:

```js
$http.shorten({
  url: "https://apple.com",
  handler: function(url) {

  }
})
```

# $http.lengthen(object)

Expand a link:

```js
$http.lengthen({
  url: "http://t.cn/RJZxkFD",
  handler: function(url) {

  }
})
```

# $network.ifa_data

Get network interface received/sent data in bytes:

```js
var ifa_data = $network.ifa_data
console.log(ifa_data)
```

Example output:

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

start pinging:

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

`summary` structure:

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

For more information: https://github.com/lmirosevic/GBPing

# $network.stopPinging()

Stop pinging.

# $network.proxy_settings

Port of [CFNetworkCopySystemProxySettings](https://developer.apple.com/documentation/cfnetwork/1426754-cfnetworkcopysystemproxysettings)