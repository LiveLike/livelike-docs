---
title: Core Concepts
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Core Concepts | LiveLike Developer Hub
  description: >-
    In the LiveLike Developer Hub, you'll find all the information you need to
    navigate widgets, live chats, spoiler prevention, user profiles, and more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: widgets
      title: Widgets
    - type: basic
      slug: chat
      title: Chat
    - type: basic
      slug: spoiler-free-sync
      title: Spoiler-Free Sync
    - type: basic
      slug: user-profiles
      title: Profiles
---
The LiveLike SDK converts the experience of watching live video from a passive one to an active one. Producers publish interactive content related to the video, and audience members can watch with others and communicate through chat, reactions and more. The SDKs don't provide a video player or require any specific player, but they do provide plug-ins for common players to support advanced features like spoiler prevention.

## Widgets

The various interactive elements that get published during live video are called *widgets*. The library of widgets is always expanding and features things like polls, quizzes, and predictions. Widgets are usually published by a producer using the Producer Suite, but they can also be published through the REST API. See [Widgets](widgets) for more info.

![1387](https://files.readme.io/b948e1d-Screen_Recording_2020-04-03_at_05.02_PM.gif "Screen Recording 2020-04-03 at 05.02 PM.gif")

## Chat

LiveLike offers a chat experience that can be customized to offer public and group chat. Public rooms are open to anybody, group chats are limited to members that have access to the group.

Public chat creates a sense of excitement around the video with lots of reactions around the action. Group chat reduces app switching and enables friends to watch together. See [Chat](chat) for more info.

![1386](https://files.readme.io/a335c1f-Core_Concepts-chat.gif "Core Concepts-chat.gif")

## Spoiler Prevention

There's often nothing worse than an ill-timed spoiler when you're watching a nail-biting finish. The engagement SDK was built with spoiler prevention in mind. User interactions are tied to events in the video feed, thereby minimizing the chances that users see spoilers in producer-driven widgets or chat messages from others. See [Spoiler Prevention](spoiler-free-sync) for more info.

## User Profiles

Profiles are used to collect user activity within widgets, chat and other features, inside a single identity. Profiles can be provisioned arbitrarily, and so they can be used to either extend your existing user account records or build anonymous experiences. See [Profiles](user-profiles) for more info.
