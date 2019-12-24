*本文档基于 [Docsify](https://docsify.js.org) 部署在 [GitHub](https://github.com/cyanzhong/jsbox-docs)，欢迎一起改进*

# JSBox APIs

通过 JavaScript 来为 JSBox 提供强大的扩展，支持 ES6 标准语法，并提供了丰富的 API 来与 Native 代码进行交互。

# JSBox Node.js

JSBox 从 2.0 开始，提供了对 Node.js 运行时的支持。关于这一部分的内容，请参考专门的文档：https://cyanzhong.github.io/jsbox-nodejs/#/

# 如何在 JSBox 里运行代码

- 在 JSBox 里面直接编写

  > JSBox 内置了一个简单的 js 编辑器，目前只提供了基本的代码高亮和自动补全，随着之后的版本更新将会提供更好的编辑器。

- 通过 URL Scheme 在线安装

  > 例如通过在 iOS 设备上点击：jsbox://import?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcyanzhong%2FxTeko%2Fmaster%2Fextension-scripts%2Fapi.js&name=%E6%B5%8B%E8%AF%95%E5%9C%A8%E7%BA%BF%E5%AE%89%E8%A3%85&icon=icon_063.png
  > 将会打开 JSBox 自动安装脚本，支持 `url`, `name`(可选), `icon`(可选) 3 个参数，均需要 URL Encode
  > icon 名称具体请参考：https://github.com/cyanzhong/xTeko/tree/master/extension-icons
  > 在线文件 URL 中请使用纯英文名

- 通过 VSCode 插件同步编辑

  > 1. 打开 JSBox 中任意一个脚本，进入设置页面打开调试模式
  > 2. 回到桌面后重新打开应用，打开设置 Tab 查看本机 HOST
  > 3. 在 VSCode 的扩展商店搜索安装 `JSBox` 插件
  > 4. 在 VSCode 打开 JavaScript 文件，点击菜单中的 `Set Host` 选项填入步骤 2 的 HOST
  > 5. 至此，编辑保存 JavaScript 文件之后，将同步运行到 JSBox 应用

- 通过 AirDrop 传输脚本

  > 你可以通过文件分享或 AirDrop 把脚本传输到 JSBox，但你需要手动同步被导入进来的脚本
  > 可以通过类似这个样例的脚本进行同步：https://github.com/cyanzhong/xTeko/blob/master/extension-demos/sync-inbox.js

- 发挥你的创造力，利用 JSBox 提供的接口获取脚本

  > 例如这个例子：https://github.com/cyanzhong/xTeko/blob/master/extension-demos/addin-gallery.js

# 开源项目

为了提供更多的样例代码，我们准备了一个开源项目：https://github.com/cyanzhong/xTeko

欢迎一起完善这个项目，通过 [提交 Issue](https://github.com/cyanzhong/xTeko/issues/new) 或 [提交 PR](https://github.com/cyanzhong/xTeko/compare) 等贡献方式。

# 联系我们

对文档有任何疑问都可以通过以下方式联系我们：

- Email: [log.e@qq.com](mailto:log.e@qq.com)
- Weibo: [@StackOverflowError](https://weibo.com/0x00eeee)
- Twitter: [@cyanapps](https://twitter.com/cyanapps)
- Telegram: [PinTG](https://t.me/PinTG)

*准备好了，[快速开始 >](quickstart/intro.md)*

> 此文档目前处于测试阶段，之后可能会有变化，如有错误欢迎指正。