---
title: Redemption Keys
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Redemption Keys | LiveLike Developer Hub
  description: >-
    A redemption key is an object created on the Application level in the
    Producer Suite. Learn more.
  robots: index
next:
  description: ''
---
## What are Redemption Keys?

A redemption key is an object that is created on the Application level in the [Producer Site](https://cf-blast.livelikecdn.com/producer).\
As an integrator, you can issue unique redemption keys to users that can be redeemed in first-party or third-party systems.\
These keys can be created from CMS ([https://cf-blast.livelikecdn.com/producer](https://cf-blast.livelikecdn.com/producer)) and then can be issued to users\
As a user, you can redeem these unique keys (using code/id)

## Creating Redemption Key

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Redemption Keys" in the Sidebar
3. Select the "New Redemption Key" button on the top right hand side
4. Enter Key Name, Description and a custom code (optional)
5. Select "Create" to finish

![](https://files.readme.io/ff65525-Screenshot_2022-02-14_at_1.49.26_PM.png "Screenshot 2022-02-14 at 1.49.26 PM.png")

## Fetching Redemption Keys  in the SDK

You can fetch all Redemption Keys (non producer users can see only keys redeemed by them) using the SDK interface **getRedemptionKeys**\
This interface supports **status** as filter\
This interface returns paginated list of Redemption Keys

```swift
let sdk: EngagementSDK

sdk.getRedemptionKeys(
  page: .first,
  options: nil
) { result in
	
  switch result {
  case .failure(let error):
    print("Error: \(error)"            
  case .success(let redeemedCodes):
    print("Success")                
  }
}
```
```javascript
LiveLike.getRedemptionKeys({
  status: "redeemed" //Valid values are active, inactive, redeemed
})
.then(paginatedRedemptionKeys => console.log(paginatedRedemptionKeys))
```
```kotlin
rewardsClient.getRedemptionKeys(LiveLikePagination.FIRST,
  object : LiveLikeCallback<LLPaginatedResult<RedemptionKey>>() {
    override fun onResponse(
      result: LLPaginatedResult<RedemptionKey>?,error: String?) {
        ...           
      }
})
```

## Redeem Key By Code  in the SDK

Keys can be redeemed using the SDK interface **redeemKeyByCode** by passing the code of the Redemption Key

```swift
let sdk: EngagementSDK

sdk.redeemKeyBy(
  redemptionCode: "xxxxxxxxx"
) { result in
	
  switch result {
  case .failure(let error):
    print("Error: \(error)"            
  case .success(let redemptionKey):
    print("Success")                
  }
}
```
```javascript
LiveLike.redeemKeyByCode({
  code: "xxxxxxxxx"
}).then(redemptionKey => console.log(redemptionKey))
```
```kotlin
rewardsClient.redeemKeyWithCode("xxxxxxxxx",
  object : LiveLikeCallback<RedemptionKey>() {
    override fun onResponse(result: RedemptionKey?, error: String?) {
      ...
    })
```

## Redeem Key By ID  in the SDK

Keys can be redeemed using the SDK interface **redeemKeyById** by passing the id of the Redemption Key

```swift
let sdk: EngagementSDK

sdk.redeemKeyBy(
  redemptionKeyID: "xxxxxxxxx"
) { result in
	
  switch result {
  case .failure(let error):
    print("Error: \(error)"            
  case .success(let redemptionKey):
    print("Success")                
  }
}
```
```javascript
LiveLike.redeemKeyById({
  redemptionKeyId: "xxxxxxxxx"
}).then(redemptionKey => console.log(redemptionKey))
```
```kotlin
rewardsClient.redeemKeyWithId("xxxxxxxxx",
  object : LiveLikeCallback<RedemptionKey>() {
    override fun onResponse(result: RedemptionKey?, error: String?) {
      ...
    })
```

## Unassign Redeem Key to CurrentProfile

Redeem Key can be unassigned from the current Profile

```kotlin
digitalGoods().unassignRedemptionKey(UnassignRedemptionKeyOptions("<key>")){ result,error -> ... }
```
```javascript JavaScript
LiveLike.unassignRedemptionKey({
 redemptionKeyId: "xxxxxxxxx"
 }).then(redemptionKey => console.log(redemptionKey))
```
