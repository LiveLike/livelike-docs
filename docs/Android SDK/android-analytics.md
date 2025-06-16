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

## Implementation

The following snippet shows how you can subscribe to analytics events with some common analytics frameworks:

```kotlin
livelikeSdk.analyticService.subscribe(this) { analyticsService ->
        analyticsService?.setEventObserver { eventKey, eventJson ->
        mFirebaseAnalytics.logEvent(eventKey, eventJson)
    }
}

// Only one observer is allowed at a time. 
// To remove the current observer, just pass an empty one:
sdk.analyticService.latest()?.setEventObserver {}
```
```java
sdk.getAnalyticService().subscribe(this, new Function1<AnalyticsService, Unit>() {
            @Override
            public Unit invoke(AnalyticsService analyticsService) {
                analyticsService.setEventObserver(new Function2<String, JSONObject, Unit>() {
                    @Override
                    public Unit invoke(String eventKey, JSONObject eventJson) {
                        mixpanel.track(eventKey, eventJson);
                        Localytics.tagEvent(eventKey, eventJson);
                        mFirebaseAnalytics.logEvent(eventKey, eventJson);
                        return null;
                    }
                });
            }
        });
```

> 🚧 Android SDK 2.48
>
> From SDK 2.48 onwards, the below snippet shows how to hook into our analytic events

```kotlin
sdk.analyticService.setEventObserver { eventkey, jsonObject ->
    mFirebaseAnalytics.logEvent(eventkey, jsonObject)
}
```
```java
sdk.getAnalyticService().setEventObserver(new Function2<String, JSONObject, Unit>() {
                    @Override
                    public Unit invoke(String eventKey, JSONObject eventJson) {
                    mFirebaseAnalytics.logEvent(eventKey, eventJson);
                     return null;
                    }
                });
```

The `eventKey` is the name of the event being fired. The following are the events that we fire. To only register specific events, you can filter down to the ones that you are interested in.

## Available Events

The following events with relevant properties are available on Android:

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
        Fired every time the user opens the keyboard. Has a "Keyboard Type" property to represent the "Sticker" or "Standard" keyboard.
      </td>
    </tr>

    <tr>
      <td>
        **Chat Message Sent**
      </td>

      <td>
        Fired each time user sends a message.
      </td>
    </tr>

    <tr>
      <td>
        **Chat Message Link Clicked**
      </td>

      <td>
        Fired each time when user clicks on a link in chat message
      </td>
    </tr>

    <tr>
      <td>
        **Widget Dismissed** 
      </td>

      <td>
        Fired when a user takes an action to dismiss the widget, such as when user swiping it away. This is event is not fired when a widget expires on its own
      </td>
    </tr>

    <tr>
      <td>
        **Widget Displayed** 
      </td>

      <td>
        Fired when a user **receives** a widget. (Note: this is a misnomer because the SDK doesn't have control over whether a widget is actually displayed to users - that is up to your application)
      </td>
    </tr>

    <tr>
      <td>
        **Widget Interacted** 
      </td>

      <td>
        Fired at the end of widget interaction. Includes a "Number Of Taps" property that counts the number of times a user taps on interactable elements in the widget.
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
        **Alert Link Opened**
      </td>

      <td>
        Fired when user clicks on a link in Alert Widget.
      </td>
    </tr>

    <tr>
      <td>
        **Video Alert Play Started**
      </td>

      <td>
        Fired when video starts playing in Video Alert Widget.
      </td>
    </tr>

    <tr>
      <td>
        **Widget Became Interactive**
      </td>

      <td>
        Fired whenever widget becomes interactive for User.
      </td>
    </tr>
  </tbody>
</Table>

See the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of available analytics events.

Note : For custom widget events

1. **Widget Became Interactive**\
   Call the markAsInteractive method available in widget model whenever your Custom Widget UI becomes interactive for the User. Interactive is loosely defined and depends on your specific implementation and use-case. Typically, the Widget is interactive when user is able to submit votes/answers or open links in the case of Alert Widgets. (Available in version 3.0)

```kotlin
// poll widget model for custom poll widget
pollWidgetModel?.markAsInteractive()
```
```java
pollWidgetModel.markAsInteractive()
```

2. **Alert Link Opened**\
   For alert widgets having links, call the alertLinkClicked method available in alert widget model. This will be responsible to trigger the Alert Link Opened event.

```kotlin
// alert widget model for custom alert widget
alertModel.alertLinkClicked(url)
```
```java
alertModel.alertLinkClicked(url)
```

3. **Video Alert Play Started**\
   For video alert widgets having links, call the registerPlayStarted method available in video alert widget model. This will be responsible to trigger the Video Alert Play Started event.

```kotlin
// video alert model for custom video aert widget
videoAlertModel.registerPlayStarted()
```
