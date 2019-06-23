> 用于与系统通讯录进行交互，例如读取或写入

# $contact.pick(object)

从通讯录中选择一个或多个联系人：

```js
$contact.pick({
  multi: false,
  handler: function(contact) {
    
  }
})
```

其中 `multi` 为 `true` 时表示选择多个联系人。

# $contact.fetch(object)

通过关键字查找某些联系人：

```js
$contact.fetch({
  key: "Ying",
  handler: function(contacts) {

  }
})
```

获得的是一个数组，每个元素支持很多属性，请参考：https://developer.apple.com/documentation/contacts/cncontact

也可以查找某个分组下面的所有联系人：

```js
$contact.fetch({
  group: group,
  handler: function(contacts) {

  }
})
```

# $contact.create(object)

创建联系人：

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

将更新后的 contact 对象存储到系统通讯录：

```js
$contact.save({
  contact: contact,
  handler: function(resp) {

  }
})
```

# $contact.delete(object)

删除一些联系人：

```js
$contact.delete({
  contacts: contacts
  handler: function(resp) {
    
  }
})
```

# $contact.fetchGroups(object)

获取联系人分组：

```js
var groups = await $contact.fetchGroups();

console.log("name: " + groups[0].name);
```

# $contact.addGroup(object)

添加一个新的分组：

```js
var group = await $contact.addGroup({"name": "Group Name"});
```

# $contact.deleteGroup(object)

删除一个分组：

```js
var groups = await $contact.fetchGroups();

$contact.deleteGroup(groups[0]);
```

# $contact.updateGroup(object)

保存更新后的分组：

```js
var group = await $contact.fetchGroups()[0];
group.name = "New Name";

$contact.updateGroup(group);
```

# $contact.addToGroup(object)

将联系人添加到分组：

```js
$contact.addToGroup({
  contact: contact,
  group: group
});
```

# $contact.removeFromGroup(object)

将联系人从分组中移除：

```js
$contact.removeFromGroup({
  contact: contact,
  group: group
});
```