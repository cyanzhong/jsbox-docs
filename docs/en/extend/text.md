> Provides a lot of utility functions to handle text

# $text.tokenize(object)

Text tokenize:

```js
$text.tokenize({
  text: "我能吞下玻璃而不伤身体",
  handler: function(results) {

  }
})
```

# $text.analysis(object)

// TODO: Text analysis

# $text.lookup(string)

Lookup text in system builtin dictionaries.

```js
$text.lookup("apple")
```

# $text.speech(object)

Text to speech (TTS):

```js
$text.speech({
  text: "Hello, World!",
  rate: 0.5,
  language: "en-US", // optional
})
```

You can stop/pause/continue a speaker by:

```js
var speaker = $text.speech({})
speaker.pause()
speaker.continue()
speaker.stop()
```

Events for state changes:

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

Supported languages:

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

# $text.ttsVoices

Returns supported voices, you can use one of them to specify the voice in $text.speech:

```js
const voices = $text.ttsVoices;
console.log(voices);

$text.speech({
  text: "Hello, World!",
  voice: voices[0]
});
```

Voice Object:

Prop | Type | Read/Write | Description
---|---|---|---
language | string | r | language
identifier | string | r | identifier
name | string | r | name
quality | number | r | quality
gender | number | r | gender
audioFileSettings | object | r | audio file settings

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

Get Chinese PinYin of a string.

# $text.markdownToHtml(text)

Convert Markdown text to HTML text.

# $text.htmlToMarkdown(object)

Convert HTML text to Markdown text, this is an async func:

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

Convert data to a string:

```js
var string = $text.decodeData({
  data: file,
  encoding: 4 // default, refer: https://developer.apple.com/documentation/foundation/nsstringencoding
})
```

# $text.sizeThatFits(object)

Calculate text bounding size dynamically:

```js
var size = $text.sizeThatFits({
  text: "Hello, World",
  width: 320,
  font: $font(20),
  lineSpacing: 15, // Optional
})
```