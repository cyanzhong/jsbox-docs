# type: "gallery"

`gallery` is used to display a series of views, it can be scrolled horizontally:

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

Create a gallery with 3 images.

# props

Prop | Type | Read/Write | Description
---|---|---|---
items | object | w | all items
page | number | rw | current page index
interval | number | rw | autoplay interval, 0 means off

# events

changed will be called when page changes:

```js
changed: function(sender) {
  
}
```

# Retrieve subviews

You can retrieve subviews with methods as below:

```js
const views = $("gallery").itemViews; // All views
const view = $("gallery").viewWithIndex(0); // The first view
```

# Scroll to a page

If you want to scroll to a page with animation, do this:

```js
$("gallery").scrollToPage(index);
```