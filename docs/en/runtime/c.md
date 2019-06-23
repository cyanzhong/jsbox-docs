# $defc

In JSBox, call C functions is also possible, you can include a C function like:

```js
$defc("NSClassFromString", "Class, NSString *")
```

The first parameter is name of C function, the second parameter is a type list that describes all parameters.

After that you can use it:

```js
NSClassFromString("NSURL")
```

Also, for a C function like: `int func(void *ptr, NSObject *obj, float num)` you need to:

```js
$defc("func", "int, void *, NSObject *, float")
```

Note: struct and block are not supported yet.