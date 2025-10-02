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

## External Chat Image Support

An external image is an image that can be taken from the iOS clipboard and pasted as a message into the chat room. As an integrator you have the ability to disable chat messages with images being posted. This excludes sticker images which are controlled separately through the content management system.

> 📘 Support for chat messages with images are turn **on** by default

```swift
class SomeClass {
  let chatController = ChatViewController()
  
  func someMethod(){
  	chatController.shouldSupportChatImagePosting = false
  }
}
```

## Updating User Display Name

A user display name is the name of your user that appears to the rest of the chat room members.

```swift
class SomeClass {
  let sdk: EngagementSDK
  
  func someMethod(){
    sdk.setUserDisplayName("<new display name>") { [weak self] result in
        guard let self = self else { return }
        switch result {
        case .success:
            print("Successfuly changed user display name")
        case let .failure(error):
            print("Error \(error.localizedDescription)")
        }
     }
   }
}
```

## Chat Avatars

A user chat avatar is an image that appears right next to the chat message signifying user's avatar. 

**Displaying Chat Avatars**\
As an integrator you can provide a chat experience with chat avatars. A default avatar will be displayed if a custom one is not set or has failed to load. Depending on how you have set up your chat experience a toggle `chatShouldDisplayAvatar` or `shouldDisplayAvatar` may be used to turn chat avatars on/off.

```swift ChatSession
class SomeClass {
  let sdk: EngagementSDK
  let chatSession: ChatSession?
  
  func someMethod(){
  	var config = ChatSessionConfig(roomID: "<chatroom id>")
    config.shouldDisplayAvatar = true
    sdk.connectChatRoom(config: config, completion: { [weak self] result in
      guard let self = self else { return }
      switch result {
      case let .success(chatSession):
     	 chatSession.avatarURL = self.chatAvatarURL
      case let .failure(error):
     	 print(error)
      }
    })
  }
}
```
```swift Content Session
class SomeClass {
  let sdk: EngagementSDK
  var session: ContentSession?
  
  func someMethod(){
    let config = SessionConfiguration(programID: programID)
    config.chatShouldDisplayAvatar = true
    session = sdk.contentSession(config: config)
  }
}
```

**Updating Chat Avatar**\
Depending on how you have set up your chat experience, you have the option to update the chat avatar image on the `ChatSession` or `ContentSession` level.

```swift ChatSession
class SomeClass {
  let sdk: EngagementSDK
  let chatSession: ChatSession?
  
  func someMethod(){
  	chatSession.avatarURL = "<avatar image url>"
  }
}
```
```swift Content Session
class SomeClass {
  var session: ContentSession?
  
  func someMethod(){
    session?.getChatSession(completion: { result in
            switch result {
            case let .success(chatSession):
                chatSession.avatarURL = "<avatar image url>"
            case let .failure(error):
                print(error)
            }
        })
  }
}
```

## Chat Message Timestamp

A chat message timestamp appears under the content of the message. As an integrator you have the option to customize the format it is displayed in to your users.

```swift
class SomeClass {
  let chatController = ChatViewController()
  
  func someMethod(){
  	chatController.messageTimestampFormatter = { date in
        let dateFormatter = DateFormatter()
        dateFormatter.amSymbol = "am"
        dateFormatter.pmSymbol = "pm"
        dateFormatter.setLocalizedDateFormatFromTemplate("MMM d hh:mm")
        return dateFormatter.string(from: date)
    }
   }
}
```

## Chat Input Visibility

In a scenario where you wish to create what is called **Influencer Chat**, you as an integrator have the ability to create a chat experience where a user does not have an option to send any messages only view the incoming ones.

```swift
class SomeClass {
    let chatViewController = ChatViewController()
    
    func someMethod() {
        chatViewController.isChatInputVisible = true // Hides the chat input
    }
}
```

## Profile Status Bar

By default, above the chat input field there appears the user's nickname and gamification stats (if gamification is turned on). This information can be hidden by toggling `shouldDisplayProfileStatusBar` variable. 

```swift
class SomeClass {
    let chatViewController = ChatViewController()
    
    func someMethod() {
        chatViewController.shouldDisplayProfileStatusBar = false
    }
}
```

## Debug Video Time

When working with the [Spoiler Prevention](doc:ios-spoiler-free-sync)  functionality, you have the ability to see the timestamp at which a chat message was sent. Knowing the timestamp at which the chat message was sent and at which timestamp your current event is at can help you verify whether Spoiler Prevention is working.

```swift
class SomeClass {
    let chatViewController = ChatViewController()
    
    func someMethod() {
        chatViewController.shouldDisplayDebugVideoTime = true
    }
}
```

## Toggling Chat Experience

When working with the [Spoiler Prevention](doc:ios-spoiler-free-sync) functionality or video playback, you have the ability to momentarily disable chat for instances like a commercial break. To toggle chat experience on/off toggle `shouldShowIncomingMessages`  and `isChatInputVisible` to its appropriate states.

```swift
let chatController = ChatViewController()
chatController.shouldShowIncomingMessages = false
chatController.isChatInputVisible = false
```

## Chat Localization

As an integrator you have the ability to localize the EngagementSDK chat experience. All of the EngagementSDK localization files can be found in `EngagementSDK/LiveLikeSDK/Resources/Common/Localization` directory. To overwrite a translated string or to add support for a new language, add the desired EngagementSDK keys to your application's local `Localizable.strings` file. The keys and values in your application's local `Localizable.strings` file will prioritize over the keys and values in the EngagementSDK `Localizable.strings` file.

For example, to replace chat input field placeholder text, add the following key and new value to your local `Localizable.strings` file.

```swift
"EngagementSDK.chat.input.placeholder" = "Dices Algo"
```

## Custom View for Custom Data Messages

As an integrator, you have the ability to use custom views to display **custom messages** (messages with custom data).

To set a custom view for messages with custom data, you should implement the **MessageViewControllerDelegate** which is a part of the **messageViewController** object  in the **ChatViewController**. When a message with custom data is received through the **chatViewForCustomDataMessage** function of the **MessageViewControllerDelegate**, you can return a custom **UIView** for the message.

```swift
class SomeViewController: UIViewController {
		let chatController = ChatViewController()
  
   override func viewDidLoad() {
		 chatViewController.messageViewController.delegate = self
   }
}

extension SomeViewController: MessageViewControllerDelegate {
    func messageViewController(_ messageViewController: MessageViewController, chatViewForCustomDataMessage customData: String) -> UIView? {
        if let view = CustomView() {
          //CustomView setup
      		return view
        } else {
          return nil
        }
    }
}
```
