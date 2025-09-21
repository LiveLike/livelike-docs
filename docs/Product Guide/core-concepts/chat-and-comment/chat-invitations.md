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
## Chat invitations support:

1. Adding new users to chat rooms
2. Sending invitations to other users
3. Receiving invitations in real-time
4. Updating invitation status (accepted, rejected, pending)
5. Fetching lists of sent and received invitations

These APIs work across iOS, Android, and Web, with platform-specific implementations for real-time notifications.

***

## Key Workflows

### Add New User to Chat Room:

Use `addNewMemberToChatRoom` API to add other users to chat rooms.

> API details 👇

<br />

<details>
  <summary>Add New User to Chat Room</summary>

  Use `addNewMemberToChatRoom` API to add other users to chat rooms.

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
</details>

<br />
