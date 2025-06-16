---
title: Chat Session
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Session | Android SDK | LiveLike Developer Hub
  description: >-
    This document provides an overview of the Chat Session interface, including
    how to start a chat session, manage message lists, send and receive
    messages, receive custom messages, access message history, send custom
    messages, and delete own messages.
  robots: index
next:
  description: ''
---
A Chat Session is your interface to interact with a chat room.
[block:callout]
{
  "type": "success",
  "body": "",
  "title": "New Custom Chat APIs are available from SDK version 2.15"
}
[/block]

[block:api-header]
{
  "title": "Starting a Chat Session"
}
[/block]
Connecting to a chat room creates a ChatSession object which represents the connection. While this object exists the ChatSession will remain connected.
**Note**: the callback in connectToChatRoom is available from 2.16.
[block:code]
{
  "codes": [
    {
      "code": "val chatSession= sdk.createChatSession(object : EngagementSDK.TimecodeGetter {\n        override fun getTimecode(): EpochTime {\n            return EpochTime(player?.getPDT() ?: 0)\n        }\n    })\nchatSession.connectToChatRoom(\"<chat-room-id>\",object : LiveLikeCallback<Unit>() {\n            override fun onResponse(result: Unit?, error: String?) {\n               \n            }\n        })  ",
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
The ChatSession maintains a list of all messages currently loaded into memory. This list is read-only and managed by the SDK - messages that a sent, received, and loaded from history are automatically added to the list. List access by ID is recommended since the indices will change as messages are loaded from history.
[block:api-header]
{
  "title": "Sending and Receiving Messages"
}
[/block]
The core of any chat experience is sending and receiving messages. ** Sending Messages **
You send a message by passing the string message into the `sendMessage` method of the ChatSession. *Note*  the callback of the `sendMessage` returns `ChatMessage` object with a unique id. You can use this id to map message updates back to the message.
*Note* the callback return doesn't mean the `ChatMessage` is successfully sent. 
[block:code]
{
  "codes": [
    {
      "code": "chatSession.sendChatMessage(\n                    msg,\n                    liveLikeCallback = object : LiveLikeCallback<LiveLikeChatMessage>() {\n                        override fun onResponse(result: LiveLikeChatMessage?, error: String?) {\n                            if (error != null) {\n                                Toast.makeText(this@CustomChatActivity, error, Toast.LENGTH_SHORT)\n                                    .show()\n                            } else {\n                                //use ChatMessage model class             \n                            }\n                        }\n                    })",
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

** Receiving Custom Messages **
[block:callout]
{
  "type": "success",
  "title": "This will be available from SDK version 2.16.2 onwards"
}
[/block]
You can receive custom chat messages and can render this using more creative and engaging ways. The custom message is received via `custom_data` (String) which is obtained from 
`LiveLikeChatMessage` in `MessageListener` (used for listening messages)

Sample use cases with custom message:-
  * share widgets into chat
  * Video/programming schedule updates into chat


[block:code]
{
  "codes": [
    {
      "code": "chatSession.setMessageListener(object : MessageListener {\n                override fun onNewMessage(chatRoom: String, message: LiveLikeChatMessage) {\n                  var customData = chatMessage.custom_data\n                }\n\n                override fun onHistoryMessage(\n                    chatRoom: String,\n                    messages: List<LiveLikeChatMessage>\n                ) {\n                    \n                }\n\n\n                override fun onDeleteMessage(messageId: String) {\n                            \n                }\n            })",
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
*Note* The `loadNextHistory` calls the API to fetch the history list of the `ChatMessage` object. This will trigger the `onHistoryMessage` method of  `MessageListener` .
[block:api-header]
{
  "title": "Send Custom Message"
}
[/block]
To send the Custom message, we have to expose the API **sendCustomMessage** which accept only string parameter, the integrator can send JSON object by parsing it to string.
[block:code]
{
  "codes": [
    {
      "code": "chatSession.sendCustomChatMessage(\"\\\"check1\\\": \\\"heyaa, this is for testing\\\"}\", object : LiveLikeCallback<LiveLikeChatMessage>() {\n                    override fun onResponse(result: LiveLikeChatMessage?, error: String?) {\n                        activity?.runOnUiThread {\n                            result?.let {\n                                Log.d(\"responseCode\", result.id!!)\n                            }\n                            error?.let {\n                                Toast.makeText(context, it, Toast.LENGTH_SHORT).show()\n                            }\n                        }\n                    }\n                })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Delete Own Message"
}
[/block]
To delete the user's own sent message, we have exposed the API named **deleteMessage** which accepts messageId and provides the callback to provide the API call status.
[block:code]
{
  "codes": [
    {
      "code": "chatSession.deleteMessage(\"<message-id>\", object : LiveLikeCallback<LiveLikeEmptyResponse>() {\n                    override fun onResponse(result: LiveLikeEmptyResponse?, error: String?) {\n                        \n                    }\n                })",
      "language": "kotlin"
    }
  ]
}
[/block]