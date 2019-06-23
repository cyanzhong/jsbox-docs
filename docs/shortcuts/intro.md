# 什么是捷径（Shortcuts）

被 Apple 收购的 Workflow 应用最终被重新塑造成了捷径应用，如果你还不知道这是什么，你可以通过[这篇文章](https://mp.weixin.qq.com/s/JGKnkHNFcz0I_A1n__-JsA)了解一下。

简单说，捷径和 Workflow 基本一样，但能够与 Siri 有更深的结合，同时也可以更好的和第三方应用协作。

当我们在说捷径的时候，指代的是下面两个部分：

- Siri 中的捷径语音指令
- 捷径独立应用（前 Workflow）

# JSBox 如何支持 Shortcuts

就目前而言，我们在 JSBox 上面设计了以下几个功能：

- 通过语音在 Siri 界面运行 JSBox 脚本
- 在 Siri 和捷径应用里面运行 JSBox 脚本
- 在 Siri 界面显示由 JSBox 脚本编写的界面
- 在捷径应用里面利用 JSBox 运行 JavaScript

# 注意事项

- 需要 iOS 12 及以上的系统版本
- 捷径独立应用请在 App Store 安装