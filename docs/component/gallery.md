# type: "gallery"

`gallery` 用于创建一个横向滚动的分页器，可以滚动显示：

```js
{
  type: "gallery",
  props: {
    items: [
      {
        type: "image",
        props: {
          src: "https://images.apple.com/v/iphone/home/v/images/home/limited_edition/iphone_7_product_red_large_2x.jpg"
        }
      },
      {
        type: "image",
        props: {
          src: "https://images.apple.com/v/iphone/home/v/images/home/airpods_large_2x.jpg"
        }
      },
      {
        type: "image",
        props: {
          src: "https://images.apple.com/v/iphone/home/v/images/home/apple_pay_large_2x.jpg"
        }
      }
    ],
    interval: 3,
    radius: 5.0
  },
  layout: function(make, view) {
    make.left.right.inset(10)
    make.centerY.equalTo(view.super)
    make.height.equalTo(320)
  }
}
```

创建一个有三个分页的视图，显示三张图片。

# props

属性 | 类型 | 读写 | 说明
---|---|---|---
items | object | 只写 | 每个分页项
page | number | 读写 | 当前页数
interval | number | 读写 | 自动播放间隔，为 0 表示不播放

# events

页面改变时将会调用 changed:

```js
changed: function(sender) {
  
}
```