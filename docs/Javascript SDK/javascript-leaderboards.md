---
title: Leaderboards
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: JavaScript Leaderboards | LiveLike Developer Hub | JavaScript SDK
  description: >-
    JavaScript leaderboards allow users to compete and see how they stack up
    against each other. Learn more about configuring JavaScript leaderboards.
  robots: index
next:
  description: ''
---
> 📘 What are Leaderboards? How to setup a leaderboard?
>
> Refer our core [leaderboards](leaderboards) documentation.

## Getting leaderboards associated with a program

You have the option to retrieve all leaderboards associated to a program by using the code samples below. This function will return an array of leaderboards.

**API Definition:** [getLeaderboards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboards)

```javascript JavaScript
import { getLeaderboards } from "@livelike/javascript"

getLeaderboards({
  programId: "<program id>"
}).then(leaderboards => console.log(leaderboards));
```

## Getting leaderboard details

If you know a leaderboard id, you are able to get its details by using the code samples below. This can be useful if you would like to know the name of the leaderboard or the type of reward a user can earn.

**API Definition:** [getLeaderboard](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboard)

```javascript JavaScript
import { getLeaderboard } from "@livelike/javascript"

getLeaderboard({leaderboardId: "<leaderboard id>"})
	.then(leaderboard => console.log(leaderboard));
```

## Getting leaderboard entries

A user that competes is considered a leaderboard entry. Use the code samples below to retrieve leaderboard entries for a specific leaderboard. Due to the nature of leaderboard entries growing to a very high number, this call is paginated with each page returning 20 leaderboard entries.

**API Definition:** [getLeaderboardEntries](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboardEntries) 

```javascript JavaScript
import { getLeaderboardEntries } from "@livelike/javascript"

getLeaderboardEntries({
  leaderboardId: "<leaderboard id>",
  profileIds: ["<profileId1>","<profileId2>"]
}).then(leaderboardEntries => console.log(leaderboardEntries));
```

## Getting leaderboard entry for a given profile

Details about a leaderboard entry can be retrieved by providing a profile id and a leaderboard id. This can be useful if there is a leaderboard entry you are interested in keeping track of.

 **API Definition:** [getLeaderboardProfileRank](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboardProfileRank)

```javascript JavaScript
import { getLeaderboardProfileRank } from "@livelike/javascript"

getLeaderboardProfileRank({
  leaderboardId: "<leaderboard id>",
  profileId: "<profile id>"
}).then(profileRank => console.log(profileRank));
```

## Getting a leaderboard entry for the current user profile

Retrieving details about the current user's profile can be done using the code samples below. This can be used to look up the current user's ranking in a specific leaderboard.

 **API Definition:** [getLeaderboardProfileRank](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboardProfileRank)

```javascript JavaScript
import { getLeaderboardProfileRank, userProfile } from "@livelike/javascript"

getLeaderboardProfileRank({
  leaderboardId: "<leaderboard id>",
  profileId: userProfile.id
}).then(profileRank => console.log(profileRank));
```

## Get Leaderboards a given profile is ranked on

Integrators can fetch the leaderboards a given profile is ranked on.

 **API Definition:** [getProfileLeaderboards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileLeaderboards)

```javascript
import { getProfileLeaderboards } from "@livelike/javascript"

// leaderboard list for current profile
getProfileLeaderboards()
.then(leaderboards => console.log(leaderboards))
 
// leaderboard list for a given profileId
getProfileLeaderboards({
  profileId: "<profile-id>"
}).then(leaderboards => console.log(leaderboards))
```

## Get Leaderboard views for a given profile

Integrators can fetch the leaderboard views for a given profile.

 **API Definition:** [getProfileLeaderboardViews](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileLeaderboardViews)

```javascript
import { getProfileLeaderboardViews } from "@livelike/javascript"

// leaderboard views for current profile
getProfileLeaderboardViews()
.then(leaderboardviews => console.log(leaderboardviews))
 
// leaderboard views for a given profileId
getProfileLeaderboardViews({
  profileId: "<profile-id>"
}).then(leaderboardviews => console.log(leaderboardviews))
```
