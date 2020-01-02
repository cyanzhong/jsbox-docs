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
db.query("SELECT * FROM User", (rs, err) => {
  while (rs.next()) {
    const values = rs.values;
    const name = rs.get("name"); // Or rs.get(0);
  }
  rs.close();
});
```

Result set supports functions as below:

```js
const columnCount = rs.columnCount; // Column count
const columnName = rs.nameForIndex(0); // Column name
const columnIndex = rs.indexForName("age"); // Column index
const query = rs.query; // SQL Query
```

Please take a look at [Result Set](en/object/result-set.md) for details.

It's similar to update when you have arguments:

```js
db.query({
  sql: "SELECT * FROM User where age = ?",
  args: [28]
}, (rs, err) => {

});
```