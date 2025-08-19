---
title: Getting Started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Getting Started | Producer Suite | LiveLike Developer Hub
  description: >-
    Get started with the LiveLike Engagement Suite by accessing our Producer
    Suite. Learn more about getting started with LiveLike.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: editorial-strategy
      title: Editorial strategy
---
## Accessing the Suite

You can access the Producer Suite at [producer.livelikecdn.com](https://cf-blast.livelikecdn.com/).

To get started, you will need account credentials. You can request these either from LiveLike, or from a member of your team that already has access (see [Inviting Your Team](inviting-organization-members)).

## Suite Layout

![2880](https://files.readme.io/d67e02d-Screen_Shot_2020-05-12_at_10.57.03_AM.png "Screen Shot 2020-05-12 at 10.57.03 AM.png")

The main components of the Producer Suite are:

* **Navigation Sidebar**: Access your programs and media library
* **Program Details**: Details for the currently selected program
* **Widget Console**: Dashboard for creating, scheduling and viewing history of widgets
* **Preview Panel**: Web preview of engagement interactions with end-users
* **Organization Settings**: Manage your app settings and invite others
* **Moderation Panel**: Monitor reported messages and take action like removing them

## Creating a Program

To publish widgets for an event, you will need to create a program associated with that event. You can access the **Event Management** window through the **Navigation Sidebar**. The video below shows how you can create your first program.

![1439](https://files.readme.io/cb3e684-Screen_Recording_2020-05-12_at_11.24_AM.gif "Screen Recording 2020-05-12 at 11.24 AM.gif")

Each event has the following fields:

* **Event Title**: An event name for your tracking purposes.
* **Scheduled Date & Time**: The start time of the event. This is for your tracking purposes and only determines the sort order & tab that the event appears on.
* **Video URL**: An optional video preview URL, which is required if you are looking to use [Spoiler Prevention](spoiler-free-sync). The stream must follow [these requirements](doc:stream-requirements).
* **Custom ID**: An optional custom identifier that you can use to query this particular event through our REST APIs. For example, this could be your internal match ID.

The Event Management Panel has 3 tabs. Note that these tabs are purely for organization and do not affect product functionality:

* **Live Now**: Displays all events that are currently live. To mark an event as "live", you will need to select "Start Event" as shown below.
* **Upcoming**: Displays all non-live events with a "scheduled date & time" in the future
* **History**: Displays all non-live events with a "scheduled date & time" in the past

<Image align="center" alt={1146} border={false} caption="Selecting &#x22;Start Event&#x22; will move the event to the &#x22;Live Now&#x22; tab" title="Screen Shot 2020-04-03 at 4.23.54 PM.png" src="https://files.readme.io/6047e76-Screen_Shot_2020-04-03_at_4.23.54_PM.png" width="smart" />

## Publishing Widgets

The Producer Suite allows you to publish a wide array of widgets. The video above shows how you can publish an Image Quiz, the rest are similar. Give them a shot!

![1439](https://files.readme.io/2002427-Screen_Recording_2020-05-12_at_11.31_AM.gif "Screen Recording 2020-05-12 at 11.31 AM.gif")

When creating widgets, you have 3 options:

1. **Queue**: Selecting the "Add to Queue" will adds the widget to a drafting board and it can be accessed later from the "Queue" tab.
2. **Schedule**: Selecting a time from the timepicker labelled "Now" will allow you to schedule a widget for a later time.
3. **Publish Now**:  Hitting "Post Now" without changing the time (default to "Now") will result in the widget being published immediately.

Note: Widgets in the Queue, Schedule and History tabs can be duplicated, thereby allowing you to post the same widget multiple times or quickly try variations on successful widgets.

## Chat Moderation

The **Preview Panel** also allows you to moderate chat content.

![2559](https://files.readme.io/293275b-Screenshot_2020-05-13_at_3.55.40_PM.png "Screenshot 2020-05-13 at 3.55.40 PM.png")

Select the "Moderation" tab, where you can see all messages reported by users and perform the following actions:

* Clear Report: The report is cleared from the system and the chat message is visible to all users
* Delete Message: <Glossary>Shadow-Mute</Glossary>s the message

## Personalised Chat Nickname

The **Preview Panel** allows you to view and update your Chat NickName. The video below shows how you can update your Chat NickName.

![640](https://files.readme.io/1b547dc-ChatNickName_1.gif "ChatNickName (1).gif")

Steps:

1. Click on "Change NickName"
2. Fill up the new NickName
3. Click "Update"

## Sticker Packs

Producers can access Sticker Packs available in the Application from the Sidebar

![2560](https://files.readme.io/c379ad1-Screenshot_2020-06-10_at_5.59.25_PM.png "Screenshot 2020-06-10 at 5.59.25 PM.png")

Producers can see the detail of any Sticker Pack by clicking on the Sticker Pack card

![2560](https://files.readme.io/41e47af-Screenshot_2020-06-10_at_6.09.42_PM.png "Screenshot 2020-06-10 at 6.09.42 PM.png")

In the Sticker Pack Detail - Producers can Add/Edit/Delete Stickers in the Pack

![2560](https://files.readme.io/ba65ca1-Screenshot_2020-06-10_at_6.11.50_PM.png "Screenshot 2020-06-10 at 6.11.50 PM.png")

Every Sticker has following fields:\
**Image** The image which will be seen in chat
**Shortcode** This is the code which represents a sticker in the chat

## Creating a Sticker Pack

Producers can create a new Sticker Pack from the Stickers screen

![2560](https://files.readme.io/dd4e00d-Screenshot_2020-06-10_at_6.04.23_PM.png "Screenshot 2020-06-10 at 6.04.23 PM.png")

Each Sticker Pack has following fields:\
**Pack Icon**
**Pack Name**

## Badges

A badge can be awarded or earned. To award a badge please use the award badge rest API.\
To set up a way to earn a badge, please follow the instructions below to setup badge automation rules.

The following items are required to be completed for a user to be able to earn a badge.

1. Create a **Reward Item**
   1. In the Producer Suite, on the left hand side click on **Rewards**.
   2. There are three tabs, make sure you are on the tab called **Items**
   3. On the top right hand side click on the button **New Reward Item**
   4. Fill in the name and click **Create**
2. Create a **Reward Action**
   1. In the Producer Suite, on the left hand side click on **Rewards**.
   2. There are three tabs, make sure you are on the tab called **Actions**
   3. On the top right hand side click on the button **New Reward Action**
   4. Fill in the details and click **Create**
3. Create a **Reward Table**
   1. In the Producer Suite, on the left hand side click on **Rewards**
   2. There are three tabs, make sure you are on the tab called **Tables**
   3. On the top right hand side click on the button **New Reward Table**
   4. Fill in the name, pick a program for it to be linked to and click **Create**
   5. Once a table is created, click on it's name in the list of all Reward Tables.
   6. You will see a screen showing all table entries. To add a new one, click on the **New Entry** button
   7. In the New Entry modal, you will be able to pick and connect a **Reward Action** with a **Reward Item** in addition you will be able to set up a **Reward Item Amount**, which is the amount that will be awarded to a user when this entry is earned.
   8. Click **Create** to create a reward table entry
4. Create a **Badge**
   1. In the Producer Suite, on the left hand side click on **Badges**.
   2. On the top right hand side, click on the button **New Badge**
   3. Fill in all the information and click **Create**
5. Connect the **Badge** with a **Reward Item**
   1. Find the **Badge** you created in the Badges list
   2. Click on the three vertical dots on the right hand side and click **Edit Badge**
   3. In this modal you will be able to create a connection between a Reward Item and a Badge. In addition you will be able to set the **Reward Item Threshold**, which is the amount of points a user is required to earn this badge.