---
title: Reward Multiplier
deprecated: false
hidden: true
metadata:
  robots: index
---
## Overview

Reward Multipliers allow you to amplify the points a user earns from any activity by a defined factor. Instead of a user earning the base point value for an action, the multiplier scales that reward - a 3x multiplier on a 100-point action yields 300 points.

Multipliers are a powerful lever for driving specific behaviors: rewarding loyalty milestones, boosting engagement during high-value windows (events, campaigns, seasons), or incentivizing users who have earned a special status. They are always scoped - by time, by user segment, or by activation - so you remain in precise control of who benefits and when.

LiveLike supports two types of Reward Multipliers, based on activation method:

| Type               | How it activates                                           | Best for                                                     |
| ------------------ | ---------------------------------------------------------- | ------------------------------------------------------------ |
| **Automatic**      | Activates automatically based on a date or date range      | Time-bound campaigns, event-day boosts, scheduled promotions |
| **User-Activated** | User earns the multiplier and must consciously activate it | Milestone rewards, streak prizes, tier perks                 |

***

## Type 1: Automatic Multiplier

### What It Is

An Automatic Multiplier is active for all eligible users during a defined time window - no user action required. When configured, any earn activity a user completes during the active window is automatically credited at the multiplied rate.

Auto-activation multipliers support **User Group&#x20;**&#x73;coping, so the multiplier can be restricted to a defined segment of your audience rather than applying globally.

### Key Parameters

| Parameter                        | Description                                                          |
| -------------------------------- | -------------------------------------------------------------------- |
| `multiplier_factor`              | The factor applied to base point earnings (e.g., `3` for 3x)         |
| `start_at` / `stopped_at`        | The date or date range during which the multiplier is active         |
| `profile_group_ids` _(optional)_ | If set, the multiplier only applies to users belonging to this group |

### Use Cases

#### Use Case 1: Event-Day Boosts with Attendance-Based Tiers

A sports franchise wants to reward fans who have shown progressive loyalty across a season. For their home games, they want different multiplier tiers to apply based on how many home games a fan has already attended.

- Create a user group `fans_attended_3_or_more_games` and assign users who qualify dynamically using rule-based user groups
- Create a user group and assign users: `fans_attended_5_or_more_games` and assign users dynamically
- Configure an auto-activation multiplier of **3x** scoped to `fans_attended_3_or_more_games`, active on Game Day 6&#x20;
- Configure a second auto-activation multiplier of **5x** scoped to `fans_attended_5_or_more_games`, active on Game Day 6

On that game day, users in the respective group automatically earn at the elevated rate. Users outside the groups earn at base rate. No manual action needed from the user or the operator on game day.

#### Use Case 2: Seasonal Campaign Windows

A streaming platform wants to run a "Binge Week" campaign where all users earn double points on any watch activity for 7 days.

- Configure an auto-activation multiplier of **2x** with a 7-day `start_date` / `end_date` window
- Leave `user_group_id` unset so it applies globally to all users

All users earn 2x on any configured earn action during that window. The campaign ends automatically when the window closes - no manual intervention required.

#### Use Case 3: Targeted Re-engagement

An app identifies users who haven't engaged in 30 days. To bring them back, they want to offer elevated rewards for a limited window without broadcasting it to active users.

- Create a dynamic user group: `lapsed_users_30_days`
- Configure an auto-activation multiplier of **4x** scoped to this group, active for 14 days

Lapsed users who return earn at 4x without knowing it's a targeted campaign. Active users are unaffected.

### Setting Up (CMS - Producers)

1. Navigate to **Reward Multipliers → Create New**
2. Set a **Name** and **Description** (optional)
3. Enter the **Multiplier Factor** (e.g., `3` for 3x). Multiplier factor **_does not_** support decimal values
4. Select **Activation Type**: **Automatic**
5. _(Optional)_ Set the **Start Time** and **End Time** (can be the same date for a single-day boost). Time **_must not be_** in the past
6. Select the **Reward Items**. A multiplier can have one or more reward items linked. On activation, all linked reward items will be impacted
7. _(Optional)_ Under **User Group**, select one or more user groups to scope the multiplier
8. **Publish** the multiplier. You can also **Save & Quit&#x20;**&#x74;o keep it in "Draft" status for editing/publishing later.

> **Note:** If no user group is selected, the multiplier applies to all users during the active window.

### Setting Up (API - Integrators)

Steps to [**Create Reward Multiplier**]().

***

## Type 2: User-Activated Multiplier

### What It Is

A User-Activated Multiplier is **earned** by the user (through reaching a streak milestone, unlocking a tier, etc.) but does not activate until the user explicitly chooses to activate it. This gives users agency - they can time their activation to coincide with a high-value activity to maximise the benefit.

This type introduces a strategic dimension to loyalty: the multiplier is a _prize_ that users hold and deploy deliberately.

### Key Parameters

| Parameter                        | Description                                                                                    |
| -------------------------------- | ---------------------------------------------------------------------------------------------- |
| `multiplier_factor`              | The factor applied when activated (e.g., `2` for 2x)                                           |
| `active_duration`                | Once activated, how long the multiplier remains active                                         |
| `source_type`                    | Source from where a user earned this multiplier (e.g., streak\_milestone, tier\_benefit, etc.) |
| `profile_group_ids` _(optional)_ | Restrict eligibility to earn a multiplier to specific user segments                            |

### Use Cases

#### Use Case 1: Streak Completion Reward

A fitness app rewards users who complete a 7-day activity streak with a 2x points multiplier they can deploy whenever they choose.

- Configure a user-activated multiplier of **2x**, granted on `milestone_reward` event when **_streak\_length_**_&#x20;_**_= 7_** (for a 7-day streak)
- Set `active_duration: 24 hours` (once activated, it's live for 24 hours)

Users who reach that milestone earn a 2x multiplie&#x72;_.&#x20;_&#x54;hey choose when to use it, making the reward feel more personal and strategic.

#### Use Case 2: Tier Attainment Perk

A loyalty program grants a 5x multiplier to any user who reaches Gold tier. The multiplier can be saved and deployed during a future high-value session.

- Configure a user-activated multiplier of **5x**, granted on `assigned_to` event where tier = `gold`
- Set `active_duration: 48 hours` (active for 48 hours once triggered)

This makes reaching Gold tier feel impactful immediately (a meaningful prize lands in their account) while giving users time to plan how to use it.

#### Use Case 3: Welcome-Back Reward for Returning Users

A platform identifies users returning after a long absence and wants to greet them with a multiplier so it feels like a personal gift rather than an automatic benefit.

- Configure a user-activated multiplier of **3x**, granted on a custom event tracking user's return (first login after 60-day gap)
- Set `active_duration: 72 hours`

Because users must activate it, the interaction creates a moment of delight and intent - far more memorable than a silent automatic activation.

### Setting Up (CMS — Producers)

1. Navigate to **Reward Multipliers → Create New**
2. Set a **Name** and **Description** (optional)
3. Enter the **Multiplier Factor** (e.g., `3` for 3x). Multiplier factor **_does not_** support decimal values
4. Select **Activation Type**: **User-Activated**
5. Select **Duration**: 24 hours / 30 mins / etc.
6. _(Optional)_ Set the **Start Time** and **End Time** (can be the same date for a single-day boost). Time **_must not be_** in the past
7. Select the **Reward Items**. A multiplier can have one or more reward items linked. On activation, all linked reward items will be impacted
8. _(Optional)_ Under **User Group**, select one or more user groups to scope the multiplier
9. **Publish** the multiplier. You can also **Save & Quit&#x20;**&#x74;o keep it in "Draft" status for editing/publishing later.

> **Note:** If no user group is selected, the multiplier applies to all users during the active window.

### Setting Up, Linking & Activating (API — Integrators)

Steps to [**Create Reward multiplier**]()**&#x20;**

Steps to **Link Reward Multiplier** with:

- **Streaks**
- **Tiers**

**Granting the multiplier to a user (on trigger event)**

When the qualifying event fires, the platform automatically issues the multiplier to the user. **_Note:_**_&#x20;At present, users&#x20;_**_cannot be manually awarded_**_&#x20;a reward multiplier. Only qualifying events issues it._

Step t&#x6F;**&#x20;Manually Activate User-Earned Multiplier**

***

## Managing Multipliers

### Updating a Multiplier (CMS)

1. Navigate to **Reward Multipliers**
2. Locate the multiplier and click **Edit**
3. Update the desired fields
4. **Publish** changes

> **Note:** A reward multiplier can be fully updated while it is in the **draft** state, allowing modification of all configuration fields before publication.
>
> Once a multiplier is **published**, only a limited set of fields can be updated to preserve configuration integrity. The following fields remain editable after publication:
>
> - `name`
> - `description`
> - `starts_at`
> - `expires_at`
> - `attributes`
>
> All other fields become immutable after the multiplier is published
>
> Changes to a published automatic multiplier take effect immediately. For a published user-activated multiplier, changes take place for the multiplier earned in future. Already earned/activated multiplier are not impacted.&#x20;

### Managing a Multiplier (API)

Steps to [**create & manage rewards multiplier**]()

***

##

<br />
