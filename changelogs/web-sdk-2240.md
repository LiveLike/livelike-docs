---
title: Web SDK 2.24.0
author: tanya gupta
hidden: false
published_at: '2022-06-07T14:35:08.088Z'
---
## Release Notes

* added support for non-realtime Widgets, Programs, and Applications
* made stock widget UI more responsive to user's vote
* added `since` query parameter in `getWidgets` API
* fixed theming of Video Alert Widget footer
* added property `clickthrough_url` in interface `ISponsorPayload`
* added property `profileIds` to arguments of `getLeaderboardEntries`. This would help in filtering leaderboard entries by a specific set of profile Ids
* add `createVideoRoom` and `getVideoRoom` API for video room feature
* add `addSdkEventListener` and `removeSdkEventListener` for sdk events like `INITIALISED`