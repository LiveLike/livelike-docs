---
title: Chat Invitations
deprecated: false
hidden: false
metadata:
  robots: index
---
Chat invitations support:

\<Tabs>
  \<Tab title="Add New User to Chat Room">
    ### Add New User to Chat Room

```
```

```
```

```
```

<br />

```
```

<br />

```
```

  \<Tab title="Invite User to Chat Room">

   ## Invite User to Chat Room

You can allow the User to invite another user to a particular chat room that they are already a part of.
You can call the `sendChatRoomInviteToUser` method which sends an invitation to the other user where the other user could decide either to `accept` or `reject` the invitation.

```
```

<br />

```
```

<br />

```
```

LiveLike.sendChatRoomInviteToProfile(\{
  roomId: roomId,
  profileId: profileId
}).then(chatRoomInvitation => console.log(chatRoomInvitation))
```

##

\</Tabs>

<br />
