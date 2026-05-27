---
title: Dynamic Profile Group Rule Structure
excerpt: >-
  This page provides an overview of the rule creation flow for Dynamic Profile
  Groups via APIs.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Basic Rule Tree Sructure

The rule trees to be passed in the JSON payload for profile group creation API follow a basic structure as shown below:

```json
{
  "operator": "AND",
  "children": [
    {
      "operator": "OR",
      "children": [
        {
          "attribute": "attribute_1",
          "condtion": "condition_1",
          "value": "value_1"
        },
        {
          "attribute": "attribute_2",
          "condition": "condition_2",
          "value": "value_2"
        }
      ]
    },
    {
      "operator": "OR",
      "children": [
        {
          "attribute": "attribute_3",
          "condtion": "condition_3",
          "value": "value_3"
        },
        {
          "attribute": "attribute_4",
          "condition": "condition_4",
          "value": "value_4"
        }
      ]
    }
  ]
}
```

We create rule groups with **OR** operators between them and combine them with **AND**.

The structure is always maintained like:

> **(Rule-1 OR Rule-2..) AND (Rule-3 OR Rule-4...)**

with certain guardrails:

* Only allowed attributes, conditions and operators must be used.
* Leaf nodes must always have (attribute, condition, value) combination
* At max,  rules should be added.
* Root operator should be AND, even though it's always internally normalized to set it to AND.

<br />

## List of Available Conditions

<br />

| Operator                 | Key                   | Accepted Values                               |
| :----------------------- | :-------------------- | :-------------------------------------------- |
| Equals                   | equals                | String, number, datetime                      |
| Not Equals               | not_equals            | String, number, datetime                      |
| Greater Than or Equal to | greater_than_or_equal | String, number, datetime                      |
| Less Than or Equal to    | less_than_or_equal    | String, number, datetime                      |
| Greater Than             | greater_than          | String, number, datetime                      |
| Less Than                | less_than             | String, number, datetime                      |
| Contains                 | contains              | String                                        |
| Not Contains             | not_contains          | String                                        |
| Ends With                | ends_with             | String                                        |
| In                       | in                    | List of String, number, datetime              |
| Not In                   | not_in                | List of String, number, datetime              |
| Between                  | between               | List of two values (String, number, datetime) |
| Before                   | before                | Datetime                                      |
| After                    | after                 | Datetime                                      |
| Within Last X Days       | within_last_x_days    | Integer                                       |
| Is                       | is                    | True, False                                   |
| Is Empty                 | is_empty              | True, False                                   |
| Is Not Empty             | is_not_empty          | True, False                                   |

## List of Available Attributes

| Attribute                      | Key                                | Description                                            | Allowed conditions                                                                              |
| :----------------------------- | :--------------------------------- | :----------------------------------------------------- | :---------------------------------------------------------------------------------------------- |
| Total Comments Posted          | **total_comments_posted**          | Number of comments posted by a user                    | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Total Comment Replies          | **total_comment_replies**          | Number of comment replies posted by a user             | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Total Comments Reported        | **total_comments_reported**        | Number of comments from a user that have been reported | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Last Comment At                | **last_comment_at**                | The last time when a user posted a comment             | Before, After, Between, Within Last X Days                                                      |
| Has Ever Commented             | **has_ever_commented**             | If a user has ever posted a comment                    | Is                                                                                              |
| Created At                     | **created_at**                     | When a user was created                                | Before, After, Between, Within Last X Days                                                      |
| Has Social Connections         | **has_social_connections**         | If a user has any social connections                   | Is                                                                                              |
| Total Active Quests            | **total_active_quests**            | Number of active quests a user has                     | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Total Completed Quests         | **total_quests_completed**         | Number of completed quests a user has                  | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Total Failed Quests            | **total_failed_quests**            | Number of failed quests a user has                     | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Quest Completion Rate          | **quest_completion_rate**          | Quest Completion Rate for a user                       | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal                     |
| Completed Any Quest            | **completed_any_quest**            | If a user has ever completed any quest                 | Is                                                                                              |
| Ever Started Quest             | **ever_started_quest**             | If a user has ever started a quest                     | Is                                                                                              |
| Quest Rewards Claimed          | **quest_rewards_claimed**          | Number of quest rewards a user has claimed             | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Quest Rewards Unclaimed        | **quest_rewards_unclaimed**        | Number of quest rewards a user has left unclaimed      | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Quest Rewards Earned           | **quest_rewards_earned**           | Number of quest rewards a user has earned              | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Has Unclaimed Quest Rewards    | **has_unclaimed_quest_rewards**    | If a user has any unclaimed quest rewards              | Is                                                                                              |
| Last Started Quest At          | **last_quest_started_at**          | The last time a user started a quest                   | Before, After, Between, Within Last X Days                                                      |
| Last Completed Quest At        | **last_quest_completed_at**        | The last time a user completed a quest                 | Before, After, Between, Within Last X Days                                                      |
| Current Streak Length          | **current_streak_length**          | The current length of a streak a user has              | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Longest Streak Length          | **longest_streak_length**          | The longest length of a streak a user has had          | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| First Streak Activity At       | **first_streak_activity**          | The first time a user had streak activity              | Before, After, Between, Within Last X Days                                                      |
| Last Streak Activity At        | **last_streak_activity**           | The last time a user had streak activity               | Before, After, Between, Within Last X Days                                                      |
| Streak Milestones Reached      | **streak_milestones_reached**      | Number of streak milestones a user has reached         | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Streak Reset Count             | **streak_reset_count**             | Number of times a streak has been reset for a user     | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Has Ever Started Streak        | **has_ever_started_streak**        | If a user has ever started a streak                    | Is                                                                                              |
| Has an Active Streak           | **is_streak_active**               | If a user has an active streak                         | Is                                                                                              |
| Has a Frozen Streak            | **is_streak_frozen**               | If a user has a frozen streak                          | Is                                                                                              |
| Periodic Streak Length         | **periodic_streak_length**         | The length of a periodic streak a user has             | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Consecutive Streak Length      | **consecutive_streak_length**      | The length of a consecutive action streak a user has   | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Status Tier                    | **status_tier**                    | The current status tier a user has                     | Equals, Not Equals                                                                              |
| Current Tier Rank              | **current_tier_rank**              | The current tier rank a user has                       | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Last Tier Change At            | **last_tier_change_at**            | The last time a user got a tier change                 | Before, After, Between, Within Last X Days                                                      |
| Has Ever Upgraded Tier         | **have_ever_upgraded_tier**        | If a user has ever upgraded a tier                     | Is                                                                                              |
| Tier Entry Date                | **tier_entry_date**                | The date a user entered the tier they currently have   | Before, After, Between, Within Last X Days                                                      |
| Days in Current Tier           | **days_in_current_tier**           | Number of days a user has spent in their current tier  | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Tier Upgrade Count             | **tier_upragde_count**             | Number of times a user has their tier upgraded         | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Tier Downgrade Count           | **tier_downgrade_count**           | Number of times a user has their tier downgraded       | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Has Ever Reached a Tier        | **has_ever_reached_tier**          | If a user has ever reached a tier                      | Is                                                                                              |
| Reward Balance                 | **reward_balance**                 | The reward balance a user has                          | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Total Earned Reward Balance    | **reward_balance_total_earned**    | The total reward balance a user has ever earned        | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Total Reward Balance Spent     | **reward_balance_total_spent**     | The total reward balance a user has spent              | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Last Reward Earned At          | **last_reward_earned_at**          | The last time a user earned a reward                   | Before, After, Between, Within Last X Days                                                      |
| Total Reward Actions Triggered | **reward_actions_triggered_total** | Number of reward actions a user has triggered          | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Has Earned Any Reward          | **has_earned_any_reward**          | If a user has ever earned a reward                     | Is                                                                                              |
| Leaderboards Ranked On         | **leaderboards_ranked_on**         | Number of leaderboards a user has been ranked on       | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
| Is Ranked on Any Leaderboard   | **is_ranked_on_leaderboard**       | If a user is ranked on any leaderboard                 | Is                                                                                              |
| Leaderboard Views Count        | **leaderboard_views_count**        | Number of leaderboard views for a user                 | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |