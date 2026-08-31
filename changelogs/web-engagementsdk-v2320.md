---
title: Web engagementsdk v2.32.0
author: ReadMe API
hidden: false
published_at: '2022-09-27T15:33:12.213Z'
---
* Added toggle property `showFilteredMessages` in component `livelike-chat` to show/hide messages with banned words in a chat room
* Added boolean param `includeFilteredMessages` in API `getMessageList` to include messages with banned words in the message list
* Fix incorrect user reaction count in `livelike-chat` element in case of stale/invalid reaction.