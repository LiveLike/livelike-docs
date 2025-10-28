---
title: 'Quests Guide: CMS + SDK'
excerpt: >-
  Quests allow users to complete multi-step challenges to earn one-time rewards.
  This guide explains how to create, manage, and track quests in the CMS and via
  SDK, including Save as Draft and A/B Testing features.
deprecated: false
hidden: true
metadata:
  robots: index
---
# What are Quests?

A Quest is a set of tasks a user must complete to achieve a goal.
Quest Tasks: Individual tasks within a quest.
Tasks can be completed in any order, but progress toward the overall Quest goal is tracked.

### Why use quests?

Quests give the end user a more gamified experience. They have to do multiple things in order to accomplish a single goal. During the quests, the user and integrators are able to see the progress of the quest. This progress allows the user to see how much is left in order for them to complete the quest.

Quests can be used to build things like:

* New user on-boarding checklists
* Product and feature tours
* One-time promotional campaigns

#### Creating Quests in CMS  - [How to create a Quest in CMS](https://docs.livelike.com/docs/how-to-create-a-quest-in-cms#/)

## Save Quests as Drafts

The Save as Draft feature lets producers save quests that are partially configured, so they can return later to complete and publish them. This provides flexibility for iterative creation and collaborative editing.

#### How to Save as Draft

Create a quest as above. [LINK](https://docs.livelike.com/docs/how-to-create-a-quest-in-cms#/)

#### Click Quit, then choose:

* **Save and Quit** – to save progress as a draft.
* Exit Without Saving – to discard changes.

<Image align="center" border={false} src="https://files.readme.io/7d7e6c38c4ef318b87b5d4bdd899a16e8e140a603ec81206001560b47f5153a5-Screenshot_2025-10-24_at_2.46.14_PM.png" />

> Drafts can be reopened later for editing and publishing.

<br />

#### Save as Draft-Specific Behaviour

| Behavior           | Description                                                                                                 |
| :----------------- | :---------------------------------------------------------------------------------------------------------- |
| Minimum validation | Only Quest Name is required to save as draft.                                                               |
| When can you save  | You can save and exit from any step — Basic Settings, Objectives, or Rewards                                |
| Editable           | All quest fields remain editable while the quest is in Draft state.                                         |
| Visibility         | Draft quests are not visible to end users in feeds or profiles.                                             |
| Publishing         | Once all required details are filled, click Publish (available on the Rewards step) to make the quest live. |
| Status label       | Draft quests appear under the Draft tab on the Quest List page.                                             |

#### Benefits

* Flexible workflow – Create and refine over time
* Collaborative editing – Different teams can contribute asynchronously
* Reduced last-minute stress – No rush to finalize everything before launch
* Faster go-live – Prepare, review, and publish efficiently

<br />

## A/B Testing Using Quests

The A/B Testing feature allows producers to create two variants of a single quest (Variant A and Variant B) to test different task setups, reward compositions, or difficulty levels. This helps identify which version drives higher user engagement or completion rates.

#### Creating A/B Quests in CMS - [How to Create an A/B Quest](https://docs.livelike.com/docs/how-to-create-ab-quest-in-cms#/)

> Configuring rewards is optional, but if a reward is added, it must include an assigned amount.
>
> There is no cap on the number of reward items per variant (one variant may have several, while
> the other may have none).

<br />

#### User Assignment & Tracking

* Users are randomly and evenly assigned to Variant A or Variant B the first time they encounter
  the quest.
* Assignment is handled server-side and remains consistent for the user.
* Key metrics per variant are automatically tracked for performance comparison.

<br />

#### Benefits

* Data-driven insights – Understand what setup drives engagement

* Easy experimentation – Test without duplicating quests

* Automatic tracking – System handles random assignment and logging

* Continuous optimization – Improve quest performance over time

<br />

<Accordion title="Analytics (Coming Soon)**" icon="fa-info-circle">
  Quest performance analytics will be available on the Quest Details page.

  #### **Overview (Default View)**

  Metrics shown for both A/B and non-A/B quests:

  * Reached (Exposure): total user quests created
  * Started: users who attempted ≥1 task
  * Completed: users who finished all tasks
  * Reward Claimed: users who claimed rewards (if applicable)
  * Funnel Graph: Reached → Started → Completed → Claimed

  #### Engagement (Expanded View)

  **When A/B Testing is Disabled**
  You’ll see overall engagement and completion metrics for a single quest version:

  * Conversion Rate: Started ÷ Reached
  * Completion Rate: Completed ÷ Started
  * Reward Claim Rate: Claimed ÷ Completed
  * Average Time to Completion: From created\_at to completed\_at

  **When A/B Testing is Enabled**
  Metrics are displayed side-by-side for Variant A and Variant B, allowing for easy comparison:

  * Users Assigned: Distribution check between variants

  * Conversion Rate per Variant

  * Completion Rate per Variant

  * Reward Claim Rate per Variant

  * Average Time to Completion: Compare duration across variants

  * Funnel Comparison: Visual breakdown of user flow (A vs B)

  * Performance Highlight: Current Leader — Variant X with Y% Completion
</Accordion>
