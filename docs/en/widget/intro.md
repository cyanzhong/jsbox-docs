# JSBox script on widget

The memory and user interaction are very limited on iOS today widget.

Therefore, not all scripts can be executed on widget correctly.

Here is a list for unavailable APIs:

API | Description
---|---
$ui.action | Present action sheet
$ui.preview | Preview content
$message.* | Send message
$photo.take | Take photo
$photo.pick | Pick photo
$photo.prompt | Ask user to get a photo
$share.sheet | Present share sheet
$text.lookup | Lookup in dictionary
$pick.* | Present pickers
$qrcode.scan | Scan QRCode
$input.speech | Speech to text

Please be careful when you are using above APIs.

When you want to get input from user, please use `$input.text` instead of `input` component.

# Some APIs are very useful on widget

Although there are some limitations, we still need to interact with users.

Here are some useful APIs you could consider:

API | Description
---|---
$ui.alert | Present alert
$ui.menu | Show popup menu
$ui.toast | Show toast message
$ui.loading | Show loading state
$input.text | Input text