---
title: Getting Started with LiveLikeSwift
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This is the developer's guide to getting started with LiveLikeSwift. We will walk you through the installation and initialization steps. First, make sure that you are using a supported OS version(s):

1. iOS 10
2. macOS 10_12
3. tvOS 10
4. watchOS 3
[block:api-header]
{
  "title": "Installation"
}
[/block]
## Swift Package Manager (Recommended)

1. Open your project inside of Xcode and navigate to File > Add Packages...
2. Search for `git@bitbucket.org:livelike/livelike-ios-sdk.git` and select the `livelike-ios-sdk` swift package 
3. Use the Up to Next Major Version dependency rule spanning from 2.0.0 < 3.0.0, and hit the Add Package button

##  CocoaPods

https://guides.cocoapods.org/using/using-cocoapods.html

Add the following to a Podfile:
[block:code]
{
  "codes": [
    {
      "code": "target '<application-target-name>' do \n  use_frameworks! \n  pod 'LiveLikeSwift' \nend",
      "language": "text",
      "name": "Podfile"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Initialization"
}
[/block]
The LiveLike object is the access point for all features. To create a LiveLike object you will need:

* A [Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id)
* An Access Token

If your billing is determined by *Monthly Active Users (MAUs)*, then at this point it is important to consider how and when LiveLikeSwift will be initialized. We recommend creating the LiveLike object _as late as possible_ for the most accurate usage metrics.

By default, LiveLikeSwift will generate a new [User Profile](doc:user-profiles) upon first initialization and store. it locally. For profile persistence, we recommend that you override where the user's access token is read and written using the `AccessTokenStorage` protocol.
[block:code]
{
  "codes": [
    {
      "code": "import LiveLikeSwift\n\nclass Initialization {\n\n    private var livelike: LiveLike?\n\n    init() {\n        var config = LiveLikeConfig(clientID: \"my-client-id\")\n        config.accessTokenStorage = self\n        self.livelike = LiveLike(config: config)\n    }\n}\n\nextension Initialization: AccessTokenStorage {\n    func fetchAccessToken() -> String? {\n        return \"user-access-token\"\n    }\n    \n    func storeAccessToken(accessToken: String) { }\n}",
      "language": "swift"
    }
  ]
}
[/block]