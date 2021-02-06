# WebSocket

JSBox 支持类似 [WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) 的接口，用于与服务器之间提供 socket 连接。

# $socket.new(object)

创建一个新的 socket 对象：

```js
const socket = $socket.new("wss://echo.websocket.org");
```

你也可以指定一些参数：

```js
const socket = $socket.new({
  url: "wss://echo.websocket.org",
  protocols: [],
  allowsUntrustedSSLCertificates: true
});
```

# socket.listen(object)

用户监听 socket 消息：

```js
socket.listen({
  didOpen: (sock) => {
    console.log("Websocket Connected");
  },
  didFail: (sock, error) => {
    console.error(`:( Websocket Failed With Error: ${error}`);
  },
  didClose: (sock, code, reason, wasClean) => {
    console.log("WebSocket closed");
  },
  didReceiveString: (sock, string) => {
    console.log(`Received: ${string}`);
  },
  didReceiveData: (sock, data) => {
    console.log(`Received: ${data}`);
  },
  didReceivePing: (sock, data) => {
    console.log("WebSocket received ping");
  },
  didReceivePong: (sock, data) => {
    console.log("WebSocket received pong");
  }
});
```

# socket.open()

打开 WebSocket。

# socket.close(object)

关闭 WebSocket:

```js
socket.close({
  code: 1000, // Optional, see: https://developer.mozilla.org/en-US/docs/Web/API/CloseEvent
  reason: "reason", // Optional
});
```

# socket.send(object)

发送内容，例如：

```js
const object = socket.send("Message");
const result = object.result;
const error = object.error;
```

也可以通过 data 发送：

```js
socket.send({
  data,
  noCopy: true, // Optional
});
```

# socket.ping(data)

```js
const object = socket.ping(data);
const result = object.result;
const error = object.error;
```

# socket.readyState

获取状态：

```js
const readyState = socket.readyState;
// 0: connecting, 1: open, 2: closing, 3: closed
```

完整例子请见：https://github.com/cyanzhong/xTeko/blob/master/extension-demos/socket.js