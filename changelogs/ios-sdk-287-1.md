---
title: iOS SDK 2.87
author: jelzon monzon
hidden: false
published_at: '2024-05-23T20:48:28.877Z'
---
# What's New?

* Chat - Exposes `clientMessageID` and `id` in `ChatMessage`. `clientMessageID` is assigned by the SDK when sending a message. This can be used to re-reference the chat message when the server responds. `id` is the identifier assigned by the server and should be used for other chat operations such as moderation and reactions.

# Bugfixes

* Chat UI - Fixes chat reaction hint image not disappearing after a reaction is made on the message
* Chat - Fixes a 400 error when sending a message in a spoiler prevention chat room
* Chat - Fixes an issue when using "high latency chat" (message polling) where messages are wrongfully ignored if they are missing "low latency chat" (realtime pubsub) data.