---
title: iOS SDK v2.61
author: Keval Shah
hidden: false
published_at: '2023-01-19T09:16:49.061Z'
---
## What's New

* Comments can now be fetched using sorting (Newest or Oldest first)
* LiveLikeSwift 
  * A pure swift module compatible with iOS, watchOS, tvOS, and macOS
  * More: [Getting Started with LiveLikeSwift](https://docs.livelike.com/docs/getting-started-with-livelikeswift)

## Bug Fixes

* When using Spoiler Prevention, `getMessages` API function returns a list of messages accordingly
* When using Spoiler Prevention, `didRecieveNewMessage` delegate function is called when a new message is received following Spoiler Prevention rules.
* Reaction Hint Image is hidden when reactions by users are present.