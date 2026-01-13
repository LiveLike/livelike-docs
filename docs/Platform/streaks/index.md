---
title: Streaks
deprecated: false
hidden: true
metadata:
  robots: index
next:
  description: Periodic Streak CMS Guide
  pages:
    - slug: how-to-create-streaks-in-cms
      title: Periodic Streak CMS Guide
      type: basic
---
# What are streaks?

Streaks are an engagement mechanic that reward users for performing an action consistently over time or across repeated opportunities.
A streak tracks a user’s progress as they repeat a defined behavior—such as watching content, making predictions, checking in, or completing challenges—and rewards them for maintaining that consistency.  
A streak starts when a user performs a defined action and continues as long as the user meets the streak rules. If the rules are broken, the streak resets

In short: Streaks turn repeat behavior into a visible, rewarding habit.

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

* A client configures a streak in CMS using a preset (Periodic, Consecutive, Milestone).
* The streak listens to eligible user actions (quests, widgets, mini-games, behaviors).
* Each time the user performs the action:  
  Progress is evaluated against streak rules
  Milestones are checked
  Rewards are granted if thresholds are met
* Streaks can be:
  Frozen (user-level or admin-level)
  Targeted to specific User Groups
  Timezone-aware
* All activity is logged for analytics and reporting.

# Types of Streaks

Streaks can be broadly classified into **Periodic Streaks** and **Consecutive Streaks**, with Streak Milestones acting as reward checkpoints.

## Periodic Streaks:

A streak where users must perform an action within a recurring time window (daily, weekly, monthly).

### How it works:

* Each period is evaluated independently
* Missing a period breaks the streak
* Timezone-aware

**Examples**:

* Make a prediction every day for 7 days
* Play a game weekly for 4 weeks
* Log in monthly for 3 months

<br />

## Consecutive Streaks (Action-Based):

A streak based on consecutive successful actions, independent of calendar time.

### How it works:

* Progress depends on uninterrupted success
* Time gaps don’t matter
* One failure resets the streak

**Examples**:

* Correctly predict 3 matches in a row
* Win 3 games consecutively
* Complete 5 challenges back-to-back

<br />

## Streak Milestones

A flexible streak where users must complete X actions out of Y opportunities.  
Milestones are reward checkpoints within a streak.
Instead of rewarding only at the end, milestones allow rewards at incremental progress points.

### How it works:

* Allows some misses, keep users motivated even if they don’t complete the full streak
* Focuses on participation rather than perfection
* Evaluated within a defined scope or window

**Examples**:

* Complete 5 out of 7 daily challenges
* Watch 4 out of 6 episodes released
* Participate in 3 of 5 events

<br />

### How Streaks Are Configured in CMS (High Level)

Streaks are created and managed via the CMS → Streaks section.

At a high level, configuration includes:

* Selecting the streak type (Periodic / Consecutive)

* Defining the triggering user action

* Setting time windows or action thresholds

* Assigning milestone-based rewards

* Publishing the streak to targeted user groups

* Once published, streak progress and rewards are automatically tracked based on user activity.

<Cards>
  <Card title="Periodic Streak CMS Guide" href="https://docs.livelike.com/docs/how-to-create-streaks-in-cms" icon="fa-code">
    Follow these steps to create and configure a new Periodic Streak in the CMS.
  </Card>

  <Card title="Consecutive Streak CMS Guide" href="https://docs.livelike.com/docs/consecutive-streak-cms-guide" icon="fa-code">
    Follow these steps to create and configure a new Consecutive Streak in the CMS.
  </Card>
</Cards>
