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
&#x20;   \### Add New User to Chat Room

&#x20;   Use \`addNewMemberToChatRoom\` API to add other users to chat rooms.

&#x20;   \> 🚧 Please Note
&#x20;   \>
&#x20;   \> User can add another user to the chat room only if they are already a member of the chat room, use \`joinChatRoom\` API for becoming a member.

&#x20;   \`\`\`swift
&#x20;   sdk.chat.addNewMemberToChatRoom(roomId: roomId, profileId: profileId) \{&#x20;
&#x20;     \[weak self] result in
&#x20;     	DispatchQueue.main.async \{
&#x20;     		guard let self = self else \{ return }
&#x20;       	switch result \{
&#x20;       	case .success(let member):
&#x20;       		self.showAlert(title: "Now Member", message: member.url.absoluteString)
&#x20;       	case let .failure(error):
&#x20;       		self.showAlert(title: "Error", message: error.localizedDescription)
&#x20;   		}
&#x20;   	}
&#x20;   }
&#x20;   \`\`\`
&#x20;   \`\`\`kotlin
&#x20;   sdk.chat().addUserToChatRoom(chatRoomId,
&#x20;                   userId,
&#x20;                   object : LiveLikeCallback\<ChatRoomMembership>() \{
&#x20;                       override fun onResponse(result: ChatRoomMembership?, error: String?) \{
&#x20;                           result?.let \{
&#x20;                               showToast("User Added Successfully")
&#x20;                           }
&#x20;                         &#x20;
&#x20;                           error?.let \{
&#x20;                               showToast(it)
&#x20;                           }
&#x20;                         &#x20;
&#x20;                       }
&#x20;                   })
&#x20;   \`\`\`
&#x20;   \`\`\`javascript
&#x20;   LiveLike.addNewMemberToChatRoom(\{
&#x20;     roomId: "9e6f1bc4-9f02-4c57-92b7-7521d0f5b027",
&#x20;     profileId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
&#x20;   }).then(membership => console.log(membership))
&#x20;   \`\`\`
&#x20; \</Tab>

&#x20; \<Tab title="Invite User to Chat Room">
&#x20;  \## Invite User to Chat Room

You can allow the User to invite another user to a particular chat room that they are already a part of.
You can call the \`sendChatRoomInviteToUser\` method which sends an invitation to the other user where the other user could decide either to \`accept\` or \`reject\` the invitation.

\`\`\`swift
sdk.chat.sendChatRoomInviteToUser(roomId: roomId, profileId: profileId) \{&#x20;
&#x20; \[weak self] result in
&#x9;	DispatchQueue.main.async \{
&#x9;		guard let self = self else \{ return }
&#x9;		switch result \{
&#x9;		case .success(let invitation):
&#x9;			self.showAlert(title: "Invitation Sent", message: invitation.url.absoluteString)
&#x9;		case let .failure(error):
&#x9;			self.showAlert(title: "Error", message: error.localizedDescription)
&#x9;	}
&#x9;}
}
\`\`\`
\`\`\`kotlin
sdk.chat().sendChatRoomInviteToUser(
&#x20;               chatRoomId,
&#x20;               userId,
&#x20;               object : LiveLikeCallback\<ChatRoomInvitation>() \{
&#x20;                   override fun onResponse(result: ChatRoomInvitation?, error: String?) \{
&#x20;                       result?.let \{
&#x20;                           showToast("User Invited Successfully")
&#x20;                       }
&#x20;                     &#x20;
&#x20;                       error?.let \{
&#x20;                           showToast(it)
&#x20;                       }
&#x20;                      &#x20;
&#x20;                   }
&#x20;               })
\`\`\`
\`\`\`javascript
// roomId of the chatRoom to which we need to invite other profile
const roomId = "9e6f1bc4-9f02-4c57-92b7-7521d0f5b027"
// other profile id
const profileId = "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"

LiveLike.sendChatRoomInviteToProfile(\{
&#x20; roomId: roomId,
&#x20; profileId: profileId
}).then(chatRoomInvitation => console.log(chatRoomInvitation))
\`\`\`

\##

\</Tabs>

<br />
