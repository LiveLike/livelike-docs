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

### Add New User to Chat Room

> 🚧 Please Note
>
> User can add another user to the chat room only if they are already a member of the chat room, use `joinChatRoom` API for becoming a member.

\<API>
&#x20; \<summary> Add New User to Chat Room \</summary>
&#x20; Use \`addNewMemberToChatRoom\` API to add other users to chat rooms.

&#x20; \`\`\`swift
&#x20; sdk.chat.addNewMemberToChatRoom(roomId: roomId, profileId: profileId) \{&#x20;
&#x20;   \[weak self] result in
&#x20;   	DispatchQueue.main.async \{
&#x20;   		guard let self = self else \{ return }
&#x20;     	switch result \{
&#x20;     	case .success(let member):
&#x20;     		self.showAlert(title: "Now Member", message: member.url.absoluteString)
&#x20;     	case let .failure(error):
&#x20;     		self.showAlert(title: "Error", message: error.localizedDescription)
&#x20; 		}
&#x20; 	}
&#x20; }
&#x20; \`\`\`
&#x20; \`\`\`kotlin
&#x20; sdk.chat().addUserToChatRoom(chatRoomId,
&#x20;                 userId,
&#x20;                 object : LiveLikeCallback\<ChatRoomMembership>() \{
&#x20;                     override fun onResponse(result: ChatRoomMembership?, error: String?) \{
&#x20;                         result?.let \{
&#x20;                             showToast("User Added Successfully")
&#x20;                         }
&#x20;                       &#x20;
&#x20;                         error?.let \{
&#x20;                             showToast(it)
&#x20;                         }
&#x20;                       &#x20;
&#x20;                     }
&#x20;                 })
&#x20; \`\`\`
&#x20; \`\`\`javascript
&#x20; LiveLike.addNewMemberToChatRoom(\{
&#x20;   roomId: "9e6f1bc4-9f02-4c57-92b7-7521d0f5b027",
&#x20;   profileId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
&#x20; }).then(membership => console.log(membership))
&#x20; \`\`\`
\</details>

***

### Invite User to Chat Room

<br />

<br />

***

### Receive Invitation in Real-time

> 📘 Platform specific implementation
>
> Implementation for receiving real time invitation is different for Web, Android and IOS

<br />

### Receive notification on adding user to chat room in Real-time

> 📘 Platform specific implementation
>
> Implementation for receiving notification when user is added to chat room is different for Web, Android and IOS.

```swift
/*
* To receive real-time notifications of the User being added a Chat Room, 
* you need to implement the `ChatClientDelegate`.
* The method `userDidBecomeMemberOfChatRoom` returns an object of type `NewChatMembershipInfo`
* that contains all the details related to the Chat Room Membership.
*/
class SomeViewController: UIViewController {

  var sdk: EngagementSDK
  
  override func viewDidLoad() {
    sdk.chat.delegate = self
  }
}

class SomeViewController: ChatClientDelegate {
  func chatClient(_ chatClient: ChatClient,\
                  userDidBecomeMemberOfChatRoom newChatMembershipInfo: NewChatMembershipInfo) {
        self.showAlert(title: "Added to Chatroom", message: "You've been added to room: \(String(describing: newChatMembershipInfo.chatRoomTitle)) by \(newChatMembershipInfo.senderNickName)")
    }
}
```
```kotlin
sdk.chat().chatRoomDelegate =
            object : ChatRoomDelegate() {
                override fun onNewChatRoomAdded(chatRoomAdd: ChatRoomAdd) {
                    
                }

                override fun onReceiveInvitation(invitation: ChatRoomInvitation) {
                    showToast("Receive invitation from ${invitation.invited_by.nickname} => ${invitation.invited_by.userId}")
                }
            }
```
```javascript
// define a listener function to be invoked when user is added 
function onNewMemberAddedToChatRoomListener(invitation){
  console.log(invitation);
}

LiveLike.addChatRoomEventListener(
  "chat-room-add",
  onNewMemberAddedToChatRoomListener
)

// to remove the attached listener function use removeUserProfileEventListener API
LiveLike.removeChatRoomEventListener(
  "chat-room-add",
  onNewMemberAddedToChatRoomListener
)
```

***

### Update the Invitation Status for a User

You can update the status of the invitation that the User has received using `updateChatRoomInviteStatus` API.

```swift
/*
	"updateChatRoomInviteStatus" method which is a part of the `chat` (ChatClient) object. 
	On successful completion, it returns a `ChatRoomInvitation` object which contains
	the details of the Invitation with its updated status. 

	The function requires the `ChatRoomInvitation` object and also a `status` of 
	type `ChatRoomInvitationStatus` which can be of type `accepted`, `pending` or `rejected`.
*/
self.sdk.chat.updateChatRoomInviteStatus(
  chatRoomInvitation: invitation,
  invitationStatus: .accepted
) { 
  result in
	switch result {
		case .success(let invitation):
			self.showAlert(title: "Invitation Accepted", message: "")
		case .failure(let error):
			self.showAlert(title: "Failed to Accept", message: error.localizedDescription)
	}
}
```
```kotlin
sdk.chat().updateChatRoomInviteStatus(
            chatRoomInvitation,
            ChatRoomInvitationStatus.ACCEPTED,
            object : LiveLikeCallback<ChatRoomInvitation>() {
                override fun onResponse(result: ChatRoomInvitation?, error: String?) {
                    result?.let {
                        showToast("Status: ${it.status}")
                    }
                    error?.let {
                        showToast(it)
                    }
                
                }
            })
```
```javascript
// invitationStatus value could be "accepted" | "rejected" | "pending"
LiveLike.updateChatRoomInviteStatus({
  invitationId: "28cc0ceb-8934-48cd-abc5-4d3a3a681c1b",
	invitationStatus: "accepted"
}).then(chatRoomInvitation => console.log(chatRoomInvitation))
```

***

### Get List of Invitations received by the current User

This API gives you list of received invitation for the current logged in user.

```swift
/*
	You can call the `getInvitationsForUserWithInvitationStatus` method 
	which is a part of the `chat` (ChatClient) object to get a paginated list 
	of the Invitations that the user has received to join Chat Rooms.

	The function also requires a `ChatRoomInvitationStatus` object to filter 
	the list of invitations based on type of status.
*/
sdk.chat.getInvitationsForUserWithInvitationStatus(
            invitationStatus: .pending,
            page: .first
        ) { result in
            switch result {
            case .success(let chatRoomInvitations):
                self.showAlert(title: "Chat Room Invitations Recieved", message: "No: \(chatRoomInvitations.count)")
            case .failure(let error):
                print(error.localizedDescription)
	}
}
```
```kotlin
sdk.chat().getInvitationsForCurrentProfileWithInvitationStatus(
            pagination,
            ChatRoomInvitationStatus.PENDING,
            object : LiveLikeCallback<List<ChatRoomInvitation>>() {
                override fun onResponse(result: List<ChatRoomInvitation>?, error: String?) {
                    result?.let {
                       
                    }
                    error?.let {
                        showToast(it)
                    }
                    
                }
            })
```
```javascript
// invitationStatus value could be "accepted" | "rejected" | "pending"
LiveLike.getReceivedChatRoomInvitations({
  invitationStatus: "pending"
}).then(paginatedInvitations => console.log(paginatedInvitations))
```

### Get List of Invitations sent by the current User

This API gives you list of sent invitation for the current logged in user.

```swift
/*
	You can call the `getInvitationsByUserWithInvitationStatus` method which
	is a part of the `chat` (ChatClient) object to get a paginated list of the Invitations
	that the user has sent to join Chat Rooms.

	The function also requires a `ChatRoomInvitationStatus` object 
	to filter the list of invitations based on type of status.
*/
sdk.chat.getInvitationsByUserWithInvitationStatus(
            invitationStatus: .pending,
            page: .first
        ) { result in
            switch result {
            case .success(let chatRoomInvitations):
                self.showAlert(title: "Chat Room Invitations Sent", message: "No: \(chatRoomInvitations.count)")
            case .failure(let error):
                print(error.localizedDescription)
	}
}
```
```kotlin
sdk.chat().getInvitationsByCurrentProfileWithInvitationStatus(
                LiveLikePagination.FIRST,
                ChatRoomInvitationStatus.PENDING,
                object : LiveLikeCallback<List<ChatRoomInvitation>>() {
                    override fun onResponse(result: List<ChatRoomInvitation>?, error: String?) {
                        result?.let {
                           
                        }
                        error?.let {
                            showToast(it)
                        }
                        
                    }
                })
```
```javascript
// invitationStatus value could be "accepted" | "rejected" | "pending"
LiveLike.getSentChatRoomInvitations({
  invitationStatus: "pending"
}).then(paginatedInvitations => console.log(paginatedInvitations))
```
