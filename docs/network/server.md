# $server

你可以使用 $http.startServer 来创建一个简单的 Web 服务器，可以将文件放到上面，然后通过 HTTP 链接下载。当你需要自定义 Request Handler 时，可以使用 $server 相关的接口：

```js
var server = $server.new();

var options = {
  port: 6060, // Required
  bonjourName: "", // Optional
  bonjourType: "", // Optional
};

server.start(options);
```

# $server.start(object)

使用简单的参数快速启动一个 HTTP 服务器：

```js
const server = $server.start({
  port: 6060,
  path: "assets/website",
  handler: () => {
    $app.openURL("http://localhost:6060/index.html");
  }
});
```

# server.stop()

停止 Web 服务器。

# server.listen(events)

通过这个接口可以监听事件：

```js
server.listen({
  didStart: server => {
    $delay(1, () => {
      $app.openURL(`http://localhost:${port}`);
    });
  },
  didConnect: server => {},
  didDisconnect: server => {},
  didStop: server => {},
  didCompleteBonjourRegistration: server => {},
  didUpdateNATPortMapping: server => {}
});
```

# server.addHandler(object)

注册一个 Request Handler:

```js
var handler = {};

// Handler filter
handler.filter = rules => {
  var method = rules.method;
  var url = rules.url;
  // rules.headers, rules.path, rules.query;
  return "data"; // default, data, file, multipart, urlencoded
}

// Handler response
handler.response = request => {
  var method = request.method;
  var url = request.url;
  return {
    type: "data", // default, data, file, error
    props: {
      html: "<html><body style='font-size: 300px'>Hello!</body></html>"
      // json: {
      //   "status": 1,
      //   "values": ["a", "b", "c"]
      // }
    }
  };
}

// Handler async response
handler.asyncResponse = (request, completion) => {
var method = request.method;
  var url = request.url;
  completion({
    type: "data", // default, data, file, error
    props: {
      html: "<html><body style='font-size: 300px'>Hello!</body></html>"
      // json: {
      //   "status": 1,
      //   "values": ["a", "b", "c"]
      // }
    }
  });
}
```

 # handler.filter

 filter 是一个函数，在这里你可以根据传入的 rules 决定对这些规则使用什么样的 request，rules 结构：

```json
{
  "method": "",
  "url": "",
  "headers": {

  },
  "path": "",
  "query": {

  }
}
```

request 类型包括：`default`, `data`, `file`, `multipart`, `urlencoded`。

从 v1.51.0 开始，你可以返回一个字典，用来覆盖之前的规则，例如：

```js
handler.filter = rules => {
  return {
    "type": "data",
    "method": "GET"
  }
}
```

当你需要重定向一个请求，或是将 `POST` 改写为 `GET` 等需求时，可能会用得上。

# handler.response

这个函数传入一个 request，根据需要返回一个 response 用于完成对这个请求的响应，例如这是一种最简单的 response：

```js
{
  type: "data",
  props: {
    html: "<html><body style='font-size: 300px'>Hello!</body></html>"
  }
}
```

创建 response 可以指定类型为：`default`, `data`, `file`，通过不同的 props 来初始化一个 response。

`data` 类型支持通过 `html`, `text` 或 `json` 字段来构造。`file` 类型支持通过 `path` 来构造。

其他支持的参数：

属性 | 类型 | 说明
---|---|---
contentType | string | content type
contentLength | number | content length
statusCode | number | status code
cacheControlMaxAge | number | cache control max age
lastModifiedDate | Date | last modified date
eTag | string | E-Tag
gzipEnabled | bool | gzip enabled
headers | object | HTTP headers

# server.clearHandlers()

清除掉所有已注册的 Request Handlers。

完整例子请见：https://github.com/cyanzhong/xTeko/blob/master/extension-demos/server.js

Request 对象和 Response 对象包括多种类型，请参考[详细文档](object/server.md)。