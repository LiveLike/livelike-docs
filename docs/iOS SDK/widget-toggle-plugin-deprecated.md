---
title: Widget Toggle Plugin [Deprecated]
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
You can use this plugin to allow users to toggle widget display.

![351](https://files.readme.io/37578ed-93dd91d-Screen_Recording_2019-09-16_at_04.42_PM.gif "93dd91d-Screen_Recording_2019-09-16_at_04.42_PM.gif")

After the user has dismissed 3 (configurable) widgets prematurely - they will be presented with a **Widget Disable Dialog**.

Selecting **For Now** will disable widgets for the duration of the Content Session.

Selecting **Forever** will disable widgets until the user explicitly toggles the widgets on. This setting is stored in UserDefaults.

Regardless of the choice, the toggle button will be added to your layout for the user to toggle widgets at will.

> 📘 Once the user has been presented with the dialog, the dialog will never be shown again and the toggle button will always be visible.

**Installation**

Pre-Requisites:

1. A reference to a Content Session
2. A UIView that will serve as the parent view for the toggle button (referred to as `someParentView` in snippet below)

```swift
let widgetTogglePlugin = WidgetToggle(toggleParentView: someParentView)
session.install(plugin: widgetTogglePlugin)
```
