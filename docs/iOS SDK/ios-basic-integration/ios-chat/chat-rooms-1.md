---
title: Chat Rooms
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Rooms | iOS SDK | LiveLike Developer Hub
  description: >-
    Creating a chat room allows your users to connect with fans around the world
    and boosts user engagement. Learn more about chat rooms.
  robots: index
next:
  description: ''
---
A guide for managing Chat Rooms

## Creating a Chat Room

To create a Chat Room, use the `sdk.createChatRoom(title: String?, visibility: ChatRoomVisibilty, completion: (Result<String, Error>) -> Void)` method on your `EngagementSDK` instance. As a result you will receive a `String` which will represent the newly created Chat Room's Id or an `Error` object if creation of a new Chat Room fails.

> 📘 Chat Room Visibility
>
> A chat room visibility represents its exposure to users. At the moment a chat room can be public (`.everyone`) or exclusive to members (`.members`). Future work is planned to expand on this functionality further and more states will be added to the `ChatRoomVisibilty` enum.

```swift
class SomeClass {
  let sdk: EngagementSDK
  
  func someMethod(){
    sdk.createChatRoom(title:"New Room", visibility: .everyone) { result in
        switch result {
        case let .success(chatRoomID):
            print("New Room Created \(chatRoomID)")
        case let .failure(error):
            print("Failed creating a room \(error)")
        }
     }
  }
}
```

In addition, you can use our backend API to create a chat room, see [https://docs.livelike.com/v1/reference#create-chat-room](https://docs.livelike.com/v1/reference#create-chat-room)

## Getting Chat Room Information

Information on a chat room can be retrieved by simply calling the `getChatRoomInfoBy(id: String, completion: (Result<ChatRoomInfo, Error>) -> Void)` function. 

```swift
class SomeClass {
  let sdk: EngagementSDK
  
  func someMethod(){
    sdk.getChatRoomInfo(roomID: "<chat room id>") { result in
      switch result {
      case let .success(chatInfo):
          print("Chat Room Title: \(chatInfo.title ?? "No Title")")
      case let .failure(error):
          print("Error: \(error.localizedDescription)")
      }
    }
	}
}
```

## Managing Chat Room Users

See [Chat Room Membership](doc:ios-chat-room-membership)

## Check User Mute Status

Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in. As an integrator you have the option to query our backend to find out whether a user is muted or not. This can be achieved using the `getChatUserMutedStatus(roomID: String, completion: @escaping (Result<ChatUserMuteStatus, Error>) -> Void)` SDK interface.

```swift
let sdk: EngagementSDK

sdk.getChatUserMutedStatus(roomID: "<chat-room-id>") { result in
  switch result {
  case let .success(mutedStatus):
    if mutedStatus.isMuted {
      // user is muted
    }
  case let .failure(error):
    // handle error
  }
}
```

## Changing User's Nickname

See [User Profiles](doc:ios-user-profiles)
