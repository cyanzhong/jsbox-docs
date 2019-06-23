# request

Prop | Type | Read/Write | Description
---|---|---|---
method | string | r | http method
url | string | r | url
headers | json | r | http headers
path | string | r | path
query | json | r | query
contentType | string | r | Content-Type
contentLength | number | r | Content-Length
ifModifiedSince | date | r | If-Modified-Since
ifNoneMatch | bool | r | If-None-Match
acceptsGzip | bool | r | accepts Gzip encoding
localAddressData | data | r | local address data
localAddress | string | r | local address string
remoteAddressData | data | r | remote address data
remoteAddress | string | r | remote address string
hasBody | bool | r | has body
hasByteRange | bool | r | has byte range

# data request

data request contains all properties like request, these are special:

Prop | Type | Read/Write | Description
---|---|---|---
data | data | r | data
text | string | r | text
json | json | r | json

# file request

file request contains all properties like request, these are special:

Prop | Type | Read/Write | Description
---|---|---|---
temporaryPath | string | r | temporary file path

# multipart request

multipart request contains all properties like request, these are special:

Prop | Type | Read/Write | Description
---|---|---|---
arguments | array | r | arguments
files | array | r | files
mimeType | string | r | MIME Type

arguments properties:

Prop | Type | Read/Write | Description
---|---|---|---
controlName | string | r | control name
contentType | string | r | Content-Type
mimeType | string | r | MIME Type
data | data | r | data
string | string | r | string
fileName | string | r | file name
temporaryPath | string | r | temporary file path

# response

response is returned from handler.response:

Prop | Type | Read/Write | Description
---|---|---|---
redirect | string | rw | redirect url
permanent | bool | rw | permanent
statusCode | number | rw | http status code
contentType | string | rw | Content-Type
contentLength | string | rw | Content-Length
cacheControlMaxAge | number | rw | Cache-Control
lastModifiedDate | date | rw | Last-Modified
eTag | string | rw | ETag
gzipEnabled | bool | rw | gzip enabled
hasBody | bool | rw | has body

You can create a response like:

```js
return {
  type: "default",
  props: {
    statusCode: 404
  }
}
```

# data response

data response contains all properties like response, these are special:

Prop | Type | Read/Write | Description
---|---|---|---
text | string | rw | text
html | string | rw | html
json | json | rw | json

# file response

file response contains all properties like response, these are special:

Prop | Type | Read/Write | Description
---|---|---|---
path | string | rw | file path
isAttachment | bool | rw | is attachment
byteRange | range | rw | byte range