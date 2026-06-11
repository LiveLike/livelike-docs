---
title: Reward Multiplier
excerpt: Reward boost for users
deprecated: false
hidden: false
metadata:
  robots: index
---
Reward Multipliers amplify the points a user earns from any activity by a defined factor. Instead of earning the base point value for an action, the multiplier scales that reward - a 3x multiplier on a 100-point action yields 300 points.

Multipliers are a powerful lever for driving specific behaviors: rewarding loyalty milestones, boosting engagement during high-value windows (events, campaigns, seasons), or incentivizing users who have earned a special status. They are always scoped - by time, by user segment, or by activation - so you remain in precise control of who benefits and when.

LiveLike supports two types of Reward Multipliers, based on how they activate:

| Type           | How It Activates                                           | Best For                                                     |
| -------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| Automatic      | Activates automatically based on a date or date range      | Time-bound campaigns, event-day boosts, scheduled promotions |
| User-Activated | User earns the multiplier and must consciously activate it | Milestone rewards, streak prizes, tier perks                 |

***

## Multiplier Types

### Automatic Multiplier

An Automatic Multiplier activates on its own during a defined time window - no user action required. Any earn activity a user completes during the active window is automatically credited at the multiplied rate.

**Who it applies to:** By default, all users. If one or more User Groups are configured on the multiplier, only users belonging to those groups are eligible. Users outside the group earn at the base rate.

**Key configuration fields:**

| Field                            | Description                                                                                       |
| -------------------------------- | ------------------------------------------------------------------------------------------------- |
| `multiplier_factor`              | The factor applied to base point earnings (e.g., 3 for 3x). Decimal values are not supported      |
| `start_at` / `stopped_at`        | The date range during which the multiplier is active. Both are required for automatic multipliers |
| `profile_group_ids` _(optional)_ | If set, restricts the multiplier to users in the specified group(s)                               |

**Use Cases**

**Event-Day Boosts with Attendance-Based Tiers**

A sports franchise wants to reward fans based on how many home games they have attended across a season.

- Create user groups `fans_attended_3_or_more_games` and `fans_attended_5_or_more_games`, populated dynamically using rule-based user groups
- Configure a 3x automatic multiplier scoped to `fans_attended_3_or_more_games`, active on Game Day 6
- Configure a 5x automatic multiplier scoped to `fans_attended_5_or_more_games`, active on Game Day 6

On game day, users in each group automatically earn at the elevated rate. Users outside both groups earn at the base rate. No manual action is needed from the user or operator.

> Note: Two automatic multipliers on the same reward item cannot share the same multiplier factor during an overlapping time window - the platform will reject this configuration. Ensure user groups are mutually exclusive to keep behavior predictable.

**Seasonal Campaign Windows**

A streaming platform wants to run a "Binge Week" campaign where all users earn double points for 7 days.

- Configure a 2x automatic multiplier with a 7-day `start_at` / `stopped_at` window
- Leave `profile_group_ids` unset so it applies globally

All users earn 2x on any configured earn action during that window. The campaign ends automatically when the window closes.

**Targeted Re-engagement**

An app identifies users who haven't engaged in 30 days and wants to offer elevated rewards for a limited window without broadcasting it to active users.

- Create a dynamic user group: `lapsed_users_30_days`
- Configure a 4x automatic multiplier scoped to this group, active for 14 days

Lapsed users who return earn at 4x. Active users are unaffected.

***

### User-Activated Multiplier

A User-Activated Multiplier is earned by a user but does not activate until they explicitly choose to use it. This gives users agency - they can time their activation to coincide with a high-value activity to maximize the benefit.

**Who it applies to:** Any user who earns the multiplier through a qualifying trigger event. If `profile_group_ids` is configured, only users in those groups are eligible to earn it.

**Key configuration fields:**

| Field                                  | Description                                                                                   |
| -------------------------------------- | --------------------------------------------------------------------------------------------- |
| `multiplier_factor`                    | The factor applied when activated (e.g., 2 for 2x). Decimal values are not supported          |
| `active_duration`                      | How long the multiplier remains active once the user activates it                             |
| `start_at` / `stopped_at` _(optional)_ | The window during which the multiplier can be earned. Optional for user-activated multipliers |
| `profile_group_ids` _(optional)_       | Restricts eligibility to earn the multiplier to specific user segments                        |

> **Expiry note:** The `start_at` / `stopped_at` window only affects a user's ability to _earn_ the multiplier. Once earned, a user can activate it at any time - even after the expiry date has passed.

**Use Cases**

**Streak Completion Reward**

A fitness app rewards users who complete a 7-day activity streak with a 2x multiplier they can deploy whenever they choose.

- Configure a 2x user-activated multiplier linked to the streak's milestone at `streak_length = 7`
- Set `active_duration`: 24 hours

Users who hit the milestone earn a 2x multiplier and choose when to use it.

**Tier Attainment Perk**

A loyalty program grants a 5x multiplier to any user who reaches Gold tier.

- Configure a 5x user-activated multiplier, granted when `tier = gold`
- Set `active_duration`: 48 hours

Reaching Gold tier immediately delivers a meaningful prize to the user's account, while giving them time to plan when to deploy it.

**Welcome-Back Reward for Returning Users**

A platform rewards users returning after a 60-day absence with a multiplier that feels like a personal gift rather than a silent automatic benefit.

- Configure a 3x user-activated multiplier, granted on a custom event tracking first login after a 60-day gap
- Set `active_duration`: 72 hours

Because users must activate it, the interaction creates a deliberate moment of engagement.

***

## Earning and Awarding Multipliers

User-Activated Multipliers are issued to users automatically when a qualifying trigger event fires. **Multipliers cannot be manually awarded to a user** - issuance is always driven by an event.

The supported trigger events are:

| Trigger              | How It Works                                                                                                                                        |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Streak milestone** | The multiplier is linked to a specific milestone within a streak. When a user reaches that milestone length, the multiplier is automatically issued |
| **Tier attainment**  | The multiplier is linked to a tier benefit. When a user is assigned to that tier, the multiplier is issued                                          |

> Automatic Multipliers are not "earned" - they apply passively to all eligible users during the active window, with no issuance step.

### Linking to Streaks and Tiers (CMS)

- **Streak Milestones:** Navigate to the Streak Milestone page and select one or more multipliers from the dropdown. Only published, user-activated multipliers can be linked to a streak milestone.
- **Tier Benefits:** Navigate to the Tier Benefits page and select a multiplier from the dropdown. Only published, user-activated multipliers can be linked to a tier benefit. Each Tier Benefit can have only one multiplier linked. To add more multipliers, create additional Tier Benefits within the same Tier.

### Linking Multipliers to Streaks and Tiers (API)

- [Link Reward Multiplier with Streak Milestones](https://docs.livelike.com/reference/create-streak-milestone)
- [Link Reward Multiplier with Tier Benefits](https://docs.livelike.com/reference/create-tier-benefit)

***

## Setting Up Multipliers

### Setting Up via CMS

1. Navigate to **Reward Multipliers → Create New**
2. Set a **Name** and optional **Description**
3. Enter the **Multiplier Factor** (e.g., 3 for 3x). Decimal values are not supported
4. Select **Activation Type**: Automatic or User-Activated
5. _(User-Activated only)_ Select **Duration** - how long the multiplier stays active once triggered (e.g., 24 hours, 30 mins)
6. _(Optional)_ Set **Start Time** and **End Time**. For automatic multipliers, both are required. Time must not be in the past
7. Select the **Reward Items** to link. A multiplier can have one or more reward items linked. All linked reward items are impacted on activation
8. _(Optional)_ Under **User Group**, select one or more user groups to scope the multiplier
9. **Publish** the multiplier, or **Save & Quit** to keep it in Draft status for editing or publishing later

> If no user group is selected, the multiplier applies to all users (automatic) or all users who complete the trigger event (user-activated).

### Setting Up via API

- [Create a Reward Multiplier](https://docs.livelike.com/reference/create-multiplier)

***

## Activating Multipliers

### Automatic Multipliers

No activation step is required. Once the configured `start_at` time is reached, the multiplier applies automatically to all eligible users for the duration of the window.

### User-Activated Multipliers

Once a user earns a multiplier, they must explicitly activate it. There is no deadline for activation - a user can activate an earned multiplier at any time, even after the earning window (`stopped_at`) has passed.

Once activated, the multiplier remains live for the configured `active_duration`, counted from the moment of activation.

- [Manually Activate a User-Earned Multiplier (API)](https://docs.livelike.com/reference/activate-user-reward-multiplier)

> **UI guidance:** If override is disabled (the default), users who already have an active multiplier on a reward item cannot activate a second one. Ensure your UI surfaces the user's currently active multiplier in this state rather than showing a generic error.

***

## Stacking and Override

### Concurrency Rules

| Scenario                                                                                       | Rule                                                                                 | Enforced At                                |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------ |
| Two user-activated multipliers on the same reward item                                         | Not allowed simultaneously - only one can be active at a time                        | Runtime (activation blocked or overridden) |
| Two automatic multipliers on the same reward item + same multiplier factor + overlapping dates | Not allowed - configuration will be rejected                                         | Setup (CMS / API validation)               |
| Two automatic multipliers on the same reward item + different multiplier factor or dates       | Allowed - treated as unique based on the combination of value, reward item, and date | —                                          |
| One user-activated + one automatic multiplier on the same reward item                          | Allowed - this is the stacking scenario                                              | —                                          |

In short: a user can hold at most one live user-activated multiplier and one live automatic multiplier per reward item at any point in time.

### Stacking: User-Activated + Automatic Together

When both a user-activated and an automatic multiplier are active simultaneously on the same reward item, the platform combines them. How they combine is a global application-level setting - contact your LiveLike account team to confirm which stacking mode is enabled for your application.

| Stack Mode           | Behavior              | Example (2x user-activated + 3x automatic) |
| -------------------- | --------------------- | ------------------------------------------ |
| Additive _(default)_ | Values are summed     | 2 + 3 = 5x effective multiplier            |
| Multiplicative       | Values are multiplied | 2 × 3 = 6x effective multiplier            |

> Stacking mode is not configurable from the CMS or API. To change the stacking behavior for your application, contact your LiveLike account team.

### Override: Replacing a Live User-Activated Multiplier

By default, a user cannot activate a new user-earned multiplier on a reward item when one is already active. If override is enabled at the application level, a new user-activated multiplier immediately replaces the currently active one.

> **Important:** Override does not evaluate which multiplier is "better." It simply replaces the currently active multiplier with the newly activated one - regardless of value or remaining duration. The replaced multiplier is forfeited entirely.

| Override Setting | Behavior                                                                              |
| ---------------- | ------------------------------------------------------------------------------------- |
| Off _(default)_  | User cannot activate a new multiplier while one is already active on that reward item |
| On               | Activating a new multiplier immediately replaces the active one                       |

> Override is not configurable from the CMS or API. If your use case requires override to be on or off, contact your LiveLike account team.

***

## Managing Multipliers

### Editing a Multiplier (CMS)

1. Navigate to **Reward Multipliers**
2. Locate the multiplier and click **Edit**
3. Update the desired fields
4. Publish changes

A multiplier in **Draft** status can be fully edited — all configuration fields are modifiable before publication.

Once **published**, only the following fields remain editable:

| Editable After Publishing                          | Not Editable After Publishing |
| -------------------------------------------------- | ----------------------------- |
| `name`                                             | `multiplier_factor`           |
| `description`                                      | `activation_type`             |
| `starts_at` / `expires_at` (if not already passed) | `active_duration`             |
| `attributes`                                       | `profile_group_ids`           |
|                                                    | Linked reward items           |

- Changes to a published **automatic** multiplier take effect immediately.
- Changes to a published **user-activated** multiplier apply to multipliers earned in the future. Already earned or activated multipliers are not affected.

### Deleting vs. Archiving

**Deleting** permanently removes the configuration. This is irreversible and only available for multipliers in Draft status.

**Archiving** deactivates the multiplier while preserving its configuration.

- For automatic multipliers: new earn events are no longer boosted.
- For user-activated multipliers: users can no longer earn the multiplier, and any already-earned multipliers can no longer be activated. Any currently live activations cease boosting earnings immediately.

> **On unarchiving:** Multiplier durations run independently of archiving status. Time spent archived counts toward the multiplier's duration. If a multiplier expired while archived, it remains expired after unarchiving.

### Managing via API

- [Create and Manage a Reward Multiplier](https://docs.livelike.com/reference/create-multiplier-1)

***

## Frequently Asked Questions

### Setup

**Can I link more than one reward item to a multiplier?**<br />Yes - a multiplier can be linked to multiple reward items. All linked reward items are impacted when the multiplier is active.

**What does "linked to a reward item" mean? Does the multiplier apply to all earn actions?**<br />A multiplier is scoped to specific reward item(s) - for example, tier points or event points. It applies to all earn actions that credit those reward items. If a user completes an action that credits a different reward item, the multiplier does not apply.

**Can I scope a multiplier to a specific earn action rather than a reward item?**<br />Not directly - multipliers are tied to reward items, not individual actions. If you need action-level targeting, structure it by ensuring the relevant earn action is the only one crediting the targeted reward item. Contact your LiveLike account team to discuss more complex use cases.

**Can I set a multiplier with no start/end date?**
Start and end date are optional for user-activated multipliers. They are required for automatic multipliers.

**I want different multiplier values for different user segments during the same time window. Is that supported?**<br />Yes for automatic multipliers - configure one multiplier per segment, each scoped to its own user group, ensuring the groups are mutually exclusive. Note that two automatic multipliers on the same reward item cannot share the same multiplier factor during an overlapping time window; the platform will reject this configuration.

**Can I reuse the same automatic multiplier configuration for a recurring event (e.g., every game day)?**<br />No - start/end dates cannot be changed once they have passed. Clone an existing multiplier and update the dates for each recurrence. To avoid last-minute setup errors on repeating campaigns, consider creating all instances in advance.

### Earning and Awarding

**Can I manually grant a user-activated multiplier to a specific user?**<br />No. Users can only earn user-activated multipliers through qualifying trigger events (streak milestone and tier attainment). Manual issuance is not supported.

**Can a user see all multipliers they have earned?**<br />Yes - all user multipliers (with status: active, earned, or expired) can be queried via the [List User Reward Multiplier API](https://docs.livelike.com/reference/activate-user-reward-multiplier-1).

**A user earned a multiplier but hasn't activated it. How long do they have?**
There is no activation deadline. Once earned, a user can activate the multiplier at any time — even after the multiplier's `stopped_at` date has passed. The expiry date only controls when new users can earn it.

**If a multiplier's earning window expires before a user earns it, what happens?**
The multiplier reward is silently skipped for that user. Other rewards configured on the same milestone or trigger event are still granted.

### Stacking and Override

**Can a user have two automatic multipliers active at the same time?**
Possibly, if they belong to two different user groups each linked to a different automatic multiplier with an overlapping time window. The platform only rejects automatic multipliers that share the same reward item, same multiplier factor, and overlapping dates. If a user belongs to multiple groups in this scenario, the configured stacking rules apply. Keeping user groups mutually exclusive is strongly recommended to avoid unpredictable outcomes.

**Can a user have two user-activated multipliers active at the same time?**<br />No - only one user-activated multiplier per reward item can be active at a time. If override is off (the default), the user cannot activate a second one while one is live. If override is on, activating a new one immediately replaces the existing one - it is not stacked.

**What is the difference between stacking and override?**<br />Stacking refers to having both a user-activated and an automatic multiplier active simultaneously - this is allowed and the values are combined using the application's configured mode (additive or multiplicative). Override refers to replacing a live user-activated multiplier with a new one - only permitted if enabled globally at the application level.

**Does override pick the better multiplier?**
No. Override simply replaces the currently active multiplier with the newly activated one, regardless of which has a higher value or longer remaining duration. The replaced multiplier is forfeited entirely.

**Who controls override and stacking mode settings?**<br />Both are global application-level configurations managed by LiveLike - they are not exposed in the CMS or API. Contact your LiveLike account team to change either setting.

**If a user has both a user-activated and an automatic multiplier active, how is the combined value calculated?**
Depending on your application's stacking mode: additive sums the values (2x + 3x = 5x), multiplicative multiplies them (2x × 3x = 6x). Contact your LiveLike account team to confirm which mode is active for your application.

### Updating and Managing

**Can I edit a multiplier that is currently active?**
Yes, but only limited fields. Once published, only `name`, `description`, `starts_at` / `expires_at` (if not already in the past), and `attributes` can be edited. Changes are near real-time.

**Can I extend the end date of an active automatic multiplier?**<br />Yes - you can update the end date provided it has not yet passed. The multiplier will continue to apply through the new end date without interruption.

**Can I change the user group linked to a multiplier after it has been published?**
No. User group configuration is locked after publication. Only `name`, `description`, `starts_at` / `expires_at`, and `attributes` can be edited post-publish.

**What is the difference between deleting and archiving a multiplier?**<br />Deleting permanently removes the configuration and is irreversible - only Draft multipliers can be deleted. Archiving deactivates the multiplier while preserving its configuration. See **Managing Multipliers** for full archiving behavior.