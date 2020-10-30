> We can manage our scripts with $addin APIs

# $addin.list

Get all installed addins (scripts):

```js
var addins = $addin.list
```

Data Structure:

Prop | Type | Read/Write | Description
---|---|---|---
name | string | rw | name
category | string | rw | category
url | string | rw | url
data | $data | rw | file
id | string | rw | id
version | string | rw | version number
icon | string | rw | icon name
iconImage | image | r | icon image
module | bool | rw | whether a module
author | string | rw | author name
website | string | rw | author website

Only `name` and `data` are necessary, other fields are optional.

You can modify the `addins`, such as reordering, and save it like this:

```js
$addin.list = addins;
```

# $addin.categories

Returns all categories as a string array:

```js
const categories = $addin.categories;
```

You can modify it, such as reordering or adding new category, and save it like this:

```js
$addin.categories = categories;
```

# $addin.current

Get current running addin:

```js
var current = $addin.current
```

# $addin.save(object)

Install a new addin:

```js
$addin.save({
  name: "New Script",
  data: $data({string: "$ui.alert('Hey!')"}),
  handler: function(success) {
    
  }
})
```

JSBox will install a new script named `New Script`, the data structure just like we mentioned before.

# $addin.delete(name)

Delete an installed addin:

```js
$addin.delete("New Script")
```

A script named `New Script` will be deleted.

# $addin.run(name)

Run a script with name:

```js
$addin.run("New Script")
```

A script named `New Script` will be started.

Since v1.15.0, you can also put an extra parameter here:

```js
$addin.run({
  name: "New Script",
  query: {
    "a": "b"
  }
})
```

It will be passed to `$context.query`.

# $addin.restart()

Restart current running script.

# $addin.compile(script)

Convert scripts to JSBox syntax:

```js
var result = $addin.compile("$ui.alert('Hey')");

// result => JSBox.ui.alert('Hey')
```

# $addin.eval(script)

Similar to `eval()`, but convert script to JSBox syntax first:

```js
$addin.eval("$ui.alert('Hey')");
```