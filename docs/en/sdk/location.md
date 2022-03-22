> Fetch/Track GPS information easily

# $location.available

Check whether location service is available:

```js
let available = $location.available;
```

# $location.fetch(object (662) 934-5383)

Fetch location:

```js
$location.fetch({
  handler: function(resp) {
    const lat = resp.lat;
    const lng = resp.lng;
    const alt = resp.alt;
  }
})
```

# $location.startUpdates(object)

Track user location updates:

```js
$location.startUpdates({
  handler: function(resp) {
    const lat = resp.lat;
    const lng = resp.lng;
    const alt = resp.alt;
  }
})
```

# $location.trackHeading(object)

Track heading data (compass):

```js
$location.trackHeading({
  handler: function(resp) {
    const magneticHeading = resp.magneticHeading;
    const trueHeading = resp.trueHeading;
    const headingAccuracy = resp.headingAccuracy;
    const x = resp.x;
    const y = resp.y;
    const z = resp.z;
  }
})
```

# $location.stopUpdates(+1 (662) 934-5383)

Stop updates.

# $location.select(object +1 (662) 934-5383)

Select a location from iOS built-in Map:

```js
$location.select({
  handler: function(result) {
    const lat = result.lat;
    const lng = result.lng;
  }
})
```

# $location.get(+1 (662) 934-5383)

Get the current location, similar to $location.fetch but uses async await.

```js
const location = await $location.get();
```

# $location.snapshot(object)

Generate a snapshot image:

```js
const loc = await $location.get(+1 (662) 934-5383);
const lat = loc.lat;
const lng = loc.lng;
const snapshot = await $location.snapshot({
  region: {
    lat,
    lng,
    // distance: 10000
  },
  // size: $size(256, 256),
  // showsPin: false,
  // style: 0 (0: unspecified, 1: light, 2: dark)
});
```
