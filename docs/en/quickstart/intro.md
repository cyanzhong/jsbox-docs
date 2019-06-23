# JavaScript

`JavaScript` is a powerful and flexible programming language, to read this document, we suppose you have basic knowledge of JavaScript.

> Resources
> - [w3schools.com](https://www.w3schools.com/js/)
> - [mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

# Similar Projects

JSBox is not alone, there are so many products can `run scripts`, JSBox is heavily inspired from them, for example `Editorial` and `Automator`, they can run script too.

But JSBox is not just a copycat of those projects, we based on `JavaScript` and provided a lot of simple APIs, let you interact with iOS much easier.

By the way, there're so many frameworks provide ability to: `render native UI with JavaScript`, for example `React Native` from Facebook and `Weex` from Alibaba, JSBox didn't leverage them, there are several reasons:

- React Native and Weex are design for cross-platform
- JSBox is designed to create iOS utilities
- JSBox has a simple goal: `Keep it simple and easy to learn`

The only thing you need to know is JavaScript, you don't need to understand what's MVVM, what's React...

# Basic Concept

- API starts with `$`, e.g. `$clipboard`
- Unlike `Cocoa`, JSBox API looks extremely short, because write code on mobile device is not easy
- Mostly, parameters are `JavaScript Object`, unless it's only one parameter
- Every script has its own environment, it's like a sandbox, it's safe

Above is the brief introduction, *I'm familiar with JavaScript, can't wait to see [Sample >](en/quickstart/sample.md).*