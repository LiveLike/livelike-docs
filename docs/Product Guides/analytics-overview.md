---
title: Analytics
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Analytics | LiveLike Developer Hub | Engagement SDK
  description: >-
    LiveLike provides you with a suite of analytics tools customized to suit
    your needs. Learn more about daily reports, available metrics, and more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: analytics-event-glossary
      title: Analytics Event Glossary
---
We provide you with a suite of analytics tools depending on your needs. This doc covers the following:

1. **Daily Reports**: Reports sent each day showing aggregated data from the previous day.
2. **SDK Hooks**: Events & properties that you can send to your own analytics service.
3. **Producer Suite Live Engagement**: Realtime engagement numbers for published widgets.
[block:api-header]
{
  "title": "Daily Reports"
}
[/block]
We collect, store and analyze data on MixPanel. This data will be made available to you in the form of daily and monthly reports that contain aggregated data across all features provided by LiveLike.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ec9763f-Daily_Report.png",
        "Daily Report.png",
        2182,
        1463,
        "#e4ebf0"
      ],
      "caption": "Sample of charts provided in the daily report"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Available Metrics"
}
[/block]
The SDKs automatically collect data points related to widgets, chat, stickers, reactions, and more. The data points provided include:

* Widget impression counts and engagement rates
* Poll, quiz, prediction, and other widget interaction counts
* Chat message activity
* Chat sticker and message reactions activity

Please see the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of the available data points.
[block:api-header]
{
  "title": "SDK Hooks"
}
[/block]
All analytics events and properties collected by LiveLike are also available to you in case you want to sift through the data in greater detail using your own analytics service. For example, you can register for chat message "send" events, new widgets notifications and more. Check out the [iOS](doc:ios-analytics), [Android](doc:android-analytics) and [Web](doc:web-custom-analytics) analytics docs for a list of supported events on each platform.
[block:api-header]
{
  "title": "Producer Suite Live Engagement"
}
[/block]
The LiveLike Producer Suite provides you with realtime engagement metrics for interactive widgets. Select the program you're interested in and the Program Details tab (top) will tell you total active users and widgets sent, while the Widget History View will tell you the impressions & interactions for each widget.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3f85ba4-Screen_Shot_2020-04-13_at_5.00.37_PM.png",
        "Screen Shot 2020-04-13 at 5.00.37 PM.png",
        2154,
        1437,
        "#40424b"
      ]
    }
  ]
}
[/block]