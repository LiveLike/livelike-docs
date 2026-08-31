---
title: javascript v0.0.1-alpha.16
author: ReadMe API
hidden: false
published_at: '2023-06-07T12:26:04.701Z'
---
### What's New:

* added `replies_count` and make `replies_url` not nullable in the comment resource
* added `autoclaim_interaction_rewards` boolean to the application resource
* added `getSmartContracts` for fetching smart contract address details that could be used to get aliases name for contract addresses Refer [Doc](https://docs.livelike.com/docs/token-gate#get-smart-contracts) for more details.
* added `attributes` and `token_type` property to `createChatRoom` API argument for creating token gated chat room.
* added `token_type` and `metadata` property to `contract_balances` in `getTokenGatedChatRoomAccessDetails` API response for getting token gated chat room.