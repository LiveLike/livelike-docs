---
title: 'Complete Quests Guide: CMS + SDK'
excerpt: >-
  Quests allow users to complete multi-step challenges to earn one-time rewards.
  This guide explains how to create, manage, and track quests in the CMS and via
  SDK, including Save as Draft and A/B Testing features.
deprecated: false
hidden: true
metadata:
  robots: index
---
# What are Quests?

A Quest is a set of tasks a user must complete to achieve a goal.
Quest Tasks: Individual tasks within a quest.
Tasks can be completed in any order, but progress toward the overall Quest goal is tracked.

### Why use quests?

Quests give the end user a more gamified experience. They have to do multiple things in order to accomplish a single goal. During the quests, the user and integrators are able to see the progress of the quest. This progress allows the user to see how much is left in order for them to complete the quest.

Quests can be used to build things like:

* New user on-boarding checklists
* Product and feature tours
* One-time promotional campaigns

### Creating Quests in CMS  - [How to create a Quest in CMS](https://docs.livelike.com/docs/how-to-create-a-quest-in-cms#/)

## Save Quests as Drafts

#### Feature Context:


You can save your quest as a draft before publishing to prevent unfinished quests from being visible to users and to allow iterative creation.

#### How to Save as Draft

Create a quest as above. [LINK](https://docs.livelike.com/docs/how-to-create-a-quest-in-cms#/)

#### Click Quit, then choose:

* **Save and Quit** – to save progress as a draft.
* Exit Without Saving – to discard changes.

<Image align="left" border={false} src="https://files.readme.io/7d7e6c38c4ef318b87b5d4bdd899a16e8e140a603ec81206001560b47f5153a5-Screenshot_2025-10-24_at_2.46.14_PM.png" />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

> Drafts can be reopened later for editing and publishing.

<br />

## A/B Testing Using Quests

#### Feature Context:

A/B Testing allows you to test two variants of a quest to see which performs better. Users are automatically segmented into Variant A or Variant B, and engagement, completion, and rewards are tracked.

### Creating A/B Quests in CMS - [How to Create an A/B Quest](https://docs.livelike.com/docs/how-to-create-ab-quest-in-cms#/)

<br />

## Managing Quests via SDK/API

#### Listing Available Quests

You can fetch a list of Quests available in current application. This list can be filtered by Quest IDs if you want to fetch only a few particular quests.

```javascript Javascript
LiveLike.getQuests({ questIds: ["<Quest Id 1>", "<Quest Id 2>"] })
  .then(paginatedResponse => console.log(paginatedResponse.results))
```
```swift Swift
let sdk: EngagementSDK
let questRequest = GetQuestsRequestOptions()

sdk.quests.getQuests(
  page: .first,
  options: questRequest
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let quests):
   	// handle success        
   }
}
```
```kotlin Kotlin
quests = (application as LiveLikeApplication).sdk.quests()

quests.getQuests(
    GetQuestsRequestOptions(),
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<LLPaginatedResult<Quest>>() {
        override fun onResponse(result: LLPaginatedResult<Quest>?, error: String?) {
            error?.let {
                ...
            }

            result?.let {
                ...
            }
        }})

//from SDK 2.79 onwards
quests.getQuests(
    GetQuestsRequestOptions(),
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<Quest>>() {
        override fun onResponse(result: List<Quest>?, error: String?) {
            error?.let {
                ...
            }

            result?.let {
                ...
            }
        }})


```

<br />

#### Starting a Quest

A UserQuest is an instance of a Quest that is attached to a user.  Upon creating a UserQuest, UserQuestTasks will automatically be created, which will then be used to track progress, status, etc.

```javascript Javascript
LiveLike.startUserQuest({ questId: "<Quest Id>" })
  .then(userQuest => console.log(userQuest))
```
```swift
let sdk: EngagementSDK

sdk.quests.startUserQuest(
  questID: self.quest.id
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let userQuest):
   	// handle success        
   }
}
```
```kotlin Kotlin
quests = (application as LiveLikeApplication).sdk.quests()

quests.startUserQuest(
    "<<QUEST ID>>",
    object : LiveLikeCallback<UserQuest>() {
        override fun onResponse(result: UserQuest?, error: String?) {
            error?.let{
                ...
            }
            result?.let {
                ...
            }
        }
    })
```

Quests can have limited eligibility. For example, they might only be available during a specific time window, or restricted to certain [Profile Groups](doc:profile-groups). Starting a quest will fail if the profile doesn't meet the eligibility requirements.

<br />

#### Listing user quests

You can fetch all userQuests started by a user.
This list is filterable by status and UserQuestIds
If you know a UserQuestId, you are able to get its details by using the code samples below. This can be useful if you would like to know the status of a UserQuest, or the individual progress from each UserQuestTask.

```javascript javascript
// query userQuest details for given userQuest ids, profileId with status incomplete
LiveLike.getUserQuests({ 
  profileId: "<User Profile Id>", 
  status: "incomplete" //accepted values of status are "completed" & "incomplete"
  userQuestIds: ["<Quest Id 1>", "<Quest Id 2>"], 
})
  .then(paginatedResponse => console.log(paginatedResponse.results))


// query userQuest whose rewards are claimed
LiveLike.getUserQuests({
    profileId: "<User Profile Id>",
    rewardStatus: LiveLike.QuestRewardStatus.CLAIMED
}).then(paginatedResponse => console.log(paginatedResponse))

// query userQuest whose rewards are unclaimed
LiveLike.getUserQuests({
    profileId: "<User Profile Id>",
    rewardStatus: LiveLike.QuestRewardStatus.UNCLAIMED
}).then(paginatedResponse => console.log(paginatedResponse))

// query all userQuest for a given profileId
LiveLike.getUserQuests({
    profileId: "<User Profile Id>"
}).then(paginatedResponse => console.log(paginatedResponse))
```
```swift
let sdk: EngagementSDK
let questRequest = GetUserQuestsRequestOptions()

sdk.quests.getUserQuests(
  page: .first,
  options: questRequest
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let quests):
   	// handle success        
   }
}
```
```kotlin Kotlin
quests = (application as LiveLikeApplication).sdk.quests()

quests.getUserQuests(
    GetUserQuestsRequestOptions(userQuestIds = listof(),status =  UserQuestStatus.COMPLETED, profileID = "<profileId>",rewardStatus = QuestRewardStatus.CLAIMED),
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<LLPaginatedResult<UserQuest>>() {
        override fun onResponse(result: LLPaginatedResult<UserQuest>?, error: String?) {
            error?.let{
                ...
            }

            result?.let {
                ...
            }
        }
    }
)

//from SDK 2.79 onwards
quests.getUserQuests(
    GetUserQuestsRequestOptions(userQuestIds = listof(),status =  UserQuestStatus.COMPLETED, profileID = "<profileId>",rewardStatus = QuestRewardStatus.CLAIMED),
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<UserQuest>>() {
        override fun onResponse(result: List<UserQuest>?, error: String?) {
            error?.let{
                ...
            }

            result?.let {
                ...
            }
        }
    }
)

```

<br />

#### Completing tasks in a user quest

The status of UserQuestTasks can be updated using `updateUserQuestTasks`.
This will go beyond and above the progress of that UserQuestTask

```javascript javascript
LiveLike.updateUserQuestTasks({ 
  userQuestId: "<User Quest Id>", 
  userQuestTaskIds: ["<Quest Task Id 1>", "<Quest Task Id 2>"], 
  status: "completed" //accepted values of status are "completed" & "incomplete"
})
  .then(userQuest => console.log(userQuest))
```
```swift
let sdk: EngagementSDK

sdk.quests.updateUserQuestTasks(
  userQuestID: "",
  userQuestTaskIDs: ["", ""],
  status: .completed
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let quests):
   	// handle success        
   }
}
```
```kotlin Kotlin
quests = (application as LiveLikeApplication).sdk.quests()

quests.updateUserQuestTask(
    "<<USER QUEST ID>>",
    listOf(
            "<<TASK ID 1>>",
            "<<TASK ID 2>>"
        ),
    UserQuestStatus.completed,
    object : LiveLikeCallback<UserQuest>() {
        override fun onResponse(result: UserQuest?, error: String?) {
            error?.let{
                ...
            }
            result?.let {
                ...
            }
        }
    })
```

<br />

#### Updating task progress in a user quest

UserQuestTask progress can be updated by utilizing one of the two SDK interfaces.

1. `incrementUserQuestTaskProgress` can be used to increment progress by the default value, or by a custom increment. The default increment is set in the CMS.
2. `setUserQuestTaskProgress` can be used to set an overall progress of the `UserQuestTask`. This will overwrite any previously set value.

```javascript javascript
LiveLike.incrementUserQuestTaskProgress({ 
  userQuestTaskId: "<Quest Task Id>", 
  customIncrement: "10" 
})
.then(userQuestTask => console.log(userQuestTask))

LiveLike.setUserQuestTaskProgress({ 
  userQuestTaskId: "<Quest Task Id>", 
  customProgress: "25" 
})
.then(userQuestTask => console.log(userQuestTask))
```
```swift Swift
let sdk: EngagementSDK

// Increment by a custom increment by passing a value in `customIncrement` variable
// or set it to `nil` to use a default increment set up in the CMS
sdk.quests.incrementUserQuestTaskProgress(
  userQuestTaskID: "",
  customIncrement: nil // Pass a `nil` to increment by a default increment
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let userQuest):
   	// handle success        
   }
}

// Set the overall progress of a `UserQuestTask`
// When set, previous progress will be overwritten 
sdk.quests.setUserQuestTaskProgress(
  userQuestTaskID: "",
  progress: 0.75
) { result in
	
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let userQuest):
   	// handle success        
   }
}
```
```kotlin Kotlin
quests.incrementUserQuestTaskProgress(
    "<<USER TASK ID>>",
    0.5f,
    object : LiveLikeCallback<UserQuestTask>() {
        override fun onResponse(result: UserQuestTask?, error: String?) {
            error?.let {
        	   ...
            }
            result?.let {
              ...  
            }
        }
    })
    
quests.setUserQuestTaskProgress(
    "<<USER TASK ID>>",
    0.5f,
    object : LiveLikeCallback<UserQuestTask>() {
        override fun onResponse(result: UserQuestTask?, error: String?) {
            error?.let{
                ...
            }
            result?.let {
                ...
            }
        }
    })
```

> 📘 Overriding user quest task progress
>
> Generally, progress on tasks is incremental, but task progress can also be set to an absolute value.
>
> The `setUserQuestTaskProgress` method can be used to set user quest task progress to a specific value, such as to zero if you'd like to reset the someone's progress on a task. For more API level details, check out the [Update User Quest Task Progress](ref:update-user-quest-task-progress) endpoint and the `custom_progress` field.

#### Getting quest rewards

Fetches the list of rewards associated with a given quest id.

```javascript
LiveLike.getQuestRewards({
    questId: "<Quest Id>"
}).then(paginatedResponse => console.log(paginatedResponse))
```
```swift
self.sdk.quests.getQuestRewards(
    page: .first,
    questID: <<Quest ID: String>>
) { result in
    switch result {
    case .failure(let error):
        //Failure Block
    case .success(let questRewards):
        //Success Block
    }
}
```
```kotlin
quests.getQuestRewards("<questID>", LiveLikePagination.FIRST,
                object : LiveLikeCallback<List<QuestReward>>() {
                    override fun onResponse(result: List<QuestReward>?, error: String?) {
                        result?.let {
                            
                        }
                        error?.let{
}
                    }

                })
```

Fetches the list of rewards associated with a given user quest id.

```javascript
LiveLike.getUserQuestRewards({
    userQuestId: "<User Quest Id>"
}).then(paginatedResponse => console.log(paginatedResponse))
```
```swift
self.sdk.quests.getUserQuestRewards(
    page: .first,
    userQuestID: <<User Quest ID: String>>,
    rewardStatus: <<QuestRewardStatus?>>
) { result in
  switch result {
  case .failure(let error):
    //Failure block
  case .success(let userQuestRewards):
    //Success Block
  }
}
```
```kotlin
quests.getUserQuestRewards(<userQuestId>,
                QuestRewardStatus.CLAIMED,
                LiveLikePagination.FIRST,
                object : LiveLikeCallback<List<UserQuestReward>>() {
                    override fun onResponse(result: List<UserQuestReward>?, error: String?) {
                        result?.let {
                           
                        }
                        error?.let{}
                    }
                })
```

Fetches the list of rewards associated with a given list of user quest id.

```javascript
LiveLike.getUserQuestRewards({
    userQuestIds: ["<User Quest Id 1>", "<User Quest Id 2>", "<User Quest Id 3>"]
}).then(paginatedResponse => console.log(paginatedResponse))
```

#### Completing a user quest

When all of the tasks in a user quest are completed, the quest itself is considered completed.

Completed user quests can have their rewards _claimed_ by the user. Rewards for a quest can only be claimed once per user completing the quest.

#### Claiming rewards for completed user quests

Claims the rewards associated with a quest once the quest is completed.

```javascript
LiveLike.claimUserQuestRewards({
    userQuestId: "<User Quest Id>"
}).then(userQuest => console.log(userQuest))
```
```swift
self.sdk.quests.claimUserQuestRewards(
    userQuestID: <<User Quest ID: String>>
) { result in
    switch result {
    case .failure(let error):
        //Failure Block
    case .success:
        //Success Block
    }
}
```
```kotlin
quests.claimUserQuestRewards("<user quest id>",
                object : LiveLikeCallback<UserQuest>() {
                    override fun onResponse(result: UserQuest?, error: String?) {
                        result?.let {
                            
                        }
                        error?.let{}
                    }
                })
```
