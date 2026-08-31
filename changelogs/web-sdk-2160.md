---
title: Web SDK 2.16.0
author: Aquib Vadsaria
hidden: false
published_at: '2022-01-18T14:34:52.758Z'
---
## Release Notes

* added new sponsors API `getApplicationSponsors`, `getProgramSponsors`, `getChatRoomSponsors`
* getSponsors API is deprecated (use `getProgramSponsors` API instead)
* fix regression issue in `addMessageListener` API where adding listener was not subscribing to chat room channel
* added `images` and `attributes` property in `IRewardItem` interface
* added filter by attributes option in `getApplicationRewardItems` API
* added `interactive` query parameter in `getWidgets` API