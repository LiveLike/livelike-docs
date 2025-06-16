---
title: Message Metadata
excerpt: >-
  Attach custom metadata to individual chat messages to customize behavior or
  display for each message
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "Versions",
  "body": "iOS SDK: 2.56\nAndroid SDK: 2.59\nWeb SDK: 2.34"
}
[/block]

[block:api-header]
{
  "title": "Introduction"
}
[/block]
Every chat message has a `message metadata` property which is a dictionary of string keys and any (json serializable) value. This dictionary is empty by default and LiveLike will never modify this field. This property can be used to attach custom flags to adjust behavior or display for each individual message.
[block:api-header]
{
  "title": "Sending a message with Message Metadata"
}
[/block]
Message Metadata can be attached to a message upon creation
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.sendMessage({\n   roomId: \"d7b2d84f-66a5-4a39-8924-9dde2fa6578a\",\n   message: \"Hi\",\n   message_metadata: {role: \"vip\"}\n}).then(res => {\n   console.log('message',res)\n   return res\n})",
      "language": "javascript"
    },
    {
      "code": "        let chatSession: ChatSession\n\t\t\t\tlet messageMetadata: MessageMetadata = [\n            \"ex-key-1\": \"some-string\",\n            \"ex-key-2\": 1\n        ]\n\n\t\t\t\tchatSession.sendMessage(\n            NewChatMessage(\n                text: \"my message\",\n                messageMetadata: messageMetadata\n            )\n        ) { result in\n            switch result {\n            case .success(let chatMessage):\n              \tprint(chatMessage.messageMetadata)\n             \t\t// Do something with chat message\n            case .failure(let error):\n                // Something went wrong\n            }\n        }",
      "language": "swift"
    },
    {
      "code": "val messageMetadataMap = mutableMapOf<String, Any?>()\nmessageMetadataMap[\"Name\"] = \"Test\"\n\n// send message\nchatSession.sendMessage(\n    message,\n    messageMetadata = messageMetadataMap,\n    liveLikePreCallback = callback\n)",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Reading Message Metadata on messages"
}
[/block]
Each chat message has a Message Metadata property. Read more on reading messages here:

[iOS Receiving Messages](https://docs.livelike.com/docs/ios-chat-session#sending-and-receiving-messages)
[Android Receiving Messages](https://docs.livelike.com/docs/chat-session-1#sending-and-receiving-messages)
[Web Receiving Messages](https://docs.livelike.com/docs/chat-api-methods#addmessagelistener)