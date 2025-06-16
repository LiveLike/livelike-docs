---
title: Custom Themes
excerpt: How to apply custom theming to features
deprecated: false
hidden: false
metadata:
  title: Custom Themes | LiveLike Developer Hub | Engagement SDK
  description: >-
    The Theme system allows you to customize the look of the Engagement SDK’s
    Widgets and Chat UI. Learn more about custom themes.
  robots: index
next:
  description: Link out to platform specific guides for applying themes
---
The Theme system allows you to customize the look of the Engagement SDK’s Widgets and Chat UI. This includes common UI properties such as background colors and border colors, corner radii, and text size and fonts. Those customizations are saved in a standard format and can be reused across platforms. Some common use cases for the theme system include:

* Quickly matching your application’s style with minimal development effort
* Uniquely theming Widgets for a sponsorship opportunity
* Improving the accessibility of your application or supporting alternate styles
[block:callout]
{
  "type": "info",
  "title": "Minimum Supported SDK Version",
  "body": "iOS: 2.5\nAndroid: 2.1\nWeb: 1.26.3"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0b181b2-b5d9ab7-6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif",
        "b5d9ab7-6a71fb7-Screen_Recording_2019-09-16_at_04.23_PM.gif",
        729,
        145,
        "#a093a4"
      ],
      "caption": ""
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f54a914-92c017a-ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif",
        "92c017a-ba4ae27-Screen_Recording_2019-09-16_at_04.24_PM.gif",
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
        "https://files.readme.io/7f6f063-ba2873e-16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif",
        "ba2873e-16186e2-Screen_Recording_2019-09-16_at_04.24_PM_1.gif",
        725,
        146,
        "#7591ac"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Theme System"
}
[/block]
Each widget is broken down into *components* that can be themed. Each component has a list of *component properties* that can be modified that will change the visual appearance of the component.

There are two types of components: *container components* and *text components*. Container components have other components inside of them, including text components and other container components. Each type of widget uses a base set of components, and then individual types can have more depending on the widget.

### Container Components

Container components have properties like backgrounds, borders, and corner radii. Container components usually have other container components inside them, as well as text components. The exact properties are:

* Background (Fill or Gradient)
* Border Color
* Border Width
* Corner Radii

### Text Components

Text components can have their font faces, sizes, and weights customized, as well as their colors. The exact properties are:

* Color
* Size
* Font Family
* Font Weight
[block:api-header]
{
  "title": "Widgets"
}
[/block]
### Alert Widgets

* Main Container
  * Header Container
    * Title Text
  * Body Container
    * Description Text (optional)
  * Footer Container (optional)
    * Link Text

### Poll, Quiz, and Prediction Widgets
    
* Main Container
  * Header Container
    * Title Text
  * Body Container
    * Option Container (repeated for each option)
      * Progress Bar Container
      * Option Description Text
      * Option Percentage Text
[block:callout]
{
  "type": "info",
  "title": "Images in options aren't themed",
  "body": "Polls, quizzes, and predictions have an image variant where each option also has an associated image. That image can't be themed, and always appears on the right. In the text variant, the Option Percentage takes the place of the image on the right."
}
[/block]
### Other Widgets

[block:callout]
{
  "type": "warning",
  "title": "More Widget Support Coming Soon",
  "body": "Cheer Meters, and Rich Text can be customized using custom code, but the common theme format does not support them yet.\n\niOS - https://docs.livelike.com/docs/ios-custom-theming\nAndroid - https://docs.livelike.com/docs/android-customization\nWeb - https://docs.livelike.com/docs/web-theming"
}
[/block]

[block:api-header]
{
  "title": "Animations"
}
[/block]
Most widgets use animations to provide user feedback. The following animations can be overridden by following the instructions on [iOS](ios-overriding-default-lottie-animations) and [Android](android-customization#section-overriding-widget-animations). Web does not have animations by default, but an example of how to add animations in Web can be [found here](web-widget-animations-tutorial).
[block:parameters]
{
  "data": {
    "h-0": "Widget",
    "h-1": "Animations",
    "0-0": "Poll",
    "1-0": "Image Slider",
    "2-0": "Trivia/Quiz",
    "3-0": "Prediction",
    "4-0": "Cheer Meter",
    "5-0": "Alerts",
    "0-1": ":no-entry-sign:",
    "1-1": ":no-entry-sign:",
    "2-1": ":white-check-mark: Correct / Incorrect",
    "3-1": ":white-check-mark: Stay Tuned / Correct / Incorrect",
    "4-1": ":white-check-mark: Win / Lose",
    "5-1": ":no-entry-sign:"
  },
  "cols": 2,
  "rows": 6
}
[/block]

[block:api-header]
{
  "title": "Chat"
}
[/block]
iOS - https://docs.livelike.com/docs/ios-custom-theming
Android - https://docs.livelike.com/docs/android-customization
Web - https://docs.livelike.com/docs/web-theming
[block:api-header]
{
  "title": "Applying Theme JSON"
}
[/block]
1. Locate and load the Theme JSON in your project.
2. Use the provided SDK API to generate the objectified Theme object from the Theme JSON.
3. Apply the Theme object to SDK UI's
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n    // Loaded from server, local storage, text field, etc.\n    // Must be compatible with `JSONSerialization.data(withJSONObject:options:)`\n    let jsonObject: Any \n    \n    let widgetViewController: WidgetPopupViewController\n    \n    func someMethod() {\n        do {\n            let theme = try Theme.create(fromJSONObject: jsonObject)\n            widgetViewController.setTheme(theme)\n        } catch {\n            // Fails if json is invalid\n            print(error)\n        }\n    }\n    \n}",
      "language": "swift"
    },
    {
      "code": "// apply theme by passing json object or theme object\nLiveLike.applyTheme(livelikeThemeObject)",
      "language": "javascript"
    },
    {
      "code": "//Create theme object\nval themeObject = LiveLikeTheme.instanceFrom(themeJsonObject)\n\n// apply theme by passing json object or theme object\nwidgetView.applyTheme(liveLikeThemeObject)\nwidgetView.applyTheme(liveLikeThemeJsonObject)\n",
      "language": "kotlin"
    }
  ]
}
[/block]