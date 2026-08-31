---
title: react-native v0.0.1-alpha.20
author: ReadMe API
hidden: false
published_at: '2023-10-26T10:17:53.240Z'
---
What’s new:

* introduced the `userAvatarUrl` property to the `LLChat` component, enabling integrators to set avatars by providing an avatar image URL.
* introduced `useChatRoomState` hook that is same as `useChatMessages` hook to align the hook name with its functionality. (`useChatMessages` is now deprecated and will be removed in future version.)\
  Fixes:
* fix issue in widget UI reward item animation causing an error when user earns more than one reward items.