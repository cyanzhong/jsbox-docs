# $xml

JSBox provides a simple XML/HTML parser, which is very easy to use, it supports `xPath` and `CSS selector` for node querying.

# $xml.parse(object)

Parsing XML string as XML document:

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

$xml.parse() returns XML Document object:

```js
let version = doc.version;
let rootElement = doc.rootElement;
```

# Element

Element represents a node in XML Document, it contains properties as below:

Prop | Type | Read/Write | Description
---|---|---|---
node | string | r | node itself
document | $xmlDoc | r | Document
blank | bool | r | is blank node
namespace | string | r | namespace
tag | string | r | tag
lineNumber | number | r | line number
attributes | object | r | attributes
parent | $xmlElement | r | parent node
previous | $xmlElement | r | previous sibling
next | $xmlElement | r | next sibling
string | string | r | string represented value
number | number | r | number represented value
date | Date | r | date represented value

# Element.firstChild(object)

Document and Element object can query first child with xPath, selector and tag:

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

Document and Element object can query children with tag and namespace:

```js
let children = doc.rootElement.children({
  "tag": "daily-values",
  "namespace": "namespace", // Optional
});

// Get all
let allChildren = doc.rootElement.children();
```

# Element.enumerate(object)

Document and Element object can enumerate elements with xPath and CSS selector:

```js
let element = doc.rootElement;
element.enumerate({
  xPath: "//food/name", // Or selector (e.g. food > serving[units])
  handler: (element, idx) => {

  }
});
```

# Element.value(object)

Document and Element object can query value with attribute and namespace:

```js
let value = doc.rootElement.value({
  "attribute": "attribute",
  "namespace": "namespace", // Optional
});
```

# Document.definePrefix(object)

Document can define prefix for namespace:

```js
doc.definePrefix({
  "prefix": "prefix",
  "namespace": "namespace"
});
```

Here is an example for $xml: https://github.com/cyanzhong/xTeko/tree/master/extension-demos/xml-demo