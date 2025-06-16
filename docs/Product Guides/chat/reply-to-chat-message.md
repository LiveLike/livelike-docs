---
title: Reply To Chat Message
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Introduction

LiveLike has introduced a new feature called to reply to chat messages, this feature allows the integrator to use API for sending replies to a particular message as a thread message or as a chat message with a visual significance of reply.

> 📘 Version
>
> This feature will be available from\
> Android SDK:\
> IOS SDK:\
> Web SDK:

> 🚧 Note
>
> To differentiate between the chat message and a reply chat message,integrator can check the value parent message in the LiveLike chat message model .

## Send Reply Chat Message

In order to send a reply chat message, Integrator can use the following API

```kotlin
chatSession.sendReplyMessage(message,imageUrl,imageWidth = 150,imageHeight = 150,
     liveLikeCallback = callback,
     parentMessage = <instance of livelikeChatMessage>,
     parentMessageId =<message of parentMessage>
                )
```
