---
title: GraphQL v0.12.0
author: Akshay Garg
hidden: false
published_at: '2024-10-30T09:19:59.114Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Ban, Reaction, Widget and Comment. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Ban

***

* **createCommentBoardBan**: Create a comment board ban to a profile to individual comment board and globally .

#### Reaction

***

* **reactionSpacesCount**: Get a list of reaction spaces counts for one or more reaction spaces.

#### Widget

***

* **widgets**: Get a list of widgets is extended to contain **createdBy**  to get creator details of a widget for types **TextPoll**, **ImagePoll**, **RichPost**.  

#### Comment

***

* **createCommentBoard**: Create a comment board is extended to input and return **contentFilter**.
* **updateCommentBoard**: Update a comment board is extended to input and return **contentFilter**.
* **commentBoard**: Get a comment board is extended to return **contentFilter**.
* **commentBoards**: Get a list of comment boards is extended to return **contentFilter** and filter it by list of comment ids.