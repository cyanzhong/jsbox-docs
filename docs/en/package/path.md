# Path

Both absolute paths and relative paths are supported:

```js
var app = require('./scripts/app')
```

In require function, `.js` can be omitted, in above case it represents `scripts/app.js`.

You can use this pattern to access all folders inside current package.

# $file

How to access files:

```js
var file = $file.read('strings/zh-Hans.strings')
```

This code opens the file in `strings/zh-Hans.strings`.

In short, in package mode, the root path is the package folder.