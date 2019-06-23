# 多线程下的 SQLite 实例

不要用多个线程同时访问一个 SQLite 实例，如果有这个必要，你可以通过 Queue 来实现：

```js
var queue = $sqlite.dbQueue("test.db");

// Operations
queue.operations(function(db) {
  db.update();
  db.query();
  //...
});

// Transaction
queue.transaction(function(db) {
  db.update();
  db.query();
  //...
  var rollback = errorOccured;
  return rollback;
});

queue.close();
```