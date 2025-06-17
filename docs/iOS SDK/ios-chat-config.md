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
> 🚧 THIS PAGE HAS MOVED
>
> See [Chat Session](doc:chat-session)

The ChatSession is your interface for viewing and interacting with a Chat Room.

## Creating a Chat Room

To create a Chat Room, use the `sdk.createChatRoom(title: String?, visibility: ChatRoomVisibilty, completion: (Result<String, Error>) -> Void)` method on your `EngagementSDK` instance. As a result you will receive a `String` which will represent the newly created Chat Room's Id or an `Error` object if creation of a new Chat Room fails.

> 📘 Chat Room Visibility
>
> A chat room visibility represents its exposure to users. At the moment a chat room can be public (`.everyone`) or exclusive to members (`.members`). Future work is planned to expand on this functionality further and more states will be added to the `ChatRoomVisibilty` enum.

```swift
class SomeClass {
  let sdk: EngagementSDK
  let chatSession: ChatSession?
  
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

## Getting Chat Room Info

Information on a chat room can be retrieved by simply calling the `getChatRoomInfoBy(id: String, completion: (Result<ChatRoomInfo, Error>) -> Void)` function. 

```swift
class SomeClass {
  let sdk: EngagementSDK
  let chatSession: ChatSession?
  
  func someMethod(){
    sdk.getChatRoomInfoBy(id: "<chat room id>") { result in
      switch result {
      case let .success(chatInfo):
          print("Chat Room Title: \(chatInfo.title ?? "No Title")")
      case let .failure(error):
          log.dev("Error: \(error.localizedDescription)")
      }
    }
	}
}
```

## Connect to a Chat Room

Connecting to a chat room creates a ChatSession object which represents the connection. While this object exists the chatSession will remain connected.

You can connect to multiple chat rooms at any given time.

```swift
class SomeClass {
  let sdk: EngagementSDK
  let chatSession: ChatSession?
  
  func someMethod(){
    let config = ChatSessionConfig(roomID: "<chat-room-id>")
    sdk.connectChatRoom(config: config) { [weak self] result in
      guard let self = self else { return }                                    
    	switch result {
        case .success(let chatSession):
        	self.chatSession = chatSession
        case .failure(let error):
        	// handle error
      }
    }
  }
}
```

Full list of ChatSessionConfig options \<link to api reference>

## Chat Sessions with ChatViewController

```swift
class SomeClass {
  let chatSession: ChatSession?
  let chatViewController: ChatViewController
  
  func someClass() {
    // Sets the chat session to be displayed
    chatViewController.setChatSession(chatSession)
    
    // Clears the current chat session if any is set
    chatViewController.clearChatSession()
  }
}
```

## Subscribing to Chat Room Messages

You can subscribe to a chat room's message stream to build supplemental features for the chat experience like an unread message count feature.

First you should implement the ChatSessionDelegate and the chatSession(chatSession:didRecieveNewMessage:) method. This is where you'll receive the new messages for the chat rooms that have been subscribed to.

```swift
class SomeClass: ChatSessionDelegate {
  let chatSession: ChatSession
  
  func someMethod(){
    chatSession.delegate = self
  }
  
  func chatSession(_ chatSession: ChatSession, didRecieveNewMessage message: ChatMessage) {
    // Do something with the new message
  }
	
}
```

## Getting Chat Room Messages from History

You can request (up to) 100 messages from a chat rooms history since a given timestamp with the getLatestChatMessages method. Alternatively, you can just request the count of messages using the getChatMessageCount method.

> 🚧 These methods are not optimized for polling so avoid calling these methods on a timer or loop.

```swift
class SomeClass {
  let chatSession: ChatSession
  
  func someMethod() {
    let fiveMinutesAgo: Date = Date().addingTimeInterval(5 * 60)
    chatSession.getMessages(
      since: TimeToken(date: fiveMinutesAgo),
      completion: { result in
      	switch result {
          case .success(let messages):
          	// do something with messages
          case .failure(let error):
          	// handle error
        }
    })
    
    chatSession.getMessageCount(
      since: TimeToken(date: fiveMinutesAgo),
      completion: { result in
      	switch result {
          case .success(let messageCount):
          	// do something with message count
          case .failure(let error):
          	// handle error
        }
    })
    
  }
}
```

## Chat User Muting

Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in. As an integrator you have the option to query our backend to find out whether a user is muted or not. This can be achieved using the `getChatUserMutedStatus(roomID: String, completion: @escaping (Result<ChatUserMuteStatus, Error>) -> Void)` SDK interface.

```swift ChatSession
class SomeClass {
  let sdk: EngagementSDK
  
  func someMethod(){
    let config = ChatSessionConfig(roomID: "<chat-room-id>")
    sdk.connectChatRoom(config: config) { [weak self] result in
      guard let self = self else { return }                                    
    	switch result {
        case .success(let chatSession):
        	self.sdk.getChatUserMutedStatus(roomID: chatSession.roomID) { result in
                        switch result {
                        case let .success(mutedStatus):
                            if mutedStatus.isMuted {
                                // user is muted
                            }
                        case let .failure(error):
                            log.dev("error getting muted status \(error.localizedDescription)")
                        }
                    }
        case .failure(let error):
        	// handle error
      }
    }
  }
}
```
```swift ContentSession
class SomeClass {
  let sdk: EngagementSDK
  var session: ContentSession
  
  func someMethod(){
    let config = SessionConfiguration(programID: programID)
    session = sdk.contentSession(config: config)
    
    session.getChatSession(completion: { [weak self] result in
            guard let self = self else { return }
            switch result {
            case let .success(chatroom):
                self.sdk.getChatUserMutedStatus(roomID: chatroom.roomID) { result in
                    switch result {
                    case let .success(mutedStatus):
                        if mutedStatus.isMuted {
                          // user is muted
                        }
                    case let .failure(error):
                        log.dev("error getting muted status \(error.localizedDescription)")
                    }
                }
            case let .failure(error):
                log.dev("error getting muted status \(error.localizedDescription)")
            }
        })
  }
}
```

Whether you decide to make the user aware of their status or not, the SDK will show an alert to a muted user once they try to send a message in a room. For more information about chat moderation please see the [Chat Moderation](https://docs.livelike.com/docs/chat#moderation) page.