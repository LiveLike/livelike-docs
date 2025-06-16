---
title: Chat Client
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Client | iOS SDK | LiveLike Developer Hub | Engagement Suite
  description: >-
    A Chat Client is an interface that can be used to add or invite other users
    to a chat room. Learn more about iOS Chat Clients.
  robots: index
next:
  description: ''
---
A Chat Client is an interface that can be used to add or invite other users to a chat room.

** Features **

- Add User to a Chat Room
- Invite User to a Chat Room
- Respond to invitations
- Get List of Invitations corresponding to the User

## Add User to Chat Room

As an integrator you can enable the current user to add users to chat rooms of which the current user is a member of. 

You can call the `addMemberToChatRoom` method which is a part of the `chat` (ChatClient) object.  
On successful completion, it returns a `ChatRoomMember` object which contains the details of the User and Chat Room they were added to

> 📘 Please Note
> 
> User can add another user to the chat room only if they are already a member of the chat room

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



## Receive notification for added user in Real-time

To receive real-time notifications of the User being added a Chat Room, you need to implement the `ChatClientDelegate`. The method `userDidBecomeMemberOfChatRoom` returns an object of type `NewChatMembershipInfo` that contains all the details related to the Chat Room Membership.

```swift
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



## Invite User to Chat Room

You can allow the User to invite another user to a particular chat room that they are already a part of. 

You can call the `sendChatRoomInviteToUser` method which is a part of the `chat` (ChatClient) object.  
On successful completion, it returns a `ChatRoomInvitation` object which contains the details of the the Invitation.

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



## Receive Invitation in Real-time

To receive real-time notifications of the User being added a Chat Room, you need to implement the `ChatClientDelegate`. The method `userDidReceiveInvitation` returns an object of type `ChatRoomInvitation` that contains all the details related to the Chat Room Invitation.

```swift
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



## Update the Invitation Status for a User

You can update the status of the invitation that the User has received.

You can call the `updateChatRoomInviteStatus` method which is a part of the `chat` (ChatClient) object.  
On successful completion, it returns a `ChatRoomInvitation` object which contains the details of the Invitation with its updated status. 

The function requires the `ChatRoomInvitation` object and also a `status` of type `ChatRoomInvitationStatus` which can be of type `accepted`, `pending` or `rejected`.

```swift
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



## Get List of Invitations received by the User

You can call the `getInvitationsForUserWithInvitationStatus` method which is a part of the `chat` (ChatClient) object to get a paginated list of the Invitations that the user has received to join Chat Rooms.

The function also requires a `ChatRoomInvitationStatus` object to filter the list of invitations based on type of status.

```swift
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



## Get List of Invitations sent by the User

You can call the `getInvitationsByUserWithInvitationStatus` method which is a part of the `chat` (ChatClient) object to get a paginated list of the Invitations that the user has sent to join Chat Rooms.

The function also requires a `ChatRoomInvitationStatus` object to filter the list of invitations based on type of status.

```swift
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