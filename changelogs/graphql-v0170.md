---
title: GraphQL v0.17.0
author: Akshay Garg
hidden: true
published_at: '2026-11-16T11:39:48.681Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This release adds count fields directly to Reaction Space and Comment Board, so counts can be fetched in the same query as the parent object.

### Release Changes

#### Reaction

***

* **ReactionSpace.reactionSpaceCount**: New field on `ReactionSpace` that returns its related`ReactionSpaceCount type`

#### Comment

***

* **CommentBoard.commentBoardCount**: New field on `CommentBoard` that returns its related`CommentBoardCount type`