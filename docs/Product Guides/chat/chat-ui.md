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
[block:api-header]
{
  "title": "Chat"
}
[/block]
A ready-to-use UI that quickly gives your user the ability to participate in a chat room. Composed of the **Message List** and **Message Input** UI
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/26b7889-ChatViewController.png",
        "ChatViewController.png",
        2364,
        1189,
        "#98999b"
      ]
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c3bcd65-Screen_Shot_2020-08-07_at_4.16.11_PM.png",
        "Screen Shot 2020-08-07 at 4.16.11 PM.png",
        856,
        584,
        "#2d2928"
      ],
      "caption": "Sticker Keyboard"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SomeViewController: UIViewController {\n  let chatViewController = ChatViewController()\n  \n  override viewDidLoad() {\n    super.viewDidLoad()\n    \n    addChild(chatViewController)\n    chatViewController.view.translatesAutoresizingMaskIntoConstraints = false\n    view.addSubview(chatViewController.view)\n    \n    NSLayoutConstraint.activate([\n      // apply layout constraints\n    ])\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]
The **Message Input** can be disabled
[block:code]
{
  "codes": [
    {
      "code": "let chatViewController = ChatViewController()\nchatViewController.isChatInputVisible = false",
      "language": "swift"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Customizing Colors and Font",
  "body": "Most colors and text properties can be modified using the Theme system. See <link-to-theme> for more information."
}
[/block]

[block:api-header]
{
  "title": "Message List"
}
[/block]
The scrolling list view that displays the messages of the chat room.
[block:code]
{
  "codes": [
    {
      "code": "class SomeViewController: UIViewController {\n  let messageViewController = MessageViewController()\n  \n  override viewDidLoad() {\n    super.viewDidLoad()\n    \n    addChild(messageViewController)\n    messageViewController.view.translatesAutoresizingMaskIntoConstraints = false\n    view.addSubview(messageViewController.view)\n    \n    NSLayoutConstraint.activate([\n      // apply layout constraints\n    ])\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Message Input"
}
[/block]
The input view that allows the user to send text, image, and sticker messages.
[block:code]
{
  "codes": [
    {
      "code": "class SomeViewController: UIViewController {\n  let chatInputView = ChatInputView.instanceFromNib()\n  \n  override viewDidLoad() {\n    super.viewDidLoad()\n    \n    chatInputView.translatesAutoresizingMaskIntoConstraints = false\n    view.addSubview(chatInputView)\n    \n    NSLayoutConstraint.activate([\n      // apply layout constraints\n    ])\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sticker Keyboard"
}
[/block]
Allows user's to add stickers to their chat message. Accessed by clicking the sticker button of the **Message Input**. The sticker has a horizontal scrolling view to switch between different sticker packs.

For more information on customizing Sticker packs see <link-to-sticker-packs>.
[block:api-header]
{
  "title": "User Nickname"
}
[/block]
Displays the user's nickname.

This can be disabled
[block:code]
{
  "codes": [
    {
      "code": "let chatViewController = ChatViewController()\nchatViewController.shouldDisplayProfileStatusBar = false",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Message"
}
[/block]
**Nickname**

The message sender's nickname.

**Message Contents**

The contents of the Chat message. 

**Reactions Display and Reaction Hint**

Displays the reactions to the message and the total count. If there are no reactions then a 'hint' icon is displayed.

The hint icon can be changed or disabled
[block:code]
{
  "codes": [
    {
      "code": "var theme = Theme()\n\n// To change\ntheme.reactionsImageHint = UIImage() \n\n// To disable\ntheme.reactionsImageHint = nil",
      "language": "swift"
    }
  ]
}
[/block]
To customize your reaction pack see <link to reaction pack tutorial>

**Timestamp**

Displays the timestamp of when the chat message was sent. By default the timestamp format is 'MMM d hh:mm' (eg. Jan 1, 12:34 am).

The timestamp format can be changed or disabled
[block:code]
{
  "codes": [
    {
      "code": "let chatViewController = ChatViewController()\n\n// To change\nchatViewController.messageViewController.messageTimestampFormatter = { (date: Date) in\n\treturn \"custom-date-format-string\"\n}\n\n// To disable\nchatViewController.messageViewController.messageTimestampFormatter",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Message Action Popup"
}
[/block]
**Reaction Picker**

Displays the available reactions and count of each reactions. Allows the user to add a reaction. A user can only add one (1) reaction per message.

To customize your reaction pack see <link to reaction pack tutorial>

**Report Button**

Gives the user the ability to report a message or block a particular user.

For more information on moderation see <link-to-moderation-guide>