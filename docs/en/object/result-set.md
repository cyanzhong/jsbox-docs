# ResultSet

`ResultSet` is returned from a SQLite query:

```js
db.query("SELECT * FROM USER", (rs, err) => {
  while (rs.next()) {

  }
  rs.close();
});
```

Prop | Type | Read/Write | Description
---|---|---|---
query | string | r | SQL Query
columnCount | number | r | column count
values | object | r | all values

# next()

Move to next result.

# close()

Close result set.

# indexForName(string)

Get index for a column name.

# nameForIndex(number)

Get name for a column index.

# get(object)

Get value for a name or index.

# isNull(object)

Check whether null for a name or index.