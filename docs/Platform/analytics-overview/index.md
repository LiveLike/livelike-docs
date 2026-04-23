---
title: Analytics
excerpt: Understand your integration performance and user behaviors
deprecated: false
hidden: false
metadata:
  title: Analytics | LiveLike Developer Hub | Engagement SDK
  description: >-
    LiveLike provides you with a suite of analytics tools customized to suit
    your needs. Learn more about daily reports, available metrics, and more.
  robots: index
next:
  pages:
    - slug: analytics-dashboard
      title: Analytics Dashboard
      type: basic
---
The LiveLike Producer Site includes a built-in analytics section accessible from the left navigation. As soon as the integration with LiveLike is launched, we start collecting data that can be used to track your success. This data helps you understand your programs' engagement performance and the usage behaviors of your audience, resulting in increased participation, engagement, and retention.

## How to access your data

We provide three ways to access and work with engagement data from your application:

| Option                 | What it is                                                   | Access                                 | Best for                                                              |
| ---------------------- | ------------------------------------------------------------ | -------------------------------------- | --------------------------------------------------------------------- |
| **Standard Analytics** | Pre-built reports in the Producer Site                       | Standard (available to all)            | Quick engagement metrics without any setup                            |
| **Visual Analytics**   | Interactive Metabase-powered dashboards in the Producer Site | Add-on (contact your account manager)  | Richer charts, multiple tabs, and deeper drill-downs                  |
| **Analytics API**      | Programmatic access to Visual Analytics data                 | API key (contact your account manager) | Pulling data into a BI tool, automating exports, external integration |

By default the Producer Site opens the **Standard Analytics** dashboard. Accounts with Visual Analytics enabled will see the Visual Analytics dashboard in its place.

***

## Standard Analytics

The Standard Analytics dashboard is available to all customers directly in the Producer Site. It provides pre-built reports generated from data collected by the LiveLike platform - no setup required.

### What it covers

* Application-level metrics — engagement summaries across your application
* Program-level metrics — performance comparisons program over program
* Widget-level metrics — individual interactive widget results
* Quest metrics — completion status and active users per quest
* Quest Task metrics — task-level completion breakdown

For full details, see the [Analytics Dashboard](https://docs.livelike.com/reference/get_collections) documentation.

***

## Visual Analytics

Visual Analytics provides an interactive data exploration experience embedded in the Producer Site. It is available as an add-on and offers richer, drill-down reporting across multiple dashboard tabs - including custom tabs configured for your specific product.

### Default dashboard tabs

* **Overview** : high-level engagement KPIs across your application - active users, session counts, total widget interactions, and trend lines over your selected date range
* **Widgets** : widget-specific performance broken down by type - impression counts, interaction rates, and completion rates for polls, predictions, quizzes, and other widget formats
* **Quest** : participation funnels, completion rates, drop-off points
* **Chat** : message volume over time, unique active chatters, reaction counts, and moderation event frequency

### Additional tabs

Accounts may have additional tabs configured based on their product - such as Leaderboard, Arcade game-specific tabs (Skilled Games, Non-Skilled Games), or custom requirements. Contact your LiveLike account manager for details.

For full details, see the [Visual Analytics](https://docs.livelike.com/docs/analytics-dashboard) documentation.

***

## Analytics API

The Analytics API gives you programmatic access to your analytics data - collections, cards (individual charts), and dashboards. Use it to pull data into your own systems, build custom reports, or automate exports.

### Authentication

All requests require the `x-api-key` header. Your API key is scoped to your organization and controls which collections and dashboards you can access.

> **Note**: Analytics API keys are separate from Producer Tokens. To obtain your Analytics API key, please reach out to your LiveLike Account Manager or designated Point of Contact.

### Quick reference

* **Base URL:** `https://metabase.livelikecdn.com/api/`
* **Authentication:** `x-api-key` header (scoped to your organization)

### Concepts

| Term           | Description                                                                                                      |
| -------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Collection** | A folder grouping related dashboards and cards. Your org will have at least one top-level collection.            |
| **Card**       | A single chart, table, or scalar metric - the building block of a dashboard. Each card runs an underlying query. |
| **Dashboard**  | A layout of multiple cards, optionally with shared filter controls and tabs.                                     |
| **Dashcard**   | A Card placed inside a Dashboard. Has its own `dashcard_id` separate from the underlying `card_id`.              |

For full details, see the [Analytics API](https://docs.livelike.com/reference/get_collections) documentation.

***

## SDK Analytics Hooks

In addition to the dashboards above, LiveLike SDKs emit client-side events that you can send to your own analytics service. These events are generated in the SDK and are not collected by the LiveLike platform, but they can augment your own application analytics.

### Platform guides

* [iOS Analytics](https://docs.livelike.com/docs/ios-analytics)
* [Android Analytics](https://docs.livelike.com/docs/android-analytics)
* [Web Analytics](https://docs.livelike.com/docs/web-custom-analytics)
* [React Native Analytics](https://docs.livelike.com/docs/react-native-analytics)

### Available data points

The SDKs provide data points related to user widgets, chat, stickers, reactions, and more:

* Widget impression counts and engagement rates
* Poll, quiz, prediction, and other widget interaction counts
* Chat message activity
* Chat sticker and message reactions activity

See the [Analytics Event Glossary](https://docs.livelike.com/docs/analytics-event-glossary) for the full list.
