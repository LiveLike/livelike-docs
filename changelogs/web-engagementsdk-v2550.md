---
title: Web engagementsdk v2.55.0
author: ReadMe API
hidden: false
published_at: '2024-03-26T10:42:17.730Z'
---
### What’s new:

* introduced `renderMessageList` , `renderLoadPrevMessageButton` , `renderComposer` methods for integrators to override `livelike-chat` web components allowing them to customize `livelike-message-list` , load previous button and `livelike-chat-composer` .
* exposed `LiveLikeChatComposer` , `LiveLikeMessageList` , `LivelikeChatMessageAvatar` , `LiveLikeGiphyPicker` , `LiveLikeStickerPicker` , `LiveLikeQuoteMessageItem` , `LiveLikeChatMessageItem` , `LiveLikeMessageListScrollDown`, `LiveLikeMessageMenu` and `LiveLikeConfirmation` web components from `livelike-chat`.
* added params to send `reward_item_amount` and `reward_item_id` in options for `createImagePredictionWidget` API.
* added param `pageSize` to `getLeaderboardEntries` API which would enable integrators to fetch leaderboard enteries based on page size.

### Fixes:

* removed pubnub dependency for showing reactions in `livelike-chat`.