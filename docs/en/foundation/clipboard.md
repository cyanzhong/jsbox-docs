> Clipboard is very important for iOS data sharing, JSBox provides various interfaces

# $clipboard.text

```js
// Get clipboard text
var text = $clipboard.text
// Set clipboard text
$clipboard.text = "Hello, World!"
```

# $clipboard.image

```js
// Get clipboard image data
var data = $clipboard.image
// Set clipboard image data
$clipboard.image = data
```

# $clipboard.items

```js
// Get all items from clipboard
var items = $clipboard.items
// Set items to clipboard
$clipboard.items = items
```

# $clipboard.phoneNumbers

Get all phone numbers from clipboard.

# $clipboard.phoneNumber

Get the first phone number from clipboard.

# $clipboard.links

Get all links from clipboard.

# $clipboard.link

Get the first link from clipboard.

# $clipboard.emails

Get all emails from clipboard.

# $clipboard.email

Get the first email from clipboard.

# $clipboard.dates

Get all dates from clipboard.

# $clipboard.date

Get the first date from clipboard.

# $clipboard.setTextLocalOnly(string)

Set text to clipboard, but ignore `Universal Clipboard`.

# $clipboard.set(object)

Set clipboard by `type` and `value`:

```js
$clipboard.set({
  "type": "public.plain-text",
  "value": "Hello, World!"
})
```

# $clipboard.copy(object)

Set clipboard, you can provide an expiration date:

```js
$clipboard.copy({
  text: "Temporary text",
  ttl: 20
})
```

Param | Type | Description
---|---|---
text | string | text
image | image | image
data | data | data
ttl | number | time to live
locally | bool | locally

*`UTTypes`: https://developer.apple.com/documentation/mobilecoreservices/uttype*

# $clipboard.clear()

Clear all items in clipboard.