# $context.query

Get all query items (URL Scheme launched script):

```js
const query = $context.query;
```

If we use `jsbox://runjs?file=demo.js&text=test` to launch it, the query is:

```js
{
  "file": "demo.js",
  "text": "test"
}
```

If the source application is another third-party app, there might be its bundle identifier:

```js
const sourceApp = $context.query.source_app;
```

You can check it when needed, it doesn't work for iOS built-in apps.

# $context.text

Returns a text (user shared a text):

```js
const text = $context.text;
```

# $context.textItems

Returns all text items.

# $context.link

Returns a link (user shared a link):

```js
const link = $context.link;
```

# $context.linkItems

Returns all link items.

# $context.image

Returns an image (user shared an image):

```js
const image = $context.image;
```

# $context.imageItems

Returns all image items.

# $context.safari.items

Returns all Safari items.

```js
const items = $context.safari.items;
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

```

# $context.data

Returns a binary data (user shared a file):

```js
const data = $context.data;
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
