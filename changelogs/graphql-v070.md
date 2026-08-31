---
title: GraphQL v0.7.0
author: Jordanco Trpcevski
hidden: false
published_at: '2024-06-28T09:10:03.762Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Social Graph, Badges, Widgets, Polls, Comments. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Social Graph

***

* **profileRelationships**: Get all profile relationships.
* **createProfileRelationship**: Create a profile relationship by ID.
* **deleteProfileRelationship**: Delete a profile relationship by ID.
* **profileRelationshipType**: Get a profile relationship type by ID.
* **profileRelationshipTypes**: Get all profile relationship types.
* **createProfileRelationshipType**: Create a new profile relationship type.
* **deleteProfileRelationshipType**: Delete a profile relationship type by ID.

#### Badge

***

* **badge**: Get a badge by ID.
* **badges**: Get all badges.

#### Widget

***

* **widgetReports**: Get all widget reports.
* **reportWidget**: Report a widget by ID.

#### Poll

***

* **createImagePoll**: Voting on image poll sets profile earned rewards.
* **createTextPoll**:  Voting on text poll sets profile earned rewards.

#### Comment

***

* **deleteComment**: Delete a comment by ID.