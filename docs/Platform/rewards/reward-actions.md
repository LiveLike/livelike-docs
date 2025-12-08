---
title: Reward Actions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Reward Actions | LiveLike Developer Hub | LiveLike
  description: >-
    Reward Actions are used to trigger the reward engine for given built-in or
    custom actions on a platform. Learn more.
  robots: index
next:
  description: ''
---
Reward Action are used to trigger the reward engine for the given action. There are already built in reward actions already defined in producer suite where producer/integrators could also create their own custom reward actions.

## Built-in Reward Actions

| Action Name                     | Key                  |
| ------------------------------- | -------------------- |
| Replied to an Ask widget prompt | `ask-replied`        |
| Made a prediction               | `prediction-made`    |
| Made a correct prediction       | `prediction-correct` |
| Answered a quiz incorrectly     | `quiz-answered`      |
| Answered a quiz correctly       | `quiz-correct`       |
| Voted on a poll                 | `poll-voted`         |

## Custom Reward Actions

Some example of custom reward actions could be:

1. Opening an app once a day
2. Completing an on-boarding process
3. Reading an article
4. Watching a video

### Creating a Custom Reward Action

1. In producer suite, browse to the "Rewards" section from the left navigation panel.
2. Click on Actions tab which will show you list of all available reward actions.
3. Click on "New Reward Action" button, fill in the required details and click "Create".

### List of all Reward Actions

Get list of all reward actions. Each list item is a reward action object that contains a "key" property which could be used to fetch invoked reward actions for a given program id.

```javascript
LiveLike.getRewardActions().then(({results}) => console.log(results))
```
```kotlin
sdk.rewards().getRewardActions(
                LiveLikePagination.FIRST,
                object : LiveLikeCallback<LLPaginatedResult<RewardActionInfo>>() {
                    override fun onResponse(
                        result: LLPaginatedResult<RewardActionInfo>?,
                        error: String?
                    ) {
                       Log.d("result",result)
                    }
                })

//SDK 2.79 onwards
sdk.rewards().getRewardActions(
                LiveLikePagination.FIRST,
                object : LiveLikeCallback<List<RewardActionInfo>>() {
                    override fun onResponse(
                        result: List<RewardActionInfo>?,
                        error: String?
                    ) {
                       Log.d("result",result)
                    }
                })

```
```swift
self.sdk.rewards.getRewardActions(
	page: .first
) { result in
	switch result {
  case .failure(let error):
    //Failure Block
	case .success(let rewardActions):
    //Success Block
	}
}
```

### List of all invoked Reward actions

Get list all the invoked reward actions for a given program. You could also filter the reward actions by passing a list of reward action keys.

```javascript
LiveLike.getInvokedRewardActions({
  programId: "xxx-yyy-zzz",
  rewardActionKeys: ["xx-yy-zz"]
}).then(({results}) => console.log(results))
```
```kotlin
sdk.rewards().getInvokedRewardActions(
                LiveLikePagination.FIRST,
                invokedActionRequestParams = GetInvokedRewardActionParams(programId, rewardActionKeys)
                , object : LiveLikeCallback<LLPaginatedResult<InvokedRewardAction>>() {
                    override fun onResponse(
                        result: LLPaginatedResult<InvokedRewardAction>?,
                        error: String?
                    ) {
                         Log.d("result",result)
                    }
                })

//SDK 2.79 onwards
sdk.rewards().getInvokedRewardActions(
                LiveLikePagination.FIRST,
                invokedActionRequestParams = GetInvokedRewardActionParams(programId, rewardActionKeys)
                , object : LiveLikeCallback<List<InvokedRewardAction>>() {
                    override fun onResponse(
                        result: List<InvokedRewardAction>?,
                        error: String?
                    ) {
                         Log.d("result",result)
                    }
                })

```
```swift
self.sdk.rewards.getInvokedRewardActions(
	page: .first,
	options: GetInvokedRewardActionsOptions(
		programID: programID,
		rewardActionKeys: rewardActionKeys
	)
) { result in
	switch result {
	case .failure(let error):
    //Failure Block
  case .success(let invokedActions):
    //Success Block
	}
}
```

further filters can be supplied to narrow down your results.

filters include:

* profile ids to limit to specific users
* attributes to filter on integration supplied data

```kotlin
sdk.rewards().getInvokedRewardActions(
                LiveLikePagination.FIRST,
                invokedActionRequestParams = GetInvokedRewardActionParams(
                  profileIDs = listOf("userA", "userB"),
                  attributes = mapOf( 
                    "Season" to "2023",
                    "Rarity" to "Uncommon"
                    )
                )
                , object : LiveLikeCallback<LLPaginatedResult<InvokedRewardAction>>() {
                    override fun onResponse(
                        result: LLPaginatedResult<InvokedRewardAction>?,
                        error: String?
                    ) {
                         Log.d("result",result)
                    }
                })

//SDK 2.79 onwards
sdk.rewards().getInvokedRewardActions(
                LiveLikePagination.FIRST,
                invokedActionRequestParams = GetInvokedRewardActionParams(
                  profileIDs = listOf("userA", "userB"),
                  attributes = mapOf( 
                    "Season" to "2023",
                    "Rarity" to "Uncommon"
                    )
                )
                , object : LiveLikeCallback<List<InvokedRewardAction>>() {
                    override fun onResponse(
                        result: List<InvokedRewardAction>?,
                        error: String?
                    ) {
                         Log.d("result",result)
                    }
                })

```
```javascript
LiveLike.getInvokedRewardActions({
  profileIds: ["xxx-yyy", "www-zzz"],
  attributes: [{ key: "color", value: "red" }]
}).then(({results}) => console.log(results))
```
