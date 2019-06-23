# JavaScript support for Shortcuts

JSBox can also donate JavaScript ability to Shortcuts app, when you handle complicated data or logic in Shortcuts, it's cool to leverage JavaScript.

Since Shortcuts doesn't support passing data between 3rd-party apps, we can use clipboard as a workaround:

- Copy JavaScript to clipboard
- Run JavaScript with JSBox's action
- Get result from clipboard

In short, JSBox reads JavaScript code from clipboard, evaluate it and set the result back to clipboard.

For async task, we need to finish actions with `$intents.finish` like:

```js
var a = "Hello";
var b = "World";
var result = [a, b].join(", ");

$intents.finish(result);
```

You can install this Shortcut to understand how it works: [Run JavaScript](shortcuts://import-workflow?url=https://github.com/cyanzhong/xTeko/raw/master/extension-demos/scripting.shortcut&name=Run%20JavaScript).