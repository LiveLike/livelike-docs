---
title: Customizing Chat Input
excerpt: How to customize a chat room message input
deprecated: false
hidden: false
metadata:
  title: Customizing Chat Input | LiveLike Developer Hub
  description: >-
    A chat message input can be customized to fit the experience you are
    building. Example use cases include influencer chats and conversation chats.
  robots: index
next:
  description: ''
---
A chat message input can be customized to fit the experience you are trying to build. Some example use cases include:

* **Influencer Chat**: Only certain users are allowed to send messages, everyone else can only receive them. Commentators, coaches, past players, or other influential members of the community can have a conversation while everyone else can watch and react.
* **Conversion CTA**: Logged out users get a modified UI provided by the integrators that prompts them to log in or sign up so that they can participate.
[block:callout]
{
  "type": "info",
  "title": "Minimum Supported SDK Version",
  "body": "iOS: 2.7\nAndroid: 2.5\nWeb: 1.25."
}
[/block]

[block:api-header]
{
  "title": "Toggling Chat Input"
}
[/block]
If you are using the `ChatViewController` on iOS, you can toggle the chat input view visibility. A similar toggle exists for Android.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n    let chatViewController = ChatViewController()\n    \n    func someMethod() {\n        chatViewController.isChatInputVisible = true // Hides the chat input\n    }\n}",
      "language": "swift",
      "name": "Swift"
    },
    {
      "code": "/** \n* use this boolean available on ChatView to hide message input to build use case like influencer chat \n**/\nlivelikeChatView.isChatInputVisible = false\n\n",
      "language": "kotlin"
    },
    {
      "code": "<!-- The hidecomposer attribute hides the chat input -->\n<livelike-chat roomid=\"example-room-id\" hidecomposer>\n</livelike-chat>",
      "language": "html",
      "name": "Web"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Customizing Chat Input"
}
[/block]
Instead of using the ChatViewController, you can opt to add the Message scroll list and/or the Chat Input View to your layout separately.
[block:code]
{
  "codes": [
    {
      "code": "class SomeViewController: UIViewController {\n    let contentSession: ContentSession\n    let messageViewController = MessageViewController()\n    let chatInputView = ChatInputView()\n    \n    override func viewDidLoad() {\n        super.viewDidLoad()\n        addChild(messageViewController)\n        view.addSubview(messageViewController.view)\n        messageViewController.view.translatesAutoresizingMaskIntoConstraints = false\n        \n        view.addSubview(chatInputView)\n        chatInputView.translatesAutoresizingMaskIntoConstraints = false\n        \n        // apply ui constraints\n        \n        messageViewController.setContentSession(contentSession)\n        chatInputView.setContentSession(contentSession)\n    }\n}",
      "language": "swift"
    },
    {
      "code": "<!-- Example: Replace input with disabled text box, replace after user signs up or logs in -->\n<livelike-chat roomid=\"example-room-id\">\n  <livelike-chat-composer slot=\"composer\">\n    <input slot=\"body\" placeholder=\"Log in or sign up to chat\" disabled>\n    <div slot=\"send\" hidden></div>\n  </livelike-chat-composer>\n</livelike-chat>",
      "language": "html",
      "name": "Web"
    }
  ]
}
[/block]