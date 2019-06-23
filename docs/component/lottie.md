# type: "lottie"

`lottie` 用于创建一个 [Lottie](http://airbnb.io/lottie/) 控件：

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

`src` 可以是 bundle 内的路径，也可以是一个 http 地址，同时，你还可以通过 `json` 或 `data` 来加载 Lottie：

```js
// JSON
$("lottie").json = {};
// Data
$("lottie").data = $file.read("assets/lottie-btn.json");
```

# lottie.play(args?)

播放动画：

```js
$("lottie").play();
```

注册回调消息：

```js
$("lottie").play({
  handler: finished => {

  }
});
```

控制起始结束帧数：

```js
$("lottie").play({
  fromFrame: 0, // Optional
  toFrame: 0,
  handler: finished => {
    // Optional
  }
});
```

控制起始结束进度：

```js
$("lottie").play({
  fromProgress: 0, // Optional
  toProgress: 0.5,
  handler: finished => {
    // Optional
  }
});
```

使用 Promise：

```js
let finished = await $("lottie").play({ toProgress: 0.5, async: true });
```

# lottie.pause()

暂停动画：

```js
$("lottie").pause();
```

# lottie.stop()

停止动画：

```js
$("lottie").stop();
```

# lottie.update()

强制重画当前帧：

```js
$("lottie").update();
```

# lottie.progressForFrame(frame)

获得帧对应的进度：

```js
let progress = $("lottie").progressForFrame(0);
```

# lottie.frameForProgress(progress)

获得进度对应的帧：

```js
let frame = $("lottie").frameForProgress(0.5);
```

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
json | json | 只写 | 使用 json 加载 Lottie
data | $data | 只写 | 使用 data 加载 Lottie
src | string | 只写 | 使用路径或网址加载 Lottie
playing | bool | 只读 | 是否正在播放
loop | bool | 读写 | 是否循环播放
autoReverse | bool | 读写 | 是否自动反转
progress | number | 读写 | 播放进度
frameIndex | number | 读写 | 播放帧数
speed | number | 读写 | 播放速度
duration | number | 只读 | 动画时长

请参考这个项目来了解更多：https://github.com/cyanzhong/xTeko/tree/master/extension-demos/lottie-example