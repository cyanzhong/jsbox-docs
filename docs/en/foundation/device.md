> Retrieve some useful information of the device, such as language, device model etc

# $device.info

Returns the basic info of device:

```js
{
  "model": "string",
  "language": "string",
  "version": "string",
  "name": "cyan's iPhone",
  "screen": {
    "width": 240,
    "height": 320,
    "scale": 2.0,
    "orientation": 1,
  }
}
```

# $device.ssid

Get the SSID of current Wi-Fi:

```js
var ssid = $device.ssid
```

Example:

```json
{
  "SSIDDATA": {},
  "BSSID": "aa:bb:cc:dd:ee:ff",
  "SSID": "SSID"
}
```

Note: In iOS 13 and above, this API needs location access, you can use `$location` APIs to request the access.

# $device.networkType

Returns the network type:

```js
var networkType = $device.networkType
```

Value | Type
---|---
0 | None
1 | Wi-Fi
2 | Cellular

# $device.space

Returns memory usage and disk usage of the device:

```js
var space = $device.space
```

Example:

```json
{
  "disk": {
    "free": {
      "bytes": 87409733632,
      "string": "87.41 GB"
    },
    "total": {
      "bytes": 127989493760,
      "string": "127.99 GB"
    }
  },
  "memory": {
    "free": {
      "bytes": 217907200,
      "string": "207.8 MB"
    },
    "total": {
      "bytes": 3221225472,
      "string": "3 GB"
    }
  }
}
```

# $device.taptic(number)

Generate a Taptic Engine Feedback:

```js
$device.taptic(0)
```

Param | Type | Description
---|---|---
level | number | 0 ~ 2

# $device.wlanAddress

Get WLAN address:

```js
var address = $device.wlanAddress
```

# $device.isDarkMode

Check whether device is dark mode:

```js
if ($device.isDarkMode) {
  
}
```

# $device.isXXX

Check screen type quickly:

```js
var isIphoneX = $device.isIphoneX;
var isIphonePlus = $device.isIphonePlus;
var isIpad = $device.isIpad;
var isIpadPro = $device.isIpadPro;
```

# $device.hasTouchID

Check whether Touch ID is supported:

```js
const hasTouchID = $device.hasTouchID;
```

# $device.hasFaceID

Check whether Face ID is supported:

```js
const hasFaceID = $device.hasFaceID;
```

# $device.isJailbroken

Check whether device is jailbroken:

```js
const isJailbroken = $device.isJailbroken;
```

# $device.isVoiceOverOn

Check whether VoiceOver is running:

```js
const isVoiceOverOn = $device.isVoiceOverOn;
```