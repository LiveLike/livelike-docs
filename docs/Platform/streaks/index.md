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
Streaks reward users for performing an action consistently over time or across repeated opportunities. A streak tracks a user's progress as they repeat a defined behavior - watching content, making predictions, checking in, completing challenges - and rewards them at incremental milestones as they maintain that consistency. A streak starts when a user performs the qualifying action and continues as long as the streak rules are met. If the rules are broken, the streak resets.

Streaks are classified into **Periodic Streaks** and **Consecutive Action Streaks**. Rewards are granted exclusively through **Streak Milestones** - there is no separate streak completion reward outside of milestones.

***

## Why Use Streaks?

Streaks help drive meaningful product outcomes by:

- Increasing user retention through habit-building
- Encouraging repeat behavior across daily, weekly, event-based, or action-based patterns
- Boosting content consumption - games, predictions, challenges, and more
- Driving deeper engagement with rewards tied to consistency
- Creating urgency and motivation through visible progress and milestone rewards

From a business perspective, streaks are especially useful for sports predictions, arcade or casual games, fitness challenges, content consumption (episodes, videos, quizzes), and loyalty and reward programs.

***

## Periodic Streaks

A Periodic streak is extended by performing an action within a recurring time window - daily, weekly, or monthly. Periodic streak is timezone-aware, based on the timezone selected during setup.

**Examples:**

- Make a prediction every day
- Play 2 trivia games every week
- Complete 4 challenges in a month
- Log in every day for a week

Missing the action within the defined window breaks the streak.

### Threshold

Threshold lets you require more than one instance of the streak progress action within a window before the streak length increments by 1. For example, if threshold is set to 4 for a weekly streak, the user must play 4 trivia games within that week for the streak to advance by 1 length. Completing fewer than 4 that week breaks the streak.

Threshold is specific to Periodic streaks.

**Threshold and Milestones:** Milestones are based on streak length, not raw action count. If threshold is 3 and a milestone is set at streak length 5, the user must satisfy the threshold 5 times - meaning 15 total qualifying actions - to reach that milestone.

***

## Consecutive Action Streaks

A Consecutive Action streak tracks whether a user successfully completes a qualifying action repeatedly without a failure or invalid interaction breaking the chain. Unlike Periodic streaks, time gaps between actions do not matter - only the continuity of successful actions does.

Every time a user performs the streak progress action - on the correct target if a target mode is configured - streak length increments by 1.

**Examples:**

- Correctly predict 3 match outcomes in a row
- Win 5 games consecutively
- Answer 10 quiz questions correctly in a row

### Sub-types

Consecutive Action streaks have three sub-types, determined by how targets are configured:

| Sub-type     | How It Works                                                                                                                                                                                                                                                                                                                                 |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **None**     | Only the action is tracked - no specific object or target is required. Every qualifying action increments streak length by 1, regardless of what it is performed on.                                                                                                                                                                         |
| **Set**      | The action must be performed against targets from a defined list. Order does not matter. Every qualifying action on a valid target increments streak length by 1.                                                                                                                                                                            |
| **Sequence** | The action must be performed against a defined list of targets in a specific order. Order is determined by position in the list - first item is Order 1, second is Order 2, and so on. Each qualifying action on the correct next target in sequence increments streak length by 1. Interacting with targets out of order resets the streak. |

### What Are Targets?

A target is the specific object against which a streak progress action is evaluated. Targets are only applicable to Consecutive Action streaks - Periodic streaks do not use targets.

Targets can be:

- **LiveLike objects** - widget IDs, game IDs, or other LiveLike-native identifiers
- **External references** - match IDs, tournament IDs, episode IDs, or any identifier from outside LiveLike

Targets are defined as key-value pairs. The key is the identifier type (e.g., `match_id`, `widget_id`) and the value is the actual identifier. When a user performs the streak progress action, the same key-value pair must be passed as an attribute in the action call for the system to evaluate it against the configured targets.

**Example:** If an admin uploads a CSV with the column header `match_id` and rows containing actual match IDs, then `match_id` is the key and each match ID is the value. The integration must pass `match_id: <value>` as an attribute when invoking the streak progress action.

### Setting Targets: Built-in vs. CSV

How targets are selected depends on the streak progress action chosen:

| Action Type                                                                                           | Target Selection Method                                                                                                                                                                                                                                |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Built-in widget action** (e.g., make a correct prediction, answer a quiz correctly, vote on a poll) | Dropdown in CMS listing all available widgets of the relevant type. Selecting "make a correct prediction" shows all prediction widgets; selecting "answer a quiz correctly" shows all quiz widgets; selecting "vote on a poll" shows all poll widgets. |
| **All other actions** (custom actions, CDP-driven actions via mParticle, Segment, etc.)               | CSV upload. Column header is the key; rows below are the values (target identifiers).                                                                                                                                                                  |

The key-value attribute passing requirement applies to all target-based streaks regardless of whether targets were configured via dropdown or CSV.

### Streak Reset Action

A streak reset action is an action that, when performed, programmatically breaks a Consecutive Action streak. It is only applicable to Consecutive Action streaks.

- For **make a correct prediction** and **answer a quiz correctly**, the system automatically assigns the incorrect counterpart (make an incorrect prediction / answer a quiz incorrectly) as the reset action.
- For all other actions - including other built-in widget actions like vote on a poll, as well as custom and CDP-driven actions - a streak reset action can optionally be configured. It is not auto-assigned.
- The streak reset action is particularly important in **None** and **Set** sub-types, where there is no inherent ordering or out-of-order logic to trigger an automatic reset. Configuring a reset action gives the system a programmatic way to break the streak when the user performs an action that should invalidate progress.
- In **Sequence** sub-type, interacting with targets out of order already resets the streak. A streak reset action can additionally be configured as a separate reset trigger.

### How Streak Progress and Reset Work

**None - Win 5 games in a row**
The streak progress action is "win a game," sub-type is None. No targets are configured. Each time the user wins a game, streak length increments by 1. If a streak reset action (e.g., "lose a game") is configured and fires, the streak resets to 0. Time gaps between games do not matter.

**Set - Predict outcomes across 3 specific matches**
The admin configures 3 match IDs as targets via CSV, sub-type is Set. Each time the user makes a correct prediction on any of the 3 matches, streak length increments by 1. Order does not matter. If a streak reset action fires at any point, the streak resets. Actions on matches not in the set are ignored.

**Sequence - Complete a tournament bracket in order**
The admin configures 4 match IDs in sequence via CSV. The user must make a correct prediction on Match 1 first, then Match 2, then Match 3, then Match 4 - each correct prediction on the next valid target increments streak length by 1. Predicting on Match 2 before completing Match 1 resets the streak. A streak reset action can also be configured as an additional reset trigger.

***

## Streak Milestones

Streak Milestones are the only mechanism through which rewards are granted within a streak. They act as checkpoints at defined streak lengths - when a user reaches a milestone, the configured rewards are automatically issued.

Milestones apply to both Periodic and Consecutive Action streaks.

**Examples:**

- Earn bonus points at streak lengths 3, 5, and 7
- Receive a badge on reaching a 10-day login streak
- Get a reward multiplier after correctly predicting 7 match outcomes in a row

### Milestone Types

| Type          | How It Works                                                              |
| ------------- | ------------------------------------------------------------------------- |
| **Recurring** | Rewards trigger at a fixed streak length interval (e.g., every 5 lengths) |
| **Custom**    | Rewards trigger at a specific streak length you define                    |

### Milestone Rewards

Each milestone can be configured to award one or more of the following:

| Reward Type                   | Details                                                                                                                                                                                 |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Reward Items (Points)**     | Standard point grants on reaching the milestone                                                                                                                                         |
| **User-Activated Multiplier** | A user-activated multiplier is granted to the user. Only user-activated multipliers can be linked - one per milestone. Once granted, the user activates it at a time of their choosing. |
| **Badges**                    | One or more badges can be awarded at a milestone. A single badge can only be attached to one milestone within a streak.                                                                 |

### Reward Behavior: Recurring and Reward on Reset

Reward Items and User-Activated Multipliers support two additional behaviors:

- **Recurring** - The reward is granted every time the milestone is reached, not just the first time.
- **Reward on Reset** - The reward is granted at the point of reset if the streak resets at that milestone length.

**Badges are excluded from both behaviors.** A user can earn a badge only once - regardless of how many times a milestone is reached or how many times the streak resets. If the user has already earned the same badge from another experience (a quest, a tier benefit, another streak), the badge award at that milestone is silently skipped while all other rewards on the same milestone are still granted.

***

## Configuring Streaks

Streaks are created and managed via **CMS - Streaks**. The setup flow is shared across both streak types, with a few fields specific to each.

### Setup Steps

1. **Name and Description** - Set a name and optional description.
2. **Streak Type** - Select **Periodic** or **Consecutive Action**.
3. **Streak Progress Action** - Select the user action that drives streak progress (e.g., make a correct prediction, answer a quiz correctly, vote on a poll, custom action, CDP-driven action).
4. **Period and Timezone** _(Periodic only)_ - Select the recurring window - Daily, Weekly, or Monthly - and set the timezone.
5. **Threshold** _(Periodic only)_ - Optionally set the number of times the progress action must be completed within the window before streak length increments by 1.
6. **Targets** _(Consecutive Action only)_ - In the dedicated Targets tab, select the sub-type (None, Set, or Sequence). For Set and Sequence, configure targets either via the built-in widget dropdown (for widget-based built-in actions) or via CSV upload (for all other actions).
7. **Streak Reset Action** _(Consecutive Action only)_ - Optionally configure the action that breaks the streak. Auto-assigned for correct prediction and correct quiz answer; optional for all others.
8. **Start / End Time** - Optionally set a campaign window for the streak.
9. **Streak Milestones** - Optionally add milestones. For each milestone, set the streak length, milestone type (Recurring or Custom), and configure rewards (Reward Items, User-Activated Multiplier, Badges). Set Recurring and Reward on Reset behavior for Reward Items and Multipliers as needed.
10. **User Groups** - Optionally scope the streak to specific user segments.
11. **Save or Publish** - The streak can be saved at any point before publishing, with all fields remaining editable. Once published, the rules below apply.

### What Can Be Edited After Publishing

Once a streak is published, most configuration is locked to preserve streak integrity.

| Editable After Publishing                              | Not Editable After Publishing             |
| ------------------------------------------------------ | ----------------------------------------- |
| Name and description                                   | Streak type                               |
| Start / End time (only if the time has not yet passed) | Streak progress action                    |
| Streak attributes                                      | Period and timezone (Periodic)            |
| Milestone attributes                                   | Threshold (Periodic)                      |
| Adding or removing milestones                          | Targets and sub-type (Consecutive Action) |
|                                                        | Streak reset action                       |
|                                                        | Existing milestone configuration          |

Milestones can be added or removed after publishing, but the configuration of existing milestones cannot be modified.

***

## Interaction With Other Features

### Streaks and Reward Multipliers

A user-activated multiplier earned via a streak milestone behaves exactly like any other user-activated multiplier. Once granted, the user can activate it at a time of their choosing. Standard multiplier concurrency and stacking rules apply:

- A user can hold at most one active user-activated multiplier per reward item at a time.
- If an automatic multiplier is also active on the same reward item, the two can stack. Stacking mode (additive or multiplicative) is a global application-level configuration - contact your LiveLike account team to confirm which mode is enabled for your application.

Refer to the **Reward Multipliers** guide for full details on stacking and override behavior.

### Streaks and Badges

Badges awarded at streak milestones follow the same uniqueness rules as badges from any other source. A user can earn a badge only once - if they already hold it from a quest, tier, or another streak, it will not be re-awarded at the milestone.

***

## Frequently Asked Questions

### Setup

**What is the difference between Periodic and Consecutive Action streaks?**
Periodic streaks are time-based - the user must act within a recurring window (daily, weekly, monthly) to maintain the streak. Consecutive Action streaks are action-based with no time dependency - what matters is the uninterrupted success of the action, regardless of when it happens.

**When should I use None, Set, or Sequence as the Consecutive Action sub-type?**
Use **None** when you only care that the user performed the action, not what they performed it on. Use **Set** when the action must be performed against a defined list of targets but order does not matter. Use **Sequence** when the user must interact with targets in a specific order - for example, completing matches in a tournament bracket in sequence.

**What is threshold and how is it different from milestones?**
Threshold defines how many times the streak progress action must be completed within a time window before streak length increments by 1. It is only applicable to Periodic streaks. Milestones define what rewards are granted at specific streak lengths. They operate at different levels - threshold controls how streak length accrues; milestones control what happens when it does.

**Does Consecutive Action streak have a threshold?**
No. Every qualifying action in a Consecutive Action streak increments streak length by 1 directly. There is no batching or threshold concept.

**Can I configure multiple reward types on the same milestone?**
Yes. A single milestone can combine Reward Items, a User-Activated Multiplier, and one or more Badges. Each reward type follows its own rules for recurring and reset behavior.

**Can the same badge be attached to more than one milestone within a streak?**
No. A badge can only be attached to one milestone within a streak. The same badge can be referenced across different streaks or experiences, but a user can earn it only once across all of them.

**Can I attach an automatic multiplier to a streak milestone?**
No. Only user-activated multipliers can be linked to streak milestones.

***

### Streak Progress and Reset

**What triggers a streak reset in a Periodic streak?**
Missing the required action - or failing to meet the threshold - within the defined time window resets the streak.

**What triggers a streak reset in a Consecutive Action streak?**
It depends on the sub-type. For **None** and **Set**, the configured streak reset action triggers the reset. For **Sequence**, interacting with targets out of order resets the streak; a streak reset action can additionally be configured. For correct prediction and correct quiz answer, the incorrect counterpart is auto-assigned as the reset action.

**Is the streak reset action mandatory for Consecutive Action streaks?**
No, it is optional - except for correct prediction and correct quiz answer, where it is automatically assigned. For all other actions, configuring a streak reset action is strongly recommended for None and Set sub-types to ensure the system can programmatically break the streak when needed.

**If a streak resets, are milestone rewards lost?**
Rewards already granted at prior milestones are not revoked. Whether a reward is granted at the point of reset depends on whether **Reward on Reset** is enabled on that milestone. Future milestone rewards are only available if the user rebuilds their streak back to those lengths.

**I set up a Consecutive Action streak with targets but progress is not tracking. What should I check?**
The most common cause is a mismatch between the target key-value pairs configured in CMS and the attributes being passed when the streak progress action is invoked. Confirm that the key (e.g., `match_id`) and value (e.g., the specific match ID) passed in the action attributes exactly match what was configured - via dropdown or CSV - in the streak setup.

***

### Milestones and Rewards

**Can milestone rewards recur every time a milestone is hit?**
Yes, for Reward Items and User-Activated Multipliers - enable the **Recurring** setting. Badges are excluded and can only be earned once per user across all experiences.

**A user already has a badge from a quest. Will they receive it again from a streak milestone?**
No. A user can earn a badge only once. If they already hold it, the badge award at that milestone is silently skipped - all other rewards on the same milestone are still granted.

**When does a user-activated multiplier granted at a milestone expire for earning purposes?**
Expiry for earning is governed by the multiplier's configured `start_at` / `stopped_at` window, if set. Once earned, the user can activate it at any time - there is no activation deadline based on when it was earned. Once activated, it remains live for the configured `active_duration`.

***

### Targeting and User Groups

**Can a streak be targeted to a specific audience?**
Yes. Streaks can be scoped to one or more User Groups at configuration. Users outside the assigned groups will not participate in the streak.

**Can different user groups have different streak configurations running simultaneously?**
Yes. Configure separate streak instances, each scoped to its own user group, to run parallel streak programs for different segments.
