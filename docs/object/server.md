# request

属性 | 类型 | 读写 | 说明
---|---|---|---
method | string | 只读 | http method
url | string | 只读 | url
headers | json | 只读 | http headers
path | string | 只读 | path
query | json | 只读 | query
contentType | string | 只读 | Content-Type
contentLength | number | 只读 | Content-Length
ifModifiedSince | date | 只读 | If-Modified-Since
ifNoneMatch | bool | 只读 | If-None-Match
acceptsGzip | bool | 只读 | accepts Gzip encoding
localAddressData | data | 只读 | local address data
localAddress | string | 只读 | local address string
remoteAddressData | data | 只读 | remote address data
remoteAddress | string | 只读 | remote address string
hasBody | bool | 只读 | has body
hasByteRange | bool | 只读 | has byte range

# data request

data request 包含所有 request 的属性，同时有如下属性：

属性 | 类型 | 读写 | 说明
---|---|---|---
data | data | 只读 | data
text | string | 只读 | text
json | json | 只读 | json

# file request

file request 包含所有 request 的属性，同时有如下属性：

属性 | 类型 | 读写 | 说明
---|---|---|---
temporaryPath | string | 只读 | temporary file path

# multipart request

multipart request 包含所有 request 的属性，同时有如下属性：

属性 | 类型 | 读写 | 说明
---|---|---|---
arguments | array | 只读 | arguments
files | array | 只读 | files
mimeType | string | 只读 | MIME Type

arguments 包含的数据结构：

属性 | 类型 | 读写 | 说明
---|---|---|---
controlName | string | 只读 | control name
contentType | string | 只读 | Content-Type
mimeType | string | 只读 | MIME Type
data | data | 只读 | data
string | string | 只读 | string
fileName | string | 只读 | file name
temporaryPath | string | 只读 | temporary file path

# response

response 是 handler.response 返回的对象：

属性 | 类型 | 读写 | 说明
---|---|---|---
redirect | string | 读写 | redirect url
permanent | bool | 读写 | permanent
statusCode | number | 读写 | http status code
contentType | string | 读写 | Content-Type
contentLength | string | 读写 | Content-Length
cacheControlMaxAge | number | 读写 | Cache-Control
lastModifiedDate | date | 读写 | Last-Modified
eTag | string | 读写 | ETag
gzipEnabled | bool | 读写 | gzip enabled
hasBody | bool | 读写 | has body

例如你能这样构造一个 response：

```js
return {
  type: "default",
  props: {
    statusCode: 404
  }
}
```

# data response

data response 包含所有 response 的属性，同时有如下属性：

属性 | 类型 | 读写 | 说明
---|---|---|---
text | string | 读写 | text
html | string | 读写 | html
json | json | 读写 | json

# file response

file response 包含所有 response 的属性，同时有如下属性：

属性 | 类型 | 读写 | 说明
---|---|---|---
path | string | 读写 | file path
isAttachment | bool | 读写 | is attachment
byteRange | range | 读写 | byte range