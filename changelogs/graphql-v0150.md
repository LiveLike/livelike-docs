---
title: GraphQL v0.15.0
author: Jordanco Trpcevski
hidden: false
published_at: '2026-03-06T14:05:04.064Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on widgets NumberPrediction, TextAsk, CheerMeter, SocialEmbed, Quest. Below is a structured documentation to outline these changes

<br />

### Release Changes

#### NumberPrediction

***

* **numberPrediction**: Fetch the number prediction widget.
* **numberPredictionFollowUp**: Fetch the number prediction follow up widget.
* **createNumberPrediction**: Create a number prediction widget.
* **createNumberPredictionFollowUp**: Create a number prediction followup widget.
* **publishNumberPrediction**: Publish a number prediction widget.
* **publishNumberPredictionFollowUp**: Publish a number prediction followup widget.
* **deleteNumberPrediction**: Delete a number prediction widget.
* **deleteNumberPredictionFollowUp**: Delete a number prediction followup widget.

#### TextAsk

***

* **textAsk**: Fetch the text ask widget.
* **textAskReplies**: Fetch a text ask replies for text ask widget.
* **createTextAsk**: Create a text ask widget.
* **publishTextAsk**: Publish a text ask widget.
* **createTextAskReply**: Create a text ask reply.
* **deleteTextAsk**: Delete a text ask widget.

#### CheerMeter

***

* **cheerMeter**: Fetch the cheer meter widget.
* **createCheerMeter**: Create a cheer meter widget.
* **publishCheerMeter**: Publish a cheer meter widget.
* **createCheerMeterVote**: Create a cheer meter vote.
* **updateCheerMeterVote**: Update a cheer meter vote.
* **deleteCheerMeter**: Delete a cheer meter widget.

#### SocialEmbed

***

* **socialEmbed**: Fetch the social embed widget.
* **createSocialEmbed**: Create a social embed widget.
* **publishSocialEmbed**: Publish a social embed widget.
* **deleteSocialEmbed**: Delete a social embed widget.

#### Quest

***

* **quest**: Fetch the quest widget.
* **questTask**: Fetch the quest task.
* **questTasks**: Fetch quest tasks.
* **createQuestTask**: Create a quest task.
* **deleteQuest**: Delete a quest widget.
* **deleteQuestTask**: Delete a quest task.