---
title: Livelike Analytics Dictionary
excerpt: 'Created by: Livelike Analytics Team'
deprecated: false
hidden: false
metadata:
  title: LiveLike Analytics Dictionary | Events Dictionary | LiveLike
  description: >-
    This is an overview about the content of the LiveLike Analytics Dashboard so
    that the users are aware of different KPIs.
  robots: index
next:
  description: ''
---
This document is built with an intention to provide an overview about the content of the LiveLike Analytics dashboard so that the users are aware of different KPIs which are being shown on the dashboard

## Applications Tab

1. Application - Name of the application
2. Organization - Name of the organization
3. New Profiles - These are profiles that used our Livelike SDK for the first time. They did not exist before the period set in the dashboard. These are based on Livelike UUID’s assigned to each of the users by LL SDK. 
4. Returning Profiles - These are the profiles which re-visited the Livelike SDK with the same UUID. These are the profiles that were registered on the backend. So, if these UUID’s use the LL SDK, then they are termed as return users.
5. Profiles - This column is created using the logic -\
   a. If unique impressions are greater than unique interactions, then profiles = unique impressions\
   b. If unique interactions are greater than unique impressions, then profiles = unique interactions

So, most of the time, we can say Profiles = Unique Impressions. If you are looking at this metric on a time frame of a month, then this is the MAUs (Monthly Active Users).

6. Unique Profiles Seen - This is the combination of New Profiles & Returning Profiles
7. Active PubNub profiles - These are the profiles which are connected to Pubnub.
8. Live Profiles - These are the profiles which are live i.e., which are connected to Pubnub. Essentially count of live profiles will always be equal to Active Pubnub Profiles.
9. Non-Live Profiles - These are the profiles which are not connected to Pubnub.
10. Impressions - These are the devices/users where a widget has been published. Below are the definitions that are being used in the dashboard -\
    a. Unique Impression - Unique devices/users who have received the widgets on their device\
    b. Total Impression - Total devices/users who have received the widgets on their device. The only difference between unique and total is that in unique impression we will be counting a device/user only once throughout the whole time which they have been active, irrespective if they got disconnected from a program at any point in the program
11. Interactions - These are the devices/users where a widget has been interacted. Below are the definitions that are being used in the dashboard -\
    a. Unique Interaction - Unique devices/users who have interacted with the widgets received on their device\
    b. Total Interaction - Total devices/users who have interacted with the widgets received on their device. The only difference between unique and total is that in unique interaction we will be counting a device/user only once throughout the whole time which they have been active, irrespective if they got disconnected from a program at any point in the program
12. Engagement - This is calculated by the logic - Interaction/Impression

## Programs Tab

1. Program - Name of the program
2. Application - Name of the application
3. Organization - Name of the organization

Apart from the above KPI’s we have already defined in the Application’s page

## Widgets Tab

1. Widget Kind - Type of widget published
2. Widget - Title of the widget
3. Widget Published - Timestamp at which a widget is published

Apart from the above KPI’s we have already defined in the Application’s & Program page

## Chat Rooms Tab

1. Chat Room - Name of the chat room
2. Total Profiles - Total profiles which were registered on a particular chat group
3. Unique Interactive Profiles - Unique profiles who interacted in the chat
4. Messages - Total number of messages sent in a chat group
5. Reactions - Total number of reactions given in a particular chat group
6. Unique Profile Messages - Unique profiles that have sent at least 1 message
7. Unique Profile Reactions - Unique profiles that have reacted to at least 1 chat message

## Quests Tab

1. Quest - Name of the quest
2. Quest Completion - Indicates completion status of quest
3. Active Audience - Indicates active users of quest
4. Tasks - Total number of quest tasks

## Quest Tasks Tab

1. Quest Task - Name of the quest task
2. Task Completion - Indications how much percent the task has been completed
3. Target - How many times this task should be done before its marked as completed

## Audience Tab

Audience - This view allows you to get an overview of the customers. In this view, you will be able to see which operating system the use, the types of devices, and the SDK versions

> 👍 Cool Features of Livelike Analytics Dashboard
>
> To be more flexible we have provided users two additional options use and share the dashboard - 
>
> 1. **Data Download** - In this dashboard there is a download option where users can download data in CSV format in their local system and derive analysis on their own
> 2. **Share Link** - One of the cool features of this dashboard is that you can share the link of a view with all the applied filters with your team members so that they can see the same view at their end. This saves time and effort when they are doing similar analysis or validation
> 3. **Search Bar** - People can search their desired data using various filters like Application ID, Program ID, Chat Room ID etc which might be beneficial to those organization which has a lot of data on the dashboard
> 4. **Navigation of inline data stored in CMS Producer Suite** - We have connected CMS links within Analytics dashboard so that people can navigate to respective Organization, Application, Programs and other different pages
