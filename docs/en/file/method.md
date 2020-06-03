> JSBox provides some APIs to store/fetch files safely

# $file.read(path)

Read a file:

```js
var file = $file.read("demo.txt")
```

# $file.download(path) -> Promise

This method ensures a iCloud drive file is downloaded before reading it:

```js
const data = await $file.download("drive://.test.db.icloud");
```

# $file.write(object)

Write a file:

```js
var success = $file.write({
  data: $data({string: "Hello, World!"}),
  path: "demo.txt"
})
```

# $file.delete(path)

Delete a file:

```js
var success = $file.delete("demo.txt")
```

# $file.list(path)

Get all file names in a folder:

```js
var contents = $file.list("download")
```

# $file.copy(object)

Copy a file:

```js
var success = $file.copy({
  src: "demo.txt",
  dst: "download/demo.txt"
})
```

# $file.move(object)

Move a file:

```js
var success = $file.move({
  src: "demo.txt",
  dst: "download/demo.txt"
})
```

# $file.mkdir(path)

Make a directory (folder):

```js
var success = $file.mkdir("download")
```

# $file.exists(path)

Check if a file exists:

```js
var exists = $file.exists("demo.txt")
```

# $file.isDirectory(path)

Checkc if a path is directory:

```js
var isDirectory = $file.isDirectory("download")
```

# $file.merge(args)

Merge multiple files into one file:

```js
$file.merge({
  files: ["assets/1.txt", "assets/2.txt"],
  dest: "assets/merged.txt",
  chunkSize: 1024 * 1024, // optional, default is 1024 * 1024
});
```

Split a file into multiple files:

```js
$file.split({
  file: "assets/merged.txt",
  chunkSize: 1024, // optional, default is 1024
});
```

The file will be split as: merged-001.txt, merged-002.txt, ...

# $file.absolutePath(path)

Returns the absolute path of a relative path:

```js
const absolutePath = $file.absolutePath(path);
```

# $file.extensions

Returns all installed scripts:

```js
var extensions = $file.extensions
```

# shared://

Access shared folder like we mentioned before:

```js
var file = $file.read("shared://demo.txt")
```

# drive://

Access iCloud Drive container like we mentioned before:

```js
var file = $file.read("drive://demo.txt")
```