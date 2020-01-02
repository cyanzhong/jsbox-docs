# $sqlite.open(path)

使用文件路径来创建一个 SQLite 实例：

```js
var db = $sqlite.open("test.db");
```

# $sqlite.close(db)

关闭一个 SQLite 实例：

```js
var db = $sqlite.open("test.db");

//...
$sqlite.close(db); // Or db.close();
```

# 更新操作

SQLite 实例支持通过 update 进行更新操作：

```js
db.update("CREATE TABLE User(name text, age integer)");
// Return: { result: true, error: error }
```

也支持占位符和参数：

```js
db.update({
  sql: "INSERT INTO User values(?, ?)",
  args: ["Cyan", 28]
});
```

注：请勿通过参数拼接来进行数据库的更新操作，在任何时候都要使用占位符和参数列表。

# 查询操作

SQLite 实例支持通过 query 进行查询操作：

```js
db.query("SELECT * FROM User", (rs, err) => {
  while (rs.next()) {
    const values = rs.values;
    const name = rs.get("name"); // Or rs.get(0);
  }
  rs.close();
});
```

Result set 还支持如下操作：

```js
const columnCount = rs.columnCount; // Column count
const columnName = rs.nameForIndex(0); // Column name
const columnIndex = rs.indexForName("age"); // Column index
const query = rs.query; // SQL Query
```

请参考 [Result Set 文档](object/result-set.md)了解更多内容。

同样的，当查询有占位符和参数时，使用方法和 update 类似：

```js
db.query({
  sql: "SELECT * FROM User where age = ?",
  args: [28]
}, (rs, err) => {

});
```