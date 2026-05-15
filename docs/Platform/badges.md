---
title: Badges
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Badges | Reward Programs | LiveLike Developer Hub
  description: >-
    A user profile badge is a badge that is linked to a user profile. A user
    profile can have multiple badges that can be earned or awarded.
  robots: index
next:
  description: ''
---
A user profile badge is a badge that is linked to a user profile. A user profile can have multiple badges that can be earned or awarded. Once a badge is earned or awarded it stays linked to the user profile regardless of any changes done to the badge. Badges can be earned by reaching a reward item thresholds or by completing [Quests](doc:quests). They can also be directly awarded via API.

## Earn badge at reward item threshold

Badges can be awarded automatically to users who reach a defined Reward Item Threshold set on the badge. For example, a badge could be set up to be awarded automatically when a user reaches 1,000 points by creating a [Reward Item](doc:rewards)  called Points, and then setting the Reward Item Threshold on the badge to 1,000 Points.

Reward item thresholds are optional and can be set when creating a new badge or modifying an existing one.

All users are eligible to earn the badge when they meet the threshold, but the badge will only be earned once per user. If a user reaches the threshold, earns the badge, and then goes below the threshold to meet it again, they will not earn the badge again.

## List badges belonging to a user

All the badges that have been earned or awarded to a user profile can be retrieved using the code samples below

```swift
let sdk: EngagementSDK
sdk.badges.getProfileBadgesBy(
	profileID: profileID, 
	page: .first
) { result in
   switch result {
     case .failure(let error):
     // print error
     case .success(let receivedProfileBadges):
     // show receivedProfileBadges
   }
}
```
```javascript
LiveLike.getProfileBadges({profileId: "<profile id>"})
  .then(badges => console.log(badges));
```
```kotlin
val badgesClient = livelikeSdk.badges()
badgesClient.getProfileBadges(
                profile_id_tv.text.toString(),
                LiveLikePagination.FIRST,
                liveLikeCallback = object :
                    LiveLikeCallback<LLPaginatedResult<ProfileBadge>>() {
                    override fun onResponse(
                        result: LLPaginatedResult<ProfileBadge>?,
                        error: String?
                    ) {
                       
                    }
                }
            )

//from SDK 2.79 onwards
badgesClient.getProfileBadges(
                profile_id_tv.text.toString(),
                LiveLikePagination.FIRST,
                liveLikeCallback = object :
                    LiveLikeCallback<List<ProfileBadge>>() {
                    override fun onResponse(
                        result: List<ProfileBadge>?,
                        error: String?
                    ) {
                       
                    }
                }
            )
```

## Retrieving user's progress towards earning a badge

A user's progress towards a badge can be retrieved using the code examples below. Since a single badge could be setup to be earned in different ways, multiple badge progressions are linked to a single Badge.

```swift
let sdk: EngagementSDK
sdk.badges.getProfileBadgeProgress(
  badgeIDs: ["<badge id>"]
) { result in
   switch result {
     case .success(let badgeProgression):
     // show badges with badge progress
     case .failure(let error):
     // show the error
   }
}
```
```javascript
LiveLike.getBadgeProgress({profileId: "<profile id>", badgeIds: ["xxxx", "xxxx"]})
  .then(res => console.log(res))
```
```kotlin
val badgesClient = livelikeSdk.badges()
badgesClient.getProfileBadgeProgress(
                profile_id_tv.text.toString(),
                mutableListOf(badge.id),
                object : LiveLikeCallback<List<BadgeProgress>>() {
                    override fun onResponse(result: List<BadgeProgress>?, error: String?) {
                       
                    }
                }
            )
```

## Retrieving all badges linked to an application

As an integrator you have the ability to retrieve all of the badges linked to an application. The results of this call can be used at a later time to query badge progress by passing badge ID's of interest.

```swift
let sdk: EngagementSDK
sdk.badges.getApplicationBadges(
  page: .first
) { result in
   switch result {
     case .failure(let error):
     // print error
     case .success(let receivedApplicationBadges):
     // show receivedApplicationBadges
   }
}
```
```javascript
LiveLike.getApplicationBadges().then(res => console.log(res));
```
```kotlin
val badgesClient = livelikeSdk.badges()
badgesClient.getApplicationBadges(
                LiveLikePagination.FIRST,
                object :
                    LiveLikeCallback<LLPaginatedResult<Badge>>() {
                    override fun onResponse(result: LLPaginatedResult<Badge>?, error: String?) {
                  
                    }
                }
            )

//from SDK 2.79 onwards
badgesClient.getApplicationBadges(
                LiveLikePagination.FIRST,
                object :
                    LiveLikeCallback<List<Badge>>() {
                    override fun onResponse(result: List<Badge>?, error: String?) {
                  
                    }
                }
            )
```

## Retrieving all profiles for a given badge

As an integrator you have the ability to retrieve all the profiles who have earned a given badge.

```javascript
LiveLike.getBadgeProfiles({
  badgeId: "<badge Id>"
}).then(res => console.log(res))
```
```kotlin
sdk.badges().getBadgeProfiles(<badge-id>,
            LiveLikePagination.FIRST,
            object : LiveLikeCallback<List<ProfilesByBadge>>(){
                override fun onResponse(result: List<ProfilesByBadge>?, error: String?)
                 {
                    result?.let {
                       
                    }
                    showError(error)
                }
            }
        )
```
```swift Swift
sdk.badges.getBadgeProfiles(
	badgeID: badgeIDInput.text!,
  page: .first
) { result in
	switch result {
		case .failure(let error):
			let alert = UIAlertController(title: "Error", message: error.localizedDescription, preferredStyle: .alert)
    	alert.addAction(UIAlertAction(title: "Ok", style: .cancel))
    	self.present(alert, animated: true, completion: nil)
		case .success(let receivedBadgeProfiles):
    	//Success Block
  }
}
```
