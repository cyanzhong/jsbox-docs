> 提供了大量的用于文字处理的接口

# $text.tokenize(object)

对文本进行分词处理：

```js
$text.tokenize({
  text: "我能吞下玻璃而不伤身体",
  handler: function(results) {

  }
})
```

# $text.analysis(object)

// TODO: 对文本进行自然语言分析

# $text.lookup(string)

在系统内置词典中查找文本：

```js
$text.lookup("apple")
```

# $text.speech(object)

文本转成语音：

```js
$text.speech({
  text: "Hello, World!",
  rate: 0.5,
  language: "zh-CN", // optional
})
```

你可以将此过程暂停/继续或停止：

```js
var speaker = $text.speech({})
speaker.pause()
speaker.continue()
speaker.stop()
```

可以通过 `events` 来获取状态：

```js
$text.speech({
  text: "Hello, World!",
  events: {
    didStart: (sender) => {},
    didFinish: (sender) => {},
    didPause: (sender) => {},
    didContinue: (sender) => {},
    didCancel: (sender) => {},
  }
})
```

支持语言列表：

```
ar-SA
cs-CZ
da-DK
de-DE
el-GR
en-AU
en-GB
en-IE
en-US
en-US
en-ZA
es-ES
es-MX
fi-FI
fr-CA
fr-FR
he-IL
hi-IN
hu-HU
id-ID
it-IT
ja-JP
ko-KR
nl-BE
nl-NL
no-NO
pl-PL
pt-BR
pt-PT
ro-RO
ru-RU
sk-SK
sv-SE
th-TH
tr-TR
zh-CN
zh-HK
zh-TW
```

# $text.base64Encode(string)

Base64 encode.

# $text.base64Decode(string)

Base64 decode.

# $text.URLEncode(string)

URL encode.

# $text.URLDecode(string)

URL decode.

# $text.HTMLEscape(string)

HTML escape.

# $text.HTMLUnescape(string)

HTML unescape.

# $text.MD5(string)

MD5.

# $text.SHA1(string)

SHA1.

# $text.SHA256(string)

SHA256.

# $text.convertToPinYin(text)

将文字转换成汉语拼音。

# $text.markdownToHtml(text)

将 Markdown 文本转换成 HTML 文本。

# $text.htmlToMarkdown(object)

将 HTML 文本转换成 Markdown 文本，这是一个异步接口：

```js
$text.htmlToMarkdown({
  html: "<p>Hey</p>",
  handler: markdown => {

  }
})

// Or
var markdown = await $text.htmlToMarkdown("<p>Hey</p>");
```

# $text.decodeData(object)

将 data 转换成字符串：

```js
var string = $text.decodeData({
  data: file,
  encoding: 4 // default, refer: https://developer.apple.com/documentation/foundation/nsstringencoding
})
```

# $text.sizeThatFits(object)

动态计算文字的高度：

```js
var size = $text.sizeThatFits({
  text: "Hello, World",
  width: 320,
  font: $font(20),
  lineSpacing: 15, // Optional
})
```