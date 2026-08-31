---
title: Android SDK 2.17
author: shivansh mittal
hidden: false
published_at: '2021-05-27T11:41:03.425Z'
---
## Whats New

**Interactable TimeLine**

[https://docs.livelike.com/docs/widget-timeline#interactable-timeline](https://docs.livelike.com/docs/widget-timeline#interactable-timeline)

**Widget Interaction Persistence**\
User's interaction history is now available. This allows user's to see their interactions on widgets between sessions. The default widgets have been updated to display previous interactions. You can access the widget interaction's via getUserInteraction() function  on all Widget Models. [https://docs.livelike.com/docs/android-widget-config#interaction-history](https://docs.livelike.com/docs/android-widget-config#interaction-history)

**UI Changes**

* Added a lock button to default Quiz and Image Slider UI
* Added a way to add spacing between Widgets in the WidgetTimeLineView
* Add default corner radius to all widgets body and header

**Engagement SDK**

* Add new API close() to close all the services, stream, and clear the variable.

## Bug Fixes

* reaction panel 2 taps required to open fixes
* Properties for Mixpanel Removed - Time Of Last Widget Interaction and Time Of Last Widget Receipt Mixpanel
* More stability and bug fixes
* Remove extra margin to headers in the alert widget.
* JSON theming update for background and progress bar
* Size management for stickers in chat.
* Added background color support to Poll,Quiz, Prediction widget body

> 📘 Important Note
>
> Artifact Resource path is changed, so when upgrading the version make sure to have the same path as :\
> implementation 'com.livelike:android-engagement-sdk:2.17'