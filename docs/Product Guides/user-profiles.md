---
title: Profiles
excerpt: Extending your user data with LiveLike profiles
deprecated: false
hidden: false
metadata:
  title: Profiles | LiveLike Developer Hub | Engagement SDK
  description: >-
    Profiles are used to collect activity in chat, widgets, and other features
    inside a single identity. Learn how to update local and persistent profiles.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: using-profiles-with-logins
      title: Integrating with Logins
    - type: link
      title: User Profile Integration on iOS
      url: https://docs.livelike.com/docs/ios-user-profiles
    - type: link
      title: User Profile Integration on Web
      url: https://docs.livelike.com/docs/web-user-profile-integration
    - type: basic
      slug: chat-avatar
      title: Chat Avatars
---
Profiles are used to collect activity in chat, widgets, and other features inside a single identity. Profiles can be provisioned arbitrarily and can be used to extend your existing user account records. These profiles can either be local, allowing you to create anonymous experiences, or persisted in your user databases, allowing you to create profiles that persist across a user's devices.

When a profile is first created it is given a unique ID and a credential called an *<<glossary:Access Token>>*. It is also automatically given a nickname if one is not provided. Profiles will persist for as long as its credentials are stored and passed back to the SDKs & APIs. Nicknames are used for personalization, and show up next to chat messages and in leaderboards.
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

[block:code]
{
  "codes": [
    {
      "code": "const updatedProfile = await LiveLike.updateUserProfile({\n  accessToken,\n  options: {\n    nickname: 'New Nickname'\n  }\n})",
      "language": "javascript"
    },
    {
      "code": "sdk.updateChatNickname(nickname)\nsdk.updateUserCustomData(<jsonString>,object:LiveLikeCallback<LiveLikeUserApi>(){\n\toverride fun onResponse(result: LiveLikeUserApi?, error: String?) { \n  \t\t\n  })\n})",
      "language": "kotlin"
    },
    {
      "code": "sdk.setUserDisplayName(\"<new display name>\") { [weak self] result in\n      guard let self = self else { return }\n      switch result {\n      case .success:\n          print(\"Successfuly changed user display name\")\n      case let .failure(error):\n          print(\"Error \\(error.localizedDescription)\")\n      }\n   }\n }",
      "language": "swift"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Looking for chat avatar images?",
  "body": "Avatars are handled as part of the chat system. Read more in the [Chat Avatars](doc:chat-avatar) section."
}
[/block]

[block:api-header]
{
  "title": "Local Profiles"
}
[/block]
Anonymous experiences can be created by persisting credentials in volatile storage, like a session store. These profiles will persist for the lifetime of the store. For example on mobile devices, you can store the profile in local storage. The profile can be reused, as long as the user doesn't clear local storage or reinstall the application.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/446c86d-Local_Profiles_1.png",
        "Local Profiles (1).png",
        671,
        389,
        "#f3f3f3"
      ],
      "caption": "Workflow for storing profile access tokens locally"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Persistent Profiles"
}
[/block]
Profiles can also be tied to your own user accounts. The user <<glossary:Access Token>> can be stored as a field in your user database. That allows you to re-use the same access token when a user reinstalls an app or signs in on another device. To understand how to tie profiles to your user accounts, see [Integrating with Logins](doc:using-profiles-with-logins).
[block:callout]
{
  "type": "danger",
  "title": "Track your profiles!",
  "body": "While you can initialize the SDKs and create profiles arbitrarily, each new profile counts as a LiveLike user. If you are using metered MAU billing, it is important that your integration does not generate more profiles than it needs. If you want to keep your profile count in line with your own user count, ensure that each user in your system has only one LiveLike profile associated with them, and that they use the same profile each time they use your app."
}
[/block]