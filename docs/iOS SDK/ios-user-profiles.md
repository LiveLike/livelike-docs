---
title: User Profiles
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: User Profiles | iOS SDK | LiveLike Developer Hub
  description: >-
    A User Profile represents the preferences and activities of a user of the
    product. Learn more about activity history and profile data.
  robots: index
next:
  description: ''
---
A User Profile represents the preferences and activities of a user of the product. This is where activity history and profile data such as usernames are stored. In the future, gamification rewards such as points & badges will also be stored here. See [Profiles](doc:user-profiles) to learn more.

As an integrator you can choose to provide a custom access token or simply rely on the SDK to handle access token management behind the scenes. 

For apps that do not have a concept of user accounts and rely on the SDK to handle access token management behind the scenes. User data will be accessible for the lifetime of the application, but will be lost when the app is reinstalled and the access token is lost. 

## Providing a Custom Access Token

Providing a custom access token will allow user data to be retrieved across app installs and multiple platforms.\
To provide a custom access token you will have to supply a class that conforms to the `AccessTokenStorage` protocol. As a result you will be providing a way for the EngagementSDK to retrieve and store an access token. 

> 📘 You cannot set the access token outside of this initializer. If you need to change or remove an access token you should reinitialize the EngagementSDK.

```swift
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

## Updating User Display Name

To update user's display name, create an instance of EngagementSDK and call the following.

```swift
var sdk: EngagementSDK!

sdk.setUserDisplayName(newNickname) { [weak self] in
      guard let self = self else { return }
      if case let .failure(error) = $0 {
          print("User Display Name set has failed")
      }
  }
```
