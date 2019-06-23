# require('path')

`require` 这个方法的机制是将被引入的脚本文件变成一个模块，从而有自己的命名空间，可以解决变量名暴露的问题。

需要模块化的文件需要使用 `module.exports`:


```js
function sayHello() {
  $ui.alert($l10n('HELLO_WORLD'));
}

module.exports = {
  sayHello: sayHello
}
```

sayHello 原本是不能被外部访问的，你可以通过配置 module.exports 来为其提供一个在外部引用时的命名。

所以引入的时候则可以使用：

```js
var app = require('./scripts/app');

app.sayHello();
```

这个机制将各个文件的代码良好的隔离了开来，并且不会出现命名冲突。

注意：请尽可能的使用相对路径，自动补全机制对于绝对路径引入的模块不起作用。

# $include('path')

另外一个方式是使用 `$include` 方式来引入代码，这个机制与 require 完全不同，他不会产生模块化的效果，而仅仅是将代码从一个文件中引入过来，并且执行一遍，效果等同于 eval 一段源码。

通过以上两种方式我们可以有效地组织源码，从而做出架构更好的设计。