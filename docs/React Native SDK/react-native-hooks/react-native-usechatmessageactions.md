---
title: useChatMessageActions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: usechatmessageseffect
      title: useChatMessagesEffect
---
The purpose of `useChatMessageActions` hook is to abstract out our store actions and exposes actions handlers responsible for updating store value. 

##### Example usage
[block:code]
{
  "codes": [
    {
      "code": "const { sendChatMessage, deleteChatMessage } = useChatMessageActions({ \n  roomId: \"<Room ID>\" \n});",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hook Argument"
}
[/block]
#### `roomId`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String (**Required**)",
    "0-1": "No Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]

[block:api-header]
{
  "title": "Hook Return Value"
}
[/block]
#### `sendChatMessage`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "",
    "0-0": "Function of type: (messageArgs: [ISendMessageArgs](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=ISendMessageArgs)) => Promise<void>"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `deleteChatMessage`
[block:parameters]
{
  "data": {
    "0-0": "Function of type:\n({ roomId, chatMessage }: {\n    roomId: any;\n    chatMessage: any;\n}) => void",
    "0-1": "",
    "h-0": "Type",
    "h-1": "Default"
  },
  "cols": 1,
  "rows": 1
}
[/block]