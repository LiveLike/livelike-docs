---
title: Blocking Profiles
deprecated: false
hidden: false
metadata:
  title: Blocking Profiles | LiveLike Developer Hub
  description: >-
    In order to help users keep themselves safe, they can block others from
    engaging with them in certain ways. Learn more about blocking profiles.
  robots: index
next:
  description: ''
---
Sometimes users are not comfortable, or are being harassed by another user. In order to help users to keep themselves safe, they can block others from engaging with them in certain ways.

## How Blocks Work

When one user blocks another, the restriction applies mutually between both profiles. This means neither user can directly interact with the other. These protections are enforced at the system level, starting from the API layer, and apply across all interaction points. Once a block is in place, both users are prevented from engaging with each other in any restricted way.

When a block exists between two users, the restriction applies mutually. Neither user can interact with the other across the following areas:
Comments

* Comment creation blocked
* Comment reply blocked
* Comment mention blocked
* Comment reporting blocked
* Comment reaction blocked (create only)

Chat

* Chat message quote blocked
* Chat message reply blocked
* Chat mention blocked
* Chat reaction blocked (create only)

Chatroom

* Chatroom membership blocked
* Chatroom invitation blocked

Social Graph

* Creating social graph relationships blocked

<br />

<Callout icon="📘" theme="info">
  Social features integrated via API have to implement content filtering at the integration level. Direct interaction between users are prevented at the system level, but indirect interaction is not.
</Callout>

## Creating a Block

As an integrator, you can now allow users to block other users from sending invitations or adding them to chat rooms.

```swift
/*
To enable the user to block other users, you can implement the `blockProfile` method which is
a part of the `ChatClient`. It accepts a parameter `profileID` which corresponds to the id 
of the profile to be blocked.

On successful completion, the method returns an object of type `BlockInfo` which contains 
details of the profile blocked and the profile it was blocked by.
*/

sdk.chat.blockProfile(
		profileID: profileID
) { result in
   	switch result {
    case .success(let blockedProfile):
         self.showAlert(
            title: "Profile Blocked",
         		message: "Id:\(blockedProfile.blockedProfileID)"
         )
    case .failure(let error):
    		self.showAlert(title: "Error", message: error.localizedDescription)
		}
}
```
```kotlin
sdk.blockProfile(
  profileId,
  object: LiveLikeCallback < BlockedData > () {
    override fun onResponse(result: BlockedData ? , error : String ? ) {
      result?.let {
        showToast("BLocked User: ${it.blockedProfileID}, BlockID: ${it.id}")
      }
      error?.let {
        it1 -> showToast(it1)
      }
    }
  }
)
```
```javascript
LiveLike.blockProfile({
    profileId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
})
.then(blockInfo => console.log(blockInfo))
```

## Removing a Block

As an integrator, you can now allow users to unblock users they had previously blocked from sending invitations or adding them to chat rooms.

```swift
/*
To enable the user to unblock other users, you can implement the `unblockProfile` method 
which is a part of the `ChatClient`. It accepts one parameter: `blockRequestID` which 
corresponds to the id of the  `BlockInfo` for the blocked profile.
*/

sdk.chat.unblockProfile(blockRequestID: requestID) { result in
		switch result {
    case .success(_):
    		break
    case .failure(let error):
    		self.showAlert(title: "Error", message: error.localizedDescription)
		}
}
```
```kotlin
sdk.unBlockProfile(blockID,
  object: LiveLikeCallback < LiveLikeEmptyResponse > () {
    override fun onResponse(result: LiveLikeEmptyResponse ? , error : String ? ) {
      error?.let {
        showToast(it)
      }
      result?.let {
        showToast("Success Unblock")
      }
    }
  }
)
```
```javascript
// blockId is the id of the blockInfo for a given blocked profile,
// could be fetched from `getBlockInfoList` or `getProfileBlockInfo`
LiveLike.unblockProfile({
    blockId: "c327a72c-94e5-4f5a-bcef-16ee84d35077"
 })
.then(response => console.log(response))
```

Unblocking can be done using alternative APIs

* By blocked user's profile ID
  * `DELETE /api/v1/profiles/{blocked_by_profile_id}/profile-blocks/{blocked_profile_id}/`
* By blocked user's profile custom ID  
  * `DELETE /api/v1/unblock-by-profile-custom-id/{client_id}/{blocked_profile_custom_id}/`

## Getting a List of Blocks

As an integrator, you can show the user a list of all the profiles blocked by the user.

```swift
/*
To display the list, you can implement the `getBlockedProfileList` method which is a part
of the `ChatClient`. The method accepts a parameter `profileID` which corresponds to the id of the 
profile blocked which can be used as a filter for the 
request and is `optional`.

On successful completion, the method returns a paginated list of type `BlockInfo` which 
contains details of the profile blocked and the profile it was blocked by.
*/

sdk.chat.getBlockedProfileList(
		blockedProfileID: profileID, 
		page: .first
) { result in
            switch result {
		case .success(let blockedProfiles):
				if blockedProfiles.count >= 1 {
						self.showAlert(
            		title: "No. of Profiles:",
                message: "\(blockedProfiles.count)"
        		)
    		}
		case .failure(let error):
    		print(error.localizedDescription)
		}
}
```
```kotlin
sdk.getBlockedProfileList(LiveLikePagination.FIRST,
  blockedProfileId, // send it as null if you want to fetch all block profile
  object: LiveLikeCallback < List < BlockedData >> () {
    override fun onResponse(result: List < BlockedData > ? , error : String ? ) {
      error?.let {
        it1 -> showToast(it1)
      }
      result?.let {
        //block profile list  
      }
    }
  }
)
```
```javascript
LiveLike.getBlockInfoList()
.then(paginatedBlockInfo => console.log(paginatedBlockInfo))
```

You can also [Get Blocked Profile Ids](ref:get-blocked-profile-ids) for a list of blocked profile IDs that isn't paginated.

## Getting block profile info

Use `getProfileBlockInfo` to get block information for a particular profile Id.

```javascript
LiveLike.getProfileBlockInfo({
    profileId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
})
.then(blockInfo => console.log(blockInfo))
```
```swift
sdk.chat.getProfileBlockInfo(profileID: profileID) { result in
	switch result {
  	case .success(let blockInfo):
    	// Success Block
    case .failure(let error):
    	print(error.localizedDescription)
	}
}
```
```kotlin Kotlin
sdk.chat().getProfileBlockInfo(<profileId>,object : LiveLikeCallback<BlockedInfo>() {
        override fun onResponse(result:BlockedInfo?,error: String?) {
//receive result or error
})
```

## Real time block/unblock profile events

You can add listeners/delegators for getting real time block/unblock profile events

> 📘 Platform specific implementation
>
> Implementation for receiving real time events is different for Web, Android and IOS.

```javascript
// For adding block profile event listener
function onBlockProfileListener(blockInfo){
    console.log(blockInfo);
}

// When user is blocked, attach listener fn to be called 
LiveLike.addUserProfileEventListener(
    LiveLike.UserProfileEvent.BLOCK_PROFILE,
    onBlockProfileListener
)

// to remove block profile event listener
LiveLike.removeUserProfileEventListener(
    LiveLike.UserProfileEvent.BLOCK_PROFILE,
    onBlockProfileListener
);


// For adding unblock profile event listener
function onUnblockProfileListener(blockInfo){
    console.log(blockInfo);
}

// When user is Unblocked, attach listener fn to be called 
LiveLike.addUserProfileEventListener(
    LiveLike.UserProfileEvent.UNBLOCK_PROFILE,
    onUnblockProfileListener
)

// to remove unblock profile event listener
LiveLike.removeUserProfileEventListener(
    LiveLike.UserProfileEvent.UNBLOCK_PROFILE,
    onUnblockProfileListener
);
```
```swift
//To receive realtime events for blocking or unblocking a profile.
//The respective ViewController should confirm to ChatClientDelegate.

class SomeClass: UIViewController {
  override func viewDidLoad() {
    super.viewDidLoad()
    sdk.chat.delegate = self
  }
}

extension SomeClass: ChatClientDelegate {
    func chatClient(_ chatClient: ChatClient, userDidGetBlocked blockInfo: BlockInfo) {
        //Block Realtime Event Received.
    }
    
    func chatClient(_ chatClient: ChatClient, userDidGetUnblocked unblockInfo: UnblockInfo) {
        // Unblock Realtime Event Received.
    }
}
```
```kotlin
sdk?.chat()?.chatRoomDelegate = object: ChatRoomDelegate() {
  override fun onBlockProfile(blockedInfo: BlockedInfo) {

  }

  override fun onUnBlockProfile(blockInfoId: String, blockProfileId: String) {

  }
}
```

<br />

## Bulk Sync Block List

`POST /api/v1/profile-blocks/bulk-sync/`

**Payload**

```
{
  "blocks": [
    {
      "blocked_by_profile_id": "<uuid>",
      "blocked_profile_id": "<uuid>"
    }
  ],
  "override": true
}

```

### Rules

* Maximum 1000 items per request (configurable)
* Both profiles must belong to same application
* Cannot block self
* if `override = true`:
  * Deletes existing block entries
  * Replaces with new list
* `override = false`:
  * Appends to existing list
