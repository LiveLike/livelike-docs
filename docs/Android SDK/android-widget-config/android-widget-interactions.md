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
[block:api-header]
{
  "title": "Interaction History"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Available on SDK version 2.17.2 and above"
}
[/block]
For many use-cases you may be interested in loading the user’s interaction history on a widget. You can do this by calling the `loadInteractionHistory` method on individual Widget Models. 
[block:code]
{
  "codes": [
    {
      "code": "pollWidgetModel?.loadInteractionHistory( object : LiveLikeCallback<List<PollWidgetUserInteraction>>(){\n    override fun onResponse(interactionList: List<PollWidgetUserInteraction>?, error: String?) {\n    }\n})\n  // Returns the list of interactions of user on the widget",
      "language": "kotlin"
    }
  ]
}
[/block]
If you are using the timeline view,  you can get the last user interaction on a widget by calling getUserInteraction() method on individual Widget Models 
[block:code]
{
  "codes": [
    {
      "code": "pollWidgetModel.getUserInteraction()\n// Returns the last interaction of user on the widget",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Interactions for which rewards have not been claimed yet"
}
[/block]
The 'getWidgetInteractionsWithUnclaimedRewards' method on the content session can be called to get a list of interactions that have not had their rewards claimed yet. 
[block:code]
{
  "codes": [
    {
      "code": "session?.getWidgetInteractionsWithUnclaimedRewards(LiveLikePagination.FIRST,\n    object : LiveLikeCallback<List<PredictionWidgetUserInteraction>>() {\n       override fun onResponse(\n         result: List<PredictionWidgetUserInteraction>?,error: String?){\n                     \n                }\n            })\n // Returns all unclaimed interactions",
      "language": "kotlin"
    }
  ]
}
[/block]