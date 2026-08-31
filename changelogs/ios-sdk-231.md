---
title: iOS SDK 2.31
author: Mike M
hidden: false
published_at: '2021-09-15T14:40:11.690Z'
---
## Whats New?

* added a way to send custom chat messages using the new `sendCustomMessage` function on the `ChatSession` object

```
func sendCustomMessage(_ customData: String, completion: @escaping (Result<ChatMessage, Error>) -> Void) -> ChatMessage
```

## Bug Fixes

* fixed a bug where quickly changing prediction widget selection would lead to a mismatch in UI and data selection