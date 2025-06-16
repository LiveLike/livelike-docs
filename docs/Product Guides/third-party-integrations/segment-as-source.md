---
title: Segment as a Source
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    You will successfully complete setting LiveLike up as a Source in Segment
    after completing all steps above. The next step is to set up the Rewards
    Table. Please read this <a
    href="https://docs.livelike.com/docs/rewards">documentation</a>to setup
    reward table
---
This integration will enable you to receive related engagement and achievement data from LiveLike into your Segment instance, which can enable and enhance your automated marketing tactics and capabilities as well as augment your analytics and first-party and zero-party data for your users. This is relevant if, for example, you wanted to know when your users earned badges, completed quests, or earned rewards, in real-time.

## Enabling Segment source integration with LiveLike

1. From your workspace’s [Sources catalog](https://app.segment.com/goto-my-workspace/sources/catalog) page click Add Source.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b010850-segment-source-p1.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


2. Search for LiveLike in the Sources Catalog. Select LiveLike, and click Add Source.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/003f87c-segment-source-p2.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


3. Give the Source a name and configure any other settings.

   The name is used as a label in the Segment app, and Segment creates a related schema name in your warehouse. The name can be anything, but Segment recommends using something that reflects the source itself and distinguishes amongst your environments (for example, LiveLike_Prod, LiveLike_Staging, LiveLike_Dev).

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/27f9cd0-segment-source-p3.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


4. Click Add Source to save your settings.
5. Copy the Write Key from the Segment UI.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a0da582-segment-source-p4.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


6. Provide the write Key to your LiveLike Account Manager so that LiveLike staff can input that write key into the platform to complete the process and enable the integration.

## How to configure Segment Source Integration in the LiveLike CMS

1. Go to the **Integrations** tab in the LiveLike CMS.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b0a7a2a-segment-source-p5.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


2. Select **Segment** from the list.
3. Enter or paste the **Write Key** from Segment in the field.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f2f312c-segment-source-p6.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


4. Press **“Connect Segment”** for finishing the setup.

## Data flow from Segment to LiveLike as a Source

User voted on a poll→ Earned points→ Based on the points → Badge rewarded (info) → Sent to segment

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/21d6077-segment-source-p7.jpg",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


## Stream

LiveLike uses Segment’s stream Source component to send Segment event data. It uses a server-side track method(s) to send data to Segment. These events are then available in any destination that accepts server-side events, and available in a schema in your data warehouse, so you can query using SQL.

The default behavior is for LiveLike to pass the userId associated with the event, which usually is your already-known userId, as well as a LiveLike User Profile ID as livelike_profile_id inside the Properties object within the Track event payload.

## Events

The table below lists events that LiveLike sends to Segment. These events appear as tables in your warehouse, and as regular events in other Destinations. LiveLike includes the userId if available.

| EVENT NAME                 | DESCRIPTION                                                |
| :------------------------- | :--------------------------------------------------------- |
| Badge Rewarded             | When a user receives a badge.                              |
| Quest Task Completed       | When a user completes a Quest Task.                        |
| Quest Reward Awarded       | When a user receives a Reward Item via a Quest Completion. |
| Reward Item Rewarded       | When a user is rewarded via a Reward Table.                |
| User Quest Task Progressed | When a user progresses a Quest Task.                       |
| User Quest Completed       | When a user completes a Quest.                             |

## Event Properties for Badge Rewarded

The table below lists the properties included in Badge Rewarded event.

| PROPERTY NAME         | DESCRIPTION                                                                       |
| :-------------------- | :-------------------------------------------------------------------------------- |
| livelike_profile_id   | The profile ID of the LiveLike user.                                              |
| badge_id              | The ID of the specific Badge the user earned.                                     |
| badge_title           | The title of the specific Badge the user earned.                                  |
| description           | The description of the specific Badge the user earned.                            |
| earned_badge_id       | The ID of the specific transaction of the user earning the Badge.                 |
| image_url             | The URL of the Badge image.                                                       |
| reward_item_id        | The ID of the Reward Item that’s associated to the threshold to earn the Badge.   |
| reward_item_name      | The name of the Reward Item that’s associated to the threshold to earn the Badge. |
| reward_item_threshold | The threshold amount of the Reward Item that’s associated to earning the Badge.   |

## Event Properties for Quest Task Completed

The table below lists the properties included in the Quest Task Completed event.

| PROPERTY NAME       | DESCRIPTION                                                               |
| :------------------ | :------------------------------------------------------------------------ |
| livelike_profile_id | The profile ID of the LiveLike user.                                      |
| quest_id            | The ID of the Quest.                                                      |
| quest_name          | The name of the Quest.                                                    |
| quest_task_id       | The ID of the specific Task within the Quest that was completed.          |
| quest_task_name     | The name of the specific Task within the Quest that was completed.        |
| user_quest_id       | The ID of the specific relationship between the User and that Quest.      |
| user_quest_task_id  | The ID of the specific relationship between the User and that Quest Task. |

## Event Properties for Quest Reward Awarded

The table below lists the properties included in the Quest Reward Awarded event.

| PROPERTY NAME              | DESCRIPTION                                                               |
| :------------------------- | :------------------------------------------------------------------------ |
| livelike_profile_id        | The profile ID of the LiveLike user.                                      |
| quest_id                   | The ID of the Quest the user completed to earn Rewards (if applicable).   |
| quest_name                 | The name of the Quest the user completed to earn Rewards (if applicable). |
| reward_item_name           | The name of the Reward Item that was rewarded.                            |
| reward_item_amount         | The amount of the Reward Item that was rewarded.                          |
| reward_item_balance        | The new balance of the Reward Item for the user.                          |
| reward_item_id             | The ID of the Reward Item that was rewarded.                              |
| reward_item_transaction_id | The ID of the transaction of the User being rewarded.                     |

## Event Properties for Reward Item Rewarded

The table below lists the properties included in the Reward Item Rewarded event.

| PROPERTY NAME              | DESCRIPTION                                           |
| :------------------------- | :---------------------------------------------------- |
| livelike_profile_id        | The profile ID of the LiveLike user.                  |
| reward_item_name           | The name of the Reward Item that was rewarded.        |
| reward_item_amount         | The amount of the Reward Item that was rewarded.      |
| reward_item_balance        | The new balance of the Reward Item for the user.      |
| reward_item_id             | The ID of the Reward Item that was rewarded.          |
| reward_item_transaction_id | The ID of the transaction of the User being rewarded. |

## Event Properties for User Quest Task Progressed

The table below lists the properties included in the User Quest Task Progressed event.

| PROPERTY NAME            | DESCRIPTION                                                                 |
| :----------------------- | :-------------------------------------------------------------------------- |
| livelike_profile_id      | The profile ID of the LiveLike user.                                        |
| quest_id                 | The ID of the Quest.                                                        |
| quest_name               | The name of the Quest.                                                      |
| quest_task_id            | The ID of the specific Task within the Quest that was completed.            |
| quest_task_name          | The name of the specific Task within the Quest that was completed.          |
| quest_task_target_value  | The target number of times this Task needs to be done to complete the Task. |
| user_quest_id            | The ID of the specific relationship between the User and that Quest.        |
| user_quest_task_id       | The ID of the specific relationship between the User and that Quest Task.   |
| user_quest_task_progress | The number of times this Task has been done so far.                         |

## Event Properties for User Quest Completed

The table below lists the properties included in the User Quest Completed event.

| PROPERTY NAME       | DESCRIPTION                                                          |
| :------------------ | :------------------------------------------------------------------- |
| livelike_profile_id | The profile ID of the LiveLike user.                                 |
| quest_id            | The ID of the Quest.                                                 |
| quest_name          | The name of the Quest.                                               |
| user_quest_id       | The ID of the specific relationship between the User and that Quest. |



## Client Side Integration

Before sending evens to Segment and make Livelike compatible to accept the data, you will need to send additional properties in the payload

Refer [LiveLike Cloud Mode (Actions) Destination](https://segment.com/docs/connections/destinations/catalog/actions-livelike-cloud/#track-event) for more details.