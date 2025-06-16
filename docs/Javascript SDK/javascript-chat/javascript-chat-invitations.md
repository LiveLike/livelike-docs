---
title: Chat Room Invitations
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: javascript-chat-messages
      title: Chat Messages
---
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
      "code": "import { sendChatRoomInviteToProfile } from '@livelike/javascript'\n\nsendChatRoomInviteToProfile({\n roomId: \"<Room ID>\",\n profileId: \"<Profile ID>\"\n}).then(chatRoomInvitation => console.log(chatRoomInvitation))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Delete chatroom invitation"
}
[/block]
Using `deleteChatRoomInvitation` API, the user who send the invitation, have a possibility to delete it, before the invited user have responded.
[block:code]
{
  "codes": [
    {
      "code": "import { deleteChatRoomInvitation } from '@livelike/javascript'\n\ndeleteChatRoomInvitation({\n invitationId: \"<Invitation ID>\",\n}).then(res => console.log(res))",
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
You can update the status of the invitation that the User has received using updateChatRoomInviteStatus API. invitationStatus value could be "accepted" | "rejected" | "pending".
[block:code]
{
  "codes": [
    {
      "code": "import { updateChatRoomInviteStatus } from '@livelike/javascript'\n\nupdateChatRoomInviteStatus({\n  invitationId: \"<Invitation ID>\",\n  invitationStatus: \"accepted\"\n}).then(chatRoomInvitation => console.log(chatRoomInvitation))",
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
invitationStatus value could be "accepted" | "rejected" | "pending".
[block:code]
{
  "codes": [
    {
      "code": "import { getReceivedChatRoomInvitations } from '@livelike/javascript'\n\ngetReceivedChatRoomInvitations({\n  invitationStatus: \"pending\"\n}).then(paginatedInvitations => console.log(paginatedInvitations))",
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
invitationStatus value could be "accepted" | "rejected" | "pending"
[block:code]
{
  "codes": [
    {
      "code": "import { getSentChatRoomInvitations } from '@livelike/javascript'\n\ngetSentChatRoomInvitations({\n  invitationStatus: \"pending\"\n}).then(paginatedInvitations => console.log(paginatedInvitations))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Add event listener for Chat Room Invitation"
}
[/block]
Whenever a new member is invited to the Chat Room, INVITE_NEW_MEMBER event is emitted
Use this method to add event listener for the INVITE_NEW_MEMBER event.
[block:code]
{
  "codes": [
    {
      "code": "import { addChatRoomEventListener } from '@livelike/javascript'\n\nfunction onReceieveChatRoomInvitationListener(invitationEvent) {\n  console.log(invitationEvent);\n}\n\naddChatRoomEventListener(\n  ChatRoomEvent.INVITE_NEW_MEMBER,\n  onReceieveChatRoomInvitationListener\n)",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Remove event listener for Chat Room Invitation"
}
[/block]
Use this method to remove the event listener for the INVITE_NEW_MEMBER event.
[block:code]
{
  "codes": [
    {
      "code": "import { removeChatRoomEventListener } from '@livelike/javascript'\n\nremoveChatRoomEventListener(\n  ChatRoomEvent.INVITE_NEW_MEMBER,\n  onReceieveChatRoomInvitationListener\n)",
      "language": "javascript"
    }
  ]
}
[/block]