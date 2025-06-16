---
title: Threading in Chat
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
Read: [Threads in Chat](doc:threads-in-chat)

## Sending a Reply

To send a reply pass the parent message’s id in the sendMessage API

```swift
var chatSesson: ChatSession

chatSession.sendMessage(
    NewChatMessage(
        text: "<text>",
        parentMessageID: "<parent-message-id>"
    )
) { result in
    ...
}
```

## Get Replies to a Message

To get the replies to a message pass the parent message’s id in the getChatMessages API

```swift
var livelike: LiveLike

livelike.chat.getChatMessages(
    page: .first,
    options: GetChatMessageRequestOptions(
        chatRoomID: "<chat-room-id>",
        parentMessageID: "<parent-message-id>"
    )
) { result in
    ...
}
```

## Listening for Replies to a Message

Listening to replies for a message is similar to listening to regular chat messages. To figure out if a new message is a reply, compare the new message’s "parent message id" with the root message’s id. [https://docs.livelike.com/docs/ios-chat-session#sending-and-receiving-messages]\(Read More)

If the parentMessageID is nil then the new message is not a reply.

```swift
class SomeClass: ChatSessionDelegate {
    let chatSession: ChatSession
    let chatMessageID: String // The id of the parent message of replies
  
    func chatSession(
        _ chatSession: ChatSession,
         didRecieveNewMessage message: ChatMessage
    ) {
        // compare new message's parent id to the chat message id of the message you're listening to replies for 
        if message.parentMessageID == chatMessageID {
            // this new message is a reply to message with id = chatMessageID
        }
    }
}
```

## Reactions for Replies

To get reactions for replies we’ll use the [Reactions Service](doc:reactions)

Use the service with:

1. `reaction space id` from  this can be found in the [Chat Room Info](https://docs.livelike.com/docs/chat-rooms-1#getting-chat-room-information)  
2. `target id` set to the id of the reply message (`ChatMessage.id.id`)
3. `reaction id` set to id of the reaction found by getting the [Reaction Space and Reaction Pack Details]\(1. 1. <https://docs.livelike.com/docs/reactions#get-reaction-space-details-by-reaction-space-id>)  for the reaction space in step 1.