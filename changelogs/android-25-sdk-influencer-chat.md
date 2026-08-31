---
title: Android SDK 2.5 - Chat Input Control
author: Victor Matos
hidden: false
published_at: '2020-07-31T17:36:17.746Z'
---
In this Android SDK release, developers now have the ability to control the visibility of the input text field for whitelisted chat experiences.

## Overview

We've added controls for controlling the input text-field in chat. This empowers developers to be able to create whitelisted chat experiences such as influencer chat, an experience where high-profile personalities can use our CMS to chat while other users can react to their comments. This is a chat experience that offers tons of visibility and interaction while also keeping moderation requirements low.

## 2.5.2 Hotfix Notes

* Fixed an issue where the setEventObserver wasn't getting any callbacks with regards to "Chat Message", "Widget Dismissed", and "Widget Displayed"

## 2.5.1 Hotfix Notes

* Fixed an issue where the setEventObserver wasn't getting any callbacks with regards to Keyboard Selected event

## 2.5.0 Release Notes

* Added the ability to toggle Chat Input View on ChatView 
* Fixed an issue where the user is unable to update the nickname for the user profile 
* Fixed a crash that can happen when a user sends a GIF under a certain scenario
* Fixed an issue where the reaction panel would not open when tapping over the chat message