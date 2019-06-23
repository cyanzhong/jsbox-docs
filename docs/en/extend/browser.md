# $browser.exec

Provides a webView based JavaScript environment, lets you use Web APIs:

```js
$browser.exec({
  script: function() {
    var parser = new DOMParser();
    var doc = parser.parseFromString("<a>hey</a>", "application/xml");
    // $notify("customEvent", {"key": "value"})
    return doc.children[0].innerHTML;
  },
  handler: function(result) {
    $ui.alert(result);
  },
  customEvent: function(message) {

  }
})
```

# Handy shortcut

You can use Promise with super neat style:

```js
var result = await $browser.exec("return 1 + 1;");
```

# How to access variables in native

You can create script dynamically by:

```js
var name = "JSBox"
$browser.exec({
  script: `
  var parser = new DOMParser();
  var doc = parser.parseFromString("<a>hey ${name}</a>", "application/xml");
  return doc.children[0].innerHTML;`,
  handler: function(result) {
    $ui.alert(result);
  }
})
```

For details of `$notify`, refer to [web component](en/component/web.md?id=notifyevent-message).