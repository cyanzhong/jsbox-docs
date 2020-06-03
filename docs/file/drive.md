> $drive 用于操作 iCloud Drive 下的文件，与 $file 高度类似

# iCloud Drive

JSBox 支持 iCloud Drive 文件的操作，主要操作有三种类型：

- `$drive.open` 让用户选择文件
- `$drive.save` 让用户存储文件
- `$drive.read` 等和 `$file.read` 一致的接口

# $drive.open

打开 iOS 的文件选择器让用户选择一个文件：

```js
$drive.open({
  handler: function(data) {
    
  }
})
```

可以传入 `types` 用于限定文件 UTI:

```js
types: ["public.png"]
```

# $drive.save

打开 iOS 文件选择器让用户把文件存储到 iCloud Drive:

```js
$drive.save({
  data: $data({string: "Hello, World!"}),
  name: "File Name",
  handler: function() {

  }
})
```

# $drive.read

此接口效果与 `$file.read` 完全相同：

```js
var file = $drive.read("demo.txt")
```

不同之处是在于这个接口会从 JSBox 的 iCloud Drive 文件夹读取相应的子目录。

另外，此操作等价于：

```js
var file = $file.read("drive://demo.txt")
```

# $drive.xxx

同样的，`$drive` 也提供了类似 `$file` 的其他方法：

- `$drive.read` vs [$file.read](file/method.md?id=filereadpath)
- `$drive.download` vs [$file.download](file/method.md?id=filedownloadpath)
- `$drive.write` vs [$file.write](file/method.md?id=filewriteobject)
- `$drive.delete` vs [$file.delete](file/method.md?id=filedeletepath)
- `$drive.list` vs [$file.list](file/method.md?id=filelistpath)
- `$drive.copy` vs [$file.copy](file/method.md?id=filecopyobject)
- `$drive.move` vs [$file.move](file/method.md?id=filemoveobject)
- `$drive.mkdir` vs [$file.mkdir](file/method.md?id=filemkdirpath)
- `$drive.exists` vs [$file.exists](file/method.md?id=fileexistspath)
- `$drive.isDirectory` vs [$file.isDirectory](file/method.md?id=fileisdirectorypath)
- `$drive.absolutePath` vs [$file.absolutePath](file/method.md?id=fileabsolutepath)