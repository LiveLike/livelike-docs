---
title: Message Metadata
excerpt: >-
  Attach custom metadata to individual chat messages to customize behavior or
  display for each message
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 Versions
>
> iOS SDK: 2.56
> Android SDK: 2.59
> Web SDK: 2.34

## Introduction

Every chat message has a `message metadata` property which is a dictionary of string keys and any (json serializable) value. This dictionary is empty by default and LiveLike will never modify this field. This property can be used to attach custom flags to adjust behavior or display for each individual message.

## Sending a message with Message Metadata

Message Metadata can be attached to a message upon creation

```javascript
LiveLike.sendMessage({
   roomId: "d7b2d84f-66a5-4a39-8924-9dde2fa6578a",
   message: "Hi",
   message_metadata: {role: "vip"}
}).then(res => {
   console.log('message',res)
   return res
})
```
```swift
let chatSession: ChatSession
				let messageMetadata: MessageMetadata = [
            "ex-key-1": "some-string",
            "ex-key-2": 1
        ]

				chatSession.sendMessage(
            NewChatMessage(
                text: "my message",
                messageMetadata: messageMetadata
            )
        ) { result in
            switch result {
            case .success(let chatMessage):
              	print(chatMessage.messageMetadata)
             		// Do something with chat message
            case .failure(let error):
                // Something went wrong
            }
        }
```
```kotlin
val messageMetadataMap = mutableMapOf<String, Any?>()
messageMetadataMap["Name"] = "Test"

// send message
chatSession.sendMessage(
    message,
    messageMetadata = messageMetadataMap,
    liveLikePreCallback = callback
)
```

## Reading Message Metadata on messages

Each chat message has a Message Metadata property. Read more on reading messages here:

[iOS Receiving Messages](https://docs.livelike.com/docs/ios-chat-session#sending-and-receiving-messages)
[Android Receiving Messages](https://docs.livelike.com/docs/chat-session-1#sending-and-receiving-messages)
[Web Receiving Messages](https://docs.livelike.com/docs/chat-api-methods#addmessagelistener)
