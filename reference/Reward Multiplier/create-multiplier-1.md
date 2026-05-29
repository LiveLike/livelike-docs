---
api:
  file: applications.json
  operationId: post_client-id-reward-multipliers-2
hidden: true
link:
  new_tab: false
metadata:
  robots: noindex
---
The Create Reward Multiplier API allows creation of reward multipliers that increase user-earned rewards from eligible sources such as streaks, tiers, and other rewardable systems.

Reward multipliers support two activation types:

## User-earned / User-activated

Earned through a rewardable source and activated by the user after earning. For this type, `active_duration` is required and defines how long the multiplier remains effective for eligible transactions after activation.

## Automatic

Automatically applied to all users during a configured time window and valid only between the `started_at` and `stopped_at` timestamps.

Reward multipliers can be configured to apply to specific reward items using `reward_item_ids` and can include custom metadata through `attributes`.

When created, a reward multiplier is saved in a **draft** state, allowing its configuration and attributes to be updated if required. The multiplier must be **explicitly published** before it becomes active and starts affecting reward transactions.