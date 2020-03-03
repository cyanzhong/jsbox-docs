> We can create Objective-C class in JSBox at runtime

# $define(object)

Here is an example:

```js
$define({
  type: "MyHelper: NSObject",
  events: {
    instanceMethod: function() {
      $ui.alert("instance")
    },
    "indexPathForRow:inSection:": function(row, section) {
      $ui.alert("row: " + row + ", section: " + section)
    }
  },
  classEvents: {
    classMethod: function() {
      $ui.alert("class")
    }
  }
})
```

There are basically 3 parts:

- `type` The class name
- `events` All instance methods
- `classEvents` All class methods

Now you can use it this way:

```js
$objc("MyHelper").invoke("alloc.init").invoke("instanceMethod")
$objc("MyHelper").invoke("classMethod")
```

It works like a native class.

# $delegate(object)

In Runtime code, we often create delegate instances, you can do that with $delegate function:

```js
const textView = $objc("UITextView").$new();
textView.$setDelegate($delegate({
  type: "UITextViewDelegate",
  events: {
    "textViewDidChange:": sender => {
      console.log(sender.$text().jsValue());
    }
  }
}));
```

It creates an anonymous delegate instance automatically, with the similar parameters like $define.