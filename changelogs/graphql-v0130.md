---
title: GraphQL v0.13.0
author: Jordanco Trpcevski
hidden: false
published_at: '2025-09-15T11:51:56.134Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Profile, Program, Leaderboard, Widget, Poll, RichPost,Prediction and Alert. Below is a structured documentation to outline these changes

### Release Changes

#### Profile

***

* **me**: Removed mandatory parameter clientId, when getting current authenticated profile.
* **createProfileByCustomId**: Create a profile by custom ID.
* **field widgetsInteractions**: Updated to return specific WidgetInteractionUnion type, against general deprecated type WidgetInteraction..

#### Program

***

* **createProgram**: Support for managing localization.
* **updateProgram**: Support for managing localization.

#### Leaderboard

***

* **linkLeaderboardWithProgram**: Link a Leaderboard with the Program.
* **unlinkLeaderboardFromProgram**: Unlink a Leaderboard from the Program.

#### Widget

***

* **type WidgetInteraction**: Deprecated.
* **union WidgetInteractionUnion**: Union of widget interaction specific types.
* **widgetsInteractions**: Updated to return specific WidgetInteractionUnion type, against
  general deprecated type WidgetInteraction.

#### Poll

***

* **createPollVote**: Deprecated.
* **updatePollVote**: Deprecated.
* **input PollVoteCreateInput**: Deprecated.
* **input PollVoteUpdateInput**: Deprecated.
* **createTextPollVote**: Create a vote on Text Poll Widget.
* **updateTextPollVote**: Update a vote on Text Poll Widget.
* **createImagePollVote**: Create a vote on Image Poll Widget.
* **updateImagePollVote**: Update a vote on Image Poll Widget.
* **createTextPoll**: Support for managing localization
* **createImagePoll**: Support for managing localization

#### RichPost

***

* **createRichPost**: Support for managing localization.

#### Prediction

***

* **textPrediction**: Get a Text Prediction by id.
* **textPredictionFollowUp**: Get a Text Prediction Follow up by id.
* **imagePrediction**: Get a Image Prediction by id.
* **imagePredictionFollowUp**: Get a Image Prediction Follow up by id.
* **createTextPrediction**: Create a Text Prediction.
* **createTextPredictionFollowUp**: Create a Text Prediction Follow Up.
* **createImagePrediction**: Create a Image Prediction.
* **createImagePredictionFollowUp**: Create a Image Prediction Follow Up.
* **createTextPredictionVote**: Vote on a Text Prediction.
* **updateTextPredictionVote**: Update a Vote on a Text Prediction.
* **createImagePredictionVote**: Vote on a Image Prediction.
* **updateImagePredictionVote**: Update a Vote on a Image Prediction.

#### Quiz

***

* **textQuiz**: Get a Text Quiz by id.
* **imageQuiz**: Get a Image Quiz by id.
* **createTextQuiz**: Create a Text Quiz.
* **createImageQuiz**: Create a Image Quiz.
* **publishTextQuiz**: Publish a Text Quiz.
* **publishImageQuiz**: Publish a Image Quiz.
* **createTextQuizAnswer**: Answer a Text Quiz.
* **updateTextQuizAnswer**: Update an answer on a Text Quiz.
* **createImageQuizAnswer**: Answer a Image Quiz.
* **updateImageQuizAnswer**: Update an answer on a Image Quiz.


#### Alert

***

* **alert**: Get a Alert by id.
* **videoAlert**: Get a Video Alert by id.
* **createAlert**: Create a Alert.
* **createVideoAlert**: Create a Video Alert.
* **publishAlert**: Publish a Alert.
* **publishVideoAlert**: Publish a Video Alert.