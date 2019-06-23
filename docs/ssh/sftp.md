# session.sftp

session 中的 sftp 对象提供对文件相关的操作，结构如下：

参数 | 类型 | 说明
---|---|---
session | session | session 实例
bufferSize | number | buffer size
connected | bool | 是否连接

# sftp.connect()

创建 SFTP 连接：

```js
await sftp.connect();
```

# sftp.moveItem(object)

移动文件：

```js
sftp.moveItem({
  src: "/home/user/notes.md",
  dest: "/home/user/notes-new.md",
  handler: function(success) {

  }
})
```

# sftp.directoryExists(object)

判断文件夹是否存在：

```js
sftp.directoryExists({
  path: "/home/user/notes.md",
  handler: function(exists) {

  }
})
```

# sftp.createDirectory(object)

创建文件夹：

```js
sftp.createDirectory({
  path: "/home/user/folder",
  handler: function(success) {

  }
})
```

# sftp.removeDirectory(object)

删除文件夹：

```js
sftp.removeDirectory({
  path: "/home/user/folder",
  handler: function(success) {

  }
})
```

# sftp.contentsOfDirectory(object)

列出文件夹中所有的文件：

```js
sftp.contentsOfDirectory({
  path: "/home/user/folder",
  handler: function(contents) {

  }
})
```

# sftp.infoForFile(object)

获取一个文件的属性：

```js
sftp.infoForFile({
  path: "/home/user/notes.md",
  handler: function(file) {

  }
})
```

file 的数据结构：

参数 | 类型 | 说明
---|---|---
filename | string | 文件名
isDirectory | bool | 是否文件夹
modificationDate | date | 修改时间
lastAccess | date | 最后访问时间
fileSize | number | 文件大小
ownerUserID | number | owner user id
ownerGroupID | number | owner group id
permissions | string | 权限
flags | number | flags

# sftp.fileExists(object)

判断文件是否存在：

```js
sftp.fileExists({
  path: "/home/user/notes.md",
  handler: function(exists) {

  }
})
```

# sftp.createSymbolicLink(object)

创建符号链接：

```js
sftp.createSymbolicLink({
  path: "/home/user/notes.md",
  dest: "/home/user/notes-symbolic.md",
  handler: function(success) {

  }
})
```

# sftp.removeFile(object)

删除文件：

```js
sftp.removeFile({
  path: "/home/user/notes.md",
  handler: function(success) {

  }
})
```

# sftp.contents(object)

获取文件二进制数据：

```js
sftp.contents({
  path: "/home/user/notes.md",
  handler: function(file) {

  }
})
```

# sftp.write(object)

将二进制文件写入到服务器：

```js
sftp.write({
  file: file,
  path: "/home/user/notes.md",
  progress: function(sent) {
    // Optional: determine whether is finished here
    return sent > 1024 * 1024
  },
  handler: function(success) {
    
  }
})
```

# sftp.append(object)

将文件追加到远程文件：

```js
sftp.append({
  file: file,
  path: "/home/user/notes.md",
  handler: function(success) {
    
  }
})
```

# sftp.copy(object)

复制文件：

```js
sftp.copy({
  path: "/home/user/notes.md",
  dest: "/home/user/notes-copy.md",
  progress: function(copied, totalBytes) {
    // Optional: determine whether is finished here
    return sent > 1024 * 1024
  },
  handler: function(success) {
    
  }
})
```

注：以上所有的 handler 也可以通过 async/await 实现。