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
## User Profile Badges

A user profile badge is a badge that is linked to a user profile. A user profile can have multiple badges that can be earned or awarded. Once a badge is earned or awarded it stays linked to the user profile regardless of any changes done to the badge.

## Utilizing Badges

A badge can be awarded or earned. To award a badge please use the award badge rest API.\
To set up a way to earn a badge, please follow the instructions below.

The following items are required to be completed for a user to be able to earn a badge.

1. Create a **Reward Item**
   1. In the Producer Suite, on the left hand side click on **Rewards**.
   2. There are three tabs, make sure you are on the tab called **Items**
   3. On the top right hand side click on the button **New Reward Item**
   4. Fill in the name and click **Create**
2. Create a **Reward Action**
   1. In the Producer Suite, on the left hand side click on **Rewards**.
   2. There are three tabs, make sure you are on the tab called **Actions**
   3. On the top right hand side click on the button **New Reward Action**
   4. Fill in the details and click **Create**
3. Create a **Reward Table**
   1. In the Producer Suite, on the left hand side click on **Rewards**
   2. There are three tabs, make sure you are on the tab called **Tables**
   3. On the top right hand side click on the button **New Reward Table**
   4. Fill in the name, pick a program for it to be linked to and click **Create**
   5. Once a table is created, click on it's name in the list of all Reward Tables.
   6. You will see a screen showing all table entries. To add a new one, click on the **New Entry** button
   7. In the New Entry modal, you will be able to pick and connect a **Reward Action** with a **Reward Item** in addition you will be able to set up a **Reward Item Amount**, which is the amount that will be awarded to a user when this entry is earned. 
   8. Click **Create** to create a reward table entry
4. Create a **Badge**
   1. In the Producer Suite, on the left hand side click on **Badges**.
   2. On the top right hand side, click on the button **New Badge**
   3. Fill in all the information and click **Create**
5. Connect the **Badge** with a **Reward Item**
   1. Find the **Badge** you created in the Badges list
   2. Click on the three vertical dots on the right hand side and click **Edit Badge**
   3. In this modal you will be able to create a connection between a Reward Item and a Badge. In addition you will be able to set the **Reward Item Threshold**, which is the amount of points a user is required to earn this badge.

## Retrieve badges earned or awarded to a user

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
