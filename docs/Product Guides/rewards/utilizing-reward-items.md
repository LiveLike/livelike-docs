---
title: Utilizing Reward Items
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Utilizing Reward Items | LiveLike Developer Hub
  description: >-
    The Engagement SDK provides a set of reward item related interfaces which
    enable integrators to build out their custom experiences.
  robots: index
next:
  description: ''
---
The Engagement SDK provides a set of reward item related interfaces which enable integrators to build out their custom experiences. 

## Retrieve all Reward Items linked to an Application

All reward items linked to an [application](https://docs.livelike.com/docs/rest-api-getting-started#create-an-application) can be retrieved using the `getApplicationRewardItems` function. 

```swift Swift
let sdk: EngagementSDK

sdk.rewards.getApplicationRewardItems(
  page: .first
) { result in
   
   switch result {
     case .failure(let error):
     print(error)
     case .success(let rewardItems):
     print(rewardItems)
   }
}
```
```javascript javascript
LiveLike.init({ clientId })

const fetchNext = (fn) => {
  fn().then(res => {
    console.log('res', res);
    if(!res.done){
      fetchNext(fn);
    }
  })
}
LiveLike.getApplicationRewardItems().then(res => {
  console.log('res', res);
  fetchNext(res.next);
});
```
```kotlin Kotlin
rewardsClient = liveLikeSdk.rewards()
 rewardsClient.getApplicationRewardItems(
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<LLPaginatedResult<RewardItem>>() {
      override fun onResponse(result: LLPaginatedResult<RewardItem>?, error: String?) {
        
        }
    })
 
 //from SDK 2.79 onwards
 rewardsClient.getApplicationRewardItems(
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<RewardItem>>() {
      override fun onResponse(result: List<RewardItem>?, error: String?) {
        
        }
    })
 
```

## Reward Item Attributes

> 🚧 Reward Item Attributes
>
> This feature is only available on upcoming releases\
> Android v2.41+\
> iOS v2.40+\
> web SDK v2.16.0+

Reward Item Attributes provide integrators with organizational and filtering tools.\
These attributes are key, value pairs of data defined in the LikeLive CMS portal.

In addition when retrieving reward items, attributes can be used to filter reward item result sets.

```swift
let sdk: EngagementSDK

let attribute = RewardItemAttribute(key: "color", value: "blue")
let options = GetApplicationRewardItemsRequestOptions(attributes: [attribute])
sdk.rewards.getApplicationRewardItems(
  page: .first,
  options: options
) { result in
   
   switch result {
     case .failure(let error):
     print(error)
     case .success(let rewardItems):
     // print first attribute of each reward item
     rewardItems.forEach { rewardItem in
     	print("\(rewardItem.attributes.first?.key)")
        print("\(rewardItem.attributes.first?.value)")
     }
   }
}
```
```kotlin
rewardsClient.getApplicationRewardItems(
    LiveLikePagination.FIRST,
    ApplicationRewardItemsRequestParams(
        listOf(
            RewardAttribute("color", "blue"),
            RewardAttribute("type", "monster")
        )
    ),
    object : LiveLikeCallback<LLPaginatedResult<RewardItem>>() {
        override fun onResponse(
            page: LLPaginatedResult<RewardItem>?,
            error: String?
        ) {
            page?.let {
                it.results?.first()?.attributes?.let { attributes ->
                    val item = attributes.find { attribute -> attribute.key == "color" }
                    Log.i("color", item?.value.orEmpty())
                }
            }
        }
    })

//from SDK 2.79 onwards
rewardsClient.getApplicationRewardItems(
    LiveLikePagination.FIRST,
    ApplicationRewardItemsRequestParams(
        listOf(
            RewardAttribute("color", "blue"),
            RewardAttribute("type", "monster")
        )
    ),
    object : LiveLikeCallback<List<RewardItem>>() {
        override fun onResponse(
            page: List<RewardItem>?,
            error: String?
        ) {
            page?.let {
                it.results?.first()?.attributes?.let { attributes ->
                    val item = attributes.find { attribute -> attribute.key == "color" }
                    Log.i("color", item?.value.orEmpty())
                }
            }
        }
    })

```
```javascript
let attributes = [{key: "color", value: "blue"}]
LiveLike.getApplicationRewardItems({ attributes })
.then(res =>
	res.results.forEach(rewardItem => console.log(rewardItem.attributes))
)
```

## Reward Item Images

Reward Item Images enable integrators to visually enhance and customize their user experience

```swift
let sdk: EngagementSDK

sdk.rewards.getApplicationRewardItems(
  page: .first
) { result in
   
   switch result {
     case .failure(let error):
     print(error)
     case .success(let rewardItems):
     // print first image info of each reward item
     rewardItems.forEach { rewardItem in
     	print("\(rewardItem.images.first?.name)")
        print("\(rewardItem.images.first?.imageURL)")
     }
   }
}
```
```kotlin
rewardsClient.getApplicationRewardItems(
LiveLikePagination.FIRST,
object : LiveLikeCallback<LLPaginatedResult<RewardItem>>() {
    override fun onResponse(
        page: LLPaginatedResult<RewardItem>?,
        error: String?
    ) {
        page?.let {
            it.results?.first()?.images?.forEach { 
                Log.i("Images", "Name ${it.name}, Url ${it.url}, Mime Type ${it.mimeType}")
            }
        }
    }
})

//from SDK 2.79 onwards
rewardsClient.getApplicationRewardItems(
LiveLikePagination.FIRST,
object : LiveLikeCallback<List<RewardItem>>() {
    override fun onResponse(
        page: List<RewardItem>?,
        error: String?
    ) {
        page?.let {
            it.results?.first()?.images?.forEach { 
                Log.i("Images", "Name ${it.name}, Url ${it.url}, Mime Type ${it.mimeType}")
            }
        }
    }
})

```
```javascript
LiveLike.getApplicationRewardItems()
.then(res =>
	res.results.forEach(rewardItem => console.log(rewardItem.images))
)
```

## Retrieving Reward Item Balances for the current user

As an integrator you have the ability to check the reward item balance the current user has. This can be done by utilizing the `getRewardItemBalances` function where you pass IDs of reward items you are interested in. 

```swift
let sdk: EngagementSDK

self.sdk.rewards.getRewardItemBalances(
  rewardItemIds: rewardItemIDs
) { result in
   
   switch result {
     case .failure(let error):
     print(error)
     case .success(let balances):
     print(balances)
   }
}
```
```javascript javascript
LiveLike.init({ clientId })

LiveLike.getRewardItemBalances({ rewardItemIds: ["xxx", "xxx"] })
  .then(res => console.log(res))
```
```kotlin Kotlin
rewardsClient.getRewardItemBalances(
    				LiveLikePagination.FIRST,
            ids,
            object : LiveLikeCallback<LLPaginatedResult<RewardItemBalance>>() {
                override fun onResponse(result: LLPaginatedResult<RewardItemBalance>?, error: String?) {
                    result?.let {
                        println("Reward Balance =" + result.results)
                    }
                    error?.let { println("Error balance List =" + error.toString()) }
                }
            })

//from SDK 2.79 onwards
rewardsClient.getRewardItemBalances(
    				LiveLikePagination.FIRST,
            ids,
            object : LiveLikeCallback<List<RewardItemBalance>>() {
                override fun onResponse(result: List<RewardItemBalance>?, error: String?) {
                    result?.let {
                        println("Reward Balance =" + result.results)
                    }
                    error?.let { println("Error balance List =" + error.toString()) }
                }
            })

```

## Transferring Reward Item Amount to another User

To build out experiences such as gifting, tipping or just transferring Reward Item amounts to another user, you can use the `transferRewardItemAmount` function. 

```swift
let sdk: EngagementSDK

self.sdk.rewards.transferRewardItemAmount(
  10,
  recipientProfileID: <"recipient user profile">,
  rewardItemID: <"reward item ID">
) { result in
   switch result {
     case .failure(let error):
     print(error)
     case .success(let successfullTransfer):
     print(successfullTransfer)
   }
}
```
```javascript javascript
LiveLike.init({ clientId })

LiveLike.transferRewardItemAmount({ rewardItemId: "xxx", recipientProfileId: "xxx", amount: 10 })
  .then(res => console.log(res))
```
```kotlin Kotlin
rewardsClient.transferAmountToProfileId(selectedrewardItem!!.id,
                                        enter_amount_et.text.toString().toInt(),
                                        receipent_profile_id.text.toString(),
                                        object : LiveLikeCallback<TransferRewardItem>() {
                                          override fun onResponse(
                                            result: TransferRewardItem?,
                                            error: String?
                                          ) {

                                          }
                                        })
```

## Retrieving Reward Item Transfers for the current user

As an integrator you can retrieve the paginated list of reward item transfers the current user has done. This can be done by utilizing the `getRewardItemTransfers` function. 

```swift
let sdk: EngagementSDK

sdk.rewards.getRewardItemTransfers(
  page: .first
) { result in
   
   switch result {
     case .failure(let error):
     print(error)
     case .success(let rewardItemTransfers):
     print(rewardItemTransfers)
   }
}
```
```kotlin
rewardsClient = liveLikeSdk.rewards()
 rewardsClient.getRewardItemTransfers(
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<LLPaginatedResult<TransferRewardItem>>() {
      override fun onResponse(result: LLPaginatedResult<TransferRewardItem>?, error: String?) {
        
        }
    })
 
 //from SDK 2.79 onwards
 rewardsClient.getRewardItemTransfers(
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<TransferRewardItem>>() {
      override fun onResponse(result: List<TransferRewardItem>?, error: String?) {
        
        }
    })
```
```javascript javascript
LiveLike.init({ clientId })

const fetchNext = (fn) => {
  fn().then(res => {
    console.log('res', res);
    if(!res.done){
      fetchNext(fn);
    }
  })
}
LiveLike.getRewardItemTransfers().then(res => {
  console.log('res', res);
  fetchNext(res.next);
});
```

## Filtering Reward Item Transfers for the current user

As an integrator, you can filter reward item transfers the current user has done. Filtering can be done based on transfer\_type which allows filtering the sent or received transfers.  This can be done by utilizing the `getRewardItemTransfers` function as mentioned below

```swift
let sdk: EngagementSDK

sdk.rewards.getRewardItemTransfers(
  page: .first,
  options: RewardItemTransferRequestOptions(transferType: .sent)
) { result in 
   
   switch result {
     case .failure(let error):
     print(error)
     case .success(let rewardItemTransfers):
     print(rewardItemTransfers)
   }
}
```
```kotlin
val requestParams = 
                RewardItemTransferRequestParams(RewardItemTransferType.SENT)
  rewardsClient.getRewardItemTransfers(
                LiveLikePagination.FIRST,
                requestParams,
                object : LiveLikeCallback<LLPaginatedResult<TransferRewardItem>>() {
                    override fun onResponse(
                        result: LLPaginatedResult<TransferRewardItem>?,
                        error: String?
                    ) {
                        processRewardTransferListResponse(result, error)
                    }
                })
  
   //from SDK 2.79 onwards
    rewardsClient.getRewardItemTransfers(
                LiveLikePagination.FIRST,
                requestParams,
                object : LiveLikeCallback<List<TransferRewardItem>>() {
                    override fun onResponse(
                        result: List<TransferRewardItem>?,
                        error: String?
                    ) {
                        processRewardTransferListResponse(result, error)
                    }
                })
   
```
```javascript
LiveLike.getRewardItemTransfers({
   transferType: "sent" //valid values are: "sent" | "received"
})
.then(res => console.log(res))
```

## Notifying when Reward Item Transfer is received

As an integrator, you can inform users when they receive a new Reward Item Transfer.\
Depending upon platform, a delegate/Listener can be attached to the event and integrators will receive a RewardItemTransfer object.\
Using the RewardItemTransfer object, you can create a notification with appropriate information to the user

```swift
class IntegratorUseCase: RewardsClientDelegate {
   let sdk: EngagementSDK
   sdk.rewards.delegate = self
   
   func rewardsClient(
        _ rewardsClient: RewardsClient, 
        userDidReceiveRewardItemTransfer rewardItemTransfer: RewardItemTransfer
   ) { 
        // 'rewardItemTransfer' is the received Reward Item Transfer
   }
}
```
```kotlin
rewardsClient.rewardEventsListener = object : RewardEventsListener() {
            override fun onReceiveNewRewardItemTransfer(rewardItemTransfer: TransferRewardItem) {
               // integrators code to show notification etc
            }
        }

// for cleanup integrator has to remove the listener by setting it as null
rewardsClient.rewardEventsListener = null
```
```javascript
const transfercb = (transferDetails) => console.log(transferDetails)

LiveLike.addRewardEventListener(
  "reward-item-transfer-received", 
  transfercb
)

LiveLike.removeRewardEventListener(
  "reward-item-transfer-received", 
  transfercb // listenerFn param is optional, if not passed all listeners attached to the event will be removed
)
```

## Retrieving earned rewards filtered by widgets

An integrator can retrieve rewards earned (filtered by widget types and widget IDs) using SDK interface method `getRewardTransactions`.

`getRewardTransactions` takes arguments where the widget types and widget IDs can be specified. 

```swift
class IntegratorUseCase: RewardsClientDelegate {
   let sdk: EngagementSDK
   
   let options = RewardTransactionsRequestOptions(
     widgetIDs: ["widget ID","widget ID"],
     widgetKind: [.textPrediction, .imagePrediction]
   )
   
   sdk.rewards.getRewardTransactions(
     page: .first,
     options: options
   ) { result in
           
      switch result {
      	case .failure(let error):
        	// handle error
      	case .success(let rewardTransactions):
        	// work with rewardTransactions
      }
}
```
```kotlin
rewardsClient.getRewardTransactions(
                        LiveLikePagination.FIRST,
                        RewardTransactionsRequestParameters( 
                            widgetKindFilter = setOf(
                                WidgetType.IMAGE_PREDICTION, 
                                WidgetType.IMAGE_PREDICTION_FOLLOW_UP),
                          	widgetIds = setOf(
                                "<<widget id 1>>",
                                "<<widget id 2>>"
                        object : LiveLikeCallback<LLPaginatedResult<RewardTransaction>>() {
                            override fun onResponse(
                                result: LLPaginatedResult<RewardTransaction>?,
                                error: String?
                            ) {
                                ..
                            }
                        }
                    )
                            
 //from SDK 2.79 onwards  
 rewardsClient.getRewardTransactions(
                        LiveLikePagination.FIRST,
                        RewardTransactionsRequestParameters( 
                            widgetKindFilter = setOf(
                                WidgetType.IMAGE_PREDICTION, 
                                WidgetType.IMAGE_PREDICTION_FOLLOW_UP),
                          	widgetIds = setOf(
                                "<<widget id 1>>",
                                "<<widget id 2>>"
                        object : LiveLikeCallback<List<RewardTransaction>>() {
                            override fun onResponse(
                                result: List<RewardTransaction>?,
                                error: String?
                            ) {
                                ..
                            }
                        }
                    )
                            
```
```javascript javascript
getRewardTransactions({
  widgetIds: ["xx", "yy"],
  widgetKinds: ["text-poll", "text-prediction"],
  profileIds: ["xx-yy", "yy-zz"],
  rewardItemIds: ["123", "456"],
  rewardActionKeys: ["quiz-correct", "prediction-correct"],
  createdSince: '2022-06-01',
  createdUntil: '2022-07-31',
}).then(res => console.log(res));
```

## Retrieving potential widget rewards

Detailed information on potential earn-able rewards are attached to widgets and can be accessed through the Content Session.

To retrieve widget data:\
On Android see [get-published-widgets](https://docs.livelike.com/docs/widget-framework-apis#get-published-widgets)\
On iOS see [getPostedWidgetModels()](https://docs.livelike.com/docs/accessing-widget-data#get-published-widget-models-from-history)\
on Web see [getWidgets](https://docs.livelike.com/docs/widget-api-methods#getwidgets)

```swift
class IntegratorUseCase: RewardsClientDelegate {
   let session: ContentSession
   contentSession.getWidgetModels(
     page: .first,
     options: reqOptions
   ) { result in
      
      switch result {
      case let .success(widgetModels):
      	guard let firstWidgetModel = widgetModels.first else { return }
        switch firstWidgetModel {
        case .prediction(let predictionWidgetModel):
        	predictionWidgetModel.earnableRewards.forEach { earnableReward in
              // work with earnable reward
            }
       	default:
          break
        }
       case let .failure(error):
        print(error)
      }
      
     }
}
```
```kotlin
session.getWidgets(
	LiveLikePagination.FIRST,
  WidgetsRequestParameters(widgetStatus = WidgetStatus.PENDING),
  object : LiveLikeCallback<List<LiveLikeWidget>>() {
  	override fun onResponse(result: List<LiveLikeWidget>?, error: String?) {
      result?.forEach {
        it.earnableRewards?.forEach { rewardSummary ->  
          Log.i("reward info ", 
                "Name ${rewardSummary.rewardItemName}, Amount ${rewardSummary.rewardItemAmount}" 
          }
        }
      }
   }
 )
```
```javascript javascript
LiveLike.getWidgets({
  programId: "xxxx",
  status: "pending", //Valid status values are 'scheduled', 'pending', 'published'
  widgetKinds: ["text-poll"],
  ordering: "recent" //Valid ordering values are 'recent'
})
.then(res => 
	res.results.forEach((widget) => {
		console.log('widget Id', widget.id, widget.earnable_rewards);
    widget.options.forEach((option) => console.log('option id', option.id, option.earnable_rewards))    
	})
);
```
