> Console related APIs

# Intro

Bug is always exists, so we need to `debug`. As a development tool, JSBox has some utilities for troubleshooting.

JSBox provides a simple console for debug purpose, we can use it to log some information, and execute some scripts.

# console

`console` provides 4 methods for logging:

```js
console.info("General Information")  // Log information
console.warn("Warning Message")      // Log warning message
console.error("Error Message")       // Log error message
console.assert(false, "Message")     // Assertion
console.clear()                      // Clear all messages
console.open()                       // Open console
console.close()                      // Close console
```

Of course, the console of JSBox can run JavaScript as well, the result will be display on the console.

Besides, when JavaScript exception occured, it shows on console as an error automatically.

# How to Use Console

- Tap the bug button to enter
- Tap an item to check the details
- Long press an item to copy the content
- Input command at the bottom to debugging