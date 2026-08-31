---
title: Web engagementsdk v2.46.0
author: ReadMe API
hidden: false
published_at: '2023-07-28T11:51:42.103Z'
---
### What's New:

* added `livelike-comments` stock UI web component (and its related components).
* `getProfileChatRoomMemberships` API now supports fetching chat room memberships based on profileIds, when no profileIds are passed it fetches chat room memberships for current profile. [https://docs.livelike.com/docs/web-chat#chat-memberships](https://docs.livelike.com/docs/web-chat#chat-memberships)
* added optional `profileIds` arg for `getChatRoomMemberships` API to filter chat room memberships based on given profileIds.
* minor TS typing change for `IComment` interface.