---
title: iOS SDK 2.8.4
author: Mike M
hidden: false
published_at: '2020-09-03T15:55:41.129Z'
---
In this release for iOS we focused on creating the ability for integrators to use Timeline widgets in `finished` and `result` states, also bug fixes and optimizations.

### New

* Added functionality that lets integrators view Timeline widgets in a `result` or `finished` states.

### Fixes / Optimizations

* removed Bugsnag dependency in our SDK lowering our dependencies down to three frameworks
* fixed a broken call that updated user Chat Cell Image
* optimized analytic calls that registered Sticker usage