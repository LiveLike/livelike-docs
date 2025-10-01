---
title: Enabling Widget Tag UI for Quiz, Poll, and Predictions
excerpt: >-
  A guide on how to enable UI to allow users to easily differentiate between
  Quiz, Polls, and Prediction Widgets
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<Image title="Screen Shot 2021-08-26 at 1.55.44 PM.png" alt={928} src="https://files.readme.io/0468dbb-Screen_Shot_2021-08-26_at_1.55.44_PM.png">
  Before
</Image>

<Image title="Screen Shot 2021-08-26 at 1.56.34 PM.png" alt={916} width="smart" border={true} src="https://files.readme.io/8e85a65-Screen_Shot_2021-08-26_at_1.56.34_PM.png">
  After
</Image>

## Guide

> 📘 These are the steps required to achieve the "After" design. You will likely need to make additional changes to match your specific customization.

1. By default, the copy for the tag is blank. You need to add your own copy via localization.

```swift Swift
// In a Localizable.strings file add the widget tag copy for the following localization keys

"EngagementSDK.widget.quiz.tag" = "QUIZ";
"EngagementSDK.widget.poll.tag" = "POLL";
"EngagementSDK.widget.prediction.tag" = "PREDICT";
"EngagementSDK.widget.followup.tag" = "FOLLOW UP";
```
```javascript
// Add the widget tag for the following localization keys in either LiveLike.init method's localizedStrings argument, or the LiveLike.applyLocalization method.

"widget.quiz.tag": "QUIZ";
"widget.poll.tag": "POLL";
"widget.prediction.tag": "PREDICT";
"widget.followup.tag": "FOLLOW UP";
```
```kotlin
// In the strings file add the widget tag copy for the following localization keys
    <string name="livelike_poll_tag">POLL</string>
    <string name="livelike_quiz_tag">QUIZ</string>
    <string name="livelike_prediction_tag">PREDICT</string>
    <string name="livelike_follow_up_tag">FOLLOW UP</string>
```

2. Apply the following theme customizations

```swift
let theme = Theme()
theme.widgetTagMargins = UIEdgeInsets(top: 10, left: 16, bottom: 0, right: 0)
theme.choiceWidgetTitleMargins = UIEdgeInsets(top: 0, left: 16, bottom: -10, right: 0)
let titleFont: UIFont = .systemFont(ofSize: 16, weight: .bold)
theme.widgets.poll.title.font = titleFont
theme.widgets.quiz.title.font = titleFont
theme.widgets.prediction.title.font = titleFont
```
