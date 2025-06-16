---
title: Deleting chat messages
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: web-delete-chat-message
      title: Deleting chat messages on Web
    - type: endpoint
      slug: delete-a-chat-room-message
      title: Delete A Chat Room Message
---
TODO: How do messages get deleted? Chat messages can be deleted through moderator actions or by integration logic.

TODO: What does it mean to delete a message? What are the integration points?

TODO: Who can delete messages? How can that be customized?

## Handling deleted messages

Integrations may need to handle more than one scenario depending on their implementation details

When a chat message is deleted, a few things happen:

- The chat message is removed from history, but may still be in cached API responses
- If the message was pinned, the related pin is also deleted
- A `message-deleted` pub/sub event is published containing details of the deleted message

The [Get Chat Messages](ref:get-chatroom-messages) API may return deleted messages in its cached results.

The pub/sub events for chat rooms are immutable, so a deleted message will have two events: one for the message being sent, and another for the message being deleted. Clients should filter messages accordingly.

## Delete a chat message by ID

Chat messages can be deleted by ID through the client SDKs.

TODO: Add snippets for Swift and Kotlin

```javascript
LiveLike.deleteMessage({ 
  roomId: "example-room-id",
  messageId: "example-message-id"
}).then((res) => console.log(res))
```

Server integrations can also delete messages using the [Delete A Chat Room Message](ref:delete-a-chat-room-message) endpoint.

## Deleted message pub/sub event

The `message-deleted` event is published to the chat room's pub/sub channel when a message is deleted.

TODO: Add sample deleted message payload

```json json
{
  "event": "message-deleted",
  "payload": {
  }
}
```