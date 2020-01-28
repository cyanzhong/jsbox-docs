# Built-in Modules

In order to make your life easier, JSBox has bundled some famous JavaScript modules:

- [underscore](https://underscorejs.org/)
- [moment](https://momentjs.com/)
- [crypto-js](https://github.com/brix/crypto-js)
- [cheerio](https://cheerio.js.org/)
- [lodash](https://lodash.com/)
- [ramba](https://ramdajs.com/)

These modules can be used with `require` directly, for instance:

```js
const lodash = require("lodash");
```

Please refer to their documentation, we don't want to be too verbose here.

If you want to use some other modules, you can bundle them with [browserify](http://browserify.org/). Generally, [CommonJS](https://en.wikipedia.org/wiki/CommonJS) modules that don't rely on native code are available.