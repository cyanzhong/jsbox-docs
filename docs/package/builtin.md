# 内置模块

为了更方便使用，JSBox 内置了一些常见的模块：

- [underscore](https://underscorejs.org/)
- [moment](https://momentjs.com/)
- [crypto-js](https://github.com/brix/crypto-js)
- [cheerio](https://cheerio.js.org/)
- [lodash](https://lodash.com/)
- [ramba](https://ramdajs.com/)

这些模块无需打包在安装包内部即可被脚本通过 require 使用，例如：

```js
const lodash = require("lodash");
```

请参考模块各自的文档来使用，在本文档中不再赘述。

如果有其他模块的使用需求，可以通过 [browserify](http://browserify.org/) 进行打包，没有 native 依赖并符合 [CommonJS](https://en.wikipedia.org/wiki/CommonJS) 标准的模块一般可以使用。