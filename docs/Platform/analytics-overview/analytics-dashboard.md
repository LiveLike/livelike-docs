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
## 1. Standard Analytics Dashboard

The Standard Analytics dashboard is available to all customers directly in the Producer Site. It provides pre-built reports generated from data collected by the LiveLike platform, no setup required.

### What it covers

* **Application-level metrics** : engagement summaries across your application
* **Program-level metrics** : performance comparisons program over program
* **Widget-level metrics** : individual interactive widget results
* **Quest metrics** : completion status and active users per quest
* **Quest Task metrics** : task-level completion breakdown

<br />

### Application View

In the Application View, you can view various KPIs associated with your application as a whole on a time-period basis, and its performance on various user-level metrics.

Key features include:

* Spreadsheet download of the page contents with the current filters that have been applied.
* Search bar in the top right corner to increase efficiency.
* Share' next to the download button for better ease of access and shareability, allowing you to share the contents between your colleagues with the same filters which you have applied at your end.

<Image align="center" width="smart" src="https://files.readme.io/91f3c7e-ezgif.com-gif-maker.gif" />

You can see data in a more granular form, such as **hour/day/week/month/year**, by using the Interval drop-down options.  Our default view option is by **Month**.

![](https://files.readme.io/751ab15-ezgif.com-gif-maker_1.gif "ezgif.com-gif-maker (1).gif")

### Program View

In the Program View, you can see KPIs by Program ID, allowing for performance comparisons on a program over program basis. The filters remain the same which are already available in the application-level view previously selected. In this view, you can see Unique Impressions and Unique Interactions for each of your programs. Below is a snapshot of how it looks.

![](https://files.readme.io/704cc4d-Screenshot_2022-01-24_at_3.57.02_PM.png "Screenshot 2022-01-24 at 3.57.02 PM.png")

Also, please note that in the above views, Interactions are calculated for interactable widgets (discussed in the next view).

### Widgets View

In the Widget View, you can see how individual interactive widgets have performed. Here, you can filter the contents, such as by Publish Date, Program ID, Widget Type. For instance, if you want to see performance individual widget level by a particular program, or on a particular date, you can filter for those use cases. We have added a new filter where you can choose from two widget categories - **Interactive widgets & Non-Interactive widgets.**

![](https://files.readme.io/6c10a0e-Screenshot_2022-01-24_at_11.37.31_PM.png "Screenshot 2022-01-24 at 11.37.31 PM.png")

For your convenience, you can select a particular program, and then you can see the widgets which were published during that time frame. You can also download the contents of a particular program by clicking on the **Download** button provided in the upper right corner.

### Quests View

In the Quest View, you can see the completion status and active users if individual quests. Here, you can filter the contents using Quest and rest of the filters remain the same which are already available in the application-level view.

![](https://files.readme.io/adbc4b0-Screenshot_2024-02-08_at_1.22.00_PM.png)

### Quest Tasks View

In the Quest Task View, you can see the task name and completion status of individual quests. Here, you can filter the contents using Quest, Quest Task and rest of the filters remain the same which are already available in the application-level view.

![](https://files.readme.io/1b2b584-Screenshot_2024-02-08_at_2.05.26_PM.png)

***

## 2. Visual Analytics

Visual Analytics provides an interactive data exploration experience embedded in the Producer Site. It is available as an add-on and offers richer, drill-down reporting across multiple dashboard tabs — including custom tabs configured for your specific product.

### Default Dashboard Tabs

All Visual Analytics-enabled accounts include the following tabs:

#### Overview

High-level engagement KPIs across your application - active users (DAU/WAU/MAU), trend lines, and an interval-level summary of profiles, impressions, interactions, and engagement percent. Your starting point for understanding overall platform health.

#### Widgets

Widget-specific performance broken down by type and program - engagement scores, widgets published by type, top-performing formats, and a per-widget statistics table with engagement rates.

<Callout icon="💡" theme="default">
  #### **Tip:** To find a Program ID: open the CMS, navigate to the program, click the three-dot menu (⋮), and select View Program ID.
</Callout>

#### Quest

Quest participation funnels and reward claim data such as users attempting/completing quests, completion status by quest, per-quest funnel analysis, and average completion time.

#### Chat

Message volume, user participation, and moderation activity - chat message trends, unique senders, average messages per user, moderation actions (shadow ban, read-only), system-filtered messages, and deleted messages.

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
  #### **Tip:** Custom tabs are configured per account. Contact your LiveLike account manager if you need additional views or metrics not listed here.
</Callout>

### Arcade Analytics Tabs

For clients using LiveLike Arcade, additional tabs are available covering both Skilled and Non-Skilled game types. These tabs are configured per client and organisation.

#### Arcade Games (Overview)

A cross-game summary with three sections:

* **User Funnel** — total game plays, total distinct users, DAU, and game plays/users across days and per game
* **Retention** — D1 retention rates across games
* **Score** — average score per game

#### Arcade Games: Skill Based

In-depth analytics for skill-based games (e.g., skate-master, ski-dash, bobsleigh-battle, curling-master). Three sections:

* **User Funnel** — Total Distinct Users, MAU, Weekly Average Users, DAU
* **Game Plays** — Total Games Played, Average Monthly/Weekly/Daily Game Plays, games plays and distinct users per game and across days, user cohorts (0–30, 31–60, 61–90, 90+ days)
* **Game Engagement** — Max Score, Average Score, Completion Rate, average score per game, games played vs scores submitted over time

#### Arcade Games: Non-Skilled

Analytics for non-skilled game types. Same structure as Skill Based but without the Game Engagement section (no scores or completion rates):

* **User Funnel** — Total Distinct Users, MAU, Weekly Average Users, DAU
* **Game Plays** — Total Game Plays, Average Monthly/Weekly/Daily Games Played, average games played per user (total/monthly/weekly/daily), game plays and distinct users across days

#### Per-Game Dashboards

Individual game dashboards (e.g., Basketball, Charity Product) may be configured for clients with specific game types. These provide game-specific breakdowns of the same core metrics.

<br />

### Custom Analytics

If a metric or dashboard view you need is not available in any of the dashboards, LiveLike can configure custom analytics dashboards tailored to your requirement. Custom tabs can include bespoke KPIs, audience segments, feature-specific funnels, or event groupings not covered by the default set.

To request custom analytics, contact your LiveLike account manager with a description of the metrics or views you need. The LiveLike team will assess feasibility and configure the custom tab for your organisation.

***

## 3. Analytics API

The Analytics API gives you programmatic access to your analytics data - collections, cards (individual charts/queries), and dashboards. Use it to pull data into your own systems, build custom reports, or automate exports.

### Base URL

```
https://metabase.livelikecdn.com/api/
```

### Authentication

All requests require the `x-api-key` header. Your API key is scoped to your organisation and controls which collections and dashboards you can access. You can request your LiveLike account manager to provide you with the require api key

```bash
curl -H "x-api-key: YOUR_API_KEY" \
  https://metabase.livelikecdn.com/api/collection/
```

### Concepts

| Term           | Description                                                                                                      |
| -------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Collection** | A folder grouping related dashboards and cards. Your org will have at least one top-level collection.            |
| **Card**       | A single chart, table, or scalar metric - the building block of a dashboard. Each card runs an underlying query. |
| **Dashboard**  | A layout of multiple cards, optionally with shared filter controls and tabs.                                     |
| **Dashcard**   | A Card placed inside a Dashboard. Has its own `dashcard_id` separate from the underlying `card_id`.              |

### Endpoints

#### GET /api/collection/

Returns a flat list of all Collections your API key can see. Use this to discover your collection structure and retrieve `id` values needed for subsequent calls.

#### GET /api/card/:card_id

Returns full metadata for a Card including its parameters, column schema, and query type - **without running the query**. Call this before downloading data to understand the card's structure.

#### GET /api/dashboard/:dashboard_id

Returns full Dashboard metadata which includes all dashcards, filter controls, tab layout, and parameter mappings. **Call this before downloading dashboard card data** - you need the `dashcard_id` and `card_id` values from this response.

### Typical API Workflow

1. `GET /api/collection/` - Discover your collections, note the `id` of the relevant one
2. `GET /api/collection/<id>/items` - List cards and dashboards inside that collection
3. `GET /api/card/<card_id>` for a single chart, or `GET /api/dashboard/<dashboard_id>` for a full dashboard - Inspect parameters and column schema before downloading
4. Download or query the card or dashboard card with the correct parameters

```
1. GET /api/collection/
   → Discover your collections, note the id of the relevant one

2. GET /api/collection/<id>/items
   → List cards and dashboards inside that collection

3. GET /api/card/<card_id>            ← for a single chart/metric
   GET /api/dashboard/<dashboard_id>  ← for an entire dashboard

4. POST /api/card/<card_id>/query/csv → Download card data as CSV
	 POST /api/dashboard/<dashboard_id>/dashcard/<dashcard_id>/card/<card_id>/query/csv → Download a specific dashboard card's data
```

For detailed API definitions, see the [Analytics API Doc](https://docs.livelike.com/reference/get_collections).

<br />
