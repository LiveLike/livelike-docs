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
