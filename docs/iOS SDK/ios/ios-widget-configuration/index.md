---
title: Widget Configuration
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget Configuration | iOS SDK | LiveLike Developer Hub
  description: >-
    Unlock the full potential of the LiveLike Engagement SDK with our Widget
    Presentation APIs guide. Learn more about widget configuration.
  robots: index
next:
  description: ''
---
This section covers additional features that will help you unlock the full potential of the Engagement SDK.

## Widget Presentation APIs

A `WidgetPresentationDelegate` can be set on a `WidgetPopupViewController`, which will then be informed and consulted about widget presentation. It can respond before and after presentation and dismissal via the will/did present/dismiss methods, which can be used to perform custom animations. It can decide for each widget whether to present, discard, or defer the presentation of the widget until a later time. Deferred widgets can then be discarded or presented, in the same order they were received and deferred, via `WidgetPopupViewController`'s `presentDeferredWidget` and `discardDeferredWidget` methods. The `nextDeferredWidget` method allows you to see if there is a deferred widget waiting to be addressed. Through these APIs, custom behaviors are made possible, such as deferring a widget due to other user interactions on your custom interface, or deferring fullscreen video mode to present a less intrusive toast before showing the full widget.

This sample implementation of a delegate demonstrates animating a constraint in response to widget presentation and dismissal.

```swift
extension MyViewController: WidgetPresentationDelegate {
    func didPresent(widget: WidgetViewModel, in view: UIView) {
        UIView.animate(withDuration: 0.33) { [weak self] in
            guard let self = self else { return }
            self.widgetSlidingConstraint.constant = widget.height + 16
            self.view.layoutIfNeeded()
        }
    }

    func willDismiss(widget: WidgetViewModel, in view: UIView) {
        UIView.animate(withDuration: 0.33) { [weak self] in
            guard let self = self else { return }
            self.widgetSlidingConstraint.constant = 0
            self.view.layoutIfNeeded()
        }
    }
}
```
