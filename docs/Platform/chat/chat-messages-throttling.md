---
title: Chat Messages Throttling
excerpt: Throttling controls how frequently fans can send chat messages in a room
deprecated: false
hidden: false
metadata:
  robots: index
---
Chat message throttling helps reduce spam and maintain healthy conversation flow without completely disabling chat activity. For example, if a room's throttling is set to 30 seconds, a user can only send one message every 30 seconds to that room. Use cases for throttling messages include:

* **Spam Prevention:** Prevent a single fan from flooding a chat with rapid messages.
* **Room-Specific Throttling:** Apply different throttle policies per room depending on audience size or event type.
* **Fair Participation:** Ensure all fans have a chance to contribute to the discussion.

## How throttling works

Each room has an optional message throttle control, specified in seconds, and a value of zero disables the throttle. Different chat rooms can have different throttle values.

Throttling is enforced by the [Send a Chat Message](ref:send-chat-message) API. When a user sends too many messages and exceeds the throttle, the API will return a 429 Too Many Requests status code.

## Configuring throttling via the CMS

The "message throttle" field controls the throttle setting for that room. The field is available when creating new chat rooms and when editing existing ones.

<Image align="center" border={false} caption="Message throttle can be set when creating a new room." src="https://files.readme.io/afe24456b3ca614fb4db090bc972f8a426ced3e5ebb1fd7e8b15857935ef7723-Screenshot_2025-09-11_at_13.04.28.png" />

<br />

<Image align="center" border={false} caption="Message throttle can be set when editing an existing room." src="https://files.readme.io/3c84a032cedd61fc3679f4be74e75b68bf323c1a9b2f71a7ac6510716bcce770-Screenshot_2025-09-11_at_12.53.05.png" />

## Configuring throttling via the API

Set the throttle in the `chat_message_throttle_seconds` field to the [Create a Chat Room](ref:create-chat-room) and [Update a Chat Room](ref:update-a-chat-room) API endpoint.
