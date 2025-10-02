---
title: Threading in Chat
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Read: [Threads in Chat](doc:threads-in-chat)

## Sending a Reply

To send a reply pass the parent message’s ID in the sendMessage API

<br />

```swift kotlin
var chatSesson: ChatSession

chatSession.sendMessage(
        message: "<text>",
        parentMessageId: "<parent-message-id>"
    )
```

## Get Replies to a Message

To get the replies to a message use the getChatMessageReplies API and pass the parent message’s id

<br />

```swift kotlin
 var chatSesson: ChatSession

        chatSesson.getChatMessageReplies(
            GetChatMessageRepliesRequestOption(parentMessageId = "<parent-message-id>")
        )
        { result, error ->
            result?.let {
                // list of replies
            }
            error?.let {
                // error
            }
        }
```

<br />

## Listening for Replies to a Message

Listening for replies to a message is similar to listening to regular chat messages. To determine if a new message is a reply, compare the new message’s "parentMessageId" with the root message’s id. \[\<https\://docs.livelike.com/docs/android-chat-session#sending-and-receiving-messages>]\(Read More)

If the parentMessageID is null then the new message is not a reply.

```kotlin
var chatSesson: ChatSession

chatSession.setMessageListener(object : MessageListener {
                override fun onNewMessage(chatRoom: String, message: LiveLikeChatMessage) {
                  // compare new message's parent id to the chat message id of the message you're listening to replies for 
                 if (message.parentMessageId!=null && message.parentMessageId == chatMessageId) {
                    // this new message is a reply to message with id = chatMessageId
                   }
                }
            })
```

<br />

## Reactions for Replies

To get reactions for replies we’ll use the [Reactions Session](https://docs.livelike.com/docs/reactions#user-reactions-api)

Create the reaction session with :

1. `reaction space id`. This can be found in Chat Room Info (getChatRoom) in Chat Client
2. Use`reactionSession.getUserReactions `and `reactionSession.getUserReactionsCount` with `target-id`which will be the message ID of the reply message

<br />

## Listening for User Reaction to a Reply

Listening for user reactions to a reply is similar to listening to reactions to regular chat messages

```kotlin

reactionSession.subscribeToUserReactionDelegate(<key>,object : UserReactionDelegate {
                    override fun onReactionAdded(reaction: UserReaction) {
                        
                    }

                    override fun onReactionRemoved(reaction: UserReaction) {
                       
                    }
                })
```
