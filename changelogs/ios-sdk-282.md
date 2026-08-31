---
title: iOS SDK 2.8.2
author: Mike M
hidden: false
published_at: '2020-08-17T21:23:00.060Z'
---
In this release for iOS we focused on implementing analytics, bug fixes and performance enhancements

* added analytics for chat reactions
* added analytics for Alert widget usage

### Fixes / Optimizations

* Optimized `getLeaderboardEntries` SDK interface to avoid race conditions when making paginated requests
* Fixed a bug with the Emoji Slider widget where the timer UI would appear in a manually controlled state scenario
* Fixed name attributes for analytics