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
[block:api-header]
{
  "title": "Add New User to Chat Room"
}
[/block]
Use `addNewMemberToChatRoom` API to add other users to chat rooms. 
[block:callout]
{
  "type": "warning",
  "title": "Please Note",
  "body": "User can add another user to the chat room only if they are already a member of the chat room, use `joinChatRoom` API for becoming a member."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "sdk.chat.addNewMemberToChatRoom(roomId: roomId, profileId: profileId) { \n  [weak self] result in\n  \tDispatchQueue.main.async {\n  \t\tguard let self = self else { return }\n    \tswitch result {\n    \tcase .success(let member):\n    \t\tself.showAlert(title: \"Now Member\", message: member.url.absoluteString)\n    \tcase let .failure(error):\n    \t\tself.showAlert(title: \"Error\", message: error.localizedDescription)\n\t\t}\n\t}\n}",
      "language": "swift"
    },
    {
      "code": "sdk.chat().addUserToChatRoom(chatRoomId,\n                userId,\n                object : LiveLikeCallback<ChatRoomMembership>() {\n                    override fun onResponse(result: ChatRoomMembership?, error: String?) {\n                        result?.let {\n                            showToast(\"User Added Successfully\")\n                        }\n                       \n                        error?.let {\n                            showToast(it)\n                        }\n                       \n                    }\n                })",
      "language": "kotlin"
    },
    {
      "code": "LiveLike.addNewMemberToChatRoom({\n  roomId: \"9e6f1bc4-9f02-4c57-92b7-7521d0f5b027\",\n  profileId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n}).then(membership => console.log(membership))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Receive notification on adding user to chat room in Real-time"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Platform specific implementation",
  "body": "Implementation for receiving notification when user is added to chat room is different for Web, Android and IOS."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "/*\n* To receive real-time notifications of the User being added a Chat Room, \n* you need to implement the `ChatClientDelegate`.\n* The method `userDidBecomeMemberOfChatRoom` returns an object of type `NewChatMembershipInfo`\n* that contains all the details related to the Chat Room Membership.\n*/\nclass SomeViewController: UIViewController {\n\n  var sdk: EngagementSDK\n  \n  override func viewDidLoad() {\n    sdk.chat.delegate = self\n  }\n}\n\nclass SomeViewController: ChatClientDelegate {\n  func chatClient(_ chatClient: ChatClient, \n                  userDidBecomeMemberOfChatRoom newChatMembershipInfo: NewChatMembershipInfo) {\n        self.showAlert(title: \"Added to Chatroom\", message: \"You've been added to room: \\(String(describing: newChatMembershipInfo.chatRoomTitle)) by \\(newChatMembershipInfo.senderNickName)\")\n    }\n}",
      "language": "swift"
    },
    {
      "code": "sdk.chat().chatRoomDelegate =\n            object : ChatRoomDelegate() {\n                override fun onNewChatRoomAdded(chatRoomAdd: ChatRoomAdd) {\n                    \n                }\n\n                override fun onReceiveInvitation(invitation: ChatRoomInvitation) {\n                    showToast(\"Receive invitation from ${invitation.invited_by.nickname} => ${invitation.invited_by.userId}\")\n                }\n            }",
      "language": "kotlin"
    },
    {
      "code": "// define a listener function to be invoked when user is added \nfunction onNewMemberAddedToChatRoomListener(invitation){\n  console.log(invitation);\n}\n\nLiveLike.addChatRoomEventListener(\n  \"chat-room-add\",\n  onNewMemberAddedToChatRoomListener\n)\n\n// to remove the attached listener function use removeUserProfileEventListener API\nLiveLike.removeChatRoomEventListener(\n  \"chat-room-add\",\n  onNewMemberAddedToChatRoomListener\n)",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Invite User to Chat Room"
}
[/block]
You can allow the User to invite another user to a particular chat room that they are already a part of. 
You can call the `sendChatRoomInviteToUser` method which sends an invitation to the other user where the other user could decide either to `accept` or `reject` the invitation.
[block:code]
{
  "codes": [
    {
      "code": "sdk.chat.sendChatRoomInviteToUser(roomId: roomId, profileId: profileId) { \n  [weak self] result in\n\t\tDispatchQueue.main.async {\n\t\t\tguard let self = self else { return }\n\t\t\tswitch result {\n\t\t\tcase .success(let invitation):\n\t\t\t\tself.showAlert(title: \"Invitation Sent\", message: invitation.url.absoluteString)\n\t\t\tcase let .failure(error):\n\t\t\t\tself.showAlert(title: \"Error\", message: error.localizedDescription)\n\t\t}\n\t}\n}",
      "language": "swift"
    },
    {
      "code": "sdk.chat().sendChatRoomInviteToUser(\n                chatRoomId,\n                userId,\n                object : LiveLikeCallback<ChatRoomInvitation>() {\n                    override fun onResponse(result: ChatRoomInvitation?, error: String?) {\n                        result?.let {\n                            showToast(\"User Invited Successfully\")\n                        }\n                       \n                        error?.let {\n                            showToast(it)\n                        }\n                        \n                    }\n                })",
      "language": "kotlin"
    },
    {
      "code": "// roomId of the chatRoom to which we need to invite other profile\nconst roomId = \"9e6f1bc4-9f02-4c57-92b7-7521d0f5b027\"\n// other profile id\nconst profileId = \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n\nLiveLike.sendChatRoomInviteToProfile({\n  roomId: roomId,\n  profileId: profileId\n}).then(chatRoomInvitation => console.log(chatRoomInvitation))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Receive Invitation in Real-time"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Platform specific implementation",
  "body": "Implementation for receiving real time invitation is different for Web, Android and IOS."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "/*\n\tTo receive real-time notifications of the User being added a Chat Room,\n\tyou need to implement the `ChatClientDelegate`.\n\tThe method `userDidReceiveInvitation` returns an object of type `ChatRoomInvitation` \n\tthat contains all the details related to the Chat Room Invitation.\n*/\nclass SomeViewController: UIViewController {\n\n  var sdk: EngagementSDK\n  \n  override func viewDidLoad() {\n    sdk.chat.delegate = self\n  }\n}\n\nclass SomeViewController: ChatClientDelegate {\n  func chatClient(_ chatClient: ChatClient, userDidReceiveInvitation newInvitationInfo: ChatRoomInvitation) {\n        self.showInviteAlert(title: \"Invitation Received\", \n                             message: \"You've been invited to room\")\n  }\n}",
      "language": "swift"
    },
    {
      "code": "sdk.chat().chatRoomDelegate =\n            object : ChatRoomDelegate() {\n                override fun onNewChatRoomAdded(chatRoomAdd: ChatRoomAdd) {\n                    \n                }\n\n                override fun onReceiveInvitation(invitation: ChatRoomInvitation) {\n                    showToast(\"Receive invitation from ${invitation.invited_by.nickname} => ${invitation.invited_by.userId}\")\n                }\n            }",
      "language": "kotlin"
    },
    {
      "code": "// define a listener function to be invoked when user is invitated to some other chatroom\nfunction onReceieveChatRoomInvitationListener(invitation){\n  console.log(invitation);\n}\n\nLiveLike.addChatRoomEventListener(\n  \"chat-room-invite\",\n  onReceieveChatRoomInvitationListener\n)\n\n// to remove the attached listener function use removeUserProfileEventListener API\nLiveLike.removeChatRoomEventListener(\n  \"chat-room-invite\",\n  onReceieveChatRoomInvitationListener\n)",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Update the Invitation Status for a User"
}
[/block]
You can update the status of the invitation that the User has received using `updateChatRoomInviteStatus` API.
[block:code]
{
  "codes": [
    {
      "code": "/*\n\t\"updateChatRoomInviteStatus\" method which is a part of the `chat` (ChatClient) object. \n\tOn successful completion, it returns a `ChatRoomInvitation` object which contains\n\tthe details of the Invitation with its updated status. \n\n\tThe function requires the `ChatRoomInvitation` object and also a `status` of \n\ttype `ChatRoomInvitationStatus` which can be of type `accepted`, `pending` or `rejected`.\n*/\nself.sdk.chat.updateChatRoomInviteStatus(\n  chatRoomInvitation: invitation,\n  invitationStatus: .accepted\n) { \n  result in\n\tswitch result {\n\t\tcase .success(let invitation):\n\t\t\tself.showAlert(title: \"Invitation Accepted\", message: \"\")\n\t\tcase .failure(let error):\n\t\t\tself.showAlert(title: \"Failed to Accept\", message: error.localizedDescription)\n\t}\n}",
      "language": "swift"
    },
    {
      "code": "sdk.chat().updateChatRoomInviteStatus(\n            chatRoomInvitation,\n            ChatRoomInvitationStatus.ACCEPTED,\n            object : LiveLikeCallback<ChatRoomInvitation>() {\n                override fun onResponse(result: ChatRoomInvitation?, error: String?) {\n                    result?.let {\n                        showToast(\"Status: ${it.status}\")\n                    }\n                    error?.let {\n                        showToast(it)\n                    }\n                \n                }\n            })",
      "language": "kotlin"
    },
    {
      "code": "// invitationStatus value could be \"accepted\" | \"rejected\" | \"pending\"\nLiveLike.updateChatRoomInviteStatus({\n  invitationId: \"28cc0ceb-8934-48cd-abc5-4d3a3a681c1b\",\n\tinvitationStatus: \"accepted\"\n}).then(chatRoomInvitation => console.log(chatRoomInvitation))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get List of Invitations received by the current User"
}
[/block]
This API gives you list of received invitation for the current logged in user.
[block:code]
{
  "codes": [
    {
      "code": "/*\n\tYou can call the `getInvitationsForUserWithInvitationStatus` method \n\twhich is a part of the `chat` (ChatClient) object to get a paginated list \n\tof the Invitations that the user has received to join Chat Rooms.\n\n\tThe function also requires a `ChatRoomInvitationStatus` object to filter \n\tthe list of invitations based on type of status.\n*/\nsdk.chat.getInvitationsForUserWithInvitationStatus(\n            invitationStatus: .pending,\n            page: .first\n        ) { result in\n            switch result {\n            case .success(let chatRoomInvitations):\n                self.showAlert(title: \"Chat Room Invitations Recieved\", message: \"No: \\(chatRoomInvitations.count)\")\n            case .failure(let error):\n                print(error.localizedDescription)\n\t}\n}",
      "language": "swift"
    },
    {
      "code": "sdk.chat().getInvitationsForCurrentProfileWithInvitationStatus(\n            pagination,\n            ChatRoomInvitationStatus.PENDING,\n            object : LiveLikeCallback<List<ChatRoomInvitation>>() {\n                override fun onResponse(result: List<ChatRoomInvitation>?, error: String?) {\n                    result?.let {\n                       \n                    }\n                    error?.let {\n                        showToast(it)\n                    }\n                    \n                }\n            })",
      "language": "kotlin"
    },
    {
      "code": "// invitationStatus value could be \"accepted\" | \"rejected\" | \"pending\"\nLiveLike.getReceivedChatRoomInvitations({\n  invitationStatus: \"pending\"\n}).then(paginatedInvitations => console.log(paginatedInvitations))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get List of Invitations sent by the current User"
}
[/block]
This API gives you list of sent invitation for the current logged in user.
[block:code]
{
  "codes": [
    {
      "code": "/*\n\tYou can call the `getInvitationsByUserWithInvitationStatus` method which\n\tis a part of the `chat` (ChatClient) object to get a paginated list of the Invitations\n\tthat the user has sent to join Chat Rooms.\n\n\tThe function also requires a `ChatRoomInvitationStatus` object \n\tto filter the list of invitations based on type of status.\n*/\nsdk.chat.getInvitationsByUserWithInvitationStatus(\n            invitationStatus: .pending,\n            page: .first\n        ) { result in\n            switch result {\n            case .success(let chatRoomInvitations):\n                self.showAlert(title: \"Chat Room Invitations Sent\", message: \"No: \\(chatRoomInvitations.count)\")\n            case .failure(let error):\n                print(error.localizedDescription)\n\t}\n}",
      "language": "swift"
    },
    {
      "code": "sdk.chat().getInvitationsByCurrentProfileWithInvitationStatus(\n                LiveLikePagination.FIRST,\n                ChatRoomInvitationStatus.PENDING,\n                object : LiveLikeCallback<List<ChatRoomInvitation>>() {\n                    override fun onResponse(result: List<ChatRoomInvitation>?, error: String?) {\n                        result?.let {\n                           \n                        }\n                        error?.let {\n                            showToast(it)\n                        }\n                        \n                    }\n                })",
      "language": "kotlin"
    },
    {
      "code": "// invitationStatus value could be \"accepted\" | \"rejected\" | \"pending\"\nLiveLike.getSentChatRoomInvitations({\n  invitationStatus: \"pending\"\n}).then(paginatedInvitations => console.log(paginatedInvitations))",
      "language": "javascript"
    }
  ]
}
[/block]