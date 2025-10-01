---
title: Spoiler-Free Chat Scenarios
excerpt: A guide on how various chat scenarios are affected by Spoiler Prevention
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Glossary

* `Message List` - The list of spoiler free messages
* `Unsynchronized Message Queue` - A sorted queue of messages that may contain spoilers. Will be checked periodically for eligible messages for synchronization (tMessage \<= tClock)
* `tClock` -  the current time of the synchronizing clock
* `tMessage` - the time of the synchronizing clock when message was sent

## Spoiler Prevention Overview

Spoiler Prevention works by delaying messages from being displayed until the user has reached a tClock >= tMessage. Spoiler Prevention prioritizes hiding potential spoiler message over perfect message ordering - when loading history and/or receiving new messages the message list isn't guaranteed to be in order of tMessage.

* Loading Initial History - Messages in the initial history where tMessage \<= tClock will be sorted and **initialize** the `Message List`. Messages in the initial history where tMessage > tClock will be sorted into the `Unsynchronized Message Queue` and eventually be **appended** to the `Message List`.
* Loading More History - Similar to Loading Initial History - messages in the history where tMessage \<= tClock will be sorted and **prepended** to the `Message List`. Messages in the history where tMessage > tClock will be sorted into the `Unsynchronized Message Queue` and eventually be **appended** to the `Message List`.
* New Messages - New Messages will always be sorted into the `Unsynchronized Message Queue`. When a message is eligible for synchronization (tMessage \<= tClock) it will be **appended** to the `Message List`.

## Scenario 1 - Initial History Load

tClock = 15\
Message List = \[]

1. User requests initial history with tMessages = \[0, 25, 10, 15, 20, 5, 30]
   * Message list = \[0, 5, 10, 15]
   * Unsynchronized Message Queue = \[20, 25, 30]
2. User moves to tClock = 20
   * Message list = \[0, 5, 10, 15, 20]
   * Unsynchronized Message Queue = \[25, 30]

## Scenario 2 - New Message with tMessage \<= tClock

tClock = 20\
Message List (tMessage) = \[5, 10, 20]

1. User receives new message with tMessage = 15. 
   * Message List = \[5, 10, 20, 15]
   * Unsynchronized Message Queue = \[]

## Scenario 3 - New Message with tMessage > tClock

tClock = 15\
Message List (tMessage) = \[5, 10, 15]

1. User receives new message with tMessage = 20
   * Message List = \[5, 10, 15]
   * Unsynchronized Message Queue = \[20]
2. User moves to tClock = 20
   * Message List = \[5, 10, 15, 20]
   * Unsynchronized Message Queue = \[]

## Scenario 4 - Load More History with tClock in Range of tMessage

tClock = 15\
Message List (tMessage) = \[5, 10 ,15]

1. User requests more history with tMessages = \[0, 20, 25]
   * Message List = \[0, 5, 10, 15]
   * Unsynchronized Message Queue = \[20, 25]
2. User moves to tClock = 20
   * Message List = \[0, 5, 10, 15, 20]
   * Unsynchronized Message Queue = \[25]
3. User moves to tClock = 25
   * Message List = \[0, 5, 10, 15, 20, 25]
   * Unsynchronized Message Queue = \[]

## Scenario 5 - Load More History with tClock >= Min tMessage

tClock = 30\
Message List (tMessage) = \[10, 20 ,30]

1. User requests more history with tMessages = \[5, 15, 25]
   * Message List = \[5, 15, 25, 10, 20 ,30]
   * Unsynchronized Message Queue = \[]

## Scenario 6 - Load More History with tClock \< Max tMessage

tClock = 15\
Message List (tMessage) = \[5, 10, 15]

1. User requests more history with tMessages = \[25, 20, 30]
   * Message List = \[5, 10, 15]
   * Unsynchronized Message Queue = \[20, 25, 30]
2. User moves to tClock = 20
   * Message List = \[5, 10, 15, 20]
   * Unsynchronized Message Queue = \[25, 30]
3. User moves to tClock = 25
   * Message List = \[5, 10, 15, 20, 25]
   * Unsynchronized Message Queue = \[30]
