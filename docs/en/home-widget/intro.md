# Home Screen Widgets

Apple has introduced home screen widgets in iOS 14, and JSBox `v2.12.0` provides full support for that. At the same time, support for the today widget has been deprecated and will be removed by Apple in future iOS releases.

Home screen widgets are very different from today widgets, so it's worth taking a moment to understand some of the basic concepts.

# Basic Concepts

Home screen widgets are essentially a series of **snapshot** based on a timeline, rather than dynamically built interfaces. So when a user sees a widget, iOS doesn't run the code contained in the widget directly. Instead, the system calls the widget's code at some point (the "timeline" mechanism, we will discuss later), and our code can provide a snapshot. The system then shows these snapshots at the appropriate time, and repeat this based on some policies.

Also, home screen widgets can only handle limited user interactions:

- 2 * 2 layout only supports tapping on the widget
- 2 * 4 and 4 * 4 layouts supports tapping on components
- Tapping will open the main app and carry a URL

These limitations dictate that the role of the home screen widget is more like **information board**, complex interactions should be delegated to the main app.

# Configuring Widgets

JSBox supports all widget layouts, to add them:

- Enter edit mode in home screen, tap the add button
- Find JSBox and drag a widget to your home screen
- In edit mode, select "Edit"
- Select a script that supports widget

In contrast to the today widget, which can only run one script (although JSBox provides three), the home screen widget can be configured to create as many instances as you like, and can be stacked to display different content via the system's "stack" feature.

For more information on how to use it, please refer to tutorials provided by Apple or other posts.

# Widget Parameter

For each widget, you can set which script to run, and an additional parameter to provide more information.

The parameter is a string value that can be retrieved like this:

```js
const inputValue = $widget.inputValue;
```