> Manage contact items in Contacts.app

# $contact.pick(object)

Pick one or multiple contact:

```js
$contact.pick({
  multi: false,
  handler: function(contact) {
    
  }
})
```

Please set `multi` to `true` if you want to pick up multiple items.

# $contact.fetch(object)

Fetch contacts with keywords:

```js
$contact.fetch({
  key: "Ying",
  handler: function(contacts) {

  }
})
```

The returned contacts is a list, please refer https://developer.apple.com/documentation/contacts/cncontact to understand the structure.

You can also query all contacts that in a group:

```js
$contact.fetch({
  group: group,
  handler: function(contacts) {

  }
})
```

# $contact.create(object)

Create contact item:

```js
$contact.create({
  givenName: "Ying",
  familyName: "Zhong",
  phoneNumbers: {
    "Home": "18000000000",
    "Office": "88888888"
  },
  emails: {
    "Home": "log.e@qq.com"
  },
  handler: function(resp) {

  }
})
```

# $contact.save(object)

Save modified contact item:

```js
$contact.save({
  contact: contact,
  handler: function(resp) {

  }
})
```

# $contact.delete(object)

Delete contacts:

```js
$contact.delete({
  contacts: contacts
  handler: function(resp) {
    
  }
})
```

# $contact.fetchGroups(object)

Fetch all groups:

```js
var groups = await $contact.fetchGroups();

console.log("name: " + groups[0].name);
```

# $contact.addGroup(object)

Create a new group with name:

```js
var group = await $contact.addGroup({"name": "Group Name"});
```

# $contact.deleteGroup(object)

Delete a group:

```js
var groups = await $contact.fetchGroups();

$contact.deleteGroup(groups[0]);
```

# $contact.updateGroup(object)

Save updated group:

```js
var group = await $contact.fetchGroups()[0];
group.name = "New Name";

$contact.updateGroup(group);
```

# $contact.addToGroup(object)

Add a contact to a group:

```js
$contact.addToGroup({
  contact: contact,
  group: group
});
```

# $contact.removeFromGroup(object)

Remove a contact from a group:

```js
$contact.removeFromGroup({
  contact: contact,
  group: group
});
```