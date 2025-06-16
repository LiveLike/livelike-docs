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
[block:api-header]
{
  "title": "Creating a Chat Room"
}
[/block]
To create a Chat Room, use the `sdk.createChatRoom(title: String?, visibility: ChatRoomVisibilty, completion: (Result<String, Error>) -> Void)` method on your `EngagementSDK` instance. As a result you will receive a `String` which will represent the newly created Chat Room's Id or an `Error` object if creation of a new Chat Room fails.
[block:callout]
{
  "type": "info",
  "body": "A chat room visibility represents its exposure to users. At the moment a chat room can be public (`.everyone`) or exclusive to members (`.members`). Future work is planned to expand on this functionality further and more states will be added to the `ChatRoomVisibilty` enum.",
  "title": "Chat Room Visibility"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  \n  func someMethod(){\n    sdk.createChatRoom(title:\"New Room\", visibility: .everyone) { result in\n        switch result {\n        case let .success(chatRoomID):\n            print(\"New Room Created \\(chatRoomID)\")\n        case let .failure(error):\n            print(\"Failed creating a room \\(error)\")\n        }\n     }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]
In addition, you can use our backend API to create a chat room, see https://docs.livelike.com/v1/reference#create-chat-room
[block:api-header]
{
  "title": "Getting Chat Room Information"
}
[/block]
Information on a chat room can be retrieved by simply calling the `getChatRoomInfoBy(id: String, completion: (Result<ChatRoomInfo, Error>) -> Void)` function. 
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  \n  func someMethod(){\n    sdk.getChatRoomInfo(roomID: \"<chat room id>\") { result in\n      switch result {\n      case let .success(chatInfo):\n          print(\"Chat Room Title: \\(chatInfo.title ?? \"No Title\")\")\n      case let .failure(error):\n          print(\"Error: \\(error.localizedDescription)\")\n      }\n    }\n\t}\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Managing Chat Room Users"
}
[/block]
See [Chat Room Membership](doc:ios-chat-room-membership)
[block:api-header]
{
  "title": "Check User Mute Status"
}
[/block]
Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in. As an integrator you have the option to query our backend to find out whether a user is muted or not. This can be achieved using the `getChatUserMutedStatus(roomID: String, completion: @escaping (Result<ChatUserMuteStatus, Error>) -> Void)` SDK interface.
[block:code]
{
  "codes": [
    {
      "code": "let sdk: EngagementSDK\n\nsdk.getChatUserMutedStatus(roomID: \"<chat-room-id>\") { result in\n  switch result {\n  case let .success(mutedStatus):\n    if mutedStatus.isMuted {\n      // user is muted\n    }\n  case let .failure(error):\n    // handle error\n  }\n}",
      "language": "swift",
      "name": null
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Changing User's Nickname"
}
[/block]
See [User Profiles](doc:ios-user-profiles)