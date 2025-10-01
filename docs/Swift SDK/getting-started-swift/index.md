---
title: Swift SDK
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
2. macOS 10\_12
3. tvOS 10
4. watchOS 3

## Installation

## Swift Package Manager (Recommended)

1. Open your project inside of Xcode and navigate to File > Add Packages...
2. Search for `git@bitbucket.org:livelike/livelike-ios-sdk.git` and select the `livelike-ios-sdk` swift package 
3. Use the Up to Next Major Version dependency rule spanning from 2.0.0 \< 3.0.0, and hit the Add Package button

## CocoaPods

[https://guides.cocoapods.org/using/using-cocoapods.html](https://guides.cocoapods.org/using/using-cocoapods.html)

Add the following to a Podfile:

```text Podfile
target '<application-target-name>' do 
  use_frameworks! 
  pod 'LiveLikeSwift' 
end
```

## Initialization

The LiveLike object is the access point for all features. To create a LiveLike object you will need:

* A [Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id)
* An Access Token

If your billing is determined by *Monthly Active Users (MAUs)*, then at this point it is important to consider how and when LiveLikeSwift will be initialized. We recommend creating the LiveLike object *as late as possible* for the most accurate usage metrics.

By default, LiveLikeSwift will generate a new [User Profile](doc:user-profiles) upon first initialization and store. it locally. For profile persistence, we recommend that you override where the user's access token is read and written using the `AccessTokenStorage` protocol.

```swift
import LiveLikeSwift

class Initialization {

    private var livelike: LiveLike?

    init() {
        var config = LiveLikeConfig(clientID: "my-client-id")
        config.accessTokenStorage = self
        self.livelike = LiveLike(config: config)
    }
}

extension Initialization: AccessTokenStorage {
    func fetchAccessToken() -> String? {
        return "user-access-token"
    }
    
    func storeAccessToken(accessToken: String) { }
}
```