# Data Types

Pass values between JavaScript and Native environment is not easy, we need to handle complicated data types.

Some types like `number`, `boolean` will be converted automatically, but there are still a lot of types can't be handled automatically, such as `color`, `size` etc.

So we provided a series of methods for data converting, you could check this doc whenever you need.

# Trade-off

To be honest, this way is not perfect. We can also pass JavaScript Objects to iOS directly (it works like a dictionary, or map in other languages), then we parse JSON objects for each API everytime.

But that's looks ugly, and it's not easy to provide IDE features like auto completion and syntax highlighting with that pattern.

The most important is, manage all types together makes the program safer and easy to read.