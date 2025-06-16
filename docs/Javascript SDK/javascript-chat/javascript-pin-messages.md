---
title: Pin Messages
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
      slug: javascript-stickers
      title: Stickers
---
In Order to show or pin some important message in chat, users can use these APIs. The APIs allow users to pin messages with real-time listeners to all the chatroom listeners.

> 🚧 Note
> 
> Only the Producer or creators of the chatroom are allowed to pin messages.  
> These are access control through backend API's so can be controlled/managed easily.

## Pin Message

`pinMessage`  API allows the producer or the creator of the chatroom to choose which message to pin. The parameters of the function are **messageID**, **roomId** and **messagePayload**. On successful completion, the function returns an object of type **PinMessageInfo**

**API Definition**: [pinMessage](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=pinMessage) 

> 📘 What is PinMessageInfo?
> 
> `PinMessageInfo` is an object which contains information related to pin messages like `roomId`, `messageId`, `pinById` etc. For doing any operation on pinned message, you may require the pinMessageInfo id (that could be fetched using `getPinMessageInfoList` API)

```javascript
import { pinMessage } from "@livelike/javascript"

pinMessage({
  roomId: "9e6f1bc4-9f02-4c57-92b7-7521d0f5b027",
  messageId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
  messagePayload: { 
    // messagePayload of type IMessagePayload
    message: "test Message"
  }
}).then(pinMessageInfo => console.log(pinMessageInfo))
```



## Unpin Message

To Unpin a message use **unpinMessage** API which requires id of PinMessageInfo object and in returns it provide success or error message string.

**API Definition**: [unpinMessage](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=unpinMessage)

```javascript
import { unpinMessage } from "@livelike/javascript"

const pinMessageInfoId = "3f81ccb0-ec95-4e71-a0b7-462889699f75";

unpinMessage({
  pinMessageInfoId: pinMessageInfoId
}).then(res => {
  // success res is no content, err response would contain error details.
  console.log(res)
})
```



## List Of Pin Messages

To get the list of pin messages, use **getPinMessageInfoList** API which requires **roomId** and optional **orderBy** that returns list of pin message info.

**API Definition**: [getPinMessageInfoList](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getPinMessageInfoList)

> 📘 Ordering of List of PinMessageInfo
> 
> `getPinMessageInfoList` accepts a parameter **orderBy** which lets you choose if the list should be received in ascending ( **asc** ) or descending ( **desc** ) order.

```javascript
import { getPinMessageInfoList } from "@livelike/javascript"

getPinMessageInfoList({
  roomId: "37e1720a-fc7b-4962-b216-6be9ed69dc96",
  orderBy: "desc" // order by pinned time, optional prop with values "asc" | "desc"
}).then(paginatedPinMessageInfoList => console.log(paginatedPinMessageInfoList))
```



## Add event listener for Pin Message

Use `addChatRoomEventListener` API with `ChatRoomEvent.PIN_MESSAGE` event for adding listener function that gets called whenever a message is pinned.

**API Definition**: [addChatRoomEventListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addChatRoomEventListener)

```javascript
import { addChatRoomEventListener, ChatRoomEvent } from "@livelike/javascript"

function onReceivedPinMessageListener(pinMessageInfoEvent) {
  console.log(pinMessageInfoEvent);
}

addChatRoomEventListener(
  ChatRoomEvent.PIN_MESSAGE,
  onReceivedPinMessageListener,
  { roomId: "<Chat Room ID>" }
)
```



Similarly use `removeChatRoomEventListener` API to remove a added listener function

```javascript
import { removeChatRoomEventListener, ChatRoomEvent } from "@livelike/javascript"

removeChatRoomEventListener(
  ChatRoomEvent.PIN_MESSAGE,
  onReceivedPinMessageListener,
  { roomId: "<Chat Room ID>" }
)
```



## Add event listener for Unpin Message

Use `addChatRoomEventListener` API with `ChatRoomEvent.UNPIN_MESSAGE` event for adding listener function that gets called whenever a message is pinned.

**API Definition**: [addChatRoomEventListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addChatRoomEventListener)

```javascript
import { addChatRoomEventListener, ChatRoomEvent } from "@livelike/javascript"

function onReceivedPinMessageListener(pinMessageInfoEvent) {
  console.log(pinMessageInfoEvent);
}

addChatRoomEventListener(
  ChatRoomEvent.UNPIN_MESSAGE,
  onReceivedPinMessageListener,
  { roomId: "<Chat Room ID>" }
)
```



Similarly use `removeChatRoomEventListener` API to remove a added listener function

```javascript
import { removeChatRoomEventListener, ChatRoomEvent } from "@livelike/javascript"

removeChatRoomEventListener(
  ChatRoomEvent.UNPIN_MESSAGE,
  onReceivedPinMessageListener,
  { roomId: "<Chat Room ID>" }
)
```