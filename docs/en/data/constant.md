# Constant Table

Here are some constants provided by JSBox, you can use it easily in your scripts.

For example `$align.left` is actually `0`, but it's no way to remember that, so we need constants.

# $env

JSBox environment:

```js
var $env = {
  app: 1 << 0,
  today: 1 << 1,
  action: 1 << 2,
  safari: 1 << 3,
  notification: 1 << 4,
  keyboard: 1 << 5,
  siri: 1 << 6,
  all: (1 << 0) | (1 << 1) | (1 << 2) | (1 << 3) | (1 << 4) | (1 << 5) | (1 << 6)
}
```

# $align

iOS text alignment type:

```js
var $align = {
  left: 0,
  center: 1,
  right: 2,
  justified: 3,
  natural: 4
}
```

# $contentMode

iOS view content mode:

```js
var $contentMode = {
  scaleToFill: 0,
  scaleAspectFit: 1,
  scaleAspectFill: 2,
  redraw: 3,
  center: 4,
  top: 5,
  bottom: 6,
  left: 7,
  right: 8,
}
```

# $btnType

iOS button type:

```js
var $btnType = {
  custom: 0,
  system: 1,
  disclosure: 2,
  infoLight: 3,
  infoDark: 4,
  contactAdd: 5,
}
```

# $alertActionType

Alert item style:

```js
var $alertActionType = {
  default: 0, cancel: 1, destructive: 2
}
```

# $zero

Zero values:

```js
var $zero = {
  point: $point(0, 0),
  size: $size(0, 0),
  rect: $rect(0, 0, 0, 0),
  insets: $insets(0, 0, 0, 0)
}
```

# $layout

Common layout functions:

```js
var $layout = {
  fill: function(make, view) {
    make.edges.equalTo(view.super)
  },
  fillSafeArea: function(make, view) {
    make.edges.equalTo(view.super.safeArea)
  },
  center: function(make, view) {
    make.center.equalTo(view.super)
  }
}
```

# $lineCap

iOS line cap:

```js
var $lineCap = {
  butt: 0,
  round: 1,
  square: 2
}
```

# $lineJoin

iOS line join:

```js
var $lineJoin = {
  miter: 0,
  round: 1,
  bevel: 2
}
```

# $mediaType

[UTI Types](https://developer.apple.com/library/content/documentation/Miscellaneous/Reference/UTIRef/Introduction/Introduction.html):

```js
var $mediaType = {
  image: "public.image",
  jpeg: "public.jpeg",
  jpeg2000: "public.jpeg-2000",
  tiff: "public.tiff",
  pict: "com.apple.pict",
  gif: "com.compuserve.gif",
  png: "public.png",
  icns: "com.apple.icns",
  bmp: "com.microsoft.bmp",
  ico: "com.microsoft.ico",
  raw: "public.camera-raw-image",
  live: "com.apple.live-photo",
  movie: "public.movie",
  video: "public.video",
  audio: "public.audio",
  mov: "com.apple.quicktime-movie",
  mpeg: "public.mpeg",
  mpeg2: "public.mpeg-2-video",
  mp3: "public.mp3",
  mp4: "public.mpeg-4",
  avi: "public.avi",
  wav: "com.microsoft.waveform-audio",
  midi: "public.midi-audio"
}
```

# $imgPicker

iOS image picker constants:

```js
var $imgPicker = {
  quality: {
    high: 0,
    medium: 1,
    low: 2,
    r640x480: 3,
    r1280x720: 4,
    r960x540: 5
  },
  captureMode: {
    photo: 0,
    video: 1
  },
  device: {
    rear: 0,
    front: 1
  },
  flashMode: {
    off: -1,
    auto: 0,
    on: 1
  }
}
```

# $kbType

iOS keyboard types:

```js
var $kbType =  {
  default: 0,
  ascii: 1,
  nap: 2,
  url: 3,
  number: 4,
  phone: 5,
  namePhone: 6,
  email: 7,
  decimal: 8,
  twitter: 9,
  search: 10,
  asciiPhone: 11
}
```

# $assetMedia

iOS asset media constants:

```js
var $assetMedia = {
  type: {
    unknown: 0,
    image: 1,
    video: 2,
    audio: 3
  },
  subType: {
    none: 0,
    panorama: 1 << 0,
    hdr: 1 << 1,
    screenshot: 1 << 2,
    live: 1 << 3,
    depthEffect: 1 << 4,
    streamed: 1 << 16,
    highFrameRate: 1 << 17,
    timelapse: 1 << 18
  }
}
```

# $pageSize

$pdf page sizes:

```js
var $pageSize = {
  letter: 0, governmentLetter: 1, legal: 2, juniorLegal: 3, ledger: 4, tabloid: 5,
  A0: 6, A1: 7, A2: 8, A3: 9, A4: 10, A5: 11, A6: 12, A7: 13, A8: 14, A9: 15, A10: 16,
  B0: 17, B1: 18, B2: 19, B3: 20, B4: 21, B5: 22, B6: 23, B7: 24, B8: 25, B9: 26, B10: 27,
  C0: 28, C1: 29, C2: 30, C3: 31, C4: 32, C5: 33, C6: 34, C7: 35, C8: 36, C9: 37, C10: 38,
  custom: 52
}
```

# $UIEvent

Event types which are used in `addEventHandler` function:

```js
var $UIEvent = {
  touchDown: 1 << 0,
  touchDownRepeat: 1 << 1,
  touchDragInside: 1 << 2,
  touchDragOutside: 1 << 3,
  touchDragEnter: 1 << 4,
  touchDragExit: 1 << 5,
  touchUpInside: 1 << 6,
  touchUpOutside: 1 << 7,
  touchCancel: 1 << 8,
  valueChanged: 1 << 12,
  primaryActionTriggered: 1 << 13,
  editingDidBegin: 1 << 16,
  editingChanged: 1 << 17,
  editingDidEnd: 1 << 18,
  editingDidEndOnExit: 1 << 19,
  allTouchEvents: 0x00000FFF,
  allEditingEvents: 0x000F0000,
  applicationReserved: 0x0F000000,
  systemReserved: 0xF0000000,
  allEvents: 0xFFFFFFFF,
}
```

# $stackViewAxis

Axis values for stack view:

```js
var $stackViewAxis = {
  horizontal: 0,
  vertical: 1,
}
```

# $stackViewDistribution

Distribution values for stack view:

```js
var $stackViewDistribution = {
  fill: 0,
  fillEqually: 1,
  fillProportionally: 2,
  equalSpacing: 3,
  equalCentering: 4,
}
```

# $stackViewAlignment

Alignment values for stack view:

```js
var $stackViewAlignment = {
  fill: 0,
  leading: 1,
  top: 1,
  firstBaseline: 2,
  center: 3,
  trailing: 4,
  bottom: 4,
  lastBaseline: 5,
}
```

# $stackViewSpacing

Spacing values for stack view:

```js
var $stackViewSpacing = {
  useDefault: UIStackViewSpacingUseDefault,
  useSystem: UIStackViewSpacingUseSystem,
}
```

# $popoverDirection

Popover arrow directions for `$ui.popover(...)` method:

```js
var $popoverDirection = {
  up: 1 << 0,
  down: 1 << 1,
  left: 1 << 2,
  right: 1 << 3,
  any: (1 << 0) | (1 << 1) | (1 << 2) | (1 << 3),
}
```

# $scrollDirection

Scroll directions for `matrix` views:

```js
var $scrollDirection = {
  vertical: 0,
  horizontal: 1,
}
```

# $blurStyle

Style constants for `blur` views:

```js
var $blurStyle = {
  // Additional Styles
  extraLight: 0,
  light: 1,
  dark: 2,
  extraDark: 3,
  regular: 4,
  prominent: 5,
  // Adaptable Styles (iOS 13)
  ultraThinMaterial: 6,
  thinMaterial: 7,
  material: 8,
  thickMaterial: 9,
  chromeMaterial: 10,
  // Light Styles (iOS 13)
  ultraThinMaterialLight: 11,
  thinMaterialLight: 12,
  materialLight: 13,
  thickMaterialLight: 14,
  chromeMaterialLight: 15,
  // Dark Styles (iOS 13)
  ultraThinMaterialDark: 16,
  thinMaterialDark: 17,
  materialDark: 18,
  thickMaterialDark: 19,
  chromeMaterialDark: 20,
}
```

Please refer to Apple's documentation for details: https://developer.apple.com/documentation/uikit/uiblureffectstyle