---
title: Widget Interactions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget Interactions | iOS SDK | LiveLike Developer Hub
  description: >-
    Load a user's interaction history on a widget by calling the
    'LoadInteractionHistory' method on individual widget models. Learn more.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Interaction History"
}
[/block]
If you are interested in loading the user’s interaction history on a widget. You can do so by calling the `loadInteractionHistory` method on individual Widget Models.
[block:code]
{
  "codes": [
    {
      "code": "quizWidgetModel.loadInteractionHistory { result in\n\tswitch result {\n    case .success(let answers):\n      print(\"\\(answers.count)\")\n    case .failure(let error):\n      print(\"Error: \\(error)\")\n  }\n }",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Interactions for which rewards have not been claimed"
}
[/block]
To get all interactions for which rewards haven not been claimed yet, use the ContentSession's `getWidgetInteractionsWithUnclaimedRewards` method to retrieve a list of `WidgetInteraction`.
[block:code]
{
  "codes": [
    {
      "code": "session.getWidgetInteractionWithUnclaimedRewards(page: .first) { result in\n\tswitch result {\n \tcase .failure(let error):\n\t\tprint(error)\n\tcase .success(let widgetInterations):\n\t\tprint(\"Found \\(widgetInterations.count) widgets with unclaimed rewards.\")\n }\n}",
      "language": "swift"
    }
  ]
}
[/block]