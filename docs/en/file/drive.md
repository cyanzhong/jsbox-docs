> JSBox provides `$drive` in order to access iCloud Drive

# iCloud Drive

There are three types of operations:

- `$drive.open` open Document Picker
- `$drive.save` save file using Document Picker
- `$drive.read` read file directly, like `$file`

# $drive.open

Pick a file using iCloud Document Picker:

```js
$drive.open({
  handler: function(data) {
    
  }
})
```

We can set the UTI types to make it more accurate:

```js
types: ["public.png"]
```

# $drive.save

Save a file using Document Picker:

```js
$drive.save({
  data: $data({string: "Hello, World!"}),
  name: "File Name",
  handler: function() {

  }
})
```

# $drive.read

This API looks similar to $file.read:

```js
var file = $drive.read("demo.txt")
```

The only difference is we are reading file in iCloud Drive container.

It equals to:

```js
var file = $file.read("drive://demo.txt")
```

# $drive.xxx

Besides, every `$file` API has an equivalent `$drive` API:

- `$drive.read` vs [$file.read](en/file/method.md?id=filereadpath)
- `$drive.download` vs [$file.download](en/file/method.md?id=filedownloadpath)
- `$drive.write` vs [$file.write](en/file/method.md?id=filewriteobject)
- `$drive.delete` vs [$file.delete](en/file/method.md?id=filedeletepath)
- `$drive.list` vs [$file.list](en/file/method.md?id=filelistpath)
- `$drive.copy` vs [$file.copy](en/file/method.md?id=filecopyobject)
- `$drive.move` vs [$file.move](en/file/method.md?id=filemoveobject)
- `$drive.mkdir` vs [$file.mkdir](en/file/method.md?id=filemkdirpath)
- `$drive.exists` vs [$file.exists](en/file/method.md?id=fileexistspath)
- `$drive.isDirectory` vs [$file.isDirectory](en/file/method.md?id=fileisdirectorypath)
- `$drive.absolutePath` vs [$file.absolutePath](en/file/method.md?id=fileabsolutepath)