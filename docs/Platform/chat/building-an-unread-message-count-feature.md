---
title: Counting Unread Messages
excerpt: >-
  In a scenario where you might choose to have many chat rooms, an Unread
  Message Count feature provides functionality that can be used to determine the
  amount of unread or unseen messages by your user.
deprecated: false
hidden: false
metadata:
  title: Counting Unread Messages | LiveLike Developer Hub
  description: >-
    An Unread Message Count feature provides functionality that can be used to
    determine the amount of unread or unseen messages by your user.
  robots: index
next:
  description: ''
---
This is a walkthrough on how to create two types of unread message count features using the EngagementSDK. 

## Unread Messages Indicator

If you want to notify the user that a message has been received on a ChatRoom you can use some kind of visual indicator. 

```swift
class SomeClass {
  let chatSession: ChatSession
  let chatViewController: ChatViewController
  let unreadMessagesIndicatorView: UIView
  
  func someMethod(){
    chatSession.addDelegate(self)
  }
   
  func hideChat(){
    chatViewController.view.isHidden = true
  }
  
  func showChat() {
    chatViewController.view.isHidden = false
    // We'll consider the messages to be read when the chatViewController is visible
    unreadMessagesIndicatorView.isHidden = true
  }
}

extension SomeClass: ChatSessionDelegate {
	func chatSession(_ chatSession: ChatSession, didRecieveNewMessage message: ChatMessage) {
    if chatViewController.view.isHidden {
      unreadMessageIndicatorView.isHidden = false
    }
  }
}
```

## Unread Message Count Since Last App Launch

Another version of an unread message count feature would be to display a number of how many messages were missed since the last time the app was open.

```swift
class SomeClass {
  let chatSession: ChatSession
  let chatViewController: ChatViewController
  // Keeps track of the latest message received. Stored in local storage.
  var dateOfLastNewMessage: Date?
 	let unreadMessageCountLabel: UILabel
  
  func someMethod(){
    session.addDelegate(self)
    
    dateOfLastNewMessage = UserDefaults.standard.object(forKey: "dateOfLastNewMessage") as? Date
    if let dateOfLastNewMessage = dateOfLastNewMessage {
      
      chatsession.getMessageCount(
        since: dateOfLastNewMessage,
        completion: { result in
         	switch result {
            case .success(let messageCount):
           		unreadMessageCountLabel.text = messageCount.description
            case .failure(let error):
            	//handle error
        })
    }
  }
}

extension SomeClass: ContentSessionDelegate {
	func chatSession(_ chatSession: ChatSession, didRecieveNewMessage message: ChatMessage) {
    dateOfLastNewMessage = message.timestamp
    UserDefaults.standard.set(dateOfLastNewMessage, forKey: "dateOfLastNewMessage")
  }
}
```
