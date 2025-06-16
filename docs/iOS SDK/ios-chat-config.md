---
title: Chat Session
excerpt: >-
  A guide on how to get started with connecting to and interacting with Chat
  Rooms
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "warning",
  "title": "THIS PAGE HAS MOVED",
  "body": "See [Chat Session](doc:chat-session)"
}
[/block]
The ChatSession is your interface for viewing and interacting with a Chat Room.
[block:api-header]
{
  "title": "Creating a Chat Room"
}
[/block]
To create a Chat Room, use the `sdk.createChatRoom(title: String?, visibility: ChatRoomVisibilty, completion: (Result<String, Error>) -> Void)` method on your `EngagementSDK` instance. As a result you will receive a `String` which will represent the newly created Chat Room's Id or an `Error` object if creation of a new Chat Room fails.
[block:callout]
{
  "type": "info",
  "title": "Chat Room Visibility",
  "body": "A chat room visibility represents its exposure to users. At the moment a chat room can be public (`.everyone`) or exclusive to members (`.members`). Future work is planned to expand on this functionality further and more states will be added to the `ChatRoomVisibilty` enum."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  let chatSession: ChatSession?\n  \n  func someMethod(){\n    sdk.createChatRoom(title:\"New Room\", visibility: .everyone) { result in\n        switch result {\n        case let .success(chatRoomID):\n            print(\"New Room Created \\(chatRoomID)\")\n        case let .failure(error):\n            print(\"Failed creating a room \\(error)\")\n        }\n     }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]
In addition, you can use our backend API to create a chat room, see https://docs.livelike.com/v1/reference#create-chat-room
[block:api-header]
{
  "title": "Getting Chat Room Info"
}
[/block]
Information on a chat room can be retrieved by simply calling the `getChatRoomInfoBy(id: String, completion: (Result<ChatRoomInfo, Error>) -> Void)` function. 
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  let chatSession: ChatSession?\n  \n  func someMethod(){\n    sdk.getChatRoomInfoBy(id: \"<chat room id>\") { result in\n      switch result {\n      case let .success(chatInfo):\n          print(\"Chat Room Title: \\(chatInfo.title ?? \"No Title\")\")\n      case let .failure(error):\n          log.dev(\"Error: \\(error.localizedDescription)\")\n      }\n    }\n\t}\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Connect to a Chat Room"
}
[/block]
Connecting to a chat room creates a ChatSession object which represents the connection. While this object exists the chatSession will remain connected.

You can connect to multiple chat rooms at any given time.
[block:code]
{
  "codes": [
    {
      "code": "\n\nclass SomeClass {\n  let sdk: EngagementSDK\n  let chatSession: ChatSession?\n  \n  func someMethod(){\n    let config = ChatSessionConfig(roomID: \"<chat-room-id>\")\n    sdk.connectChatRoom(config: config) { [weak self] result in\n      guard let self = self else { return }                                    \n    \tswitch result {\n        case .success(let chatSession):\n        \tself.chatSession = chatSession\n        case .failure(let error):\n        \t// handle error\n      }\n    }\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]
Full list of ChatSessionConfig options <link to api reference>
[block:api-header]
{
  "title": "Chat Sessions with ChatViewController"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let chatSession: ChatSession?\n  let chatViewController: ChatViewController\n  \n  func someClass() {\n    // Sets the chat session to be displayed\n    chatViewController.setChatSession(chatSession)\n    \n    // Clears the current chat session if any is set\n    chatViewController.clearChatSession()\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Subscribing to Chat Room Messages"
}
[/block]
You can subscribe to a chat room's message stream to build supplemental features for the chat experience like an unread message count feature.

First you should implement the ChatSessionDelegate and the chatSession(chatSession:didRecieveNewMessage:) method. This is where you'll receive the new messages for the chat rooms that have been subscribed to.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass: ChatSessionDelegate {\n  let chatSession: ChatSession\n  \n  func someMethod(){\n    chatSession.delegate = self\n  }\n  \n  func chatSession(_ chatSession: ChatSession, didRecieveNewMessage message: ChatMessage) {\n    // Do something with the new message\n  }\n\t\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting Chat Room Messages from History"
}
[/block]
You can request (up to) 100 messages from a chat rooms history since a given timestamp with the getLatestChatMessages method. Alternatively, you can just request the count of messages using the getChatMessageCount method.
[block:callout]
{
  "type": "warning",
  "body": "These methods are not optimized for polling so avoid calling these methods on a timer or loop."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let chatSession: ChatSession\n  \n  func someMethod() {\n    let fiveMinutesAgo: Date = Date().addingTimeInterval(5 * 60)\n    chatSession.getMessages(\n      since: TimeToken(date: fiveMinutesAgo),\n      completion: { result in\n      \tswitch result {\n          case .success(let messages):\n          \t// do something with messages\n          case .failure(let error):\n          \t// handle error\n        }\n    })\n    \n    chatSession.getMessageCount(\n      since: TimeToken(date: fiveMinutesAgo),\n      completion: { result in\n      \tswitch result {\n          case .success(let messageCount):\n          \t// do something with message count\n          case .failure(let error):\n          \t// handle error\n        }\n    })\n    \n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Chat User Muting"
}
[/block]
Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in. As an integrator you have the option to query our backend to find out whether a user is muted or not. This can be achieved using the `getChatUserMutedStatus(roomID: String, completion: @escaping (Result<ChatUserMuteStatus, Error>) -> Void)` SDK interface.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  \n  func someMethod(){\n    let config = ChatSessionConfig(roomID: \"<chat-room-id>\")\n    sdk.connectChatRoom(config: config) { [weak self] result in\n      guard let self = self else { return }                                    \n    \tswitch result {\n        case .success(let chatSession):\n        \tself.sdk.getChatUserMutedStatus(roomID: chatSession.roomID) { result in\n                        switch result {\n                        case let .success(mutedStatus):\n                            if mutedStatus.isMuted {\n                                // user is muted\n                            }\n                        case let .failure(error):\n                            log.dev(\"error getting muted status \\(error.localizedDescription)\")\n                        }\n                    }\n        case .failure(let error):\n        \t// handle error\n      }\n    }\n  }\n}",
      "language": "swift",
      "name": "ChatSession"
    },
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  var session: ContentSession\n  \n  func someMethod(){\n    let config = SessionConfiguration(programID: programID)\n    session = sdk.contentSession(config: config)\n    \n    session.getChatSession(completion: { [weak self] result in\n            guard let self = self else { return }\n            switch result {\n            case let .success(chatroom):\n                self.sdk.getChatUserMutedStatus(roomID: chatroom.roomID) { result in\n                    switch result {\n                    case let .success(mutedStatus):\n                        if mutedStatus.isMuted {\n                          // user is muted\n                        }\n                    case let .failure(error):\n                        log.dev(\"error getting muted status \\(error.localizedDescription)\")\n                    }\n                }\n            case let .failure(error):\n                log.dev(\"error getting muted status \\(error.localizedDescription)\")\n            }\n        })\n  }\n}",
      "language": "swift",
      "name": "ContentSession"
    }
  ]
}
[/block]
Whether you decide to make the user aware of their status or not, the SDK will show an alert to a muted user once they try to send a message in a room. For more information about chat moderation please see the [Chat Moderation](https://docs.livelike.com/docs/chat#moderation) page.