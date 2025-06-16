---
title: useChatMessagesEffect
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
      slug: react-native-usemessageitempopover
      title: useMessageItemPopover
---
The purpose of `useChatMessagesEffect` hook is set appropriate message listeners and using callbacks it makes [chat messages resource](https://docs.livelike.com/docs/react-native-usechatmessages) live and reactive

##### Example Usage: 
[block:code]
{
  "codes": [
    {
      "code": "useChatMessagesEffect({ roomId: \"<Room ID>\" });",
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
    "0-0": "String",
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
#### `removeMessageListener`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: (arg: [IChatRoomArgs](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IChatRoomArgs), callback: [MessageListenerCallback](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=MessageListenerCallback)) => Promise<void>"
  },
  "cols": 1,
  "rows": 1
}
[/block]