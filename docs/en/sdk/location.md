> Fetch/Track GPS information easily

# $location.available

Check whether location service is available:

```js
let available = $location.available;
```

# $location.fetch(object)

Fetch location:

```js
$location.fetch({
  handler: function(resp) {
    var lat = resp.lat
    var lng = resp.lng
    var alt = resp.alt
  }
})
```

# $location.startUpdates(object)

Track user location updates:

```js
$location.startUpdates({
  handler: function(resp) {
    var lat = resp.lat
    var lng = resp.lng
    var alt = resp.alt
  }
})
```

# $location.trackHeading(object)

Track heading data (compass):

```js
$location.trackHeading({
  handler: function(resp) {
    var magneticHeading = resp.magneticHeading
    var trueHeading = resp.trueHeading
    var headingAccuracy = resp.headingAccuracy
    var x = resp.x
    var y = resp.y
    var z = resp.z
  }
})
```

# $location.stopUpdates()

Stop updates.

# $location.select(object)

Select a location from iOS built-in Map:

```js
$location.select({
  handler: function(result) {
    var lat = result.lat
    var lng = result.lng
  }
})
```