---
title: Chat Invitations
deprecated: false
hidden: false
metadata:
  robots: index
---
Chat invitations support:

\<Tabs>
&#x20; \<Tab title="Add New User to Chat Room">


<br />

  ## Add New User to Chat Room

<br />

  Use `addNewMemberToChatRoom` API to add other users to chat rooms.

<br />

<Callout icon="📘" theme="info">
  Users can add another user only if they are already a member of the chat room. Use `joinChatRoom` to become a member first.
</Callout>

  **Example (Swift):**
  ```swift
  sdk.chat.addNewMemberToChatRoom(roomId: roomId, profileId: profileId) { result in
      DispatchQueue.main.async {
          switch result {
          case .success(let member):
              print("Now Member: \(member.url.absoluteString)")
          case .failure(let error):
              print("Error: \(error.localizedDescription)")
          }
      }
  }

Real-time Notification:
Implement ChatClientDelegate to receive notifications when a user is added:

func chatClient(_ chatClient: ChatClient, userDidBecomeMemberOfChatRoom newChatMembershipInfo: NewChatMembershipInfo) {
    print("Added to room: \(newChatMembershipInfo.chatRoomTitle) by \(newChatMembershipInfo.senderNickName)")
}

</Tab> <Tab title="Send Invitation to User"> ## Invite User to Chat Room

Use sendChatRoomInviteToUser to allow a user to invite another to a room they are already part of. The invitee can accept or reject.

Example (Swift):
sdk.chat.sendChatRoomInviteToUser(roomId: roomId, profileId: profileId) { result in
    DispatchQueue.main.async {
        switch result {
        case .success(let invitation):
            print("Invitation Sent: \(invitation.url.absoluteString)")
        case .failure(let error):
            print("Error: \(error.localizedDescription)")
        }
    }
}
</Tab> <Tab title="Receive Invitation in Real-Time"> ## Receive Invitation in Real-Time
Implement ChatClientDelegate to get notified when a user receives an invitation.
Example (Swift):
func chatClient(_ chatClient: ChatClient, userDidReceiveInvitation newInvitationInfo: ChatRoomInvitation) {
    print("You've been invited to room: \(newInvitationInfo.chatRoomTitle)")
}
</Tab> <Tab title="Update Invitation Status"> ## Update Invitation Status
Use updateChatRoomInviteStatus to accept, reject, or mark an invitation as pending.
Example (Swift):
sdk.chat.updateChatRoomInviteStatus(chatRoomInvitation: invitation, invitationStatus: .accepted) { result in
    switch result {
    case .success(let updatedInvitation):
        print("Invitation Accepted")
    case .failure(let error):
        print("Failed: \(error.localizedDescription)")
    }
}
</Tab> <Tab title="List Received Invitations"> ## Get Received Invitations
Use getInvitationsForUserWithInvitationStatus to fetch invitations received by the current user.
Example (Swift):
sdk.chat.getInvitationsForUserWithInvitationStatus(invitationStatus: .pending, page: .first) { result in
    switch result {
    case .success(let invitations):
        print("Received Invitations: \(invitations.count)")
    case .failure(let error):
        print(error.localizedDescription)
    }
}
</Tab> <Tab title="List Sent Invitations"> ## Get Sent Invitations
Use getInvitationsByUserWithInvitationStatus to fetch invitations sent by the current user.
Example (Swift):
sdk.chat.getInvitationsByUserWithInvitationStatus(invitationStatus: .pending, page: .first) { result in
    switch result {
    case .success(let invitations):
        print("Sent Invitations: \(invitations.count)")
    case .failure(let error):
        print(error.localizedDescription)
    }
}
</Tab> </Tabs> ```
