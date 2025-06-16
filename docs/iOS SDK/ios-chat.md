---
title: Chat
excerpt: An overview on Chat systems of the EngagementSDK
deprecated: false
hidden: false
metadata:
  title: Chat | iOS SDK | LiveLike Developer Hub
  description: >-
    Check out this overview on iOS Chat systems of the Engagement SDK to learn
    about chat rooms, chat messages, chat sessions, and more.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Chat Room"
}
[/block]
A Chat Room is an entity that contains *Users* and *Chat Messages*. It is a persistent entity that can be connected to and **interacted** with.

For more information see [Chat Rooms](doc:chat-rooms-1) 

[block:api-header]
{
  "title": "Chat Message"
}
[/block]
A Chat Message is an entry into a Chat Room. It contains a body of content (text, images and gifs, *Stickers* ,etc.). It also contains information about the sender and when it was created. A message can be interacted with in various ways including Reactions.

[block:api-header]
{
  "title": "Chat Session"
}
[/block]
A Chat Session represents a connection to a Chat Room. You can read and interact with a Chat Room via a Chat Session.

For more information see [Chat Session](doc:chat-session) 

[block:api-header]
{
  "title": "ChatViewController"
}
[/block]
A UIViewController provided out-of-the-box in the EngagementSDK. This is a plug and play UI that enables you to integrate Chat and many of it's features into your application very quickly. There are options for customizing cosmetic details of the UI.

See [ChatViewController](doc:chat-configuration)