---
title: User Profile Moderation
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
      slug: javascript-chat
      title: Chat
    - type: basic
      slug: javascript-reactions
      title: Reactions
---
Sometimes users are not comfortable, or are being harassed by another user. In order to help users to keep themselves safe, they can block others from engaging with them in certain ways.
[block:api-header]
{
  "title": "What blocking a profile does?"
}
[/block]
When Profile A blocks Profile B:
* Profile A doesn't not see any messages send by Profile B.
* Prevent Profile B from inviting Profile A to chat rooms.
* Prevent Profile B from adding Profile A to chat rooms. 
[block:api-header]
{
  "title": "Block a Profile"
}
[/block]
Use this method to block a user profile for the given `profileId`
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.blockProfile({\n    profileId: \"<Profile ID>\"\n})\n.then(blockInfo => console.log(blockInfo))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Unblocking a Profile"
}
[/block]
Use this method to unblock profile using Block Info id for a given blocked profile, use `getProfileBlockInfo` or `getBlockInfoList` to get corresponding profile block info id
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.unblockProfile({\n    blockId: \"<Block ID>\"\n })\n.then(response => console.log(response))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting a List of Blocked Profile Info"
}
[/block]
Using this method you can get a list of all the profiles blocked by the current user.
It returns a Promise that resolves in paginated list of Block Info objects.
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getBlockInfoList()\n\t.then(paginatedBlockInfo => console.log(paginatedBlockInfo))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting a List of Blocked Profile Ids"
}
[/block]
Use this method to get a list of blocked profile ids, could be used to filter chat messages by blocked profile.
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getBlockedProfileIds().then(profileIds => console.log(profileIds))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting blocked profile Info"
}
[/block]
Use this method to get block information for a particular profile Id.
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getProfileBlockInfo({\n    profileId: \"<Profile ID>\"\n})\n.then(blockInfo => console.log(blockInfo))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Block Profile Events"
}
[/block]
You can use [`addUserProfileEventListener`](https://docs.livelike.com/docs/javascript-user-profile#add-user-profile-event-listener) and [`removeUserProfileEventListener`](https://docs.livelike.com/docs/javascript-user-profile#remove-user-profile-event-listener) to attach and remove listener function for block profile events respectively. This events are exposed as part of `UserProfileEvent` from javascript package
[block:parameters]
{
  "data": {
    "h-0": "Event Name",
    "h-1": "Description",
    "h-2": "",
    "0-0": "BLOCK_PROFILE",
    "0-1": "Triggered when a given profile is blocked",
    "0-2": "",
    "1-0": "UNBLOCK_PROFILE",
    "1-1": "Triggered when a given profile is unblocked"
  },
  "cols": 2,
  "rows": 2
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import { addUserProfileEventListener, UserProfileEvent } from '@livelike/javascript'\n\nfunction onUserProfileBlockCb(event){\n  // process block event\n}\naddUserProfileEventListener(UserProfileEvent.BLOCK_PROFILE, onUserProfileBlockCb)",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": ""
}
[/block]