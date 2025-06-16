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
Providing a custom access token will allow user data to be retrieved across app installs and multiple platforms.
To provide a custom access token you will have to supply a class that conforms to the `AccessTokenStorage` protocol. As a result you will be providing a way for the EngagementSDK to retrieve and store an access token. 
[block:callout]
{
  "type": "info",
  "body": "You cannot set the access token outside of this initializer. If you need to change or remove an access token you should reinitialize the EngagementSDK."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class SampleClass {\n    private func setupEngagementSDK(clientID: \"<client-id>\") {\n        var sdkConfig = EngagementSDKConfig(clientID: clientID)\n        sdkConfig.accessTokenStorage = self\n        let sdk = EngagementSDK(config: sdkConfig)\n    }\n}\n\nextension SampleClass: AccessTokenStorage {\n    func fetchAccessToken() -> String? {\n         return \"<access token>\"\n    }\n    \n    func storeAccessToken(accessToken: String) {\n        // store access token\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]
## Updating User Display Name

To update user's display name, create an instance of EngagementSDK and call the following.
[block:code]
{
  "codes": [
    {
      "code": "var sdk: EngagementSDK!\n\nsdk.setUserDisplayName(newNickname) { [weak self] in\n      guard let self = self else { return }\n      if case let .failure(error) = $0 {\n          print(\"User Display Name set has failed\")\n      }\n  }",
      "language": "swift"
    }
  ]
}
[/block]