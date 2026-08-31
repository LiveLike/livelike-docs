---
title: Web engagementsdk v2.42.0
author: ReadMe API
hidden: false
published_at: '2023-05-25T12:04:08.370Z'
---
### What's New:

* added `imagePicker` property to `livelike-chat` element for allowing stock UI users to upload images from device storage in the chat rooms. Refer [Chat Image Picker](https://docs.livelike.com/docs/chat-message-image-picker#showing-image-picker) Doc.
* added `chatImagePickerRenderer` property to `livelike-chat` element to customise the chat image picker. Refer [Customise Image Picker](https://docs.livelike.com/docs/chat-message-image-picker#customise-image-picker) Doc.
* Reactions in a Chat Room are now supported using the LiveLike Reaction as a Service.
* added `getTokenGatedChatRoomAccessDetails` API for fetching token gated chat room details that could be used to verify whether a user’s wallet address has access to chat room Refer [Token Gating Chat](https://docs.livelike.com/docs/token-gating-chat) for more details.
* added `token_gates` property to `createChatRoom` API argument for creating token gated chat room.