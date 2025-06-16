---
title: List User Quests
excerpt: ''
api:
  file: engagement-suite.json
  operationId: list-user-quests
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
### List Current Quests

Use the `status=incomplete` and `profile_id` query parameters to show all the current quests for a given user.

### Show Past Completed Quests

Use the `status=completed` and `profile_id` query parameters to show all past quests completed by the given user.

### List Completed Quests with Unclaimed Rewards

Use the `status=completed` and `rewards_status=unclaimed` to list only completed quests that still have rewards pending. Quests can be filtered to specific users with the `profile_id` query parameter, or all users of a given app with the `client_id` parameter.