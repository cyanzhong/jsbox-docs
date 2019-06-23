# Method list

Here is a list to show you promise interfaces that supported by JSBox, we are using `required` to indicate the callback must be handled, which means you can use promise directly. And `optional` means the callback can be omitted, as a result you need to set `async: true` to use Promise style.

# $thread

API | Type
---|---
main | required
background | required

# $http

API | Type
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

API | Type
---|---
schedule | optional

# $drive

API | Type
---|---
save | required
open | required

# $cache

API | Type
---|---
setAsync | required
getAsync | required
removeAsync | required
clearAsync | required

# $photo

API | Type
---|---
take | required
pick | required
save | optional
fetch | required
delete | optional

# $input

API | Type
---|---
text | required
speech | required

# $ui

API | Type
---|---
animate | optional
alert | required
action | required
menu | required

# $message

API | Type
---|---
sms | optional
mail | optional

# $calendar

API | Type
---|---
fetch | required
create | optional
save | optional
delete | optional

# $reminder

API | Type
---|---
fetch | required
create | optional
save | optional
delete | optional

# $contact

API | Type
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

API | Type
---|---
select | required

# $ssh

API | Type
---|---
connect | required

# $text

API | Type
---|---
analysis | required
tokenize | required
htmlToMarkdown | required

# $qrcode

API | Type
---|---
scan | required

# $pdf

API | Type
---|---
make | required

# $quicklook

API | Type
---|---
open | optional

# $safari

API | Type
---|---
open | optional

# $archiver

API | Type
---|---
zip | required
unzip | required

# $browser

API | Type
---|---
exec | required

# $picker

API | Type
---|---
date | required
data | required
color | required

# $keyboard

API | Type
---|---
getAllText | required