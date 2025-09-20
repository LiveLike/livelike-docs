---
title: Chat Invitations
excerpt: >-
  The Chat Invitations feature allows users to invite others to join chat rooms,
  accept or reject invitations, and manage membership. This system enables both
  public and private interactions, giving flexibility for event-based and
  persistent chat experiences.
deprecated: false
hidden: false
metadata:
  robots: index
---
Overview

## Chat invitations support:

* Adding new users to chat rooms
* Sending invitations to other users
* Receiving invitations in real-time
* Updating invitation status (accepted, rejected, pending)
* Fetching lists of sent and received invitations

These APIs work across iOS, Android, and Web, with platform-specific implementations for real-time notifications.

> dwedwe
>
> we

## Key Workflows

### Add New User to Chat Room

Use `addNewMemberToChatRoom` API to add other users to chat rooms.

> 🚧 Please Note
>
> User can add another user to the chat room only if they are already a member of the chat room, use `joinChatRoom` API for becoming a member.

```swift
sdk.chat.addNewMemberToChatRoom(roomId: roomId, profileId: profileId) { 
  [weak self] result in
  	DispatchQueue.main.async {
  		guard let self = self else { return }
    	switch result {
    	case .success(let member):
    		self.showAlert(title: "Now Member", message: member.url.absoluteString)
    	case let .failure(error):
    		self.showAlert(title: "Error", message: error.localizedDescription)
		}
	}
}
```
```kotlin
sdk.chat().addUserToChatRoom(chatRoomId,
                userId,
                object : LiveLikeCallback<ChatRoomMembership>() {
                    override fun onResponse(result: ChatRoomMembership?, error: String?) {
                        result?.let {
                            showToast("User Added Successfully")
                        }
                       
                        error?.let {
                            showToast(it)
                        }
                       
                    }
                })
```
```javascript
LiveLike.addNewMemberToChatRoom({
  roomId: "9e6f1bc4-9f02-4c57-92b7-7521d0f5b027",
  profileId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
}).then(membership => console.log(membership))
```

<br />

### Invite User to Chat Room

You can allow the User to invite another user to a particular chat room that they are already a part of.
You can call the `sendChatRoomInviteToUser` method which sends an invitation to the other user where the other user could decide either to `accept` or `reject` the invitation.

```swift
sdk.chat.sendChatRoomInviteToUser(roomId: roomId, profileId: profileId) { 
  [weak self] result in
		DispatchQueue.main.async {
			guard let self = self else { return }
			switch result {
			case .success(let invitation):
				self.showAlert(title: "Invitation Sent", message: invitation.url.absoluteString)
			case let .failure(error):
				self.showAlert(title: "Error", message: error.localizedDescription)
		}
	}
}
```
```kotlin
sdk.chat().sendChatRoomInviteToUser(
                chatRoomId,
                userId,
                object : LiveLikeCallback<ChatRoomInvitation>() {
                    override fun onResponse(result: ChatRoomInvitation?, error: String?) {
                        result?.let {
                            showToast("User Invited Successfully")
                        }
                       
                        error?.let {
                            showToast(it)
                        }
                        
                    }
                })
```
```javascript
// roomId of the chatRoom to which we need to invite other profile
const roomId = "9e6f1bc4-9f02-4c57-92b7-7521d0f5b027"
// other profile id
const profileId = "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"

LiveLike.sendChatRoomInviteToProfile({
  roomId: roomId,
  profileId: profileId
}).then(chatRoomInvitation => console.log(chatRoomInvitation))
```

##

<br />
