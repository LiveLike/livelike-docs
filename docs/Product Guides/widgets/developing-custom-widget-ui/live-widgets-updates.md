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

## Configuring PubNub

The PubNub SDK must be initialized with an *origin* and a *subscribe key* in order to subscribe to channels. The configuration details are available on the <Glossary>Application Resource</Glossary> for your application. The origin is inside the `pubnub_origin` property, and the subscribe key is inside the property `pubnub_subscribe_key`.

```javascript
var pubnub = new PubNub({
  origin: livelikeAppResource.pubnub_origin,
  subscribeKey: livelikeAppResource.pubnub_subscribe_key
})
```

> 🚧 Make sure to use the specified origin and subscribe key!
>
> Your client won't receive updates unless both the LiveLike origin and the subscribe key are configured in the PubNub client.

## Subscribing to Channels

Any resource that can be subscribed to will have a `subscribe_channel` property in its resource response. Subscribing to that channel with the PubNub SDK will start listening for updates to that resource.

## Poll Result Updates

Poll widgets have results updates published periodically while they are active. The update is a message delivered over the PubNub channel associated with the widget. It has an `event` named `"text-poll-results"` for Text Polls, and `"image-poll-results"` for Image Polls. The payload is a list of objects containing an ID of an option and its current vote count.

```json text-poll-results.json
{
  "event": "text-poll-results",
  "payload": {
    "id": "b02f5c9a-f365-44dd-8a9c-8aec9cd84fee",
    "kind": "text-poll",
    "options": [
      {
        "id": "579c15f2-4cec-418f-926b-ed2a770e2c1a",
        "vote_count": 1
      },
      {
        "id": "9c72e228-906f-4b5d-a649-ec8e93e09028",
        "vote_count": 0
      }
    ]
  }
}
```
```json image-poll-results.json
{
  "event": "image-poll-results",
  "payload": {
    "options": [
      {
        "id": "579c15f2-4cec-418f-926b-ed2a770e2c1a",
        "vote_count": 1
      },
      {
        "id": "9c72e228-906f-4b5d-a649-ec8e93e09028",
        "vote_count": 0
      }
    ]
  }
}
```

## Quiz Result Updates

Quiz widgets have results updates published periodically while they are active. The update is a message delivered over the PubNub channel associated with the widget. It has an `event` named `"text-quiz-results"` for Text Quizzes, and `"image-quiz-results"` for Image Quizzes. The payload is a list of objects containing an ID of a choice and its current answer count.

```json text-quiz-results.json
{
  "event": "text-quiz-results",
  "payload": {
    "id" "a02f5c9a-f365-44dd-8a9c-8aec9cd84fee",
    "kind": "text-quiz",
    "choices": [
      {
        "id": "579c15f2-4cec-418f-926b-ed2a770e2c1a",
        "answer_count": 1
      },
      {
        "id": "9c72e228-906f-4b5d-a649-ec8e93e09028",
        "answer_count": 0
      }
    ]
  }
}
```
```json image-quiz-results.json
{
  "event": "image-quiz-results",
  "payload": {
    "choices": [
      {
        "id": "579c15f2-4cec-418f-926b-ed2a770e2c1a",
        "answer_count": 1
      },
      {
        "id": "9c72e228-906f-4b5d-a649-ec8e93e09028",
        "answer_count": 0
      }
    ]
  }
}
```

## Cheer Meter Updates

```json
{
  "event": "cheer-meter-results",
  "payload": {
    "id": "d02f5c9a-f365-44dd-8a9c-8aec9cd84fee",
    "kind": "cheer-meter",
    "options": [
      {
        "id": "579c15f2-4cec-418f-926b-ed2a770e2c1a",
        "vote_count": 1
      },
      {
        "id": "9c72e228-906f-4b5d-a649-ec8e93e09028",
        "vote_count": 0
      }
    ]
  }
}
```
