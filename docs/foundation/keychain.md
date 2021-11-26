> 相较于对象缓存，钥匙串以安全的方式存储密码、登录票据等敏感信息。

# $keychain.set(key, value, domain)

写入到钥匙串：

```js
const succeeded = $keychain.set("key", "value", "my.domain");
```

> 当提供 `domain` 时，`key` 应该在您的脚本内唯一。反之，`key` 应该在所有脚本内唯一。

# $keychain.get(key, domain)

从钥匙串中读取：

```js
const item = $keychain.get("key", "my.domain");
```

> 当提供 `domain` 时，`key` 应该在您的脚本内唯一。反之，`key` 应该在所有脚本内唯一。

# $keychain.remove(key, domain)

删除一个钥匙串项目：

```js
const succeeded = $keychain.remove("key", "my.domain");
```

> 当提供 `domain` 时，`key` 应该在您的脚本内唯一。反之，`key` 应该在所有脚本内唯一。

# $keychain.clear(domain)

删除所有的钥匙串项目：

```js
const succeeded = $keychain.clear("my.domain");
```

> `domain` 为必填项。

# $keychain.keys(domain)

获取所有钥匙串键：

```js
const keys = $keychain.keys("my.domain");
```

> `domain` 为必填项。