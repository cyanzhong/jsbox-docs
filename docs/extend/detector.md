> JSBox 自带的文本检测模块，用于方便的提取文本中的特定内容

# $detector

严格的说来，这部分能提供的内容，用原生 JavaScript 的正则表达式同样可以实现，这里只是一个相对简洁的实现方式。

# $detector.date(string)

将文本中所有的日期提取出来：

```js
var dates = $detector.date("2017年10月10日")
```

# $detector.address(string)

将文本中所有的地址提取出来：

```js
var addresses = $detector.address("")
```

# $detector.link(string)

将文本中所有的链接提取出来：

```js
var links = $detector.link("http://apple.com hello http://xteko.com")
```

# $detector.phoneNumber(string)

将文本中所有的电话号码提取出来：

```js
var phoneNumbers = $detector.phoneNumber("18666666666 hello 18777777777")
```