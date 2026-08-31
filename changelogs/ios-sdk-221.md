---
title: iOS SDK 2.21
author: Mike M
hidden: false
published_at: '2021-04-08T18:52:16.458Z'
---
### New Features

As an integrator you are now able to send messages and query chat history using new SDK Chat API's

* `sendMessage(_ chatMessage: NewChatMessage, completion: @escaping (Result<ChatMessage, Error>) -> Void) -> ChatMessage`
* `loadNextHistory(completion: @escaping (Result<[ChatMessage], Error>) -> Void)`

For more information please see the [Chat Session documentation](https://docs.livelike.com/docs/chat-session)

### Bug Fixes / Optimizations

* Fixed an issue where chat messages are being cut off in a chat room with avatars
* Optmizations to the chat infrastructure