---
title: Timeline Widgets
excerpt: Android guide to Timeline Widgets
deprecated: false
hidden: false
metadata:
  title: Timeline Widgets | Android SDK | LiveLike Developer Hub
  description: >-
    The WidgetTimelineView is a presentation mode provided by the EngagementSDK.
    Learn more about LiveLike Timeline Widgets.
  robots: index
next:
  description: ''
---
> 👍 Intractable TimeLine View is available from 2.17 onwards
>
> Version 2.17 introduces the IntractableWidgetTimelineViewModel which is the preferred user experience for a Timeline style presentation mode. We highly recommend using it instead.\
> [https://docs.livelike.com/docs/widget-timeline#interactable-timeline-view](https://docs.livelike.com/docs/widget-timeline#interactable-timeline-view) 

## What are Timeline Widgets?

The WidgetTimelineView is a presentation mode provided by the EngagementSDK.\
A great use case for the Timeline Mode for widgets is to show a live blog. When a page with a live blog on it loads, all the widgets published to that page will load oldest to newest but they won't be interactive in the default behaviour of the timeline view. New widgets will be interactive though and they will appear at the top of the timeline without having to reload the page.

## Setup

Steps:

* Create a content session [Session Management](doc:android-sessions) ]
* Create TimeLineViewModel
* Attach TimeLineViewModel to TimeLineView
* Add timeline view in yours view container

```kotlin
val timeLineViewModel = WidgetTimeLineViewModel(session)
  val timeLineView = WidgetsTimeLineView(
            this,
            timeLineViewModel,
            (application as LiveLikeApplication).sdk
 )
viewContainer.addView(timeLineView)
```

## Use custom widgets for timeline

For custom widget [LiveLikeWidgetViewFactory](doc:livelikewidgetviewfactory) implemntation has to initialized on timelineview 

```kotlin
timeLineView.widgetViewFactory = TimeLineWidgetFactory(this,timeLineViewModel.timeLineWidgets)
```

## Decide interactivity of widget in a timeline

This strategy can be placed on a timeline view model to make any widget interactive or non-interactive

```kotlin
timeLineViewModel.decideWidgetInteractivity = object : DecideWidgetInteractivity{
            override fun wouldAllowWidgetInteraction(widget: LiveLikeWidget): Boolean {
                return true
            }
        }
```

## **Custom Theme of Widget in a timeline**

Adding theme for widgets in timeline

```kotlin
timeLineView.applyTheme(jonObject.json)
```

```kotlin
val element = LiveLikeEngagementTheme.instanceFrom(JsonParser.parseString(theme).asJsonObject)
timeLineView.applyTheme(<object of LiveLikeEngagementTheme>)
```

## UseCase : Filter Widget

You may want to hide specific widget types from appearing in the timeline, it is for both history and real-time widgets.

> 🚧 Android SDK version 2.16.3
>
> The filter method in the timeline is available from 2.16.3

In this example, we will filter all *Alert Widgets* from being displayed in the timeline.

```kotlin
val timeLineViewModel = WidgetTimeLineViewModel(getSession()!!) { widget ->
 widget.getWidgetType() == WidgetType.ALERT           
}
```

> 📘 All the features below are available from android SDK version 2.17

## Customise Timeline Collection Divider

This will allow add a custom separator between widgets in a timeline.\
The example below adds a drawable as separator with white as backgroundColor and height as 20

```kotlin
timeLineView.setSeparator(ContextCompat.getDrawable(this, R.drawable.white_separator))
```

```xml
<layer-list
    xmlns:android="http://schemas.android.com/apk/res/android">
    <item >
        <shape
            android:shape="rectangle">
            <size
                android:width="1dp"
                android:height="20dp" />
            <solid android:color="#FFFFFF" />
        </shape>
    </item>

</layer-list>
```

## Interactable TimeLine View

We have added an **InteractiveTimeLineViewModel class**, in which all Widgets are interactive by default unless previous user input would make interactions invalid, like an already answered quiz or a prediction that has already been followed up on.

**How to create a Intractable TimeLine View\&#xA;**\
The below code sample shows how to create a timeline view with IntractableTimelineViewModel

```kotlin
val timeLineViewModel = IntractableWidgetTimeLineViewModel(session)
  val timeLineView = WidgetsTimeLineView(
            this,
            timeLineViewModel,
            (application as LiveLikeApplication).sdk
 )
viewContainer.addView(timeLineView)
```

Integrator can now also control the timer on widgets in the Intractable timeline. By default there will be no timer, interaction duration will be kept indefinite if implementation of widgetTimerController is not defined.

The below code sample shows how we can implement a widgetTimerController.

```kotlin
if(customTime){
    // integrator timeout configured
    timeLineView.widgetTimerController = object : WidgetTimerController(){
      override fun timeValue(widget: LiveLikeWidget): String {
        return customTime // customTime should be in ISO8601 duration formatted String
        }
    }
  }else{
    //CMS timeout configured
    timeLineView.widgetTimerController = CMSSpecifiedDurationTimer()
  }
```
