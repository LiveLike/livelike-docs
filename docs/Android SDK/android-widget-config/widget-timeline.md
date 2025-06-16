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
[block:callout]
{
  "type": "success",
  "title": "Intractable TimeLine View is available from 2.17 onwards",
  "body": "Version 2.17 introduces the IntractableWidgetTimelineViewModel which is the preferred user experience for a Timeline style presentation mode. We highly recommend using it instead. \n[https://docs.livelike.com/docs/widget-timeline#interactable-timeline-view](https://docs.livelike.com/docs/widget-timeline#interactable-timeline-view) "
}
[/block]

[block:api-header]
{
  "title": "What are Timeline Widgets?"
}
[/block]
The WidgetTimelineView is a presentation mode provided by the EngagementSDK. 
A great use case for the Timeline Mode for widgets is to show a live blog. When a page with a live blog on it loads, all the widgets published to that page will load oldest to newest but they won't be interactive in the default behaviour of the timeline view. New widgets will be interactive though and they will appear at the top of the timeline without having to reload the page.
[block:api-header]
{
  "title": "Setup"
}
[/block]
Steps:

* Create a content session [Session Management](doc:android-sessions) ]
* Create TimeLineViewModel
* Attach TimeLineViewModel to TimeLineView
* Add timeline view in yours view container

[block:code]
{
  "codes": [
    {
      "code": " val timeLineViewModel = WidgetTimeLineViewModel(session)\n  val timeLineView = WidgetsTimeLineView(\n            this,\n            timeLineViewModel,\n            (application as LiveLikeApplication).sdk\n )\nviewContainer.addView(timeLineView)\n",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Use custom widgets for timeline"
}
[/block]
For custom widget [LiveLikeWidgetViewFactory](doc:livelikewidgetviewfactory) implemntation has to initialized on timelineview 
[block:code]
{
  "codes": [
    {
      "code": " timeLineView.widgetViewFactory = TimeLineWidgetFactory(this,timeLineViewModel.timeLineWidgets)",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Decide interactivity of widget in a timeline"
}
[/block]
This strategy can be placed on a timeline view model to make any widget interactive or non-interactive
[block:code]
{
  "codes": [
    {
      "code": " timeLineViewModel.decideWidgetInteractivity = object : DecideWidgetInteractivity{\n            override fun wouldAllowWidgetInteraction(widget: LiveLikeWidget): Boolean {\n                return true\n            }\n        }",
      "language": "kotlin"
    }
  ]
}
[/block]
## **Custom Theme of Widget in a timeline**

Adding theme for widgets in timeline
[block:code]
{
  "codes": [
    {
      "code": "timeLineView.applyTheme(jonObject.json)",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "\nval element = LiveLikeEngagementTheme.instanceFrom(JsonParser.parseString(theme).asJsonObject)\ntimeLineView.applyTheme(<object of LiveLikeEngagementTheme>)",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "UseCase : Filter Widget"
}
[/block]
You may want to hide specific widget types from appearing in the timeline, it is for both history and real-time widgets.

[block:callout]
{
  "type": "warning",
  "title": "Android SDK version 2.16.3",
  "body": "The filter method in the timeline is available from 2.16.3"
}
[/block]
In this example, we will filter all *Alert Widgets* from being displayed in the timeline.
[block:code]
{
  "codes": [
    {
      "code": "val timeLineViewModel = WidgetTimeLineViewModel(getSession()!!) { widget ->\n widget.getWidgetType() == WidgetType.ALERT           \n}",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "All the features below are available from android SDK version 2.17"
}
[/block]

[block:api-header]
{
  "title": "Customise Timeline Collection Divider"
}
[/block]
This will allow add a custom separator between widgets in a timeline. 
The example below adds a drawable as separator with white as backgroundColor and height as 20
[block:code]
{
  "codes": [
    {
      "code": "timeLineView.setSeparator(ContextCompat.getDrawable(this, R.drawable.white_separator))",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "<layer-list\n    xmlns:android=\"http://schemas.android.com/apk/res/android\">\n    <item >\n        <shape\n            android:shape=\"rectangle\">\n            <size\n                android:width=\"1dp\"\n                android:height=\"20dp\" />\n            <solid android:color=\"#FFFFFF\" />\n        </shape>\n    </item>\n\n</layer-list>",
      "language": "xml"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Interactable TimeLine View"
}
[/block]
We have added an **InteractiveTimeLineViewModel class**, in which all Widgets are interactive by default unless previous user input would make interactions invalid, like an already answered quiz or a prediction that has already been followed up on.

**How to create a Intractable TimeLine View
**
The below code sample shows how to create a timeline view with IntractableTimelineViewModel
[block:code]
{
  "codes": [
    {
      "code": "val timeLineViewModel = IntractableWidgetTimeLineViewModel(session)\n  val timeLineView = WidgetsTimeLineView(\n            this,\n            timeLineViewModel,\n            (application as LiveLikeApplication).sdk\n )\nviewContainer.addView(timeLineView)",
      "language": "kotlin"
    }
  ]
}
[/block]
Integrator can now also control the timer on widgets in the Intractable timeline. By default there will be no timer, interaction duration will be kept indefinite if implementation of widgetTimerController is not defined.

The below code sample shows how we can implement a widgetTimerController.
[block:code]
{
  "codes": [
    {
      "code": "  if(customTime){\n    // integrator timeout configured\n    timeLineView.widgetTimerController = object : WidgetTimerController(){\n      override fun timeValue(widget: LiveLikeWidget): String {\n        return customTime // customTime should be in ISO8601 duration formatted String\n        }\n    }\n  }else{\n    //CMS timeout configured\n    timeLineView.widgetTimerController = CMSSpecifiedDurationTimer()\n  }",
      "language": "kotlin"
    }
  ]
}
[/block]