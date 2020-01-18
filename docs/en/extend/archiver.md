> JSBox has builtin archiver/unarchiver module

# $archiver.zip(object)

Compress files to a zip:

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

`files` is a file array, we could use `paths` as well.

You could also compress a folder by:

```js
$archiver.zip({
  directory: "",
  dest: "",
  handler: function(success) {
    
  }
})
```

# $archiver.unzip(object)

Unzip a file:

```js
$archiver.unzip({
  file: file,
  dest: "folder",
  handler: function(success) {

  }
})
```

File has to be a zip document, dest is the destination folder, it has to be existed.

Starts from 2.0, you can also use `path` property which points to the zip file, it uses less memory:

```js
const success = await $archiver.unzip({
  path: "archive.zip",
  dest: "folder"
});
```