---
title: Rewards
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Rewards | LiveLike Developer Hub | Fan Engagement Suite
  description: >-
    Rewards are digital goods that users can earn, accumulate, or collect. Your
    apps can use rewards to make things more fun and engaging.
  robots: index
next:
  description: Setup a Leaderboard to let users compete with Rewards!
  pages:
    - type: basic
      slug: leaderboards
      title: Leaderboards
    - type: endpoint
      slug: invoking-custom-actions
      title: Invoking custom actions
---
Rewards are digital goods managed by LiveLike that users can earn, accumulate, or collect. Your apps can use rewards to make things more fun and engaging, and to encourage users to feel invested in your products. When paired with the [Leaderboards](doc:leaderboards) system, it can make for a more competitive and challenging experience.

The Rewards system provides customization, inventory management, balance tracking, and rule-based automation to allow you to design the exact experience you need.
[block:api-header]
{
  "title": "Rewards Overview"
}
[/block]
The Rewards system is made up of a few components that can be configured in order to create a customized experience for your users. The components are:

* **Items**. An item is a blueprint of a reward that a user can earn. You can set up as many of them as you would like. Users can collect and accumulate items, so they can work like score, XP, or collectibles.
* **Actions**. An action is something a user can do in order to earn rewards. There are a number of built-in actions like voting on polls and answering quizzes correctly. You can also create your own actions, like "invited a friend" or "completed your profile."
* **Tables**. A table is a set of actions and items that determines the rewards users earn for performing those actions. You can have many tables so that many scenarios can be supported concurrently. For example, you might want different tables for different sports, or for regular seasons and playoffs. 
[block:api-header]
{
  "title": "Reward Items"
}
[/block]
A Reward Item defines the properties of a type of reward a user can earn. Once you create a Reward Item it can be set up to be given to users automatically based on their activity through Reward Tables and Quests. 
[block:api-header]
{
  "title": "Reward Actions"
}
[/block]
Rewards can be set up to be earned automatically by associating them with *actions*. An action is something that the user does that the system recognizes as having the potential for earning a reward. There some built-in actions for interacting with [widgets](doc:widgets):

* Voting on a poll widget
* Answering a quiz widget correctly
* Replying to an ask widget

You can also register **custom actions** to reward users for doing things outside of the LiveLike system. Some example custom actions include:

* Making a purchase
* Inviting a friend
* Reading an article
* Watching a video

Once you recognize that a user has performed that action, you can [invoke the action](ref:invoking-custom-actions) to trigger it and grant rewards from Reward Tables and Quests.
[block:api-header]
{
  "title": "Reward Tables"
}
[/block]
Tables make it easy to automate earning rewards and can be re-used by many programs. A table consists of a list of *entries*, and each entry has an action, a reward item, and an amount. Each time a user performs an action in a program, all of the reward tables linked to the program are consulted. For each entry that matches the action, the reward is earned by the user who performed the action.

An integration can have multiple reward tables concurrently. Some use cases for multiple reward tables include:

* An app featuring matches from different sports, and each sport has its own reward schedule and items
* Basic rewards during the regular season, and bigger rewards during the playoffs and finals
* Customized rewards for one-time events like tournaments or exhibitions
[block:callout]
{
  "type": "info",
  "title": "Use Quests for incentivizing user journeys and funnel optimizations",
  "body": "Reward Tables are great for recurring rewards, like for giving points each time a user votes on a poll or refers a friend. Quests are better for one-time rewards with complex criteria. Read more about [quests](doc:quests) to see how you can use them in your apps."
}
[/block]