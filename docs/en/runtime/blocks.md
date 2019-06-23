# Objective-C Blocks

Block is a special type in Objective-C, it's very similar to closure in other languages. It works like a function, and it can capture variable outside the block, it can be a variable, a parameter, or even a return value.

Teach you Blocks isn't the goal of our document, you can read more at here: https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/WorkingwithBlocks/WorkingwithBlocks.html

Let's see how to implement Blocks in JSBox.

# $block

In JSBox you can use $block to declare a block, for example:

```js
var handler = $block("void, UITableViewRowAction *, NSIndexPath *", function(action, indexPath) {
  $ui.alert("Action")
})
```

That means you need to declare all types (including return value and all parameters) with a string, and pass a function as the block body.

If you implement this block in Objective-C, it would be:

```objc
void(^handler)(UITableViewRowAction *, NSIndexPath *) = ^(UITableViewRowAction *action, NSIndexPath *indexPath) {
  // Alert
};
```

Please don't forget the return value, otherwise it can't be recognized correctly.

Here's an example to create a TableView with only Runtime code:

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