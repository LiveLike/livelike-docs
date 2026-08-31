---
title: Android SDK 2.77
author: Sumon
hidden: false
published_at: '2023-06-02T06:16:51.072Z'
---
## What's New?

* added getTokenGatedChatRoomAccessDetails API for fetching token gated chat room details that could be used to verify whether a user’s wallet address has access to chat room Refer [Token Gating Chat](https://docs.livelike.com/docs/token-gating-chat) for more details.
* added tokenGates property to createChatRoom API argument for creating token gated chat room.
* added getSmartContracts API for fetching aliases for contract addresses to be used in chat room creation
* Ability to see the replies count on a comment by utilizing property `repliesCount` of the `Comment` resource.
* A way to know whether the auto claim interaction rewards is set utilizing the autoClaimInteractionRewards flag in app resource.