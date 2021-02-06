# SQLite in multi-thread

Don't use a SQLite connection in multiple threads, if necessary, use Queue instead:

```js
const queue = $sqlite.dbQueue("test.db");

// Operations
queue.operations(db => {
  db.update();
  db.query();
  //...
});

// Transaction
queue.transaction(db => {
  db.update();
  db.query();
  //...
  const rollback = errorOccured;
  return rollback;
});

queue.close();
```