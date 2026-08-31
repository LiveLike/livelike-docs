---
title: GraphQL v0.9.0
author: Akshay Garg
hidden: false
published_at: '2024-09-05T06:23:34.997Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Ban, Badge, Quests. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Ban

***

* **createProgramBan**: Create an program ban for profile.
* **deleteProgramBan**: Delete program ban by ID.
* **programBans**: Get all program bans by program ID and profile ID .

#### Badge

***

* **badgeProfiles**: Get all profiles by badge ID.

#### Quests

***

* **createQuest**: Create a quest.
* **createUserQuest**: Create a user quest.
* **quests**: Get all quests by client ID.