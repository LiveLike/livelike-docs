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
[block:api-header]
{
  "title": "Pausing Chat & Widgets"
}
[/block]
You can [Pause a Content Session](https://livelike.readme.io/docs/ios-basic-integration#section-pause-a-content-session) as described earlier. Alternatively, you can just pause Chat or Widgets through the respective ViewControllers.
[block:code]
{
  "codes": [
    {
      "code": "let widgetViewController = WidgetViewController()\nwidgetViewController.pause()\nwidgetViewController.resume()\n\nlet chatViewController = ChatViewController()\nchatViewController.pause()\nchatViewController.resume()",
      "language": "swift"
    }
  ]
}
[/block]