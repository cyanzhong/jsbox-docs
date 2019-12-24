*This website is based on [Docsify](https://docsify.js.org), hosted on the [GitHub](https://github.com/cyanzhong/jsbox-docs), pull requests are welcome.*

# JSBox APIs

Create powerful addins for JSBox with JavaScript, ES6 is supported, and we provide tons of APIs to interact with iOS directly

# JSBox Node.js

JSBox 2.0 provides Node.js runtime, you can also use Node APIs. For details, please refer to: https://cyanzhong.github.io/jsbox-nodejs/#/en/

# How to run code in JSBox

- Write code in JSBox directly

  > There's a simple code editor inside JSBox, provides auto completion and syntax highlighting, it will be better in the future

- Get code through URL Scheme

  > For example: jsbox://import?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcyanzhong%2FxTeko%2Fmaster%2Fextension-scripts%2Fapi.js&name=test&icon=icon_063.png
  > - Parameters:
  >  - `url`: Code file url
  >  - `name`: The script name
  >  - `icon`: JSBox icon set name, refer: https://github.com/cyanzhong/xTeko/tree/master/extension-icons
  > - Note:
  >  - Parameters should be URL Encoded
  >  - Please use ASCII characters to naming a URL

- Write code using VSCode extension

  > 1. Open editor settings in JSBox, turn on `Debug Mode`
  > 2. Back to home screen and restart JSBox, switch to the 4th tab to check `Host`
  > 3. Search & install `JSBox` extension in VSCode extension market
  > 4. Open a JavaScript file with VSCode, set host on the menu
  > 5. Now you can write code, and sync it to your iPhone automatically

- AirDrop & Share Sheet

  > You can share a js file with AirDrop to JSBox, but you need to import those files manually.
  > For example you can do that with this script: https://github.com/cyanzhong/xTeko/blob/master/extension-demos/sync-inbox.js

- Do it yourself! JSBox provides APIs to manage your scripts

  > Here's an example: https://github.com/cyanzhong/xTeko/blob/master/extension-demos/addin-gallery.js

# Open Source

In order to provide more demo scripts, we created a open source project on GitHub: https://github.com/cyanzhong/xTeko

Welcome to improve this project together, you can contribute by [New issue](https://github.com/cyanzhong/xTeko/issues/new) or [New pull request](https://github.com/cyanzhong/xTeko/compare).

Thank you!

# Contact us

If you have any question or suggestion about JSBox, you can find us by:

- Email: [log.e@qq.com](mailto:log.e@qq.com)
- Weibo: [@StackOverflowError](https://weibo.com/0x00eeee)
- Twitter: [@cyanapps](https://twitter.com/cyanapps)
- Telegram: [PinTG](https://t.me/PinTG)

*I'm ready, [let's start >](en/quickstart/intro.md)*

> This document is still under construction, please note changes in the future