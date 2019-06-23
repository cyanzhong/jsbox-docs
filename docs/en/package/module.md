# require('path')

`require` is designed for modularizing a script, with its own namespace we can expose functions and variables correctly.

You can easily expose APIs with `module.exports`:

```js
function sayHello() {
  $ui.alert($l10n('HELLO_WORLD'));
}

module.exports = {
  sayHello: sayHello
}
```

With the name `sayHello`, the function sayHello will be accessible to other scripts.

Here's how to require:

```js
var app = require('./scripts/app');

app.sayHello();
```

This mechanism separates all logic into multiple files, without naming conflicts.

Note: please use relative as you can, auto-completion system doesn't work with absolute path.

# $include('path')

Another way is `$include`, but this is totally different, this function just simply copy the code from another file, and execute it like `eval`.

With 2 solutions above, we can design our architecture better comparing to single file.