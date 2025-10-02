---
title: Chat Session
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
A Chat Session is your interface to interact with a chat room.

**Features**

* Message List
* Sending and Receiving Messages
* Message History

## Starting a Chat Session

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
        
        // if you choose to show the `ChatSession` to the user
        // you have to set it on the `ChatViewController`
        self.chatViewController.setChatSession(chatSession)
        
        case .failure(let error):
        	// handle error
      }
    }
  }
}
```

## Message List

The ChatSession maintains list of all messages currently loaded into memory. This list stores messages in ascending order of the time that the message was published (index 0 is the oldest message loaded). This list is readonly and managed by the SDK - messages that a sent, received, and loaded from history are automatically added to the list. 

List access by ID is recommended since the indices will change as messages are loaded from history.

## Sending and Receiving Messages

The core of any chat experience is sending and receiving messages. 

**Sending Messages**\
You send a message by creating a `NewChatMessage` instance and then passing it into the `sendMessage` method of the ChatSession. 

As a result you will receive a `ChatMessage` object representing the new message. 

```swift
let chatSession: ChatSession

// Send a text message
let textMessage = NewChatMessage(text: "")
chatSession.sendMessage(textMessage) { result in
  switch result {
  case .success(let newMessage):
    // the message was successfully sent
  case .failure(let error):
    // handle failures
  }
}

// Send an image message using image URL
let imageMessage = NewChatMessage(
  imageURL: URL(), 
  imageSize: CGSize(width: 100, height: 100)
)
chatSession.sendMessage(imageMessage) { result in
  switch result {
  case .success(let newMessage):
    // the message was successfully sent
  case .failure(let error):
    // handle failures
  }
}

// Send an image message using image URL
let imageDataMessage = NewChatMessage(
  imageData: Data(), 
  imageSize: CGSize(width: 100, height: 100)
)
chatSession.sendMessage(imageDataMessage) { result in
  switch result {
  case .success(let newMessage):
    // the message was successfully sent
  case .failure(let error):
    // handle failures
  }
}
```

**Receiving Messages**\
To observe when new messages are received from other users you need to implement the `didRecieveNewMessage` method of the `ChatSessionDelegate`. This will get raised every time another user successfully publishes a Chat Message to the Chat Room.

```swift
class SomeClass: ChatSessionDelegate {
	let chatSession: ChatSession
  
  func chatSession(_ chatSession: ChatSession, didRecieveNewMessage message: ChatMessage) {
    // do something with new message
  }
}
```

## Message History

You can request more messages from the Chat Room history by calling the `loadNextHistory` method on the `ChatSession`. This will load the next page of the transcript. The maximum page size is 25 messages.

```swift
let chatSession: ChatSession

chatSession.loadNextHistory { result in
  switch result {
  case .success(let messages):
    // do something with the loaded page
  case .failure(let error):
    // handle failures
  }
}
```

The `loadNextHistory` returns the messages of the loaded page. These messages are also added to the `ChatSession().messages`.

## Sending Custom Messages

To send a custom message, you can use the `sendCustomMessage' method in the `ChatSession\`. It accepts a string parameter where the integrator can send a JSON Object parsed as String.

```swift Swift
chatSession.sendCustomMessage(customString) { [weak self] result in
		guard let self = self else { return }
    switch result {
    	case .failure(let error):
      		//Handle Failures
      case .success:
          //Custom chat message is received on the chatroom
		}
}
```

## Configure Clickable URLs in Chat Messages

To show and enable links in the chat messages, you have to set the value of **enableChatMessageURLs** in the Chat Session Configuration or Content Session Configuration.

The value is set to true by default and can be set to **false** to disable.

```swift
let config = ChatSessionConfig(roomId: chatRoomId)
config.enableChatMessageURLs = true
```

To add link validation of your own choice, you can add a regex to determine if the chat message text string is linkable or not. For that, you have to set the value of **chatMessageUrlPatterns**  in the Chat Session Configuration or Content Session Configuration as type String.

```swift
let config = ChatSessionConfig(roomId: chatRoomId)
config.enableChatMessageURLs = true
config.chatMessageUrlPatterns = "Validation RegEx"
```

## Deleting a message

Deleting a user's own message in the stock UI has two configurable properties in the **MessagesViewController**. These properties are set to default by true.

**enableUserDeleteMessage** is a boolean value to determine if the users can delete their messages in a chat room.

**shouldShowDeleteConfirmation** is a boolean value to determine if a confirmation alert should be displayed in a chat room when the user attempts to delete a displayed message.

```swift
let chatController = ChatViewController()

override func viewDidLoad() {
	chatController.messageViewController.enableUserDeleteMessage = true
	chatController.messageViewController.shouldShowDeleteConfirmation = true 
}
```

You can also delete users' chat message in a chat room using the **deleteMessage** function in the **ChatSession**. It accepts a **ChatMessage** type parameter which is the message object to be deleted.

```swift
chatSession.deleteMessage(message: chatMessage) { result in
	switch result {
	case .success:
		log.info("Successfult deleted Message with id: \(chatMessage.id.asString)")
	case .failure(let error):
		log.info("Failed to delete Message with id: \(chatMessage.id.asString) due to error: \(error)")
	}
}
```
