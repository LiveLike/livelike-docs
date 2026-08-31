---
title: GraphQL v0.10.0
author: Akshay Garg
hidden: false
published_at: '2024-09-18T11:35:59.937Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Quest, Ban and Leaderboard. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Quest

***

* **userQuests**: Get all user quests by profile ID.
* **updateUserQuestTaskProgress**: Update user quest task progress by user quest task ID.

#### Ban

***

* **commentBoardBan**: Get comment board ban by ID.
* **commentBoardBans**: List all comment board bans by profile ID and commentBoard ID.
* **deleteCommentBoardBan**: Delete comment board ban by ID.

#### Leaderboard

***

* **createLeaderboard**: Create a leaderboard.
* **updateLeaderboard**: Update leaderboard by ID.
* **deleteLeaderboard**: Delete leaderboard by ID.