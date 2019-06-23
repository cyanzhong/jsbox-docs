> Persistence is always needed for a software, JSBox offers various persistence ways, cache is the easiest one

# Hint

JSBox provides memory cache and disk cache with a really simple interface, all JavaScript objects could be cached.

All APIs have both `sync` and `async` ways, choose one according to your scenarios.

# $cache.set(string, object)

Write to cache:

```js
$cache.set("sample", {
  "a": [1, 2, 3],
  "b": "1, 2, 3"
})
```

# $cache.setAsync(object)

Write to cache (async):

```js
$cache.setAsync({
  key: "sample",
  value: {
    "a": [1, 2, 3],
    "b": "1, 2, 3"
  },
  handler: function(object) {

  }
})
```

# $cache.get(string)

Read from cache:

```js
$cache.get("sample")
```

# $cache.getAsync(object)

Read from cache (async):

```js
$cache.getAsync({
  key: "sample",
  handler: function(object) {

  }
})
```

# $cache.remove(string)

Delete a cache:

```js
$cache.remove("sample")
```

# $cache.removeAsync(object)

Delete a cache (async):

```js
$cache.removeAsync({
  key: "sample",
  handler: function() {
    
  }
})
```

# $cache.clear()

Delete all cached objects:

```js
$cache.clear()
```

# $cache.clearAsync(object)

Delete all cached objects (async):

```js
$cache.clearAsync({
  handler: function() {

  }
})
```