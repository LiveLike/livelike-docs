---
title: Delivery Channel – SQS
excerpt: SQS Events
deprecated: false
hidden: true
metadata:
  robots: index
---
### To enable sending events to SQS, application needs to have below details:

* Enable SQS Events
* Valid Sqs Event Queue Url
* SQS queue will be shared between LiveLike and client.

# What Are SQS Events?

SQS (Simple Queue Service) Events allow the LiveLike platform to deliver event notifications to your application via an AWS SQS queue. Instead of polling for updates, your systems can consume events asynchronously from a shared queue as they occur. This enables scalable, reliable event-driven workflows for moderation and engagement features.

# Key Concepts

* SQS Queue URL: The AWS SQS endpoint where LiveLike will deliver event payloads.
* Event Key: A string identifier that describes the type of event (e.g., create-chatroom-mute).
* Event Payload: The JSON body sent to the queue containing the event key and associated data.
* Shared Queue: The SQS queue is shared between LiveLike and the client application.
* Event Subscriptions: You can subscribe to specific event types relevant to your use case.

# Subscription Details

### To enable SQS event delivery for your application, the following must be configured:

1. Enable SQS Events on the application.
2. Provide a valid SQS Event Queue URL.

Both are required. The SQS queue will be shared between LiveLike and the client. Please contact your LiveLike Admin to configure these settings.

# SQS Event Types

You can subscribe to specific events that match your business needs. The following event categories are currently supported:

## Comment Board Moderation Events

These events are triggered by moderation actions on comment boards.

### Event Keys:

`CREATE_COMMENT_BOARD_BAN_EVENT_KEY = "create-comment-board-ban"
UPDATE_COMMENT_BOARD_BAN_EVENT_KEY = "update-comment-board-ban"
DELETE_COMMENT_BOARD_BAN_EVENT_KEY = "delete-comment-board-ban"`

### Event Payload Structure:

`{
    "event_key": "<EVENT_KEY>",
    "event_data": {
        "id": "<uuid>",
        "comment_board_id": "<uuid>",
        "banned_by_profile_id": "<uuid>",
        "banned_profile_id": "<uuid>",
        "created_at": "<DateTime>",
        "description": "string"
    }
}`

## Chat Room Moderation Events

These events are triggered by mute and shadow-mute moderation actions within chat rooms.

### Event Keys:

CREATE_CHATROOM_MUTE = "create-chatroom-mute"
CREATE_GLOBAL_CHATROOM_MUTE = "create-global-chatroom-mute"
CREATE_CHATROOM_SHADOW_MUTE = "create-chatroom-shadow-mute"
CREATE_GLOBAL_CHATROOM_SHADOW_MUTE = "create-global-chatroom-shadow-mute"
UPDATE_CHATROOM_MUTE = "update-chatroom-mute"
UPDATE_GLOBAL_CHATROOM_MUTE = "update-global-chatroom-mute"
UPDATE_CHATROOM_SHADOW_MUTE = "update-chatroom-shadow-mute"
UPDATE_GLOBAL_CHATROOM_SHADOW_MUTE = "update-global-chatroom-shadow-mute"
DELETE_CHATROOM_MUTE = "delete-chatroom-mute"
DELETE_GLOBAL_CHATROOM_MUTE = "delete-global-chatroom-mute"
DELETE_CHATROOM_SHADOW_MUTE = "delete-chatroom-shadow-mute"
DELETE_GLOBAL_CHATROOM_SHADOW_MUTE = "delete-global-chatroom-shadow-mute"

### Event Payload Structure:

`{
    "event_key": "EVENT_KEY",
    "event_data": {
        "id": "<uuid>",
        "chat_room_id": "<uuid>",
        "muted_profile_id": "<uuid>",
        "muted_by_profile_id": "<uuid>",
        "created_at": "<DateTime>"
    }
}`

## Consuming SQS Events

When an event is triggered, the payload is delivered to your SQS queue. Your application should poll the queue and process messages as they arrive. Each message contains an event_key identifying the event type and an event_data object with the relevant details.
