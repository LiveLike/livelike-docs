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
[block:callout]
{
  "type": "warning",
  "title": "Nicknames are not unique!",
  "body": "The profile ID and access token are the identifying fields of a profile. Nicknames are not guaranteed to be unique and can often be freely updated by users."
}
[/block]

[block:api-header]
{
  "title": "Updating a Profile"
}
[/block]
To modify an existing user profile, use the `LiveLike.updateUserProfile` method. Providing a `nickname` property in the options argument will update the name shown for future chat messages sent by that profile.
[block:code]
{
  "codes": [
    {
      "code": "import { updateUserProfile } from '@livelike/javascript'\n\nconst updatedProfile = await updateUserProfile({\n  accessToken,\n  options: {\n    nickname: 'New Nickname'\n  }\n})",
      "language": "javascript"
    }
  ]
}
[/block]
The `updateProfile` function will return a promise which resolves the updated user profile object. This profile object does not contain the access token, so it is important to save it before running this function.
[block:api-header]
{
  "title": "Creating a New Profile"
}
[/block]
You can create a profile manually at any time using `LiveLike.createUserProfile`. Even if the SDK has already been initialised, a new profile will be returned.
[block:code]
{
  "codes": [
    {
      "code": "import { createUserProfile } from '@livelike/javascript'\n\nconst newProfile = await createUserProfile({ nickname: 'New Nickname' })",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get User Profile"
}
[/block]
Use this method to get a User Profile using the `profileId` or `AccessToken` as a parameter
[block:code]
{
  "codes": [
    {
      "code": "import { createUserProfile } from '@livelike/javascript'\n\n// get user profile using access token\nconst profile = await getUserProfile({ accessToken })\n\n// get user profile using profileId\nconst profile = await getUserProfile({ profileId })",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Add User Profile Event Listener"
}
[/block]
Use this method to add event listener for a given UserProfileEvent.
UserProfileEvent could be:
1. BLOCK_PROFILE
2. UNBLOCK_PROFILE
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
  "title": "Remove User Profile Event Listener"
}
[/block]
Remove a attached listenerFn for the given UserProfileEvent, when no listener passed, all registered event listener will be removed.
[block:code]
{
  "codes": [
    {
      "code": "import { removeUserProfileEventListener, UserProfileEvent } from '@livelike/javascript'\n\nfunction onUserProfileBlockCb(event){\n  // process block event\n}\nremoveUserProfileEventListener(UserProfileEvent.BLOCK_PROFILE, onUserProfileBlockCb)",
      "language": "javascript"
    }
  ]
}
[/block]