---
title: Overriding Default Animations
excerpt: A guide on how to override the various Lottie animations used for Widgets
deprecated: false
hidden: false
metadata:
  title: Overriding Default Animations | iOS SDK | LiveLike Developer Hub
  description: >-
    Check out our guide on how to override the various Lottie animations for
    widgets. Learn more about overriding default animations.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "What is Lottie?"
}
[/block]
Lottie is a Framework used to add high-quality animations to the EngagementSDK. https://airbnb.design/lottie/

For design guidelines and instruction on building your Lottie animations for the EngagementSDK see https://docs.livelike.com/docs/lottie-animation-guidelines
[block:api-header]
{
  "title": "Which animations can be overriden?"
}
[/block]
* Win - Played after winning a Quiz
* Lose
* Stay Tuned
* Interaction Timer

Multiple animations can be set for the Win, Lose, and Stay Tuned animations. The EngagementSDK will randomly cycle through each one.
[block:api-header]
{
  "title": "Integration Steps"
}
[/block]
The animations are defined as part of the Theme. To override the Lottie animations you need to provide the full filepath to the Lottie animation in your project. For more information on how to get the full filepath see https://developer.apple.com/documentation/foundation/bundle/1410989-path.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  \n  let widgetViewController = WidgetPopupViewController()\n  \n  func someMethod() {\n    var theme = Theme()\n    \n    //Overriding win lottie animations\n    theme.lottieFilepaths.win = [\n      Bundle.main.path(forResource: \"custom_win1\", ofType: \"json\")!,\n      Bundle.main.path(forResource: \"custom_win2\", ofType: \"json\")!\n    ]\n\n    //Overriding lose lottie animations\n    theme.lottieFilepaths.lose = [\n      Bundle.main.path(forResource: \"custom_lose1\", ofType: \"json\")!,\n      Bundle.main.path(forResource: \"custom_lose2\", ofType: \"json\")!\n    ]\n    \n    //Overriding stay tuned lottie animations\n    theme.lottieFilepaths.predictionTimerComplete = [\n      Bundle.main.path(forResource: \"custom_stayTuned1\", ofType: \"json\")!,\n      Bundle.main.path(forResource: \"custom_stayTuned2\", ofType: \"json\")!\n    ]\n    \n    //Overriding interaction timer lottie animations\n    theme.lottieFilepaths.timer = \n    \tBundle.main.path(forResource: \"custom_timer1\", ofType: \"json\")!\n    \n    // After you're done customizing your theme\n    // You can apply it to the WidgetPopupViewController\n    widgetViewController.setTheme(theme)\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]