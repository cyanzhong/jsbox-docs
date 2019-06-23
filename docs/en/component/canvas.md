# type: "canvas"

`canvas` provides drawing ability to JSBox, in most cases you could create UI with views, but sometimes you need to draw something:

```js
{
  type: "canvas",
  layout: $layout.fill,
  events: {
    draw: function(view, ctx) {
      var centerX = view.frame.width * 0.5
      var centerY = view.frame.height * 0.3
      var radius = 50.0
      ctx.fillColor = $color("red")
      ctx.moveToPoint(centerX, centerY - radius)
      for (var i=1; i<5; ++i) {
        var x = radius * Math.sin(i * Math.PI * 0.8)
        var y = radius * Math.cos(i * Math.PI * 0.8)
        ctx.addLineToPoint(x + centerX, centerY - y)
      }
      ctx.fillPath()
    }
  }
}
```

It creates a red pentagram, the radius is 50pt.

# ctx

`canvas` is very complicated, and is still under construction, please refer [CoreGraphics](https://developer.apple.com/documentation/coregraphics) to learn more.

`ctx` means a context in drawing operations, to understand that please read Apple Developer Docs first.

Here are some interfaces we implemented now.

# ctx.fillColor

`fillColor` is the color to fill a rect.

# ctx.strokeColor

`strokeColor` is the color to draw a line.

# ctx.font

`font` is the font to draw texts.

# ctx.fontSize

`fontSize` is the font size when draw texts.

# ctx.allowsAntialiasing

`allowsAntialiasing` allows antialiasing.

# saveGState()

Save current state.

# restoreGState()

Restore state.

# scaleCTM(sx, sy)

Scale CTM.

# translateCTM(tx, ty)

Translate CTM.

# rotateCTM(scale)

Rotate CTM.

# setLineWidth(width)

Set the line width of context.

# setLineCap(lineCap)

Set the line cap of context: https://developer.apple.com/documentation/coregraphics/cglinecap

# setLineJoin(lineJoin)

Set the line join of context: https://developer.apple.com/documentation/coregraphics/cglinejoin

# setMiterLimit(miterLimit)

Set the miter limit of context: https://developer.apple.com/documentation/coregraphics/cgcontext/1456499-setmiterlimit

# setAlpha(alpha)

Set the alpha value of context.

# beginPath()

Begin a path.

# moveToPoint(x, y)

Move a point to (x, y).

# addLineToPoint(x, y)

Add a line to point (x, y).

# addCurveToPoint(cp1x, cp1y, cp2x, cp2y, x, y)

Add a curve to point (x, y), the curvature is controlled by `(cp1x, cp1y)` and `(cp2x, cp2y)`.

# addQuadCurveToPoint(cpx, cpy, x, y)

Add a curve to point (x, y), the curvature is controlled by `(cpx, cpy)`.

# closePath()

Close the path.

# addRect(rect)

Add a rect.

# addArc(x, y, radius, startAngle, endAngle, clockwise)

Add an arc, centered at `(x, y)`, starts from `startAngle`, ends with `endAngle`.

# addArcToPoint(x1, y1, x2, y2, radius)

Add an arch between `(x1, y1)` and `(x2, y2)`.

# fillRect(rect)

Fill the rect.

# strokeRect(rect)

Stroke the rect.

# clearRect(rect)

Clear the rect.

# fillPath()

Fille the path.

# strokePath()

Stroke the path.

# drawImage(rect, image)

Draw an image to rect.

# drawText(rect, text, attributes)

Draw a text to rect:

```js
ctx.drawText($rect(0, 0, 100, 100), "Hey!", {
  color: $color("red"),
  font: $font(30)
});
```