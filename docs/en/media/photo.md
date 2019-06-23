> JSBox provided a series of APIs to interact with photos

# $photo.take(object)

Take a photo with camera:

```js
$photo.take({
  handler: function(resp) {
    var image = resp.image
  }
})
```

Param | Type | Description
---|---|---
format | string | "image" or "data", default is "image"
edit | boolean | edit image after picked
mediaTypes | array | media types
maxDuration | number | max duration of video
quality | number | quality
showsControls | boolean | shows controls
device | number | front/rear camera
flashMode | number | flash mode

Refer [Constant](en/data/constant.md) to see how constant works.

# $photo.pick(object)

Pick a photo from photo library:

```js
$photo.pick({
  handler: function(resp) {
    var image = resp.image
  }
})
```

All parameters are same as `$photo.take`, they are just have different source type.

Besides, we can set `multi: true` to pick multiple photos, the result list is like:

Prop | Type | Description
---|---|---
status | bool | success
results | array | all images

The structure of an object in result (when format is `image`):

Prop | Type | Description
---|---|---
image | image | image object
metadata | object | metadata

The structure of an object in result (when format is `data`):

Prop | Type | Description
---|---|---
data | data | image file
metadata | object | metadata

# $photo.prompt(object)

Ask user take a photo or pick a photo:

```js
$photo.prompt({
  handler: function(resp) {
    var image = resp.image
  }
})
```

# Get metadata of photo

We can retrieve metadata from a photo:

```js
$photo.pick({
  handler: function(resp) {
    var metadata = resp.metadata
    if (metadata) {
      var gps = metadata["{GPS}"]
      var url = "https://maps.apple.com/?ll=" + gps.Latitude + "," + gps.Longitude
      $app.openURL(url)
    }
  }
})
```

It gets the GPS information, open it in Maps.

# $photo.scan()

Open documentation camera (iOS 13 only):

```js
const response = await $photo.scan();
// response.status, response.results
```

# $photo.save(object)

Save a photo to photo library:

```js
// data
$photo.save({
  data: data,
  handler: function(success) {

  }
})
```

```js
// image
$photo.save({
  image: image,
  handler: function(success) {

  }
})
```

# $photo.fetch(object)

Fetch photos from photo library:

```js
$photo.fetch({
  count: 3,
  handler: function(images) {

  }
})
```

There are some parameters to make fetch operation more accurate:

Param | Type | Description
---|---|---
type | number | type
subType | number | sub type
format | string | "image" or "data", default is "image"
size | $size | image size, default to raw size
count | number | fetch limit

# $photo.delete(object)

Delete photos in photo library:

```js
$photo.delete({
  count: 3,
  handler: function(success) {

  }
})
```

The parameters are same as `$photo.fetch`.

# Convert image object to binary data

We could convert image object to PNG or JPEG data:

```js
// PNG
var png = image.png
// JPEG
var jpg = image.jpg(0.8)
```

There is a number (0.0 ~ 1.0) means jpeg compress quality.