---
title: react-native v0.0.1-alpha.27
author: ReadMe API
hidden: false
published_at: '2023-12-07T11:22:42.960Z'
---
### What’s new:

* added a feature to enable users to view all previous chat messages by clicking the `Load Previous Messages` button in `LLChat` component. (Requires RN version `0.72.x` or higher to use this feature, since it uses `maintainVisibleContentPosition` property of `Flatlist` react-native component which is only available for all devices post `0.72.x` release)
* added a feature to unblock a mistakenly blocked chat message user in `LLChat` component.
* added a feature to display error banner if a user reports a reported chat message in `LLChat` component.