---
title: Chat Room Memberships (Web)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Once a profile joins a room, they are a member of that room until they leave it. Joining a room is useful because the list of room memberships can be maintained per-user and looked up across sessions and devices.

A user does not have to be a member of a room to enter it and send messages.

> 📘 Use of chatroom memberships?
> 
> Use memberships to keep track of users in a given room, to identify common chatroom between list of user profiles etc.

## Get chatroom memberships for the current user

Use `getProfileChatRoomMemberships` API to get list of chat room memberships the current profile is member of. This returns a Promise that resolves a list of all memberships present for the current user.

```javascript Web
LiveLike.getProfileChatRoomMemberships()
.then(res => console.log(res.results))
```

## Get common chatroom between mulitple users

Pass profileIds argument property to`getProfileChatRoomMemberships` API for getting list of chat room memberships that reflects common chatroom between the provided profileIds.

```javascript Web
// This gives memberships for a chat rooms
// where profile-id-1, profile-id-2 and profile-id-3 are already a member
// useful for finding common chat room between list of users
LiveLike.getProfileChatRoomMemberships({
  profileIds: ["<profile-id-1>", "<profile-id-2>", "<profile-id-3>"]
}).then(res => console.log(res.results))
```

## Get chatroom memberships for a given chat room

Returns a Promise that resolves a list of all memberships present on a given chat room.

```javascript Web
LiveLike.getChatRoomMemberships({
  roomId: "<Chat Room ID>"
}).then(res => console.log(res.results))
```

## Join a chat room

Adds a membership for the current user for the chat room that is supplied by the room id argument. Returns a Promise that resolves the membership info object.

```javascript Web
LiveLike.joinChatRoom({roomId: "<Chat Room ID>"})
  .then(membership => console.log(membership))
```

## Leave a chat room

Removes the current user's membership from the chat room that is supplied by the room id argument. Resolves a Boolean.

```javascript Web
LiveLike.leaveChatRoom({roomId: "<Chat Room ID>"})
  .then(success => console.log(success))
```

## Add new member to chat room

Use this method to add other users to chat rooms.  
The method takes an object argument with a chat room id string as a `roomId` property,  
an object argument with a user profile id string as a `profileId` property.

> 🚧 Please note
> 
> User can add another user to the chat room only if they are already a member of the chat room, use `joinChatRoom` API for becoming a member.

```javascript Web
LiveLike.addNewMemberToChatRoom({
  roomId: "<Chat Room ID>",
  profileId: "<Profile ID>"
}).then(membership => console.log(membership))
```

## Add event listener for Chat Room Membership

Whenever a new member is added to the Chat Room, ADD_NEW_MEMBER event is emitted  
Use this method to add event listener for the ADD_NEW_MEMBER event

```javascript Web
function onReceieveNewMemberListener(newMemberEvent) {
  console.log(newMemberEvent);
}

LiveLike.addChatRoomEventListener(
  ChatRoomEvent.ADD_NEW_MEMBER,
  onReceieveNewMemberListener,
})
```

## Remove event listener for Chat Room Membership

Use this method to remove the event listener for the ADD_NEW_MEMBER event

```javascript Web
LiveLike.removeChatRoomEventListener(
  ChatRoomEvent.ADD_NEW_MEMBER,
  onReceieveNewMemberListener,
})
```