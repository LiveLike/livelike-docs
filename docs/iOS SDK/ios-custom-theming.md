---
title: Custom Theming
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom Theming | iOS SDK | LiveLike Developer Hub
  description: >-
    The Engagement SDK allows you to customize fonts, colors, corner radii,
    padding, margins and spacing to conform to your style guide.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Customize Your Theme"
}
[/block]
The Engagement SDK allows you to customize fonts, colors, corner radii, padding, margins and spacing to conform to your style guide. The snippets below show chat corner radii and chat background colors, as well as widget corner radii and widget background colors as sample customizations.

Currently there are two different approaches in creating themes. To use the theme web tool approach please see the [Custom Themes](doc:custom-themes) page. To use the `Theme()` object approach, continue reading.

To get started, create a theme object, adjust the relevant properties, and apply that object to your `WidgetPopupViewController` and `ChatViewController`. For the full list of customizable properties see the [API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/Theme.html).

The same widget with different themes:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b5d9ab7-6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif",
        "6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif",
        729,
        145,
        "#a093a4"
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
        "https://files.readme.io/92c017a-ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif",
        "ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif",
        726,
        149,
        "#cbc0c3"
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
        "https://files.readme.io/ba2873e-16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif",
        "16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif",
        725,
        146,
        "#7591ac"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "We recommend applying your theme before adding `WidgetPopupViewController` and `ChatViewController` into your layout."
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "You can also override the default Lottie animations for some widgets. To do this you need to provide the full filepath that points to your custom animation (Lottie compatible json file). You can provide 1 or more custom animations. If more than 1 animation is provided we will cycle through those in random order. Instructions for creating the Lottie animation can be found [here](lottie-animation-guidelines).",
  "title": "Overriding Widget Lottie Animations"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a084acf-5e237a3-BCG_App.png",
        "5e237a3-BCG_App.png",
        472,
        1034,
        "#e3e4e5"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "You can provide the EngagementSDK with a UIView to display within the ChatViewController's message container when there are 0 messages in a chat room. \n\nThe custom view will fill the message container's height and width.\n\nThe custom view will disappear after the first message has been sent to the chat room.",
  "title": "Customize Empty Chat View"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "let customTheme = Theme()\ncustomTheme.chatCornerRadius = 16\ncustomTheme.chatBodyBackgroundColor = .red\ncustomTheme.widgetCornerRadius = 8\ncustomTheme.widgetBodyColor = .blue\nif let font = UIFont(name: \"<font-name>\", size: 16) {\n    customTheme.fontPrimary = font\n}\n\n//Overriding win lottie animations\nlet filePathOfWinAnimation1 = Bundle.main.path(forResource: \"custom_win1\", ofType: \"json\")!\nlet filePathOfWinAnimation2 = Bundle.main.path(forResource: \"custom_win2\", ofType: \"json\")!\ncustomTheme.filepathsForLottieWinningAnimations = [\n  filePathOfCustomAnimation1,\n  filePathOfCustomAnimation2,\n]\n\n//Overriding lose lottie animations\nlet filePathOfLoseAnimation1 = Bundle.main.path(forResource: \"custom_lose1\", ofType: \"json\")!\ncustomTheme.filepathsForLottieWinningAnimations = [\n  filePathOfLoseAnimation1\n]\n\n//Customize empty chat view (with subviews and contraints)\ncustomTheme.emptyChatCustomView = {\n    // The root view\n    let container: UIView()\n\n    // Additional ui elements\n    let image: UIImageView()\n    let title: UILabel()\n    let body: UIlabel()\n\n    /// add additional ui as subviews to root view \n    container.addSubview(image)\n    container.addSubview(title)\n    container.addSubview(body)\n\n    NSLayoutConstraints.activate([\n        // Apply layout constraints\n    ])\n\n    // return the root view\n    return container\n}()\n\nwidgetViewController.setTheme(customTheme)\nchatViewController.setTheme(customTheme)",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Customize Chat Avatar Image"
}
[/block]
Chat avatar image is an image that appears next to a chat message. This functionality is disabled by default. To enable chat avatar image you need to pass an image URL to the `ContentSession.updateUserChatRoomImage` function and 
set the chat avatar image width and height on your theme object.
[block:code]
{
  "codes": [
    {
      "code": "// Setting Image\nlet session: ContentSession\noverride func viewDidAppear(_ animated: Bool) {\n  super.viewDidAppear(animated)\n\tsession.updateUserChatRoomImage(url:<image url> ,\n  \t                              completion: {},\n    \t                            failure: { error in })\n}\n\n// Modifying the Theme\nlet sampleTheme = Theme()\nsampleTheme.chatImageWidth = 20.0\nsampleTheme.chatImageHeight = 20.0",
      "language": "swift"
    }
  ]
}
[/block]