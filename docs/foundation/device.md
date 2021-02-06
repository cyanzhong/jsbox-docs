> 在这里可以获取和设备有关的一些信息，例如设备语言、设备型号等等。

# $device.info

返回设备的基本信息，例如：

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
  },
  "battery": {
    "state": 1, // 0: unknown 1: normal 2: charging 3: charging & fully charged
    "level": 0.9399999976158142
  }
}
```

# $device.ssid

获取当前 Wi-Fi 的 SSID 信息：

```js
const ssid = $device.ssid;
```

返回数据样例：

```json
{
  "SSIDDATA": {},
  "BSSID": "aa:bb:cc:dd:ee:ff",
  "SSID": "SSID"
}
```

注：在 iOS 13 上，使用此接口需要应用具备地理位置权限，你可以通过 `$location` 相关接口获得权限。

# $device.networkType

获取当前设备的网络类型：

```js
const networkType = $device.networkType;
```

数值 | 说明
---|---
0 | 无网络
1 | Wi-Fi
2 | 蜂窝数据

# $device.space

获取设备的内存/磁盘空间：

```js
const space = $device.space;
```

返回数据样例：

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

在有 Taptic Engine 的设备上触发一个轻微的振动，例如：

```js
$device.taptic(0)
```

参数 | 类型 | 说明
---|---|---
level | number | 0 ~ 2 表示振动等级

# $device.wlanAddress

获得局域网 IP 地址：

```js
const address = $device.wlanAddress;
```

# $device.isDarkMode

检查设备是否处于 Dark Mode 状态：

```js
if ($device.isDarkMode) {
  
}
```

# $device.isXXX

快速检查设备屏幕类型：

```js
const isIphoneX = $device.isIphoneX;
const isIphonePlus = $device.isIphonePlus;
const isIpad = $device.isIpad;
const isIpadPro = $device.isIpadPro;
```

# $device.hasTouchID

检查是否支持 Touch ID:

```js
const hasTouchID = $device.hasTouchID;
```

# $device.hasFaceID

检查是否支持 Face ID:

```js
const hasFaceID = $device.hasFaceID;
```

# $device.isJailbroken

检查设备是否越狱：

```js
const isJailbroken = $device.isJailbroken;
```

# $device.isVoiceOverOn

检查是否在使用 VoiceOver:

```js
const isVoiceOverOn = $device.isVoiceOverOn;
```