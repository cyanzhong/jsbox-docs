# Safari Extension

On iOS 15 and above, JSBox offers full-fledged support for [Safari Extensions](https://support.apple.com/en-us/guide/iphone/iphab0432bf6/ios), you can customize your Safari using JavaScript, scripts can be run automatically or manually.

For more information on how to use Safari extensions, please refer to the official Apple documentation mentioned above, we are focusing on extension development here.

## JavaScript Web APIs

Unlike JSBox scripts, Safari extensions run in the browser environment and scripts can use all web APIs, but not JSBox-specific APIs.

For development documentation related to this, please refer to Mozilla's [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) documentation.

> You can test Safari extensions in a desktop browser or in an in-app WebView environment, but testing in a real Safari environment is still a necessary step.

## Safari Tools

Safari tools are designed to provide extensions to Safari that require users to manually select to run them, creating tools:

- New Project
- Safari Tool

To create Safari tools using VS Code, make the file name to end with `.safari-tool.js`, so that JSBox will recognize it as a Safari tool.

Example code:

```js
const video = document.querySelector("video");
if (video) {
  video.webkitSetPresentationMode("picture-in-picture");
} else {
  alert("No videos found.");
}
```

This tool turns videos on the YouTube website into Picture in Picture (PiP) mode.

## Safari Rules

Safari rules are designed to provide Safari with plugins that run automatically, without the user having to manually select to run them, creating rules:

- New Project
- Safari Rule

To create Safari rules using VS Code, make the file name to end with `.safari-rule.js`, so that JSBox will recognize it as a Safari rule.

Example code:

```js
const style = document.createElement("style");
const head = document.head || document.getElementsByTagName("head")[0];
head.appendChild(style);
style.appendChild(document.createTextNode("._9AhH0 { display: none }"));
```

When this rule is enabled, users will be able to download images on the Instagram website.

> For security reasons, Safari rules are disabled by default and need to be turned on manually by users in the app settings.