---
title: Private Chat
excerpt: How to let users create and join their own chats
deprecated: false
hidden: false
metadata:
  robots: index
---
Users can create their own chat rooms with others. A private chat (aka a group chat) can be created using the Create Chat Room API, and others can join them using the Enter Chat Room API.

![609](https://files.readme.io/6e8b5f6-Private_Chat_Flow.png "Private Chat Flow.png")

> 🚧 Sharing chat room IDs between users happens outside of LiveLike
>
> Clients need to know the ID of a chat room to be able to enter it and send messages. LiveLike doesn't provide a way for users to communicate the IDs of chat rooms to each other, so an out-of-band solution like a link that includes the chat room ID is assumed.

## Create a chat room

A chat room has to be created before it can be used.  Once a chat room is created, it is assigned a unique ID that clients can then use to enter the room and send messages. That chat room ID is also what should be shared between users so that others can participate.

* [Web: Create chat room](doc:web-chat#chatroom-methods)

## Enter a chat room

Once a chat room has been created, others can enter it and send messages in it. Clients need to know the unique ID of a room to be able to enter it.

* [Web: Enter chat room](doc:web-chat#chat-basics)
