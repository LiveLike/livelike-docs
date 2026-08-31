---
title: Web engagementsdk v2.29.0
author: ReadMe API
hidden: false
published_at: '2022-08-02T12:29:54.645Z'
---
### What’s New:

* Added reaction pack based API `getReactionPacks` and `getReactionPackDetail`.
* Added reaction space based API `createReactionSpace`, `updateReactionSpace`, `deleteReactionSpace`, `getReactionSpaces`, `getReactionSpaceDetail`, `addReactionSpaceEventListener`, `removeReactionSpaceEventListener`.
* Added user reaction based API `addUserReaction`, `removeUserReaction`, `getUserReactions`, `getUserReactionsCount`.

### Fixes:

* fix `livelike-chat` web component issue where after loading previous messages, user were not able to react on initially loaded messages.