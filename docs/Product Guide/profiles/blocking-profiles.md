---
title: Blocking Profiles
deprecated: false
hidden: false
metadata:
  robots: index
---
Sometimes users are not comfortable, or are being harassed by another user. In order to help users to keep themselves safe, they can block others from engaging with them in certain ways.

## How Blocks Work

When someone blocks someone else, they prevent the blocked person from actively engaging with them. Protections against active engagements are enforced at the system level, from the API layer upwards. Once a bock is in place, it prevents the blocked user from:

* inviting them to chat rooms.
* adding them to chat rooms.
* mentioning them in chat messages.
* directly replying to their comments.
* commenting on boards they own, and vice versa.
* mentioning them in comments.
* creating social graph relationships with them.

Blocks do not prevent passive engagement at the system level. For example, API responses will include content from others that may be blocked by the current user. Content filtering can be applied at the integration level, and the stock user interface implementations bundled with the SDKs include some basic functionality:

* Chat messages sent from blocked users are not shown.
* Comments authored by blocked users are not shown.

<Callout icon="📘" theme="info">
  Social features integrated via API have to implement content filtering at the integration level. Active engagement between users are prevented at the system level, but passive engagement is not.
</Callout>

## Creating a Block

As an integrator, you can now allow users to block other users from sending invitations or adding them to chat rooms.

> API Details
>
> <br />
>
> <details>
>   <summary>Creating a Block</summary>
>
>   ```swift
>   /*
>   To enable the user to block other users, you can implement the `blockProfile` method which is
>   a part of the `ChatClient`. It accepts a parameter `profileID` which corresponds to the id 
>   of the profile to be blocked.
>
>   On successful completion, the method returns an object of type `BlockInfo` which contains 
>   details of the profile blocked and the profile it was blocked by.
>   */
>
>   sdk.chat.blockProfile(
>   		profileID: profileID
>   ) { result in
>      	switch result {
>       case .success(let blockedProfile):
>            self.showAlert(
>               title: "Profile Blocked",
>            		message: "Id:\(blockedProfile.blockedProfileID)"
>            )
>       case .failure(let error):
>       		self.showAlert(title: "Error", message: error.localizedDescription)
>   		}
>   }
>   ```
>   ```kotlin
>   sdk.blockProfile(
>     profileId,
>     object: LiveLikeCallback < BlockedData > () {
>       override fun onResponse(result: BlockedData ? , error : String ? ) {
>         result?.let {
>           showToast("BLocked User: ${it.blockedProfileID}, BlockID: ${it.id}")
>         }
>         error?.let {
>           it1 -> showToast(it1)
>         }
>       }
>     }
>   )
>   ```
>   ```javascript
>   LiveLike.blockProfile({
>       profileId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
>   })
>   .then(blockInfo => console.log(blockInfo))
>   ```
> </details>

## Removing a Block

As an integrator, you can now allow users to unblock users they had previously blocked from sending invitations or adding them to chat rooms.

> API Details
>
> <details>
>   <summary>Removing a Block</summary>
>
>   ```swift
>   /*
>   To enable the user to unblock other users, you can implement the `unblockProfile` method 
>   which is a part of the `ChatClient`. It accepts one parameter: `blockRequestID` which 
>   corresponds to the id of the  `BlockInfo` for the blocked profile.
>   */
>
>   sdk.chat.unblockProfile(blockRequestID: requestID) { result in
>   		switch result {
>       case .success(_):
>       		break
>       case .failure(let error):
>       		self.showAlert(title: "Error", message: error.localizedDescription)
>   		}
>   }
>   ```
>   ```kotlin
>   sdk.unBlockProfile(blockID,
>     object: LiveLikeCallback < LiveLikeEmptyResponse > () {
>       override fun onResponse(result: LiveLikeEmptyResponse ? , error : String ? ) {
>         error?.let {
>           showToast(it)
>         }
>         result?.let {
>           showToast("Success Unblock")
>         }
>       }
>     }
>   )
>   ```
>   ```javascript
>   // blockId is the id of the blockInfo for a given blocked profile,
>   // could be fetched from `getBlockInfoList` or `getProfileBlockInfo`
>   LiveLike.unblockProfile({
>       blockId: "c327a72c-94e5-4f5a-bcef-16ee84d35077"
>    })
>   .then(response => console.log(response))
>   ```
> </details>

<br />

## Getting a list of Blocks

As an integrator, you can show the user a list of all the profiles blocked by the user.

> API Details
>
> <br />
>
> <details>
>   <summary>Getting a List of Blocks</summary>
>
>   ```swift
>   /*
>   To display the list, you can implement the `getBlockedProfileList` method which is a part
>   of the `ChatClient`. The method accepts a parameter `profileID` which corresponds to the id of the 
>   profile blocked which can be used as a filter for the 
>   request and is `optional`.
>
>   On successful completion, the method returns a paginated list of type `BlockInfo` which 
>   contains details of the profile blocked and the profile it was blocked by.
>   */
>
>   sdk.chat.getBlockedProfileList(
>   		blockedProfileID: profileID, 
>   		page: .first
>   ) { result in
>               switch result {
>   		case .success(let blockedProfiles):
>   				if blockedProfiles.count >= 1 {
>   						self.showAlert(
>               		title: "No. of Profiles:",
>                   message: "\(blockedProfiles.count)"
>           		)
>       		}
>   		case .failure(let error):
>       		print(error.localizedDescription)
>   		}
>   }
>   ```
>   ```kotlin
>   sdk.getBlockedProfileList(LiveLikePagination.FIRST,
>     blockedProfileId, // send it as null if you want to fetch all block profile
>     object: LiveLikeCallback < List < BlockedData >> () {
>       override fun onResponse(result: List < BlockedData > ? , error : String ? ) {
>         error?.let {
>           it1 -> showToast(it1)
>         }
>         result?.let {
>           //block profile list  
>         }
>       }
>     }
>   )
>   ```
>   ```javascript
>   LiveLike.getBlockInfoList()
>   .then(paginatedBlockInfo => console.log(paginatedBlockInfo))
>   ```
> </details>

<br />

## Getting block profile info

Use `getProfileBlockInfo` to get block information for a particular profile Id.

> API Details
>
> <details>
>   <summary>Getting block profile info</summary>
>
>   ```javascript
>   LiveLike.getProfileBlockInfo({
>       profileId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
>   })
>   .then(blockInfo => console.log(blockInfo))
>   ```
>   ```swift
>   sdk.chat.getProfileBlockInfo(profileID: profileID) { result in
>   	switch result {
>     	case .success(let blockInfo):
>       	// Success Block
>       case .failure(let error):
>       	print(error.localizedDescription)
>   	}
>   }
>   ```
>   ```kotlin Kotlin
>   sdk.chat().getProfileBlockInfo(<profileId>,object : LiveLikeCallback<BlockedInfo>() {
>           override fun onResponse(result:BlockedInfo?,error: String?) {
>   //receive result or error
>   })
>   ```
> </details>

<br />

## Real time block/unblock profile events

You can add listeners/delegators for getting real time block/unblock profile events

> 📘 Platform specific implementation
>
> Implementation for receiving real time events is different for Web, Android and IOS.

> API Details
>
> \<details>
> \<summary>Real time block/unblock profile events
> \</summary>
>
> \`\`\` javascript
> // For adding block profile event listener
> function onBlockProfileListener(blockInfo)\{
> &#x20;   console.log(blockInfo);
> }
>
> // When user is blocked, attach listener fn to be called&#x20;
> LiveLike.addUserProfileEventListener(
> &#x20;   LiveLike.UserProfileEvent.BLOCK\_PROFILE,
> &#x20;   onBlockProfileListener
> )
>
> // to remove block profile event listener
> LiveLike.removeUserProfileEventListener(
> &#x20;   LiveLike.UserProfileEvent.BLOCK\_PROFILE,
> &#x20;   onBlockProfileListener
> );
>
>
> // For adding unblock profile event listener
> function onUnblockProfileListener(blockInfo)\{
> &#x20;   console.log(blockInfo);
> }
>
> // When user is Unblocked, attach listener fn to be called&#x20;
> LiveLike.addUserProfileEventListener(
> &#x20;   LiveLike.UserProfileEvent.UNBLOCK\_PROFILE,
> &#x20;   onUnblockProfileListener
> )
>
> // to remove unblock profile event listener
> LiveLike.removeUserProfileEventListener(
> &#x20;   LiveLike.UserProfileEvent.UNBLOCK\_PROFILE,
> &#x20;   onUnblockProfileListener
> );
> \`\`\`
> \`\`\`swift
> //To receive realtime events for blocking or unblocking a profile.
> //The respective ViewController should confirm to ChatClientDelegate.
>
> class SomeClass: UIViewController \{
> &#x20; override func viewDidLoad() \{
> &#x20;   super.viewDidLoad()
> &#x20;   sdk.chat.delegate = self
> &#x20; }
> }
>
> extension SomeClass: ChatClientDelegate \{
> &#x20;   func chatClient(\_ chatClient: ChatClient, userDidGetBlocked blockInfo: BlockInfo) \{
> &#x20;       //Block Realtime Event Received.
> &#x20;   }
> &#x20;  &#x20;
> &#x20;   func chatClient(\_ chatClient: ChatClient, userDidGetUnblocked unblockInfo: UnblockInfo) \{
> &#x20;       // Unblock Realtime Event Received.
> &#x20;   }
> }
> \`\`\`
> \`\`\`kotlin
> sdk?.chat()?.chatRoomDelegate = object: ChatRoomDelegate() \{
> &#x20; override fun onBlockProfile(blockedInfo: BlockedInfo) \{
>
> &#x20; }
>
> &#x20; override fun onUnBlockProfile(blockInfoId: String, blockProfileId: String) \{
>
> &#x20; }
> }
> \`\`\`
>
> \</details>
>
