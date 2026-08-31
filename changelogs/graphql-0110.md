---
title: GraphQL v0.11.0
author: Akshay Garg
hidden: false
published_at: '2024-10-09T07:16:44.401Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Social Graph, Widget and Poll. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Social Graph

***

* **profileRelationshipType**: Get a profile relationship type by ID.
* **profileRelationshipTypes**: Get Profile relationship types by clientId and key.

#### Widget

***

* **widgets**: Get a list of widgets is extended to contain **customData**, and optional include current auth user vote field **userVote** of type **WidgetInteraction** for types **TextPoll**, **ImagePoll**, **RichPost**.

#### Poll

***

* **createPollVote**: Create a poll of kind TextPoll, ImagePoll is extended to return its respective **Widget** type.
* **updatePollVote**: Update a poll of kind TextPoll, ImagePoll is extended to return its respective **Widget** type.
* **createTextPoll**: Create a TextPoll is extended to optional include current auth user vote field **userVote**\
  of type **WidgetInteraction**.
* **createImagePoll**: Create a ImagePoll is extended to optional include current auth user vote field **userVote** of type **WidgetInteraction**.
* **textPoll**: Get a TextPoll is extended to optional include current auth user vote field **userVote** of type\
   **WidgetInteraction**.
* **imagePoll**: Get a ImagePoll is extended to optional include current auth user vote field **userVote** of type\
  **WidgetInteraction**.