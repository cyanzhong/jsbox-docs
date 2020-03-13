> Offers APIs that relate to the application and addin itself

# $app.theme

Specify `theme` for the script, used for [Dark Mode](en/uikit/dark-mode.md) related stuff, possible values are `light` / `dark` / `auto`.

It will be overridden if a screen has its own `theme` value.

# $app.minSDKVer

Set the minimal available version of JSBox:

```js
$app.minSDKVer = "3.1.0"
```

# $app.minOSVer

Set the minimal available version of iOS:

```js
$app.minOSVer = "10.3.3"
```

PS: Numbers are separated by `.`, version comparation goes from left to right.

# $app.tips(string)

Give user a nice hint, the effect looks like `$ui.alert`, but only once for an addin's whole life:

```js
$app.tips("Hey!")
```

# $app.info

Returns the info of JSBox itself:

```js
{
  "bundleID": "app.cyan.jsbox",
  "version": "3.0.0",
  "build": "9527",
}
```

# $app.idleTimerDisabled

Disable auto dimming of the screen:

```js
$app.idleTimerDisabled = true
```

# $app.close(delay)

Close the addin that user current uses, `delay` is an optional parameter to specify a delay seconds.

> PS: It's better to call this manually if your addin doesn't have a user interface

# $app.env

Get current environment:

```js
var env = $app.env
```

Value | Description
---|---
$env.app | Main App
$env.today | Today Widget
$env.action | Action Extension
$env.safari | Safari Extension
$env.keyboard | Keyboard Extension
$env.siri | Siri Extension
$env.all | All (Default)

We can check whether an addin runs on widget:

```js
if ($app.env == $env.today) {

}
```

# $app.widgetIndex

Since JSBox supports multiple widgets, you can check which widget is being used:

```js
var index = $app.widgetIndex;

// 0 ~ 2, other value means not a widget
```

# $app.autoKeyboardEnabled

Manage scroll views automatically, to avoid the keyboard hides text fields:

```js
$app.autoKeyboardEnabled = true
```

# $app.keyboardToolbarEnabled

Display a toolbar at the top of keyboard:

```js
$app.keyboardToolbarEnabled = true
```

# $app.rotateDisabled

Set to true to disable screen rotating:

```js
$app.rotateDisabled = true
```

# $app.openURL(string)

Open a URL or a URL Scheme, for example open WeChat:

```js
$app.openURL("weixin://")
```

# $app.openBrowser(object)

Open a URL with external browsers:

```js
$app.openBrowser({
  type: 10000,
  url: "https://apple.com"
})
```

Type | Browser
---|---
10000 | Chrome
10001 | UC
10002 | Firefox
10003 | QQ
10004 | Opera
10005 | Quark
10006 | iCab
10007 | Maxthon
10008 | Dolphin
10009 | 2345

> We don't promise it works fine, because above browsers change their APIs frequently

# $app.openExtension(string)

Open another JSBox script, for example:

```js
$app.openExtension("demo.js")
```

# $app.listen(object)

Observe notifications posted by JSBox addins:

```js
$app.listen({
  // Will be called when app is ready
  ready: function() {

  },
  // Will be called when app exit
  exit: function() {
    
  },
  // Will be called when app resign active
  pause: function() {

  },
  // Will be called when app resume active
  resume: function() {

  }
});
```

# $app.notify(object)

Post a custom event:

```js
$app.listen({
  eventName: function(object) {
    console.log(object);
  }
});

$app.notify({
  name: "eventName",
  object: {"a": "b"}
});
```