---
title: iOS SDK 2.88.2
author: jelzon monzon
hidden: false
published_at: '2024-06-20T04:20:01.295Z'
---
# Bugfixes

* Reactions - Renames `UserReactionCount().selfReactedUserReactionID` to `UserReactionCount().selfReactedUserReactionId` and makes it optional
* Reactions - Fixes race condition where calling `getReactionPacks` and `getReactionSpaces` immediately after initialization could fail