---
title: Chat Room Membership
excerpt: Tracking and counting members of chat rooms
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: ios-chat-room-membership
      title: Chat Room Membership (iOS)
    - type: basic
      slug: web-chat-room-memberships
      title: Chat Room Memberships (Web)
    - type: basic
      slug: javascript-chat-room-memberships
      title: Chat Room Memberships (JavaScript)
---
Use Chat Room Memberships to track which users are permanent members of rooms, even when they're offline. That way users can leave the app, come back later, and still be a part of the same rooms that they were before. Being a member of a room is separate from being _present_ in a room, which tracks whether or not someone is online.

Once someone _joins_ a room, they are a member of that room until they _leave_ it. Joining a room is useful because the list of room memberships can be maintained per-user and looked up across sessions and devices.

> 📘 Trying to count how many people are online in a chat room?
>
> Use the [User Presence service](doc:presence) to count how many people are online, show connection status indicators, and more.

A user does not have to be a member of a room to enter it and send messages.

## Member Limits

Rooms can have an optional member limit which controls the maximum number of members a room can have. Once that limit is reached, new members can't be added.
