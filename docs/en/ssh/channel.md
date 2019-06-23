# session.channel

session object provides script executing operations, properties:

Prop | Type | Description
---|---|---
session | session | session
bufferSize | number | buffer size
type | number | type
lastResponse | string | last response
requestPty | bool | request pty
ptyTerminalType | number | pty terminal type
environmentVariables | json | environment variables

# channel.execute(object)

Execute script:

```js
channel.execute({
  script: "ls -l /var/lib/",
  timeout: 0,
  handler: function(result) {
    console.log("response: " + result.response)
    console.log("error: " + result.error)
  }
})
```

# channel.write(object)

Execute command:

```js
channel.write({
  command: "",
  timeout: 0,
  handler: function(result) {
    console.log("success: " + result.success)
    console.log("error: " + result.error)
  }
})
```

# channel.upload(object)

Upload local file to remote:

```js
channel.upload({
  path: "resources/notes.md",
  dest: "/home/user/notes.md",
  handler: function(success) {
    console.log("success: " + success)
  }
})
```

# channel.download(object)

Download remote file to local:

```js
channel.download({
  path: "/home/user/notes.md",
  dest: "resources/notes.md",
  handler: function(success) {
    console.log("success: " + success)
  }
})
```