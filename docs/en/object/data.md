# data

`data` means a binary file:

Prop | Type | Read/Write | Description
---|---|---|---
info | object | r | metadata
string | string | r | convert to utf-8 string
byteArray | [number] | r | convert to byte array
image | image | r | convert to image object
fileName | string | r | possible file name
gzipped | $data | r | get gzipped data
gunzipped | $data | r | get gunzipped data
isGzipped | bool | r | check whether is a gzip file