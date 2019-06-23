# type: "lottie"

`lottie` creates a [Lottie](http://airbnb.io/lottie/) view:

```js
{
  type: "lottie",
  props: {
    src: "assets/lottie-btn.json",
  },
  layout: (make, view) => {
    make.size.equalTo($size(100, 100));
    make.center.equalTo(view.super);
  }
}
```

`src` could be a bundle path, or a http url. Also, you can load lottie with `json` or `data`:

```js
// JSON
$("lottie").json = {};
// Data
$("lottie").data = $file.read("assets/lottie-btn.json");
```

# lottie.play(args?)

Play the animation:

```js
$("lottie").play();
```

Register completion callback:

```js
$("lottie").play({
  handler: finished => {

  }
});
```

Specify from frame and to frame:

```js
$("lottie").play({
  fromFrame: 0, // Optional
  toFrame: 0,
  handler: finished => {
    // Optional
  }
});
```

Specify from progress and to progress:

```js
$("lottie").play({
  fromProgress: 0, // Optional
  toProgress: 0.5,
  handler: finished => {
    // Optional
  }
});
```

Work with promise:

```js
let finished = await $("lottie").play({ toProgress: 0.5, async: true });
```

# lottie.pause()

Pause the animation:

```js
$("lottie").pause();
```

# lottie.stop()

Stop the animation:

```js
$("lottie").stop();
```

# lottie.update()

Force update current frame:

```js
$("lottie").update();
```

# lottie.progressForFrame(frame)

Convert frame to progress:

```js
let progress = $("lottie").progressForFrame(0);
```

# lottie.frameForProgress(progress)

Convert progress to frame:

```js
let frame = $("lottie").frameForProgress(0.5);
```

# props

Prop | Type | Read/Write | Description
---|---|---|---
json | json | w | load with json
data | $data | w | load with data
src | string | w | load with src
playing | bool | r | is playing
loop | bool | rw | is loop animation
autoReverse | bool | rw | is auto-reverse animation
progress | number | rw | animation progress
frameIndex | number | rw | current frame
speed | number | rw | animation speed
duration | number | r | animation duration

Learn more from here: https://github.com/cyanzhong/xTeko/tree/master/extension-demos/lottie-example