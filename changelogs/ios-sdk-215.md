---
title: iOS SDK 2.15
author: Mike M
hidden: false
published_at: '2021-01-20T15:58:25.445Z'
---
## New Features

* Chat Moderation - As an integrator you now have the ability to know whether a user has been muted by the host. For a deeper dive, check out the [Chat Muting documentation](https://docs.livelike.com/docs/ios-chat-config#chat-user-muting) 

## Bug Fixes

* We updated our [Mixpanel](https://mixpanel.com/) framework used for analytics to avoid some crashes that were reported by some of our clients
* Fixed an issue with the [Image Slider Widget](https://docs.livelike.com/docs/widgets#image-slider) where sliding the picture would accidentally activate a gesture recognizer and dismiss the widget from the view