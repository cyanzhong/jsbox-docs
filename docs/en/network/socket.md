# WebSocket

JSBox provides [WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) like interfaces, it creates socket connection between client and server.

# $socket.new(object)

Create a new socket connection:

```js
var socket = $socket.new("wss://echo.websocket.org");
```

You can specify some parameters:

```js
var socket = $socket.new({
  url: "wss://echo.websocket.org",
  protocols: [],
  allowsUntrustedSSLCertificates: true
});
```

# socket.listen(object)

Observe socket events:

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

Open WebSocket.

# socket.close(object)

Close WebSocket.

```js
socket.close({
  code: 1000, // Optional, see: https://developer.mozilla.org/en-US/docs/Web/API/CloseEvent
  reason: "reason", // Optional
});
```

# socket.send(object)

Send content:

```js
var object = socket.send("Message");
var result = object.result;
var error = object.error;
```

You can also use data:

```js
socket.send({
  data: data,
  noCopy: true, // Optional
});
```

# socket.ping(data)

```js
var object = socket.ping(data);
var result = object.result;
var error = object.error;
```

# socket.readyState

Get ready state:

```js
var readyState = socket.readyState;
// 0: connecting, 1: open, 2: closing, 3: closed
```

For detailed example: https://github.com/cyanzhong/xTeko/blob/master/extension-demos/socket.js