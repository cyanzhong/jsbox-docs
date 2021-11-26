> Compared to object caching, keychain stores sensitive data like passwords and credentials in a safe way.

# $keychain.set(key, value, domain)

Write to keychain:

```js
const succeeded = $keychain.set("key", "value", "my.domain");
```

> When `domain` is provided, `key` should be unique in your script. Otherwise, `key` should be unique in all scripts.

# $keychain.get(key, domain)

Read from keychain:

```js
const item = $keychain.get("key", "my.domain");
```

> When `domain` is provided, `key` should be unique in your script. Otherwise, `key` should be unique in all scripts.

# $keychain.remove(key, domain)

Delete a keychain item:

```js
const succeeded = $keychain.remove("key", "my.domain");
```

> When `domain` is provided, `key` should be unique in your script. Otherwise, `key` should be unique in all scripts.

# $keychain.clear(domain)

Delete all keychain items:

```js
const succeeded = $keychain.clear("my.domain");
```

> `domain` is required.

# $keychain.keys(domain)

Retrieve all keychain item keys:

```js
const keys = $keychain.keys("my.domain");
```

> `domain` is required.