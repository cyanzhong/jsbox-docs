# 键盘上运行的脚本

从 v1.12.0 开始，JSBox 支持让用户通过脚本直接编写一个键盘扩展，你可以通过 JavaScript 来实现对输入区域的操作，可以用于制作辅助输入的插件。

你完全无须关心这个机制是如何实现的，你只需通过 `$keyboard` 相关接口准备好你的脚本。

这里有两个完整的例子用于演示如何构建一个键盘插件：

https://github.com/cyanzhong/xTeko/tree/master/extension-demos/keyboard

[点击这里安装体验](https://xteko.com/redir?url=https://github.com/cyanzhong/xTeko/raw/master/extension-demos/keyboard.box)

https://github.com/cyanzhong/xTeko/tree/master/extension-demos/emoji-key

[点击这里安装体验](https://xteko.com/redir?url=https://github.com/cyanzhong/xTeko/raw/master/extension-demos/emoji-key.box)

# $keyboard.insert(string)

向当前的输入框插入一段文字：

```js
$keyboard.insert("Hey!")
```

# $keyboard.delete()

删除当前选中的内容或者向后删除一个字符：

```js
$keyboard.delete()
```

# $keyboard.moveCursor(number)

移动当前光标（向后移动 5 个位置）：

```js
$keyboard.moveCursor(5)
```

# $keyboard.playInputClick()

播放键盘按下去的音效：

```js
$keyboard.playInputClick()
```

# $keyboard.hasText

判断当前输入区域是否有文字：

```js
var hasText = $keyboard.hasText
```

# $keyboard.selectedText

获取当前选中的文字（iOS 11 以上）：

```js
var selectedText = $keyboard.selectedText
```

# $keyboard.textBeforeInput

输入前的文字：

```js
const textBeforeInput = $keyboard.textBeforeInput;
```

# $keyboard.textAfterInput

输入后的文字：

```js
const textAfterInput = $keyboard.textAfterInput;
```

# $keyboard.getAllText(handler)

获取当前的全部文字（iOS 11 以上）：

```js
$keyboard.getAllText(function(text) {
  
})
```

# $keyboard.next()

切换到下个输入法：

```js
$keyboard.next()
```

# $keyboard.send()

模拟键盘上的发送事件：

```js
$keyboard.send()
```

# $keyboard.dismiss()

将键盘收起来：

```js
$keyboard.dismiss()
```

# $keyboard.barHidden

是否隐藏底部的工具栏，这是一个属性，应该尽早设置。

以上所有的接口，都只能在键盘上面运行，但用户尝试将其运行在别的环境时，会得到运行时错误。

# $keyboard.height

获取和设置键盘的高度：

```js
let height = $keyboard.height;

$keyboard.height = 500;
```