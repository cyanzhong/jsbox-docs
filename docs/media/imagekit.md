# 图像处理

JSBox 2.1.0 增加了图像处理模块 `$imagekit`，通过这个模块你可以很轻松的处理图像，例如：

- 调整大小
- 旋转
- 制作灰度图像
- 图像叠加
...

为了更直观的介绍，我们构建了一个使用了所有接口的样例项目：https://github.com/cyanzhong/jsbox-imagekit

# $imagekit.render(options, handler)

创建一张图片，并可以使用 canvas 进行绘制：

```js
const options = {
  size: $size(100, 100),
  color: $color("#00FF00"),
  // scale: default to screen scale
  // opaque: default to false
}

const image = $imagekit.render(options, ctx => {
  const centerX = 50;
  const centerY = 50;
  const radius = 25;
  ctx.fillColor = $color("#FF0000");
  ctx.moveToPoint(centerX, centerY - radius);
  for (let i = 1; i < 5; ++i) {
    const x = radius * Math.sin(i * Math.PI * 0.8);
    const y = radius * Math.cos(i * Math.PI * 0.8);
    ctx.addLineToPoint(x + centerX, centerY - y);
  }
  ctx.fillPath();
});
```

`ctx` 与 `canvas` 组件中的一样，请参考 [canvas](component/canvas.md) 文档。

# $imagekit.info(image)

获取图片信息：

```js
const info = $imagekit.info(source);
// width, height, orientation, scale, props
```

# $imagekit.grayscale(image)

转换成灰度图像：

```js
const output = $imagekit.grayscale(source);
```

# $imagekit.invert(image)

将图像反色：

```js
const output = $imagekit.invert(source);
```

# $imagekit.sepia(image)

添加棕褐色滤镜：

```js
const output = $imagekit.sepia(source);
```

# $imagekit.adjustEnhance(image)

自动改善图像效果：

```js
const output = $imagekit.adjustEnhance(source);
```

# $imagekit.adjustRedEye(image)

自动红眼消除：

```js
const output = $imagekit.adjustRedEye(source);
```

# $imagekit.adjustBrightness(image, value)

调整图片亮度：

```js
const output = $imagekit.adjustBrightness(source, 100);
// value range: (-255, 255)
```

# $imagekit.adjustContrast(image, value)

调整图片对比度：

```js
const output = $imagekit.adjustContrast(source, 100);
// value range: (-255, 255)
```

# $imagekit.adjustGamma(image, value)

调整图片伽马值：

```js
const output = $imagekit.adjustGamma(source, 4);
// value range: (0.01, 8)
```

# $imagekit.adjustOpacity(image, value)

调整图片不透明度：

```js
const output = $imagekit.adjustOpacity(source, 0.5);
// value range: (0, 1)
```

# $imagekit.blur(image, bias)

高斯模糊效果：

```js
const output = $imagekit.blur(source, 0);
```

# $imagekit.emboss(image, bias)

浮雕效果：

```js
const output = $imagekit.emboss(source, 0);
```

# $imagekit.sharpen(image, bias)

锐化：

```js
const output = $imagekit.sharpen(source, 0);
```

# $imagekit.unsharpen(image, bias)

钝化:

```js
const output = $imagekit.unsharpen(source, 0);
```

# $imagekit.detectEdge(source, bias)

边缘检测：

```js
const output = $imagekit.detectEdge(source, 0);
```

# $imagekit.mask(image, mask)

使用 `mask` 作为蒙版进行切图：

```js
const output = $imagekit.mask(source, mask);
```

# $imagekit.reflect(image, height, fromAlpha, toAlpha)

创建上下镜像的图片，从 `height` 处折叠，透明度从 `fromAlpha` 变化到 `toAlpha`：

```js
const output = $imagekit.reflect(source, 100, 0, 1);
```

# $imagekit.cropTo(image, size, mode)

图片裁剪：

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

使用比例调整图片大小：

```js
const output = $imagekit.scaleBy(source, 0.5);
```

# $imagekit.scaleTo(image, size, mode)

使用 size 调整图片大小：

```js
const output = $imagekit.scaleTo(source, $size(100, 100), 0);
// mode:
//   - 0: scaleFill
//   - 1: scaleAspectFit
//   - 2: scaleAspectFill
```

# $imagekit.scaleFill(image, size)

使用 `scaleFill` 模式调整大小：

```js
const output = $imagekit.scaleFill(source, $size(100, 100));
```

# $imagekit.scaleAspectFit(image, size)

使用 `scaleAspectFit` 模式调整大小：

```js
const output = $imagekit.scaleAspectFit(source, $size(100, 100));
```

# $imagekit.scaleAspectFill(image, size)

使用 `scaleAspectFill` 模式调整大小：

```js
const output = $imagekit.scaleAspectFill(source, $size(100, 100));
```

# $imagekit.rotate(image, radians)

旋转图片（将会调整图像大小）：

```js
const output = $imagekit.rotate(source, Math.PI * 0.25);
```

# $imagekit.rotatePixels(image, radians)

旋转图片（不会改变图像大小，可能会裁剪）：

```js
const output = $imagekit.rotatePixels(source, Math.PI * 0.25);
```

# $imagekit.flip(image, mode)

获得镜像图片：

```js
const output = $imagekit.flip(source, 0);
// mode:
//   - 0: vertically
//   - 1: horizontally
```

# $imagekit.concatenate(images, space, mode)

拼接多张图片，可以添加间距：

```js
const output = $imagekit.concatenate(images, 10, 0);
// mode:
//   - 0: vertically
//   - 1: horizontally
```

# $imagekit.combine(image, mask, mode)

将两个图片叠加：

```js
const output = $imagekit.combine(image1, image2, mode);
// mode:
//   - 0: top-left
//   - 1: top-center
//   - 2: top-right
//   - 3: bottom-left
//   - 4: bottom-center
//   - 5: bottom-right
//   - 6: left-center
//   - 7: right-center
//   - 8: center (default)
//   - $point(x, y): absolute position
```

# $imagekit.rounded(image, radius)

获取圆角图片：

```js
const output = $imagekit.rounded(source, 10);
```

# $imagekit.circular(image)

获取正圆形图片，如果原图不是正方形则会居中并从来裁剪：

```js
const output = $imagekit.circular(source);
```

# $imagekit.extractGIF(data) -> Promise

将 GIF 文件分解成单帧：

```js
const {images, durations} = await $imagekit.extractGIF(data);
// image: all image frames
// durations: duration for each frame
```

# $imagekit.makeGIF(source, options) -> Promise

将 image 数组或视频文件 data 合成为 GIF 文件：

```js
const images = [image1, image2];
const options = {
  durations: [0.5, 0.5],
  // size: 16, 12, 8, 4, 2
}
const data = await $imagekit.makeGIF(images, options);
```

若使用 `duration` 替代 `durations`，则每张图片时长一致。

# $imagekit.makeVideo(source, options) -> Promise

将 image 数组或 GIF 文件合成为视频文件：

```js
const images = [image1, image2];
const data = await $imagekit.makeVideo(images, {
  durations: [0.5, 0.5]
});
```

若使用 `duration` 替代 `durations`，则每张图片时长一致，使用 GIF 时不需要指定时长。