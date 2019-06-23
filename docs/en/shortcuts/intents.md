# Run JSBox script

It's very easy to run JSBox script in Siri/Shortcuts app, you can send a request and return a result for it.

All you need to do is use `$intents.finish()` like:

```js
var result = await $http.get("");

$intents.finish(result.data);
```

You can do it asynchronously, and finish it with `$intents.finish()`.

If you want to run code synchronously, you can simply ignore `$intents.finish()`, the shortcut will be finished automatically.

# Specify view height

By default, the view height is 320, you can change it by:

```js
$intents.height = 180;
```