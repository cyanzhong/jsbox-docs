> Manage reminder items in Reminders.app

# $reminder.fetch(object)

Fetch reminder items (request access first):

```js
$reminder.fetch({
  startDate: new Date(),
  hours: 2 * 24,
  handler: function(resp) {
    var events = resp.events
  }
})
```

It looks very similar to `$calendar` APIs, the object structure:

Prop | Type | Read/Write | Description
---|---|---|---
title | string | rw | title
identifier | string | r | id
location | string | rw | location
notes | string | rw | notes
url | string | rw | url
modifiedDate | date | r | last modified date
creationDate | date | r | creation date
completed | boolean | rw | is completed
completionDate | date | r | completion date
alarmDate | date | rw | alarm date
priority | number | rw | priority (1 ~ 9) 

# $reminder.create(object)

Create a reminder item:

```js
$reminder.create({
  title: "Hey!",
  alarmDate: new Date(),
  notes: "Hello, World!",
  url: "https://apple.com",
  handler: function(resp) {

  }
})
```

We could have alarm by set `alarmDate` or `alarmDates`.

# $reminder.save(object)

Similar to `$calendar.save`:

```js
$reminder.save({
  event: event,
  handler: function(resp) {

  }
})
```

# $reminder.delete(object)

Delete a calendar item:

```js
$reminder.delete({
  event: event,
  handler: function(resp) {
    
  }
})
```

> You may notice that `$reminder` is very similar to `$calendar`, you're right, they have same structure in iOS.