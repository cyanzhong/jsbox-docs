# Secure Shell

从 v1.14.0 开始，JSBox 支持 SSH，你可以通过简单的 JavaScript 连接至你的服务器，这里有一个完整的例子来帮你有个宏观的了解：[ssh-example](https://github.com/cyanzhong/xTeko/tree/master/extension-demos/ssh-example)。

JSBox 提供的 SSH 相关接口主要包括三个方面：

- session
- channel
- sftp

通过这些接口你可以连接服务器，执行脚本，也能上传下载文件。

JSBox 的 SSH 接口基于 [NMSSH](https://github.com/NMSSH/NMSSH) 的实现，你可以参考 NMSSH 的文档来了解整体设计。

# $ssh.connect(object)

通过密码或公钥私钥连接至服务器，同时能执行一段脚本：

```js
$ssh.connect({
  host: "",
  port: 22,
  username: "",
  public_key: "",
  private_key: "",
  // password: "",
  script: "ls -l /var/lib/",
  handler: function(session, response) {
    console.log("connect: " + session.connected)
    console.log("authorized: " + session.authorized)
    console.log("response: " + response)
  }
})
```

这个例子通过 `public_key` 和 `private_key` 来授权，你可以将密钥文件打包放在安装包里，正如 [ssh-example](https://github.com/cyanzhong/xTeko/tree/master/extension-demos/ssh-example) 里面所示例的那样。

这个接口会返回一个 session 实例和 response，session 对象结构：

参数 | 类型 | 说明
---|---|---
host | string | 主机
port | number | 端口
username | string | 用户名
timeout | number | 超时时间
lastError | error | 错误
fingerprintHash | string | fingerprint
banner | string | banner
remoteBanner | string | remote banner
connected | bool | 是否连接
authorized | bool | 是否授权
channel | channel | channel 实例
sftp | sftp | sftp 实例

通过 session 对象中的 channel 和 sftp，我们可以完成后续的各种操作。

# $ssh.disconnect()

关掉 JSBox 开启的所有 SSH session:

```js
$ssh.disconnect()
```