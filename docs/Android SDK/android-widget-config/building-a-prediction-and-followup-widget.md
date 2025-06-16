---
title: Building a Prediction and followup widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building a Prediction and Followup Widget | Android SDK | LiveLike
  description: >-
    This is a guide on building a Custom Prediction and Followup Widget for
    Android applications. Learn More.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK Version",
  "body": "2.9"
}
[/block]
This is a guide on building a custom Prediction and followup Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Prediction Widget Model"
}
[/block]
The Prediction Widget Model is responsible for providing prediction specific data and remote apis for vote and results;

***Prediction Data(object of LiveLikeWidget class)***
The Prediction Data provides data about the Prediction Widget such as the title text and the options.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

Note: Use options in livelikeWidget class for the Prediction.

[block:code]
{
  "codes": [
    {
      "code": " predictionWidgetModel?.widgetData?.let { liveLikeWidget ->\n            liveLikeWidget.options?.let {\n                if (it.size > 2) {\n                    rcyl_poll_list.layoutManager = GridLayoutManager(context, 2)\n                }\n                val adapter =\n                    PredictionListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))\n                rcyl_poll_list.adapter = adapter\n                adapter.pollListener = object : PollListAdapter.PollListener {\n                    override fun onSelectOption(id: String) {\n                        predictionWidgetModel?.submitVote(id)\n                    }\n                }\n                button2.visibility = View.GONE\n            }\n        }",
      "language": "kotlin"
    }
  ]
}
[/block]
***lockInVote***
For submitting or changing the vote on the option for the poll which needed optionId to send to the backend for changing/submitting the vote for the poll.
[block:code]
{
  "codes": [
    {
      "code": "  pollWidgetModel?.submitVote(optionId)",
      "language": "kotlin"
    }
  ]
}
[/block]
***VoteResults***
The VoteResults gives you events for updates on the Prediction Widget. The event contains the vote count changes for each option on the server.
[block:code]
{
  "codes": [
    {
      "code": "predictionWidgetModel?.voteResults?.subscribe(this) { result ->\n                    result?.choices?.let { options ->\n                        options.forEach { op ->\n                            adapter.optionIdCount[op.id] = op.vote_count ?: 0\n                        }\n                        adapter.notifyDataSetChanged()\n                    }\n                }",
      "language": "kotlin"
    }
  ]
}
[/block]
***Interaction History***
To load the interaction history, you can call the loadInteractionHistory method
Eg:
[block:code]
{
  "codes": [
    {
      "code": " predictionWidgetViewModel?.loadInteractionHistory( object : LiveLikeCallback<List<PredictionWidgetUserInteraction>>(){\n            override fun onResponse(result: List<PredictionWidgetUserInteraction>?, error: String?) {\n\n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "FollowUp Widget Model"
}
[/block]
The follow-up model has the same functions as the above one except lockInVote.

***getPredictionVoteId()***
This method on the model allows you to the retrieve predictionVoteId that user voted on prediction associated with this follow up

[block:code]
{
  "codes": [
    {
      "code": "val voteId = followUpWidgetViewModel?.getPredictionVoteId()\noptionsAdapter.selectedIndex = optionList.indexOfFirst { option-> option?.id == followUpWidgetViewModel?.getPredictionVoteId() }  ",
      "language": "kotlin"
    }
  ]
}
[/block]
***claimRewards()***
    * claims the rewards on the prediction follow up using a user’s vote
    * returns nothing but notifies leaderboard clients


[block:code]
{
  "codes": [
    {
      "code": "followUpWidgetViewModel?.claimRewards()",
      "language": "kotlin"
    }
  ]
}
[/block]