# $context.query

Get all query items (URL Scheme launched script):

```js
var query = $context.query
```

If we use `jsbox://runjs?file=demo.js&text=test` to launch it, the query is:

```js
{
  "file": "demo.js",
  "text": "test"
}
```

# $context.text

Returns a text (user shared a text):

```js
var text = $context.text
```

# $context.textItems

Returns all text items.

# $context.link

Returns a link (user shared a link):

```js
var link = $context.link
```

# $context.linkItems

Returns all link items.

# $context.image

Returns an image (user shared an image):

```js
var image = $context.image
```

# $context.imageItems

Returns all image items.

# $context.safari.items

Returns all Safari items.

```js
var items = $context.safari.items
```

Returns:

```json
{
  "baseURI": "",
  "source": "",
  "location": "",
  "contentType": "",
  "title": "",
  "selection": {
    "html": "",
    "text": "",
    "style": ""
  }
}

# $context.data

Returns a binary data (user shared a file):

```js
var data = $context.data
```

# $context.dataItems

Returns all binary files.

# $context.allItems

Returns all items, ignores the type.

Basically, if we want to get external parameters, use `$context` APIs.

# $context.clear()

Clear all data in the context object, including query and Action Extension objects:

```js
$context.clear();
```

# $context.close()

Close current action extension, the script stops running.