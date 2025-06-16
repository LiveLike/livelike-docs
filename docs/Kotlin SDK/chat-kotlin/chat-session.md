---
title: Chat Session
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Sessions | Kotlin SDK | LiveLike Developer Hub
  description: >-
    This document provides instructions on how to start a chat session, send and
    receive messages, and request message history in a chat room using the
    Kotlin SDK.
  robots: index
next:
  description: ''
---
A Chat Session is your interface to interact with a chat room.

## Starting a Chat Session

```kotlin
val chatSession = sdk.createChatSession(
        timecodeGetter = object:LiveLikeKotlin.TimecodeGetterCore{
            override fun getTimecode(): EpochTime {
                return EpochTime(0) //provide your epoch time to enable sync with live video 
            }

        },
        isPlatformLocalContentImageUrl = {false},
        uiDispatcher = Dispatchers.Default
    )
  
  //connect to chat room
  chatSession.connectToChatRoom("<chat-room-id>",object : LiveLikeCallback<Unit>() {
            override fun onResponse(result: Unit?, error: String?) {
               
            }
        })
```

## Message List

The ChatSession maintains a list of all messages currently loaded into memory. This list is read-only and managed by the SDK - messages that a sent, received, and loaded from history are automatically added to the list. 

## Sending and Receiving Messages

**Sending Messages**

```kotlin
chatSession.sendMessage(
                    message, imageUrl = imageUrl, imageWidth = 150, imageHeight = 150,
                    messageMetadata = sampleMapForMessageMetadata(),
                    liveLikePreCallback = object :LiveLikeCallback<LiveLikeChatMessage>(){
                        override fun onResponse(result: LiveLikeChatMessage?, error: String?) {
                            //message sent
                        }

                    }
                )
```

**Receiving Messages**\
The `MessageListener` provide the following method for listening :

* To observe when new messages are received from other users you need to implement the `onNewMessage` method of the `MessageListener`. This will get raised every time another user successfully publishes a Chat Message to the Chat Room.\
  *Note* this listener will also raise if the sender also sent the ChatMessage to the ChatRoom.
* To observe when the history method call to fetch the history message, this will receive only current connected chatRoom messages. For this, you need to implement the `onHistoryMessage` method of the `MessageListener`.
* To observe when the message is deleted you need to implement the `onDeleteMessage` method of the `MessageListener`. This will be raised when the message is deleted from the connected ChatRoom.

```kotlin
chatSession.setMessageListener(object : MessageListener {
        override fun onDeleteMessage(messageId: String) {

        }

        override fun onErrorMessage(error: String, clientMessageId: String?) {

        }

        override fun onHistoryMessage(messages: List<LiveLikeChatMessage>) {
          //history message received for connected chatroom
        }

        override fun onNewMessage(message: LiveLikeChatMessage) {
            //new message received here
         
        }

        override fun onPinMessage(message: PinMessageInfo) {

        }

        override fun onUnPinMessage(pinMessageId: String) {

        }
     })
```

## Message History

You can request more messages from the Chat Room history by calling the loadNextHistory method on the ChatSession. This will load the next page of the transcript. The default limit is 20 messages and the maximum is 100.

```kotlin
chatSession.loadNextHistory()
```

*Note* The `loadNextHistory` calls the API to fetch the history list of the `ChatMessage` object. This will trigger the `onHistoryMessage` method of  `MessageListener`.
