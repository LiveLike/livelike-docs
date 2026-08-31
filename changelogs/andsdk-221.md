---
title: ANDSDK 2.21
author: Shivam Verma
hidden: false
published_at: '2021-08-09T10:34:15.273Z'
---
## What's New

* Added enableChatMessageURLs in the ChatView to enable web URL links in the chat.
* Added chatMessageUrlPatterns in the ChatView to allow custom Regex to allow specific links
* Added analytics for clicking on the link in the chat
* Added API in the Content Session to provide User Interaction Data for a particular widget
* Update displayWidget method to fetch widget interaction data when displaying the widget with user interaction data
* Bug Fix for maintaining the state of ChatView on orientation change