---
title: Popup Widgets
excerpt: Android guide to Popup Widgets
deprecated: false
hidden: false
metadata:
  title: Popup Widgets | Android SDK | LiveLike Developer Hub
  description: >-
    The WidgetPopupView is a presentation mode provided by the EngagementSDK
    that displays real-time widgets from the Producer.
  robots: index
next:
  description: ''
---
The WidgetPopupView is a presentation mode provided by the EngagementSDK.\
It is a pop-up style presenter that displays realtime widgets from the Producer one-at-a-time.\
Users have a limited time to engage with each widget before it goes away to make room for the next one

A swipe to dismiss gesture will be applied to all widgets allowing users to only engage with the widgets they care most about

## Getting started

Steps:

* Add widget view to your xml layout
* Create a content session [Session Management](doc:android-sessions) to start displayed real time widgets
* Attach the session to the widget view

Example:

```kotlin
val contentSession = engagementSDK.createContentSession("<program-id >")
widget_view.setSession(contentSession)
```

## Instantiate Widget From Widget Object

If you are getting the Livelike widget object from our method(fetchWidgetDetails) then you can use it to show in the widgetView by using the method displayWidget.

Example

```kotlin
widget_view.displayWidget(sdk,livelikeWidget )
```

## Use custom widgets for pop-up

For custom widget [LiveLikeWidgetViewFactory](doc:livelikewidgetviewfactory) implementation has to initialized on the widget view

Example:

```kotlin
widget_view.widgetViewFactory = object : LiveLikeWidgetViewFactory {
                    override fun createCheerMeterView(viewModel: CheerMeterWidgetmodel): View? {
                         return CustomCheerMeter(this@ExoPlayerActivity).apply {
                            cheerMeterWidgetModel = viewModel
                        }
                    }

                    override fun createAlertWidgetView(alertWidgetModel: AlertWidgetModel): View? {
                        return null
                    }
                }
```

## Apply theme

In order to apply theme for the widget, you need to call applyTheme on the widget view\
Example: 

```kotlin
widget_view.applyTheme(LiveLikeEngagementTheme)
```
