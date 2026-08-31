---
title: iOS SDK 2.23.1
author: Mike M
hidden: false
published_at: '2021-05-21T17:37:56.672Z'
---
## What's New?

With this release we added an ability for integrators to add custom data to the user profile. This custom data can later be shared across all platforms per user profile.

```swift
let sdk = EngagementSDK

sdk.setUserCustomData(data: "< data >") { result in
	switch result {
    case .success(()):
      // handle success
    case .failure(let error):
    	// handle error
}
```