---
title: Live Widgets Updates
excerpt: How to subscribe to data channels to receive live widget updates
deprecated: false
hidden: false
metadata:
  title: Live Widgets Updates | REST API | LiveLike Developer Hub
  description: >-
    Learn how to subscribe to data channels to receive live widget updates
    delivered by the PubNub SDK.
  robots: index
next:
  description: ''
---
All live updates for widgets are delivered by [PubNub's publish/subscribe](https://www.pubnub.com/docs/platform/quickstart/publish-subscribe). These updates are received by initializing a PubNub SDK instance and then subscribing to channels associated with the widgets you are interested in receiving updates for. The updates are delivered as PubNub messages with two properties:

* `event` is the string name of the event, ex. `text-poll-results`
* `payload` is an object containing data related to the event
[block:api-header]
{
  "title": "Configuring PubNub"
}
[/block]
The PubNub SDK must be initialized with an *origin* and a *subscribe key* in order to subscribe to channels. The configuration details are available on the <<glossary:Application Resource>> for your application. The origin is inside the `pubnub_origin` property, and the subscribe key is inside the property `pubnub_subscribe_key`.
[block:code]
{
  "codes": [
    {
      "code": "var pubnub = new PubNub({\n  origin: livelikeAppResource.pubnub_origin,\n  subscribeKey: livelikeAppResource.pubnub_subscribe_key\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Make sure to use the specified origin and subscribe key!",
  "body": "Your client won't receive updates unless both the LiveLike origin and the subscribe key are configured in the PubNub client."
}
[/block]

[block:api-header]
{
  "title": "Subscribing to Channels"
}
[/block]
Any resource that can be subscribed to will have a `subscribe_channel` property in its resource response. Subscribing to that channel with the PubNub SDK will start listening for updates to that resource.
[block:api-header]
{
  "title": "Poll Result Updates"
}
[/block]
Poll widgets have results updates published periodically while they are active. The update is a message delivered over the PubNub channel associated with the widget. It has an `event` named `"text-poll-results"` for Text Polls, and `"image-poll-results"` for Image Polls. The payload is a list of objects containing an ID of an option and its current vote count.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"event\": \"text-poll-results\",\n  \"payload\": {\n    \"id\": \"b02f5c9a-f365-44dd-8a9c-8aec9cd84fee\",\n    \"kind\": \"text-poll\",\n    \"options\": [\n      {\n        \"id\": \"579c15f2-4cec-418f-926b-ed2a770e2c1a\",\n        \"vote_count\": 1\n      },\n      {\n        \"id\": \"9c72e228-906f-4b5d-a649-ec8e93e09028\",\n        \"vote_count\": 0\n      }\n    ]\n  }\n}",
      "language": "json",
      "name": "text-poll-results.json"
    },
    {
      "code": "{\n  \"event\": \"image-poll-results\",\n  \"payload\": {\n    \"options\": [\n      {\n        \"id\": \"579c15f2-4cec-418f-926b-ed2a770e2c1a\",\n        \"vote_count\": 1\n      },\n      {\n        \"id\": \"9c72e228-906f-4b5d-a649-ec8e93e09028\",\n        \"vote_count\": 0\n      }\n    ]\n  }\n}",
      "language": "json",
      "name": "image-poll-results.json"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Quiz Result Updates"
}
[/block]
Quiz widgets have results updates published periodically while they are active. The update is a message delivered over the PubNub channel associated with the widget. It has an `event` named `"text-quiz-results"` for Text Quizzes, and `"image-quiz-results"` for Image Quizzes. The payload is a list of objects containing an ID of a choice and its current answer count.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"event\": \"text-quiz-results\",\n  \"payload\": {\n    \"id\" \"a02f5c9a-f365-44dd-8a9c-8aec9cd84fee\",\n    \"kind\": \"text-quiz\",\n    \"choices\": [\n      {\n        \"id\": \"579c15f2-4cec-418f-926b-ed2a770e2c1a\",\n        \"answer_count\": 1\n      },\n      {\n        \"id\": \"9c72e228-906f-4b5d-a649-ec8e93e09028\",\n        \"answer_count\": 0\n      }\n    ]\n  }\n}",
      "language": "json",
      "name": "text-quiz-results.json"
    },
    {
      "code": "{\n  \"event\": \"image-quiz-results\",\n  \"payload\": {\n    \"choices\": [\n      {\n        \"id\": \"579c15f2-4cec-418f-926b-ed2a770e2c1a\",\n        \"answer_count\": 1\n      },\n      {\n        \"id\": \"9c72e228-906f-4b5d-a649-ec8e93e09028\",\n        \"answer_count\": 0\n      }\n    ]\n  }\n}",
      "language": "json",
      "name": "image-quiz-results.json"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Cheer Meter Updates"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"event\": \"cheer-meter-results\",\n  \"payload\": {\n    \"id\": \"d02f5c9a-f365-44dd-8a9c-8aec9cd84fee\",\n    \"kind\": \"cheer-meter\",\n    \"options\": [\n      {\n        \"id\": \"579c15f2-4cec-418f-926b-ed2a770e2c1a\",\n        \"vote_count\": 1\n      },\n      {\n        \"id\": \"9c72e228-906f-4b5d-a649-ec8e93e09028\",\n        \"vote_count\": 0\n      }\n    ]\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]