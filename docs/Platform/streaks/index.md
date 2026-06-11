---
title: Streaks
excerpt: Reward users for consistent participation
deprecated: false
hidden: true
metadata:
  robots: index
next:
  pages:
    - slug: how-to-create-streaks-in-cms
      title: Periodic Streak CMS Guide
      type: basic
---
Streaks reward users for performing an action consistently over time or across repeated opportunities. A streak tracks a user's progress as they repeat a defined behavior - watching content, making predictions, checking in, completing challenges - and rewards them at incremental milestones as they maintain that consistency.

A streak starts when a user performs the qualifying action and continues as long as the streak rules are met. If the rules are broken, the streak resets. Rewards are granted exclusively through Streak Milestones - there is no separate streak completion reward outside of milestones.

***

## Streak Types

LiveLike supports two streak types, based on how progress is tracked:

| Type               | How Progress Works                                                    | Resets When                                                                               |
| ------------------ | --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Periodic           | User must act within a recurring time window (daily, weekly, monthly) | The window closes without the required action being completed                             |
| Consecutive Action | User must perform a qualifying action repeatedly without interruption | A configured reset action fires, or (in Sequence mode) targets are completed out of order |

***

### Periodic Streaks

A Periodic streak advances when a user performs the streak progress action within a recurring time window. Each window the user satisfies increments streak length by 1. Missing the action within a window resets the streak.

Periodic streaks are timezone-aware, based on the timezone selected during setup.

**Supported windows:** Daily, Weekly, Monthly

**Examples:**

- Make a prediction every day
- Play 2 trivia games every week
- Complete 4 challenges in a month
- Log in every day for a week

#### Threshold

Threshold lets you require more than one instance of the streak progress action within a window before streak length increments by 1.

For example, if threshold is set to 4 for a weekly streak, the user must complete the action 4 times within that week for the streak to advance by 1. Completing fewer than 4 breaks the streak.

> **Threshold and milestones:** Milestones are based on streak length, not raw action count. If threshold is 3 and a milestone is set at streak length 5, the user must satisfy the threshold 5 times - meaning 15 total qualifying actions - to reach that milestone.

Threshold is specific to Periodic streaks. Consecutive Action streaks do not have a threshold - every qualifying action increments streak length by 1 directly.

***

### Consecutive Action Streaks

A Consecutive Action streak tracks whether a user completes a qualifying action repeatedly without a failure or invalid interaction breaking the chain. Unlike Periodic streaks, time gaps between actions do not matter - only the continuity of successful actions does.

Every qualifying action increments streak length by 1.

**Examples:**

- Correctly predict 3 match outcomes in a row
- Win 5 games consecutively
- Answer 10 quiz questions correctly in a row

#### Sub-types

Consecutive Action streaks have three sub-types, determined by how targets are configured:

| Sub-type | How It Works                                                                                                                                                     |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None     | Only the action is tracked - no specific target is required. Every qualifying action increments streak length by 1, regardless of what it is performed on        |
| Set      | The action must be performed against targets from a defined list. Order does not matter. Every qualifying action on a valid target increments streak length by 1 |
| Sequence | The action must be performed against a defined list of targets in a specific order. Interacting with targets out of order resets the streak                      |

**None - Win 5 games in a row**

The streak progress action is "win a game," sub-type is None. No targets are configured. Each time the user wins a game, streak length increments by 1. If a reset action (e.g., "lose a game") is configured and fires, the streak resets to 0. Streak does not automatically reset unless a streak reset action is passed. Time gaps between games do not matter.

**Set - Predict outcomes across 3 specific matches**

The admin configures 3 match IDs as targets via CSV, sub-type is Set. Each time the user makes a correct prediction on any of the 3 matches, streak length increments by 1. Order does not matter. If a reset action fires, the streak resets. Streak does not automatically reset unless a streak reset action is passed. Actions on matches not in the set are ignored. Time gaps between games do not matter.

**Sequence - Complete a tournament bracket in order**

The admin configures 4 match IDs in sequence via CSV. The user must make a correct prediction on Match 1 first, then Match 2, then Match 3, then Match 4 - each correct prediction on the next valid target increments streak length by 1. Predicting on Match 2 before completing Match 1 automatically resets the streak. A reset action can also be configured as an additional reset trigger. Time gaps between games do not matter.

***

## Streak Progress Actions

A streak progress action can be **any action a user performs** - whether a LiveLike built-in action or any custom or CDP-driven event from outside LiveLike. There is no fixed list of supported actions.

| Action Type         | Examples                                                                                                          | Target Selection Method                                             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| LiveLike built-in   | Make a correct prediction, answer a quiz correctly, vote on a poll                                                | Dropdown in CMS, listing all available widgets of the relevant type |
| Custom / CDP-driven | Any event from outside LiveLike - match completion, login, purchase, content view, or any custom-defined behavior | CSV upload                                                          |

How the action type affects target selection is covered in **Configuring Targets** below.

***

## Configuring Targets

Targets are only applicable to Consecutive Action streaks. A target is the specific object against which the streak progress action is evaluated - for example, a specific match, widget, or episode.

Targets are defined as key-value pairs:

- The **key** is the identifier type (e.g., `match_id`, `widget_id`)
- The **value** is the actual identifier (e.g., a specific match ID)

When a user performs the streak progress action, the same key-value pair must be passed as an attribute in the action call for the system to evaluate it against the configured targets.

**Example:** If an admin uploads a CSV with the column header `match_id` and rows containing match IDs, then `match_id` is the key and each match ID is a value. The integration must pass `match_id: <value>` as an attribute when invoking the streak progress action.

Targets can reference LiveLike objects (widget IDs, game IDs) or any external identifier (match IDs, tournament IDs, episode IDs, or any identifier from outside LiveLike).

### Setting Targets: Built-in vs. CSV

How targets are selected depends on the streak progress action chosen:

| Action Type                                                                                       | Target Selection Method                                            |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Built-in widget action (e.g., make a correct prediction, answer a quiz correctly, vote on a poll) | Dropdown in CMS listing all available widgets of the relevant type |
| All other actions (custom, CDP-driven, or any non-widget built-in)                                | CSV upload. Column header is the key; rows below are the values    |

> **Common setup issue:** Progress not tracking on a Consecutive Action streak with targets is almost always caused by a mismatch between the key-value pairs configured in CMS and the attributes being passed when the action is invoked. Confirm that the key (e.g., `match_id`) and value (e.g., the specific match ID) passed in the action attributes exactly match what was configured as targets.

***

## Streak Reset Behavior

### Periodic Streaks

A Periodic streak resets when the user fails to complete the required action - or fails to meet the threshold - within the defined time window.

### Consecutive Action Streaks

A streak reset action is an action that, when performed, programmatically breaks a Consecutive Action streak.

**If no reset action is configured**, the streak has no programmatic way to break - it will only stop advancing, not reset. For None and Set sub-types especially, configuring a reset action is strongly recommended so the system can correctly invalidate progress when the user performs a failing action.

Reset action behavior varies by sub-type and action:

| Scenario                                            | Reset Behavior                                                                                                                             |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Make a correct prediction / answer a quiz correctly | The incorrect counterpart (make an incorrect prediction / answer a quiz incorrectly) is automatically assigned as the reset action         |
| All other actions (built-in, custom, CDP-driven)    | A reset action can optionally be configured. Not auto-assigned                                                                             |
| Sequence sub-type                                   | Interacting with targets out of order automatically resets the streak. A reset action can additionally be configured as a separate trigger |
| None and Set sub-types                              | No inherent ordering logic to trigger an automatic reset. A configured reset action is the only programmatic way to break the streak       |

***

## Configuring Milestones

Streak Milestones are the only mechanism through which rewards are granted within a streak. They act as checkpoints at defined streak lengths — when a user reaches a milestone, the configured rewards are automatically issued. Milestones apply to both Periodic and Consecutive Action streaks.

Configuring milestones is optional - only needed when users should be rewarded for reaching specific streak lengths.

**Examples:**

- Earn bonus points at streak lengths 3, 5, and 7
- Receive a badge on reaching a 10-day login streak
- Get a reward multiplier after correctly predicting 7 match outcomes in a row

### Milestone Types

| Type            | How It Works                                                                      |
| --------------- | --------------------------------------------------------------------------------- |
| Standard        | Triggers once when the user first reaches that streak length                      |
| Recurring       | Triggers at a fixed streak length interval (e.g., every 5 lengths)                |
| Repeat on Reset | Triggers every time a user reaches that milestone, including after a streak reset |

### Milestone Rewards

Each milestone can be configured to award one or more of the following:

| Reward Type                             | Details                                                                                                                                                                       |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Reward Items                            | Standard point grants on reaching the milestone                                                                                                                               |
| Reward Multiplier (User-Activated only) | One or more user-activated multipliers granted to the user. Only user-activated multipliers can be linked. Once granted, the user can activate it at a time of their choosing |
| Badges                                  | One or more badges awarded at the milestone. A single badge can only be attached to one milestone within a streak                                                             |

### Reward Behaviors

Reward Items and Reward Multipliers support two additional behaviors that can be enabled per milestone:

**Recurring** - The reward triggers at a fixed streak length interval (e.g., every 5 lengths), rather than only once.

**Reward on Reset** - The reward triggers every time the user reaches that milestone, even after the streak has reset and been rebuilt.

> **Badges are excluded from both behaviors.** A user can earn a badge only once - regardless of how many times a milestone is reached or how many times the streak resets. If the user already holds the badge from another experience (a quest, a tier benefit, another streak), the badge award is silently skipped while all other rewards on the same milestone are still granted.

### Milestone Stacking

If a recurring milestone and a non-recurring milestone coincide at the same streak length, both fire simultaneously and the user receives rewards from both. For example, if a recurring milestone is set at every 3 lengths and a standard milestone is set at length 15, the user receives both rewards when they reach length 15.

***

## Setting Up Streaks

Streaks are created and managed via CMS or API. The CMS setup flow is described below.

For API setup, refer to the [Periodic Streak API Guide](https://docs.livelike.com/reference/create-a-periodic-streak) and [Consecutive Action Streak API Guide](https://docs.livelike.com/reference/create-a-periodic-streak-1).

### CMS Setup Steps

1. **Name and Description** - Set a name and optional description
2. **Streak Type** - Select Periodic or Consecutive Action
3. **Streak Progress Action** - Select the action that drives streak progress. This can be any LiveLike built-in action or any custom / CDP-driven event
4. **Period and Timezone** _(Periodic only)_ - Select the recurring window (Daily, Weekly, or Monthly) and set the timezone
5. **Threshold** _(Periodic only)_ - Optionally set the number of times the progress action must be completed within the window before streak length increments by 1
6. **Streak Reset Action** _(Consecutive Action only)_ - Optionally configure the action that breaks the streak. Auto-assigned for correct prediction and correct quiz answer; optional for all others
7. **Targets** _(Consecutive Action only)_ - In the Targets tab, select the sub-type (None, Set, or Sequence). For Set and Sequence, configure targets via the built-in widget dropdown (for widget-based built-in actions) or via CSV upload (for all other actions)
8. **Start / End Time** - Optionally set a campaign window for the streak
9. **Milestones** - Optionally add milestones. For each milestone, set the streak length and configure rewards (Reward Items, Reward Multiplier, Badges). Enable Recurring and Reward on Reset behaviors as needed
10. **User Groups** - Optionally scope the streak to specific user segments. Users outside the assigned groups will not participate
11. **Save or Publish** - The streak can be saved at any point before publishing, with all fields remaining editable. Once published, the rules below apply

***

## Editing After Publishing

Once a streak is published, most configuration is locked to preserve streak integrity.

| Editable After Publishing                 | Not Editable After Publishing             |
| ----------------------------------------- | ----------------------------------------- |
| Name and description                      | Streak type                               |
| Start / End time (only if not yet passed) | Streak progress action                    |
| Streak attributes                         | Period and timezone (Periodic)            |
| Milestone attributes                      | Threshold (Periodic)                      |
| Adding or removing milestones             | Targets and sub-type (Consecutive Action) |
|                                           | Streak reset action                       |
|                                           | Existing milestone configuration          |

> Milestones can be added or removed after publishing, but the configuration of existing milestones cannot be modified.

***

## Frequently Asked Questions

### Streak Types and Setup

**What is the difference between Periodic and Consecutive Action streaks?**<br />Periodic streaks are time-based - the user must act within a recurring window to maintain the streak. Consecutive Action streaks are action-based with no time dependency - what matters is the uninterrupted success of the action, regardless of when it happens.

**When should I use None, Set, or Sequence as the Consecutive Action sub-type?**<br />Use None when you only care that the user performed the action, not what they performed it on. Use Set when the action must be performed against a defined list of targets but order does not matter. Use Sequence when the user must interact with targets in a specific order - for example, completing matches in a tournament bracket in sequence.

**What is threshold and how is it different from milestones?**<br />Threshold controls how streak length accrues - it defines how many times the action must be completed within a window before streak length increments. Milestones control what happens when it does - they define rewards at specific streak lengths. They operate at different levels and are independent of each other.

**Does Consecutive Action streak have a threshold?**
No. Every qualifying action in a Consecutive Action streak increments streak length by 1 directly. There is no batching or threshold concept.

**Can a streak be targeted to a specific audience?**
Yes. Streaks can be scoped to one or more User Groups. Users outside the assigned groups will not participate in the streak.

**Can different user groups have different streak configurations running simultaneously?**
Yes. Configure separate streak instances, each scoped to its own user group, to run parallel streak programs for different segments.

### Targets

**I set up a Consecutive Action streak with targets but progress is not tracking. What should I check?**
The most common cause is a mismatch between the target key-value pairs configured in CMS and the attributes being passed when the streak progress action is invoked. Confirm that the key (e.g., `match_id`) and value (e.g., the specific match ID) passed in the action attributes exactly match what was configured - via dropdown or CSV.

### Streak Reset

**What triggers a streak reset in a Periodic streak?**<br />Missing the required action - or failing to meet the threshold - within the defined time window.

**What triggers a streak reset in a Consecutive Action streak?**
It depends on the sub-type. For None and Set, the configured reset action triggers the reset — if no reset action is configured, the streak has no programmatic way to break. For Sequence, interacting with targets out of order resets the streak; a reset action can additionally be configured. For correct prediction and correct quiz answer, the incorrect counterpart is auto-assigned as the reset action.

**Is the streak reset action mandatory for Consecutive Action streaks?**<br />No, it is optional - except for correct prediction and correct quiz answer, where it is automatically assigned. For None and Set sub-types, configuring a reset action is strongly recommended. Without one, the streak has no programmatic way to break when the user performs a failing action.

### Milestones and Rewards

**Can I configure multiple reward types on the same milestone?**
Yes. A single milestone can combine Reward Items, a User-Activated Multiplier, and one or more Badges. Each reward type follows its own rules for recurring and reset behavior.

**Can the same badge be attached to more than one milestone within a streak?**
No. A badge can only be attached to one milestone within a streak. The same badge can be referenced across different streaks or experiences, but a user can earn it only once across all of them.

**Can I attach an automatic reward multiplier to a streak milestone?**
No. Only user-activated multipliers can be linked to streak milestones.

**If I have a recurring milestone at length 3 and a standard milestone at length 15, does the user get both rewards when they reach length 15?**
Yes. Since 15 is a multiple of 3, the recurring milestone fires at that point in addition to the standard milestone at length 15. The user receives rewards from both simultaneously.

**If my streak resets after reaching a milestone, can I re-earn the same milestone rewards?**
Whether a milestone reward is granted again after reset depends on whether Reward on Reset is enabled on that milestone. Future milestone rewards are only available if the user rebuilds their streak back to those lengths.

**A user already has a badge from a quest. Will they receive it again from a streak milestone?**<br />No. A user can earn a badge only once. If they already hold it, the badge award at that milestone is silently skipped - all other rewards on the same milestone are still granted.

**When does a user-activated reward multiplier granted at a milestone expire for earning purposes?**
Expiry for earning is governed by the multiplier's configured `start_at` / `stopped_at` window, if set. Once earned, the user can activate it at any time - there is no activation deadline based on when it was earned. Once activated, it remains live for the configured `active_duration`. If the multiplier expired before the user earned it, that reward is silently skipped without impacting other rewards configured for that milestone.
