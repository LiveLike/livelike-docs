---
title: Widget Apis
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget APIs | Kotlin SDK | LiveLike
  description: >-
    This document explains how to subscribe to new widgets using the widgetFlow
    in ContentSession and how to retrieve details of a specific published widget
    by querying the backend with its id and kind.
  robots: index
next:
  description: ''
---
## Subscribing to Realtime Widgets

Using the widgetFlow inside ContentSession, you can subscribe to the upcoming new widgets that are published by the producer. 

```kotlin
private var contentSession: ContentSession
 
 runBlocking {
        contentSession.widgetFlow?.collect{ widget ->
          // handle new widget received
        }
    }
```

## Get Details of Published Widget

As an integrator, you have the ability to query our backend for a specific widget to either display it to the user right away or save the widget details for later use. In order to retrieve a Widget, you will need to know it's id and kind 

```kotlin
private var contentSession: ContentSession
   
   contentSession.getPublishedWidgets(
        LiveLikePagination.FIRST,
        object : LiveLikeCallback<List<LiveLikeWidget>>() {
            override fun onResponse(
                result: List<LiveLikeWidget>?,
                error: String?
            ) {
               result?.let{
                // handle published widget
               }
            }
        }
    )
 }
```
