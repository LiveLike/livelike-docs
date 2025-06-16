---
title: User Profile
excerpt: Extending your user data with LiveLike profiles
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: To read more about User Profiles, go to the main Profiles section
  pages:
    - type: basic
      slug: user-profiles
      title: Profiles
    - type: basic
      slug: javascript-user-profile-integration
      title: User Profile Integration
    - type: basic
      slug: javascript-blocking-profiles
      title: User Profile Moderation
---
Profiles are used to collect activity in chat, widgets, and other features inside a single identity. Profiles can be provisioned arbitrarily and can be used to extend your existing user account records. These profiles can either be local, allowing you to create anonymous experiences, or persisted in your user databases, allowing you to create profiles that persist across a user's devices.

When a profile is first created it is given a unique ID and a credential called an Access Token. It is also automatically given a nickname if one is not provided. Profiles will persist for as long as its credentials are stored and passed back to the SDKs & APIs. Nicknames are used for personalization, and show up next to chat messages and in leaderboards.

> 🚧 Nicknames are not unique!
>
> The profile ID and access token are the identifying fields of a profile. Nicknames are not guaranteed to be unique and can often be freely updated by users.

## Updating a Profile

To modify an existing user profile, use the `LiveLike.updateUserProfile` method. Providing a `nickname` property in the options argument will update the name shown for future chat messages sent by that profile.

```javascript
import { updateUserProfile } from '@livelike/javascript'

const updatedProfile = await updateUserProfile({
  accessToken,
  options: {
    nickname: 'New Nickname'
  }
})
```

The `updateProfile` function will return a promise which resolves the updated user profile object. This profile object does not contain the access token, so it is important to save it before running this function.

## Creating a New Profile

You can create a profile manually at any time using `LiveLike.createUserProfile`. Even if the SDK has already been initialised, a new profile will be returned.

```javascript
import { createUserProfile } from '@livelike/javascript'

const newProfile = await createUserProfile({ nickname: 'New Nickname' })
```

## Get User Profile

Use this method to get a User Profile using the `profileId` or `AccessToken` as a parameter

```javascript
import { createUserProfile } from '@livelike/javascript'

// get user profile using access token
const profile = await getUserProfile({ accessToken })

// get user profile using profileId
const profile = await getUserProfile({ profileId })
```

## Add User Profile Event Listener

Use this method to add event listener for a given UserProfileEvent.\
UserProfileEvent could be:

1. BLOCK\_PROFILE
2. UNBLOCK\_PROFILE

```javascript
import { addUserProfileEventListener, UserProfileEvent } from '@livelike/javascript'

function onUserProfileBlockCb(event){
  // process block event
}
addUserProfileEventListener(UserProfileEvent.BLOCK_PROFILE, onUserProfileBlockCb)
```

## Remove User Profile Event Listener

Remove a attached listenerFn for the given UserProfileEvent, when no listener passed, all registered event listener will be removed.

```javascript
import { removeUserProfileEventListener, UserProfileEvent } from '@livelike/javascript'

function onUserProfileBlockCb(event){
  // process block event
}
removeUserProfileEventListener(UserProfileEvent.BLOCK_PROFILE, onUserProfileBlockCb)
```
