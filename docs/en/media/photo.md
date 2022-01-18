> JSBox provided a series of APIs to interact with photos

# $photo.take(object)

Take a photo with camera:

```js
$photo.take({
  handler: function(resp) {
    const image = resp.image;
  }
})
```

Param | Type | Description
---|---|---
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
    const image = resp.image;
  }
})
```

All parameters are same as `$photo.take`, they are just have different source type.

Unlike the `take` method, `pick` allows you to choose the return data type:

Param | Type | Description
---|---|---
format | string | "image" or "data", default is "image"

Besides, we can set `multi: true` to pick multiple photos, and `selectionLimit` for maximum number of selections, the result list is like:

Prop | Type | Description
---|---|---
status | bool | success
results | array | all images

The structure of an object in result (when format is `image`):

Prop | Type | Description
---|---|---
image | image | image object
metadata | object | metadata
filename | string | file name

The structure of an object in result (when format is `data`):

Prop | Type | Description
---|---|---
data | data | image file
metadata | object | metadata
filename | string | file name

# $photo.prompt(object)

Ask user take a photo or pick a photo:

```js
$photo.prompt({
  handler: function(resp) {
    const image = resp.image;
  }
})
```

# Get metadata of photo

We can retrieve metadata from a photo:

```js
$photo.pick({
  handler: function(resp) {
    const metadata = resp.metadata;
    if (metadata) {
      const gps = metadata["{GPS}"];
      const url = `https://maps.apple.com/?ll=${gps.Latitude},${gps.Longitude}`;
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
  data,
  handler: function(success) {

  }
})
```

```js
// image
$photo.save({
  image,
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
const png = image.png;
// JPEG
const jpg = image.jpg(0.8);
```

There is a number (0.0 ~ 1.0) means jpeg compress quality.