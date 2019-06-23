# Two different ways

We have 2 different ways to handle an asynchronous function:

- You can use Promise directly
- You need to specify `async: true` to indicate it's Promise call

That's really easy to understand, in short, in some cases like:

```js
$ui.menu({
  items: ["A", "B", "C"],
  handler: (title, index) => {

  }
})
```

If you popup a menu, it doesn't make sense to not handle it, so we treat this as a `must be handled` API, you can directly:

```js
var result = await $ui.menu({ items: ["A", "B", "C"] })
var title = result.title
var index = result.index
// Or: var result = await $ui.menu(["A", "B", "C"])
```

But in some other cases, the callback could be omitted, you can simply do nothing:

```js
$photo.delete({
  count: 3,
  screenshot: true,
  handler: success => {
    // It's OK to remove handler here
  }
})
```

In that case you need to specify async mode to use Promise:

```js
var success = await $photo.delete({
  count: 3,
  screenshot: true,
  async: true
})
```

If you don't do that, we will treat this as a normal call instead of Promise.

Also, not all APIs are async calls, some APIs are total sync call, for example:

```js
var success = $file.delete("sample.txt")
```

There's no need (and can't) to provide Promise API for that, we will have a checklist for each API soon.

# Some handy shortcuts

Once you use Promise, you may realize there is only a parameter, so it's not needed to wrap it as JSON:

```js
var resp = await $http.get('https://docs.xteko.com')
```

Remember these shortcuts can save your time:

```js
// Thread
await $thread.main(3)
await $thread.background(3)

// HTTP
var resp = await $http.get('https://docs.xteko.com')
var result = await $http.shorten("http://docs.xteko.com")

// UIKit
var result = await $ui.menu(["A", "B", "C"])

// Cache
var cache = await $cache.getAsync("key")
```