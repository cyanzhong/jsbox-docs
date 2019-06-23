> Manage calendar items in Calendar.app

# $calendar.fetch(object)

Fetch calendar items (request access first):

```js
$calendar.fetch({
  startDate: new Date(),
  hours: 3 * 24,
  handler: function(resp) {
    var events = resp.events
  }
})
```

Fetch all calendar items from now to 3 days later, we could either use `hours` or `endDate`.

The structure of an object in results is:

Prop | Type | Read/Write | Description
---|---|---|---
title | string | rw | title
identifier | string | r | id
location | string | rw | location
notes | string | rw | notes
url | string | rw | url
modifiedDate | date | r | last modified date
creationDate | date | r | creation date
allDay | boolean | r | is all day event
startDate | date | r | start date
endDate | date | r | end date
status | number | r | [Refer](https://developer.apple.com/documentation/eventkit/ekeventstatus)

# $calendar.create(object)

Create a calendar item:

```js
$calendar.create({
  title: "Hey!",
  startDate: new Date(),
  hours: 3,
  notes: "Hello, World!",
  handler: function(resp) {

  }
})
```

# $calendar.save(object)

Save modified calendar item:

```js
$calendar.fetch({
  startDate: new Date(),
  hours: 3 * 24,
  handler: function(resp) {
    var event = resp.events[0]
    event.title = "Modified"
    $calendar.save({
      event: event
    })
  }
})
```

# $calendar.delete(object)

Delete a calendar item:

```js
$calendar.delete({
  event: event,
  handler: function(resp) {
    
  }
})
```