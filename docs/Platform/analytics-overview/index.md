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

1. **Analytics dashboard**: reports showing the data collected by the LiveLike platform.
2. **SDK Hooks**: events generated client-side by the SDKs that you can send to your own analytics service.

## Analytics dashboard

The analytics dashboard shows interactive reports generated from the data collected by the LiveLike platform. For more details check out the  [Analytics Dashboard](doc:analytics-dashboard) documentation.

## SDK Hooks

Events are generated client-side by the SDKs. These events generally aren't collected by the LiveLike platform, but they can be used to augment your own application analytics.  For example, you can register for events like chat messages sent, widget impressions, and more. Check out the [iOS](doc:ios-analytics), [Android](doc:android-analytics) and [Web](doc:web-custom-analytics) analytics docs for a list of supported events on each platform.

## Available data points

The SDKs  data points related to user widgets, chat, stickers, reactions, and more. The data points provided include:

* Widget impression counts and engagement rates
* Poll, quiz, prediction, and other widget interaction counts
* Chat message activity
* Chat sticker and message reactions activity

Please see the [Analytics Event Glossary](doc:analytics-event-glossary) for the full list of the available data points.

<br />
