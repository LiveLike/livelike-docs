---
title: User Profiles
excerpt: Extending your user data with LiveLike profiles
deprecated: false
hidden: false
metadata:
  robots: index
---
Profiles are used to collect activity in chat, widgets, and other features inside a single identity. Profiles can be provisioned arbitrarily and can be used to extend your existing user account records. These profiles can either be local, allowing you to create anonymous experiences, or persisted in your user databases, allowing you to create profiles that persist across a user's devices.

When a profile is first created it is given a unique ID and a credential called an _<Glossary>Access Token</Glossary>_. It is also automatically given a nickname if one is not provided. Profiles will persist for as long as its credentials are stored and passed back to the SDKs & APIs. Nicknames are used for personalization, and show up next to chat messages and in leaderboards.

> 🚧 Nicknames are not unique!
>
> The profile ID and access token are the identifying fields of a profile. Nicknames are not guaranteed to be unique and can often be freely updated by users.

## Updating a Profile

```javascript
const updatedProfile = await LiveLike.updateUserProfile({
  accessToken,
  options: {
    nickname: 'New Nickname'
  }
})
```
```kotlin
sdk.updateChatNickname(nickname)
sdk.updateUserCustomData(<jsonString>,object:LiveLikeCallback<LiveLikeUserApi>(){
	override fun onResponse(result: LiveLikeUserApi?, error: String?) { 
  		
  })
})
```
```swift
sdk.setUserDisplayName("<new display name>") { [weak self] result in
      guard let self = self else { return }
      switch result {
      case .success:
          print("Successfuly changed user display name")
      case let .failure(error):
          print("Error \(error.localizedDescription)")
      }
   }
 }
```

> 📘 Looking for chat avatar images?
>
> Avatars are handled as part of the chat system. Read more in the [Chat Avatars](doc:chat-avatar) section.

## Local Profiles

Anonymous experiences can be created by persisting credentials in volatile storage, like a session store. These profiles will persist for the lifetime of the store. For example on mobile devices, you can store the profile in local storage. The profile can be reused, as long as the user doesn't clear local storage or reinstall the application.

<Image alt={671} border={false} caption="Workflow for storing profile access tokens locally" title="Local Profiles (1).png" src="https://files.readme.io/446c86d-Local_Profiles_1.png" />

## Persistent Profiles

Profiles can also be tied to your own user accounts. The user <Glossary>Access Token</Glossary> can be stored as a field in your user database. That allows you to re-use the same access token when a user reinstalls an app or signs in on another device. To understand how to tie profiles to your user accounts, see [Integrating with Logins](doc:using-profiles-with-logins). --- edit link

> ❗️ **Track your profiles carefully**
>
> Each new profile created in LiveLike counts as a unique user. If you are on metered MAU billing, creating unnecessary profiles may increase costs.
> To avoid this:
>
> * Reuse the same LiveLike profile for each of your app users.
> * Ensure that every user in your system has only one LiveLike profile associated with them.
> * Do not create new profiles arbitrarily on every SDK initialization.

<br />