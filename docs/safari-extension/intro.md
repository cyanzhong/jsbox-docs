# Safari 浏览器扩展

在 iOS 15 及以上，JSBox 为 [Safari 浏览器扩展](https://support.apple.com/zh-cn/guide/iphone/iphab0432bf6/ios) 提供了全面支持，您可以使用 JavaScript 定制自己的 Safari，并且支持自动运行和手动运行两种形式。

关于 Safari 扩展的使用方法，请参考上述 Apple 官方文档，本文档主要讲解开发相关内容。

## JavaScript Web API

与 JSBox 脚本不同的是，Safari 扩展运行在浏览器环境，脚本可以使用所有的 Web 接口，但不能使用 JSBox 专属的接口。

与之相关的开发文档，请查询 Mozilla 的 [Web API 接口参考](https://developer.mozilla.org/zh-CN/docs/Web/API)。

> 您可以在桌面端浏览器或应用内的 WebView 环境测试 Safari 扩展，但在真实的 Safari 环境中测试仍然是必要的步骤。

## Safari 工具

Safari 工具旨在为 Safari 提供扩展功能，需用户手动点击运行，创建方式：

- 新建项目
- Safari 工具

如使用 VS Code 插件创建项目，文件名需以 `.safari-tool.js` 结尾，同步到 JSBox 后会被识别为 Safari 工具。

样例代码：

```js
const video = document.querySelector("video");
if (video) {
  video.webkitSetPresentationMode("picture-in-picture");
} else {
  alert("No videos found.");
}
```

此工具运行后，将会让 YouTube 页面的视频进入画中画模式。

## Safari 规则

Safari 规则旨在为 Safari 提供自动运行的插件，无需用户手动点击运行，创建方式：

- 新建项目
- Safari 规则

如使用 VS Code 插件创建项目，文件名需以 `.safari-rule.js` 结尾，同步到 JSBox 后会被识别为 Safari 规则。

样例代码：

```js
const style = document.createElement("style");
const head = document.head || document.getElementsByTagName("head")[0];
head.appendChild(style);
style.appendChild(document.createTextNode("._9AhH0 { display: none }"));
```

此规则运行后，将会允许用户下载 Instagram 页面的图片。

> 出于安全考虑，Safari 规则默认禁止自动运行，需用户在应用设置中手动开启。