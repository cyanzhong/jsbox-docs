# $objc_retain(object)

在有些时候通过 Runtime 声明的对象会被系统释放掉，如果你想要长期持有一个对象，可以使用这个方法：

```js
var manager = $objc("Manager").invoke("new")
$objc_retain(manager)
```

这将在整个脚本运行期间保持 manger 不被释放。

# $objc_relase(object)

与 retain 相对应的函数，目的是手动释放掉对象：

```js
$objc_release(manager)
```