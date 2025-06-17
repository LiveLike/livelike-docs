---
title: Detailed Chat UI
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
```markdown
## Chat

A ready-to-use UI that quickly gives your user the ability to participate in a chat room. Composed of the **Message List** and **Message Input** UI

![2364](https://files.readme.io/26b7889-ChatViewController.png "ChatViewController.png")

<Image title="Screen Shot 2020-08-07 at 4.16.11 PM.png" alt={856} src="https://files.readme.io/c3bcd65-Screen_Shot_2020-08-07_at_4.16.11_PM.png">
  Sticker Keyboard
</Image>

```swift
class SomeViewController: UIViewController {
  let chatViewController = ChatViewController()
  
  override viewDidLoad() {
    super.viewDidLoad()
    
    addChild(chatViewController)
    chatViewController.view.translatesAutoresizingMaskIntoConstraints = false
    view.addSubview(chatViewController.view)
    
    NSLayoutConstraint.activate([
      // apply layout constraints
    ])
  }
}
```

The **Message Input** can be disabled

```swift
let chatViewController = ChatViewController()
chatViewController.isChatInputVisible = false
```

> 📘 Customizing Colors and Font
>
> Most colors and text properties can be modified using the Theme system. See \<link-to-theme> for more information.

## Message List

The scrolling list view that displays the messages of the chat room.

```swift
class SomeViewController: UIViewController {
  let messageViewController = MessageViewController()
  
  override viewDidLoad() {
    super.viewDidLoad()
    
    addChild(messageViewController)
    messageViewController.view.translatesAutoresizingMaskIntoConstraints = false
    view.addSubview(messageViewController.view)
    
    NSLayoutConstraint.activate([
      // apply layout constraints
    ])
  }
}
```

## Message Input

The input view that allows the user to send text, image, and sticker messages.

```swift
class SomeViewController: UIViewController {
  let chatInputView = ChatInputView.instanceFromNib()
  
  override viewDidLoad() {
    super.viewDidLoad()
    
    chatInputView.translatesAutoresizingMaskIntoConstraints = false
    view.addSubview(chatInputView)
    
    NSLayoutConstraint.activate([
      // apply layout constraints
    ])
  }
}
```

## Sticker Keyboard

Allows user's to add stickers to their chat message. Accessed by clicking the sticker button of the **Message Input**. The sticker has a horizontal scrolling view to switch between different sticker packs.

For more information on customizing Sticker packs see \<link-to-sticker-packs>.

## User Nickname

Displays the user's nickname.

This can be disabled

```swift
let chatViewController = ChatViewController()
chatViewController.shouldDisplayProfileStatusBar = false
```

## Message

**Nickname**

The message sender's nickname.

**Message Contents**

The contents of the Chat message. 

**Reactions Display and Reaction Hint**

Displays the reactions to the message and the total count. If there are no reactions then a 'hint' icon is displayed.

The hint icon can be changed or disabled

```swift
var theme = Theme()

// To change
theme.reactionsImageHint = UIImage()

// To disable
theme.reactionsImageHint = nil
```

To customize your reaction pack see \<link to reaction pack tutorial>

**Timestamp**

Displays the timestamp of when the chat message was sent. By default the timestamp format is 'MMM d hh:mm' (eg. Jan 1, 12:34 am).

The timestamp format can be changed or disabled

```swift
let chatViewController = ChatViewController()

// To change
chatViewController.messageViewController.messageTimestampFormatter = { (date: Date) in
	return "custom-date-format-string"
}

// To disable
chatViewController.messageViewController.messageTimestampFormatter = nil
```

## Message Action Popup

**Reaction Picker**

Displays the available reactions and count of each reactions. Allows the user to add a reaction. A user can only add one (1) reaction per message.

To customize your reaction pack see \<link to reaction pack tutorial>

**Report Button**

Gives the user the ability to report a message or block a particular user.

For more information on moderation see \<link-to-moderation-guide>
```