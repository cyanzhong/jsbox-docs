# contact

`contact` is used on `$contact` APIs:

Prop | Type | Read/Write | Description
---|---|---|---
identifier | string | r | identifier
content | string | r | content
contactType | number | r | type
namePrefix | string | rw | name prefix
givenName | string | rw | given name
middleName | string | rw | middle name
familyName | string | rw | family name
nameSuffix | string | rw | name suffix
nickname | string | rw | nick name
organizationName | string | rw | organization name
departmentName | string | rw | department name
jobTitle | string | rw | job title
note | string | rw | note
imageData | data | rw | avatar image data
phoneNumbers | array | rw | phone numbers
emailAddresses | array | rw | email addresses
postalAddresses | array | rw | postal addresses
urlAddresses | array | rw | url addresses
instantMessageAddresses | array | rw | instant message addresses

# group

`group` is object that returned from `$contact.fetchGroup`:

Prop | Type | Read/Write | Description
---|---|---|---
identifier | string | r | identifier
name | string | rw | name