# 接口列表

这里是一个表格，用于列举我们在前面文章中提到过的 Promise 接口问题，我们用 `required` 表示这是一个必须要回调的接口，也即你可以直接使用 Promise，用 `optional` 来表示该接口的回调可以省略，当你需要 Promise 调用的时候，需要 `async: true` 参数来指明。

# $thread

接口 | 类型
---|---
main | required
background | required

# $http

接口 | 类型
---|---
request | required
get | required
post | required
download | required
upload | required
shorten | required
lengthen | required
startServer | required

# $push

接口 | 类型
---|---
schedule | optional

# $drive

接口 | 类型
---|---
save | required
open | required

# $cache

接口 | 类型
---|---
setAsync | required
getAsync | required
removeAsync | required
clearAsync | required

# $photo

接口 | 类型
---|---
take | required
pick | required
save | optional
fetch | required
delete | optional

# $input

接口 | 类型
---|---
text | required
speech | required

# $ui

接口 | 类型
---|---
animate | optional
alert | required
action | required
menu | required

# $message

接口 | 类型
---|---
sms | optional
mail | optional

# $calendar

接口 | 类型
---|---
fetch | required
create | optional
save | optional
delete | optional

# $reminder

接口 | 类型
---|---
fetch | required
create | optional
save | optional
delete | optional

# $contact

接口 | 类型
---|---
pick | required
fetch | required
create | optional
save | optional
delete | optional
fetchGroups | required
addGroup | optional
deleteGroup | optional
updateGroup | optional
addToGroup | optional
removeFromGroup | optional

# $location

接口 | 类型
---|---
select | required

# $ssh

接口 | 类型
---|---
connect | required

# $text

接口 | 类型
---|---
analysis | required
tokenize | required
htmlToMarkdown | required

# $qrcode

接口 | 类型
---|---
scan | required

# $pdf

接口 | 类型
---|---
make | required

# $quicklook

接口 | 类型
---|---
open | optional

# $safari

接口 | 类型
---|---
open | optional

# $archiver

接口 | 类型
---|---
zip | required
unzip | required

# $browser

接口 | 类型
---|---
exec | required

# $picker

接口 | 类型
---|---
date | required
data | required
color | required

# $keyboard

接口 | 类型
---|---
getAllText | required