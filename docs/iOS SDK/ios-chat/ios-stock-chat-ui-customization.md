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
## Snap to Live Button Customization

Users can customize the `SnaptoLive` Button in the Stock Chat UI. Customization of the button can be done in two steps.

1. Customization of the UI of the `SnapToLive` Button can be achieved by implementing the `MessageViewControllerDelegate` which implements a function which can be used to return an object of type `UIButton` which replaces the Stock Button.

```swift
func messageViewController(
  customSnapToLiveButtonForMessageView messageViewController: MessageViewController
) -> UIButton? {
  	let button = UIButton()
  	button.backgroundColor = .gray
  	button.setTitle("Unread Messages", for: .normal)
  	button.layer.cornerRadius = 20.0
  	button.titleLabel?.textColor = .white
  	button.frame = CGRect(x: 0, y: 0, width: 80, height: 40)
  	return button
}
```

2. Customization of the position of the `SnapToLive` Button can be done using the `Theme` object by setting the value for the following variables: 

```swift
/// Changes the horizontal alignment of the "Snap To Live" button
public var snapToLiveButtonHorizontalAlignment: HorizontalAlignment
/// Add a horizontal offset to the "Snap To Live" button
public var snapToLiveButtonHorizontalOffset: CGFloat
/// Add a vertical offset to the "Snap To Live" button
public var snapToLiveButtonVerticalOffset: CGFloat
/// Set the width of the custom button
public var snapToLiveButtonWidthConstant: CGFloat
/// Set the height of the custom button
public var snapToLiveButtonHeightConstant: CGFloat
```

## Stock Chat UI Scrollbar Customization

Users can customize the visibility and indicator style of the scrollbar in the stock chat UI using the following two variables in the Theme object set to the `MessageViewController`

```swift
/// Toggle display of scrollbar indicators in the chat view
public var displayChatScrollIndicators: Bool
/// Toggle color of scrollbar indicators in the chat view
public var chatScrollIndicatorColor: UIScrollView.IndicatorStyle
```

> 🚧 UIScrollView\.IndicatorStyle
>
> The value for `chatScrollIndicatorColor` is of type `UIScrollView.IndicatorStyle` which can only accept values of `IndicatorStyle` type such as `.default`, `.black`, `.white`.

## Insert Custom Content between Messages in Stock Chat UI

Users can insert custom content as UIView objects either before or after a message in the Stock Chat UI. After implementing the `MessageViewControllerDelegate` and confirming to it, users can implement the following function to return the `Custom UIView` object using the `beforeMessageWithID` for before a particular message and `afterMessageWithID` for after a particular message as parameters in the function.

```swift
func messageViewController(
  _ messageViewController: MessageViewController, 
  customViewToDisplayBetweenMessages beforeMessageWithID: String?, 
  afterMessageWithID: String?
) -> UIView? {
        if beforeMessageWithID == "messageID1" || afterMessageWithID == "messageID2" {
            let separatorView = UIView(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))
            let label = UILabel(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))
            label.text = "--------New Messages-------"
            label.textColor = .red
            separatorView.addSubview(label)
            label.heightAnchor.constraint(equalTo: separatorView.heightAnchor).isActive = true
            label.centerXAnchor.constraint(equalTo: separatorView.centerXAnchor).isActive = true
            label.centerYAnchor.constraint(equalTo: separatorView.centerYAnchor).isActive = true

            return separatorView
        } else if beforeMessageWithID == "otherMessageID" {
          	let separatorView = UIView(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))
            let label = UILabel(frame: CGRect(x: 0, y: 0, width: UIScreen.main.bounds.width, height: 60))
            label.text = "----Messages before game began----"
            label.textColor = .white
          	separatorView.backgroundColor = .gray
            separatorView.addSubview(label)
            label.heightAnchor.constraint(equalTo: separatorView.heightAnchor).isActive = true
            label.centerXAnchor.constraint(equalTo: separatorView.centerXAnchor).isActive = true
            label.centerYAnchor.constraint(equalTo: separatorView.centerYAnchor).isActive = true

            return separatorView
        } else {
            return nil
        }
}
```
