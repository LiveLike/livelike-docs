---
title: iOS SDK 2.73
author: LJupcho Nastevski
hidden: false
published_at: '2023-07-03T15:49:55.523Z'
---
## What's New?

* Adds support for video playback sync
* Fixes an race condition where, if you call a method that uses the reactionSpacesUrl immediately/quickly after initializing the sdk, the method exits early and does not raise its completion
* Message history request optimization
* Timeline scrolling optimization
* Chat - delete message button will now be using the same tint color as flag message button.