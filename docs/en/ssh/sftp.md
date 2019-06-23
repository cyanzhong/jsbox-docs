# session.sftp

sftp instance in session object provides file related APIs, object properties:

Prop | Type | Description
---|---|---
session | session | session
bufferSize | number | buffer size
connected | bool | is connected

# sftp.connect()

Create SFTP connection:

```js
await sftp.connect();
```

# sftp.moveItem(object)

Move a file:

```js
sftp.moveItem({
  src: "/home/user/notes.md",
  dest: "/home/user/notes-new.md",
  handler: function(success) {
    
  }
})
```

# sftp.directoryExists(object)

Check whether a directory exists:

```js
sftp.directoryExists({
  path: "/home/user/notes.md",
  handler: function(exists) {

  }
})
```

# sftp.createDirectory(object)

Create a directory:

```js
sftp.createDirectory({
  path: "/home/user/folder",
  handler: function(success) {

  }
})
```

# sftp.removeDirectory(object)

Delete a directory:

```js
sftp.removeDirectory({
  path: "/home/user/folder",
  handler: function(success) {

  }
})
```

# sftp.contentsOfDirectory(object)

List all files in a directory:

```js
sftp.contentsOfDirectory({
  path: "/home/user/folder",
  handler: function(contents) {

  }
})
```

# sftp.infoForFile(object)

Get file information:

```js
sftp.infoForFile({
  path: "/home/user/notes.md",
  handler: function(file) {

  }
})
```

Object properties:

Prop | Type | Description
---|---|---
filename | string | file name
isDirectory | bool | is directory
modificationDate | date | modification date
lastAccess | date | last access date
fileSize | number | file size
ownerUserID | number | owner user id
ownerGroupID | number | owner group id
permissions | string | permissions
flags | number | flags

# sftp.fileExists(object)

Check whether a file exists:

```js
sftp.fileExists({
  path: "/home/user/notes.md",
  handler: function(exists) {

  }
})
```

# sftp.createSymbolicLink(object)

Create symbolic link:

```js
sftp.createSymbolicLink({
  path: "/home/user/notes.md",
  dest: "/home/user/notes-symbolic.md",
  handler: function(success) {

  }
})
```

# sftp.removeFile(object)

Delete a file:

```js
sftp.removeFile({
  path: "/home/user/notes.md",
  handler: function(success) {

  }
})
```

# sftp.contents(object)

Get a file (binary):

```js
sftp.contents({
  path: "/home/user/notes.md",
  handler: function(file) {

  }
})
```

# sftp.write(object)

Write file (binary) to remote:

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

Append file (binary) to remote:

```js
sftp.append({
  file: file,
  path: "/home/user/notes.md",
  handler: function(success) {
    
  }
})
```

# sftp.copy(object)

Copy a file:

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

Note: handler could be implemented with async/await.