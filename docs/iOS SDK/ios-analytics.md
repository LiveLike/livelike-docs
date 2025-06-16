---
title: Analytics
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Analytics | iOS SDK | LiveLike Developer Hub | Engagement Suite
  description: >-
    The Engagement SDK allows you to hook into our analytic events, making it
    possible for you to pass through the analytics data to your own provider.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: analytics-event-glossary
      title: Analytics Event Glossary
---
The Engagement SDK allows you to hook into our analytic events, making it possible for you to pass through the analytics data to your own provider.
[block:api-header]
{
  "title": "Implementation"
}
[/block]
You can subscribe to analytics events by conforming to the `EngagementAnalyticsDelegate`. In the code snippet below, we've included potential implementations with the most common analytic frameworks.
[block:callout]
{
  "type": "info",
  "body": "For more details on what types can be expected in the data dictionary, please see our [API reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Protocols/EngagementAnalyticsDelegate.html). Please take note to ensure that the data is compatible with your chosen analytic solution."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "extension VideoViewController: EngagementAnalyticsDelegate {\n    func engagementAnalyticsEvent(name: String, withData data: [String: Any]) {\n        print(\"EngagementAnalyticsDelegate: Name->\\(name), data->\\(data)\")\n\n        // Localytics\n        Localytics.tagEvent(name, attributes: data)\n\n        // Google Analytics - Firebase\n        Analytics.logEvent(name, parameters: data)\n    \n        // Mixpanel\n        Mixpanel.mainInstance().track(event: name, properties: data)\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]
And then setting the `analyticsDelegate` in the desired class:
[block:code]
{
  "codes": [
    {
      "code": "var sdk: EngagementSDK\n\nsdk.analyticsDelegate = self",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Available Events"
}
[/block]
The following events with relevant properties are available on iOS:
[block:parameters]
{
  "data": {
    "0-0": "**Keyboard Selected** ",
    "0-1": "Fired every time the user opens the keyboard. Has a \"Keyboard Type\" property to represent \"Sticker\" or \"Standard\" keyboard.",
    "h-0": "Event",
    "h-1": "Description",
    "1-0": "**Message Sent** ",
    "1-1": "Fired each time user sends a message.",
    "2-1": "Fired each time user dismisses a widget by swiping or pressing a close button. This does not apply to Custom Widgets or Widgets in a Custom Presentation.",
    "2-0": "**Widget Dismissed** ",
    "3-0": "**Widget Displayed** ",
    "3-1": "Fired when a Widget is displayed. For Default Widgets this happens whenever a Widget's `viewDidLoad()` is called. For Custom Widgets this will be called whenever `registerImpression()` is called.",
    "4-0": "**Widget Interacted** ",
    "4-1": "Fired at the end of widget interaction. Includes a \"Number Of Taps\" property that counts the number of times a user taps on interactable elements in the widget. This does not apply to Custom Widgets.",
    "5-0": "**Widget Engaged**",
    "5-1": "Fired when a `vote` or `answer` is submitted on a Widget.",
    "6-0": "**Widget Became Interactive**",
    "6-1": "Fired when the Widget UI allows the user to interact with it"
  },
  "cols": 2,
  "rows": 7
}
[/block]
See the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of available analytics events.