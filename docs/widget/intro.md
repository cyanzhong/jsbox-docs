# 运行在 Widget 上的扩展

由于 Widget 的交互限制，并不是所有的扩展都可以运行在 Widget 之上，以下是不支持运行在 Widget 的 API 黑名单：

API | 说明
---|---
$ui.action | 弹出 action sheet
$ui.preview | 预览文件或网页
$message.* | 消息相关接口
$photo.take | 拍照
$photo.pick | 选取图片
$photo.prompt | 询问用户获得图片
$share.sheet | 弹出 share sheet
$text.lookup | 查询词典
$pick.* | 选择器
$qrcode.scan | 扫描二维码
$input.speech | 语音识别

当扩展中包含上述接口时，在通知中心运行可能会出现问题。

当你需要进行文字输入时，请尽可能使用 `$input.text` 接口，而不是通过 input 控件。

# Widget 上支持的交互

尽管 Widget 上支持的交互很有限，但对于 `$ui` 还是有少量的接口可以用于提示用户：

API | 说明
---|---
$ui.alert | 弹出 alert
$ui.menu | 弹出菜单
$ui.toast | 显示消息
$ui.loading | 显示加载状态
$input.text | 输入文字