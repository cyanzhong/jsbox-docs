# 路径

引入一个脚本时，可以使用绝对路径或相对路径：

例如：

```js
var app = require('./scripts/app')
```

`scripts/` 则是应用根目录 -> scripts 目录下的 app.js 文件，其中 `.js` 可以省略。

路径应用可以跨越各个文件夹，但仅限于当前应用根目录下。

# $file

可以这样读取一个文件：

```js
var file = $file.read('strings/zh-Hans.strings')
```

这会打开 strings 目录下的 zh-Hans.strings 文件。

简而言之，在安装包里面，和文件有关的根目录是应用的根目录。