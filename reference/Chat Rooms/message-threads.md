---
title: Using Message Threads
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: endpoint
      slug: send-chat-message
      title: Send a Chat Message
---
## Introduction to Threads

Threads enhance the chat experience by allowing users to create focused and organized conversations within the main chat. This feature helps users follow and participate in specific discussions without losing context in the overall chat flow.

## What is a Thread?

A thread is a sequence of messages that originate from a single parent message. Users can start a thread by replying to an existing message, and all replies in the thread are grouped together under the parent message. Threads provide a clear and structured way to manage discussions on particular topics.

## Key Characteristics of Threads

**Thread Creation:**

Users can start a thread by replying to any existing message in the chat.\
Each thread has a parent message, which is the message that started the thread.

**No Nested Threads:**

Threads are limited to a single level of replies. This means that replies within a thread cannot start another thread.

**Parent Message ID:**

The parent message ID is a crucial identifier in the thread feature. It links each reply to the original message that started the thread.\
When a message is part of a thread, it includes a `parent_message_id` that points to the ID of the parent message.\
Standalone messages (not part of a thread) have a `parent_message_id` set to null.

**Thread Message Count:**

Each parent message in a thread displays the count of replies it has received.\
This count provides a quick overview of the activity within the thread, helping users gauge the extent of discussions.

## Using Threads in the Chat

**Starting a Thread:**  To start a thread, reply to any existing message in the chat. Your reply will be grouped under the parent message, initiating a new thread.  [Send ChatRoom Message](https://docs.livelike.com/reference/send-chat-message)\
**Viewing Threads:** Threads are visually distinct, often nested under the parent message. You can expand or collapse threads to follow specific discussions. [Get ChatRoom Messages](https://docs.livelike.com/reference/get-chatroom-messages)\
**Participating in Threads**: When participating in a thread, your replies will automatically be linked to the parent message, keeping the conversation organized.

## Summary

Threads are a powerful feature designed to keep chat conversations organized and focused. By allowing users to group related messages together under a parent message, threads make it easier to follow and participate in discussions on specific topics.