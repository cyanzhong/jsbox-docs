# Objective-C Blocks

Block 是 Objective-C 里面一种特殊的类型，虽然不完全相同但也很类似其他语言里面的闭包，如果用更通俗一点的语言来解释的话，你可以理解成 Block 很像一个函数，他能捕获外层的变量，并且能作为参数、变量甚至返回值。

关于 Block 的更多内容请参考 Apple 的官方文档：https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/WorkingwithBlocks/WorkingwithBlocks.html

本文档的内容是介绍如何在 JSBox 的 Runtime 环境里面使用 Blocks。

# $block

JSBox 里面使用 $block 来定义一个 block，例如：

```js
var handler = $block("void, UITableViewRowAction *, NSIndexPath *", function(action, indexPath) {
  $ui.alert("Action")
})
```

即使用一个字符串来按顺序声明函数的返回值和参数数据类型，然后使用一个函数来定义 Block 的函数体，这个 Block 在 Objective-C 实现的时候长这样：

```objc
void(^handler)(UITableViewRowAction *, NSIndexPath *) = ^(UITableViewRowAction *action, NSIndexPath *indexPath) {
  // Alert
};
```

请注意返回值一定要声明，否则将不能正确地识别。

这里有一个完整的使用 Runtime 构建 TableView 的例子：

```js
//-- Create window --//

$ui.render()

//-- Cell --//

$define({
  type: "TableCell: UITableViewCell"
})

//-- TableView --//

$define({
  type: "TableView: UITableView",
  events: {
    "init": function() {
      self = self.invoke("super.init")
      self.invoke("setTableFooterView", $objc("UIView").invoke("new"))
      self.invoke("registerClass:forCellReuseIdentifier:", $objc("TableCell").invoke("class"), "identifier")
      return self
    }
  }
})

//-- Manager --//

$define({
  type: "Manager: NSObject <UITableViewDelegate, UITableViewDataSource>",
  events: {
    "tableView:numberOfRowsInSection:": function(tableView, section) {
      return 5
    },
    "tableView:cellForRowAtIndexPath:": function(tableView, indexPath) {
      var cell = tableView.invoke("dequeueReusableCellWithIdentifier:forIndexPath:", "identifier", indexPath)
      cell.invoke("textLabel").invoke("setText", "Row: " + indexPath.invoke("row"))
      return cell
    },
    "tableView:didSelectRowAtIndexPath:": function(tableView, indexPath) {
      tableView.invoke("deselectRowAtIndexPath:animated:", indexPath, true)
      var cell = tableView.invoke("cellForRowAtIndexPath:", indexPath)
      var text = cell.invoke("textLabel.text").jsValue()
      $ui.alert("Tapped: " + text)
    },
    "tableView:editActionsForRowAtIndexPath:": function(tableView, indexPath) {
      var handler = $block("void, UITableViewRowAction *, NSIndexPath *", function(action, indexPath) {
        $ui.alert("Action")
      })
      var action = $objc("UITableViewRowAction").invoke("rowActionWithStyle:title:handler:", 1, "Foobar", handler)
      return [action]
    }
  }
})

var window = $ui.window.ocValue()
var manager = $objc("Manager").invoke("new")

var table = $objc("TableView").invoke("new")
table.invoke("setFrame", window.invoke("bounds"))
table.invoke("setDelegate", manager)
table.invoke("setDataSource", manager)
window.invoke("addSubview", table)
```