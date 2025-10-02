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
> 📘 Minimum SDK Version
>
> 2.9

This is a guide on building a custom Prediction and followup Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Prediction Widget Model

The Prediction Widget Model is responsible for providing prediction specific data and remote apis for vote and results;

***Prediction Data(object of LiveLikeWidget class)***\
The Prediction Data provides data about the Prediction Widget such as the title text and the options.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

Note: Use options in livelikeWidget class for the Prediction.

```kotlin
predictionWidgetModel?.widgetData?.let { liveLikeWidget ->
            liveLikeWidget.options?.let {
                if (it.size > 2) {
                    rcyl_poll_list.layoutManager = GridLayoutManager(context, 2)
                }
                val adapter =
                    PredictionListAdapter(context, isImage, ArrayList(it.map { item -> item!! }))
                rcyl_poll_list.adapter = adapter
                adapter.pollListener = object : PollListAdapter.PollListener {
                    override fun onSelectOption(id: String) {
                        predictionWidgetModel?.submitVote(id)
                    }
                }
                button2.visibility = View.GONE
            }
        }
```

***lockInVote***\
For submitting or changing the vote on the option for the poll which needed optionId to send to the backend for changing/submitting the vote for the poll.

```kotlin
pollWidgetModel?.submitVote(optionId)
```

***VoteResults***\
The VoteResults gives you events for updates on the Prediction Widget. The event contains the vote count changes for each option on the server.

```kotlin
predictionWidgetModel?.voteResults?.subscribe(this) { result ->
                    result?.choices?.let { options ->
                        options.forEach { op ->
                            adapter.optionIdCount[op.id] = op.vote_count ?: 0
                        }
                        adapter.notifyDataSetChanged()
                    }
                }
```

***Interaction History***\
To load the interaction history, you can call the loadInteractionHistory method\
Eg:

```kotlin
predictionWidgetViewModel?.loadInteractionHistory( object : LiveLikeCallback<List<PredictionWidgetUserInteraction>>(){
            override fun onResponse(result: List<PredictionWidgetUserInteraction>?, error: String?) {

            }
        })
```

## FollowUp Widget Model

The follow-up model has the same functions as the above one except lockInVote.

***getPredictionVoteId()***\
This method on the model allows you to the retrieve predictionVoteId that user voted on prediction associated with this follow up

```kotlin
val voteId = followUpWidgetViewModel?.getPredictionVoteId()
optionsAdapter.selectedIndex = optionList.indexOfFirst { option-> option?.id == followUpWidgetViewModel?.getPredictionVoteId() }
```

***claimRewards()***\
    *claims the rewards on the prediction follow up using a user’s vote\&#xA;* returns nothing but notifies leaderboard clients

```kotlin
followUpWidgetViewModel?.claimRewards()
```
