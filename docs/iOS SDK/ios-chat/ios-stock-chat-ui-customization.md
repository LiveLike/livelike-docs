---
title: Stock Chat UI Customization
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Stock Chat UI Customization | IOS SDK | LiveLike Developer Hub
  description: >-
    Users can customize the Snap to Live Button in the Stock Chat UI by changing
    its appearance and position, and they can also customize the visibility and
    style of the scrollbar. Additionally, users can insert custom content before
    or after a message in the Stock Chat UI.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Snap to Live Button Customization"
}
[/block]
Users can customize the `SnaptoLive` Button in the Stock Chat UI. Customization of the button can be done in two steps.
1. Customization of the UI of the `SnapToLive` Button can be achieved by implementing the `MessageViewControllerDelegate` which implements a function which can be used to return an object of type `UIButton` which replaces the Stock Button.

[block:code]
{
  "codes": [
    {
      "code": "func messageViewController(\n  customSnapToLiveButtonForMessageView messageViewController: MessageViewController\n) -> UIButton? {\n  \tlet button = UIButton()\n  \tbutton.backgroundColor = .gray\n  \tbutton.setTitle(\"Unread Messages\", for: .normal)\n  \tbutton.layer.cornerRadius = 20.0\n  \tbutton.titleLabel?.textColor = .white\n  \tbutton.frame = CGRect(x: 0, y: 0, width: 80, height: 40)\n  \treturn button\n}",
      "language": "swift"
    }
  ]
}
[/block]
2. Customization of the position of the `SnapToLive` Button can be done using the `Theme` object by setting the value for the following variables: 
[block:code]
{
  "codes": [
    {
      "code": "/// Changes the horizontal alignment of the \"Snap To Live\" button\npublic var snapToLiveButtonHorizontalAlignment: HorizontalAlignment\n/// Add a horizontal offset to the \"Snap To Live\" button\npublic var snapToLiveButtonHorizontalOffset: CGFloat\n/// Add a vertical offset to the \"Snap To Live\" button\npublic var snapToLiveButtonVerticalOffset: CGFloat\n/// Set the width of the custom button\npublic var snapToLiveButtonWidthConstant: CGFloat\n/// Set the height of the custom button\npublic var snapToLiveButtonHeightConstant: CGFloat",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Stock Chat UI Scrollbar Customization"
}
[/block]
Users can customize the visibility and indicator style of the scrollbar in the stock chat UI using the following two variables in the Theme object set to the `MessageViewController`
[block:code]
{
  "codes": [
    {
      "code": "/// Toggle display of scrollbar indicators in the chat view\npublic var displayChatScrollIndicators: Bool\n/// Toggle color of scrollbar indicators in the chat view\npublic var chatScrollIndicatorColor: UIScrollView.IndicatorStyle",
      "language": "swift"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "UIScrollView.IndicatorStyle",
  "body": "The value for `chatScrollIndicatorColor` is of type `UIScrollView.IndicatorStyle` which can only accept values of `IndicatorStyle` type such as `.default`, `.black`, `.white`."
}
[/block]

[block:api-header]
{
  "title": "Insert Custom Content between Messages in Stock Chat UI"
}
[/block]
Users can insert custom content as UIView objects either before or after a message in the Stock Chat UI. After implementing the `MessageViewControllerDelegate` and confirming to it, users can implement the following function to return the `Custom UIView` object using the `beforeMessageWithID` for before a particular message and `afterMessageWithID` for after a particular message as parameters in the function.
[block:code]
{
  "codes": [
    {
      "code": "func messageViewController(\n  _ messageViewController: MessageViewController, \n  customViewToDisplayBetweenMessages beforeMessageWithID: String?, \n  afterMessageWithID: String?\n) -> UIView? {\n        if beforeMessageWithID == \"messageID1\" || afterMessageWithID == \"messageID2\" {\n            let separatorView = UIView(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))\n            let label = UILabel(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))\n            label.text = \"--------New Messages-------\"\n            label.textColor = .red\n            separatorView.addSubview(label)\n            label.heightAnchor.constraint(equalTo: separatorView.heightAnchor).isActive = true\n            label.centerXAnchor.constraint(equalTo: separatorView.centerXAnchor).isActive = true\n            label.centerYAnchor.constraint(equalTo: separatorView.centerYAnchor).isActive = true\n\n            return separatorView\n        } else if beforeMessageWithID == \"otherMessageID\" {\n          \tlet separatorView = UIView(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))\n            let label = UILabel(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))\n            label.text = \"----Messages before game began----\"\n            label.textColor = .white\n          \tseparatorView.backgroundColor = .gray\n            separatorView.addSubview(label)\n            label.heightAnchor.constraint(equalTo: separatorView.heightAnchor).isActive = true\n            label.centerXAnchor.constraint(equalTo: separatorView.centerXAnchor).isActive = true\n            label.centerYAnchor.constraint(equalTo: separatorView.centerYAnchor).isActive = true\n\n            return separatorView\n        } else {\n            return nil\n        }\n}",
      "language": "swift"
    }
  ]
}
[/block]