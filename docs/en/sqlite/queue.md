# SQLite in multi-thread

Don't use a SQLite connection in multiple threads, if necessary, use Queue instead:

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