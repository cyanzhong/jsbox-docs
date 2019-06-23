> JSBox has builtin data detector, it enhances the readability of regex

*PS: If you are an expert of regex, you don't need this then.*

# $detector.date(string)

Retrieve all dates from a string:

```js
var dates = $detector.date("2017.10.10")
```

# $detector.address(string)

Retrieve all addresses from a string:

```js
var addresses = $detector.address("")
```

# $detector.link(string)

Retrieve all links from a string:

```js
var links = $detector.link("http://apple.com hello http://xteko.com")
```

# $detector.phoneNumber(string)

Retrieve all phone numbers from a string:

```js
var phoneNumbers = $detector.phoneNumber("18666666666 hello 18777777777")
```