# JSBox Package

Starting from `v1.9.0`, JSBox supports both JavaScript file and package format.

There're so many advantages:

- Modularize code by multiple files, folders
- JSON file based configurations
- Built-in resources like images, audio files

# Format Design

JSBox Package is actually a zip file, any zip file including these structure will be considered as a package:

- **assets/** Resources folder
- **scripts/** Scripts folder
- **strings/** Localization strings folder
- **config.json** Configurations
- **main.js** The main entrance

Here's an example: https://github.com/cyanzhong/xTeko/tree/master/extension-demos/package

By the way, you can also generate a package template inside JSBox app.

# assets

Put the resource files of your app here, you can refer them by path like `assets/filename`.

These files could be used in `$file` related APIs, also it can be a `src` for image and button.

There's an `icon.png` inside by default, the icon of this app, you replace it with your own design.

For the spec of icon, please refer to: https://github.com/cyanzhong/xTeko/tree/master/extension-icons

# scripts

Put script files here, you can require them by syntax like `require('./scripts/utility')`, we will introduce modules soon.

You can also create sub-folders here, with this said you can manage your scripts gracefully.

# strings

This folder is designed for providing localizable strings, in other words, provide resource for `$l10n`:

- **en.strings** English
- **zh-Hans.strings** Simplified-Chinese

The pattern of a string file:

```
"OK" = "好的";
"DONE" = "完成";
"HELLO_WORLD" = "你好，世界！";
```

PS: If you're using `strings` files and `$app.strings` at the same time, the later one will be used.

# config.json

Currently this file including 2 parts, the `info` node represents metadata of the app, refer: [$addin](en/addin/method.md?id=addinlist).

The `settings` node provides some settings like `$app` provided formerly: [$app](en/foundation/app.md?id=appminsdkver)

We will add more settings here in near future.

# main.js

main.js is the main entrance of an app, we can load other scripts here:

```js
var app = require('./scripts/app');

app.sayHello();
```

We are gonna to talk about how it works.