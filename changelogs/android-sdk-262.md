---
title: Android SDK 2.62
author: Shivam Verma
hidden: false
published_at: '2022-12-02T11:34:19.849Z'
---
## What's New

* Added `getBadgeProfiles` API to fetch the list of profiles by given badge id
* Added `getProgramByCustomID` API in Engagement SDK to fetch the list of programs associated with\
   CustomId
* Added `enableDeleteMessage` to enable/disable the delete feature in Chat
* Added a new API to provide a custom interceptor for deleting requests in Chat.

## Bug Fix

* Updated UpdateCustomData API to work without waiting for Engagement SDK init.
* Updated code for ChatInputVisible boolean behavior in ChatView