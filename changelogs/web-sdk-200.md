---
title: Web SDK 2.0.0 - Widget UI Customisation
author: tanya gupta
hidden: false
published_at: '2020-11-20T17:05:44.812Z'
---
## 2.0.0 Release Notes

## Additions

* Added Widget Customization support
* Added ability to render single widget on page outside of `<livelike-widgets>` element
* Added `rankchange` event
* Added pagination to getLeaderboardEntries and getPostedWidgets methods.

## Fixes

* Fixed bug in Load More widgets not going through widget lifecycle
* Fixed cheer meter 0 vote not reflecting bug
* Fixed emoji slider not displaying correct average
* Fixed default message input creating a newline

## Breaking Changes

* *programid* attribute is nor more supported in livelike-chat element
* *fetchUserProfile* method has been renamed to *getUserProfile*
* deprecated method *getProfile* has been removed