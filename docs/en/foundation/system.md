> Operating System related APIs

# $system.brightness

Get/Set the brightness of screen:

```js
$system.brightness = 0.5
```

# $system.volume

Get/Set the volume of speaker (0.0 ~ 1.0):

```js
$system.volume = 0.5
```

# $system.call(number)

Make a phone call, similar to `$app.openURL("tel:number")`.

# $system.sms(number)

Send a text message, similar to `$app.openURL("sms:number")`.

# $system.mailto(email)

Send an email, similar to `$app.openURL("mailto:email")`.

# $system.facetime(number)

Create a FaceTime session, similar to `$app.openURL("facetime:number")`.

# $system.makeIcon(object)

Create home screen icon for url:

```js
$system.makeIcon({
  title: "Title",
  url: "https://sspai.com",
  icon: image
})
```