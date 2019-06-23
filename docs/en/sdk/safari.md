> APIs related to Safari or Safari View Controller

# $safari.open(object)

Open website with [Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller):

```js
$safari.open({
  url: "https://www.apple.com",
  entersReader: true,
  height: 360,
  handler: function() {

  }
})
```

`entersReader`: enters reader if available, optional.

`height`: the height when it runs on widget, optional.

`handler`: callback to handle dismiss event.

Above 3 parameters are optional.

# $safari.items

Get items in Safari when you are using Action Extension:

```js
var items = $safari.items // JSON format
```

# $safari.inject(script)

Inject JavaScript code to Safari when you are using Action Extension:

```js
$safari.inject("window.location.href = 'https://apple.com';")
```

The action extension will be closed, and the JavaScript will be executed on Safari.

More useful examples: https://github.com/cyanzhong/xTeko/tree/master/extension-scripts/safari-extensions

# $safari.addReadingItem(object)

Add item to Safari reading list:

```js
$safari.addReadingItem({
  url: "https://sspai.com",
  title: "Title", // Optional
  preview: "Preview text" // Optional
})
```