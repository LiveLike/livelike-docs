---
title: useChatRoom
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
      slug: usechatmessages
      title: useChatMessages
---
The purpose of `useChatRoom` hook is to fetch and expose the chatroom resources

##### Example usage
[block:code]
{
  "codes": [
    {
      "code": "const { chatRoom } = useChatRoom({ roomId: \"<Room ID>\" });",
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
#### `chatRoom`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[IChatRoomPayload](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IChatRoomPayload)",
    "0-1": "null"
  },
  "cols": 2,
  "rows": 1
}
[/block]