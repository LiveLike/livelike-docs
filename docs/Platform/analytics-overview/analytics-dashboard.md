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
  description: ''
  pages:
    - type: basic
      slug: livelike-events-dictionary
      title: Livelike Analytics Dictionary
    - type: basic
      slug: analytics-event-glossary
      title: Analytics Event Glossary
---
## 1. Standard Analytics Dashboard

The Standard Analytics dashboard is available to all customers directly in the Producer Site. It provides pre-built reports generated from data collected by the LiveLike platform, no setup required.

### What it covers

* **Application-level metrics** : engagement summaries across your application
* **Program-level metrics** — performance comparisons program over program
* **Widget-level metrics** — individual interactive widget results
* **Quest metrics** — completion status and active users per quest
* **Quest Task metrics** — task-level completion breakdown

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

High-level engagement KPIs across your application - active users, session counts, total widget interactions, and trend lines over your selected date range. This is your starting point for understanding overall platform health.

#### Widgets

Widget-specific performance broken down by type. See impression counts, interaction rates, answer accuracy, and completion rates for polls, predictions, quizzes, and other widget formats side by side.

#### Quest

Quest participation funnels, step-by-step completion rates, drop-off points, and reward redemption counts. Useful for measuring the effectiveness of your engagement programs.

#### Chat

Message volume over time, unique active chatters, reaction counts, and moderation event frequency. Helps identify peak activity windows and community engagement patterns.

### Additional Tabs

Accounts may have additional tabs configured based on the features they are using. Examples include:  

<Callout icon="💡" theme="default">
  #### **Custom tabs are configured per account upon request.** If you need additional tabs or custom analytics views, contact your LiveLike account manager.
</Callout>

#### Leaderboard

Point distribution histograms, top-user rankings, and rank change velocity over time. Useful for calibrating reward structures and identifying highly engaged users.

#### Arcade Analytics — Skilled Games

| Tab                  | What it covers                                                                                                     |
| -------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Guess the Word (GTW) | Prediction participation rates, outcome distributions, accuracy per match, and user prediction volume trends       |
| Play Predictor       | Per-play prediction volumes, accuracy trends, and comparison across game events                                    |
| Trivia               | Question-level performance, answer option distributions, average completion rates, and difficulty calibration data |
| Shoot the Web (STW)  | Score submission volumes, accuracy distributions                                                                   |

#### Arcade Analytics — Non-Skilled Games

Non-skilled arcade game tabs follow the same structure as their skilled counterparts but exclude accuracy and prediction-correctness metrics, focusing instead on participation volume and engagement depth.

***

### 3. Analytics API

The Analytics API lets you programmatically access the same data that powers Visual Analytics. Use it to build custom reports, integrate with external BI tools, or automate exports.

**Base URL:**

```
https://metabase.livelikecdn.com/api/
```

**Authentication:** All requests require the `x-api-key` header. Your API key is scoped to your organisation and controls which collections and dashboards you can access. Contact your LiveLike account manager to get your API key.

```bash
curl -H "x-api-key: YOUR_API_KEY" \
  https://metabase.livelikecdn.com/api/collection/
```

### Concepts

| Term           | Description                                                                                                    |
| -------------- | -------------------------------------------------------------------------------------------------------------- |
| **Collection** | A folder containing your reports and dashboards. Your LiveLike account has its own collection.                 |
| **Card**       | A single saved question (chart, table, or metric). Each Card has a `card_id` and can be queried independently. |
| **Dashboard**  | A layout of multiple Cards with shared filters. Has its own `dashboard_id`.                                    |
| **Dashcard**   | A Card placed inside a Dashboard. Has its own `dashcard_id` separate from the underlying `card_id`.            |

### Typical API Workflow

```
1. GET /api/collection/
   → Discover your collections, note the id of the relevant one

2. GET /api/collection/{id}/items
   → List cards and dashboards inside that collection

3. GET /api/card/{card_id}        ← for a single chart/metric
   GET /api/dashboard/{dashboard_id}  ← for an entire dashboard

4. POST /api/card/{card_id}/query/csv   ← download card data
   POST /api/dashboard/{dashboard_id}/dashcard/{dashcard_id}/card/{card_id}/query/csv
   ← download a specific dashboard card's data
```

<br />
