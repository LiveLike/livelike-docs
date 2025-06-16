---
title: Quest
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## What are Quests?

Quests are sets of tasks that the user must be completed to achieve a quest goal. Quest tasks are individual tasks or jobs a user must complete in order to make progress on the quest. Quest tasks can be completed in any order to still have progress towards the Quest goal. 

## Why use Quests?

Quests give the end user a more gamified experience. They have to do multiple things in order to accomplish a single goal. During the quests, the user and integrators are able to see the progress of the quest. This progress allows the user to see how much is left in order for them to complete the quest. 

Quests can be used to build things like:

* New user on-boarding checklists
* Product and feature tours
* One-time promotional campaigns

## Configuring Quests

From the CMS:

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Quests" in the Sidebar
3. Select the "New Quest" button
4. Set the Quest name, Description, and add at least one subtask.\
   Note: When creating a subtask, you may link a reward action for automating quest task progress
5. Select "Create" to finish

![3336](https://files.readme.io/45bb0cc-Quests_in_CMS.png "Quests in CMS.png")

The quest is now created and should be visible in the Quest list view.

## Getting Quest List

You can fetch a list of Quests available in current application. This list can be filtered by Quest IDs if you want to fetch only a few particular quests.

**API Definition:** [getQuests](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getQuests)

```javascript Javascript
import { getQuests } from "@livelike/javascript"

getQuests({ questIds: ["<Quest Id 1>", "<Quest Id 2>"] })
  .then(paginatedResponse => console.log(paginatedResponse.results))
```

## Starting a UserQuest

A UserQuest is an instance of a Quest that is attached to a user.  Upon creating a UserQuest, UserQuestTasks will automatically be created, which will then be used to track progress, status, etc.

**API Definition:** [startUserQuest](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=startUserQuest)

```javascript Javascript
import { startUserQuest } from "@livelike/javascript"

startUserQuest({ questId: "<Quest Id>" })
  .then(userQuest => console.log(userQuest))
```

## Getting UserQuest List

You can fetch all userQuests started by a user.\
This list is filterable by status and UserQuestIds\
If you know a UserQuestId, you are able to get its details by using the code samples below. This can be useful if you would like to know the status of a UserQuest, or the individual progress from each UserQuestTask. 

**API Definition:** [getUserQuests](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getUserQuests)

```javascript javascript
import { getUserQuests, UserQuestStatus, QuestRewardStatus } from "@livelike/javascript"

// query userQuest details for given userQuest ids, profileId with status incomplete
getUserQuests({ 
  profileId: "<User Profile Id>", 
  status: UserQuestStatus.INCOMPLETE, //accepted values of status are "completed" & "incomplete"
  userQuestIds: ["<Quest Id 1>", "<Quest Id 2>"], 
})
  .then(paginatedResponse => console.log(paginatedResponse.results))


// query userQuest whose rewards are claimed
getUserQuests({
    profileId: "<User Profile Id>",
    rewardStatus: QuestRewardStatus.CLAIMED
}).then(paginatedResponse => console.log(paginatedResponse))

// query userQuest whose rewards are unclaimed
getUserQuests({
    profileId: "<User Profile Id>",
    rewardStatus: QuestRewardStatus.UNCLAIMED
}).then(paginatedResponse => console.log(paginatedResponse))

// query all userQuest for a given profileId
getUserQuests({
    profileId: "<User Profile Id>"
}).then(paginatedResponse => console.log(paginatedResponse))
```

## Updating UserQuestTask Status

The status of UserQuestTasks can be updated using `updateUserQuestTasks`.\
This will go beyond and above the progress of that UserQuestTask

**API Definition:** [updateUserQuestTasks](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=updateUserQuestTasks)

```javascript
import { updateUserQuestTasks, UserQuestStatus } from "@livelike/javascript"

updateUserQuestTasks({ 
  userQuestId: "<User Quest Id>", 
  userQuestTaskIds: ["<Quest Task Id 1>", "<Quest Task Id 2>"], 
  status: UserQuestStatus.COMPLETED //accepted values of status are "completed" & "incomplete"
})
  .then(userQuest => console.log(userQuest))
```

## Updating UserQuestTask Progress

`UserQuestTask` progress can be updated by utilizing one of the two SDK interfaces.

1. `incrementUserQuestTaskProgress` can be used to increment progress by the default value, or by a custom increment. The default increment is set in the CMS. 
2. `setUserQuestTaskProgress` can be used to set an overall progress of the `UserQuestTask`. This will overwrite any previously set value. 

**API Definition:** [incrementUserQuestTaskProgress](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=incrementUserQuestTaskProgress)\
**API Definition:** [setUserQuestTaskProgress](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=setUserQuestTaskProgress)

```javascript javascript
import { incrementUserQuestTaskProgress, setUserQuestTaskProgress } from "@livelike/javascript"

incrementUserQuestTaskProgress({ 
  userQuestTaskId: "<Quest Task Id>", 
  customIncrement: "10" 
})
.then(userQuestTask => console.log(userQuestTask))

setUserQuestTaskProgress({ 
  userQuestTaskId: "<Quest Task Id>", 
  customProgress: "25" 
})
.then(userQuestTask => console.log(userQuestTask))
```

## Get Quest Rewards

Fetches the list of rewards associated with a given quest id.

**API Definition:** [getQuestRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getQuestRewards)

```javascript
import { getQuestRewards } from "@livelike/javascript"

getQuestRewards({
    questId: "<Quest Id>"
}).then(paginatedResponse => console.log(paginatedResponse))
```

## Get User Quest Rewards

Fetches the list of rewards associated with a given user quest id.

**API Definition:** [getUserQuestRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getUserQuestRewards)

```javascript
import { getUserQuestRewards } from "@livelike/javascript"

getUserQuestRewards({
    userQuestId: "<User Quest Id>"
}).then(paginatedResponse => console.log(paginatedResponse))
```

## Claim User Quest Rewards

Claims the rewards associated with a quest once the quest is completed.

**API Definition:** [claimUserQuestRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=claimUserQuestRewards)

```javascript
import { claimUserQuestRewards } from "@livelike/javascript"

claimUserQuestRewards({
    userQuestId: "<User Quest Id>"
}).then(userQuest => console.log(userQuest))
```
