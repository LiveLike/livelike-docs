---
title: Web SDK 1.25 - Chat Analytics & Chat Input Controls
author: Victor Matos
hidden: false
published_at: '2020-07-31T19:21:34.746Z'
---
In this Web SDK release, we added support for Sticker and Chat analytics for MixPanel and added controls for the input field to allow experiences such as Influencer Chat.

## Overview

We added support for Sticker and Chat analytics for MixPanel. We can now provide clients, a MixPanel report with a breakdown of different stats and metrics for Stickers and Chats. 

In additional to Mixpanel Analytics, we've added controls for controlling the input textfield in chat. This empowers developers to be able to create whitelisted chat experiences such as influencer chat.

## 1.25.1 Hotfix Notes

* Fixed an issue with chat room not loading properly with roomid attribute. 

## 1.25.0 Release Notes

* Added mixpanel tracking for user profile creation, message/sticker sending and receiving.
* Added `hidecomposer` attribute to livelike-chat element to show or hide composer.
* Added `composer`, `body`, `send` slot to composer to enable composer customization.