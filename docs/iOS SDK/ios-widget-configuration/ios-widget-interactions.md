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
## Interaction History

If you are interested in loading the user’s interaction history on a widget. You can do so by calling the `loadInteractionHistory` method on individual Widget Models.

```swift
quizWidgetModel.loadInteractionHistory { result in
	switch result {
    case .success(let answers):
      print("\(answers.count)")
    case .failure(let error):
      print("Error: \(error)")
  }
 }
```

## Interactions for which rewards have not been claimed

To get all interactions for which rewards haven not been claimed yet, use the ContentSession's `getWidgetInteractionsWithUnclaimedRewards` method to retrieve a list of `WidgetInteraction`.

```swift
session.getWidgetInteractionWithUnclaimedRewards(page: .first) { result in
	switch result {
 	case .failure(let error):
		print(error)
	case .success(let widgetInterations):
		print("Found \(widgetInterations.count) widgets with unclaimed rewards.")
 }
}
```
