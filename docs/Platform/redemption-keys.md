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
## Redemption Keys basics

Redemption Keys facilitate exchanging codes for virtual or physical goods. Each redemption key these properties:

* **Code**: the value shown to users that they would enter to exchange the key for something.
* **Status**: represents whether the key has been redeemed or not to prevent using the same key multiple times. 
* **Assignee**: the profile the key is assigned to. If the key is assigned to a profile, it can only be redeemed by that profile.

## Creating Redemption Keys

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Redemption Keys" in the sidebar
3. Select the "New Redemption Key" button on the top right hand side
4. Enter Key name, description and a custom code (optional)
5. Select "Create" to finish

## Listing Redemption Keys

You can fetch all Redemption Keys (non producer users can see only keys redeemed by them) using the SDK interface **getRedemptionKeys**.  This interface supports **status** as a filter and returns a paginated list of Redemption Keys.

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

## Redeeming Keys by Code

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

## Redeem Keys by ID

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

## Unassign Key from Current Profile

Redeem Key can be unassigned from the current Profile

```kotlin
digitalGoods().unassignRedemptionKey(UnassignRedemptionKeyOptions("<key>")){ result,error -> ... }
```
```javascript JavaScript
LiveLike.unassignRedemptionKey({
 redemptionKeyId: "xxxxxxxxx"
 }).then(redemptionKey => console.log(redemptionKey))
```
