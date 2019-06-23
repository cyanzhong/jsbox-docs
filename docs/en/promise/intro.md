# Promise

Promise is an elegant solution to resolve callback hell, please refer to Mozilla's doc to have a better understanding: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise

Of course you can use Promise in JSBox, but previously APIs that we provided don't support Promise style, for example:

```js
$http.get({
  url: 'https://docs.xteko.com',
  handler: function(resp) {
    var data = resp.data
  }
})
```

You have to specify a handler to take next action, but since v1.15.0, you have better solution:

```js
$http.get({ url: 'https://docs.xteko.com' }).then(function(resp) {
  var data = resp.data
})
```

This can save you from callback hell, or even better (>= iOS 10.3):

```js
var resp = await $http.get({ url: 'https://docs.xteko.com' })
var data = resp.data
```

Or, you can use a very handy shortcut:

```js
var resp = await $http.get('https://docs.xteko.com')
var data = resp.data
```

There are so many details in Promise, we don't want to go deep at here, but we recommend you this article: https://javascript.info/async

Overall, we provide Promise style for JSBox APIs.