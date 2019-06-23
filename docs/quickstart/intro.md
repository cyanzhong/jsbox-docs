# JavaScript

`JavaScript` 是一门强大而灵活的编程语言，本文假设读者具有基本的 JavaScript 基础。

> 相关资源
> - [w3schools.com](https://www.w3schools.com/js/)
> - [mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

# 相似的项目

JSBox 从理念上来说并没有太多的开创性，有很多 `可以运行脚本` 的产品，他们的形态和理念深深地影响着 JSBox 的开发，比如 `Editorial` 和 `Automator`，他们都是可以通过脚本来设计小程序的产品。

但 JSBox 开发过程中并没有模仿他们设计和实现，并且采用了完全不同的道路，就是基于 `JavaScript`，JSBox 与他们唯一的相似之处是能够运行脚本。

另外，市面上有大量的通过 JavaScript 描述 `Native UI` 的框架，例如 Facebook 的 `React Native` 和阿里的 `Weex`，JSBox 在设计和实现的过程中考虑过直接采用他们的方案，但最终考虑到灵活度的问题没有这样做，主要原因有三点：

- React Native 和 Weex 都是为了跨平台需求而设计的框架
- JSBox 是完全为了 iOS 而生，能更好的描述 iOS 的 Native 控件
- JSBox 有一个更重要的目标是：`尽可能简单和易学`，不会引入 JavaScript 之外的概念

# API 设计原则

- API 都以 `$` 符号开始，例如 `$clipboard`
- 与 `Cocoa` 的哲学相反，JSBox 的 API 会尽可能的短，因为在移动平台上面编写、修改代码不是一件容易的事情
- 绝大部分的时候，参数会是一个 `JavaScript Object`，除非只有一个参数
- 每个扩展有自己的运行环境，这个环境产生的数据是与其他的扩展隔绝的，也会随着扩展的删除而消失

以上是对于 JSBox 的基本介绍，*已经对 JavaScript 有所了解，想要看看[简单样例 >](quickstart/sample.md)。*