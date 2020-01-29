# Image Processing

JSBox 2.1.0 brings `$imagekit` module for image processing, you can achieve many effects easily:

- Resize
- Rotate
- Grayscale
- Masking
...

In order to make it easier to understand, we created a demo project that uses all APIs: https://github.com/cyanzhong/jsbox-imagekit

# $imagekit.grayscale(image)

Get grayscaled image:

```js
const output = $imagekit.grayscale(source);
```

# $imagekit.invert(image)

Invert colors:

```js
const output = $imagekit.invert(source);
```

# $imagekit.sepia(image)

Apply sepia filter:

```js
const output = $imagekit.sepia(source);
```

# $imagekit.adjustEnhance(image)

Enhance image automatically:

```js
const output = $imagekit.adjustEnhance(source);
```

# $imagekit.adjustRedEye(image)

Red-eye adjustment:

```js
const output = $imagekit.adjustRedEye(source);
```

# $imagekit.adjustBrightness(image, value)

Adjust brightness:

```js
const output = $imagekit.adjustBrightness(source, 100);
// value range: (-255, 255)
```

# $imagekit.adjustContrast(image, value)

Adjust contrast:

```js
const output = $imagekit.adjustContrast(source, 100);
// value range: (-255, 255)
```

# $imagekit.adjustGamma(image, value)

Adjust gamma value:

```js
const output = $imagekit.adjustGamma(source, 4);
// value range: (0.01, 8)
```

# $imagekit.adjustOpacity(image, value)

Adjust opacity:

```js
const output = $imagekit.adjustOpacity(source, 0.5);
// value range: (0, 1)
```

# $imagekit.blur(image, bias)

Apply gaussian blur:

```js
const output = $imagekit.blur(source, 0);
```

# $imagekit.emboss(image, bias)

Emboss effect:

```js
const output = $imagekit.emboss(source, 0);
```

# $imagekit.sharpen(image, bias)

Sharpen:

```js
const output = $imagekit.sharpen(source, 0);
```

# $imagekit.unsharpen(image, bias)

Unsharpen:

```js
const output = $imagekit.unsharpen(source, 0);
```

# $imagekit.detectEdge(source, bias)

Edge detection:

```js
const output = $imagekit.detectEdge(source, 0);
```

# $imagekit.mask(image, mask)

Crop an image with `mask`:

```js
const output = $imagekit.mask(source, mask);
```

# $imagekit.reflect(image, height, fromAlpha, toAlpha)

Create an up-down reflected image, from `height` position, change alpha value from `fromAlpha` to `toAlpha`:

```js
const output = $imagekit.reflect(source, 100, 0, 1);
```

# $imagekit.cropTo(image, size, mode)

Crop an image:

```js
const output = $imagekit.cropTo(source, $size(100, 100), 0);
// mode:
//   - 0: top-left
//   - 1: top-center
//   - 2: top-right
//   - 3: bottom-left
//   - 4: bottom-center
//   - 5: bottom-right
//   - 6: left-center
//   - 7: right-center
//   - 8: center
```

# $imagekit.scaleBy(image, value)

Resize an image with scale:

```js
const output = $imagekit.scaleBy(source, 0.5);
```

# $imagekit.scaleTo(image, size, mode)

Resize an image to a specific size:

```js
const output = $imagekit.scaleTo(source, $size(100, 100), 0);
// mode:
//   - 0: scaleFill
//   - 1: scaleAspectFit
//   - 2: scaleAspectFill
```

# $imagekit.scaleFill(image, size)

Resize an image using `scaleFill` mode:

```js
const output = $imagekit.scaleFill(source, $size(100, 100));
```

# $imagekit.scaleAspectFit(image, size)

Resize an image using `scaleAspectFit` mode:

```js
const output = $imagekit.scaleAspectFit(source, $size(100, 100));
```

# $imagekit.scaleAspectFill(image, size)

Resize an image using `scaleAspectFill` mode:

```js
const output = $imagekit.scaleAspectFill(source, $size(100, 100));
```

# $imagekit.rotate(image, radians)

Rotate an image (it may change the size):

```js
const output = $imagekit.rotate(source, Math.PI * 0.25);
```

# $imagekit.rotatePixels(image, radians)

Rotate an image (keeps the image size, some contents might be clipped):

```js
const output = $imagekit.rotatePixels(source, Math.PI * 0.25);
```

# $imagekit.flip(image, mode)

Flip an image:

```js
const output = $imagekit.flip(source, 0);
// mode:
//   - 0: vertically
//   - 1: horizontally
```

# $imagekit.concatenate(images, space, mode)

Concatenate images with space:

```js
const output = $imagekit.concatenate(images, 10, 0);
// mode:
//   - 0: vertically
//   - 1: horizontally
```

# $imagekit.combine(image, mask)

Add `mask` directly on `image`:

```js
const output = $imagekit.combine(image1, image2);
```

# $imagekit.rounded(image, radius)

Get an image with rounded corners:

```js
const output = $imagekit.rounded(source, 10);
```

# $imagekit.extractGIF(data) -> Promise

Extract GIF data to frames:

```js
const {images, durations} = await $imagekit.extractGIF(data);
// image: all image frames
// durations: duration for each frame
```

# $imagekit.makeGIF(source, options) -> Promise

Make GIF with image array or video data:

```js
const images = [image1, image2];
const data = await $imagekit.makeGIF(images, {
  durations: [0.5, 0.5]
});
```

You can also use `duration` instead of `durations`, it makes the duration of each frame are the same.

# $imagekit.makeVideo(source, options)

Make video with image array or GIF data:

```js
const images = [image1, image2];
const data = await $imagekit.makeVideo(images, {
  durations: [0.5, 0.5]
});
```

You can also use `duration` instead of `durations`, it makes the duration of each frame are the same, GIF data doesn't require durations.