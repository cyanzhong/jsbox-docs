# $xml

JSBox 内置了一个简单易用的 XML 解析器，你可以用它来解析 XML 和 HTML 文档，并支持 `xPath` 和 `CSS selector` 两种查询方式。

# $xml.parse(object)

使用 `parse` 函数完成对字符串或文件的解析：

```js

let xml = 
`
<note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
`;

let doc = $xml.parse({
  string: xml, // Or data: data
  mode: "xml", // Or "html", default to xml
});
```

# Document

$xml.parse() 返回一个 XML Document 对象：

```js
let version = doc.version;
let rootElement = doc.rootElement;
```

# Element

Element 对象表示 XML Document 上面的某一个节点，具有如下属性：

属性 | 类型 | 读写 | 说明
---|---|---|---
node | string | 只读 | 包括 tag 在内的字符串表示
document | $xmlDoc | 只读 | 此节点的 Document
blank | bool | 只读 | 节点是否为空
namespace | string | 只读 | 命名空间
tag | string | 只读 | tag
lineNumber | number | 只读 | 行数
attributes | object | 只读 | attributes
parent | $xmlElement | 只读 | 父节点
previous | $xmlElement | 只读 | 前一个兄弟节点
next | $xmlElement | 只读 | 后一个兄弟节点
string | string | 只读 | 节点的字符串表示
number | number | 只读 | 节点的数字表示
date | Date | 只读 | 节点的 Date 类型表示

# Element.firstChild(object)

Document 对象和 Element 对象都通过 xPath, selector 和 tag 获取第一个节点：

```js
let c1 = doc.rootElement.firstChild({
  "xPath": "//food/name"
});

let c2 = doc.rootElement.firstChild({
  "selector": "food > serving[units]"
});

let c3 = doc.rootElement.firstChild({
  "tag": "daily-values",
  "namespace": "namespace", // Optional
});
```

# Element.children(object)

Document 对象和 Element 对象都通过 tag 和 namespace 获取子节点：

```js
let children = doc.rootElement.children({
  "tag": "daily-values",
  "namespace": "namespace", // Optional
});

// Get all
let allChildren = doc.rootElement.children();
```

# Element.enumerate(object)

Document 对象和 Element 对象都通过 xPath 和 CSS selector 枚举：

```js
let element = doc.rootElement;
element.enumerate({
  xPath: "//food/name", // Or selector (e.g. food > serving[units])
  handler: (element, idx) => {

  }
});
```

# Element.value(object)

Document 对象和 Element 对象都通过 attribute 和 namespace 获取值：

```js
let value = doc.rootElement.value({
  "attribute": "attribute",
  "namespace": "namespace", // Optional
});
```

# Document.definePrefix(object)

Document 对象可以通过 definePrefix 定义命名空间前缀：

```js
doc.definePrefix({
  "prefix": "prefix",
  "namespace": "namespace"
});
```

请参考这个样例来了解更多：https://github.com/cyanzhong/xTeko/tree/master/extension-demos/xml-demo