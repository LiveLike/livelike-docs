---
title: Threads in Chat
excerpt: Replying to messages in chat using threads
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Threads enhance the chat experience by allowing users to create focused and organized conversations within a chat room. This feature helps users follow and participate in specific discussions without losing context in the overall chat.

## What is a Thread?

A thread is a sequence of messages that originate from a single parent message. Users can start a thread by replying to an existing message, and all replies in the thread are grouped together under the parent message. Threads provide a clear and structured way to manage discussions on particular topics.

## Key Characteristics of Threads

- **How a thread is created:** Threads are started by replying to a message in the chat. Each thread has a parent message, which is the message that other messages are replying to. Once a message has at least one reply, it is considered a thread.
- **Parent Message ID:** The parent message ID is a crucial identifier in the thread feature. It links each reply to the original message that started the thread. When a message is part of a thread, it includes a `parent_message_id` that points to the ID of the parent message. Standalone messages (not part of a thread) have a `parent_message_id` set to null.
- **No nesting inside of threads:** Threads are limited to a single level of replies. This means that replies within a thread cannot start another thread.
- **Thread reply count:** Each parent message of a thread tracks the count of replies it has received. This count provides a quick overview of the activity within the thread, helping users gauge the extent of discussions.
- **Reactions work with replies too:** Reactions can be added to replies inside threads just like regular chat messages.

## Using Threads in the Chat

- **Starting a Thread:**  To start a thread, reply to any existing message in the chat by setting the `parent_message_id` field of your message to the ID of the message you're replying to. Your reply will be grouped under the parent message, initiating a new thread.  [Send ChatRoom Message](https://docs.livelike.com/reference/send-chat-message)
- **Viewing Threads:** Threads are visually distinct, often nested under the parent message. Filter chat messages by `parent_message_id` to load past messages for a specific thread. [Get ChatRoom Messages](https://docs.livelike.com/reference/get-chatroom-messages)
- **Participating in Threads**: When participating in a thread, your replies will automatically be linked to the parent message, keeping the conversation organized.