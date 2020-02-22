# data

`data` 类型表示一个二进制数据，亦即一个文件。

属性 | 类型 | 读写 | 说明
---|---|---|---
info | object | 只读 | metadata
string | string | 只读 | 转换成 UTF8 字符串
byteArray | [number] | 只读 | 转换成 byte array
image | image | 只读 | 转换成 image
fileName | string | 只读 | 可能的文件名
gzipped | $data | 只读 | 获取 gzip 后的文件
gunzipped | $data | 只读 | 获取 gunzip 后的文件
isGzipped | bool | 只读 | 检测是否是一个 gzip 文件