# SQLite

除了使用文件和缓存系统以外，在 JSBox v1.28 之后你还可以使用 SQLite 作为数据持久化方案，SQLite 是一个轻量级的数据库系统，适合在移动平台使用。请参考 SQLite 官方文档以获得更多信息：https://www.sqlite.org/。

# FMDB

[FMDB](https://github.com/ccgus/fmdb) 是 SQLite 的一个 Objective-C 封装，JSBox 使用了这个库，并提供了更上一层的封装让你可以通过 JavaScript 调用。也即，在必要的情况下你可以通过 Runtime 直接使用 FMDB。当然在大部分的时候，JSBox 提供的接口已经够用。

# SQLite 浏览器

为了更好地支持 SQLite，与接口同时推出的还有一个轻量、简便的 SQLite 浏览器。你可以可视化的查看 SQLite 文件的内容，目前还是只读版本，敬请期待后续的更新。