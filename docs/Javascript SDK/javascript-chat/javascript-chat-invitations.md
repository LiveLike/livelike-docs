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
## Invite User to Chat Room

You can allow the User to invite another user to a particular chat room that they are already a part of.\
You can call the `sendChatRoomInviteToUser` method which sends an invitation to the other user where the other user could decide either to `accept` or `reject` the invitation.

```javascript
import { sendChatRoomInviteToProfile } from '@livelike/javascript'

sendChatRoomInviteToProfile({
 roomId: "<Room ID>",
 profileId: "<Profile ID>"
}).then(chatRoomInvitation => console.log(chatRoomInvitation))
```

## Delete chatroom invitation

Using `deleteChatRoomInvitation` API, the user who send the invitation, have a possibility to delete it, before the invited user have responded.

```javascript
import { deleteChatRoomInvitation } from '@livelike/javascript'

deleteChatRoomInvitation({
 invitationId: "<Invitation ID>",
}).then(res => console.log(res))
```

## Update the Invitation Status for a User

You can update the status of the invitation that the User has received using updateChatRoomInviteStatus API. invitationStatus value could be "accepted" | "rejected" | "pending".

```javascript
import { updateChatRoomInviteStatus } from '@livelike/javascript'

updateChatRoomInviteStatus({
  invitationId: "<Invitation ID>",
  invitationStatus: "accepted"
}).then(chatRoomInvitation => console.log(chatRoomInvitation))
```

## Get List of Invitations received by the current User

This API gives you list of received invitation for the current logged in user.\
invitationStatus value could be "accepted" | "rejected" | "pending".

```javascript
import { getReceivedChatRoomInvitations } from '@livelike/javascript'

getReceivedChatRoomInvitations({
  invitationStatus: "pending"
}).then(paginatedInvitations => console.log(paginatedInvitations))
```

## Get List of Invitations sent by the current User

This API gives you list of sent invitation for the current logged in user.\
invitationStatus value could be "accepted" | "rejected" | "pending"

```javascript
import { getSentChatRoomInvitations } from '@livelike/javascript'

getSentChatRoomInvitations({
  invitationStatus: "pending"
}).then(paginatedInvitations => console.log(paginatedInvitations))
```

## Add event listener for Chat Room Invitation

Whenever a new member is invited to the Chat Room, INVITE\_NEW\_MEMBER event is emitted\
Use this method to add event listener for the INVITE\_NEW\_MEMBER event.

```javascript
import { addChatRoomEventListener } from '@livelike/javascript'

function onReceieveChatRoomInvitationListener(invitationEvent) {
  console.log(invitationEvent);
}

addChatRoomEventListener(
  ChatRoomEvent.INVITE_NEW_MEMBER,
  onReceieveChatRoomInvitationListener
)
```

## Remove event listener for Chat Room Invitation

Use this method to remove the event listener for the INVITE\_NEW\_MEMBER event.

```javascript
import { removeChatRoomEventListener } from '@livelike/javascript'

removeChatRoomEventListener(
  ChatRoomEvent.INVITE_NEW_MEMBER,
  onReceieveChatRoomInvitationListener
)
```
