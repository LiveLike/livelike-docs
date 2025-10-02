---
title: Session Management
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Session Management | Android SDK | LiveLike Developer Hub
  description: >-
    A Content Session represents a user's subscription to a particular program.
    Learn more about Android SDK Session Management.
  robots: index
next:
  description: ''
---
## Start a Content Session

A Content Session represents a user's subscription to a particular program (typically a live, linear TV show, game or episode). To start a Content Session you will need a **Program ID**. Integrating teams are expected to create programs within the LiveLike system, either through the API or through the Producer Suite. The team should then copy the **Program ID**s into the relevant media metadata in their own systems, so that content sessions can be started along with media playback.

**Starting a Session**

```kotlin
val session = engagementSDK.createContentSession("<program-id >")
widget_view.setSession(session)
chat_view.setSession(session.chatSession)
```
```java
ContentSession session = engagementSDK.createContentSession("<program-id>");
WidgetView widgetView = findViewById(R.id.widgetView);
widgetView.setSession(session);
ChatView chatView = findViewById(R.id.chatView);
chatView.setSession(session);
```

**Recommendations**

It is recommended to keep the session object separated from the activity lifecycle. If your session is destroyed (eg: Orientation change) the Widget and Chat state will be lost and the services disconnected.

If you are using a ViewModel it is a good practice to create the Content Session here.

## Pause a Content Session

Content Sessions can be **paused** to temporarily ignore all incoming Widgets and Chat messages until **resumed**. This can be useful if you need to display an advertisement without overlay from the Engagement SDK, as an example.

> 📘 Removes all widgets on screen
>
> When you pause or close a Content Session all widgets on screen will be removed, even if the user was interacting.

```kotlin
//Pause
session.pause()

//Resume
session.resume()
```
```java
//Pause
session.pause();

//Resume
session.resume();
```

## Close a Content Session

When the user returns to your application's home page and away from your live video screen you will want to **close** the ContentSession. Closing a session will disconnect from Widgets and Chat and release all the related resources.\
**NOTE**: Once the session is closed, you cannot use the same session object again.

```kotlin
session.close()
```
```java
session.close();
```
