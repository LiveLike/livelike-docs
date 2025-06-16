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
[block:api-header]
{
  "title": "Starting a Chat Session"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": " val chatSession = sdk.createChatSession(\n        timecodeGetter = object:LiveLikeKotlin.TimecodeGetterCore{\n            override fun getTimecode(): EpochTime {\n                return EpochTime(0) //provide your epoch time to enable sync with live video \n            }\n\n        },\n        isPlatformLocalContentImageUrl = {false},\n        uiDispatcher = Dispatchers.Default\n    )\n  \n  //connect to chat room\n  chatSession.connectToChatRoom(\"<chat-room-id>\",object : LiveLikeCallback<Unit>() {\n            override fun onResponse(result: Unit?, error: String?) {\n               \n            }\n        })  ",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Message List"
}
[/block]
The ChatSession maintains a list of all messages currently loaded into memory. This list is read-only and managed by the SDK - messages that a sent, received, and loaded from history are automatically added to the list. 
[block:api-header]
{
  "title": "Sending and Receiving Messages"
}
[/block]
** Sending Messages **


[block:code]
{
  "codes": [
    {
      "code": " chatSession.sendMessage(\n                    message, imageUrl = imageUrl, imageWidth = 150, imageHeight = 150,\n                    messageMetadata = sampleMapForMessageMetadata(),\n                    liveLikePreCallback = object :LiveLikeCallback<LiveLikeChatMessage>(){\n                        override fun onResponse(result: LiveLikeChatMessage?, error: String?) {\n                            //message sent\n                        }\n\n                    }\n                )",
      "language": "kotlin"
    }
  ]
}
[/block]
** Receiving Messages **
The `MessageListener` provide the following method for listening :
  * To observe when new messages are received from other users you need to implement the `onNewMessage` method of the `MessageListener`. This will get raised every time another user successfully publishes a Chat Message to the Chat Room.
    *Note* this listener will also raise if the sender also sent the ChatMessage to the ChatRoom.
  *  To observe when the history method call to fetch the history message, this will receive only current connected chatRoom messages. For this, you need to implement the `onHistoryMessage` method of the `MessageListener`.
  * To observe when the message is deleted you need to implement the `onDeleteMessage` method of the `MessageListener`. This will be raised when the message is deleted from the connected ChatRoom.
[block:code]
{
  "codes": [
    {
      "code": "chatSession.setMessageListener(object : MessageListener {\n        override fun onDeleteMessage(messageId: String) {\n\n        }\n\n        override fun onErrorMessage(error: String, clientMessageId: String?) {\n\n        }\n\n        override fun onHistoryMessage(messages: List<LiveLikeChatMessage>) {\n          //history message received for connected chatroom\n        }\n\n        override fun onNewMessage(message: LiveLikeChatMessage) {\n            //new message received here\n         \n        }\n\n        override fun onPinMessage(message: PinMessageInfo) {\n\n        }\n\n        override fun onUnPinMessage(pinMessageId: String) {\n\n        }\n     })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Message History"
}
[/block]
You can request more messages from the Chat Room history by calling the loadNextHistory method on the ChatSession. This will load the next page of the transcript. The default limit is 20 messages and the maximum is 100.
[block:code]
{
  "codes": [
    {
      "code": "chatSession.loadNextHistory()",
      "language": "kotlin"
    }
  ]
}
[/block]
*Note* The `loadNextHistory` calls the API to fetch the history list of the `ChatMessage` object. This will trigger the `onHistoryMessage` method of  `MessageListener`.