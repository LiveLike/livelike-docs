---
title: Analytics Dictionary
excerpt: >-
  This dictionary defines the key metrics used across both the Standard
  Analytics and Visual Analytics dashboards. Entries are grouped by feature area
  and include guidance on how to interpret each metric in context
deprecated: false
hidden: false
metadata:
  title: LiveLike Analytics Dictionary | Events Dictionary | LiveLike
  description: >-
    This is an overview about the content of the LiveLike Analytics Dashboard so
    that the users are aware of different KPIs.
  robots: index
next:
  pages:
    - slug: analytics-event-glossary
      title: Analytics Event Glossary
      type: basic
---
## Standard Analytics Metrics

The following KPIs appear in the Standard Analytics dashboard tabs.

### Applications Tab

| Metric                     | Definition                                                                                                                                                                                                                                                  |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Application**            | Name of the application                                                                                                                                                                                                                                     |
| **Organization**           | Name of the organization                                                                                                                                                                                                                                    |
| **New Profiles**           | Profiles that used the LiveLike SDK for the first time. They did not exist before the period set in the dashboard. Based on LiveLike UUIDs assigned by the SDK.                                                                                             |
| **Returning Profiles**     | Profiles that re-visited the LiveLike SDK with an existing UUID. These are profiles that were previously registered on the backend.                                                                                                                         |
| **Profiles**               | Calculated as: if unique impressions > unique interactions, then Profiles = Unique Impressions; otherwise Profiles = Unique Interactions. In most cases, Profiles ≈ Unique Impressions. On a monthly timeframe, this represents MAU (Monthly Active Users). |
| **Unique Profiles Seen**   | Combination of New Profiles and Returning Profiles.                                                                                                                                                                                                         |
| **Active PubNub Profiles** | Profiles currently connected to PubNub.                                                                                                                                                                                                                     |
| **Live Profiles**          | Profiles that are currently live (connected to PubNub). Count is always equal to Active PubNub Profiles.                                                                                                                                                    |
| **Non-Live Profiles**      | Profiles that are not connected to PubNub.                                                                                                                                                                                                                  |
| **Impressions**            | Devices/users where a widget has been published. **Unique Impression**: unique devices/users who received widgets (counted once regardless of disconnects). **Total Impression**: total count including repeat deliveries.                                  |
| **Interactions**           | Devices/users where a widget has been interacted with. **Unique Interaction**: unique devices/users who interacted (counted once). **Total Interaction**: total count including repeat interactions.                                                        |
| **Engagement**             | Calculated as: Interaction / Impression.                                                                                                                                                                                                                    |

<br />

### Programs Tab

| Metric           | Definition               |
| ---------------- | ------------------------ |
| **Program**      | Name of the program      |
| **Application**  | Name of the application  |
| **Organization** | Name of the organization |

All other KPIs (Impressions, Interactions, Engagement, etc.) carry the same definitions as the Applications tab.

### Widgets Tab

| Metric               | Definition                                  |
| -------------------- | ------------------------------------------- |
| **Widget Kind**      | Type of widget published                    |
| **Widget**           | Title of the widget                         |
| **Widget Published** | Timestamp at which the widget was published |

All other KPIs carry the same definitions as the Applications and Programs tabs.

### Chat Rooms Tab

| Metric                          | Definition                                                   |
| ------------------------------- | ------------------------------------------------------------ |
| **Chat Room**                   | Name of the chat room                                        |
| **Total Profiles**              | Total profiles registered in a particular chat group         |
| **Unique Interactive Profiles** | Unique profiles who interacted in the chat                   |
| **Messages**                    | Total number of messages sent in a chat group                |
| **Reactions**                   | Total number of reactions given in a particular chat group   |
| **Unique Profile Messages**     | Unique profiles that have sent at least 1 message            |
| **Unique Profile Reactions**    | Unique profiles that have reacted to at least 1 chat message |

### Quests Tab

| Metric               | Definition                               |
| -------------------- | ---------------------------------------- |
| **Quest**            | Name of the quest                        |
| **Quest Completion** | Indicates completion status of the quest |
| **Active Audience**  | Indicates active users of the quest      |
| **Tasks**            | Total number of quest tasks              |

### Quest Tasks Tab

| Metric              | Definition                                                               |
| ------------------- | ------------------------------------------------------------------------ |
| **Quest Task**      | Name of the quest task                                                   |
| **Task Completion** | Indicates how much percent the task has been completed                   |
| **Target**          | How many times this task should be done before it is marked as completed |

### Audience Tab

This view provides an overview of the customer base — operating systems in use, device types, and SDK versions.

> 👍 Cool Features of Livelike Analytics Dashboard
>
> To be more flexible we have provided users two additional options use and share the dashboard -
>
> 1. **Data Download** - In this dashboard there is a download option where users can download data in CSV format in their local system and derive analysis on their own
> 2. **Share Link** - One of the cool features of this dashboard is that you can share the link of a view with all the applied filters with your team members so that they can see the same view at their end. This saves time and effort when they are doing similar analysis or validation
> 3. **Search Bar** - People can search their desired data using various filters like Application ID, Program ID, Chat Room ID etc which might be beneficial to those organization which has a lot of data on the dashboard
> 4. **Navigation of inline data stored in CMS Producer Suite** - We have connected CMS links within Analytics dashboard so that people can navigate to respective Organization, Application, Programs and other different pages

***

## Visual Analytics Metrics

The following metrics appear in the Visual Analytics (Metabase-powered) dashboards. 

<Callout icon="📘" theme="info">
  #### **Note:** Metrics in the Streaks, Reward Store, and Status Tiers sections are only available in Visual Analytics dashboards where those features are enabled for your account. Contact your account manager if you need to enable additional feature analytics.
</Callout>

### Overview

| Metric / Chart                     | Definition & How to Use It                                                                                                                                                                |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Daily Active Users (DAU)**       | Distinct users who performed at least one tracked engagement action on a given day. Compared against the previous day in the Overview dashboard using a smart scalar.                     |
| **Weekly Active Users (WAU)**      | Distinct users with at least one engagement event in a rolling 7-day window. The Overview dashboard shows a week-over-week comparison.                                                    |
| **Monthly Active Users (MAU)**     | Distinct users with at least one engagement event in a rolling 30-day window. Compared month-over-month in the Overview dashboard.                                                        |
| **Distinct User Profiles Created** | Total users within the selected date range, whether they interacted or not. This is a count of all LiveLike profiles created in the application, regardless of activity.                  |
| **Total Active Users (Trend)**     | An area chart showing the trend of unique active profiles over your selected date range. Use the Interval filter to view by day, week, month, or year.                                    |
| **Active Users by Hour of Day**    | Counts of distinct active users grouped by hour of the day (UTC). Useful for identifying peak engagement windows and scheduling widget or content drops.                                  |
| **Analytics Overview Table**       | A row-per-interval summary table covering: total profiles created, total and unique active profiles, total and unique impressions, total and unique interactions, and engagement percent. |

***

### Widgets

| Metric / Chart                       | Definition & How to Use It                                                                                                                                                                            |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Unique Users per Program**         | Bar chart showing the number of distinct users who interacted with widgets in each program. Use the Program Name or Program ID filter to isolate specific programs.                                   |
| **Overall Engagement Score**         | A gauge chart showing the average engagement percentage across all widgets in the selected programs and date range. Indicates how well your widget mix is driving user interaction overall.           |
| **Widgets Published by Type**        | Bar chart showing the count of published widgets broken down by widget kind (poll, quiz, prediction, cheer-meter, etc.). Useful for understanding your content mix.                                   |
| **Top Widget Types by Engagement %** | Bar chart ranking widget types by their average engagement percentage. Use this to identify which formats are most effective with your audience.                                                      |
| **Widget Statistics Table**          | Row-per-widget table showing widget type, title, publish date, unique impressions, unique interactions, and engagement percent. Color-coded with a red-to-green scale for quick performance scanning. |
| **Engagement Percent (Widget)**      | Percentage of users who interacted with a widget out of those who were shown it. Calculated as: (Unique Interactions / Unique Impressions) × 100.                                                     |

***

### Chat

| Metric / Chart                           | Definition & How to Use It                                                                                                                                                                                                                                                         |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Number of Chat Messages**              | Combo chart showing total message volume and unique sending users over time. The two series together reveal whether message growth is driven by a broader audience or by a small group of highly active users.                                                                     |
| **Unique Users Sending a Chat Message**  | Scalar metric showing the count of distinct users who sent at least one message in the selected time range and chatroom.                                                                                                                                                           |
| **Avg. Chat Messages per User**          | Average number of chat messages a user sends within the selected time range. A rising average alongside flat unique-user counts can signal growing engagement depth among existing participants.                                                                                   |
| **Moderation Action by Number of Users** | Bar chart showing how many users received each type of moderation action (shadow ban, read-only, etc.) within the time range. Shadow-banned users can still send messages, but those messages are not visible to others. Read-only users can read messages but cannot participate. |
| **Messages Filtered by System**          | Bar chart of messages automatically filtered by the platform based on a configured dictionary of banned words. Filtered content is replaced with `***` for other users. Track this to calibrate your content filter dictionary.                                                    |
| **Messages Deleted**                     | Bar chart showing messages explicitly removed by a moderator or automated rule. Distinct from system filtering — these are post-publish removals.                                                                                                                                  |

***

### Comments

| Metric / Chart             | Definition & How to Use It                                                                                                                                                                                  |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Comment and User Count** | Combo chart showing total comments posted and unique users commenting over time. Filtered by Client ID, Date Range, Program ID, and Program Name. The two series reveal participation breadth versus depth. |
| **Avg. Comments per User** | Average number of comments submitted per user during the specified date range. Measures engagement depth — how much individual commenters are contributing.                                                 |
| **Avg. Replies per User**  | Average number of replies a user receives on their comments within the selected time range. A rising reply rate suggests content is driving genuine back-and-forth conversation.                            |
| **Reactions Trend**        | Combo chart tracking the volume of user reactions on comments over time. Reactions include emoji responses and upvotes. Use this to identify content that resonates most strongly.                          |

***

### Leaderboard

| Metric / Chart                    | Definition & How to Use It                                                                                                                                                                                       |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Number of Leaderboard Entries** | Table showing the count of leaderboard entries per leaderboard. Not affected by the date range filter — reflects total cumulative entries per leaderboard at the time of viewing.                                |
| **Games Leaderboard Entry Table** | Detailed table of leaderboard entries showing Profile ID, Custom ID, Nickname, and Score per leaderboard. Can be filtered by Leaderboard Name. Useful for reviewing top performers and validating scoring logic. |

***

### Badges

| Metric / Chart                    | Definition & How to Use It                                                                                                                                                                           |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Badges by Number of Users**     | Bar chart showing the number of users who received each badge type within the selected time range. Helps identify which badges are most commonly awarded and which may need threshold recalibration. |
| **User Badge Data**               | Table listing individual user badge grants — showing which badges each user earned and when. Accessible via the Overview dashboard's Badge Data section.                                             |
| **Distinct Users per Badge Tier** | Bar chart showing how many distinct users have earned badges at each tier level. Use this to understand the shape of your badge engagement pyramid.                                                  |

***

### Quests

| Metric / Chart                     | Definition & How to Use It                                                                                                                                                                                                          |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Auto Opt-In for Quests Enabled** | Scalar indicating whether Auto Opt-In is on for the selected application. When `true`, all users are automatically enrolled in quests; when `false`, users must opt in manually. Affects how you interpret participation baselines. |
| **Users Attempting a Quest**       | Total number of users who have attempted at least one quest. Serves as the top of the quest funnel.                                                                                                                                 |
| **Users Completing a Quest**       | Total number of users who completed at least one quest within the selected date range. Compare against users attempting to calculate funnel completion rate.                                                                        |
| **Avg. Number of Quests per User** | The average number of quests a user participates in, among users who have started at least one quest. A higher number indicates that your quest program is successfully re-engaging users across multiple campaigns.                |
| **Completion Status by Quest**     | Grouped bar chart showing the completion status (completed, in-progress, not started) broken down per quest name. Identifies which quests have healthy completion rates and where users are dropping off.                           |
| **User Funnel Analysis**           | Funnel chart (from Quest Analytics dashboard) showing user progression through: Viewed Quest → Started Quest → Completed Quest → Claimed Reward. Filter by Client ID and Quest UUID to analyse a specific campaign.                 |
| **Users Who Started Quest**        | Count of distinct users who began the selected quest. The top-of-funnel number for per-quest analysis.                                                                                                                              |
| **Users Who Completed Quest**      | Count of distinct users who finished all required tasks for the selected quest.                                                                                                                                                     |
| **Users Who Claimed Rewards**      | Count of users who claimed the reward associated with quest completion. Lower-than-expected claim rates may indicate a friction point in the reward claim flow.                                                                     |
| **Completion Rate (Quest)**        | Percentage of users who started the quest and finished all required tasks. Calculated as: (Users Completed / Users Started) × 100.                                                                                                  |
| **Rewards Claimed Rate**           | Percentage of users who completed the quest and also claimed their reward. A low claimed rate vs completion rate highlights a drop-off at the final step.                                                                           |
| **Average Completion Time**        | Median time (in hours) from a user starting a quest to completing it. Useful for calibrating quest duration and ensuring the time commitment is appropriate for your audience.                                                      |
| **User Aggregated Table**          | Per-user table showing Profile ID, Custom ID, Nickname, whether they Viewed the Quest, whether they Completed it, whether they Claimed Rewards, and their Completion Time (hours).                                                  |

***

### Streaks

| Metric / Chart                                  | Definition & How to Use It                                                                                                                                                                             |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Total Streak Challenges**                     | Total number of streak challenge enrollments across all users. Reflects overall adoption of the streak program.                                                                                        |
| **Distinct Streak Challenges**                  | Number of unique streak challenges configured for the application. Contextualises total enrollments relative to the number of active streak programs.                                                  |
| **Distinct Users (Streaks)**                    | Count of unique users who have participated in at least one streak challenge. The participation baseline for streak analytics.                                                                         |
| **Average Streak Length**                       | Mean number of consecutive qualifying days across all user streaks. A key health indicator — declining averages may suggest users are not being pulled back consistently.                              |
| **Maximum Streak Length**                       | The highest streak length achieved by any single user. Useful as a benchmark and for surfacing power-user behaviour.                                                                                   |
| **Drop Off Rate**                               | Percentage of users who started a streak but did not maintain it to a milestone. Identifies the scale of early abandonment.                                                                            |
| **Participation Rate**                          | Percentage of the total user base that has participated in at least one streak challenge. Low participation rates may indicate the streak mechanic needs greater discoverability or promotional push.  |
| **First Milestone Achievement Rate**            | Percentage of users who reached the first configured streak milestone. This is the first proof-of-engagement checkpoint and is a leading indicator of long-term streak retention.                      |
| **Final Milestone Achievement Rate**            | Percentage of users who completed the full streak challenge by reaching the final milestone. Measures end-to-end programme effectiveness.                                                              |
| **Milestone Reach Rate**                        | For a given milestone, the percentage of enrolled users who reached that specific milestone threshold. Used to map the drop-off curve across milestones.                                               |
| **Restart Rate**                                | Percentage of users whose streak was broken (reset to zero) but who subsequently restarted. A high restart rate indicates the programme is compelling enough to re-engage users after they fail.       |
| **Freeze Rate**                                 | Percentage of streaks that used a freeze (a streak protection mechanism that prevents a break for one missed day). Monitors how heavily users are relying on the safety net.                           |
| **Average Freeze Hours**                        | Mean duration (in hours) for which users activated a streak freeze. Longer average freeze use may indicate your daily task window is not well-aligned with user schedules.                             |
| **Distribution of Streaks**                     | Bar chart bucketing all streaks by their length (e.g., 1–3 days, 4–7 days, 8–14 days). Useful for identifying natural drop-off points and sizing incentive milestones appropriately.                   |
| **Distribution of Users Across Streak Lengths** | Bar chart showing how many users are clustered at each streak length bucket. Reveals where the largest user cohorts sit and which milestone thresholds matter most.                                    |
| **Streak Drop Off Rate by Streak Length**       | Bar chart mapping drop-off rate at each streak length increment. Spikes at specific lengths identify the hardest days to maintain a streak — and the most valuable places to add rewards or reminders. |
| **Streak Activity over the Days**               | Line chart showing daily streak activity (qualifying interactions) over the selected date range. Use this to correlate streak engagement with external events like match days or content drops.        |
| **Streak Creation Distribution**                | Bar chart showing when user streaks were first created (i.e., when users first enrolled). Useful for evaluating campaign launches and promotion timing.                                                |
| **Completed Streak Participation**              | Bar chart showing the volume of fully completed streak challenges over time. Compare against total attempts to track your overall streak completion rate trend.                                        |
| **Total Streak Milestones Reached**             | Scalar showing the cumulative number of milestone completions across all users and all challenges.                                                                                                     |
| **Distinct Streak Milestones**                  | Number of unique milestone checkpoints across all configured streak challenges.                                                                                                                        |
| **Average Milestone Length**                    | Mean number of days required to reach a milestone across all configured milestones.                                                                                                                    |
| **Milestone Distribution**                      | Bar chart showing how milestone completions are distributed across different milestone thresholds. Identifies which milestones are reached frequently and which are rarely achieved.                   |
| **Streak Milestones per Day**                   | Line chart of daily milestone completions. Spikes correspond to milestone-driven reward events and can indicate how effectively milestone incentives are driving daily returns.                        |
| **Total Rewards (Streaks)**                     | Total number of rewards issued to users who reached streak milestones. Reflects the volume of the streak reward economy.                                                                               |
| **Average Reward Amount**                       | Mean reward value (in points or configured currency) granted per streak milestone completion.                                                                                                          |
| **Reward Redemption Rate (Streaks)**            | Percentage of streak-earned rewards that users actually redeemed. Useful in conjunction with Reward Store data to measure the full lifecycle of streak rewards.                                        |
| **Percent of Streaks with User Goal Applied**   | Percentage of active streaks where a user-defined goal has been set. Indicates adoption of the goal-setting feature, where available.                                                                  |
| **Freeze Distribution**                         | Bar chart showing how freeze usage is distributed across users — i.e., how many users used 0, 1, 2, or more freezes. High usage at 0 freezes may indicate users aren't aware of the feature.           |
| **Current Streak Length**                       | The current active streak length for users at time of viewing. Useful for identifying users who are close to a milestone and may benefit from a nudge.                                                 |
| **Total Streak Activity**                       | Total count of qualifying streak activity events recorded. Serves as a raw volume measure of streak engagement.                                                                                        |

***

### Reward Store

| Metric / Chart                              | Definition & How to Use It                                                                                                                                                                           |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Total Rewards Redeemed from Store**       | Scalar showing the total number of items redeemed from the reward store. The headline metric for store activity.                                                                                     |
| **Total Reward Points Spent**               | Total loyalty points spent by users on store redemptions. Compare against total points issued to calculate your overall redemption rate.                                                             |
| **Distinct Transactions per Product (SKU)** | Bar chart showing the number of unique redemption transactions per reward item. Use this to identify your most popular items and items that are not moving.                                          |
| **Total Orders by Reward Amount**           | Pie chart showing the breakdown of redemption orders by their point cost. Reveals whether users are predominantly redeeming low-cost or high-cost items.                                             |
| **Weekly Order Trends Across SKUs**         | Line chart tracking weekly redemption volume per reward item (SKU). Use to spot seasonal trends, identify items that spike after promotions, and find items with declining interest.                 |
| **Reward Transaction History**              | Row-level transaction table showing Product Name, UUID, Custom User ID, Quantity, Point Amount, and Time of Order for every redemption. Useful for audits, debugging, and user-level investigations. |
