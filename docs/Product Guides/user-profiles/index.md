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
  pages:
    - slug: using-profiles-with-logins
      title: Integrating with Logins
      type: basic
    - slug: chat-avatar
      title: Chat Avatars
      type: basic
---
Profiles are used to collect fan activity on LiveLike inside a single identity. Integrations should associate each of their users with a profile.

## Identifiers

Each profile has an ID an an optional _custom ID_. The ID is assigned by LiveLike, but you can assign your own custom IDs. If you want to reuse user IDs from your system, store them in [Custom Profile IDs](doc:custom-profile-ids).

## Authenticating

Interactions with the LiveLike service are authenticated with an _<Glossary>Access Token</Glossary>_. You can generate your own access tokens from your backend with [Client-generated Access Tokens](doc:client-generated-access-tokens), or you can store the access tokens that are generated when creating a new profile.

## Personalizing and customizing

Nicknames are used for personalization, and show up next to chat messages and in leaderboards. If you have a username or display name in your system, you should use it as the profile's nickname.

<Callout icon="🚧" theme="warn">
  Nicknames are not guaranteed to be unique and can often be freely updated by users.
</Callout>

## Creating a profile

A new profile will be created when initializing the SDKs without an access token.

```javascript
const newProfile = await LiveLike.init({ accessToken })
```

<br />

Profiles can also be explicitly created.

```javascript
const newProfile = await LiveLike.createUserProfile({ nickname: 'New Nickname' })
// the access token is in profile.access_token
```

<br />

## Updating a profile

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

## Integration strategies

Generally integrations should associate each of their users with a LiveLike profile. In that case, using a persistent strategy is the recommended approach. If your integration doesn't have a user concept, or each session should be considered an independent user, the local strategy can work. 

> 🚧 Track your profiles!
>
> While you can initialize the SDKs and create profiles arbitrarily, each new profile counts as a LiveLike user. If you are using metered MAU billing, it is important that your integration does not generate more profiles than it needs. If you want to keep your profile count in line with your own user count, ensure that each user in your system has only one LiveLike profile associated with them, and that they use the same profile each time they use your app.

### Persistent profiles

Profiles should be associated with your own user accounts if you have them. The user <Glossary>Access Token</Glossary> can be stored as a field in your user database. That allows you to re-use the same access token when a user reinstalls an app or signs in on another device. To understand how to tie profiles to your user accounts, see [Integrating with Logins](doc:using-profiles-with-logins).

If you have an access token, you can initialize the SDK with it to reuse the same profile across sessions.

```swift
// You cannot set the access token outside of this initializer.
// If you need to change or remove an access token you should reinitialize the EngagementSDK.

class SampleClass {
    private func setupEngagementSDK(clientID: "<client-id>") {
        var sdkConfig = EngagementSDKConfig(clientID: clientID)
        sdkConfig.accessTokenStorage = self
        let sdk = EngagementSDK(config: sdkConfig)
    }
}

extension SampleClass: AccessTokenStorage {
    func fetchAccessToken() -> String? {
         return "<access token>"
    }
    
    func storeAccessToken(accessToken: String) {
        // store access token
    }
}
```
```javascript
const profile = await LiveLike.init({
  clientId,
  accessToken
});
```

### Local profiles

Anonymous experiences can be created by persisting credentials in volatile storage, like a session store. These profiles will persist for the lifetime of the store. For example on mobile devices, you can store the profile in local storage. The profile can be reused, as long as the user doesn't clear local storage or reinstall the application.

<Image alt={671} border={false} caption="Workflow for storing profile access tokens locally" title="Local Profiles (1).png" src="https://files.readme.io/446c86d-Local_Profiles_1.png" />
