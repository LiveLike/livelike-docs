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
[block:api-header]
{
  "title": "Introduction"
}
[/block]
LiveLike has introduced a new feature called to reply to chat messages, this feature allows the integrator to use API for sending replies to a particular message as a thread message or as a chat message with a visual significance of reply.



[block:callout]
{
  "type": "info",
  "title": "Version",
  "body": "This feature will be available from\nAndroid SDK:\nIOS SDK:\nWeb SDK:"
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "To differentiate between the chat message and a reply chat message,integrator can check the value parent message in the LiveLike chat message model .",
  "title": "Note"
}
[/block]

[block:api-header]
{
  "title": "Send Reply Chat Message"
}
[/block]
In order to send a reply chat message, Integrator can use the following API
[block:code]
{
  "codes": [
    {
      "code": "chatSession.sendReplyMessage(message,imageUrl,imageWidth = 150,imageHeight = 150,\n     liveLikeCallback = callback,\n     parentMessage = <instance of livelikeChatMessage>,\n     parentMessageId =<message of parentMessage>\n                )",
      "language": "kotlin"
    }
  ]
}
[/block]