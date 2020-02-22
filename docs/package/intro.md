# JSBox 安装包格式

从 `v1.9.0` 开始，JSBox 不仅支持运行单个 JavaScript 文件，还设计了自己的安装包格式，可以带来如下好处：

- 可以将代码模块化，不需要将所有逻辑都放在同一个文件
- 可以将配置文件化，这样更容易维护
- 可以内置图片等资源，从而不需要通过 Base64 等手段引入图片

# 格式说明

JSBox 安装包格式是一个 zip 文件，只要文件目录包含以下结构则会被认为是一个 JSBox 安装包：

- **assets/** 用于存放资源
- **scripts/** 用于存放脚本
- **strings/** 用于存放本地化字符串
- **config.json** 安装包配置文件
- **main.js** 脚本主要入口，在这里加载其他脚本

这是一个样例：https://github.com/cyanzhong/xTeko/tree/master/extension-demos/package

你也可以通过 JSBox 应用直接创建一个应用模板。

# assets

将应用将用到的资源文件放置于这里，然后可以通过 `assets/filename` 样式的路径引用文件。

这些文件可以被用在 `$file` 相关接口，也可以作为 `src` 被设置为 image 或 button 等组件。

该文件夹默认包含一个 `icon.png`，这将作为应用的图标，在设置里面切换图标将会替换这个文件，你也可以手动替换这个文件以实现自定义图标。

图标制作标准请参考：https://github.com/cyanzhong/xTeko/tree/master/extension-icons

# scripts

将会用到的脚本放到这个文件夹下，可以通过 `require('scripts/utility')` 样式的代码模块化的加载文件，我们稍后会介绍如何模块化。

你可以在这个文件夹下面建立子文件夹，将脚本放到合适的位置，从而实现整个应用的架构划分。

# strings

这个文件夹提供的功能与 `$app.strings` 类似，即为 `$l10n` 提供本地化的字符串，默认包含：

- **en.strings** 英文
- **zh-Hans.strings** 中文简体

strings 文件是一个如下格式的文本文件（键值对）：

```
"OK" = "好的";
"DONE" = "完成";
"HELLO_WORLD" = "你好，世界！";
```

PS: 如果你同时使用了 strings 文件和 $app.strings，将以后者为准。

# config.json

此文件目前包含两个部分，一个是安装文件的元信息，位于 `info` 节点下面，请参考：[$addin](addin/method.md?id=addinlist)。

另一部分是 `settings` 节点，这部分设置与 `$app` 接口相关的一些设置相同，请参考：[$app](foundation/app.md?id=appminsdkver)。

使用 config.json 能更好的组织你的设置项，以后新增的设置项也会被放到这里。

# main.js

当一个应用被执行的时候，main.js 将是入口，在这里我们可以加载 scripts 文件夹里面的脚本，例如：

```js
var app = require('./scripts/app');

app.sayHello();
```

这将会以模块的形式引入 `scripts/app.js` 这个文件，然后调用该文件的 `sayHello` 函数，我们将稍后介绍这个机制。