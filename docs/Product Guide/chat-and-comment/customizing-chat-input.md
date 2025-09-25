---
title: Customizing Chat Input
excerpt: How to customize a chat room message input
deprecated: false
hidden: false
metadata:
  robots: index
---
A chat message input can be customized to fit the experience you are trying to build. Some example use cases include:

* **Influencer Chat**: Only certain users are allowed to send messages, everyone else can only receive them. Commentators, coaches, past players, or other influential members of the community can have a conversation while everyone else can watch and react.
* **Conversion CTA**: Logged out users get a modified UI provided by the integrators that prompts them to log in or sign up so that they can participate.

> 📘 Minimum Supported SDK Version
>
> iOS: 2.7
> Android: 2.5
> Web: 1.25.

## Toggling Chat Input

If you are using the `ChatViewController` on iOS, you can toggle the chat input view visibility. A similar toggle exists for Android.

```swift Swift
class SomeClass {
    let chatViewController = ChatViewController()
    
    func someMethod() {
        chatViewController.isChatInputVisible = true // Hides the chat input
    }
}
```
```kotlin
/** 
* use this boolean available on ChatView to hide message input to build use case like influencer chat 
**/
livelikeChatView.isChatInputVisible = false
```
```html Web
<!-- The hidecomposer attribute hides the chat input -->
<livelike-chat roomid="example-room-id" hidecomposer>
</livelike-chat>
```

## Customizing Chat Input

Instead of using the ChatViewController, you can opt to add the Message scroll list and/or the Chat Input View to your layout separately.

```swift
class SomeViewController: UIViewController {
    let contentSession: ContentSession
    let messageViewController = MessageViewController()
    let chatInputView = ChatInputView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        addChild(messageViewController)
        view.addSubview(messageViewController.view)
        messageViewController.view.translatesAutoresizingMaskIntoConstraints = false
        
        view.addSubview(chatInputView)
        chatInputView.translatesAutoresizingMaskIntoConstraints = false
        
        // apply ui constraints
        
        messageViewController.setContentSession(contentSession)
        chatInputView.setContentSession(contentSession)
    }
}
```
```html Web
<!-- Example: Replace input with disabled text box, replace after user signs up or logs in -->
<livelike-chat roomid="example-room-id">
  <livelike-chat-composer slot="composer">
    <input slot="body" placeholder="Log in or sign up to chat" disabled>
    <div slot="send" hidden></div>
  </livelike-chat-composer>
</livelike-chat>
```
