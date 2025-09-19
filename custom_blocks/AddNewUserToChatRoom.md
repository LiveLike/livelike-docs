---
name: AddNewUserToChatRoom
---
<br />

## Add New User to Chat Room

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
