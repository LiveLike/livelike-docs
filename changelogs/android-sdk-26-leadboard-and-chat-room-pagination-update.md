---
title: Android SDK 2.6 - Leaderboard and Chat Room Pagination Update
author: shivansh mittal
hidden: false
published_at: '2020-08-06T15:11:55.281Z'
---
In this Android SDK release we have added the following functionalities:

* **Chat Room Visibility** - When creating a chat room, you will now be able to control its visibility (everyone or member)
* **Leaderboards** - Working with gamification has become much easier as we have added various ways an SDK can provide information about leaderboards and its entries.
* **ChatRoom Pagination** - We have updated our SDK for handling the chatRoom Api with pagination,\
  so for the initial, the user has to use FIRST for fetching the data first time and then use NEXT for getting next data and PREVIOUS for getting previous data, in case if there is not next data to load then we provide a null result with the message "No more data to load" in the error of the callback.

## 2.6 Release Notes

* Added getLeaderBoardsForProgram
* Added getLeaderBoardDetails
* Added getEntriesForLeaderBoard
* Added getLeaderBoardEntryForProfile
* Added getLeaderBoardEntryForCurrentUserProfile
* Updated getMembersOfChatRoom
* Updated getCurrentUserChatRoomList
* Updated updateChatRoom
* Updated createChatRoom
* Update ChatRoomMembershipPagination changed to LiveLikePagination for common usage.