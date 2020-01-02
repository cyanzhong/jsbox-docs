# ResultSet

`ResultSet` 是 SQLite 返回的查询结果：

```js
db.query("SELECT * FROM USER", (rs, err) => {
  while (rs.next()) {

  }
  rs.close();
});
```

属性 | 类型 | 读写 | 说明
---|---|---|---
query | string | 只读 | SQL Query
columnCount | number | 只读 | 列数
values | object | 只读 | 所有值

# next()

移动到下一个结果。

# close()

关闭查询结果。

# indexForName(string)

根据列的名字获得列的序号。

# nameForIndex(number)

根据列的序号获得列的名字。

# get(object)

根据列的序号或名字获得值。

# isNull(object)

根据列的序号或名字判断是否为空。