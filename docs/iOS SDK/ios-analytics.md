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

## Implementation

You can subscribe to analytics events by conforming to the `EngagementAnalyticsDelegate`. In the code snippet below, we've included potential implementations with the most common analytic frameworks.

> 📘 For more details on what types can be expected in the data dictionary, please see our [API reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Protocols/EngagementAnalyticsDelegate.html). Please take note to ensure that the data is compatible with your chosen analytic solution.

```swift
extension VideoViewController: EngagementAnalyticsDelegate {
    func engagementAnalyticsEvent(name: String, withData data: [String: Any]) {
        print("EngagementAnalyticsDelegate: Name->\(name), data->\(data)")

        // Localytics
        Localytics.tagEvent(name, attributes: data)

        // Google Analytics - Firebase
        Analytics.logEvent(name, parameters: data)
    
        // Mixpanel
        Mixpanel.mainInstance().track(event: name, properties: data)
    }
}
```

And then setting the `analyticsDelegate` in the desired class:

```swift
var sdk: EngagementSDK

sdk.analyticsDelegate = self
```

## Available Events

The following events with relevant properties are available on iOS:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Event
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Keyboard Selected** 
      </td>

      <td>
        Fired every time the user opens the keyboard. Has a "Keyboard Type" property to represent "Sticker" or "Standard" keyboard.
      </td>
    </tr>

    <tr>
      <td>
        **Message Sent** 
      </td>

      <td>
        Fired each time user sends a message.
      </td>
    </tr>

    <tr>
      <td>
        **Widget Dismissed** 
      </td>

      <td>
        Fired each time user dismisses a widget by swiping or pressing a close button. This does not apply to Custom Widgets or Widgets in a Custom Presentation.
      </td>
    </tr>

    <tr>
      <td>
        **Widget Displayed** 
      </td>

      <td>
        Fired when a Widget is displayed. For Default Widgets this happens whenever a Widget's `viewDidLoad()` is called. For Custom Widgets this will be called whenever `registerImpression()` is called.
      </td>
    </tr>

    <tr>
      <td>
        **Widget Interacted** 
      </td>

      <td>
        Fired at the end of widget interaction. Includes a "Number Of Taps" property that counts the number of times a user taps on interactable elements in the widget. This does not apply to Custom Widgets.
      </td>
    </tr>

    <tr>
      <td>
        **Widget Engaged**
      </td>

      <td>
        Fired when a `vote` or `answer` is submitted on a Widget.
      </td>
    </tr>

    <tr>
      <td>
        **Widget Became Interactive**
      </td>

      <td>
        Fired when the Widget UI allows the user to interact with it
      </td>
    </tr>
  </tbody>
</Table>

See the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of available analytics events.
