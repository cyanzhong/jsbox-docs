> JSBox 自带的压缩/解压缩模块

# $archiver.zip(object)

将多个文件压缩成一个 ZIP 文件：

```js
var files = $context.dataItems
var dest = "Archive.zip"

if (files.length == 0) {
  return
}

$archiver.zip({
  files: files,
  dest: dest,
  handler: function(success) {
    if (success) {
      $share.sheet([dest, $file.read(dest)])
    }
  }
})
```

`files` 是一个 data 数组，也可以通过 `paths` 指定一组文件。

你也可以通过 directory 参数来对一个文件夹进行压缩：

```js
$archiver.zip({
  directory: "",
  dest: "",
  handler: function(success) {
    
  }
})
```

# $archiver.unzip(object)

将一个 ZIP 文件解压到某个路径下：

```js
$archiver.unzip({
  file: file,
  dest: "folder",
  handler: function(success) {

  }
})
```

file 是一个 zip 的 data 对象，dest 所指向的目录需要存在，否则将会失败。

从 2.0 开始，你也可以使用 `path` 来指定需要解压的 zip 文件位置，这种方式使用更少的内存：

```js
const success = await $archiver.unzip({
  path: "archive.zip",
  dest: "folder"
});
```