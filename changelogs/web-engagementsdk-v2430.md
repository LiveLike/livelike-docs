---
title: Web engagementsdk v2.43.0
author: ReadMe API
hidden: false
published_at: '2023-06-07T12:25:42.401Z'
---
### What's New:

* added `replies_count` and make `replies_url` not nullable in the comment resource
* added `dateTimeFormatter` function to `livelike-chat` and `livelike-widgets` element
* added `autoclaim_interaction_rewards` boolean to the application resource
* added `getSmartContracts` for fetching smart contract address details that could be used to get aliases name for contract addresses for logged in user. Refer [Doc](https://docs.livelike.com/docs/token-gating-chat#get-smart-contracts-to-create-token-gated-chatroom) for more details.
* added `attributes` and `token_type` property to `createChatRoom` API argument for creating token gated chat room.
* added `token_type` and `metadata` property to `contract_balances` in `getTokenGatedChatRoomAccessDetails` API response for getting token gated chat room.
* added `uploadImage` API.