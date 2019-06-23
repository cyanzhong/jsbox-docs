# type: "canvas"

`canvas` 提供的是画图的功能，在绝大部分的情况下，你可以通过各种控件的组合构造出想要的效果，如果哪些控件仍然不让你满意，你可以自己绘图，比如：

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

这将在屏幕上画一个红色的五角星，半径为 50pt。

# ctx

`canvas` 控件其实也是有一点点复杂，目前并未实现完全，请参考 Apple [官方文档](https://developer.apple.com/documentation/coregraphics)获得更多信息。

上述代码的 `ctx` 对象是我们绘制图形的上下文，要理解这个概念首先要阅读 Apple 的官方文档，其次我将介绍目前 JSBox 里面实现了的部分。

# ctx.fillColor

`fillColor` 是用于填充的颜色。

# ctx.strokeColor

`strokeColor` 是用于描边的颜色。

# ctx.font

`font` 是绘制文字时的字体。

# ctx.fontSize

`fontSize` 是绘制文字时的字号大小。

# ctx.allowsAntialiasing

`allowsAntialiasing` 表示是否允许自动抗锯齿，抗锯齿会获得更平滑的效果，但性能有所损失。

# saveGState()

存储状态。

# restoreGState()

恢复状态。

# scaleCTM(sx, sy)

进行缩放操作。

# translateCTM(tx, ty)

进行平移操作。

# rotateCTM(scale)

进行旋转操作。

# setLineWidth(width)

设置描边宽度。

# setLineCap(lineCap)

请参考文档：https://developer.apple.com/documentation/coregraphics/cglinecap

# setLineJoin(lineJoin)

请参考文档：https://developer.apple.com/documentation/coregraphics/cglinejoin

# setMiterLimit(miterLimit)

请参考文档：https://developer.apple.com/documentation/coregraphics/cgcontext/1456499-setmiterlimit

# setAlpha(alpha)

设置透明度。

# beginPath()

路径开始。

# moveToPoint(x, y)

移动到 `(x, y)` 这个点。

# addLineToPoint(x, y)

从当前点画一条线到 `(x, y)` 这个点。

# addCurveToPoint(cp1x, cp1y, cp2x, cp2y, x, y)

绘制一条曲线到 `(x, y)`，通过 `(cp1x, cp1y)` 和 `(cp2x, cp2y)` 进行曲率控制。

# addQuadCurveToPoint(cpx, cpy, x, y)

还是绘制曲线到 `(x, y)` 这个点，但是这次只有一个控制点 `(cpx, cpy)`。

# closePath()

将路径闭合。

# addRect(rect)

添加一个矩形。

# addArc(x, y, radius, startAngle, endAngle, clockwise)

添加一条弧线，以 `(x, y)` 为中点，`radius` 为半径，`startAngle` 为起始弧度，`endAngle` 为终止弧度，`clockwise` 表示是否顺时针。

# addArcToPoint(x1, y1, x2, y2, radius)

在 `(x1, y1)` 和 `(x2, y2)` 之间添加一条弧线。

# fillRect(rect)

填充一个矩形。

# strokeRect(rect)

对矩形进行描边。

# clearRect(rect)

清除一个矩形。

# fillPath()

填充一个闭合的路径。

# strokePath()

对闭合的路径进行描边。

# drawImage(rect, image)

将 `image` 绘制到 `rect` 这个矩形上。

# drawText(rect, text, attributes)

将文字绘制到 `rect` 这个矩形上：

```js
ctx.drawText($rect(0, 0, 100, 100), "你好", {
  color: $color("red"),
  font: $font(30)
});
```