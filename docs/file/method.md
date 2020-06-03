> 提供安全的接口用于操作沙盒内的文件

# $file.read(path)

读取文件：

```js
var file = $file.read("demo.txt")
```

# $file.download(path) -> Promise

当使用 `drive://` 路径时，这个方法先会保证文件被下载下来，然后返回其数据：

```js
const data = await $file.download("drive://.test.db.icloud");
```

# $file.write(object)

写入文件：

```js
var success = $file.write({
  data: $data({string: "Hello, World!"}),
  path: "demo.txt"
})
```

# $file.delete(path)

删除文件：

```js
var success = $file.delete("demo.txt")
```

# $file.list(path)

获取目录下所有文件名：

```js
var contents = $file.list("download")
```

# $file.copy(object)

复制文件：

```js
var success = $file.copy({
  src: "demo.txt",
  dst: "download/demo.txt"
})
```

# $file.move(object)

移动文件：

```js
var success = $file.move({
  src: "demo.txt",
  dst: "download/demo.txt"
})
```

# $file.mkdir(path)

创建文件夹：

```js
var success = $file.mkdir("download")
```

# $file.exists(path)

判断文件/目录是否存在：

```js
var exists = $file.exists("demo.txt")
```

# $file.isDirectory(path)

判断某个路径是否是目录：

```js
var isDirectory = $file.isDirectory("download")
```

# $file.merge(args)

将多个文件合并成一个：

```js
$file.merge({
  files: ["assets/1.txt", "assets/2.txt"],
  dest: "assets/merged.txt",
  chunkSize: 1024 * 1024, // optional, default is 1024 * 1024
});
```

将一个文件分割成多个：

```js
$file.split({
  file: "assets/merged.txt",
  chunkSize: 1024, // optional, default is 1024
});
```

文件将会被分割成 merged-001.txt, merged-002.txt, ...

# $file.absolutePath(path)

返回一个相对路径对应的绝对路径：

```js
const absolutePath = $file.absolutePath(path);
```

# $file.extensions

返回所有安装的 JavaScript extension 文件名：

```js
var extensions = $file.extensions
```

# shared://

上述示例操作都是在扩展各自的目录下进行文件读写，如果目录以 `shared://` 开头，则读写操作都发生在共享目录，可以被别的扩展读取和覆盖：

```js
var file = $file.read("shared://demo.txt")
```

# drive://

用于读写在 iCloud Drive 目录下的文件和子目录：

```js
var file = $file.read("drive://demo.txt")
```