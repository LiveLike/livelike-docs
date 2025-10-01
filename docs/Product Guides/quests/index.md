---
title: Quests
excerpt: Complete multi-step challenges to earn one-time rewards
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## What are quests?

Quests are sets of tasks that the user must be completed to achieve a quest goal. Quest tasks are individual tasks or jobs a user must complete in order to make progress on the quest. Quest tasks can be completed in any order to still have progress towards the Quest goal.

## Why use quests?

Quests give the end user a more gamified experience. They have to do multiple things in order to accomplish a single goal. During the quests, the user and integrators are able to see the progress of the quest. This progress allows the user to see how much is left in order for them to complete the quest.

Quests can be used to build things like:

* New user on-boarding checklists
* Product and feature tours
* One-time promotional campaigns

## Creating quests

From the CMS:

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Quests" in the Sidebar
3. Select the "New Quest" button
4. Set the Quest name, Description, and add at least one subtask.
   Note: When creating a subtask, you may link a reward action for automating quest task progress
5. Select "Create" to finish

<Image border={false} src="https://files.readme.io/45bb0cc-Quests_in_CMS.png" title="Quests in CMS.png" />

The quest is now created and should be visible in the Quest list view.

## Listing quests

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

## Starting a quest

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

## Listing user quests

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

## Completing tasks in a user quest

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

## Updating task progress in a user quest

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

## Getting quest rewards

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

<br />

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

<br />

Fetches the list of rewards associated with a given list of user quest id.

```javascript
LiveLike.getUserQuestRewards({
    userQuestIds: ["<User Quest Id 1>", "<User Quest Id 2>", "<User Quest Id 3>"]
}).then(paginatedResponse => console.log(paginatedResponse))
```

## Claiming rewards for completed user quests

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
