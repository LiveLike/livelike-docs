---
title: Streaks
excerpt: Reward users for regular participation
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
Streaks reward users for performing an action consistently over time or across repeated opportunities. A streak tracks a user’s progress as they repeat a defined behavior, such as watching content, making predictions, checking in, or completing challenges, and then rewards them for maintaining that consistency. A streak starts when a user performs an action associated with the streak and continues as long as the user meets the streak rules. If the rules are broken, the streak resets.

Streaks are classified into **Periodic Streaks** and **Consecutive Action Streaks**. Milestones within streaks act as reward checkpoints.

## Why use streaks?

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

## How streaks work

* A client configures a streak in CMS using a preset such as Periodic (Daily, Weekly, Monthly - time and action based) or Consecutive Action (only action based, no time dependency).
* The streak listens to eligible user actions such as voting, watching content, login, making predictions, playing mini game, etc.).
* Each time the user performs the action, progress is evaluated against streak rules and rewards are granted if streak milestones are reached.
* Streaks can be frozen (user-level or global), targeted to specific User Groups, and timezone-aware.
* All activity is logged for analytics and reporting.

## Periodic streaks

A periodic streak is extended by performing an action within a recurring time window such as daily, weekly, or monthly. Examples:

* Make a prediction every day
* Play 2 trivia games every week
* Referr 5 friends every month

Periodic streaks are timezone-aware.

Missing a period breaks the streak.

## Consecutive Action streaks

A consecutive action streak is extended by performing an action in a defined order. Examples:

* Correctly predict 3 match outcomes in a row
* Win 3 games consecutively
* Send a chat message on every match day in a tournament

Progress depends on uninterrupted success, so a failure resets the streak, but time gaps don’t matter.

## Streak milestones

Streak Milestones are reward checkpoints within a streak. Instead of rewarding only at the end, milestones allow rewards at incremental progress points (streak lengths). Examples:

* Get bonus points for 3, 5, and 7 consecutive correct predictions
* Earn points on every streak length increment

Streak Milestones can be of two types:

* Recurring: Set a periodic length interval for users to get rewards
* Custom: Define a custom streak length to be rewardable

Rewards for reaching Streak Milestones can be configured to trigger only once or every time the milestone is reached.

## Configuring streaks

Streaks are created and managed via the CMS → Streaks section. At a high level, configuration includes:

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