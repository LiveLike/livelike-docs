---
title: iOS SDK 2.30
author: jelzon monzon
hidden: false
published_at: '2021-08-31T15:07:08.246Z'
---
## What's New?

* Adjusts the default UI of the Text Ask Widget to be more similar with other widgets
* Adds a character counter to the Text Ask Widget default UI
* Adds a label to Quiz, Poll, Prediction, and Follow Up to display the Widget type. See how to enable here: [https://docs.livelike.com/docs/enabling-widget-tag-ui-for-quiz-poll-and-predictions](https://docs.livelike.com/docs/enabling-widget-tag-ui-for-quiz-poll-and-predictions)
* Adds a new delegate `chatSession(chatSession:didRecieveRoomUpdate:)` to `ChatSessionDelegate` to observe changes to a chat room's `visibility` and `contentFilter`
* Default UI for Poll and Image Slider widgets now has the ability to display a sponsor.