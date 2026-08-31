---
title: iOS SDK 2.7 - Chat Input Control
author: Victor Matos
hidden: false
published_at: '2020-07-31T19:24:47.961Z'
---
In this iOS SDK release, developers now have the ability to control the visibility of the input text field for whitelisted chat experiences.

## Overview

We've added controls for controlling the input text-field in chat. This empowers developers to be able to create whitelisted chat experiences such as influencer chat, an experience where high-profile personalities can use our CMS to chat while other users can react to their comments. This is a chat experience that offers tons of visibility and interaction while also keeping moderation requirements low.

## 2.7.1 Release Notes

* Fixed a crash when a new message is being inserted into chat while closing chat
* Fixed a bug where progress bar not showing for prediction and prediction follow up widgets 

## 2.7.0 Release Notes

* Fixed a bug where sending messages on a Chat Session did not raise Chat Message Sent analytics event
* Added the ability to toggle the Chat Input View on ChatViewController
* Added the ability to add the message list view (MessageViewController) and the input view (ChatInputView) to a layout separately.