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
## What is Lottie?

Lottie is a Framework used to add high-quality animations to the EngagementSDK. [https://airbnb.design/lottie/](https://airbnb.design/lottie/)

For design guidelines and instruction on building your Lottie animations for the EngagementSDK see [https://docs.livelike.com/docs/lottie-animation-guidelines](https://docs.livelike.com/docs/lottie-animation-guidelines)

## Which animations can be overriden?

* Win - Played after winning a Quiz
* Lose
* Stay Tuned
* Interaction Timer

Multiple animations can be set for the Win, Lose, and Stay Tuned animations. The EngagementSDK will randomly cycle through each one.

## Integration Steps

The animations are defined as part of the Theme. To override the Lottie animations you need to provide the full filepath to the Lottie animation in your project. For more information on how to get the full filepath see [https://developer.apple.com/documentation/foundation/bundle/1410989-path](https://developer.apple.com/documentation/foundation/bundle/1410989-path).

```swift
class SomeClass {
  
  let widgetViewController = WidgetPopupViewController()
  
  func someMethod() {
    var theme = Theme()
    
    //Overriding win lottie animations
    theme.lottieFilepaths.win = [
      Bundle.main.path(forResource: "custom_win1", ofType: "json")!,
      Bundle.main.path(forResource: "custom_win2", ofType: "json")!
    ]

    //Overriding lose lottie animations
    theme.lottieFilepaths.lose = [
      Bundle.main.path(forResource: "custom_lose1", ofType: "json")!,
      Bundle.main.path(forResource: "custom_lose2", ofType: "json")!
    ]
    
    //Overriding stay tuned lottie animations
    theme.lottieFilepaths.predictionTimerComplete = [
      Bundle.main.path(forResource: "custom_stayTuned1", ofType: "json")!,
      Bundle.main.path(forResource: "custom_stayTuned2", ofType: "json")!
    ]
    
    //Overriding interaction timer lottie animations
    theme.lottieFilepaths.timer = 
    	Bundle.main.path(forResource: "custom_timer1", ofType: "json")!
    
    // After you're done customizing your theme
    // You can apply it to the WidgetPopupViewController
    widgetViewController.setTheme(theme)
  }
}
```
