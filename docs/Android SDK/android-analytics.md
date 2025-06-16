---
title: Analytics
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Analytics | Android SDK | LiveLike Developer Hub
  description: >-
    The Engagement SDK allows you to hook into our analytic events, allowing you
    to pass through the analytics data to your own provider.
  robots: index
next:
  description: ''
---
The Engagement SDK allows you to hook into our analytic events, making it possible for you to pass through the analytics data to your own provider.
[block:api-header]
{
  "title": "Implementation"
}
[/block]
The following snippet shows how you can subscribe to analytics events with some common analytics frameworks:
[block:code]
{
  "codes": [
    {
      "code": "livelikeSdk.analyticService.subscribe(this) { analyticsService ->\n        analyticsService?.setEventObserver { eventKey, eventJson ->\n        mFirebaseAnalytics.logEvent(eventKey, eventJson)\n    }\n}\n\n// Only one observer is allowed at a time. \n// To remove the current observer, just pass an empty one:\nsdk.analyticService.latest()?.setEventObserver {}",
      "language": "kotlin"
    },
    {
      "code": "          sdk.getAnalyticService().subscribe(this, new Function1<AnalyticsService, Unit>() {\n            @Override\n            public Unit invoke(AnalyticsService analyticsService) {\n                analyticsService.setEventObserver(new Function2<String, JSONObject, Unit>() {\n                    @Override\n                    public Unit invoke(String eventKey, JSONObject eventJson) {\n                        mixpanel.track(eventKey, eventJson);\n                        Localytics.tagEvent(eventKey, eventJson);\n                        mFirebaseAnalytics.logEvent(eventKey, eventJson);\n                        return null;\n                    }\n                });\n            }\n        });\n",
      "language": "java"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Android SDK 2.48",
  "body": "From SDK 2.48 onwards, the below snippet shows how to hook into our analytic events"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "sdk.analyticService.setEventObserver { eventkey, jsonObject ->\n    mFirebaseAnalytics.logEvent(eventkey, jsonObject)\n}",
      "language": "kotlin"
    },
    {
      "code": "  sdk.getAnalyticService().setEventObserver(new Function2<String, JSONObject, Unit>() {\n                    @Override\n                    public Unit invoke(String eventKey, JSONObject eventJson) {\n                    mFirebaseAnalytics.logEvent(eventKey, eventJson);\n                     return null;\n                    }\n                });\n            \n        ",
      "language": "java"
    }
  ]
}
[/block]
The `eventKey` is the name of the event being fired. The following are the events that we fire. To only register specific events, you can filter down to the ones that you are interested in.
[block:api-header]
{
  "title": "Available Events"
}
[/block]
The following events with relevant properties are available on Android:
[block:parameters]
{
  "data": {
    "h-0": "Event",
    "h-1": "Description",
    "0-0": "**Keyboard Selected**",
    "0-1": "Fired every time the user opens the keyboard. Has a \"Keyboard Type\" property to represent the \"Sticker\" or \"Standard\" keyboard.",
    "3-1": "Fired when a user takes an action to dismiss the widget, such as when user swiping it away. This is event is not fired when a widget expires on its own",
    "3-0": "**Widget Dismissed** ",
    "4-0": "**Widget Displayed** ",
    "4-1": "Fired when a user **receives** a widget. (Note: this is a misnomer because the SDK doesn't have control over whether a widget is actually displayed to users - that is up to your application)",
    "5-0": "**Widget Interacted** ",
    "5-1": "Fired at the end of widget interaction. Includes a \"Number Of Taps\" property that counts the number of times a user taps on interactable elements in the widget.",
    "1-0": "**Chat Message Sent**",
    "1-1": "Fired each time user sends a message.",
    "7-0": "**Alert Link Opened**",
    "7-1": "Fired when user clicks on a link in Alert Widget.",
    "9-0": "**Widget Became Interactive**",
    "9-1": "Fired whenever widget becomes interactive for User.",
    "8-0": "**Video Alert Play Started**",
    "8-1": "Fired when video starts playing in Video Alert Widget.",
    "2-0": "**Chat Message Link Clicked**",
    "2-1": "Fired each time when user clicks on a link in chat message",
    "6-0": "**Widget Engaged**",
    "6-1": "Fired when a `vote` or `answer` is submitted on a Widget."
  },
  "cols": 2,
  "rows": 10
}
[/block]
See the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of available analytics events.

Note : For custom widget events

1. **Widget Became Interactive** 
Call the markAsInteractive method available in widget model whenever your Custom Widget UI becomes interactive for the User. Interactive is loosely defined and depends on your specific implementation and use-case. Typically, the Widget is interactive when user is able to submit votes/answers or open links in the case of Alert Widgets. (Available in version 3.0)


[block:code]
{
  "codes": [
    {
      "code": "// poll widget model for custom poll widget\npollWidgetModel?.markAsInteractive()",
      "language": "kotlin"
    },
    {
      "code": "  pollWidgetModel.markAsInteractive()",
      "language": "java"
    }
  ]
}
[/block]
2. **Alert Link Opened** 
For alert widgets having links, call the alertLinkClicked method available in alert widget model. This will be responsible to trigger the Alert Link Opened event.

[block:code]
{
  "codes": [
    {
      "code": "// alert widget model for custom alert widget\nalertModel.alertLinkClicked(url)",
      "language": "kotlin"
    },
    {
      "code": "alertModel.alertLinkClicked(url)",
      "language": "java"
    }
  ]
}
[/block]
3. **Video Alert Play Started**
For video alert widgets having links, call the registerPlayStarted method available in video alert widget model. This will be responsible to trigger the Video Alert Play Started event.
[block:code]
{
  "codes": [
    {
      "code": "// video alert model for custom video aert widget\nvideoAlertModel.registerPlayStarted()",
      "language": "kotlin"
    }
  ]
}
[/block]