---
title: Pinning Chat Messages
deprecated: false
hidden: false
metadata:
  robots: index
---
In Order to show or pin some important message in chat, users can use these APIs. The APIs allow users to pin messages with real-time listeners to all the chatroom listeners.

> 📘 Note
>
> Only the Producer or creators of the chatroom are allowed to pin messages.
> These are access control through backend API's so can be controlled/managed easily.

## Pin Message

The function **pinMessage** allows the producer or the creator of the chatroom to choose which message to focus on. The parameters of the function are **messageID**, **chatRoomID** and **chatMessage**. On successful completion, the function returns an object of type **PinMessageInfo**

> 📘 What is PinMessageInfo?
>
> `PinMessageInfo` is an object which contains information related to pin messages like `roomId`, `messageId`, `pinById` etc. For doing any operation on pinned message, you may require the pinMessageInfo id (through `getPinMessageInfoList` API)

<br />

<details>
  <summary>Pin Message in Chat</summary>

  ```kotlin
  // requires an instance of LiveLikeChatMessage, 
  // returns an instance of pinMessageInfo or error string.
   sdk.chat().pinMessage(
     messageId = chatMessage.id!!,
     chatRoomId = chatRoomId!!,
     chatMessagePayload = chatMessage,
     liveLikeCallback = object: LiveLikeCallback < PinMessageInfo > () {
       override fun onResponse(result: PinMessageInfo ? , error : String ? ) {
         error?.let {}
         result?.let {
           messageInfo ->
         }
       }
     }
   )
  ```
  ```javascript
  LiveLike.pinMessage({
          roomId: "9e6f1bc4-9f02-4c57-92b7-7521d0f5b027",
          messageId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
          messagePayload: { // messagePayload of type IMessagePayload
          message: "test Message"
      }
  }).then(pinMessageInfo => console.log(pinMessageInfo))
  ```
  ```swift
  //pinMessage(_ message: ChatMessage) is a part of the chatSession of a particular Chat Room
  //It requires an object of the chat message to be passed as a parameter to the API

  chatSession.pinMessage(message) { result in
  	switch result {
    	case .failure(let error):
      	//Returns an error
      case .success(let pinMessage):
      	//Returns an object of type PinMessageInfo
      }
  }
  ```
</details>

## Unpin Message

To Unpin a message use **unpinMessage** API which requires id of PinMessageInfo object and in returns it provide success or error message string.

<details>
  <summary>Unpin Message in Chat</summary>

  ```kotlin
  sdk.chat().unPinMessage(pinMessageInfoId = pinnedList[index].id!!,
    liveLiveLikeCallback = object: LiveLikeCallback < LiveLikeEmptyResponse > () {
      override fun onResponse(result: LiveLikeEmptyResponse ? , error : String ? ) {
        error?.let {}
        result?.let {}
      }
    }
  )
  ```
  ```javascript
  const pinMessageInfoId = "3f81ccb0-ec95-4e71-a0b7-462889699f75";

  LiveLike.unpinMessage({
      pinMessageInfoId: pinMessageInfoId
  }).then(res => {
    // success res is no content, err response would contain error details.
    console.log(res)
  })
  ```
  ```swift
  chatSession.unpinMessage(pinMessageInfoID: messageID) { result in
  		switch result {
      		case .success:
          	//Successfully Unpinned Message
          case .failure(let error):
          	//Returns error
  		}
  }
  ```
</details>

## List Of Pin Messages

To get the list of pin messages, use **getPinMessageInfoList** which requires **ChatRoomID** and **orderBy** and returns list of pin message info or error message string.

> 📘 Ordering of List of PinMessageInfo
>
> The API **getPinMessageInfoList** accepts a parameter **orderBy** which lets you choose if the list should be received in ascending ( **asc** ) or descending ( **desc** ) order.

<br />

<details>
  <summary>Get PinMessage Info List</summary>

  ```kotlin
  // Also requires instance of LiveLikePagination and instance of PinMessageOrder 
  sdk?.chat()?.getPinMessageInfoList(
    chatRoomId!!,
    LiveLikeOrdering.ASC,
    LiveLikePagination.FIRST,
    object: LiveLikeCallback < List < PinMessageInfo >> () {
      override fun onResponse(result: List < PinMessageInfo > ? , error : String ? ) {
        result?.let {}
        error?.let {}
      }
    }
  )
  ```
  ```javascript
  LiveLike.getPinMessageInfoList({
      roomId: "37e1720a-fc7b-4962-b216-6be9ed69dc96",
      orderBy: "desc" // order by pinned time, optional prop, could be "asc" | "desc"
  }).then(paginatedPinMessageInfoList => console.log(paginatedPinMessageInfoList))
  ```
  ```swift
  chatSession.getPinMessageInfoList(orderBy: .asc, page: .first) { result in
  	switch result {
  	case .success(let pinMessages):
      //Returns a list of pinMessages based on pagination
    case .failure(let error):
    	//Returns an error to handle  
    }
  }
  ```
</details>

## Real Time Events for Pin/Unpin Message

In order to receive real-time events for pin/unpin messages, add listeners/delegates.

> 📘 Platform specific implementation
>
> Implementation for receiving real time events is different for Web, Android and IOS.

<details>
  <summary>Pin/Unpin Message</summary>

  ```kotlin
  chatSession.setMessageListener(object: MessageListener {
    private val TAG = "LiveLike"
    override fun onNewMessage(message: LiveLikeChatMessage) {

    }

    override fun onHistoryMessage(messages: List < LiveLikeChatMessage > ) {

    }

    override fun onDeleteMessage(messageId: String) {

    }

    override fun onPinMessage(message: PinMessageInfo) {
      activity?.runOnUiThread {
        // use ui thread to work on any UI element here
      }

    }

    override fun onUnPinMessage(pinMessageId: String) {
      activity?.runOnUiThread {
        // id of the pinMessageInfo class
      }
    }
  })
  ```
  ```javascript
  // For getting real time pin message event with the pinMessageInfo
  function onReceivedPinMessageListener (pinMessageInfoEvent) { 
      console.log(pinMessageInfoEvent)
  }
  LiveLike.addChatRoomEventListener(
      LiveLike.ChatRoomEvent.PIN_MESSAGE,
      onReceivedPinMessageListener,
      { roomId: "695ea6f4-fe7b-47cc-817c-2d73fdba264a" }
  );

  // For removing pin message listener
  LiveLike.removeChatRoomEventListener(
      LiveLike.ChatRoomEvent.PIN_MESSAGE,
      onReceivedPinMessageListener,
      { roomId: "695ea6f4-fe7b-47cc-817c-2d73fdba264a" }
  );



  // For getting real time unpin message event with unpin message info id
  function onReceivedUnpinMessageListener (unpinEventMessage) { 
      console.log(unpinEventMessage)
  }
  LiveLike.addChatRoomEventListener(
      LiveLike.ChatRoomEvent.UNPIN_MESSAGE,
      onReceivedUnpinMessageListener,
      { roomId: "695ea6f4-fe7b-47cc-817c-2d73fdba264a" }
  );

  // For removing unpin message listener
  LiveLike.removeChatRoomEventListener(
      LiveLike.ChatRoomEvent.UNPIN_MESSAGE,
      onReceivedUnpinMessageListener,
      { roomId: "695ea6f4-fe7b-47cc-817c-2d73fdba264a" }
  );
  ```
</details>
