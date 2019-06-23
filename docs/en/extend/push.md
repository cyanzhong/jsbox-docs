> Used to schedule a notification or cancel a scheduled notification

# $push.schedule(object)

Schedule a local notification:

```js
$push.schedule({
  title: "title",
  body: "content",
  delay: 5,
  handler: function(result) {
    var id = result.id
  }
})
```

This notification will be delivered after 5 seconds.

Param | Type | Description
---|---|---
title | string | title
body | string | body
id | string | identifier (optional)
sound | string | sound
mute | bool | mute
repeats | bool | repeats
script | string | script name
height | number | 3D Touch view height
query | json | extra parameters, will be passed to $context.query
attachments | array | media attachments, e.g. ["assets/icon.png"]
renew | bool | whether renew

Above case is how to schedule a push with delay, you can also setup a date:

```js
var date = new Date()
date.setSeconds(date.getSeconds() + 10)

$push.schedule({
  title: "title",
  body: "content",
  date: date,
  handler: function(result) {
    var id = result.id
  }
})
```

Not only that, you have another cool choice, schedule by location:

```js
$push.schedule({
  title: "title",
  body: "content",
  region: {
    lat: 0, // latitude
    lng: 0, // longitude
    radius: 1000, // meters
    notifyOnEntry: true, // notify on entry
    notifyOnExit: true // notify on exit
  }
})
```

JSBox will ask user for location access once this code get called.

Started from v1.10.0, $push supports setup a script to push notification by setting `script`, user can tap to run it, or simply force touch to have a quick preview.

# $push.cancel(object)

Cancel a scheduled notification:

```js
$push.cancel({
  title: "title",
  body: "content",
})
```

JSBox will cancel all notifications that match the `title` and `body`.

You can also can it the identifier:

```js
$push.cancel({id: ""})
```

# $push.clear()

Clear all scheduled notifications (notifications that registered before build 462 will be ignored):

```js
$push.clear()
```