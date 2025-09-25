---
title: Core Concepts
deprecated: false
hidden: false
metadata:
  robots: index
---
The LiveLike SDK transforms watching live video from a passive experience into an active, interactive event. Producers can publish engagement content alongside the video, while viewers connect with each other through chat, reactions, and other interactive features.

Note: LiveLike does not provide its own video player or require any specific player. However, we do offer plug-ins for common players that enable advanced features like spoiler prevention.

## Widgets

Widgets are interactive elements published during a live event. They give audiences a way to participate in real time while staying connected to the action.
Examples include:

* Polls
* Quizzes
* Predictions
* Mini-games

Widgets are typically published by a producer through the Producer Suite, but they can also be published programmatically via the REST API.

Learn more: [Widgets](https://docs.livelike.com/v1_doc_rewire_vk/update/docs/widgets#/)

## Chat

LiveLike provides a flexible chat system to keep your audience engaged:

* Public Chat: Open rooms where everyone can react and comment in real time, building hype and excitement around the event.
* Group Chat: Private spaces for friends or closed communities to watch and chat together — without switching apps.

Learn more: [Chat](https://docs.livelike.com/v1_doc_rewire_vk/update/docs/chat#/)

## Spoiler Prevention

Avoid the frustration of spoilers. The LiveLike SDK is designed with spoiler prevention in mind:

* Interactions and chat messages are synchronized to video events
* Audiences only see widgets and messages when the timing matches their playback position

This ensures users stay in sync with the action, even if they’re watching with different delays.

## User Profiles

Every interaction is tied to a User Profile, which represents a single identity across the LiveLike experience.
Profiles can be:

* Linked to your existing user accounts
* Provisioned anonymously for quick, lightweight experiences
  Profiles store user activity across widgets, chat, and other features, enabling you to build personalized engagement journeys.

Learn More: [User Profiles](https://docs.livelike.com/v1_doc_rewire_vk/update/docs/profiles#/)

<br />
