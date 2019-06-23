# Promise

Promise 是一种为了解决回调地狱而引入的方案，请参考 Mozilla 的文档了解更多：https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise

JSBox 里面当然可以使用 Promise，但是 JSBox 里面提供的接口早期并不支持 Promise，只支持通过 callback 回调，比如说：

```js
$http.get({
  url: 'https://docs.xteko.com',
  handler: function(resp) {
    var data = resp.data
  }
})
```

这个例子通过 `handler` 进行下一步操作，但从 v1.15.0 开始，你可以有更好的方案：

```js
$http.get({ url: 'https://docs.xteko.com' }).then(function(resp) {
  var data = resp.data
})
```

这种写法可以避免你陷入回调地狱，或者更进一步地（iOS 10.3 以上）：

```js
var resp = await $http.get({ url: 'https://docs.xteko.com' })
var data = resp.data
```

如果你为了测试之用，对于 `$http.get` 你还能使用这个极简形式：

```js
var resp = await $http.get('https://docs.xteko.com')
var data = resp.data
```

关于 Promise 的种种细节，本文档不会详细描述，但这里会推荐一篇文档：https://javascript.info/async

总的来说，JSBox 现在已经对于一些 API 提供了 Promise 调用。