---
title: Leaderboards
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: JavaScript Leaderboards | LiveLike Developer Hub | JavaScript SDK
  description: >-
    Leaderboards allow users to compete and see how they stack up against each
    other. Learn more about configuring leaderboards on JavaScript.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: rewards
      title: Rewards
---
## Overview

Leaderboards allow users to compete and see how they stack up against each other. Once a leaderboard has been associated with a <Glossary>Program</Glossary>, users who earn [rewards](https://docs.livelike.com/docs/rewards) in that program will have them counted toward their score on that leaderboard.

A program can have many leaderboards associated, and a leaderboard can be linked with many programs. This allows you to better capture your own experience's structure, such as allowing all-time, seasonal, or single-event leaderboards. You can even mix and match multiple leaderboards with the same program.

## Leaderboard Basics

Each leaderboard has these properties:

* An **ID** containing the unique identifier of the leaderboard. This can't be changed.
* A human-readable **Name**.
* A **Tracked Reward Item**. When fans earn these rewards in linked programs their scores in the leaderboard automatically update.
* A set of **Linked Programs** that determine which programs are eligible to automatically update the leaderboard.
* An ordered list of **Entries**, one for each profile ranked on the leaderboard. Each entry contains the profile, their rank on the leaderboard, and their score.

## Entries and Score

Each leaderboard maintains a list of entries ordered by rank for each profile ranked on the leaderboard. Entries are ranked high to low by score, where the profile with the highest score has rank 1. In addition to the rank, each entry also has fields for the profile and for their current score on the leaderboard. Score increases each time a profile gains the same kind of reward that the leaderboard is tracking, and only while the program the profile earned the rewards in is linked to the leaderboard. When using automatically-updating leaderboards that track rewards, score only accumulates, it does not go down when the profile spends, transfers, or otherwise depletes their reward balances.

> 📘 Scores only update when the program is linked to the leaderboard
>
> Rewards earned in a program will only increase score when the program is linked to the leaderboard, and when the rewards earned are the same kind being tracked by the leaderboard.

## Setting Up Leaderboards in the CMS

To get started you need to first configure a [Reward Item](https://docs.livelike.com/docs/rewards#configuring-reward-items).

When you've configured a Reward Item you can:

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Leaderboards" in the Sidebar
3. Select the "New Leaderboard" button
4. Set the Leaderboard name, Reward Item, and the associated Program(s).
5. Select "Create" to finish

Now, the Leaderboard will be tracking user's progress!

## Getting leaderboards associated with a program

You have the option to retrieve all leaderboards associated to a program by using the code samples below. This function will return an array of leaderboards.

```swift
class HelloWorld {
  let sdk: EngagementSDK
  
  sdk.getLeaderboards(programID: "<program id>") { result in
  	 switch result {
       case let .success(leaderboards):
       	//do something with leaderboards
       case let .failure(error):
       	print(error)
     }
  }
}
```
```javascript JavaScript
LiveLike.getLeaderboards({programId: "<program id>"})
	.then(leaderboards => console.log(leaderboards));
```
```kotlin
sdk.leaderboard().getLeaderBoardsForProgram(
                    "<program id>"
                ) { result, error ->
                    result?.let {
                      //handle result
                    }
                    error?.let {
                        //handle error
                    }
                }
```
```text Dart
final List<LeaderBoard> list = await sdk.getLeaderBoards(<program-id>);
```

## Getting leaderboard details

If you know a leaderboard id, you are able to get its details by using the code samples below. This can be useful if you would like to know the name of the leaderboard or the type of reward a user can earn.

```swift
class HelloWorld {
  let sdk: EngagementSDK
  
  sdk.getLeaderboard(leaderboardID: "<leaderboard id>") { result in
  	 switch result {
       case let .success(leaderboard):
       	//do something with a leaderboard
       case let .failure(error):
       	print(error)
     }
  }
}
```
```javascript JavaScript
LiveLike.getLeaderboard({leaderboardId: "<leaderboard id>"})
	.then(leaderboard => console.log(leaderboard));
```
```kotlin
sdk.getLeaderBoardDetails("<leaderboard id>",
                        object : LiveLikeCallback<LeaderBoard>() {
                            override fun onResponse(result: LeaderBoard?, error: String?) {
                                result?.let {}
                            error?.let {
                                showToast(error)
                            }
                            }

                        })
```
```text Dart
final LeaderBoard detail=await sdk.getLeaderBoardDetails(<leaderBoardId>);
```

## Getting leaderboard entries

A user that competes is considered a leaderboard entry. Use the code samples below to retrieve leaderboard entries for a specific leaderboard. Due to the nature of leaderboard entries growing to a very high number, this call is paginated with each page returning 20 leaderboard entries.

```swift
class HelloWorld {
  let sdk: EngagementSDK
  
  sdk.getLeaderboardEntries(leaderboardID: "<leaderboard id>", page: .first) { result in
  	 switch result {
       case let .success(leaderboardEntries):
       	//do something with leaderboardEntries
       if leaderboardEntries.hasNext == false {
         // you have reached the last leaderboard entry page
       }
       case let .failure(error):
       	print(error)
     }
  }
  
  // ** Available in iOS SDK 2.48+ **
  // Get leaderboard entries filtered by profile IDs
  let requestOptions = GetLeaderboardEntriesRequestOptions(
    leaderboardID: "<leaderboard ID>",
    profileIDs: ["<profile ID 1>", "<profile ID 2"]
  )
  sdk.getLeaderboardEntries(
 	  page: .first,
      options: requestOptions
  ) { result in
        
    switch result {
    case let .success(leaderboardEntries):
        // handle success 
    case let .failure(error):
        // handle failu
    }
  }
}
```
```javascript JavaScript
LiveLike.getLeaderboardEntries({
  leaderboardId: "<leaderboard id>",
  profileIds: ["<profileId1>","<profileId2>"]
})
.then(leaderboardEntries => console.log(leaderboardEntries));
```
```kotlin
sdk.leaderboard().getEntriesForLeaderBoard(
                leaderBoardId!!, pagination
            ) { result, error ->
                result?.let {
                    //handle result
                }
              
                error?.let {
                   //handle error
                }
            }
```
```text Dart
final List<LeaderBoardEntry> result = await sdk.getEntriesForLeaderBoard(
        <leaderboard-id>, <LiveLikePagination>);
```

## Getting leaderboard entry for a given profile

Details about a leaderboard entry can be retrieved by providing a profile id and a leaderboard id. This can be useful if there is a leaderboard entry you are interested in keeping track of.

```swift
class HelloWorld {
  let sdk: EngagementSDK
 
  sdk.getLeaderboardEntry(profileID: "<profile id>", leaderboardID: "<leaderboard id>") { result in
  	 switch result {
       case let .success(entry):
       	//do something with a leaderboard entry
       case let .failure(error):
       	print(error)
     }
  }
}
```
```javascript JavaScript
LiveLike.getLeaderboardProfileRank({leaderboardId:"<leaderboard id>", profileId:"<profile id>"})
	.then(profileRank => console.log(profileRank));
```
```kotlin
sdk.leaderboard().getLeaderBoardEntryForProfile(
    "<leaderboard ID>",
    "<profile id>"
) { result, error ->  
    result?.let {  
        // Handle result  
    }  

    error?.let {  
        // Handle error  
    }  
}
```
```text Dart
final LeaderBoardEntry result = await sdk.getLeaderBoardEntryForProfile(
        <leaderboard-id>, <profile-id>);
```

## Getting a leaderboard entry for the current user profile

Retrieving details about the current user's profile can be done using the code samples below. This can be used to look up the current user's ranking in a specific leaderboard.

```swift
class HelloWorld {
  let sdk: EngagementSDK

  sdk.getLeaderboardEntryForCurrentProfile(leaderboardID: "<leaderboard id>") { result in
  	 switch result {
       case let .success(entry):
       	//do something with a leaderboard entry
       case let .failure(error):
       	print(error)
     }
  }
}
```
```javascript JavaScript
LiveLike.init({ clientId }).then(profile => {
	LiveLike.getLeaderboardProfileRank({leaderboardId: "<leaderboard id>", profileId: profile.id})
  	.then(profileRank => console.log(profileRank))
});

// or
LiveLike.getLeaderboardProfileRank({leaderboardId: "<leaderboard id>", profileId: LiveLike.userProfile.id})
	.then(profileRank => console.log(profileRank))
```
```kotlin
sdk.leaderboard().getLeaderBoardEntryForCurrentUserProfile("<leaderboardID>") { result, error-> 
                        result?.let {
                           
                        }
                        error?.let {
                           
                        }
                    }
```
```text Dart
final LeaderBoardEntry result = await sdk.getLeaderBoardEntryForCurrentUserProfile(<leaderboard-id>);
```

## Subscribe to the Current User's Leaderboard Position

You can subscribe to the current user's Leaderboard position to receive updates when their position changes.

> 📘 Minimum SDK Version
>
> iOS: 2.9
> Android:
> Web: 2.0.0

#### Get LeaderboardClients from Content Session

```swift
class MyViewController: UIViewController {
  let session: ContentSession
  var leaderboards: [LeaderboardClients]?
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    session.getLeaderboardClients { result in
      switch result {
      case .success(let leaderboards):
        self.leaderboards = leaderboards
        leaderboards.forEach { leaderboard in
          leaderboard.delegate = self
        }
      case .failure(let error):
      	// handle error
      }
    }
  }
}

extension MyViewController: LeaderboardDelegate {
  func leaderboard(_ leaderboardClient: LeaderboardClient, currentPositionDidChange position: LeaderboardPosition) {
    // Do something (ie. update ui)
  }
}
```
```javascript
const widgetContainer = document.querySelector('livelike-widgets');
widgetContainer.addEventListener('rankchange', e => console.log(e.detail));
```
```kotlin
session?.getLeaderboardClients(leaderboardIDs, object : LiveLikeCallback<LeaderboardClient>(){
                                    override fun onResponse(result: LeaderboardClient?, error: String?) {
                                       // result received, do something
                                    }
                                })
```

#### Get LeaderboardClient with Leaderboard ID

```swift
class MyViewController: UIViewController {
  let sdk: EngagementSDK
  var leaderboards: [LeaderboardClients]?  
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    sdk.getLeaderboardClients(leaderboardIDs: ["my-leaderboard"]) { result in
      switch result {
      case .success(let leaderboards):
        self.leaderboards = leaderboards
        leaderboards.forEach { leaderboard in
          leaderboard.delegate = self
        }
      case .failure(let error):
      	// handle error
      }
    }
  }
}

extension MyViewController: LeaderboardDelegate {
  func leaderboard(_ leaderboardClient: LeaderboardClient, currentPositionDidChange position: LeaderboardPosition) {
    // Do something (ie. update ui)
  }
}
```

## Getting the total count of leaderboard entries

Integrators can fetch the total count of leaderboard entries to contextualize the user’s own rank.

```swift
let sdk: EngagementSDK

sdk.getLeaderboardEntries(leaderboardID: "<leaderboard id>", page: .first) { result in
     switch result {
     case let .success(leaderboardEntries):
         self.sdk.getLeaderboardEntryForCurrentProfile(leaderboardID: "<leaderboard id>") { result in
             switch result {
             case let .success(entry):
                 print("You placed \(entry.rank) out of \(leaderboardEntries.total)")
             case let .failure(error):
                 print(error)
             }
         }
     case let .failure(error):
         print(error)
     }
}
```
```javascript
LiveLike.getLeaderboardEntries({leaderboardId: "<leaderboard id>"})
  .then(leaderboard => {
    LiveLike.getLeaderboardProfileRank(
      {
        leaderboardId: "<leaderboard id>", 
        profileId: LiveLike.userProfile.id
      })
      .then(entry => console.log(`You are placed ${entry.rank} out of ${leaderboard.count}`))
      .catch(err => console.log(err))
  });
  .catch(err => console.log(err));
```
```kotlin
lateinit var sdk: EngagementSDK
 sdk.leaderboard().getEntriesForLeaderBoard(
                leaderBoardId!!, pagination
            ) { result, error ->
                result?.let {
                  Log.d(result)
                }
       
                error?.let {
                 Log.d(error)
                }
            }

```

## Get Leaderboards a given profile is ranked on

Integrators can fetch the leaderboards a given profile is ranked on.

```swift
let sdk: EngagementSDK

sdk.getProfileLeaderboards(profileID: "<Profile ID>", page: .first) { result in
	switch result {
  case .success(let leaderboardEntries):
  	self.entries.append(contentsOf: leaderboardEntries.entries)
	case .failure(let error):
  	print(error)
	}
}
```
```javascript
// leaderboard for current profile
LiveLike.getProfileLeaderboards()
.then(leaderboards => console.log(leaderboards))
 
// leaderboard for a given profileId
LiveLike.getProfileLeaderboards({profileId: "<profile-id>"})
.then(leaderboards => console.log(leaderboards))
```
```kotlin
var sdk: EngagementSDK
  sdk.leaderboard().getProfileLeaderboards("<profile_id>", LiveLikePagination.FIRST,
            object: LiveLikeCallback<LLPaginatedResult<LeaderBoardEntry>>(){
                override fun onResponse(
                    result: LLPaginatedResult<LeaderBoardEntry>?,
                    error: String?
                ) {
                    Log.d(result)
                }

            })
  
  //from SDK 2.79 onwards
  sdk.leaderboard().getProfileLeaderboards("<profile_id>", LiveLikePagination.FIRST,
            object: LiveLikeCallback<List<LeaderBoardEntry>>(){
                override fun onResponse(
                    result: List<LeaderBoardEntry>?,
                    error: String?
                ) {
                    Log.d(result)
                }

            })
```

## Get Leaderboard views a given profile is part of

Integrators can fetch the leaderboard views a given profile is part of

```swift
let sdk: EngagementSDK

sdk.getProfileLeaderboardViews(profileID: "<Profile ID>", page: .first) { result in
	switch result {
		case .success(let leaderboardViews):
			self.views.append(contentsOf: leaderboardViews.entries)
		case .failure(let error):
			print(error)
	}
}
```
```javascript
// leaderboard views for current profile
LiveLike.getProfileLeaderboardViews()
.then(leaderboardviews => console.log(leaderboardviews))
 
// leaderboard views for a given profileId
LiveLike.getProfileLeaderboardViews({profileId: "<profile-id>"})
.then(leaderboardviews => console.log(leaderboardviews))
```
```kotlin
var sdk: EngagementSDK
  val profileIds: Array<String> = arrayOf("<id1>", "<id2>")
    sdk.leaderboard().getProfileLeaderboardViews(
                profileIds.trim(), LiveLikePagination.FIRST
            ) { result, error ->
                Log.d(result)
            }
  
 
```

<br />

## Get Leaderboard By Custom ID

Integrators can fetch the leaderboard via Custom ID

```kotlin
// Available for SDK version 2.98.9 onwards
  var sdk: EngagementSDK
  sdk.leaderboard().getLeaderBoardDetailsByCustomId("<custom_id>") { result, error ->
                        result?.let {
                          Log.d(result)
                        }
                        error?.let {
                            Log.d(error)
                        }
                    }
```
