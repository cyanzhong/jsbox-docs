# $sqlite.open(path)

Open a SQLite connection with file path:

```js
var db = $sqlite.open("test.db");
```

# $sqlite.close(db)

Close a SQLite connection:

```js
var db = $sqlite.open("test.db");

//...
$sqlite.close(db); // Or db.close();
```

# Update

Here's how to execute update:

```js
db.update("CREATE TABLE User(name text, age integer)");
// Return: { result: true, error: error }
```

You can also use placeholders and arguments:

```js
db.update({
  sql: "INSERT INTO User values(?, ?)",
  args: ["Cyan", 28]
});
```

PS: never concatenate strings as sql, use placeholders and values forever.

# Query

Let's see how to execute query:

```js
var object = db.query("SELECT * FROM User");
var result = object.result;
var error = object.error;

while (result.next()) {
  var values = result.values;
  var name = result.get("name"); // Or result.get(0);
}

result.close();
```

Result set supports functions as below:

```js
var columnCount = result.columnCount; // Column count
var columnName = result.nameForIndex(0); // Column name
var columnIndex = result.indexForName("age"); // Column index
var query = result.query; // SQL Query
```

Please take a look at [Result Set](en/object/result-set.md) for details.

It's similar to update when you have arguments:

```js
var rs = db.query({
  sql: "SELECT * FROM User where age = ?",
  args: [28]
});
```