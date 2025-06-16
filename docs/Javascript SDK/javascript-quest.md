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
[block:api-header]
{
  "title": "What are Quests?"
}
[/block]
Quests are sets of tasks that the user must be completed to achieve a quest goal. Quest tasks are individual tasks or jobs a user must complete in order to make progress on the quest. Quest tasks can be completed in any order to still have progress towards the Quest goal. 
[block:api-header]
{
  "title": "Why use Quests?"
}
[/block]
Quests give the end user a more gamified experience. They have to do multiple things in order to accomplish a single goal. During the quests, the user and integrators are able to see the progress of the quest. This progress allows the user to see how much is left in order for them to complete the quest. 

Quests can be used to build things like:

* New user on-boarding checklists
* Product and feature tours
* One-time promotional campaigns
[block:api-header]
{
  "title": "Configuring Quests"
}
[/block]
From the CMS:
1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Quests" in the Sidebar
3. Select the "New Quest" button
4. Set the Quest name, Description, and add at least one subtask.
    Note: When creating a subtask, you may link a reward action for automating quest task progress
5. Select "Create" to finish
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/45bb0cc-Quests_in_CMS.png",
        "Quests in CMS.png",
        3336,
        1000,
        "#c2d8e5"
      ]
    }
  ]
}
[/block]
The quest is now created and should be visible in the Quest list view.
[block:api-header]
{
  "title": "Getting Quest List"
}
[/block]
You can fetch a list of Quests available in current application. This list can be filtered by Quest IDs if you want to fetch only a few particular quests.

**API Definition:** [getQuests](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getQuests)
[block:code]
{
  "codes": [
    {
      "code": "import { getQuests } from \"@livelike/javascript\"\n\ngetQuests({ questIds: [\"<Quest Id 1>\", \"<Quest Id 2>\"] })\n  .then(paginatedResponse => console.log(paginatedResponse.results))",
      "language": "javascript",
      "name": "Javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Starting a UserQuest"
}
[/block]
A UserQuest is an instance of a Quest that is attached to a user.  Upon creating a UserQuest, UserQuestTasks will automatically be created, which will then be used to track progress, status, etc.

**API Definition:** [startUserQuest](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=startUserQuest)
[block:code]
{
  "codes": [
    {
      "code": "import { startUserQuest } from \"@livelike/javascript\"\n\nstartUserQuest({ questId: \"<Quest Id>\" })\n  .then(userQuest => console.log(userQuest))",
      "language": "javascript",
      "name": "Javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting UserQuest List"
}
[/block]
You can fetch all userQuests started by a user.
This list is filterable by status and UserQuestIds
If you know a UserQuestId, you are able to get its details by using the code samples below. This can be useful if you would like to know the status of a UserQuest, or the individual progress from each UserQuestTask. 

**API Definition:** [getUserQuests](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getUserQuests)
[block:code]
{
  "codes": [
    {
      "code": "import { getUserQuests, UserQuestStatus, QuestRewardStatus } from \"@livelike/javascript\"\n\n// query userQuest details for given userQuest ids, profileId with status incomplete\ngetUserQuests({ \n  profileId: \"<User Profile Id>\", \n  status: UserQuestStatus.INCOMPLETE, //accepted values of status are \"completed\" & \"incomplete\"\n  userQuestIds: [\"<Quest Id 1>\", \"<Quest Id 2>\"], \n})\n  .then(paginatedResponse => console.log(paginatedResponse.results))\n\n\n// query userQuest whose rewards are claimed\ngetUserQuests({\n    profileId: \"<User Profile Id>\",\n    rewardStatus: QuestRewardStatus.CLAIMED\n}).then(paginatedResponse => console.log(paginatedResponse))\n\n// query userQuest whose rewards are unclaimed\ngetUserQuests({\n    profileId: \"<User Profile Id>\",\n    rewardStatus: QuestRewardStatus.UNCLAIMED\n}).then(paginatedResponse => console.log(paginatedResponse))\n\n// query all userQuest for a given profileId\ngetUserQuests({\n    profileId: \"<User Profile Id>\"\n}).then(paginatedResponse => console.log(paginatedResponse))",
      "language": "javascript",
      "name": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Updating UserQuestTask Status"
}
[/block]
The status of UserQuestTasks can be updated using `updateUserQuestTasks`.
This will go beyond and above the progress of that UserQuestTask

**API Definition:** [updateUserQuestTasks](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=updateUserQuestTasks)
[block:code]
{
  "codes": [
    {
      "code": "import { updateUserQuestTasks, UserQuestStatus } from \"@livelike/javascript\"\n\nupdateUserQuestTasks({ \n  userQuestId: \"<User Quest Id>\", \n  userQuestTaskIds: [\"<Quest Task Id 1>\", \"<Quest Task Id 2>\"], \n  status: UserQuestStatus.COMPLETED //accepted values of status are \"completed\" & \"incomplete\"\n})\n  .then(userQuest => console.log(userQuest))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Updating UserQuestTask Progress"
}
[/block]
`UserQuestTask` progress can be updated by utilizing one of the two SDK interfaces.
1. `incrementUserQuestTaskProgress` can be used to increment progress by the default value, or by a custom increment. The default increment is set in the CMS. 
2. `setUserQuestTaskProgress` can be used to set an overall progress of the `UserQuestTask`. This will overwrite any previously set value. 

**API Definition:** [incrementUserQuestTaskProgress](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=incrementUserQuestTaskProgress)
**API Definition:** [setUserQuestTaskProgress](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=setUserQuestTaskProgress)
[block:code]
{
  "codes": [
    {
      "code": "import { incrementUserQuestTaskProgress, setUserQuestTaskProgress } from \"@livelike/javascript\"\n\nincrementUserQuestTaskProgress({ \n  userQuestTaskId: \"<Quest Task Id>\", \n  customIncrement: \"10\" \n})\n.then(userQuestTask => console.log(userQuestTask))\n\nsetUserQuestTaskProgress({ \n  userQuestTaskId: \"<Quest Task Id>\", \n  customProgress: \"25\" \n})\n.then(userQuestTask => console.log(userQuestTask))",
      "language": "javascript",
      "name": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Quest Rewards"
}
[/block]
Fetches the list of rewards associated with a given quest id.

**API Definition:** [getQuestRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getQuestRewards)
[block:code]
{
  "codes": [
    {
      "code": "import { getQuestRewards } from \"@livelike/javascript\"\n\ngetQuestRewards({\n    questId: \"<Quest Id>\"\n}).then(paginatedResponse => console.log(paginatedResponse))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get User Quest Rewards"
}
[/block]
Fetches the list of rewards associated with a given user quest id.

**API Definition:** [getUserQuestRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getUserQuestRewards)
[block:code]
{
  "codes": [
    {
      "code": "import { getUserQuestRewards } from \"@livelike/javascript\"\n\ngetUserQuestRewards({\n    userQuestId: \"<User Quest Id>\"\n}).then(paginatedResponse => console.log(paginatedResponse))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Claim User Quest Rewards"
}
[/block]
Claims the rewards associated with a quest once the quest is completed.

**API Definition:** [claimUserQuestRewards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=claimUserQuestRewards)
[block:code]
{
  "codes": [
    {
      "code": "import { claimUserQuestRewards } from \"@livelike/javascript\"\n\nclaimUserQuestRewards({\n    userQuestId: \"<User Quest Id>\"\n}).then(userQuest => console.log(userQuest))",
      "language": "javascript"
    }
  ]
}
[/block]