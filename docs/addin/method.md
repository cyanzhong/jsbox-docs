> 通过脚本可以控制 JSBox 的脚本，包括安装新脚本、删除脚本等操作

# $addin.list

获得已安装的全部脚本：

```js
var addins = $addin.list
```

数据结构：

属性 | 类型 | 读写 | 说明
---|---|---|---
name | string | 读写 | 名称
category | string | 读写 | 分类
url | string | 读写 | url
data | $data | 读写 | 文件
id | string | 读写 | id
version | string | 读写 | 版本号
icon | string | 读写 | 图标
iconImage | image | 只读 | 获得图标
module | bool | 读写 | 是否保存为模块
author | string | 读写 | 作者
website | string | 读写 | 网站

以上字段 `name` 和 `data` 为必须，其余字段可选。

你可以对取出的 `addins` 进行更改，例如重新排序，然后这样保存：

```js
$addin.list = addins;
```

# $addin.categories

获取当前设备所有的脚本分类，返回 string 数组：

```js
const categories = $addin.categories;
```

你可以进行修改，例如重新排序或增加分类，然后这样保存：

```js
$addin.categories = categories;
```

# $addin.current

获取当前正在运行的脚本，结构如上述所示：

```js
var current = $addin.current
```

# $addin.save(object)

安装一个新的脚本：

```js
$addin.save({
  name: "New Script",
  data: $data({string: "$ui.alert('Hey!')"}),
  handler: function(success) {
    
  }
})
```

JSBox 内将会安装一个叫做 New Script 的脚本，save 的所有字段遵循上述数据结构。

# $addin.delete(name)

通过脚本的名字删除一个脚本：

```js
$addin.delete("New Script")
```

将会删除前一个例子里面创建的脚本。

# $addin.run(name)

通过脚本的名字运行一个脚本：

```js
$addin.run("New Script")
```

将会运行名为 New Script 的脚本，当然前提是你没有删掉它。

从 v1.15.0 开始，你也可以传递而外的参数：

```js
$addin.run({
  name: "New Script",
  query: {
    "a": "b"
  }
})
```

参数将会被传递到 `$context.query` 以便获取到。

# $addin.restart()

重新运行当前的脚本。

# $addin.compile(script)

将 script 转换成 JSBox 可用的语法：

```js
var result = $addin.compile("$ui.alert('Hey')");

// result => JSBox.ui.alert('Hey')
```

# $addin.eval(script)

与 `eval()` 类似，但先会将 script 转换成 JSBox 语法：

```js
$addin.eval("$ui.alert('Hey')");
```