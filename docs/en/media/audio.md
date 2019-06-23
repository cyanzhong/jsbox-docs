> JSBox can play simple audio, for example a keyboard clicked sound

# $audio.play(object)

Use sound id:

```js
// Use sound id
$audio.play({
  id: 1000
})
```

Refer https://github.com/TUNER88/iOSSystemSoundsLibrary to learn more about system sounds.

```js
// Play remote audio
$audio.play({
  url: "https://"
})
```

```js
// Play local audio
$audio.play({
  path: "audio.wav"
})
```

```js
// Pause audio track
$audio.pause()
```

```js
// Resume audio track
$audio.resume()
```

```js
// Stop audio track
$audio.stop()
```

```js
// Seek to a position (in seconds)
$audio.seek(60)
```

```js
// Get current status
var status = $audio.status
// 0: paused, 1: waiting, 2: playing
```

```js
// Get duration
var duration = $audio.duration
```

```js
// Get current time
var offset = $audio.offset
```

# Events

You can observe some events during play an audio track:

```js
$audio.play({
  events: {
    itemEnded: function() {},
    timeJumped: function() {},
    didPlayToEndTime: function() {},
    failedToPlayToEndTime: function() {},
    playbackStalled: function() {},
    newAccessLogEntry: function() {},
    newErrorLogEntry: function() {},
  }
})
```

Refer: https://developer.apple.com/documentation/avfoundation/avplayeritem?language=objc