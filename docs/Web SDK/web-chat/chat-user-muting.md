---
title: Chat User Muting
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat User Muting | Web SDK | LiveLike Developer Hub
  description: >-
    Using the LiveLike Engagement SDK, producers have the ability to mute users
    in a chat, disabling their ability to send messages.
  robots: index
next:
  description: ''
---
Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in. As an integrator you have the ability to query our backend to find out whether a user is muted or not. This can be achieved using the `getChatUserMutedStatus` function.
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getChatUserMutedStatus({roomId: \"<Chat Room ID>\"}).then(muted_status => console.log(muted_status))",
      "language": "javascript"
    }
  ]
}
[/block]
Whether you decide to make the user aware of their status or not, the SDK will show an alert to a muted user once they try to send a message in a room. For more information about chat moderation please see the  [Chat Moderation](https://docs.livelike.com/docs/chat#moderation) page.