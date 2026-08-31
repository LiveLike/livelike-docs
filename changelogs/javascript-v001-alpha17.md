---
title: javascript v0.0.1-alpha.17
author: ReadMe API
hidden: false
published_at: '2023-07-06T16:50:59.511Z'
---
### What’s New?

* `getPostedWidgets` API now supports video on demand widgets where we have introduced `playback_time_ms` property in `IWidgetPay load`. Refer [VOD Widgets](https://docs.livelike.com/docs/vod-widgets) doc for more details.

### Fixes

* Instead of SDK deriving next url for `getMessageList` API iterator, now next url is based on the server response.