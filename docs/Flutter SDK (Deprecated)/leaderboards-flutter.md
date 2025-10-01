---
title: Leaderboards
excerpt: Leaderboard API's for handling leaderboard data
deprecated: false
hidden: false
metadata:
  title: Leaderboards | REST API | LiveLike Developer Hub
  description: >-
    Leaderboards allow users to compete and see how they stack up against each
    other. Learn more about configuring REST API leaderboards.
  robots: index
next:
  description: ''
---
## Getting Leaderboard associated with a Program

You have the option to retrieve all leaderboards associated with a program by using the code samples below. This function will return an array of leaderboards.

```text
final List<LeaderBoard> list = await sdk.getLeaderBoards(<program-id>);
```

## Getting leaderboard details

If you know a leaderboard id, you are able to get its details by using the code samples below. This can be useful if you would like to know the name of the leaderboard or the type of reward a user can earn.

```text
final LeaderBoard detail=await sdk.getLeaderBoardDetails(<leaderBoardId>);
```

## Getting leaderboard entries

A user that competes is considered a leaderboard entry. Use the code samples below to retrieve leaderboard entries for a specific leaderboard. Due to the nature of leaderboard entries growing to a very high number, this call is paginated with each page returning 20 leaderboard entries. 

```text
final List<LeaderBoardEntry> result = await sdk.getEntriesForLeaderBoard(
        <leaderboard-id>, <LiveLikePagination>);
```

## Getting leaderboard entry for a given profile

Details about a leaderboard entry can be retrieved by providing a profile id and a leaderboard id. This can be useful if there is a leaderboard entry you are interested in keeping track of. 

```text
final LeaderBoardEntry result = await sdk.getLeaderBoardEntryForProfile(
        <leaderboard-id>, <profile-id>);
```

## Getting a leaderboard entry for the current user profile

Retrieving details about the current user's profile can be done using the code samples below. This can be used to look up the current user's ranking in a specific leaderboard.

```text
final LeaderBoardEntry result = await sdk.getLeaderBoardEntryForCurrentUserProfile(<leaderboard-id>);
```