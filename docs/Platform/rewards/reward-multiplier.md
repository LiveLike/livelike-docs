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

LiveLike supports two types of Reward Multipliers:

| Type                  | How it activates                                           | Best for                                                     |
| --------------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| **Auto-Activation**   | Activates automatically based on a date or date range      | Time-bound campaigns, event-day boosts, scheduled promotions |
| **Manual Activation** | User earns the multiplier and must consciously activate it | Milestone rewards, streak prizes, tier perks                 |

***

## Type 1: Auto-Activation Multiplier

### What It Is

An Auto-Activation Multiplier is active for all eligible users during a defined time window - no user action required. When configured, any earn activity a user completes during the active window is automatically credited at the multiplied rate.

Auto-activation multipliers support **User Group&#x20;**&#x73;coping, so the multiplier can be restricted to a defined segment of your audience rather than applying globally.

### Key Parameters

| Parameter                        | Description                                                          |
| -------------------------------- | -------------------------------------------------------------------- |
| `multiplier_factor`              | The factor applied to base point earnings (e.g., `3` for 3x)         |
| `start_at` / `stopped_at`        | The date or date range during which the multiplier is active         |
| `profile_group_ids` _(optional)_ | If set, the multiplier only applies to users belonging to this group |

### Use Cases

#### Use Case 1: Event-Day Boosts with Attendance-Based Tiers

A sports franchise wants to reward fans who have shown progressive loyalty across a season. For their next three home games, they want different multiplier tiers to apply based on how many games a fan has already attended.

- Create a user group: `fans_attended_3_or_more_games` (dynamically updated as attendance data flows in)
- Create a user group: `fans_attended_5_or_more_games`
- Configure an auto-activation multiplier of **3x** scoped to `fans_attended_3_or_more_games`, active on Game 8 date
- Configure a second auto-activation multiplier of **5x** scoped to `fans_attended_5_or_more_games`, active on Game 10 date

On each game day, users in the respective group automatically earn at the elevated rate. Users outside the groups earn at base rate. No manual action needed from the user or the operator on game day.

#### Use Case 2: Seasonal Campaign Windows

A streaming platform wants to run a "Binge Week" campaign where all users earn double points on any watch activity for 7 days.

- Configure an auto-activation multiplier of **2x** with a 7-day `start_date` / `end_date` window
- Leave `user_group_id` unset so it applies globally

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

## Type 2: Manual Activation Multiplier

### What It Is

A Manual Activation Multiplier is **earned** by the user (through completing a streak, reaching a milestone, or attaining a tier) but does not activate until the user explicitly chooses to activate it. This gives users agency — they can time their activation to coincide with a high-value activity to maximise the benefit.

This type introduces a strategic dimension to loyalty: the multiplier is a _prize_ that users hold and deploy deliberately.

### Key Parameters

| Parameter                    | Description                                                                               |
| ---------------------------- | ----------------------------------------------------------------------------------------- |
| `multiplier_value`           | The factor applied when activated (e.g., `2` for 2x)                                      |
| `activation_window_hours`    | How long the user has to activate after earning before it expires unused                  |
| `active_duration_hours`      | Once activated, how long the multiplier remains active                                    |
| `earn_trigger`               | The event that grants the user this multiplier (e.g., streak completion, tier attainment) |
| `user_group_id` _(optional)_ | Restrict eligibility to a specific user segment                                           |

### Use Cases

#### Use Case 1: Streak Completion Reward

A fitness app rewards users who complete a 7-day activity streak with a 2x points multiplier they can deploy whenever they choose.

- Configure a manual-activation multiplier of **2x**, granted on `streak_completed` event (7-day streak)
- Set `activation_window_hours: 168` (user has 7 days to activate before it expires)
- Set `active_duration_hours: 24` (once activated, it's live for 24 hours)

Users who complete the streak receive a notification: _"You've earned a 2x multiplier — activate it before your next big workout session!"_ They choose when to use it, making the reward feel more personal and strategic.

#### Use Case 2: Tier Attainment Perk

A loyalty program grants a one-time 5x multiplier to any user who reaches Gold tier. The multiplier can be saved and deployed during a future high-value session.

- Configure a manual-activation multiplier of **5x**, granted on `tier_attained` event where tier = `gold`
- Set `activation_window_hours: 720` (30 days to activate)
- Set `active_duration_hours: 48` (active for 48 hours once triggered)

This makes reaching Gold tier feel impactful immediately (a meaningful prize lands in their account) while giving users time to plan how to use it.

#### Use Case 3: Welcome-Back Reward for Returning Users

A platform identifies users returning after a long absence and wants to greet them with a manually activatable multiplier so it feels like a personal gift rather than an automatic benefit.

- Configure a manual-activation multiplier of **3x**, granted on `user_return_event` (first login after 60-day gap)
- Set `activation_window_hours: 336` (14 days to activate)
- Set `active_duration_hours: 72`

Because users must activate it, the interaction creates a moment of delight and intent — far more memorable than a silent auto-activation.

### Setting Up (CMS — Producers)

1. Navigate to **Loyalty → Reward Multipliers → Create New**
2. Select type: **Manual Activation**
3. Enter the **multiplier value**
4. Under **Earn Trigger**, select the qualifying event (streak completion, tier attainment, custom event, etc.)
5. Set **Activation Window** — how many hours/days the user has to activate after earning
6. Set **Active Duration** — how long the multiplier is live once the user activates it
7. _(Optional)_ Select a **User Group** to restrict eligibility
8. Save and set status to **Active**

### Setting Up (API — Integrators)

**Step 1: Create the multiplier&#x20;**

**Step 2: Granting the multiplier to a user (on trigger event)**

When the qualifying event fires, the platform automatically issues the multiplier to the user's wallet. You can also grant it manually:

**Step 3: User activates their multiplier**

***

## Managing Multipliers

### Updating a Multiplier (CMS)

1. Navigate to **Loyalty → Reward Multipliers**
2. Locate the multiplier and click **Edit**
3. Update the desired fields (value, dates, user group, etc.)
4. Save changes

> **Note:** Changes to an active auto-activation multiplier take effect immediately. If the multiplier is currently live and you reduce the value, ongoing sessions within the window will use the new value.

### Updating a Multiplier (API)

```http
PATCH /v1/reward-multipliers/{multiplier_id}
Authorization: Bearer {token}
Content-Type: application/json

{
  "end_date": "2025-10-16T23:59:59Z",
  "multiplier_value": 5
}
```

Only the fields provided in the request body are updated; all other fields remain unchanged.

### Deactivating a Multiplier

To stop a multiplier from applying to future earn events without deleting it:

**CMS:** Open the multiplier → set **Status** to `Inactive` → Save

**API:**

```http
PATCH /v1/reward-multipliers/{multiplier_id}
Authorization: Bearer {token}
Content-Type: application/json

{
  "status": "inactive"
}
```

Deactivating an auto-activation multiplier mid-window stops it immediately. Users currently in an active session will not receive multiplied points for subsequent earn events.

### Deleting a Multiplier

Deletion is permanent and cannot be undone. If in doubt, deactivate instead of delete.

**CMS:** Open the multiplier → **Delete** → Confirm

**API:**

```http
DELETE /v1/reward-multipliers/{multiplier_id}
Authorization: Bearer {token}
```

***

## Stacking Behaviour

When a user is eligible for more than one active multiplier simultaneously (e.g., they are in a user group with an auto-activation multiplier AND they have manually activated a separate multiplier), the platform applies the **highest active multiplier value**. Multipliers are not additive.

**Example:**

- Auto-activation multiplier: **5x** (user is in qualifying group, game day is active)
- User's manually activated multiplier: **3x**
- **Effective multiplier applied: 5x**

> **Implication for producers:** If high-tier users are already covered by a high-value auto-activation multiplier during a given window, manual-activation multipliers of equal or lower value are effectively wasted if activated during that window. Consider targeting manual-activation multiplier communications to users _not_ covered by a higher auto-activation multiplier.

***

## Frequently Asked Questions

**Can I have multiple auto-activation multipliers active at the same time?**
Yes. If a user belongs to multiple groups each with their own auto-activation multiplier, the highest value among all active multipliers applies.

**What happens to a manual-activation multiplier if the user never activates it?**
It expires after the `activation_window_hours` lapses and is removed from the user's wallet. No points are awarded.

**Can a user see their available (unactivated) manual multipliers?**
Yes — unactivated multipliers appear in the user's reward wallet. You can surface these via the SDK widget or query them via API (`GET /v1/users/{user_id}/reward-multipliers`).

**Does a multiplier apply to all earn actions or only specific ones?**
By default, a multiplier applies to all earn actions active during its window. Action-level scoping (restricting a multiplier to a specific earn action type) may be available depending on your plan — check with your LiveLike account team.

**Can a multiplier be granted to a user before the active window starts?**
For manual-activation multipliers, yes — you can grant the multiplier in advance so it sits in the user's wallet ready to activate. For auto-activation multipliers, the system evaluates eligibility at the time of the earn event, so pre-granting is not applicable.
