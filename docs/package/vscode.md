# VSCode

JSBox 从一开始就提供了 VSCode 插件：https://marketplace.visualstudio.com/items?itemName=Ying.jsbox

你可以用这个插件增强你写 JSBox 脚本的体验，他可以帮你将脚本从桌面端实时同步到手机端（在同一个 Wi-Fi 下面），也提供了简单的自动补全功能。

从 0.0.6 版本开始，JSBox 的 VSCode 插件也支持了安装包格式，只要当前编辑的文件夹符合 JSBox 安装包的定义：

- **assets/**
- **scripts/**
- **strings/**
- **config.json**
- **main.js**

同步的时候则会将整个目录（安装包）同步到手机，然后运行。