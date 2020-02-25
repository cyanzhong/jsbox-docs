> The easiest way to create user preferences

# prefs.json

Start from v1.51.0, you can create user preferences with a simple `prefs.json` in the root folder. It generates settings view for you automatically.

Here is an example:

```json
{
  "title": "SETTINGS",
  "groups": [
    {
      "title": "GENERAL",
      "items": [
        {
          "title": "USER_NAME",
          "type": "string",
          "key": "user.name",
          "value": "default user name"
        },
        {
          "title": "AUTO_SAVE",
          "type": "boolean",
          "key": "auto.save",
          "value": true
        },
        {
          "title": "OTHERS",
          "type": "child",
          "value": {
            "title": "OTHERS",
            "groups": [
              
            ]
          }
        }
      ]
    }
  ]
}
```

In your script, the settings view can be opened with the following code:

```js
$prefs.open(() => {
  // Done
});
```

# Definition

The root element is a JSON object that contains `title` and `groups` nodes. `title` will be displayed as the page title, and `groups` specifies all setting groups in the current page.

Under `groups`, there is a JSON object which contains `title` and `items`. `items` means all setting rows in the current group.

If there is only one group, you can also simplify the configuration as:

```json
{
  "title": "GENERAL",
  "items": [
    {
      "title": "USER_NAME",
      "type": "string",
      "key": "user.name",
      "value": "default user name"
    }
  ]
}
```

A setting item contains the following attributes:

- `title`: title
- `type`: value type, such as "string" or "boolean"
- `key`: the key that will be used to persistent settings
- `value`: default value for the current setting, can be null

# title

In order to make localization easier, a title will be used as the localization key first, if nothing is found in the `strings` folder, itself will be used.

# type

Currently, below types are supported:

- `string`: normal text
- `number`: decimal numbers
- `integer`: integer numbers
- `boolean`: boolean value, shows a switch
- `slider`: decimal between 0 and 1, shows a slider
- `list`: shows a string list, let the user pick one
- `info`: shows a readonly informative text
- `link`: shows a link, tap it to open
- `script`: contains a code snippet, tap it to run
- `child`: child node, tap it to open a new settings view

Types like `string`, `number` or `integer` are relatively easy to use, I'm going to show you some exceptions.

# type: "slider"

It provides a slider that can be used to select a decimal value between 0 and 1. So, the `value` should also between 0 and 1.

If you don't want a value between 0 and 1, you need to do some transformations. In short, take it as a percentage.

# type: "list"

Shows a string list, like a memu:

```json
{
  "title": "IMAGE_QUALITY",
  "type": "list",
  "key": "image.quality",
  "items": ["LOW", "MEDIUM", "HIGH"],
  "value": 1
}
```

It displays "LOW", "MEDIUM" and "HIGH" in a list, and the `value` is actually an `index`. Also, it will be localized.

Note that, `items` are user-facing strings, not something that will be stored. What will be stored is the index value.

# type: "script"

Sometimes, you may want some customizable behaviors, like this:

```json
{
  "title": "TEST",
  "type": "script",
  "value": "require('scripts/test').runTest();"
}
```

# type: "child"

Sometimes, you may want to fold some settings to 2nd level or 3rd level, like this:

```json
{
  "title": "OTHERS",
  "type": "child",
  "value": {
    "title": "OTHERS",
    "groups": []
  }
}
```

The above `value` has exactly the same structure comparing to the root element, you can nest them as much as you can.

# key

`key` is a string that will be used to save/read settings, you have to make sure they are unique in the whole script.

Read settings:

```js
const name = $prefs.get("user.name");
```

In most cases, settings should be changed by users, but just in case you want some flexibility, you can change them programmatically:

```js
$prefs.set("user.name", "cyan");
```

# $prefs.all()

Returns all key values:

```js
const prefs = $prefs.all();
```

Obviously, `$prefs` cannot cover all scenarios, but for most common used ones, it's good enough, and easy to use. Here is an example: https://github.com/cyanzhong/xTeko/tree/master/extension-demos/prefs