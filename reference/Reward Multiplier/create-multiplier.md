---
api:
  file: applications.json
  operationId: post_client-id-reward-multipliers
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
The Create Reward Multiplier API allows creation of reward multipliers that gives users a boost in earning rewards for a specific time period from all rewardable interactions, tied to a specific reward item.

There are two types of reward multipliers, based on their activation method:

## User-earned / User-activated

Earned through a rewardable source such as streak milestone, tier benefit, etc. and then manually activated by a user after earning. For this type, it is mandatory to set an `active_duration` which determines how long the multiplier remains effective, once activated. The multiplier, when active, is applicable to all rewardable interactions tied to that reward item for which the multiplier was earned.

## Automatic

Automatically activated for all users (or selected user groups) during a pre-configured time window. For this type, users do not need to separately earn a the reward multiplier or manually activate it. Multiplier remains effective only between the `started_at` and `stopped_at` timestamps set at the time of configuring.

Reward multipliers can be configured to effect specific reward items or user groups using `reward_item_ids` and `profile_groups_ids`, and can include custom metadata through `attributes`.

When created, a reward multiplier is saved, by default, in a **draft** state, allowing its configuration and attributes to be updated, if required. The multiplier must be **explicitly published** before it becomes usable and starts affecting reward transactions.