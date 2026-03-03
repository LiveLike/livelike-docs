---
title: Segment
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    You will successfully complete Livelike as Destination and Source on Segment
    after completing all the above steps. The next step is to set up the
    Rewards. Please read [this](https://docs.livelike.com/docs/rewards)
    documentation to set up rewards.
---
## What is Segment?

With Segment, you can collect, transform, send, and archive your first-party customer data. Segment simplifies the process of collecting data and connecting new tools, allowing you to spend more time using your data, and less time trying to collect it. You can use Segment to track events that happen when a user interacts with the interfaces. “Interfaces” is Segment’s generic word for any digital properties you own: your website, mobile apps, and processes that run on a server or OTT device.  
When you capture interaction data in Segment, you can send it (often in real-time) to your marketing, product, analytics tools, and data warehouses. In most cases, you won’t even need to touch your tracking code to connect to new tools.

## How Segment Works?

In a nutshell, the Segment libraries (**Sources**) generate messages about what’s happening in your site or app and send them to the Segment servers. The segment then translates the content of those messages into different formats for use by other tools (which the Segment calls **Destinations**) and sends the translated messages to those tools. The Segment servers also archive a copy of the data and can send data to your storage systems (such as databases, warehouses, or bulk-storage buckets).

![](https://files.readme.io/4989ff2-image_2.png "image (2).png")

## How Livelike and Segment will benefit your platform?

When livelike is set as the destination, the segment will send data to livelike, enabling customers to provide rewards and perform automation in response to events that occur within the source application.

**Improved User Engagement**: Livelike enables customers to offer rewards to their users in response to specific events within their source application. This can help increase user engagement and retention by providing a more personalized and gamified user experience.

**Automation**: By integrating Segment and Livelike, customers can automate the process of delivering rewards to users based on specific events or triggers within their application. This can save time and resources by eliminating the need for manual intervention.

**Enhanced Data Analysis**: Segment provides detailed insights and analytics about user behavior and interactions with the source application. By integrating with Livelike, customers can gain further insights into how users engage with reward systems and gamification features, allowing for more informed decision-making and optimization of the user experience.

**Flexibility**: Both Livelike and Segment are highly customizable and can be tailored to meet the specific needs of each individual customer. This allows for a more personalized and effective approach to engaging users and delivering rewards.

![](https://files.readme.io/4b7e416-Infographic_-1.jpg "Infographic -1.jpg")

Livelike can be configured as a **Source** as well as **Destination** on Segment Dashboard.

##

## How to configure LiveLike as a Destination on Segment Dashboard?

> 🚧 Make sure you have an account with Segment
>
> Make sure you have an account with Segment and have access to their dashboard.

We have made enabling this feature very easy for you and please follow the below steps in LiveLike CMS for integration.

1. Navigate to **Integrations** then look for Segment and click **Connect** button to start integrating.

![](https://files.readme.io/32d0f55-Screenshot_2023-02-27_at_5.28.40_PM.png "Screenshot 2023-02-27 at 5.28.40 PM.png")

#

2. Copy the **Client id** and **Producer Token**

![](https://files.readme.io/a91cdad-image_3.png "image (3).png")

From the Segment web app dashboard, navigate to Connections > Catalog. Under the Destinations tab, search for “LiveLike Cloud Mode (Actions)”, and select the destination.

#

3. Click Configure LiveLike button on the top right.

![](https://files.readme.io/6c28c83-ConfigureLL.png "ConfigureLL.png")

#

4. Select the source that will send data to “LiveLike Cloud Mode (Actions)”, click Next to enter the name of your destination.

![](https://files.readme.io/870220e-Select_source.png "Select source.png")

#

5. Enter Destination name, select Fill in settings manually and click Save

![](https://files.readme.io/31b8e76-Select_Destination.png "Select Destination.png")

#

6. Paste the corresponding Client ID and Producer Token. Enable Destination and Save Changes.

![](https://files.readme.io/b920226-CleintidToken.png "CleintidToken.png")

#

## Data flow from Segment to Livelike as Destination

![](https://files.readme.io/e81ee60-Infographic_-2.jpg "Infographic -2.jpg")

## Client Side Integration

Before sending events to Segment and making Livelike compatible to accept the data, you will need to send additional properties in the payload.  
Refer to [LiveLike Cloud Mode (Actions) Destination](https://segment.com/docs/connections/destinations/catalog/actions-livelike-cloud/) for more details.

# Segment as a source

This integration will enable you to receive related engagement and achievement data from LiveLike into your Segment instance, which can enable and enhance your automated marketing tactics and capabilities as well as augment your analytics and first-party and zero-party data for your users. This is relevant if, for example, you wanted to know when your users earned badges, completed quests, or earned rewards, in real-time.

#

## Enabling Segment source integration with LiveLike

1. From your workspace’s [Sources catalog](https://app.segment.com/goto-my-workspace/sources/catalog) page click Add Source.

<Image align="center" src="https://files.readme.io/b010850-segment-source-p1.png" />

#

2. Search for LiveLike in the Sources Catalog. Select LiveLike, and click Add Source.

<Image align="center" src="https://files.readme.io/003f87c-segment-source-p2.png" />

#

3. Give the Source a name and configure any other settings.

   The name is used as a label in the Segment app, and Segment creates a related schema name in your warehouse. The name can be anything, but Segment recommends using something that reflects the source itself and distinguishes amongst your environments (for example, LiveLike_Prod, LiveLike_Staging, LiveLike_Dev).

<Image align="center" src="https://files.readme.io/27f9cd0-segment-source-p3.png" />

#

4. Click Add Source to save your settings.
5. Copy the Write Key from the Segment UI.

<Image align="center" src="https://files.readme.io/a0da582-segment-source-p4.png" />

6. Provide the write Key to your LiveLike Account Manager so that LiveLike staff can input that write key into the platform to complete the process and enable the integration.

#

## How to configure Segment Source Integration in the LiveLike CMS

1. Go to the **Integrations** tab in the LiveLike CMS.

<Image align="center" src="https://files.readme.io/b0a7a2a-segment-source-p5.png" />

#

2. Select **Segment** from the list.
3. Enter or paste the **Write Key** from Segment in the field.

<Image align="center" src="https://files.readme.io/f2f312c-segment-source-p6.png" />

4. Press **“Connect Segment”** for finishing the setup.

#

## Data flow from Segment to LiveLike as a Source

User voted on a poll→ Earned points→ Based on the points → Badge rewarded (info) → Sent to segment

<Image align="center" src="https://files.readme.io/21d6077-segment-source-p7.jpg" />

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
| variant_id          | Quest A/B test variant ID if applicable                                   |
| variant_name        | Quest A/B test variant name if applicable                                 |

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
| variant_id                 | Quest A/B test variant ID if applicable                                   |
| variant_name               | Quest A/B test variant name if applicable                                 |

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
| variant_id               | Quest A/B test variant ID if applicable                                     |
| variant_name             | Quest A/B test variant name if applicable                                   |

## Event Properties for User Quest Completed

The table below lists the properties included in the User Quest Completed event.

| PROPERTY NAME       | DESCRIPTION                                                          |
| :------------------ | :------------------------------------------------------------------- |
| livelike_profile_id | The profile ID of the LiveLike user.                                 |
| quest_id            | The ID of the Quest.                                                 |
| quest_name          | The name of the Quest.                                               |
| user_quest_id       | The ID of the specific relationship between the User and that Quest. |
| variant_id          | Quest A/B test variant ID if applicable                              |
| variant_name        | Quest A/B test variant name if applicable                            |

<br />

## Quest Published Event

The table below lists the properties included in the Quest published event that is triggered when a quest is published via CMS.

| PROPERTY NAME       | DESCRIPTION                                                                                                                                                                                          |
| :------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| livelike_profile_id | The profile ID of the producer.                                                                                                                                                                      |
| quest_id            | The ID of the Quest.                                                                                                                                                                                 |
| quest_name          | The name of the Quest.                                                                                                                                                                               |
| quest_start_at      | The start time of quest if any.                                                                                                                                                                      |
| quest_end_at        | The end time of quest if any                                                                                                                                                                         |
| user_specific_timer | User specific timer if any                                                                                                                                                                           |
| rewards             | The quest rewards objects that includes reward_item_id, reward_item_name, reward_item_amount and test_varaint_ids (the variants associated with the reward in case the quest is part of an A/B test) |
| badges              | The quest badge object includes badge_id, badge_name, test_variant_ids (the variants associated with the reward in case the quest is part of an A/B test)                                            |
| profile_groups      | Profile Group object includes id, name                                                                                                                                                               |
| test_variants       | Includes variant_id and variant_name if quest if an A/B test quest                                                                                                                                   |

## Client Side Integration

Before sending evens to Segment and make Livelike compatible to accept the data, you will need to send additional properties in the payload

Refer [LiveLike Cloud Mode (Actions) Destination](https://segment.com/docs/connections/destinations/catalog/actions-livelike-cloud/#track-event) for more details.
