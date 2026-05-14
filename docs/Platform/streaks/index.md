---
title: Streaks
excerpt: Reward users for regular participation
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: how-to-create-streaks-in-cms
      title: Periodic Streak CMS Guide
      type: basic
---
# What are streaks?

Streaks are an engagement mechanic that reward users for performing an action consistently over time or across repeated opportunities.
A streak tracks a user’s progress as they repeat a defined behavior—such as watching content, making predictions, checking in, or completing challenges—and rewards them for maintaining that consistency.  
A streak starts when a user performs a defined action and continues as long as the user meets the streak rules. If the rules are broken, the streak resets

# Why use streaks?

Streaks help drive meaningful product outcomes by:

* Increasing user retention through habit-building
* Encouraging repeat behavior (daily, weekly, or event-based actions)
* Boosting content consumption (games, predictions, challenges, etc.)
* Driving deeper engagement with rewards tied to consistency
* Creating urgency and motivation through progress and milestones

From a business perspective, streaks are especially useful for:

* Sports predictions
* Arcade or casual games
* Fitness challenges
* Content consumption (episodes, videos, quizzes)
* Loyalty and reward programs

# How Streaks Work (High Level)

* A client configures a streak in CMS using a preset such as Periodic (Daily, Weekly, Monthly - time and action based) or Consecutive Action (only action based, no time dependency).
* The streak listens to eligible user actions such as voting, watching content, login, making predictions, playing mini game, etc.).
* Each time the user performs the action:  
  Progress is evaluated against streak rules
  Streak milestones are checked
  Rewards are granted if streak milestones are reached
* Streaks can be:
  Frozen (user-level or global)
  Targeted to specific User Groups
  Timezone-aware
* All activity is logged for analytics and reporting.

# Types of Streaks

Streaks can be broadly classified into **Periodic Streaks** and **Consecutive Action Streaks**, with Streak Milestones acting as reward checkpoints.

## Periodic Streaks (Time-Dependent):

A streak where users must perform an action within a recurring time window (daily, weekly, monthly).

### How it works:

* Each period is evaluated independently
* Missing a period breaks the streak
* Timezone-aware

**Examples**:

* Make a prediction every day
* Play 2 trivia games every week
* Referring 5 friends every month

<br />

## Consecutive Action Streaks (Action-Dependent):

A streak based on successful consecutive actions, independent of time / when those actions are performed.

### How it works:

* Progress depends on uninterrupted success
* Time gaps don’t matter
* One failure resets the streak

**Examples**:

* Correctly predict 3 match outcomes in a row
* Win 3 games consecutively
* Send a chat message on every match day in a tournament

<br />

## Streak Milestones

Streak Milestones are reward checkpoints within a streak. Instead of rewarding only at the end, milestones allow rewards at incremental progress points (streak lengths).

### How it works:

* Focuses on participation rather than perfection
* Evaluated within a defined scope or window (as long as streak is active)

**Examples**:

* Get bonus points for 3/5/7 consecutive correct predictions
* Earn points on every streak length increment

Streak Milestones can be of two types:

* Recurring - Set a periodic length interval for users to get rewards
* Custom - Define a custom streak length to be rewardable

Streak Milestones inherently can be configured to allow or stop each achieved milestone to be rewardable after user streak resets.

## How Streaks Are Configured in CMS (High Level)

Streaks are created and managed via the CMS → Streaks section.

At a high level, configuration includes:

* Selecting the streak type (Periodic / Consecutive Action)

* Defining the triggering user action

* Setting time windows or action thresholds (for Periodic); Setting targets (for Consecutive Action)

* Assigning rewards for streaks milestones

* Publishing the streak to targeted user groups

* Once published, streak progress and rewards are automatically tracked based on user activity.

<Cards>
  <Card title="Periodic Streak CMS Guide" href="https://docs.livelike.com/docs/how-to-create-streaks-in-cms" icon="fa-code">
    Follow these steps to create and configure a new Periodic Streak in the CMS.
  </Card>

  <Card title="Consecutive Action Streak CMS Guide" href="https://docs.livelike.com/docs/consecutive-streak-cms-guide" icon="fa-code">
    Follow these steps to create and configure a new Consecutive Action Streak in the CMS.
  </Card>
</Cards>