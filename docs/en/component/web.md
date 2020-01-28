# type: "web"

`web` is used to render a website:

```js
{
  type: "web",
  props: {
    url: "https://www.apple.com"
  },
  layout: $layout.fill
}
```

It shows the home page of Apple.

# Load local resources

You can load html, js and css files locally:

```js
let html = $file.read("assets/index.html").string;
$ui.render({
  views: [
    {
      type: "web",
      props: {
        html: html
      },
      layout: $layout.fill
    }
  ]
});
```

```html
<html>
  <head>
    <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">
    <link rel="stylesheet" href="local://assets/index.css">
    <script src="local://assets/index.js"></script>
  </head>
  <body>
    <h1>Hey, there!</h1><img src="local://assets/icon.png">
  </body>
  <script>
    window.onload = () => {
      alert(sum(1, 1));
    }
  </script>
</html>
```

Local files will be loaded from bundle, `shared://` and `drive://` are supported.

# props

Prop | Type | Read/Write | Description
---|---|---|---
title | string | r | web page title
url | string | w | address
toolbar | bool | w | shows a toolbar
html | string | w | html content
text | string | w | text content
loading | boolean | r | is loading
progress | number | r | loading progress
canGoBack | boolean | r | can go back
canGoForward | boolean | r | can go forward
ua | string | w | User Agent
scrollEnabled | bool | rw | is scroll enabled
bounces | bool | rw | is bounces enabled
transparent | bool | rw | is background transparent
showsProgress | bool | w | whethe shows progress bar
inlineMedia | bool | w | allows inline video
airPlay | bool | w | allows AirPlay
pictureInPicture | bool | w | allows picture in picture
allowsNavigation | bool | rw | allows back gestures
allowsLinkPreview | bool | rw | allows link preview

# goBack()

Go back.

# goForward()

Go forward.

# reload()

Reload current page.

# reloadFromOrigin()

Reload from origin.

# stopLoading()

Stop loading.

# eval(object)

Evaluate JavaScript:

```js
webView.eval({
  script: "var sum = 1 + 2",
  handler: function(result, error) {

  }
})
```

# exec(script)

Similar to `eval`, but this one is an async function:

```js
const {result, error} = await webView.exec("1 + 1");
```

# events: didClose

`didClose` will be called after closed:

```js
didClose: function(sender) {

}
```

# events: decideNavigation

`decideNavigation` can be used to intercept requests:

```js
decideNavigation: function(sender, action) {
  if (action.requestURL === "https://apple.com") {
    return false
  }
  return true
}
```

# events: didStart

`didStart` will be called after started:

```js
didStart: function(sender, navigation) {

}
```

# events: didReceiveServerRedirect

`didReceiveServerRedirect` will be called after received server redirect:

```js
didReceiveServerRedirect: function(sender, navigation) {

}
```

# events: didFinish

`didFinish` will be called after load finished:

```js
didFinish: function(sender, navigation) {

}
```

# events: didFail

`didFail` will be called after load failed:

```js
didFail: function(sender, navigation, error) {

}
```

# events: didSendRequest

`didSendRequest` will be called after XMLHttpRequest sent:

```js
didSendRequest: function(request) {
  var method = request.method
  var url = request.url
  var header = request.header
  var body = request.body
}
```

# JavaScript Injection

We could control the web view by inject JavaScript, for example:

```js
props: {
  script: function() {
    var images = document.getElementsByTagName("img")
    for (var i=0; i<images.length; ++i) {
      var element = images[i]
      element.onclick = function(event) {
        var source = event.target || event.srcElement
        $notify("share", {"url": source.getAttribute("data-original")})
        return false
      }
    }
  }
}
```

`script` is a `function`, all code inside it will be executed after website load finished.

`script` could also be a `string`, but need to be escaped, for example use [Escape](https://www.freeformatter.com/json-escape.html):

```js
props: {
  script: "for(var images=document.getElementsByTagName(\"img\"),i=0;i<images.length;++i){var element=images[i];element.onclick=function(e){var t=e.target||e.srcElement;return $notify(\"share\",{url:t.getAttribute(\"data-original\")}),!1}}"
}
```

Obviously, use function as script looks more delightful.

# $notify(event, message)

Send message from script to native components, `$notify` message to `events`:

```js
props: {
  script: function() {
    $notify("customEvent", {"key": "value"})
  }
},
events: {
  customEvent: function(object) {
    // object = {"key": "value"}
  }
}
```

The message will be passed to `events -> customEvent`, we could handle native events here.

Above logic looks a bit complicated, please check this example:

```js
$ui.render({
  props: {
    title: "Doutu"
  },
  views: [
    {
      type: "button",
      props: {
        title: "Search"
      },
      layout: function(make) {
        make.right.top.inset(10)
        make.size.equalTo($size(64, 32))
      },
      events: {
        tapped: function(sender) {
          search()
        }
      }
    },
    {
      type: "input",
      props: {
        placeholder: "Please input keywords"
      },
      layout: function(make) {
        make.top.left.inset(10)
        make.right.equalTo($("button").left).offset(-10)
        make.height.equalTo($("button"))
      },
      events: {
        returned: function(sender) {
          search()
        }
      }
    },
    {
      type: "web",
      props: {
        script: "for(var images=document.getElementsByTagName(\"img\"),i=0;i<images.length;++i){var element=images[i];element.onclick=function(e){var t=e.target||e.srcElement;return $notify(\"share\",{url:t.getAttribute(\"data-original\")}),!1}}"
      },
      layout: function(make) {
        make.left.bottom.right.equalTo(0)
        make.top.equalTo($("input").bottom).offset(10)
      },
      events: {
        share: function(object) {
          $http.download({
            url: "http:" + object.url,
            handler: function(resp) {
              $share.universal(resp.data)
            }
          })
        }
      }
    }
  ]
})

function search() {
  var keyword = $("input").text
  var url = "https://www.doutula.com/search?keyword=" + encodeURIComponent(keyword)
  $("input").blur()
  $("web").url = url
}

$("input").focus()
```

# CSS Injection

Similar to JavaScript Injection, CSS Injection is also supported:

```js
props: {
  style: ""
}
```

Of course, you can implement this by using JavaScript Injection, it's just an easy way.

# webView.notify

Native code could send message to web view as well, just use `notify(event, message)`:

```js
var webView = $("webView");
webView.notify({
  "event": "foobar",
  "message": {"key": "value"}
});
```

Above mechanism provies opportunity to switch context between web and native.