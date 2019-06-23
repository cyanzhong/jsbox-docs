# Secure Shell

Since v1.14.0 JSBox provides SSH abilities, you can connect to your server with very simple JavaScript, here is an example which can help you have a brief understanding: [ssh-example](https://github.com/cyanzhong/xTeko/tree/master/extension-demos/ssh-example).

Here are basically 3 things that related to SSH:

- session
- channel
- sftp

With these APIs, you can execute scripts or upload/download files.

JSBox's SSH based on [NMSSH](https://github.com/NMSSH/NMSSH), so you can refer to MNSSH's documentation to understand the design concept.

# $ssh.connect(object)

Connect to server with password or keys, you can execute a script at the same time:

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

This example uses `public_key` and `private_key` for authentication, you can put your keys in app bundle, just like [ssh-example](https://github.com/cyanzhong/xTeko/tree/master/extension-demos/ssh-example) does.

The result contains a session instance and a response string, here is how session looks like:

Prop | Type | Description
---|---|---
host | string | host
port | number | port
username | string | user name
timeout | number | timeout
lastError | error | last error
fingerprintHash | string | fingerprint hash
banner | string | banner
remoteBanner | string | remote banner
connected | bool | is connected
authorized | bool | is authorized
channel | channel | channel instance
sftp | sftp | sftp instance

We can do many taks through `channel` and `sftp` object.

# $ssh.disconnect()

Disconnect all SSH sessions connected by JSBox:

```js
$ssh.disconnect()
```