---
title: Leaderboards
deprecated: false
hidden: false
metadata:
  robots: index
---
Leaderboards let users compete and see how they rank against others. Once a leaderboard is linked to a <Glossary>Program</Glossary>, any rewards earned in that program automatically count toward the leaderboard score.
A program can be linked to multiple leaderboards, and a leaderboard can track multiple programs. This flexibility lets you model experiences like all-time, seasonal, or single-event leaderboards—or even mix and match across the same program.

## Leaderboard Basics

Each leaderboard includes:

* ID: The unique identifier of the leaderboard (cannot be changed).
* Name: A human-readable name.
* Tracked Reward Item: The reward type that contributes to scores.
* Linked Programs: Programs where tracked rewards are counted.
* Entries: An ordered list of ranked profiles, each with:
  * Profile details
  * Current rank
  * Current score

<br />

## Entries and Scoring

* Entries are ordered high to low by score (rank 1 = highest score).
* Scores increase automatically whenever a profile earns the tracked reward in a linked program.
* Scores do not decrease when users spend, transfer, or deplete their reward balances.

> 📘 Important
>
> Rewards only affect scores when both conditions are met:
> The program is linked to the leaderboard.
> The reward matches the type tracked by the leaderboard.

<br />

## Setting Up Leaderboards in the CMS

Before creating a leaderboard, configure a Reward Item.

1. Go to your Application in the Producer Site.
2. Select Leaderboards in the sidebar.
3. Click New Leaderboard.
4. Enter the leaderboard name, tracked Reward Item, and associated Program(s).
5. Click Create.

The leaderboard is now live and tracking progress.

## SDK Usage

Below are common operations with code examples in Swift, JavaScript, Kotlin, and Flutter.

### Getting leaderboards associated with a program

You have the option to retrieve all leaderboards associated to a program by using the code samples below. This function will return an array of leaderboards.

<details>
  <summary>Get Leaderboards for a Program</summary>

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
  ```text Flutter
  final List<LeaderBoard> list = await sdk.getLeaderBoards(<program-id>);
  ```
</details>

<br />

### Getting leaderboard details

If you know a leaderboard id, you are able to get its details by using the code samples below. This can be useful if you would like to know the name of the leaderboard or the type of reward a user can earn.

<details>
  <summary>Get Leaderboard Details</summary>

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
  ```text Flutter
  final LeaderBoard detail=await sdk.getLeaderBoardDetails(<leaderBoardId>);
  ```
</details>

<br />

### Getting leaderboard entries

A user that competes is considered a leaderboard entry. Use the code samples below to retrieve leaderboard entries for a specific leaderboard. Due to the nature of leaderboard entries growing to a very high number, this call is paginated with each page returning 20 leaderboard entries.

<details>
  <summary>Get Leaderboard Entries</summary>

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
  ```text Flutter
  final List<LeaderBoardEntry> result = await sdk.getEntriesForLeaderBoard(
          <leaderboard-id>, <LiveLikePagination>);
  ```
</details>

<br />

## Getting leaderboard entry for a given profile

Details about a leaderboard entry can be retrieved by providing a profile id and a leaderboard id. This can be useful if there is a leaderboard entry you are interested in keeping track of.

<details>
  <summary>Get a Profile’s Entry</summary>

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
  ```text Flutter
  final LeaderBoardEntry result = await sdk.getLeaderBoardEntryForProfile(
          <leaderboard-id>, <profile-id>);
  ```
</details>

<br />

## Getting a leaderboard entry for the current user profile

Retrieving details about the current user's profile can be done using the code samples below. This can be used to look up the current user's ranking in a specific leaderboard.

<details>
  <summary>Get Current User’s Entry</summary>

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
  ```text Flutter
  final LeaderBoardEntry result = await sdk.getLeaderBoardEntryForCurrentUserProfile(<leaderboard-id>);
  ```
</details>

<br />

## Subscribe to the Current User's Leaderboard Position

You can subscribe to the current user's Leaderboard position to receive updates when their position changes.

> 📘 Minimum SDK Version
>
> iOS: 2.9
> Android:
> Web: 2.0.0

#### Get LeaderboardClients from Content Session

<details>
  <summary>Get LeaderboardClients from Content Session</summary>

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
</details>

<br />
