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
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0468dbb-Screen_Shot_2021-08-26_at_1.55.44_PM.png",
        "Screen Shot 2021-08-26 at 1.55.44 PM.png",
        928,
        380,
        "#2e253d"
      ],
      "caption": "Before"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8e85a65-Screen_Shot_2021-08-26_at_1.56.34_PM.png",
        "Screen Shot 2021-08-26 at 1.56.34 PM.png",
        916,
        476,
        "#3e2f55"
      ],
      "caption": "After",
      "border": true,
      "sizing": "smart"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Guide"
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "These are the steps required to achieve the \"After\" design. You will likely need to make additional changes to match your specific customization."
}
[/block]
1. By default, the copy for the tag is blank. You need to add your own copy via localization.
[block:code]
{
  "codes": [
    {
      "code": "// In a Localizable.strings file add the widget tag copy for the following localization keys\n\n\"EngagementSDK.widget.quiz.tag\" = \"QUIZ\";\n\"EngagementSDK.widget.poll.tag\" = \"POLL\";\n\"EngagementSDK.widget.prediction.tag\" = \"PREDICT\";\n\"EngagementSDK.widget.followup.tag\" = \"FOLLOW UP\";",
      "language": "swift",
      "name": "Swift"
    },
    {
      "code": "// Add the widget tag for the following localization keys in either LiveLike.init method's localizedStrings argument, or the LiveLike.applyLocalization method.\n\n\"widget.quiz.tag\": \"QUIZ\";\n\"widget.poll.tag\": \"POLL\";\n\"widget.prediction.tag\": \"PREDICT\";\n\"widget.followup.tag\": \"FOLLOW UP\";",
      "language": "javascript"
    },
    {
      "code": "    // In the strings file add the widget tag copy for the following localization keys\n    <string name=\"livelike_poll_tag\">POLL</string>\n    <string name=\"livelike_quiz_tag\">QUIZ</string>\n    <string name=\"livelike_prediction_tag\">PREDICT</string>\n    <string name=\"livelike_follow_up_tag\">FOLLOW UP</string>",
      "language": "kotlin"
    }
  ]
}
[/block]
2. Apply the following theme customizations
[block:code]
{
  "codes": [
    {
      "code": "let theme = Theme()\ntheme.widgetTagMargins = UIEdgeInsets(top: 10, left: 16, bottom: 0, right: 0)\ntheme.choiceWidgetTitleMargins = UIEdgeInsets(top: 0, left: 16, bottom: -10, right: 0)\nlet titleFont: UIFont = .systemFont(ofSize: 16, weight: .bold)\ntheme.widgets.poll.title.font = titleFont\ntheme.widgets.quiz.title.font = titleFont\ntheme.widgets.prediction.title.font = titleFont\n",
      "language": "swift"
    }
  ]
}
[/block]