---
title: Pinning Chat Messages
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Pin Messages | LiveLike Developer Hub
  description: >-
    Users can use APIs to show or pin important messages in a chat. These APIs
    allow users to pin messages and unpin messages in real time.
  robots: index
next:
  description: ''
---
In Order to show or pin some important message in chat, users can use these APIs. The APIs allow users to pin messages with real-time listeners to all the chatroom listeners.

[block:callout]
{
  "type": "info",
  "title": "Note",
  "body": "Only the Producer or creators of the chatroom are allowed to pin messages.\nThese are access control through backend API's so can be controlled/managed easily."
}
[/block]

[block:api-header]
{
  "title": "Pin Message"
}
[/block]
The function **pinMessage** allows the producer or the creator of the chatroom to choose which message to focus on. The parameters of the function are **messageID**, **chatRoomID** and **chatMessage**. On successful completion, the function returns an object of type **PinMessageInfo**
[block:callout]
{
  "type": "info",
  "title": "What is PinMessageInfo?",
  "body": "`PinMessageInfo` is an object which contains information related to pin messages like `roomId`, `messageId`, `pinById` etc. For doing any operation on pinned message, you may require the pinMessageInfo id (through `getPinMessageInfoList` API)"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "// requires an instance of LiveLikeChatMessage, \n// returns an instance of pinMessageInfo or error string.\n sdk.chat().pinMessage(\n   messageId = chatMessage.id!!,\n   chatRoomId = chatRoomId!!,\n   chatMessagePayload = chatMessage,\n   liveLikeCallback = object: LiveLikeCallback < PinMessageInfo > () {\n     override fun onResponse(result: PinMessageInfo ? , error : String ? ) {\n       error?.let {}\n       result?.let {\n         messageInfo ->\n       }\n     }\n   }\n )",
      "language": "kotlin"
    },
    {
      "code": " LiveLike.pinMessage({\n        roomId: \"9e6f1bc4-9f02-4c57-92b7-7521d0f5b027\",\n        messageId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n        messagePayload: { // messagePayload of type IMessagePayload\n        message: \"test Message\"\n    }\n}).then(pinMessageInfo => console.log(pinMessageInfo))",
      "language": "javascript"
    },
    {
      "code": "//pinMessage(_ message: ChatMessage) is a part of the chatSession of a particular Chat Room\n//It requires an object of the chat message to be passed as a parameter to the API\n\nchatSession.pinMessage(message) { result in\n\tswitch result {\n  \tcase .failure(let error):\n    \t//Returns an error\n    case .success(let pinMessage):\n    \t//Returns an object of type PinMessageInfo\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Unpin Message"
}
[/block]
To Unpin a message use **unpinMessage** API which requires id of PinMessageInfo object and in returns it provide success or error message string.
[block:code]
{
  "codes": [
    {
      "code": "sdk.chat().unPinMessage(pinMessageInfoId = pinnedList[index].id!!,\n  liveLiveLikeCallback = object: LiveLikeCallback < LiveLikeEmptyResponse > () {\n    override fun onResponse(result: LiveLikeEmptyResponse ? , error : String ? ) {\n      error?.let {}\n      result?.let {}\n    }\n  }\n)",
      "language": "kotlin"
    },
    {
      "code": "const pinMessageInfoId = \"3f81ccb0-ec95-4e71-a0b7-462889699f75\";\n\nLiveLike.unpinMessage({\n    pinMessageInfoId: pinMessageInfoId\n}).then(res => {\n  // success res is no content, err response would contain error details.\n  console.log(res)\n}) ",
      "language": "javascript"
    },
    {
      "code": "chatSession.unpinMessage(pinMessageInfoID: messageID) { result in\n\t\tswitch result {\n    \t\tcase .success:\n        \t//Successfully Unpinned Message\n        case .failure(let error):\n        \t//Returns error\n\t\t}\n}         ",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "List Of Pin Messages"
}
[/block]
To get the list of pin messages, use **getPinMessageInfoList** which requires **ChatRoomID** and **orderBy** and returns list of pin message info or error message string.
[block:callout]
{
  "type": "info",
  "title": "Ordering of List of PinMessageInfo",
  "body": "The API **getPinMessageInfoList** accepts a parameter **orderBy** which lets you choose if the list should be received in ascending ( **asc** ) or descending ( **desc** ) order."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "// Also requires instance of LiveLikePagination and instance of PinMessageOrder \nsdk?.chat()?.getPinMessageInfoList(\n  chatRoomId!!,\n  LiveLikeOrdering.ASC,\n  LiveLikePagination.FIRST,\n  object: LiveLikeCallback < List < PinMessageInfo >> () {\n    override fun onResponse(result: List < PinMessageInfo > ? , error : String ? ) {\n      result?.let {}\n      error?.let {}\n    }\n  }\n)",
      "language": "kotlin"
    },
    {
      "code": "LiveLike.getPinMessageInfoList({\n    roomId: \"37e1720a-fc7b-4962-b216-6be9ed69dc96\",\n    orderBy: \"desc\" // order by pinned time, optional prop, could be \"asc\" | \"desc\"\n}).then(paginatedPinMessageInfoList => console.log(paginatedPinMessageInfoList))",
      "language": "javascript"
    },
    {
      "code": "chatSession.getPinMessageInfoList(orderBy: .asc, page: .first) { result in\n\tswitch result {\n\tcase .success(let pinMessages):\n    //Returns a list of pinMessages based on pagination\n  case .failure(let error):\n  \t//Returns an error to handle  \n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Real Time Events for Pin/Unpin Message"
}
[/block]
In order to receive real-time events for pin/unpin messages, add listeners/delegates.
[block:callout]
{
  "type": "info",
  "title": "Platform specific implementation",
  "body": "Implementation for receiving real time events is different for Web, Android and IOS."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "chatSession.setMessageListener(object: MessageListener {\n  private val TAG = \"LiveLike\"\n  override fun onNewMessage(message: LiveLikeChatMessage) {\n\n  }\n\n  override fun onHistoryMessage(messages: List < LiveLikeChatMessage > ) {\n\n  }\n\n  override fun onDeleteMessage(messageId: String) {\n\n  }\n\n  override fun onPinMessage(message: PinMessageInfo) {\n    activity?.runOnUiThread {\n      // use ui thread to work on any UI element here\n    }\n\n  }\n\n  override fun onUnPinMessage(pinMessageId: String) {\n    activity?.runOnUiThread {\n      // id of the pinMessageInfo class\n    }\n  }\n})",
      "language": "kotlin"
    },
    {
      "code": "// For getting real time pin message event with the pinMessageInfo\nfunction onReceivedPinMessageListener (pinMessageInfoEvent) { \n    console.log(pinMessageInfoEvent)\n}\nLiveLike.addChatRoomEventListener(\n    LiveLike.ChatRoomEvent.PIN_MESSAGE,\n    onReceivedPinMessageListener,\n    { roomId: \"695ea6f4-fe7b-47cc-817c-2d73fdba264a\" }\n);\n\n// For removing pin message listener\nLiveLike.removeChatRoomEventListener(\n    LiveLike.ChatRoomEvent.PIN_MESSAGE,\n    onReceivedPinMessageListener,\n    { roomId: \"695ea6f4-fe7b-47cc-817c-2d73fdba264a\" }\n);\n\n\n\n// For getting real time unpin message event with unpin message info id\nfunction onReceivedUnpinMessageListener (unpinEventMessage) { \n    console.log(unpinEventMessage)\n}\nLiveLike.addChatRoomEventListener(\n    LiveLike.ChatRoomEvent.UNPIN_MESSAGE,\n    onReceivedUnpinMessageListener,\n    { roomId: \"695ea6f4-fe7b-47cc-817c-2d73fdba264a\" }\n);\n\n// For removing unpin message listener\nLiveLike.removeChatRoomEventListener(\n    LiveLike.ChatRoomEvent.UNPIN_MESSAGE,\n    onReceivedUnpinMessageListener,\n    { roomId: \"695ea6f4-fe7b-47cc-817c-2d73fdba264a\" }\n);",
      "language": "javascript"
    }
  ]
}
[/block]