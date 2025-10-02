---
title: Widget Interactions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget Interactions | Android SDK | LiveLike Developer Hub
  description: ''
  robots: index
next:
  description: ''
---
## Interaction History

> 📘 Available on SDK version 2.17.2 and above

For many use-cases you may be interested in loading the user’s interaction history on a widget. You can do this by calling the `loadInteractionHistory` method on individual Widget Models. 

```kotlin
pollWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<PollWidgetUserInteraction>>(){
    override fun onResponse(interactionList: List<PollWidgetUserInteraction>?, error: String?) {
    }
})
  // Returns the list of interactions of user on the widget
```

If you are using the timeline view,  you can get the last user interaction on a widget by calling getUserInteraction() method on individual Widget Models 

```kotlin
pollWidgetModel.getUserInteraction()
// Returns the last interaction of user on the widget
```

## Interactions for which rewards have not been claimed yet

The 'getWidgetInteractionsWithUnclaimedRewards' method on the content session can be called to get a list of interactions that have not had their rewards claimed yet. 

```kotlin
session?.getWidgetInteractionsWithUnclaimedRewards(LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<PredictionWidgetUserInteraction>>() {
       override fun onResponse(
         result: List<PredictionWidgetUserInteraction>?,error: String?){
                     
                }
            })
 // Returns all unclaimed interactions
```
