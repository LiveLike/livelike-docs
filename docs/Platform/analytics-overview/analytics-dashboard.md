---
title: Analytics Dashboard
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: LiveLike Analytics Dashboard | Events Glossary | LiveLike
  description: >-
    As soon as your integration with LiveLike is launched, we start collecting
    data that can be used to track your success. Learn more.
  robots: index
next:
  pages:
    - slug: livelike-events-dictionary
      title: Livelike Analytics Dictionary
      type: basic
---
## Standard Analytics Dashboard

The Standard Analytics dashboard is available to all customers directly in the Producer Site. LiveLike generates these reports automatically from your platform data, so you do not need to configure the dashboard before viewing them.

### Application View

In the Application View, you can view various KPIs for your application over time. You can also track performance across user-level metrics.

Key features include:

* Use **Download** to export the page contents as a spreadsheet with your current filters applied.
* Use the search bar in the top right corner to find results faster.
* Use **Share** next to **Download** to share the current view with colleagues while keeping your applied filters.

<Image align="center" alt="Application View with download, search, and share controls" width="smart" src="https://files.readme.io/91f3c7e-ezgif.com-gif-maker.gif" />

Use the **Interval** drop-down to switch between **hour/day/week/month/year** views so you can compare short-term spikes with longer-term trends. The default view is **Month**.

![Interval drop-down expanded showing granularity options](https://files.readme.io/751ab15-ezgif.com-gif-maker_1.gif "ezgif.com-gif-maker (1).gif")

### Program View

The Program View shows KPIs per Program ID for side-by-side program comparisons. Each row lists Unique Impressions and Unique Interactions for one program. Filters carry over from the Application View.

![Program View with Unique Impressions and Interactions per program](https://files.readme.io/704cc4d-Screenshot_2022-01-24_at_3.57.02_PM.png "Screenshot 2022-01-24 at 3.57.02 PM.png")

Note: these views count interactions only for interactive widgets - covered in the next section.

### Widgets View

The Widgets View shows how individual widgets have performed. Filter by **Publish Date, Program ID, Widget Type, or Widget Category** to narrow the results.

The Widget Category filter has two options:

* Interactive : polls, predictions, quizzes, and other widgets that produce interaction data.
* Non-Interactive : images, cheer meters, alerts, and other display-only widgets.

Use it to exclude display-only content from your engagement numbers. To see only the widgets from one program, filter by that Program ID.

![Widgets View with Interactive vs Non-Interactive filter](https://files.readme.io/6c10a0e-Screenshot_2022-01-24_at_11.37.31_PM.png "Screenshot 2022-01-24 at 11.37.31 PM.png")

Select a program to see the widgets published during that time frame. Download that program's contents from the **Download** button in the upper-right corner.

### Quests View

The Quests View shows completion status and active-user counts per quest. Filter by **Quest**; all other filters carry over from the Application View.

![Quests View showing per-quest completion and active users](https://files.readme.io/adbc4b0-Screenshot_2024-02-08_at_1.22.00_PM.png)

### Quest Tasks View

The Quest Tasks View shows the task name and completion status for each quest. Filter by **Quest** and **Quest Task**; all other filters carry over from the Application View.

![Quest Tasks View showing task-level completion status](https://files.readme.io/1b2b584-Screenshot_2024-02-08_at_2.05.26_PM.png)

***

## Visual Analytics

Visual Analytics provides an interactive data exploration experience embedded in the Producer Site. It is available as an add-on and offers richer, drill-down reporting across multiple dashboard tabs, including custom tabs configured for your specific product.

### Default Dashboard Tabs

All Visual Analytics-enabled accounts include the following tabs:

#### Overview

High-level engagement KPIs across your application - active users (DAU/WAU/MAU), trend lines, and an interval-level summary of profiles, impressions, interactions, and engagement percent. Your starting point for understanding overall platform health.

<Image align="center" alt="Visual Analytics Overview tab with DAU, WAU, MAU and trend lines" border={true} src="https://files.readme.io/ac33fde430d4b61dcac245ab0b6cb65e0ce4d5a82b4c4b5da1e62038f39565b9-overview.gif" className="border" />

#### Widgets

Widget-specific performance broken down by type and program - engagement scores, widgets published by type, top-performing formats, and a per-widget statistics table with engagement rates.

<Image align="center" alt="Visual Analytics Widgets tab with engagement scores and per-widget table" src="https://files.readme.io/e11ec02ee5b2c03b52a8a7c2e6e0d46e89eec9ac886a627cb355c40bb5f585e0-widgets.gif" />

<Callout icon="💡" theme="default">
  **Tip:** To find a Program ID: open the CMS, navigate to the program, click the three-dot menu (⋮), and select **View Program ID**.
</Callout>

#### Quest

Quest participation funnels and reward claim data such as users attempting/completing quests, completion status by quest, per-quest funnel analysis, and average completion time.

<Image align="center" alt="Visual Analytics Quest tab showing funnel and completion time" src="https://files.readme.io/853460e3fa1089a12b1356f4853da7347340354217ea60170fc4d122992eca4f-quest.gif" />

#### Chat

Message volume, user participation, and moderation activity - chat message trends, unique senders, average messages per user, moderation actions (shadow ban, read-only), system-filtered messages, and deleted messages.

<Image align="center" alt="Visual Analytics Chat tab with message volume and moderation metrics" src="https://files.readme.io/9747c574b4c109dd0fc94df587945b66803116e967b4e409d47fca3cf69508f0-chat.gif" />

### Additional Tabs

Accounts may have additional tabs configured based on their product:

| Tab              | What it covers                                                                                                                   |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Comments**     | Comment volume, unique commenters, reply depth, and reaction trends                                                              |
| **Leaderboard**  | Entry counts per leaderboard and detailed entry-level tables (Profile ID, Nickname, Score)                                       |
| **Streaks**      | Streak adoption, average/max streak lengths, milestone achievement rates, drop-off analysis, freeze usage, and reward redemption |
| **Badges**       | Badges awarded by type, user badge grants, and distribution across badge tiers                                                   |
| **Status Tiers** | Tier distribution, upgrades/downgrades, and average time to tier (custom configuration)                                          |
| **Reward Store** | Redemption volumes, points spent, per-SKU transaction trends, and transaction history                                            |

For detailed metric definitions, see the [Analytics Dictionary](https://docs.livelike.com/docs/livelike-events-dictionary).

<Callout icon="💡" theme="default">
  **Tip:** Custom tabs are configured per account. Contact your LiveLike account manager if you need additional views or metrics not listed here.
</Callout>

### Arcade Analytics Tabs

For clients using LiveLike Arcade, additional tabs are available covering both Skilled and Non-Skilled game types. These tabs are configured per client and organisation.

#### Arcade Games (Overview)

A cross-game summary with three sections:

* **User Funnel** - total game plays, total distinct users, DAU, and game plays/users across days and per game
* **Retention** - D1 retention rates across games
* **Score** - average score per game

#### Arcade Games: Skill Based

In-depth analytics for skill-based games (e.g., skate-master, ski-dash, bobsleigh-battle, curling-master). Three sections:

* **User Funnel** - Total Distinct Users, MAU, Weekly Average Users, DAU
* **Game Plays** - Total Games Played, Average Monthly/Weekly/Daily Game Plays, game plays and distinct users per game and across days, user cohorts (0–30, 31–60, 61–90, 90+ days)
* **Game Engagement** - Max Score, Average Score, Completion Rate, average score per game, games played vs scores submitted over time

#### Arcade Games: Non-Skilled

Analytics for non-skilled game types. Same structure as Skill Based but without the Game Engagement section (no scores or completion rates):

* **User Funnel** - Total Distinct Users, MAU, Weekly Average Users, DAU
* **Game Plays** - Total Game Plays, Average Monthly/Weekly/Daily Games Played, average games played per user (total/monthly/weekly/daily), game plays and distinct users across days

#### Per-Game Dashboards

Individual game dashboards (e.g., Basketball, Charity Product) may be configured for clients with specific game types. These provide game-specific breakdowns of the same core metrics.

### Custom Analytics

If a metric or dashboard view you need is not available in any of the dashboards, LiveLike can configure custom analytics dashboards tailored to your requirement. Custom tabs can include bespoke KPIs, audience segments, feature-specific funnels, or event groupings not covered by the default set.

To request custom analytics, contact your LiveLike account manager with a description of the metrics or views you need. The LiveLike team will assess feasibility and configure the custom tab for your organisation.

<br />

<br />
