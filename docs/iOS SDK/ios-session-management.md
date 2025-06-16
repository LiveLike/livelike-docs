---
title: Session Management
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Pausing Chat & Widgets

You can [Pause a Content Session](https://livelike.readme.io/docs/ios-basic-integration#section-pause-a-content-session) as described earlier. Alternatively, you can just pause Chat or Widgets through the respective ViewControllers.

```swift
let widgetViewController = WidgetViewController()
widgetViewController.pause()
widgetViewController.resume()

let chatViewController = ChatViewController()
chatViewController.pause()
chatViewController.resume()
```
