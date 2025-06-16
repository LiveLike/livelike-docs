---
title: Native Mobile WebViews
excerpt: Using the Web SDK inside of native mobile WebViews
deprecated: false
hidden: false
metadata:
  title: Native Mobile WebViews | Web SDK | LiveLike
  description: >-
    The Web SDK is designed with cross-platform compatibility in mind, and
    native mobile Web Views are no exception. Learn more.
  robots: index
next:
  description: ''
---
The Web SDK is designed with cross-platform compatibility in mind, and native mobile WebViews are no exception. There are some things to be aware of before proceeding with a WebView-based integration inside of a mobile application though.

## Alert Widgets

Links on Alert widgets will open in a new tab when clicked in a browser. Inside of a WebView though, they may appear not to work unless they are long-pressed. This is because of the `<a>` element has a `target="_blank"` attribute on it, which most WebViews do not have a default handler for. Consult the documentation for your WebView implementation to see how this scenario can be handled.
