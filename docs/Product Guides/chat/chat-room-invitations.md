---
title: Chat Invitations
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Room Invitations | LiveLike Developer Hub
  description: >-
    Learn how to add new users to chat rooms in real time, invite users to chat
    rooms, and receive chat room invitations.
  robots: index
next:
  description: ''
---
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

## Receive notification on adding user to chat room in Real-time

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
  func chatClient(_ chatClient: ChatClient, 
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

## Invite User to Chat Room

You can allow the User to invite another user to a particular chat room that they are already a part of.\
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

## Receive Invitation in Real-time

> 📘 Platform specific implementation
>
> Implementation for receiving real time invitation is different for Web, Android and IOS.

```swift
/*
	To receive real-time notifications of the User being added a Chat Room,
	you need to implement the `ChatClientDelegate`.
	The method `userDidReceiveInvitation` returns an object of type `ChatRoomInvitation` 
	that contains all the details related to the Chat Room Invitation.
*/
class SomeViewController: UIViewController {

  var sdk: EngagementSDK
  
  override func viewDidLoad() {
    sdk.chat.delegate = self
  }
}

class SomeViewController: ChatClientDelegate {
  func chatClient(_ chatClient: ChatClient, userDidReceiveInvitation newInvitationInfo: ChatRoomInvitation) {
        self.showInviteAlert(title: "Invitation Received", 
                             message: "You've been invited to room")
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
// define a listener function to be invoked when user is invitated to some other chatroom
function onReceieveChatRoomInvitationListener(invitation){
  console.log(invitation);
}

LiveLike.addChatRoomEventListener(
  "chat-room-invite",
  onReceieveChatRoomInvitationListener
)

// to remove the attached listener function use removeUserProfileEventListener API
LiveLike.removeChatRoomEventListener(
  "chat-room-invite",
  onReceieveChatRoomInvitationListener
)
```

## Update the Invitation Status for a User

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

## Get List of Invitations received by the current User

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

## Get List of Invitations sent by the current User

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
