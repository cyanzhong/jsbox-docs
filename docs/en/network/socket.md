# WebSocket

JSBox provides [WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) like interfaces, it creates socket connection between client and server.

# $socket.new(object)

Create a new socket connection:

```js
const socket = $socket.new("wss://echo.websocket.org");
```

You can specify some parameters:

```js
const socket = $socket.new({
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
const object = socket.send("Message");
const result = object.result;
const error = object.error;
```

You can also use data:

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

Get ready state:

```js
const readyState = socket.readyState;
// 0: connecting, 1: open, 2: closing, 3: closed
```

For detailed example: https://github.com/cyanzhong/xTeko/blob/master/extension-demos/socket.js