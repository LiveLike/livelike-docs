---
title: Chat Avatars
excerpt: Chat avatar image is an image that appears next to a chat message.
deprecated: false
hidden: false
metadata:
  title: Chat Avatars | LiveLike Developer Hub | Fan Engagement Suite
  description: >-
    Chat avatars are images representing the sender of a chat message. Learn
    more about enabling chat avatars.
  robots: index
next:
  description: ''
---
Chat avatars are images representing the sender of a chat message.

> 📘 Avatars are properties of chat messages
>
> Chat avatars are properties on individual chat messages, not on profiles. That means that the same user can have different avatars in different rooms, or even on different messages in the same room.

## Enabling Avatars

If a chat message has a valid avatar associated, the avatar will be displayed inside of the message element. If the avatar is missing or invalid, a default avatar will be shown instead.

```html
<livelike-chat showavatar></livelike-chat>
```
```kotlin
chatsession.shouldDisplayAvatar= <true|false>
```
```swift
var config = ChatSessionConfig(roomID: "example-room-id")
config.shouldDisplayAvatar = true
```

## Setting Avatars

Setting the an avatar will cause all future messages sent by the current user to the room to use that avatar.

```html
<livelike-chat showavatar avatarurl="https://example.com/my-avatar.png" roomid="648bb105-bba4-4c3c-8017-e8f390681759"></livelike-chat>
```
```kotlin
chatsession.avatarUrl = "https://example.com/my-avatar.png"
```
```swift
chatSession.avatarURL = "https://example.com/my-avatar.png"
```
