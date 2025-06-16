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

## What blocking a profile does?

When Profile A blocks Profile B:

* Profile A doesn't not see any messages send by Profile B.
* Prevent Profile B from inviting Profile A to chat rooms.
* Prevent Profile B from adding Profile A to chat rooms. 

## Block a Profile

Use this method to block a user profile for the given `profileId`

```javascript
LiveLike.blockProfile({
    profileId: "<Profile ID>"
})
.then(blockInfo => console.log(blockInfo))
```

## Unblocking a Profile

Use this method to unblock profile using Block Info id for a given blocked profile, use `getProfileBlockInfo` or `getBlockInfoList` to get corresponding profile block info id

```javascript
LiveLike.unblockProfile({
    blockId: "<Block ID>"
 })
.then(response => console.log(response))
```

## Getting a List of Blocked Profile Info

Using this method you can get a list of all the profiles blocked by the current user.\
It returns a Promise that resolves in paginated list of Block Info objects.

```javascript
LiveLike.getBlockInfoList()
	.then(paginatedBlockInfo => console.log(paginatedBlockInfo))
```

## Getting a List of Blocked Profile Ids

Use this method to get a list of blocked profile ids, could be used to filter chat messages by blocked profile.

```javascript
LiveLike.getBlockedProfileIds().then(profileIds => console.log(profileIds))
```

## Getting blocked profile Info

Use this method to get block information for a particular profile Id.

```javascript
LiveLike.getProfileBlockInfo({
    profileId: "<Profile ID>"
})
.then(blockInfo => console.log(blockInfo))
```

## Block Profile Events

You can use [`addUserProfileEventListener`](https://docs.livelike.com/docs/javascript-user-profile#add-user-profile-event-listener) and [`removeUserProfileEventListener`](https://docs.livelike.com/docs/javascript-user-profile#remove-user-profile-event-listener) to attach and remove listener function for block profile events respectively. This events are exposed as part of `UserProfileEvent` from javascript package

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Event Name
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        BLOCK\_PROFILE
      </td>

      <td>
        Triggered when a given profile is blocked
      </td>
    </tr>

    <tr>
      <td>
        UNBLOCK\_PROFILE
      </td>

      <td>
        Triggered when a given profile is unblocked
      </td>
    </tr>
  </tbody>
</Table>

```javascript
import { addUserProfileEventListener, UserProfileEvent } from '@livelike/javascript'

function onUserProfileBlockCb(event){
  // process block event
}
addUserProfileEventListener(UserProfileEvent.BLOCK_PROFILE, onUserProfileBlockCb)
```

##
