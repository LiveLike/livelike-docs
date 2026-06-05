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

With Segment, you can collect, transform, send, and archive your first-party customer data. Segment simplifies the process of collecting data and connecting new tools, allowing you to spend more time using your data, and less time trying to collect it. You can use Segment to track events that happen when a user interacts with the interfaces. “Interfaces” is Segment’s generic word for any digital properties you own: your website, mobile apps, and processes that run on a server or OTT device.<br />When you capture interaction data in Segment, you can send it (often in real-time) to your marketing, product, analytics tools, and data warehouses. In most cases, you won’t even need to touch your tracking code to connect to new tools.

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

Before sending events to Segment and making Livelike compatible to accept the data, you will need to send additional properties in the payload.<br />Refer to [LiveLike Cloud Mode (Actions) Destination](https://segment.com/docs/connections/destinations/catalog/actions-livelike-cloud/) for more details.

# Segment as a source

This integration will enable you to receive related engagement and achievement data from LiveLike into your Segment instance, which can enable and enhance your automated marketing tactics and capabilities as well as augment your analytics and first-party and zero-party data for your users. This is relevant if, for example, you wanted to know when your users earned badges, completed quests, or earned rewards, in real-time.

#

## Enabling Segment source integration with LiveLike

1. From your workspace’s [Sources catalog](https://app.segment.com/goto-my-workspace/sources/catalog) page click Add Source.


<Image src="https://files.readme.io/b010850-segment-source-p1.png" align="center" />


#

2. Search for LiveLike in the Sources Catalog. Select LiveLike, and click Add Source.


<Image src="https://files.readme.io/003f87c-segment-source-p2.png" align="center" />


#

3. Give the Source a name and configure any other settings.

   The name is used as a label in the Segment app, and Segment creates a related schema name in your warehouse. The name can be anything, but Segment recommends using something that reflects the source itself and distinguishes amongst your environments (for example, LiveLike\_Prod, LiveLike\_Staging, LiveLike\_Dev).


<Image src="https://files.readme.io/27f9cd0-segment-source-p3.png" align="center" />


#

4. Click Add Source to save your settings.
5. Copy the Write Key from the Segment UI.


<Image src="https://files.readme.io/a0da582-segment-source-p4.png" align="center" />


6. Provide the write Key to your LiveLike Account Manager so that LiveLike staff can input that write key into the platform to complete the process and enable the integration.

#

## How to configure Segment Source Integration in the LiveLike CMS

1. Go to the **Integrations** tab in the LiveLike CMS.


<Image src="https://files.readme.io/b0a7a2a-segment-source-p5.png" align="center" />


#

2. Select **Segment** from the list.
3. Enter or paste the **Write Key** from Segment in the field.


<Image src="https://files.readme.io/f2f312c-segment-source-p6.png" align="center" />


4. Press **“Connect Segment”** for finishing the setup.

#

## Data flow from Segment to LiveLike as a Source

User voted on a poll→ Earned points→ Based on the points → Badge rewarded (info) → Sent to segment


<Image src="https://files.readme.io/21d6077-segment-source-p7.jpg" align="center" />


## Stream

LiveLike uses Segment’s stream Source component to send Segment event data. It uses a server-side track method(s) to send data to Segment. These events are then available in any destination that accepts server-side events, and available in a schema in your data warehouse, so you can query using SQL.

The default behavior is for LiveLike to pass the userId associated with the event, which usually is your already-known userId, as well as a LiveLike User Profile ID as livelike\_profile\_id inside the Properties object within the Track event payload.

## Events

The table below lists events that LiveLike sends to Segment. These events appear as tables in your warehouse, and as regular events in other Destinations. LiveLike includes the userId if available.

| EVENT NAME                 | DESCRIPTION                                                            |
| :------------------------- | :--------------------------------------------------------------------- |
| Badge Rewarded             | When a user receives a badge.                                          |
| Quest Task Completed       | When a user completes a Quest Task.                                    |
| Quest Reward Awarded       | When a user receives a Reward Item via a Quest Completion.             |
| Reward Item Rewarded       | When a user is rewarded via a Reward Table.                            |
| User Quest Task Progressed | When a user progresses a Quest Task.                                   |
| User Quest Completed       | When a user completes a Quest.                                         |
| Quest Published            | When a quest is published for users to interact with.                  |
| A/B Test Variant Assigned  | When a user is assigned an A/B test variant in a quest.                |
| Streak Published           | When a streak was published by the admin.                              |
| Streak Progressed          | When a user completes an eligible action that advances their streak.   |
| Streak Milestone Achieved  | When a user reaches a milestone threshold (streak length) in a streak. |
| Streak Reset               | When a user's streak is broken due to inactivity or failure.           |

## Event Properties for Badge Rewarded

The table below lists the properties included in Badge Rewarded event.

| PROPERTY NAME           | DESCRIPTION                                                                                                     |
| :---------------------- | :-------------------------------------------------------------------------------------------------------------- |
| livelike\_profile\_id   | The profile ID of the LiveLike user.                                                                            |
| badge\_id               | The ID of the specific Badge the user earned.                                                                   |
| badge\_title            | The title of the specific Badge the user earned.                                                                |
| description             | The description of the specific Badge the user earned.                                                          |
| earned\_badge\_id       | The ID of the specific transaction of the user earning the Badge.                                               |
| image\_url              | The URL of the Badge image.                                                                                     |
| source                  | The trigger point or origin of the badge that user earned.                                                      |
| quest\_id               | The ID of Quest, if source of badge was a quest completion.                                                     |
| quest\_name             | The name of Quest, if source of badge was a quest completion.                                                   |
| user\_quest\_id         | The ID of the specific relationship between the User and that Quest, if source of badge was a quest completion. |
| variant\_id             | The ID of the A/B quest variant that was assigned to the user, if source was an A/B Quest.                      |
| variant\_name           | The name of the A/B quest variant that was assigned to the user, if source was an A/B Quest.                    |
| reward\_item\_id        | The ID of the Reward Item that’s associated to the threshold to earn the Badge, if source was Reward Item.      |
| reward\_item\_name      | The name of the Reward Item that’s associated to the threshold to earn the Badge, if source was Reward Item.    |
| reward\_item\_threshold | The threshold amount of the Reward Item that’s associated to earning the Badge, if source was Reward Item.      |

## Event Properties for Quest Task Completed

The table below lists the properties included in the Quest Task Completed event.

| PROPERTY NAME         | DESCRIPTION                                                               |
| :-------------------- | :------------------------------------------------------------------------ |
| livelike\_profile\_id | The profile ID of the LiveLike user.                                      |
| quest\_id             | The ID of the Quest.                                                      |
| quest\_name           | The name of the Quest.                                                    |
| quest\_task\_id       | The ID of the specific Task within the Quest that was completed.          |
| quest\_task\_name     | The name of the specific Task within the Quest that was completed.        |
| user\_quest\_id       | The ID of the specific relationship between the User and that Quest.      |
| user\_quest\_task\_id | The ID of the specific relationship between the User and that Quest Task. |
| variant\_id           | The ID of the A/B Test variants in Quest.                                 |
| variant\_name         | The name of the A/B Test variants in Quest.                               |

## Event Properties for Quest Reward Awarded

The table below lists the properties included in the Quest Reward Awarded event.

| PROPERTY NAME                 | DESCRIPTION                                                               |
| :---------------------------- | :------------------------------------------------------------------------ |
| livelike\_profile\_id         | The profile ID of the LiveLike user.                                      |
| quest\_id                     | The ID of the Quest the user completed to earn Rewards (if applicable).   |
| quest\_name                   | The name of the Quest the user completed to earn Rewards (if applicable). |
| reward\_item\_name            | The name of the Reward Item that was rewarded.                            |
| reward\_item\_amount          | The amount of the Reward Item that was rewarded.                          |
| reward\_item\_balance         | The new balance of the Reward Item for the user.                          |
| reward\_item\_id              | The ID of the Reward Item that was rewarded.                              |
| reward\_item\_transaction\_id | The ID of the transaction of the User being rewarded.                     |
| variant\_id                   | The ID of the A/B Test variants in Quest.                                 |
| variant\_name                 | The name of the A/B Test variants in Quest.                               |

## Event Properties for Reward Item Rewarded

The table below lists the properties included in the Reward Item Rewarded event.

| PROPERTY NAME                 | DESCRIPTION                                           |
| :---------------------------- | :---------------------------------------------------- |
| livelike\_profile\_id         | The profile ID of the LiveLike user.                  |
| reward\_item\_name            | The name of the Reward Item that was rewarded.        |
| reward\_item\_amount          | The amount of the Reward Item that was rewarded.      |
| reward\_item\_balance         | The new balance of the Reward Item for the user.      |
| reward\_item\_id              | The ID of the Reward Item that was rewarded.          |
| reward\_item\_transaction\_id | The ID of the transaction of the User being rewarded. |

## Event Properties for User Quest Task Progressed

The table below lists the properties included in the User Quest Task Progressed event.

| PROPERTY NAME               | DESCRIPTION                                                                 |
| :-------------------------- | :-------------------------------------------------------------------------- |
| livelike\_profile\_id       | The profile ID of the LiveLike user.                                        |
| quest\_id                   | The ID of the Quest.                                                        |
| quest\_name                 | The name of the Quest.                                                      |
| quest\_task\_id             | The ID of the specific Task within the Quest that was completed.            |
| quest\_task\_name           | The name of the specific Task within the Quest that was completed.          |
| quest\_task\_target\_value  | The target number of times this Task needs to be done to complete the Task. |
| user\_quest\_id             | The ID of the specific relationship between the User and that Quest.        |
| user\_quest\_task\_id       | The ID of the specific relationship between the User and that Quest Task.   |
| user\_quest\_task\_progress | The number of times this Task has been done so far.                         |
| variant\_id                 | The ID of the A/B Test variant assigned to a user in Quest.                 |
| variant\_name               | The name of the A/B Test variant assigned to a user in Quest.               |

## Event Properties for User Quest Completed

The table below lists the properties included in the User Quest Completed event.

| PROPERTY NAME         | DESCRIPTION                                                          |
| :-------------------- | :------------------------------------------------------------------- |
| livelike\_profile\_id | The profile ID of the LiveLike user.                                 |
| quest\_id             | The ID of the Quest.                                                 |
| quest\_name           | The name of the Quest.                                               |
| user\_quest\_id       | The ID of the specific relationship between the User and that Quest. |
| variant\_id           | The ID of the A/B Test variant assigned to a user in Quest.          |
| variant\_name         | The name of the A/B Test variant assigned to a user in Quest.        |

## Event Properties for Quest Published

The table below lists the properties included in the Quest Published event.

| PROPERTY NAME         | DESCRIPTION                                                     |
| :-------------------- | :-------------------------------------------------------------- |
| livelike\_profile\_id | The profile ID of the producer.                                 |
| quest\_id             | The ID of the Quest.                                            |
| quest\_name           | The name of the Quest.                                          |
| quest\_start\_at      | The start time of Quest, if any.                                |
| quest\_end\_at        | The end time of Quest, if any.                                  |
| user\_specific\_timer | The user-specific duration of Quest, if any.                    |
| rewards               | The object with details for quest reward items.                 |
| badges                | The object with details for quest badges.                       |
| profile\_groups       | The object with details of user groups linked to Quest, if any. |
| test\_variants        | The object with details of A/B Test variant in a quest, if any. |

## Event Properties for A/B Test Variant Assignment

The table below outlines the properties included in the A/B Test Variant Assignment event.

| PROPERTY NAME         | DESCRIPTION                                                              |
| :-------------------- | :----------------------------------------------------------------------- |
| livelike\_profile\_id | The profile ID of the LiveLike user.                                     |
| quest\_id             | The ID of the Quest.                                                     |
| quest\_name           | The name of the Quest.                                                   |
| variant\_id           | The ID of the A/B Test variant that was assigned to the user in Quest.   |
| variant\_name         | The name of the A/B Test variant that was assigned to the user in Quest. |

## Event Properties for Streak Published

The table below outlines the properties included in the Streak Published event.

| PROPERTY NAME     | DESCRIPTION                                                                                                             |
| :---------------- | :---------------------------------------------------------------------------------------------------------------------- |
| streak\_id        | The unique ID of the streak.                                                                                            |
| streak\_name      | The name of the streak.                                                                                                 |
| streak\_type      | The type of streak (periodic, consecutive\_action).                                                                     |
| user\_action\_id  | The ID of the action that counted toward progress.                                                                      |
| user\_action\_key | The unique key of the user action.                                                                                      |
| user\_groups      | Array of User Group IDs that can participate (null = all users).                                                        |
| milestones        | Object of milestone IDs, threshold streak length, reward\_id, reward\_name and reward\_amount attached with the streak. |
| start\_date       | Start date if configured (null if starts immediately).                                                                  |
| end\_date         | End date if configured (null if ongoing).                                                                               |
| timezone          | The timezone configuration for the streak.                                                                              |
| published\_by     | The ID of the admin who published the streak.                                                                           |
| published\_at     | Timestamp when the streak was published.                                                                                |

## Event Properties for Streak Progressed

The table below outlines the properties included in the Streak Progressed event.

| PROPERTY NAME              | DESCRIPTION                                                                 |
| :------------------------- | :-------------------------------------------------------------------------- |
| livelike\_profile\_id      | The profile ID of the LiveLike user.                                        |
| user\_streak\_id           | The unique ID of the user's streak instance.                                |
| streak\_id                 | The unique ID of the streak.                                                |
| streak\_name               | The name of the streak.                                                     |
| streak\_type               | The type of streak (consecutive\_action, periodic).                         |
| target\_id                 | The object on which streak progress happened (widget\_id, video\_id, etc.)  |
| current\_streak\_length    | The current length/count of the user's streak.                              |
| max\_streak\_length        | The maximum length a user achieved for this streak.                         |
| user\_action\_id           | The ID of the action that counted toward progress.                          |
| user\_action\_key          | The unique key of the user action.                                          |
| next\_milestone\_threshold | The next milestone threshold (null if no more milestones).                  |
| progressed\_at             | Timestamp when the progress occurred.                                       |

## Event Properties for Streak Milestone Achieved

The table below outlines the properties included in the Streak Milestone Achieved event.

| PROPERTY NAME             | DESCRIPTION                                                       |
| :------------------------ | :---------------------------------------------------------------- |
| livelike\_profile\_id     | The profile ID of the LiveLike user.                              |
| user\_streak\_id          | The unique ID of the user's streak instance.                      |
| streak\_id                | The unique ID of the streak.                                      |
| streak\_name              | The name of the streak.                                           |
| streak\_type              | The type of streak.                                               |
| milestone\_id             | The unique ID of the milestone.                                   |
| milestone\_streak\_length | The threshold streak length for this milestone (e.g., 7, 14, 30). |
| reward\_item\_ids         | Array of Reward Item IDs associated with this milestone.          |
| reward\_item\_names       | Array of Reward Item names.                                       |
| reward\_amounts           | Array of reward amounts.                                          |
| achieved\_at              | Timestamp when the milestone was achieved.                        |

## Event Properties for Streak Reset

The table below outlines the properties included in the Streak Reset event.

| PROPERTY NAME             | DESCRIPTION                                                        |
| :------------------------ | :----------------------------------------------------------------- |
| livelike\_profile\_id     | The profile ID of the LiveLike user.                               |
| user\_streak\_id          | The unique ID of the user's streak instance.                       |
| streak\_id                | The unique ID of the streak.                                       |
| streak\_name              | The name of the streak.                                            |
| streak\_type              | The type of streak.                                                |
| current\_streak\_length   | The current length/count of the user's streak when it was broken.  |
| last\_activity            | Timestamp of last activity before break.                           |
| milestones\_achieved      | Number of milestones achieved before break.                        |
| last\_milestone\_achieved | The last milestone threshold achieved before break (null if none). |
| reset\_at                 | Timestamp when broken.                                             |

<br />

## Client Side Integration

Before sending evens to Segment and make Livelike compatible to accept the data, you will need to send additional properties in the payload

Refer [LiveLike Cloud Mode (Actions) Destination](https://segment.com/docs/connections/destinations/catalog/actions-livelike-cloud/#track-event) for more details.