---
title: ChatViewController
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ChatViewController | iOS SDK Chat Configuration | LiveLike
  description: >-
    The ChatViewController is a UIViewController provided out-of-the-box in the
    Engagement SDK. Learn more.
  robots: index
next:
  description: ''
---
The ChatViewController is a UIViewController provided out-of-the-box in the EngagementSDK. This is a plug and play UI that enables you to integrate Chat and many of it's features into your application very quickly. 

This a guide on how to customize the default ChatViewController experience.
[block:api-header]
{
  "title": "External Chat Image Support"
}
[/block]
An external image is an image that can be taken from the iOS clipboard and pasted as a message into the chat room. As an integrator you have the ability to disable chat messages with images being posted. This excludes sticker images which are controlled separately through the content management system.
[block:callout]
{
  "type": "info",
  "body": "Support for chat messages with images are turn **on** by default"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let chatController = ChatViewController()\n  \n  func someMethod(){\n  \tchatController.shouldSupportChatImagePosting = false\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Updating User Display Name"
}
[/block]
A user display name is the name of your user that appears to the rest of the chat room members.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  \n  func someMethod(){\n    sdk.setUserDisplayName(\"<new display name>\") { [weak self] result in\n        guard let self = self else { return }\n        switch result {\n        case .success:\n            print(\"Successfuly changed user display name\")\n        case let .failure(error):\n            print(\"Error \\(error.localizedDescription)\")\n        }\n     }\n   }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Chat Avatars"
}
[/block]
A user chat avatar is an image that appears right next to the chat message signifying user's avatar. 

**Displaying Chat Avatars**
As an integrator you can provide a chat experience with chat avatars. A default avatar will be displayed if a custom one is not set or has failed to load. Depending on how you have set up your chat experience a toggle `chatShouldDisplayAvatar` or `shouldDisplayAvatar` may be used to turn chat avatars on/off.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  let chatSession: ChatSession?\n  \n  func someMethod(){\n  \tvar config = ChatSessionConfig(roomID: \"<chatroom id>\")\n    config.shouldDisplayAvatar = true\n    sdk.connectChatRoom(config: config, completion: { [weak self] result in\n      guard let self = self else { return }\n      switch result {\n      case let .success(chatSession):\n     \t chatSession.avatarURL = self.chatAvatarURL\n      case let .failure(error):\n     \t print(error)\n      }\n    })\n  }\n}",
      "language": "swift",
      "name": "ChatSession"
    },
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  var session: ContentSession?\n  \n  func someMethod(){\n    let config = SessionConfiguration(programID: programID)\n    config.chatShouldDisplayAvatar = true\n    session = sdk.contentSession(config: config)\n  }\n}",
      "language": "swift",
      "name": "Content Session"
    }
  ]
}
[/block]
**Updating Chat Avatar**
Depending on how you have set up your chat experience, you have the option to update the chat avatar image on the `ChatSession` or `ContentSession` level.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let sdk: EngagementSDK\n  let chatSession: ChatSession?\n  \n  func someMethod(){\n  \tchatSession.avatarURL = \"<avatar image url>\"\n  }\n}",
      "language": "swift",
      "name": "ChatSession"
    },
    {
      "code": "class SomeClass {\n  var session: ContentSession?\n  \n  func someMethod(){\n    session?.getChatSession(completion: { result in\n            switch result {\n            case let .success(chatSession):\n                chatSession.avatarURL = \"<avatar image url>\"\n            case let .failure(error):\n                print(error)\n            }\n        })\n  }\n}",
      "language": "swift",
      "name": "Content Session"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Chat Message Timestamp"
}
[/block]
A chat message timestamp appears under the content of the message. As an integrator you have the option to customize the format it is displayed in to your users.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let chatController = ChatViewController()\n  \n  func someMethod(){\n  \tchatController.messageTimestampFormatter = { date in\n        let dateFormatter = DateFormatter()\n        dateFormatter.amSymbol = \"am\"\n        dateFormatter.pmSymbol = \"pm\"\n        dateFormatter.setLocalizedDateFormatFromTemplate(\"MMM d hh:mm\")\n        return dateFormatter.string(from: date)\n    }\n   }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Chat Input Visibility"
}
[/block]
In a scenario where you wish to create what is called **Influencer Chat**, you as an integrator have the ability to create a chat experience where a user does not have an option to send any messages only view the incoming ones.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n    let chatViewController = ChatViewController()\n    \n    func someMethod() {\n        chatViewController.isChatInputVisible = true // Hides the chat input\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Profile Status Bar"
}
[/block]
By default, above the chat input field there appears the user's nickname and gamification stats (if gamification is turned on). This information can be hidden by toggling `shouldDisplayProfileStatusBar` variable. 
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n    let chatViewController = ChatViewController()\n    \n    func someMethod() {\n        chatViewController.shouldDisplayProfileStatusBar = false\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Debug Video Time"
}
[/block]
When working with the [Spoiler Prevention](doc:ios-spoiler-free-sync)  functionality, you have the ability to see the timestamp at which a chat message was sent. Knowing the timestamp at which the chat message was sent and at which timestamp your current event is at can help you verify whether Spoiler Prevention is working.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n    let chatViewController = ChatViewController()\n    \n    func someMethod() {\n        chatViewController.shouldDisplayDebugVideoTime = true\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Toggling Chat Experience"
}
[/block]
When working with the [Spoiler Prevention](doc:ios-spoiler-free-sync) functionality or video playback, you have the ability to momentarily disable chat for instances like a commercial break. To toggle chat experience on/off toggle `shouldShowIncomingMessages`  and `isChatInputVisible` to its appropriate states.
[block:code]
{
  "codes": [
    {
      "code": "let chatController = ChatViewController()\nchatController.shouldShowIncomingMessages = false\nchatController.isChatInputVisible = false",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Chat Localization"
}
[/block]
As an integrator you have the ability to localize the EngagementSDK chat experience. All of the EngagementSDK localization files can be found in `EngagementSDK/LiveLikeSDK/Resources/Common/Localization` directory. To overwrite a translated string or to add support for a new language, add the desired EngagementSDK keys to your application's local `Localizable.strings` file. The keys and values in your application's local `Localizable.strings` file will prioritize over the keys and values in the EngagementSDK `Localizable.strings` file.

For example, to replace chat input field placeholder text, add the following key and new value to your local `Localizable.strings` file.
[block:code]
{
  "codes": [
    {
      "code": "\"EngagementSDK.chat.input.placeholder\" = \"Dices Algo\"",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Custom View for Custom Data Messages"
}
[/block]
As an integrator, you have the ability to use custom views to display **custom messages** (messages with custom data).

To set a custom view for messages with custom data, you should implement the **MessageViewControllerDelegate** which is a part of the **messageViewController** object  in the **ChatViewController**. When a message with custom data is received through the **chatViewForCustomDataMessage** function of the **MessageViewControllerDelegate**, you can return a custom **UIView** for the message.
[block:code]
{
  "codes": [
    {
      "code": "class SomeViewController: UIViewController {\n\t\tlet chatController = ChatViewController()\n  \n   override func viewDidLoad() {\n\t\t chatViewController.messageViewController.delegate = self\n   }\n}\n\nextension SomeViewController: MessageViewControllerDelegate {\n    func messageViewController(_ messageViewController: MessageViewController, chatViewForCustomDataMessage customData: String) -> UIView? {\n        if let view = CustomView() {\n          //CustomView setup\n      \t\treturn view\n        } else {\n          return nil\n        }\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]