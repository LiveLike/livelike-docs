---
title: Web engagementsdk v2.45.0
author: ReadMe API
hidden: false
published_at: '2023-07-06T16:46:29.066Z'
---
### What's New?

* `getPostedWidgets` API now supports video on demand widgets where we have introduced `playback_time_ms` property in `IWidgetPayload`. Refer [VOD Widgets](https://docs.livelike.com/docs/vod-widgets) doc for more details.

### Fixes

* Instead of SDK deriving next url for `getMessageList` API iterator, now next url is based on the server response.