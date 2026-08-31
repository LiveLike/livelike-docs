---
title: javascript v0.0.1-alpha.18
author: ReadMe API
hidden: false
published_at: '2023-07-28T11:52:19.635Z'
---
### What's New:

* `getProfileChatRoomMemberships` API now supports fetching chat room memberships based on profileIds, when no profileIds are passed it fetches chat room memberships for current profile.
* added optional `profileIds` arg for `getChatRoomMemberships` API to filter chat room memberships based on given profileIds.
* minor TS typing change for `IComment` interface.