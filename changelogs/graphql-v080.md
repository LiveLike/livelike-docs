---
title: GraphQL v0.8.0
author: Akshay Garg
hidden: false
published_at: '2024-07-10T09:24:07.160Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on Badge, Reward, Profile. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Badge

***

* **badges**: Get all badges by application ID.
* **badgeProgress**: Get a non earned badge progress by badge and profile ID.
* **earnedBadges**: Get all earned badges by profile ID.
* **awardBadge**: Create an award badge for profile.
* **revokeEarnedBadge**: Revoke earned badge for profile.

#### Reward

***

* **rewardTable**: Get a reward table by ID.
* **rewardTables**: Get all reward tables by application ID.
* **createRewardTable**: Create reward table.
* **updateRewardTable**: Update reward table by ID.
* **deleteRewardTable**: Delete reward table by ID.
* **linkRewardTableWithProgram**: Link reward table with program ID.
* **unlinkRewardTableWithProgram** Unlink reward table with program ID.
* **invokeRewardAction**: Invoke a reward action.

#### Profile

***

Type **Profile** is extended to contain relation type to **profileRelationship**

* field **incomingProfileRelationships**: Get incoming profile relationships.
* field **outgoingProfileRelationships**: Get outgoing profile relationships.