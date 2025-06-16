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
[block:api-header]
{
  "title": "Subscribing to Realtime Widgets"
}
[/block]
Using the widgetFlow inside ContentSession, you can subscribe to the upcoming new widgets that are published by the producer. 
[block:code]
{
  "codes": [
    {
      "code": "private var contentSession: ContentSession\n \n runBlocking {\n        contentSession.widgetFlow?.collect{ widget ->\n          // handle new widget received\n        }\n    }",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Details of Published Widget"
}
[/block]
As an integrator, you have the ability to query our backend for a specific widget to either display it to the user right away or save the widget details for later use. In order to retrieve a Widget, you will need to know it's id and kind 
[block:code]
{
  "codes": [
    {
      "code": " private var contentSession: ContentSession\n   \n   contentSession.getPublishedWidgets(\n        LiveLikePagination.FIRST,\n        object : LiveLikeCallback<List<LiveLikeWidget>>() {\n            override fun onResponse(\n                result: List<LiveLikeWidget>?,\n                error: String?\n            ) {\n               result?.let{\n                // handle published widget\n               }\n            }\n        }\n    )\n }\n    ",
      "language": "kotlin"
    }
  ]
}
[/block]