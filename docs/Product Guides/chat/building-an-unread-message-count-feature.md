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
[block:api-header]
{
  "title": "Unread Messages Indicator"
}
[/block]
If you want to notify the user that a message has been received on a ChatRoom you can use some kind of visual indicator. 
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let chatSession: ChatSession\n  let chatViewController: ChatViewController\n  let unreadMessagesIndicatorView: UIView\n  \n  func someMethod(){\n    chatSession.addDelegate(self)\n  }\n   \n  func hideChat(){\n    chatViewController.view.isHidden = true\n  }\n  \n  func showChat() {\n    chatViewController.view.isHidden = false\n    // We'll consider the messages to be read when the chatViewController is visible\n    unreadMessagesIndicatorView.isHidden = true\n  }\n}\n\nextension SomeClass: ChatSessionDelegate {\n\tfunc chatSession(_ chatSession: ChatSession, didRecieveNewMessage message: ChatMessage) {\n    if chatViewController.view.isHidden {\n      unreadMessageIndicatorView.isHidden = false\n    }\n  }\n}\n  ",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Unread Message Count Since Last App Launch"
}
[/block]
Another version of an unread message count feature would be to display a number of how many messages were missed since the last time the app was open.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let chatSession: ChatSession\n  let chatViewController: ChatViewController\n  // Keeps track of the latest message received. Stored in local storage.\n  var dateOfLastNewMessage: Date?\n \tlet unreadMessageCountLabel: UILabel\n  \n  func someMethod(){\n    session.addDelegate(self)\n    \n    dateOfLastNewMessage = UserDefaults.standard.object(forKey: \"dateOfLastNewMessage\") as? Date\n    if let dateOfLastNewMessage = dateOfLastNewMessage {\n      \n      chatsession.getMessageCount(\n        since: dateOfLastNewMessage,\n        completion: { result in\n         \tswitch result {\n            case .success(let messageCount):\n           \t\tunreadMessageCountLabel.text = messageCount.description\n            case .failure(let error):\n            \t//handle error\n        })\n    }\n  }\n}\n\nextension SomeClass: ContentSessionDelegate {\n\tfunc chatSession(_ chatSession: ChatSession, didRecieveNewMessage message: ChatMessage) {\n    dateOfLastNewMessage = message.timestamp\n    UserDefaults.standard.set(dateOfLastNewMessage, forKey: \"dateOfLastNewMessage\")\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]