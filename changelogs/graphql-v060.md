---
title: GraphQL v0.6.0
author: Jordanco Trpcevski
hidden: false
published_at: '2024-05-27T08:30:49.524Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Schema Public Access, Leaderboard, Reward and Profile. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Schema

***

GraphQL schema graph and it's federation subgraph publicly available.

* [Graph](https://graphql-schema.livelikecdn.com/schema.generated.graphql)
* [SubGraph](https://graphql-schema.livelikecdn.com/schema.subgraph.generated.graphql)

#### Leaderboard

***

* **leaderboard**: Get a specific leaderboard by ID.
* **leaderboards**: Get all leaderboards related to application.
* **leaderboardEntry** Get a specific leaderboard entry by ID.
* **leaderboardEntries** Get all leaderboard entries related to application.

#### Reward

***

* **rewardBalance**: Get a specific reward balance for given profile and reward ID.
* **rewardBalances**: Get all reward balances for given profile and reward ID's.

#### Profile

***

* **blockedProfileIds**: Get all blocked profile ID's.
* **blockProfile**: Block given profile by ID.
* **deleteProfileBlock**: Unblock specific profile by blocked ID.

Type **Profile** is extended to contain relation type **rewardBalance** and **rewardBalances** data.

#### Poll

***

Type **PollVote** is extended to contain relation type **rewards** data.