# JSBox script on action extension

`Action Extension` is displayed on iOS share sheet, JSBox scripts could be launched from here.

Besides, action extension can retrieve the data selected by user.

# Limitations

Action extension also has some Limitations, not so much like today widget.

For now, there are basically two main restrictions:

- Memory are very limited, don't launch a script that needs huge memory
- Don't use `$photo.pick`, it doesn't work

# $context

We could use `$context` to fetch external data, that's very important to make an action extension.

Please refer to [Method](en/context/method.md) to see more details.