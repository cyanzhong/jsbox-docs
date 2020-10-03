# Timeline

As we mentioned before, a home widget is a series of time-based snapshots. Timelines are the foundation of the entire way widgets work, and we'll spend a little time explaining that concept. But before we do, please read an article provided by Apple： https://developer.apple.com/documentation/widgetkit/keeping-a-widget-up-to-date

This article is extremely important for understanding how the timeline works, especially the following diagram:

<img src='https://docs-assets.developer.apple.com/published/2971813b6a098a34d134a04e38a50b83/2550/WidgetKit-Timeline-At-End@2x.png' width=320px/>

Our code plays the role of the timeline provider in the diagram, where the system fetches a timeline and reload policy from us at the appropriate time. The system then calls the method we provide to display the widget, and makes the next fetch when the policy is satisfied.

So, an accurate timeline and a well-designed reload strategy are essential for the widget experience. For example, the weather app knows what the weather will be like for the next few hours, so it can provide multiple snapshots to the system at once and perform the next update after all snapshots are displayed.

# $widget.setTimeline(object)

JSBox uses `$widget.setTimeline(...)` to provide timelines mentioned above, E.g.:

```js
$widget.setTimeline({
  entries: [
    {
      date: new Date()
      info: {}
    }
  ],
  policy: {
    atEnd: true
  },
  render: ctx => {
    return {
      type: "text",
      props: {
        text: "Hello, World!"
      }
    }
  }
});
```

Before calling `setTimeline`, we can perform some data fetching operations, such as requesting network or getting location. However, please note that we must provide a timeline as quick as we can, to avoid possible performance issues.

## entries

Specify the date and context data for a snapshot, when timeline is predictable, we can provide many entries at the same time.

In an `entry`, we use `date` for the time when a snapshot will be displayed, and use `info` to carry some contextual information that can be retrieved in the `render` function.

> If no entry is provided, JSBox will generate a default entry using the current time.

## policy

Specify the reload policy, there are several ways to do this:

```js
$widget.setTimeline({
  policy: {
    atEnd: true
  }
});
```

This method reloads the timeline after all entries are used.

```js
$widget.setTimeline({
  policy: {
    afterDate: aDate
  }
});
```

This method reloads the timeline with an expiration date called `afterDate`.

```js
$widget.setTimeline({
  policy: {
    never: true
  }
});
```

This methods marks the timeline as static, it won't be updated periodically.

Note that, the above strategy is just "suggestions" to the system, the system does not guarantee that the reload will be done. To prevent the system from filtering out aggressive updates, please design a moderate strategy to ensure the experience.

> Without providing `entries` and `policy`, JSBox provides a default implementation of an hourly refresh for each script.

## render

When the system wants to display an entry

Upon reaching the time specified in each entry, the system will call the above `render` function, where our code returns a JSON data to describe the view.

```js
$widget.setTimeline({
  render: ctx => {
    return {
      type: "text",
      props: {
        text: "Hello, World!"
      }
    }
  }
});
```

This code shows a "Hello, World!" on the widget, we will go into more detail about the syntax later.

`ctx` contains the context to get some environmental information including entry:

```js
$widget.setTimeline({
  render: ctx => {
    const entry = ctx.entry;
    const family = ctx.family;
    const displaySize = ctx.displaySize;
    const isDarkMode = ctx.isDarkMode;
  }
});
```

Where `family` represents the type of the widget, and the values from 0 to 2 represent the three layouts: small, medium and large. `displaySize` reflects the current display size of the widget.

With these values, we can dynamically decide what view to return to the system.

## Default Implementation

When your script doesn't need to be refreshed, or the default refresh strategy is sufficient, you can simply provide a render function.

```js
$widget.setTimeline(ctx => {

});
```

As a result, JSBox will automatically create entries and set the policy to refresh every hour.

# In-app Preview

During development, when `$widget.setTimeline` is called from within the main app, a preview of the widget is opened. Three sizes are supported, and the first entry is fixed to be displayed in the timeline.

To apply the script to your actual home screen, please refer to the aforementioned setup method.