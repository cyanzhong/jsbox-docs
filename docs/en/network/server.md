# $server

You can create a simple web server with $http.startServer, it creates a http server with standard html template.

If you want to create a server with custom request handlers, you can use $server APIs:

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

Start a simple HTTP server:

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

Stop the web server.

# server.listen(events)

Observer server events:

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

Register a request handler:

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

 filter is a function, it passes rules as the parameter, you should return the type of request for it. Rules:

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

Types include: `default`, `data`, `file`, `multipart`, `urlencoded`.

Starting from v1.51.0, you can also return an object that overrides the original rules:

```js
handler.filter = rules => {
  return {
    "type": "data",
    "method": "GET"
  }
}
```

You probably need this if you want to redirect a request, or change a `POST` method to `GET`, etc.

# handler.response

Response function passes request as the parameter, you should return a response for it:

```js
{
  type: "data",
  props: {
    html: "<html><body style='font-size: 300px'>Hello!</body></html>"
  }
}
```

Response type can be: `default`, `data`, `file`, it initiates response with different props.

`data` response can be created with `html`, `text` or `json` parameter. `file` response can be created with `path` parameter.

Other parameters:

Prop | Type | Description
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

Remove all registered handlers.

For detailed example, refer to: https://github.com/cyanzhong/xTeko/blob/master/extension-demos/server.js

Request and Response are complicated objects, please take a look [Detailed Docs](en/object/server.md).