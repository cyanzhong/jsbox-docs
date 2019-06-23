# SQLite

Other than file or cache system, in JSBox you can also use SQLite as persistence layer, SQLite is a lightweight database which is very good for mobile. For more information you can refer to: https://www.sqlite.org/.

# FMDB

[FMDB](https://github.com/ccgus/fmdb) is an Objective-C wrapper for SQLite, JSBox uses this library and provides a wrapper on a higher level, so you can interact SQLite with JavaScript. That means, you can also call SQLite APIs with Runtime if necessary, but in most cases JSBox APIs are good enough.

# SQLite Browser

For better user experience, we also provide a lightweight SQLite browser, you get it for free in file explorer, it can preview SQLite files with a decent user interface.

It is read-only for now, we will add more functionalities in the future.