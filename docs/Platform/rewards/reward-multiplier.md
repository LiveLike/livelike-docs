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

### Setting Up (CMS)

1. Navigate to **Reward Multipliers → Create New**
2. Set a **Name** and **Description** (optional)
3. Enter the **Multiplier Factor** (e.g., `3` for 3x). Multiplier factor **_does not_** support decimal values
4. Select **Activation Type**: **Automatic**
5. _(Optional)_ Set the **Start Time** and **End Time** (can be the same date for a single-day boost). Time **_must not be_** in the past
6. Select the **Reward Items**. A multiplier can have one or more reward items linked. On activation, all linked reward items will be impacted
7. _(Optional)_ Under **User Group**, select one or more user groups to scope the multiplier
8. **Publish** the multiplier. You can also **Save & Quit&#x20;**&#x74;o keep it in "Draft" status for editing/publishing later.

> **Note:** If no user group is selected, the multiplier applies to all users during the active window.

### Setting Up (API)

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
| `start_at` / `stopped_at`        | The date or date range during which the user-activated multiplier can be earned                |
| `source_type`                    | Source from where a user earned this multiplier (e.g., streak\_milestone, tier\_benefit, etc.) |
| `profile_group_ids` _(optional)_ | Restrict eligibility to earn a multiplier to specific user segments                            |

**Note:** Expiry date only impacts users' ability to earn a multiplier. Once earned, users can activate the multiplier at any point, even past the expiry date.&#x20;

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

### Setting Up (CMS)

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

### Linking Multiplier to other Loyalty Features (CMS)

1. Navigate to **Streak Milestone&#x20;**&#x70;age and select one or more multipliers available in the drop-down list. Only published, user-activated multipliers can be linked to a streak milestone.&#x20;
2. Navigate to **Tier Benefits** page and select a multiplier available in the drop-down list. Only published, user-activated multipliers can be linked to a tier benefit. Each Tier Benefit can only have one multiplier linked. To add more multipliers, create new Tier Benefits within a Tier.

### Setting Up, Linking & Activating (API)

Steps to [**Create Reward multiplier**]()**&#x20;**

Steps to **Link Reward Multiplier** with:

- **Streaks**
- **Tiers**

**Granting the multiplier to a user (on trigger event)**

When the qualifying event fires, the platform automatically issues the multiplier to the user. **_Note:_**_&#x20;At present, users&#x20;_**_cannot be manually awarded_**_&#x20;a reward multiplier. Only qualifying events issues it._

Step t&#x6F;**&#x20;**[**Manually Activate User-Earned Multiplier**]()

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

# Stacking & Override

## Concurrency Rules

Each multiplier type has its own concurrency constraint, enforced at different levels:

| Scenario                                                                               | Rule                                                                                | Enforced at                              |
| -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------- |
| Two user-activated multipliers on the same reward item                                 | Not allowed simultaneously - only one can be active at a time                       | Runtime (activation blocked / overriden) |
| Two automatic multipliers on the same reward item + same multiplier factor + same date | Not allowed - configuration will be rejected                                        | Setup (CMS / API validation)             |
| Two automatic multipliers on the same reward item + different multiplier factor / date | Allowed - combination of multiplier value + reward item + date is treated as unique | -                                        |
| One user-activated + one automatic multiplier on the same reward item                  | Allowed - this is the stacking scenario (see below)                                 | -                                        |

**In short:** a user can hold at most one live user-activated multiplier and one live automatic multiplier per reward item at any point in time.

***

## Stacking: User-Activated + Automatic Together

A user can have one user-activated and one automatic multiplier active simultaneously on the same reward item. When both are active, the platform combines them - but **how they combine is a global application-level configuration**. Contact your LiveLike account team to confirm which stacking mode is enabled for your application.

| Stack Mode                  | Behaviour             | Example (2x manual + 3x auto)       |
| --------------------------- | --------------------- | ----------------------------------- |
| **Additive&#x20;**(default) | Values are summed     | 2 + 3 = **5x** effective multiplier |
| **Multiplicative**          | Values are multiplied | 2 × 3 = **6x** effective multiplier |

> **Note:** Stacking mode is not configurable from the CMS/API. If you need to change the stacking behaviour for your application, raise it with your LiveLike account team.

***

## Override: Replacing a Live User-Activated Multiplier

By default, a user cannot activate a new user-earned multiplier on a reward item when one is already active. However, **override can be enabled at the global application-level configuration**, allowing a new user-activated multiplier to replace the currently active one.

**Important:** Override does not evaluate which multiplier is "better." It simply replaces the currently active multiplier with the newly activated one - regardless of value or remaining duration. The replaced multiplier is forfeited.

| Override Setting  | Behaviour                                                                                                                   |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **Off** (default) | User cannot activate a new user-earned multiplier while one is already active on that reward item                           |
| **On**            | User can activate a new user-earned multiplier for the same reward item at any time; it immediately replaces the active one |

> **Note:** Override is not configurable from the CMS/API. It is enabled or disabled at the application level. If your use case requires override to be on or off, communicate this to your LiveLike account team. When override is off, users who attempt to activate a second manual multiplier will see an error; ensure your UI handles this gracefully by surfacing their currently active multiplier.

***

## Frequently Asked Questions

### Setup

**Can I link more than one reward item to a multiplier?**<br />Yes - multipliers can be linked to a multiple reward items. It impacts all linked reward items when active.

**Can I reuse the same automatic multiplier configuration for a recurring event (e.g., every game day)?**<br />No. However, you can clone an existing automatic multiplier and update the dates. To avoid setup errors on repeating campaigns, consider creating all instances in advance.

**I want different multiplier values for different user segments during the same time window. Is that supported?**<br />Yes for automatic multipliers - configure one multiplier per segment, each scoped to its own user group, but ensure the groups are mutually exclusive. However, two automatic multipliers on the same reward item cannot have same multiplier factor during the same time window; the platform will reject the configuration during setup.

**What does "linked to a reward item" mean? Does the multiplier apply to all earn actions?**<br />A multiplier is scoped to a specific reward item (e.g., tier points, event points). It applies to all earn actions that credit that reward item. If a user completes an action that credits a different reward item, the multiplier does not apply.

**Can I scope a multiplier to a specific earn action rather than a reward item?**<br />Not directly - multipliers are tied to reward items, not individual actions. If you need action-level targeting, structure it by ensuring the relevant earn action is the only one crediting the targeted reward item, or contact your LiveLike account team to discuss your use case.

**Can I set a multiplier with no end date for an auto-activation type?**<br />Yes - it serves as an open-ended boost. To end it, you will need to archive it or manually add an end date in future.

***

### Updating and Managing

**Can I edit a multiplier that is published / currently active?**<br />Ye, but it's limited. Only multiplier name, description, start/end date and attributes can be edited once the multiplier is published. Change is near-real-time. Note that there is no retroactive recalculation - users who already earned points during the current window are unaffected by the change.

**Can I extend the end date of an active automatic multiplier?**<br />Yes - update the `End Date`. The multiplier will continue to apply through the new end date without any interruption.

**Can I change the user group linked to a multiplier after it has been activated?**<br />No. Only multiplier name, description, start/end date and attributes can be edited once the multiplier is published.

**What is the difference between deleting and archiving  a multiplier?**<br />Deleting removes the configuration entirely. This is irreversible. Only multiplier is "Draft" status can be deleted.

Archiving deactivates the multiplier but preserves the configuration in LiveLike backend. For automatic multiplier, it stops new earn events from being boosted. For user-activated multipliers, it stops users from earning or activating and already earned multiplier. Any live multipliers will cease to boost earnings.&#x20;

***

### Linking and Activation

**A user earned a multiplier but hasn't activated it. How long do they have?**<br />Activation is not time-bound once a multiplier is earned by the user.

**Can a user see all multipliers they have earned?**<br />Yes - all user multipliers (with status as active, earned & expired) can queried via the [**List User Reward Multiplier API**]().

**Once a user activates a manual multiplier, when does it expire?**
It remains active for the duration set in `active_duration_hours`, counted from the moment of activation.

**Can I grant a user-activated multiplier to a user directly, without them completing a trigger event?**<br />No - at present, users can only earn user-activated multiplier from specific trigger events (such as reaching a streak milestone, unlocking a tier, etc.)

<br />

***

### Stacking and Override

**Can a user have two automatic multipliers active at the same time?**<br />The only restriction enforced at the configuration level is that the platform will not allow two automatic multipliers on the same reward item having same multiplier factor, with overlapping time windows. If a user belong to more than one group linked to different multipliers and overlapping time window, preferred rules of stacking will apply. However, it is advisable that groups be mutually exclusive to keep implementation clean and predictable.

**Can a user have two user-activated multipliers active at the same time?**<br />No - only one user-activated multiplier per reward item can be active at a time. If override is off (the default), a user cannot activate a second manual multiplier while one is already active. If override is on, activating a new one immediately replaces the existing one - it is not additive.

**What is the difference between stacking and override?**<br />Stacking refers to a user having more than one multiplier active simultaneously - this is allowed in come cases discussed above and the two values are combined based on configured global rules (additive / multiplicative). Override refers to a user replacing a live user-activated multiplier with a new user-activated multiplier - this is only permitted if enabled globally at the application level.

**Does override pick the better multiplier (higher value or longer duration)?**<br />No. Override is not intelligent - it simply replaces the currently active multiplier with the newly activated one, regardless of which is more favourable. The replaced multiplier is forfeited entirely. This behaviour is intentional and consistent.

**Who controls whether override and stacking mode are enabled?**<br />Both are global application-level configurations managed by LiveLike, not exposed in the CMS/API. If you want to change the override setting or the stacking mode (additive vs. multiplicative) for your application, contact your LiveLike account team.

**If a user has both a manual and auto multiplier active (stacking), how is the combined value calculated?**<br />Depending on your application's stacking mode: additive sums the values (2x + 3x = 5x), multiplicative multiplies them (2x × 3x = 6x). To confirm which mode is active for your application, check with your LiveLike account team.
