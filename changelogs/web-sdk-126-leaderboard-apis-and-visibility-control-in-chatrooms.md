---
title: Web SDK 1.26 - Leaderboard APIs and Visibility control in Chatrooms
author: tanya gupta
hidden: false
published_at: '2020-08-05T15:58:42.059Z'
---
In this Web SDK release, we added Leaderboard APIs and added visibility control while creating and updating Chatrooms.

## Overview

We added Leaderboard APIs. Integrators can use these APIs to display leaderboards

In additional to Leaderboard APIs, we've added visibility control while creating and updating Chatrooms. This empowers integrators to be able to control who all should be able to access the chatrooms that are being created - everyone or just members of that room.

## 1.26.1 Release Notes

* Fixed an issue where a chat message can be duplicated when loading from a different browser.

## 1.26.0 Release Notes

* Added getLeaderboards method
* Added getLeaderboard method
* Added getLeaderboardEntries method
* Added getLeaderboardProfileRank method 
* Added visibility parameter while creating and updating chatRooms
* Fixed issue of GIFs sent from Web SDK not being received by iOS