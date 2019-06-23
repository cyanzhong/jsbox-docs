# session.channel

session 中的 channel 对象提供执行脚本等操作，结构如下：

参数 | 类型 | 说明
---|---|---
session | session | session 实例
bufferSize | number | buffer size
type | number | 类型
lastResponse | string | 响应
requestPty | bool | request pty
ptyTerminalType | number | pty terminal type
environmentVariables | json | 环境变量

# channel.execute(object)

执行脚本：

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

执行 command:

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

上传本地文件到服务器：

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

从服务器下载文件到本地：

```js
channel.download({
  path: "/home/user/notes.md",
  dest: "resources/notes.md",
  handler: function(success) {
    console.log("success: " + success)
  }
})
```