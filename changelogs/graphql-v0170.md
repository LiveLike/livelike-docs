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

* **ReactionSpace.reactionSpaceCount**: New field on `ReactionSpace` that returns its `ReactionSpaceCount` (`reactionsCount` and `emojiCounts`). Counts can now be fetched together with the reaction space instead of through a separate `reactionSpacesCount` query. Returns `null` if no count is available.

#### Comment

***

* **CommentBoard.commentBoardCount**: New field on `CommentBoard` that returns its `CommentBoardCount` (`commentsCount` and `topLevelCommentsCount`). Counts can now be fetched together with the comment board instead of through a separate `commentBoardsCount` query. Returns `null` if no count is available.

The existing `reactionSpacesCount` and `commentBoardsCount` queries are unchanged.